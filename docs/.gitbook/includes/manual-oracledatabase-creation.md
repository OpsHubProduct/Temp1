---
title: manual-oracledatabase-creation
---

> **Note:** Replace `<<SERVER_PASSWORD>>` with the actual password.

Let's name the database as `db1`:

```sql
drop user db1 CASCADE;
CREATE USER db1 IDENTIFIED BY <<SERVER_PASSWORD>> DEFAULT TABLESPACE users QUOTA 500M ON users TEMPORARY TABLESPACE temp PROFILE DEFAULT ACCOUNT UNLOCK
```

Let's name the reports database as reportsdb:

```sql
drop user reportsdb CASCADE;
CREATE USER reportsdb IDENTIFIED BY <<SERVER_PASSWORD>> DEFAULT TABLESPACE users QUOTA 2048M ON users TEMPORARY TABLESPACE temp PROFILE DEFAULT ACCOUNT UNLOCK
```

> **Note**: Ensure both `db1` and `reportsdb` users have the required privileges. For system and object privileges, refer to [Database Prerequisites](../../getting-started/prerequisites.md#database-prerequisites).

* Note, in case of manual database creation with Oracle database, OpsHub database user ("db1") and OpsHub reports database user ("reportsdb") shall be created on the same server. At the time of installation, you need to provide the username and password for the database server.
* In case of Oracle database, passwords for the database users ("db1" and "reportsdb") shall be the same as the password of the server on which they are created.
* If you want to change the tablespace quota for OpsHub database "db1", following query can be used:

```sql
ALTER USER db1 QUOTA <size_of_tablespace> ON users;
```

> **Note:** `"db1"` and `"reportsdb"` are the database/schema/database user names used in the above queries. You can name them differently as per your requirements.
