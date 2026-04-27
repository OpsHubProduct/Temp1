---
title: manual-postgresdatabase-creation
---

* In case of manual database creation for PostgreSQL Server database, database and schema should be in lowercase only.
  * We need 1 database and 2 schemas to be created manually, out of which database and schema's names must be same for opshub database. The other schema will be created for reportsdb.

Let's say the name of the database is `db1`:

```sql
drop database IF EXISTS db1
db1 database: CREATE DATABASE db1
WITH
ENCODING = 'UTF8'
LC_COLLATE = 'en_US.UTF-8'
LC_CTYPE = 'en_US.UTF-8'
TEMPLATE = template0;
```

> **Note**: The above query will create database with Collate United States, UTF-8. For creating database with desired collate, update `LC_COLLATE` and `LC_CTYPE` as per the requirement.

```sql
db1 schema: create schema db1;
Reports schema: create schema <schema_name>;
```

Here \<schema\_name> will be the schema name of reportsdb.
