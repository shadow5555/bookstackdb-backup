# bookstackdb-backup
backup your bookstackdb using docker

Backup
There are two types of content you need to backup: Files and database records.

Database
The easiest way to backup the database is via mysqldump:

1
1
# Syntax
2
1
mysqldump -u {mysql_user} -p {database_name} > {output_file_name}
3
1
## Only specify the -p if the user provided has a password
4
1
•
5
1
•
6
1
# Example
7
1
mysqldump -u benny bookstack > bookstack.backup.sql
If you are using MySQL 5.7 on Ubuntu 16.04 and are using the root MySQL user you will likely have to run the command above with sudo:

1
1
sudo mysqldump -u root bookstack > bookstack.backup.sql
The resulting file (bookstack.backup.sql in the examples above) will contain all the data from the database you specified. Copy this file to somewhere safe, ideally on a different device.

Files
Below is a list of files and folders containing data you should back up. The paths are shown relative to the root BookStack folder.

.env - File, Contains important configuration information.
public/uploads - Folder, Contains any uploaded images (If not using amazon s3).
storage/uploads - Folder, Contains uploaded page attachments (Only exists as of BookStack v0.13).
Alternatively you could backup up your whole BookStack folder but only the above are non-restorable.

The following command will create a compressed archive of the above folders and files:

1
1
# BookStack v0.13+:
2
1
tar -czvf bookstack-files-backup.tar.gz .env public/uploads storage/uploads
3
1
•
4
1
# BookStack v0.12.* and below:
5
1
tar -czvf bookstack-files-backup.tar.gz .env public/uploads
The resulting file (bookstack-files-backup.tar.gz) will contain all your file data. Copy this to a safe place, ideally on a different device.


