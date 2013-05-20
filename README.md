backup-mysql-to-S3
==================

backup your mysql DB to S3 automatically via crontab

<h1>Install s3cmd</h1>
use command live to control s3 
http://s3tools.org/repositories

Setup Access key 和& Secret key

s3cmd --configure

more command:
http://s3tools.org/s3cmd

add a new bucket for mysql backup files

s3cmd mb s3://mysql_backup

write down a command document as below

mysqldump -u DB_USER -pDB_PASSWORD DB_NAME > /backup_folder/backup_`date '+%Y_%m_%d'`.sql
s3cmd put /backup_folder/backup_`date '+%Y_%m_%d'`.sql s3://mysql_backup/backup_`date '+%Y_%m_%d'`.sql 

use crontab -e to edit crontab task as below

0 3 * * * sh backup_command
