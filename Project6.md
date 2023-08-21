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
<img width="462" alt="Screenshot 2023-08-14 222102" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/d7eb13f0-236b-4f7a-b1ee-5fe6f7ec8469">

```bash
sudo gdisk /dev/xvdg
```
<img width="472" alt="Screenshot 2023-08-15 172433" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/6fa6c3be-6e12-4edf-bfc6-a9050487322b">

```bash
sudo gdisk /dev/xvdh
```
<img width="469" alt="Screenshot 2023-08-15 173318" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/60d4abe7-0fca-41ec-87bd-82dc8ec566f4">

Install lvm2 package using sudo yum install lvm2. Run sudo lvmdiskscan command to check for available partitions.
Note: Previously, in Ubuntu we used apt command to install packages, in RedHat/CentOS a different package manager is used, so we shall use yum command instead.

```bash
 sudo yum install lvm2 -y
```
<img width="470" alt="Screenshot 2023-08-15 173737" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/ff7aee48-081b-4910-8aa0-e15d8f72ffad">


```bash
sudo lvmdiskscan
```
<img width="341" alt="Screenshot 2023-08-15 174042" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/effcb50d-7b08-4a7b-964f-5594b5620135">


Use pvcreate utility to mark each of 3 disks as physical volumes (PVs) to be used by LVM

```bash
sudo pvcreate /dev/xvdf1 /dev/xvdg1 /dev/xvdh1
```
<img width="472" alt="Screenshot 2023-08-15 174318" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/5603bbb2-f007-46d6-974a-6ee73a3bdb6c">

Verify that your Physical volume has been created successfully by running sudo pvs
```bash
sudo pvs
```
<img width="308" alt="Screenshot 2023-08-15 174813" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/8da34c94-6ca8-424b-9035-c892e4875887">

Use vgcreate utility to add all 3 PVs to a volume group (VG). Name the VG webdata-vg
```bash
sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1
```
<img width="471" alt="Screenshot 2023-08-15 175414" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/e294d374-7655-452a-a9b7-569ecd572b89">

Verify that your VG has been created successfully by running
```bash
sudo vgs
```
<img width="328" alt="Screenshot 2023-08-15 175748" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/27e3ffcb-207e-4c20-b9fd-528a7e67e2cc">

Use lvcreate utility to create 2 logical volumes. apps-lv (Use half of the PV size), and logs-lv Use the remaining space of the PV size. NOTE: apps-lv will be used to store data for the Website while, logs-lv will be used to store data for logs.

```bash
sudo lvcreate -n apps-lv -L 14G webdata-vg
```
<img width="472" alt="Screenshot 2023-08-15 184532" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/615311ab-afeb-4991-afd0-0731d752f42a">

```bash
sudo lvcreate -n logs-lv -L 14G webdata-vg
```

<img width="472" alt="Screenshot 2023-08-15 184932" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/46a72ede-8c60-4774-a1e9-1fd1fc5ee39e">

Verify that your Logical Volume has been created successfully by running sudo lvs
```bash
sudo lvs
```
<img width="472" alt="Screenshot 2023-08-15 185625" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/fe1eadab-4a8f-49eb-8d6e-26007543d3c0">

Verify the entire setup
```bash
sudo vgdisplay -v #view complete setup - VG, PV, and LV
```
<img width="472" alt="Screenshot 2023-08-15 193039" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/cf6ff20e-860b-42b3-b217-8b05bb94dab3">

```bash
sudo lsblk
```
<img width="428" alt="Screenshot 2023-08-15 193412" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/a4fc6167-1740-4a98-b141-de28512aaf63">

Use mkfs.ext4 to format the logical volumes with ext4 filesystem
```bash
sudo mkfs -t ext4 /dev/webdata-vg/apps-lv
```
<img width="470" alt="Screenshot 2023-08-15 193956" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/0e294870-6a4f-4e85-9581-c01a783eab18">

```bash
sudo mkfs -t ext4 /dev/webdata-vg/logs-lv
```
<img width="474" alt="Screenshot 2023-08-15 194535" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/5672247f-7879-4f71-a8d3-b167feb652a1">

Create /var/www/html directory to store website files
```bash
sudo mkdir -p /var/www/html
```
<img width="386" alt="Screenshot 2023-08-15 195124" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/503655c4-e7f4-463e-a699-d0eb56e9234f">

