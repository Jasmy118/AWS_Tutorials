# Step 1
- Run Anaconda prompt as administrator. Activate test environment. Install pymysql.
  - conda activate test
  - conda install pymysql
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
# Step 4
- Display data from the table :
  - pd.read_sql('SELECT * FROM Planet', con=conn)
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
