---
title: manual-mysqldatabase-creation
---

Let's name the database as `db1`:

```sql
DROP DATABASE IF EXISTS db1;
CREATE DATABASE db1 CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
```

Let's name the reports database as reportsdb:

```sql
DROP DATABASE IF EXISTS reportsdb;
CREATE DATABASE reportsdb CHARACTER SET latin1 COLLATE latin1_general_cs; 
```
