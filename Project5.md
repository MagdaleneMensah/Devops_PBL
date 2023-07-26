
## CLIENT-SERVER ARCHITECTURE WITH MYSQL

IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).
TASK – Implement a Client Server Architecture using MySQL Database Management System (DBMS).
To demonstrate a basic client-server using MySQL Relational Database Management System (RDBMS), follow the below instructions

Create and configure two Linux-based virtual servers (EC2 instances in AWS).
Server A name - `mysql server`
Server B name - `mysql client`

<img width="813" alt="Screenshot 2023-07-25 172113" On mysql server Linux Server install MySQL Server software.src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/25a92fb1-90bd-465f-a649-d8d1be730248">

## On mysql server Linux Server install MySQL Server software.

sudo apt update -y
<img width="875" alt="Screenshot 2023-07-25 174453" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/f6ecfe6c-f63b-43af-aa95-f7dfac703614">

sudo apt install mysql-server -y
<img width="929" alt="Screenshot 2023-07-25 185939" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/4279b6ff-8f6a-4452-bf5b-1b53c72a2c6d">

sudo systemctl enable mysql
<img width="758" alt="Screenshot 2023-07-25 190631" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/fe90b2e4-12fe-4230-8147-a27b8ef520ca">

## On mysql client Linux Server install MySQL Client software.

sudo apt update -y
<img width="472" alt="Screenshot 2023-07-25 192241" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/f345512f-4181-4f09-b46d-ea41d4846c26">

sudo apt install mysql-client -y
<img width="472" alt="Screenshot 2023-07-25 193003" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/d326b1b1-89e0-446f-af17-b91e2bf95c36">


## By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from mysql client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

<img width="484" alt="Screenshot 2023-07-25 200744" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/4ce44a5e-bb72-4264-9078-16cfde0653a4">


## In the mysql-server run a security script that comes pre-installed with MySQL

$ sudo mysql
<img width="472" alt="Screenshot 2023-07-25 202055" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/be227c5f-fede-4ebd-9a29-f74f7e3e762f">

 ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
 <img width="468" alt="image" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/2ed1ba15-4f97-4234-9d51-7c5d0016ed07">

 mysql> exit
 

$ sudo mysql_secure_installtion














