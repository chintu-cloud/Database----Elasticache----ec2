<img width="1207" height="256" alt="DMS" src="https://github.com/user-attachments/assets/7e06d32c-c843-44fd-b6c4-96c5aa299ce3" />



# 📘 EC2 – RDS – ElastiCache (Redis) – Node.js Backend Setup

This project demonstrates how to:

* Create an **EC2 instance**
* Connect it with **Amazon RDS (MySQL)**
* Use **Amazon ElastiCache (Redis)** for caching
* Run a **Python cache layer**
* Deploy a **Node.js backend** connected to RDS
* Test APIs using **curl** and **Postman**

---

## 🧱 Architecture Overview

* **EC2 (Amazon Linux)** – Application server
* **RDS (MySQL / MariaDB)** – Persistent database
* **ElastiCache (Redis OSS)** – In-memory cache (TTL: 90 seconds)
* **Node.js Backend** – REST API
* **Python Script (`cache.py`)** – RDS + Redis cache demo

---

## 🚀 Step 1: Create EC2 Instance

1. Launch an **EC2 instance**

   * OS: **Amazon Linux**
2. Connect to the EC2 server using SSH

---

## 🗄️ Step 2: Create RDS Database

1. Create an **Amazon RDS (MySQL/MariaDB)** instance
2. Note down:

   * **RDS Endpoint**
   * **Username**
   * **Password**
   * **Port (3306)**

---

## ⚡ Step 3: Create ElastiCache (Redis)

1. Open **Amazon ElastiCache**
2. Click **Create cache**
3. Choose **Redis OSS**
4. Give a cache name and create it
5. Open the cache cluster
6. Copy the **Cache Endpoint**
   👉 *Remove the port number*

---

## 📦 Step 4: Install Dependencies on EC2

```bash
sudo yum install mariadb105-server -y
sudo yum install python3-pip -y
pip install pymysql redis
```

---

## 🔌 Step 5: Connect to RDS from EC2

```bash
mysql -h <rds-endpoint> -u admin -p<rds-password>
```

---

## 🧪 Step 6: Create Database and Table

```sql
CREATE DATABASE test;
USE test;

CREATE TABLE users (
    user_id VARCHAR(50) PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(100)
);
```

### Insert Sample Data

```sql
INSERT INTO users (user_id, first_name, last_name, email)
VALUES ('12345', 'John', 'Doe', 'john.doe@example.com');
```

---

## 🐍 Step 7: Create `cache.py`

1. Create the file:

```bash
vi cache.py
```

2. Paste the provided Python code
3. Update:

   * **RDS credentials** in RDS config section
   * **Redis endpoint** in Redis config section

---

## ▶️ Step 8: Run Cache Script

```bash
python3 cache.py
```

### Expected Behavior

* **First run** → Data fetched from **RDS**
* **Second run** → Data fetched from **Redis cache**
* Cache TTL = **90 seconds**
* New RDS records will appear **after cache expiry**

---

## 🌐 Step 9: Node.js Backend Setup

### Install Required Packages

```bash
sudo su -
yum install mariadb105-server -y
sudo dnf install -y nodejs
yum install git -y
```

### Clone Repository

```bash
git clone https://github.com/CloudTechDevOps/2nd10WeeksofCloudOps-main.git
cd 2nd10WeeksofCloudOps-main/
```

Remove unnecessary files if required.

---

## 📂 Backend Configuration

```bash
cd backend/
vi .env
```

Update `.env`:

```env
DB_HOST=<rds-endpoint>
DB_USERNAME=admin
DB_PASSWORD="chandan31234"
PORT=3306
```

---

## 📥 Install & Start Application

```bash
npm install
npm start
```

---

## 🗃️ Create Tables Using SQL File

```bash
mysql -h <rds-endpoint> -u admin -p<password> < test.sql
```

---

## 🔄 Run App with PM2

```bash
npm install -g pm2
pm2 start index.js --name node-app
```

---

## 🧪 API Testing Using Curl

### POST Request

```bash
curl -X POST http://localhost/books \
  -H "Content-Type: application/json" \
  -d '{
        "title": "chandan",
        "desc": "this is my backend to rds connection",
        "price": 24543.2,
        "cover": "https://docs.multy.dev/assets/images/multi-cloud-314609adeec670988dff0882a93fdcb0.png"
      }'
```

