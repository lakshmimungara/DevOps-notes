Day-6 session-6(19/08/2024)
------------------------------

Recap:
------
User management 
1. creating user
2. Enabling password-based authentication
3. Enabling key-based authentication
4. Primary and secondary groups

Package management
yum --> dnf
dnf install
dnf list installed

service management
1. start the service 
2. stop the service
3. service status
4. enabling the status 
5. Disbaling the status 

systemctl status sshd

Process management
1. ps -ef | grep nginx 
2. foreground
3. Background

Network management
1. netstat -lntp 

===============================================
Project: - Introduction
--------
-> Previously, few years back we have desktop applications 
-> Now, it is all about web-based applications

Disadvantages of desktop applications:
---------------------------------------
1. we have to install 
2. we have to maintain storage
3. we h ave to upgrade
4. Fixing the problems
5. Only in single system 
7. What if system crash --> everything erases 
8. system resourses 

Because of these disadvantages, people moved to Web-based applications 

Web-based applications:
------------------------
1. No installations 
2. No upgrade
3. No compatibility issues 
4. No storage issues 
5. You can open everywhere 

-> Web-based applications are fully flexiable. so, everyone moved to web-based applications 
-> We follow 3-tier architecture 

for example:
------------
Road side cart
---------------
-> Only one person takes care of everything like cooking, billing, serving, etc
-> At a time he can manage 10 members/persons 
-> he cannot manage everyone at a time 

what if the business gets popular?
-----------------------------------
-> He hires someone 
-> The owner has to focus on product taste and quality 
-> He divides the remainings to others like billing, serving

what if it became hotel
------------------------
-> cook, billing counter 
-> Owner --> issues the tokens 
-> Cook --> he will cook and serve 
-> He can manage 15 members 

what if 50 members came at a time?
-----------------------------------
-> It is difficult to manage cooking and serving for cook

Then It will upgrade to restaurant:
-----------------------------------
-> when you enter --> someone will welcome you, he will show tha table --> captain --> responsibility is, which table is free/empty 
-> waiter --> takes the order --> responsibility is; queue management, taking order, serving order 
-> chef --> sees the order and cook the meal --> only cooking responsibility 
->  chef --> raw products --> eatable format

-> If the internet traffic is less, desktop applications are enough 
-> But the internet traffic is more and more. so, we moved to web-based applications

-> In web-based applications, it is 1-tier architecture
-> waiter  --> web server 
-> chef --> App server 
-> Raw items --> DB server/ data 

raw products ==> data 

for example;
------------
-> If we take facebook data, it is in the format of tables 
user_id , user_name, first_name, last_name, password, created date, dob
1          lakshmi    lakshmi      mungara  lakshmi2297  19-aug-2024 05-07-1999

chef ==> App server
-> Through SQl queries, app server will check the data 

for eg: If you given user-name and password 
select * from user where user_name = 'lakshmi' and password = 'lakshmi2997'

web server --> put that data into HTML format, so that a normal person can easily understandable format
-> App server gives in this format 
{
	"user":"lakshmi",
	"dob":05-07-1999,
	"location":"Hyderabad"
}


-> If web server is accesing DB server, then the code might expose and easily can hack it 
-> Web server is like security 
-> client directly connects to load balance and web server 

web tier --> Load balancers, web servers 
App tier --> App servers 
Data tier --> DB servers 

Technologies in ,
Databases --> MySQL, MSSQL, Oracle, Postgress, MongoDB, Redis 
App servers/API(Backend tier)--> Java, Python, NodeJS, dotnet, Go, #C etc 
Web tier(frontend tier) --> HTML, CSS, Javascript, AngularJS, ReactJS, ExpressJS, Jquery etc..

-> Frontend applications are static --> There are generally post in Nginx, Apache etc
-> Backend applications are Dynamic --> previously, JBoss, webspher, WebLogic, etc --> Now, we are using Tomcat 
============================================================

AWS account --> EC2 instance --> launch instance --> enter the name of the instance --> In applications and OS image -> search for devops-practice  -> go to community AMIs-> select Redhat(RHEL -9-DevOps-Practice)  --> t3.micro --> Key_pair is "no"(we will use only username and password to login server) -->  security group(allow-all)

security group --> create security group --> enter the name(allow-all) --> description(allow every port from every IP) --> Inbound rules --> select All traffic -> 0.0.0.0/ -> click on create security group 


username --> ec2-user -> ssh ec2-user@54.90.214.156
password --> DevOps321


Database server
----------------
Install DB --> MySQL
dnf install 

run DB --> systemctl 
check the status --> systemctl status mysqld
check port opened or not --> netstat -lntp 
check the process --> ps -ef | grep mysqld 
Enabling the mysql service --> systemctl enable mysqld

By default, username is root 
password we have to setup --> mysql_secure_installation --set-root-pass ExpenseApp@1

client software:
-----------------

-> server software is mysql-server and it is running, to check the data you should connect to server through client 
-> client package is just mysql 

-> By default, client package is installed with the server 
-> we need command to connect to the client --> mysql -h <IP> -u root -p<password>  --> when client is outside the server 
-> mysql -u root -p<password> --> when client is inside the server --> just enter 'mysql'

user related information is stored in --> user schema 
posts related information is stored in --> posts schema 
videos related information is stored in --> videos schema 

Note: MySQL is a Database server 

mysql
-------
show databases;
use <database-name>;
show tables;
select * from <table-name>;



