
# MySQL image backup and restore (Linux)

## MySQL physical backup and restore
DB version : 8.0.31  

Distribution : Debian  

OS : "Linux Mint 20.2" 
- Perform a full image backup of database (Single File Backup)
- Restore a database from a full image backup 


## Download & Install mysqlbackup

[Download MySQL enterprise backup](https://edelivery.oracle.com/osdc/faces/SoftwareDelivery)  
After click this link search "MySQL enterprise backup"  
Enter the link and download expected version according to your distribution.
After downloaded you will have a zip/tar file, extract this. After extract this you will get a directory as same name as file. Enter the directory
```bash
    $ cd V1031535-01
```
In my case, "V1031535-01" this is my directory.  
After enter the directory you will see couple of .deb file. Install it on your system
```bash
    $ dpkg -i mysql-commercial-backup_8.0.31+commercial-1ubuntu20.04_amd64.deb
```
In my case, this is "mysql-commercial-backup_8.0.31+commercial-1ubuntu20.04_amd64.deb" my .deb file, you could see a differnet name but installed as your system.
After install please check the version of mysqlbackup
```bash
    $ mysqlbackup --version
```
If you watch a output with version, That means you can move forward to the next step
## MySQl datadir location
Find where mysql datadir is stored  
Run,
```bash 
    $ mysql -u root -p -e 'SHOW VARIABLES WHERE Variable_Name LIKE "%dir"'
```
You will find a list and please check the word "datadir", and besides datadir you can look the localtion, In my case /var/lib/mysql is the directory where MySQL stores data.
## Make an image backup of full database
```bash
    $ mysqlbackup --user=user --password=password --host=127.0.0.1 --backup-image=/home/sharfuzzaman/backup/local.mbi --backup-dir=/home/sharfuzzaman/backup/backup_tmp backup-to-image
```

- --user : It is your mysql user
- --password : mysql user password
- --host : Hostname
- --backup-image= /home/userDir/backup/local.mbi (This user directory will store your mysql backup image of your database named "local.mbi")
- --backup-dir= /home/userDir/backup/backup_tmp (This directory stores all additional datas without images)
- backup-to-image (We are saying please backup this image which we have mentioned earlier)

After run this command if everything goes find, you will look a message like the screenshot

![App Screenshot](https://github.com/sharfuzzaman/backup_restore_mysql_db_image_full/blob/main/backup-completed.png)

After that, you will see a directory named backup under your user home directory
```bash
    $ cd /home/sharfuzzaman/backup
    $ ls
```
You will see a directory named backup_tmp also.

That means, we have cretaed a successfull backup of our MySQL databases.

## Restore database from an image backup
For validate the backup run 
```bash
    $ mysqlbackup --backup-image=/home/sharfuzzaman.local.mbi validate
```
Give the path of the image, if image validates properly then you'll find a response like "mysqlbackup completed OK!
"

Before restart database make sure your mysql server is not running. Check the status of mysql server, if it is running please stop this
```bash
    $ sudo service mysql stop
```
**When you are restoring mysql image make sure there has no mysql directory in  /var/lib/ directory, If mysql directory exists then please move it in another location**.

