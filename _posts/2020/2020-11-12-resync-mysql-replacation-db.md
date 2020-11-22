---
last_modified_at: 2020-11-12T01:53:49+00:00
title: Resync MySQL Replacation DB
categories:
- mysql
- replication

---
## The Problem

We have a primary MySQL database and a replication, we plan to migrate them to another widget, so, IT cloned both of them in the new widget, and new two VMs are up. But the new replication database uses its default setting and sync from the old primary database, cause the new replication has diverged from the new primary.

## The Requirement

Let the new replication to sync with the new primary to do validation test.

## Solution

1. Stop the replication.  
   `stop slave;`
2. Issue a CHANGE MASTER command but omit the log file name and position  
   `CHANGE MASTER to MASTER_HOST='<new primary hos_>',MASTER_USER='<user>', MASTER_PASSWORD='<password>';`
3. Dump a backup from the new primary  
   `mysqldump -uroot -p --master-data --all-databases --flush-privileges | gzip -1 > replication.sql.gz`
4. Copy the dump to replication
5. Import the dump to replication  
   `zcat 'gz file'| mysql -uroot -p`
6. Start the replication  
   `start slave;`
7. Check the status  
   `show slave status\G`