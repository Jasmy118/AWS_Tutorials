# Step 1
- Run Anaconda prompt as administrator. Activate test environment. Install pymysql.
  - conda activate test
  - conda install pymysql
![image1](https://github.com/Jasmy118/scripturient/blob/master/1%20install%20conda%20mysql.JPG)
![image2](https://github.com/Jasmy118/scripturient/blob/master/2%20install%20conda%20mysql.JPG)
# Step 2
- In Jupiter(Anaconda Test env) :
  - import pandas as pd
  - import pymysql
# Step 3
- Opening or creating the connection :
  - host="mydbinstance.c8xo2pfnll3f.us-east-1.rds.amazonaws.com" # endpoint
  - port=3306
  - dbname="MyDB_1" # Initial database name provided while creating RDS in AWS
  - user="admin"
  - password="admin1234"
  - conn = pymysql.connect(host, user=user,port=port, passwd=password, db=dbname)
![image4](https://github.com/Jasmy118/scripturient/blob/master/4%20RDS%20connected%20with%20python%20and%20workbench.JPG)
# Step 4
- Display data from the table :
  - pd.read_sql('SELECT * FROM Planet', con=conn)
![image3](https://github.com/Jasmy118/scripturient/blob/master/3%20Connect%20to%20RDS%20and%20retrieve%20data%20in%20python.JPG)
# Step 5
-Inserting data :
  - cursor = conn.cursor()
  - sql = "INSERT INTO Planet (idPlanet, PlanetName) VALUES (%s, %s)"
  - val = (4, "Mars")
  - cursor.execute(sql, val)
  - conn.commit()
# Step 6
- Displaying inserted data in python and MySQL Workbench :
  - pd.read_sql('SELECT * FROM Planet', con=conn)
![image5](https://github.com/Jasmy118/scripturient/blob/master/5%20RDS%20Connection%20Python.JPG)
![image6](https://github.com/Jasmy118/scripturient/blob/master/6%20Final%20Update.JPG)
# Step 7
- Delete RDS Instance
![image7](https://github.com/Jasmy118/scripturient/blob/master/7%20Delete%20Instance.JPG)