✔️ Data will be stored in **RDS**

---

## 📮 API Testing Using Postman

### GET Request

```http
GET http://<public-ip>/books
```

### Sample GET Output

```json
[
  {
    "id": 1,
    "title": "chandan",
    "desc": "this is my backend to rds connection",
    "price": 24543.2,
    "cover": "https://docs.multy.dev/assets/images/multi-cloud-314609adeec670988dff0882a93fdcb0.png"
  }
]
```

---

### POST Request in Postman

* Method: **POST**
* Body → **raw → JSON**

```json
{
  "title": "CloudOps",
  "desc": "Data added from Postman",
  "price": 1200,
  "cover": "https://example.com/image.png"
}
```

Click **Send** ✅
Data will be saved in RDS.

---

## ✅ Final Result

* EC2 successfully connected to RDS
* Redis cache working with TTL (90 seconds)
* Python cache layer tested
* Node.js backend running with PM2
* API tested using **curl** and **Postman**

---


```

-------------------------step1----------------------
create the ec2 with amzon Linux os server
then connect to the server
-- create rds database
 
----------------- creation of rds cache---------------
select the rds go to actions click on create cache cluster 
-- just give name and click on create it 
---search for elastic cahe and open it 
-------click on redies oss caches
------------open your cache and copy the cache endpoint with out port number 

---------------------install the dependencies-----------------
sudo yum install mariadb105-server -y 
sudo yum install python3-pip -y
pip install pymysql redis	 //dependencies for cache python file 

--------------connect to your rds database from server -------------

mysql -h <rdsendpoint> -u admin -p<rds-password>

------------------create a database and table with below configuration 
CREATE DATABASE test;

USE test;

CREATE TABLE users (
    user_id VARCHAR(50) PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(100)
);

--------------- Sample data for testing--------------------------------------------
INSERT INTO users (user_id, first_name, last_name, email)
VALUES ('12345', 'John', 'Doe', 'john.doe@example.com');

------------- create cache.py file ---------- 
# paste the  code 
# and change the rds credentials in Rds config section 
# and change elastic cache details in redis config section  according to your end--------
# this is code 

    vi cache.py  file inside code there 


--------------------------------------------------------------after that run the file by using pythin3 cache.py -----------------------------
python3 cache.py

------now  first time your cache fetch the records form rds directly 
---------run again now you will get the records from cache only 
--------------- your rds cache is is stored up to  90 sec 
--------- in this 90 sec if we add new records in rds it wont refeleect in cache because cache wont take new records form rds upto 90 sec 
----------after 90 sec cache fetch the what ever the new records added in the database it will be fetched  


 # after that we can create rds 




create rds 
-	create an ec2
-	connect to the ec2
-	sudo su -
-	yum install mariadb105-server
-	install node js
		sudo dnf install -y nodejs
-	install git 
		yum install git -y
-	git clone https://github.com/CloudTechDevOps/2nd10WeeksofCloudOps-main.git
-	cd 2nd10WeeksofCloudOps-main/
-	ls 
then remove the unnecessary file 
-	go to backend 
		cd backend/
-	go to vi.env file to set the correct configuration 
		DB_HOST= <database endpoint>
		DB_USERNAME=admin
		DB_PASSWORD="chandan31234"
		PORT=3306
-	npm install
-	npm start
-	run your test.sql through rds so that database and tables create 
		MySQL -h <rds-endpoint> -u admin -p<password> <test.sql
-	npm install -g pm2
-	pm2 start index.js --name node-app
-	run curl command

################################################

curl -X POST http://localhost/books \
  -H "Content-Type: application/json" \
  -d '{
        "title": "chandan",
        "desc": "this is my backend to rds connection",
        "price": 24543.2,
        "cover": "https://docs.multy.dev/assets/images/multi-cloud-314609adeec670988dff0882a93fdcb0.png"
      }'

connect to sql to see the data is available or not

#####################################################################################
inside postman 

get http://publicip/tablename


post

inside postman >> inside raw
  we can add data in raw option 

 ****  data are store inside postman file

   
//  all data are enter in raw option then 
      then send
```
