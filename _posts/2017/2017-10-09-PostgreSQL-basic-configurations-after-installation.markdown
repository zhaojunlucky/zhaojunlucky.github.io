---
title:  "PostgreSQL Basic Configurations After Installation"
date:   2017-10-09 21:27:21 +0800
categories: postgres
---

## Allow all connections  
Edit /etc/postgresql/${version}/main/pg_hba.conf, add `host    all             all             0.0.0.0/0               md5` in section `IPv4 local connections`  
## Listen on all IP addresses
Edit /etc/postgresql/${version}/main/postgres.conf, in section `Connection Settings`, uncomment `listen_addresses = 'localhost'`, change the `localhost` to `*`
## Create a superuser
Run in shell,  
1. `su - postgres`  
2. `createuser -P -s -e <username>`, will prompt to input the password for the user
