Day-5 session-5(16/08/2024)
---------------------------
Recap:
------
-> Every system is and everything is based on CRUD
-> In Linux also, user management is also based on CRUD operations

User management:
-----------------
CRUD operations:
1. create the users 
2. Read the users  
3. Update the users
4. Delete the users 
-> Total administration is all done by using root access
For Password-based Authentication:
-----------------------------
-> Root access --> sudo su -
-> To create the user --> useradd <user-name>
-> To create the group --> groupadd <user-name>
-> Root user information --> cat /etc/passwd
-> group information  --> cat etc/group
-> primary group --> usermod -g <group-name> <user-name>
-> Secondary group --> usermod -aG <group-name> <user-name>
-> To set password --> passwd <user-name>
-> To display the user information --> id <user-name>

-> By default, password is disabled. So, to enable the password follow the command,
vim /etc/ssh/sshd_config
-> change the passwdAuthentication to 'yes'
-> Restart the system --> systemctl restart sshd

For key-based Authentication:
-----------------------------
-> To generate the key-pair --> ssh-keygen -f <user-name>
-> cat <public-key>
-> Administrator goes to user folder /home/ramesh
-> create the directory --> mkdir .ssh
-> change the permissions --> chmod 700 <directory-name>
-> Goes inside the .ssh/ folder --> cd .ssh/
-> create a file --> touch <file-name>
-> change the permissions --> chmod 600 <file-name>
-> change the ownership --> chown -R <user-name>:<user-name> <folder-name>
-> copy the public-key and paste it in the file
cd .ssh/ 
vim authorized_keys 
-> restart the server --> systemctl restart sshd
-> Login using the details of the user 
ssh -i ramesh ramesh@54.145.141.144

-> Removing from the group --> gpasswd -d <user-name> <group-name>
-> Changing the group under the name of the user --> usermod -g <user-name> <user-name(as group-name)>
-> Deleting the user --> userdel <user-name>


Now, in towards class we are going to learn about;

Package management:
===================
-> In any OS, installation of softwares is common
-> In windows, like if we download any software from the browser. Then in backgroud, first it downloads the related/dependent softwares and installs them and later on it downloads the required software and installs 
-> A software have lot of dependencies on other softwares 
-> It is difficult to install all the dependencies manually(identifying the dependencies, installing the dependencies and finally installing the required software you want) --> This is a painful process 
-> Before, we have rpm --> redhat package manager 

-> Later on, we got 'yum' and then 'dnf'
yum --> dnf 
-> dnf is the latest 


for example:
------------
-> In windows, it automatically downloads the updates like how?
-> Windows OS directly connects to the cloud through URL and automatically downloads the required packages  
-> URLs which help to download are configured in the windows 

-> So, In Linux server, some URLs are configured in the location /etc/yum.repo.d 
-> Linux contacts with URLs, fetch the data and installs the packages 

-> cd /etc/yum.repos.d --> changes to this location 
-> ls -la 
drwxr-xr-x.  2 root root    59 Jul 30 17:41 .
drwxr-xr-x. 77 root root 16384 Aug 17 01:30 ..
-rw-r--r--.  1 root root   968 Jul 30 17:41 amazonlinux.repo
-rw-r--r--.  1 root root   689 Jul 30 17:41 kernel-livepatch.repo

-> cat amazonlinux.repo  --> It gives some URLs which helps to download the packages

To install the packages:
------------------------
command is,  dnf install <package-name>
-> eg: dnf install git

To list out the packages in our system:
---------------------------------------
command is ,  dng list installed 

To count the no.of packages installed:
---------------------------------------
dnf list installed | wc -l 

To know how many packages are available to install?:
---------------------------------------------------
command is, dnf list available
-> dnf list available | wc -l 

To remove the package:
---------------------
command is, dnf remove <package-name> -y 
-> eg: dnf remove git -y 

for example:
------------
-> In companies, they have there own URLs and placed in the directory /etc/yum.repos.d, so we download the packages and install them from companies website 

Note :
----
we use package management heavily 

Important for interviews:
=========================

How can you check cpuinfo, memory info, OS?
-------------------------------------------
-> For cpu information --> cat /proc/cpuinfo
-> For memory information --> cat /proc/meminfo 
-> For OS information --> cat /etc/os-release


Service Management:
===================
-> If suppose, we are connecting to server. The service should be in running state 

Service lifecycle
------------------
1. start the service
2. stopping the service
3. Restarting the service
4. Check the status 
5. Enabling the service
6. Disabling the service 

To check the status of SSH:
----------------------------
command is, systemctl status sshd 

