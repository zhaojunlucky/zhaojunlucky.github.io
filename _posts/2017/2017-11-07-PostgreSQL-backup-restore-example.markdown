---
title:  "PostgreSQL backup & restore example"
date:   2017-11-07 21:27:21 +0800
categories: postgres
---

### Backup 
`pg_dump --file ${backup file}  --port "5432"  --format=c --blobs --schema ${schema} ${database} -U ${user}` 
### Restore
`pg_restore  -U ${user} --exit-on-error --verbose --dbname=${database} ${backup file}`
