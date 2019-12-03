# Step 1
In AWS, search RDS. Choose Create Database.
# Step 2
Choose a database creation method : Standard create.
# Step 3
Engine options : My SQL, 5.7.22
# Step 4
Templates : Free Tier
# Step 5
Settings:
  - DB Instance identifier - MyDBInstance
# Step 6
Credential setting:
  - Username : admin
  - Password : admin1234
# Step 7
Storage : Deactivate Enable storage Scaling
# Step 8
Connectivity :
  - VPC : Jas_VPC_1
  - VPC should have atleast 2 subnets in 2 different availability zones. If not create a subnet in a different zone.
  - Go to VPC -> Actions -> ( Edit DNS resolution, Edit DNS hostnames) -> Enable both.
Additional connectivity configuration :
  - Publicly acessible - yes
VPC Security Group :
  - Create new -> Name = J_RDS_SG -> Availability zone = No preference -> leave the same port(3306)
# Step 9
Database authentication :  password authentication
# Step 10
Additional configuration:
  - Initial database name - MyDB_1
  - BackUp - disable
  - Maintenance - leave it as it is
# Step 11
Create Database.

# Step 12 : Connecting through an interface (MySQL Workbench)
Open MySQL Workbench. Add MySQL Connections.
	- Connection name : JDb1
	- Hostame : mydbinstance.c8xo2pfnll3f.us-east-1.rds.amazonaws.com
	- Username: admin
	- Password: admin1234
	- Test Connection - OK
# Step 13
  - Double click on the new MySQLConnection.
  - View - panels- sidebar(if side bar is hidden)
# Result
