
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

<img width="475" alt="Screenshot 2023-07-26 075459" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/8145df6d-64f2-4cb9-a74b-142f583c6785">


## On mysql client Linux Server install MySQL Client software.

sudo apt update -y

<img width="472" alt="Screenshot 2023-07-25 192241" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/f345512f-4181-4f09-b46d-ea41d4846c26">

sudo apt install mysql-client -y

<img width="472" alt="Screenshot 2023-07-25 193003" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/d326b1b1-89e0-446f-af17-b91e2bf95c36">


## By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from mysql client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’

<img width="836" alt="Screenshot 2023-07-26 083544" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/083456a3-777d-42c8-80c7-72f194b927b9">


## In the mysql-server run a security script that comes pre-installed with MySQL

$ sudo mysql_secure_installation

<img width="473" alt="Screenshot 2023-07-26 084252" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/6af5605a-5605-4fd5-9fa1-61aced7f5ea4">

$ sudo mysql
<img width="409" alt="Screenshot 2023-07-26 124508" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/4684c372-e56b-4869-8b86-7699b14dfd94">

CREATE USER 'remote_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
<img width="470" alt="Screenshot 2023-07-26 130226" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/8d716e48-80b1-41e5-85ff-7ccc6c6e7e9e">

CREATE DATABASE test_db;
<img width="295" alt="Screenshot 2023-07-26 130623" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/a9621dbf-a501-4b3f-b684-c5cbee6ef36f">

GRANT ALL ON test_db.* TO 'remote_user'@'%' WITH GRANT OPTION;
<img width="459" alt="Screenshot 2023-07-26 131543" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/246e5221-0536-4ab5-83d7-cfe61b52ace6">

FLUSH PRIVILEGES;
<img width="303" alt="Screenshot 2023-07-26 132007" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/49418b70-0087-4e2f-9e36-5bcff318111f">


exit
<img width="243" alt="Screenshot 2023-07-26 132216" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/26a12970-dc6c-4974-b013-4a565695c766">



## You might need to configure MySQL server to allow connections from remote hosts.

sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
<img width="479" alt="Screenshot 2023-07-26 171738" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/31f31e5f-b09a-49e3-814c-7c4c6541c0f2">


## Replace ‘127.0.0.1’ to ‘0.0.0.0’ like this:
<img width="256" alt="Screenshot 2023-07-26 172050" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/433fd7ef-aa6e-44c2-a524-8ffaf820528f">

sudo systemctl restart mysql
<img width="473" alt="Screenshot 2023-07-26 175110" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/f4de2014-d33b-4797-8dc0-1f57c918492d">

## From mysql client Linux Server connect remotely to mysql server Database Engine without using SSH. You must use the mysql utility to perform this action.

sudo mysql -u remote_user -h 172.31.42.92 -p




























