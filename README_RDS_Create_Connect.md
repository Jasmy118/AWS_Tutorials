# Step 1 : Create RDS (Db)
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
![image1](https://github.com/Jasmy118/scripturient/blob/master/1%20DB%20Created.JPG)
![image2](https://github.com/Jasmy118/scripturient/blob/master/2%20DB%20Created.JPG)
# Step 2 : Connecting through an interface (MySQL Workbench)
- Open MySQL Workbench. Add MySQL Connections.
	- Connection name : JDb1
	- Hostame : mydbinstance.c8xo2pfnll3f.us-east-1.rds.amazonaws.com
	- Username: admin
	- Password: admin1234
	- Test Connection - OK
![image3](https://github.com/Jasmy118/scripturient/blob/master/3%20Connection%20successful.JPG)
# Step 3
- Double click on the new MySQLConnection.
- View - panels- sidebar(if side bar is hidden)
# Result
![image4](https://github.com/Jasmy118/scripturient/blob/master/4%20DB.JPG)
# Step 4
- Create a table
- Insert data
- Display data
![image5](https://github.com/Jasmy118/scripturient/blob/master/5%20TableCreate_WorkBench.jpg)
![image6](https://github.com/Jasmy118/scripturient/blob/master/6%20TableInsertDataWorkbench.JPG)
![image7](https://github.com/Jasmy118/scripturient/blob/master/7%20Display%20DB%20data%20in%20workbench.JPG)
