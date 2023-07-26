
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
<img width="471" alt="Screenshot 2023-07-26 074756" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/dd0579b2-ea20-4d87-b7c8-fecd45a60b23">



sudo apt install mysql-server -y
<img width="475" alt="Screenshot 2023-07-26 075459" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/2c60f2a0-9b62-4be7-b0ee-f9d734caecb8">


sudo systemctl enable mysql


## On mysql client Linux Server install MySQL Client software.

sudo apt update -y
<img width="472" alt="Screenshot 2023-07-25 192241" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/f345512f-4181-4f09-b46d-ea41d4846c26">

sudo apt install mysql-client -y
<img width="472" alt="Screenshot 2023-07-25 193003" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/d326b1b1-89e0-446f-af17-b91e2bf95c36">


## By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from mysql client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

<img width="484" alt="Screenshot 2023-07-25 200744" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/4ce44a5e-bb72-4264-9078-16cfde0653a4">


## In the mysql-server run a security script that comes pre-installed with MySQL

$ sudo mysql_secure_installation
<img width="478" alt="Screenshot 2023-07-25 221652" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/986824a4-8710-481f-aa5f-47d83141e3d9">



















