## Designing your own website and running it on a raspberry pi:
### What cybersecurity tools do you need to consider?
Low cost software and hardware creates the opportunity to bring empowering technology to people with low-budget. In this project I hope the people  learn to install an operating system and the software needed to design a website using a raspberry pi. Prototyped source code to design the website will be tested in advance to be re-used during the session. The structure of the code will be modular and flexible to incorporate people ideas.

We expect that the audience take this exercise as a initial step to think about how to create secure websites and which tools exist to prevent hacks.  After having an introduction to the vulnerabilities of  websites we could discuss how sites with sensitive data protect themselves in the cyberspace.

### Project tools: Python v3, Flask and MYSQL


### Raspberry Pi project
Raspberry Pi  is a small and affordable computer that you can use to learn programming. \
https://www.raspberrypi.org/

### Flask project 
Flask is a Python web framework built with a small core and easy-to-extend philosophy. \
http://flask.pocoo.org/

#### Tutorial to create a webserver with Flask, code explained step by step: 
https://www.youtube.com/watch?v=zRwy8gtgJ1A

#### Visit this Github repository to download the code for the Flask application: 
Developer site: https://github.com/bradtraversy/myflaskapp \
Code edited: https://github.com/cihernand/myflaskapp

``` console
sudo apt-get install git
git clone https://github.com/cihernand/myflaskapp
```

#### Virtual enviroment explanation 
https://www.youtube.com/watch?v=N5vscPTWKOk

#### Installation requirements:

##### 1. You may need to install the Python and MySQL development headers and libraries like so: 

``` console
sudo apt-get install python3-dev 
sudo apt-get install  libmysqlclient-dev  mysql-server 
```

##### 2. Install Virtual Environment 
```sh
sudo apt install virtualenv 
Create Virtual Environment 
virtualenv   myapp  -p [insert path to python3] 
```

##### Activate Virtual Environment 

```sh
source myapp/bin/activate
```

###### Install Flask and MySQL python modules 

```sh
pip install Flask 
pip install mysql-python 
pip install mysqlclient 
pip install flask-mysqldb

```

###### Install Forms and Hashing passwords python modules 

```sh

pip install wtforms 
pip install passlib 
pip install --upgrade setuptools 
pip freeze > requirements.txt

```

## Commands to run the application

##### Access MySQL & create the database for the website 

```sh
mysqladmin -u root [insert password]
mysql -u [insert username] -p [insert password]
```
If the instructions above do not work  try:

``` sh
sudo mysql -u root

```

Change the plugin for user root from unix_socket into mysql_native_password:

``` mysql
SELECT User, Host, plugin FROM mysql.user;
UPDATE mysql.user SET plugin = 'mysql_native_password' WHERE user = 'root' AND plugin = 'unix_socket';
FLUSH PRIVILEGES;
```

Once you can login to MySQL create the Database myflaskapp with the following commands: 

```mysql

SHOW DATABASES;
CREATE DATABASE myflaskapp;
USE myflaskapp;
CREATE TABLE users( id INT(11) AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(100), email VARCHAR (100) ,username VARCHAR(30), password VARCHAR (100),
register_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP);

SHOW TABLES;
DESCRIBE users;

CREATE TABLE articles( id INT(11) AUTO_INCREMENT PRIMARY KEY,
title VARCHAR(255), author VARCHAR (100) , body TEXT,
create_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP);

SHOW TABLES;

```

##### Change Python Code app.py with your MySQL credentials

```python

app.config['MYSQL_HOST'] = 'localhost' 
app.config['MYSQL_USER'] = 'INSERT YOUR MYSQL USERNAME HERE' 
app.config['MYSQL_PASSWORD'] = 'INSERT YOUR MYSQL PASSWORD HERE'

```

##### Run Flask application 

```sh
python app.py 

```

##### Open your web-browser with the following URL
 http://127.0.0.1:5000/ 

##### SQL injections tutorial 
https://www.go4expert.com/articles/complete-mysql-injection-newbies-t20438/

### MOZFEST EXERCISE
#### TEST THE FOLLOWING QUERIES TO THE DATABASE  
##### What will be the output of the following MYSQL query?

```mysql
# SELECT DATABASE NAME
USE myflaskapp;

# GET MYSQL VERSION 
SELECT @@version;

# TEST EXAMPLE INJECTION INSIDE MYSQL
SELECT * from  users WHERE username='a' or 1=1; -- AND password=''
SELECT * from users  WHERE username='a' or 1=1;

```

##### How  can you insert a username using the webserver that executes the code from above?
[Hints:]

```sh
username:' or 1='1  password:' or 1='1
username:' or '1'='1'  password:' or '1'='1'
username:or 1=1  password:or 1=1

```

### MOZFEST SESSION CHALLENGES
Identify the flask modules that remove special characters from the MYSQL injection. \
Identify what do passlib and sha256_crypt do with the passwords from the users. \
Hack the site. 