Create /home/recovery/logs to store backup of log data
```bash
sudo mkdir -p /home/recovery/logs
```
<img width="414" alt="Screenshot 2023-08-15 195543" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/d2381cb5-184c-41e7-8347-ed73fc36af6f">

Mount /var/www/html on apps-lv logical volume
```bash
sudo mount /dev/webdata-vg/apps-lv /var/www/html/
```
<img width="470" alt="image" src="https://github.com/MagdaleneMensah/Devops_PBL/assets/133181270/b9fd75e5-02c2-4b6a-8401-183340d30282">

Use rsync utility to backup all the files in the log directory /var/log into /home/recovery/logs (This is required before mounting the file system)
```bash
sudo rsync -av /var/log/. /home/recovery/logs/
```
<img width="473" alt="Screenshot 2023-08-15 203027" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/21f29121-3b81-41f3-8d8a-f79dd69292b7">

Mount /var/log on logs-lv logical volume. (Note that all the existing data on /var/log will be deleted. That is why step 15 above is very important)
```bash
sudo mount /dev/webdata-vg/logs-lv /var/log
```
<img width="472" alt="Screenshot 2023-08-15 203458" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/0bab25bd-a290-460f-850d-d05c60863600">

Restore log files back into /var/log directory
```bash
sudo rsync -av /home/recovery/logs/log/. /var/log
```
<img width="472" alt="Screenshot 2023-08-15 204007" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/723dde1d-0a6c-40f9-a8e1-80baf68481d0">

Update /etc/fstab file so that the mount configuration will persist after restart of the server.
The UUID of the device will be used to update the /etc/fstab file;
```bash
sudo blkid
```
<img width="467" alt="Screenshot 2023-08-15 205406" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/16dcb942-f49f-40c2-b823-6bc1ec1c9e4c">

```bash
sudo vi /etc/fstab
```
<img width="479" alt="Screenshot 2023-08-15 205838" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/df3c13a6-e3cb-4ca8-95bc-cea8088f6278">

Test the configuration and reload the daemon
```bash
sudo mount -a
```
<img width="315" alt="Screenshot 2023-08-15 230439" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/54cbfb12-ccaa-422c-ad9f-fac6d9bafbb2">

```bash
sudo systemctl daemon-reload
```
<img width="407" alt="Screenshot 2023-08-16 182734" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/d2b5ddd4-bebe-4f7d-821e-3e6d3a55861c">

Verify your setup by running df -h, output must look like this:
```bash
df -h
```
<img width="470" alt="Screenshot 2023-08-16 183203" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/3567482d-d19b-4137-bfef-b5440dca97e3">


## PREPARE THE DATABASE SERVER

Prepare the Database Server
Launch a second RedHat EC2 instance that will have a role – ‘DB Server’
Repeat the same steps as for the Web Server, but instead of apps-lv create db-lv and mount it to /db directory instead of /var/www/html/.

Create three Volumes:
<img width="812" alt="Screenshot 2023-08-16 201018" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/dd680bc3-cc18-4929-8ea7-319da3e0f41b">

Attach Volumes one at a time to the DB-Server:
<img width="821" alt="Screenshot 2023-08-16 202443" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/acdfa14f-5eb6-49ea-b793-db625fd2636f">

Open up the Linux terminal to begin configuration your DB-Server
```bash
sudo su
hostname DB-Server
bash
```
<img width="524" alt="Screenshot 2023-08-16 203826" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/67eccfe6-2467-4c73-b035-2056f0169b5e">

Use lsblk command to inspect what block devices are attached to the server. Notice names of your newly created devices. All devices in Linux reside in /dev/ directory. Inspect it with ls /dev/ and make sure you see all 3 newly created block devices there – their names will likely be xvdf, xvdh, xvdg.

```bash
lsblk
```
<img width="321" alt="Screenshot 2023-08-16 204242" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/c6486e30-b6c8-4137-849e-02bf83accbc4">

Use df -h command to see all mounts and free space on your server
```bash
df -h
```
<img width="364" alt="Screenshot 2023-08-16 204704" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/493400f9-7d41-448e-bf95-c45c9f9fb901">

Use gdisk utility to create a single partition on each of the 3 disks
```bash
sudo gdisk /dev/xvdf
```
<img width="457" alt="Screenshot 2023-08-16 205858" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/bad028f3-d5d1-46ca-971e-7f905393010f">

```bash
sudo gdisk /dev/xvdg
```
<img width="472" alt="Screenshot 2023-08-16 220528" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/76e3ee98-59c4-45ac-8685-c6e028501351">

