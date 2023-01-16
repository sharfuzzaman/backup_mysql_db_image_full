
# MySQL physical image backup and restore (Linux)

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

