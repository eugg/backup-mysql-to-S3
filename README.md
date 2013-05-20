backup-mysql-to-S3
==================

backup your mysql DB to S3 automatically via crontab

<h2>Install s3cmd</h2>
use command live to control s3 
http://s3tools.org/repositories

<h2>Setup Access key & Secret key</h2>

use <pre>s3cmd --configure</pre>

more command:
http://s3tools.org/s3cmd

<h2>add a new bucket </h2>

for mysql backup files

<pre>s3cmd mb s3://mysql_backup</pre>

<h2>write down a command document </h2>
<pre>
mysqldump -u DB_USER -pDB_PASSWORD DB_NAME > /backup_folder/backup_`date '+%Y_%m_%d'`.sql
s3cmd put /backup_folder/backup_`date '+%Y_%m_%d'`.sql s3://mysql_backup/backup_`date '+%Y_%m_%d'`.sql 
</pre>
use <pre>crontab -e</pre> to edit crontab task as below

</pre>0 3 * * * sh backup_command</pre>
