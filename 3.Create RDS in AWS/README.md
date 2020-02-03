## Step 1 : Create RDS (Db)
- In AWS, search RDS. Choose Create Database.
- Choose a database creation method : Standard create.
- Engine options : My SQL, 5.7.22
- Templates : Free Tier
- Settings:
	- DB Instance identifier -> MyDBInstance
- Credential setting:
	- Username : admin
	- Password : admin1234
- Storage : Deactivate Enable storage Scaling
- Connectivity :
	- VPC : Jas_VPC_1
	- VPC should have atleast 2 subnets in 2 different availability zones. If not create a subnet in a different zone.
	- Go to VPC -> Actions -> ( Edit DNS resolution, Edit DNS hostnames) : Enable both.
- Additional connectivity configuration :
	- Publicly acessible - yes
- VPC Security Group :
	- Create new -> Name = J_RDS_SG -> Availability zone = No preference -> leave the same port(3306)
- Database authentication :  password authentication
- Additional configuration:
	- Initial database name - MyDB_1
	- BackUp - disable
	- Maintenance - leave it as it is
- Create Database.
![image1](https://github.com/Jasmy118/scripturient/blob/Image/1%20DB%20Created.JPG)
![image2](https://github.com/Jasmy118/scripturient/blob/Image/2%20DB%20Created.JPG)
