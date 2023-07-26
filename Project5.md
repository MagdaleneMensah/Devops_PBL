
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











