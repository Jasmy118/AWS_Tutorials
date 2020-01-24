# Step 1: Create VPC in AWS
- Search VPC. Click VPC - Create VPC (Jas_VPC_1, 10.0.0.0/16, No IPv6 CIDR Block, Tenancy-Default) - Create.
# Step 2: Create Subnet
- Select Subnet - Create Subnet(J_Subnet_1, Jas_VPC_1, any zone, 10.0.1.0/24) - Create. 
- Note: Available IPv4:251
    - 10.0.1.0 : Network address
    - 10.0.1.1 : Reserved by AWS for the VPC router
    - 10.0.1.2 : Reserved by AWS for mapping to Amazon provided DNS
    - 10.0.1.3 : Reserved by AWS for future use
    - 10.0.1.255 : Network broadcast address
# Step 3: Create Internet Gateway
- Select Internet Gateway - Create internet gateway(J_IGW_1) - Create. Select J_IGW_1. Actions - Attach to VPC(Jas_VPC_1) - Attach.
- Note : For one VPC, one internet gateway
# Step 4: Make subnet PUBLIC
- Select Subnets - Select J_Subnet_1 - Route Table(below).See Destination and target, if not associated with an IGW, this subnet is private. Click on the Route Table ID(the blue link with rtb id). Select Routes(below) - Edit Routes - Add route(Dest : 0.0.0.0/0, Target: igw - J_IGW_1) - Save routes. GoTo Subnets - Select subnet - Route Table(below)(Destination can be seen). Now this subnet is public because it is associated with an IGW.
- Note:
    - Destination : 0.0.0.0/0 - means everywhere around the world.
    - A subnet can have only 1 route table. A route table can have multiple subnets associated.
# Step 5: Creating or launching a Instance
- Search EC2 - Select Instances - Click Launch Instance
  - Amazon Linux 2 AMI(Free tier eligible) - Select
  - Select Free Tier eligible - Next: Configure Instance Details
  - Select JAS_VPC_1, J_Subnet_1, Auto-assign Public IP:Use subnet setting(disable) - Next:Add Storage
  - Next:Add Tags - Add Tag: Name,J_EC2_1 - Next: Configure Security Group
  - Create new security group: Jas_SG - My first SG (firewall) - SSH - Anywhere
  - Review and Launch - Launch - Create a new key pair - JJ_KeyPair - Download. 
  - Launch Instances - View Instances.
- Note
  - Auto-assign Public IP:Use subnet setting(disable) - Will have to assign an elastic public IP to this instance.
  - Security Group SSH : 0.0.0.0/0, ::/0 - IPv6 equivalent of IPv4
# Step 6: Assigning Elastic IP Address for the instance (Public IP)
- Do this step if, Auto-assign Public IP: was disabled while creating instance.
- Select Elastic IP - Allocate Elastic IP address - Allocate. Select the EIP: Actions - Associate Elastic IP address(Instance, Private Ip)- Associate.
- Note: Now the instance will have a IPv4 public IP (34.206.42.82)
# Step 7: Ping test and Edit Security Group
- Ping 34.206.42.82 - Times out
- Reason : Firewall - Security Group
- Instance J_EC2_1 - Click Jas_SG - Inbound Rules - Edit - Add Rule(All ICMP - IPv4, Anywhere) - Save.
- Note: ICMP is the protocol for ping.
# Step 8: Test
- ping 34.206.42.82 - gets the reply.
# Step 9: Connect to the Instance
- Select instance J_EC2_1 - Connect.
- In cmdprompt, direct cmd to the path of the pem file -> 
    - ssh -i "JJ_KeyPair.pem" ec2-user@34.206.42.82
![image of instance connect](https://github.com/Jasmy118/scripturient/blob/Image/Instance%20Connect.JPG)
# Step 10: Stop instance and release elastic IP
