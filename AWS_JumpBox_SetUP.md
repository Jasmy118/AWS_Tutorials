# Step 1: Create VPC
  - Create a jumpbox VPC - VPC_JumpBox - 20.0.0.0/16
# Step 2: Create Subnet (Public)
  - Create a subnet - Public_Subnet_JB - 20.0.1.0/24
# Step 3: Create Internet Gateway and attach to VPC
  - Create an internet gateway - IGW_JumpBox
  - Attach IGW_JumpBox to VPC_JumpBox
# Step 4: Making the subnet in step 2 PUBLIC
  - Select Public_Subnet_JB - Select Route Table below - Click route table id - Select Routes(below) - Edit routes - Add Route(0.0.0.0/0, igw - of IGW_JumpBox)
  - Note: Now Public_Subnet_JB is a public subnet
# Step 5: Create Subnet (Private)
  - Create a subnet - Private_Subnet_JB - 20.0.2.0/24
# Step 6: Create NAT Instance (EC2 instance)
  - Select EC2 - Select Launch Instance.
    - Choose AMI : Community AMIs - Search amzn-ami-vpc-nat - Select ami-00a9d4a05375b2763.
    - Choose instance type : Select Free Tier
    - Configure Instance : Select VPC_JumpBox, Public_Subnet_JB, Auto-assign Public IP - Enable
    - Add Tags : Name-NAT_Instance_JB
    - Configure Security Group : Create new security group - NAT_SG, Security group for nat instance of jumpbox. Rule: SSH, custom - 0.0.0.0/0
    - Review and Launch : Proceed without a key pair - if you never need to connect to this instance (You can also create new key pair)
    - Launch : (Public IP: 54.147.99.213)
# Step 7: Creating JumpBox (EC2 instance)
  - Select EC2 - Select Launch Instance
    - Choose AMI : Amazon Linux 2 AMI (HVM) Free Tier eligible
    - Choose Instance Type : Free Tier eligible
    - Configure Instance : Select VPC_JumpBox, Public_Subnet_JB, Auto-assign Public IP - Enable
    - Add Tags : Name, JumpBox
    - Configure Security Group : Create new security group - SG_JumpBox, Security group for jumpbox. Rule: SSH, custom - 0.0.0.0/0
    - Review and Launch: Key pair : create a new key pair : JumpBox_Key
    - Launch : (Public IP : 54.82.202.80)
# Step 8: Creating private instance(FI) (EC2 instance)
  - Select EC2 - Select Launch Instance
    - Choose AMI : Amazon Linux 2 AMI (HVM) Free Tier eligible
    - Choose Instance Type : Free Tier eligible
    - Configure Instance : Select VPC_JumpBox, Private_Subnet_JB, Auto-assign Public IP - Disable
    - Add Tags : Name, FI_Private_Instance
    - Configure Security Group: Create new security group - SG_FI, Security group for private instance. Rule: SSH, custom - 0.0.0.0/0
    - Launch: Key pair: choose existing key pair(same as jumpbox) : JumpBox_Key
# Step 9: Create Route table
  - If we check the Private_Subnet_JB, it is using the route table of the public subnet. We need a separate route table for the private subnet. 
  - Select VPC - Route Tables - Create route table - Private_Sub_RT_JB - Create.
  - Select Private_Sub_RT_JB - Select Routes - Edit routes - Add route (0.0.0.0/0, i- select Nat instance - NAT_Instance_JB) - Save routes.
# Step 10: Associating private subnet to private route table
  - Select Subnets - Select Private_Subnet_JB - Routes - Edit route table association - Select Private_Sub_RT_JB - Save.
Note: eni - elastic network interface
# Step 11: Checking security group(inbound rules) of each instance
  - JumpBox - Inbound rules are correct(SSH-port 22-from any source)
  - FI_Private_Instance - Inbound rules(SSH-port 22-from any source). This is not correct. We need to add more security. We need to edit.
    - Select FI_Private_Instance - Click SG_FI in description. In Inbound tab - Edit. Edit existing rule - Custom - sg - select security group of JumpBox (NAT_SG).
  - Note : Now only the machines associated with jumpbox security group have access to the FI. So if jumpbox is not ON, FI is not accessible.
# Step 12: Connect to jumpbox.
  - $ ssh -i "JumpBox_Key.pem" ec2-user@54.82.202.80
    - Connects successfully.
# Step 13: Copy "JumpBox_Key.pem" file from local to remote (local to JB)
  - Copying this key pair so that it can be used to connect to FI from JB. Run the following commad from local machine (cmd prompt):
  - $ scp -i JumpBox_Key.pem JumpBox_Key.pem ec2-user@54.82.202.80:J_Key.pem
  - Connect to JumpBox now - $ ssh -i "JumpBox_Key.pem" ec2-user@54.82.202.80
  - $ ls --> J_Key.pem
# Step 13: Connect to FI from JumpBox now:
  - $ ssh -i "J_Key.pem" ec2-user@20.0.2.24
  - Connection denied due to permission issues.
  - To view permission:
    - $ ls -l
  - To change permission:
    - $ chmod 400 J_Key.pem
    - (View permission) $ ls -l
# Step 14: Ping google.com test from FI
  - Does not seem to work
  - Go To NAT_Instance_JB. Actions - Networking - Change Source/Dest Check - Disable.
  - Ping Google.com - Still does not work.
  - Select NAT_Instance_JB - Select NAT_SG - Inbound - Edit - All Traffic, Custom, sg - private instance SG.
    Now NAT instance allow all traffic to pass through but from FI.
  - $ ping google.com now works