```bash
sudo gdisk /dev/xvdg
```
<img width="474" alt="Screenshot 2023-08-16 221538" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/588b616c-5187-4a29-bf03-49018a8fcf90">

```bash
lsblk
```
<img width="374" alt="Screenshot 2023-08-16 221905" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/8ad74aa1-b1ac-4ad6-ad5b-f1de1a981162">

Install lvm2 package using sudo yum install lvm2. Run sudo lvmdiskscan command to check for available partitions. Note: Previously, in Ubuntu we used apt command to install packages, in RedHat/CentOS a different package manager is used, so we shall use yum command instead.

```bash
 sudo yum install lvm2 -y
```
<img width="473" alt="Screenshot 2023-08-16 222452" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/bf484d1d-bb1a-4e0f-b7b9-badf7f520625">

```bash
sudo lvmdiskscan
```
<img width="365" alt="Screenshot 2023-08-16 223024" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/8bdad833-26e4-43e2-8606-0075a04deaf5">

```bash
sudo pvcreate /dev/xvdf1 /dev/xvdg1 /dev/xvdh1
```
<img width="473" alt="Screenshot 2023-08-16 223331" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/61791eca-491c-4a09-96b7-1789a20d8ade">

Verify that your Physical volume has been created successfully by running sudo pvs
```bash
sudo pvs
```
<img width="440" alt="Screenshot 2023-08-16 225531" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/f076e58c-dc72-4b01-8df3-b9b7c759272d">

Use vgcreate utility to add all 3 PVs to a volume group (VG). Name the VG database-vg
```bash
sudo vgcreate database-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1
```
<img width="470" alt="Screenshot 2023-08-16 230219" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/c40e5a7c-0ae7-4305-bd46-24f9e760dec8">

```bash
sudo vgs
```
<img width="325" alt="Screenshot 2023-08-16 230627" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/2d9ceaca-7275-4af4-bd20-9ce84d84eb57">

```bash
sudo lvcreate -n db-lv -L 20G database-vg
```
<img width="467" alt="Screenshot 2023-08-17 215314" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/472faf3a-12f4-4bbc-80df-075d819ef7fd">

```bash
sudo mkdir /db
```
<img width="281" alt="Screenshot 2023-08-17 215716" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/311374b5-f667-4c90-aae1-15ff879df88d">

```bash
sudo mkfs.ext4 /dev/database-vg/db-lv
```
<img width="470" alt="Screenshot 2023-08-17 220535" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/986e542c-5241-447f-9437-e4079e45abdb">

```bash
sudo mount /dev/database-vg/db-lv /db
```
<img width="443" alt="Screenshot 2023-08-17 221332" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/a9215a2d-8477-446b-9a2d-e408adba343a">

```bash
df -h
```
<img width="470" alt="Screenshot 2023-08-17 223355" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/8cbfce7b-8ad2-4957-aa2e-3b4902e1da29">

```bash
sudo blkid
```
<img width="474" alt="Screenshot 2023-08-17 223759" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/9ba2fa7a-de35-4a51-a528-d6e49ba32518">

```bash
sudo vi /etc/fstab
```
<img width="485" alt="Screenshot 2023-08-17 225340" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/dbce0a20-93bc-470d-97a4-e6a4a8c8a865">

```bash
sudo mount -a
```
<img width="293" alt="Screenshot 2023-08-17 230008" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/d93de0dc-685c-4328-9299-814214fa43ce">

```bash
sudo systemctl daemon-reload
```
<img width="392" alt="Screenshot 2023-08-17 230855" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/00c0e012-03da-4166-b42d-24e7325678e7">

```bash
df -h
```
<img width="463" alt="Screenshot 2023-08-17 231606" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/3339c11e-b308-434f-9fa7-efbe262dfc7f">

##  Install WordPress on your Web Server EC2

Update the repository
```bash
sudo yum update -y
```
<img width="459" alt="Screenshot 2023-08-20 235334" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/897cea6e-5159-4d8a-a5f7-55fafd40834f">

## Install wget, Apache and it’s dependencies
```bash
sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json
```
<img width="476" alt="Screenshot 2023-08-21 001308" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/a7de4bd8-7f73-49ed-8d09-1072286779af">


```bash
 sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
```
<img width="472" alt="Screenshot 2023-08-21 001624" src="https://github.com/MagdaleneMensah/DevopsmyAWS/assets/133181270/395e3732-ee21-4699-acc5-2d333cc23a42">

```bash
sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
```
















