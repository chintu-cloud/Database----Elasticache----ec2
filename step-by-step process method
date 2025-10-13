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

   
//  all data are enter in raw option then send
