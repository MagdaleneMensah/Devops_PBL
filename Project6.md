## WEB SOLUTION WITH WORDPRESS

You are progressing in practicing to implement web solutions using different technologies. As a DevOps engineer you will most probably encounter PHP-based solutions since, even in 2021, it is the dominant web programming language used by more websites than any other programming language.

In this project you will be tasked to prepare storage infrastructure on two Linux servers and implement a basic web solution using WordPress. WordPress is a free and open-source content management system written in PHP and paired with MySQL or MariaDB as its backend Relational Database Management System (RDBMS).

Project 6 consists of two parts:

Configure storage subsystem for Web and Database servers based on Linux OS. The focus of this part is to give you practical experience of working with disks, partitions and volumes in Linux.
Install WordPress and connect it to a remote MySQL database server. This part of the project will solidify your skills of deploying Web and DB tiers of Web solution.
As a DevOps engineer, your deep understanding of core components of web solutions and ability to troubleshoot them will play essential role in your further progress and development.

Three-tier Architecture
Generally, web, or mobile solutions are implemented based on what is called the Three-tier Architecture.

Three-tier Architecture is a client-server software architecture pattern that comprise of 3 separate layers.
<img width="557" alt="Screenshot 2023-08-13 135708" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/869fd3c0-d585-47c3-99ea-8194285ee769">


    

Presentation Layer (PL): This is the user interface such as the client server or browser on your laptop.
Business Layer (BL): This is the backend program that implements business logic. Application or Webserver
Data Access or Management Layer (DAL): This is the layer for computer data storage and data access. Database Server or File System Server such as FTP server, or NFS Server
In this project, you will have the hands-on experience that showcases Three-tier Architecture while also ensuring that the disks used to store files on the Linux servers are adequately partitioned and managed through programs such as gdisk and LVM respectively.

You will be working working with several storage and disk management concepts, to have a better understanding, watch following video:
Disk management in Linux

Note: We are gradually introducing new AWS elements into our solutions, but do not be worried if you do not fully understand AWS Cloud Services yet, there are Cloud focused projects ahead where we will get into deep details of various Cloud concepts and technologies – not only AWS, but other Cloud Service Providers as well.

Your 3-Tier Setup
A Laptop or PC to serve as a client
An EC2 Linux Server as a web server (This is where you will install WordPress)
An EC2 Linux server as a database (DB) server
Use RedHat OS for this project

By now you should know how to spin up an EC2 instance on AWS, but if you forgot – refer to Project1 Step 0.
In previous projects we used ‘Ubuntu’, but it is better to be well-versed with various Linux distributions, thus, for this projects we will use very popular distribution called ‘RedHat’ (it also has a fully compatible derivative – CentOS)

Note: for Ubuntu server, when connecting to it via SSH/Putty or any other tool, we used ubuntu user, but for RedHat you will need to use ec2-user user. Connection string will look like ec2-user@<Public-IP>

Let us get started!

## Step 1 — Prepare a Web Server
Launch an EC2 instance that will serve as “Web Server”.

Create 3 volumes in the same AZ as your Web Server EC2, each of 10 GiB.
<img width="945" alt="Screenshot 2023-08-14 202453" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/c95cf5de-0da5-49dc-86c8-c9359395574b">

<img width="840" alt="Screenshot 2023-08-14 110228" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/afcabae3-227b-4c9b-be83-22864c0a3e88">
<img width="948" alt="image" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/d2c1e66b-0c4b-4120-a610-f11c6946d642">

Now Attach all three of your Volumes to your Web-server
<img width="440" alt="Screenshot 2023-08-14 213602" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/bc3dbf0f-4860-48aa-a7a9-75bdbd5df892">

Open up the Linux terminal to begin configuration your Web-server

```bash
sudo su
hostname Web-server
bash
```
<img width="462" alt="Screenshot 2023-08-14 212042" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/1021431e-75f0-4234-b9ec-2f303176b71d">

Use lsblk command to inspect what block devices are attached to the server. Notice names of your newly created devices. All devices in Linux reside in /dev/ directory. Inspect it with ls /dev/ and make sure you see all 3 newly created block devices there – their names will likely be xvdf, xvdh, xvdg.

```bash
lsblk
```
<img width="472" alt="Screenshot 2023-08-14 220121" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/9d5bc446-4d34-4554-9cbb-2926638a6c69">

Use df -h command to see all mounts and free space on your server
```bash
df -h
```
<img width="370" alt="Screenshot 2023-08-14 220705" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/2b61d08a-136b-480b-9689-588271daef8a">

Use gdisk utility to create a single partition on each of the 3 disks
```bash
sudo gdisk /dev/xvdf
```