HTTP --> 80
-> Generally for HTTP, we use 'nginx' package 
-> First install the nginx package 
-> start the service  --> systemctl start nginx
-> check the status of nginx --> systemctl status nginx 

-> The public IP address doesn't work directly
-> So, change the inbound rules in security group in AWS to HTTP with port number 80 

Path to change the inbound rules:
---------------------------------
Instance details --> security --> click on security group --> Edit inbound rules --> add HTTP --> save details 

http://54.145.141.144:80

What's happening in the background?
------------------------------------
-> Before reaching to the server it reaches to Security group --> port no 80 allowed 
-> It forwards the request to Linux server 

To stop the package nginx:
--------------------------
systemctl stop nginx 

-> If we get any problem, we have to restart the package 
-> nginx is used to host the websites 
-> We host our project in nginx 

for example:
------------
->In windows, some softwares are automatically on, and shows in taskbar 

-> Enable --> by default enabled services will start automatically 
-> Sometimes server stops and restarts, so in that case we use this enable mode 

To anable the package:
----------------------
command is, systemctl enable nginx

To disable the package:
------------------------
command is, systemctl disable nginx


Process management
==================
-> A sequence of steps to be executed to complete a task 

For example1 - marriage:
------------------------
-> A marriage cannot be possible for one individual 
-> One person divides the tasks into sub-tasks in the marriage to all the relatives and sub-ordinates etc.

For example2 - Office:
----------------------
-> Delivery manager - he is responsible for everything in the office 
-> He assigns the work to different people 

1. Team lead
2. Senior engineer
3. Junior engineer
4. Freshers/Trainers 

Freshers/Trainers --> reports to Junior engineer
Junior engineer --> reports to Senior engineer
senior engineer --> reports to team lead 
Team lead --> reports to Delivery manager 

-> Every team uses the task ID in any task we use that task ID to check the status of the task 

-> Every process should have an ID for tracking purpose

eg:
DM --> 001
TL --> 002
SE --> 003
JE --> 004 
Trainees --> 005 

Child(005) --> Parent(004)
004 --> 003
003 --> 002
002 --> 001 
001 --> Root process

-> If nginx is running --> process ID should be there 

To check the entire process:
----------------------------
command is, ps 

 PID TTY          TIME CMD
  32784 pts/3    00:00:00 sudo
  32785 pts/3    00:00:00 su
  32786 pts/3    00:00:00 bash
  32910 pts/3    00:00:00 ps

How to list all the running processes inside our linux server?
------------------------------------------------
command is, ps -ef

PID --> process ID 
PPID --> parent process ID 

To search any package in all the processes:
-------------------------------------------
command is, ps -ef | grep nginx

Foreground and Background processes:
-------------------------------------
Foreground --> It blocks the screen, runs in foreground 
-> if we given a command --> sleep 10
-> It blocks the screen for 10 seconds. so, we cannot do anything during that time  

Background --> it runs in backgroud, you can do other works 
-> If we given a command --> sleep 100 & 
-> It runs in the backgroud for 100 seconds 
-> so, we can do other works till that time 

To check the memory usage:
---------------------------
command is, top

note: 
shortcut to come out is, ctrl+c

-> for suppose, if a process is stuck in between that we have to kill 
-> for example, sleep 100 --> ps -ef | grep sleep 
-> kill <process-ID>  --> request 
-> kill -9 <process-ID>  --> order 

-> The only difference between kill <process-ID> and kill -9 <process-ID> is, kill is requesting manner and kill -9 is ordering to kill immediately
example:
-----------

[root@ip-172-31-34-208 ~]# sleep 100 &
[1] 33469
[root@ip-172-31-34-208 ~]# ps -ef | grep sleep
root       33469   32786  0 04:24 pts/3    00:00:00 sleep 100
root       33471   32786  0 04:24 pts/3    00:00:00 grep --color=auto sleep
[root@ip-172-31-34-208 ~]# kill 33469
[root@ip-172-31-34-208 ~]# sleep 100 &
[2] 33472
[1]   Terminated              sleep 100
[root@ip-172-31-34-208 ~]# kill -9 33472
[root@ip-172-31-34-208 ~]# ps -ef | grep sleep
root       33474   32786  0 04:25 pts/3    00:00:00 grep --color=auto sleep
[2]+  Killed                  sleep 100

 
Network management:
===================
-> Network is on instead of on-premise, it came to the cloud. Then we are not doing anything 
-> The main thing we have to do is, to check the ports by using, 

netstat --> network statistics
network -l 
network -lt --> t is for transfer control protocol(we need internet-based)
netstat -ltp --> p is for process
netstat -lntp --> it will tell you what ports are open 
