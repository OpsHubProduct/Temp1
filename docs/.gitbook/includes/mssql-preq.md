---
title: mssql-preq
---

> **Note**: Azure SQL is an alias for MS SQL on cloud.

* **Supported versions:** 2012 or above
* MS SQL version should support TLS v1.2 protocol or above, as it is recommended to use MS SQL with TLSv1.2 enabled. Refer [this link](https://support.microsoft.com/en-us/topic/kb3135244-tls-1-2-support-for-microsoft-sql-server-e4472ef8-90a9-13c1-e4d8-44aad198cdbe) to upgrade MS SQL server to enable support for TLSv1.2 or above.
* Enable Client protocols **TCP/IP** and **Named pipes** on MSSQLSERVER instance

**User permission pre-requisites list:**

| **Db operation**       | **Privilege**                         | **Installation** | **Upgradation** | **Running** |
| ---------------------- | ------------------------------------- | ---------------- | --------------- | ----------- |
| Create Database/Schema | Create Database, Create Schema        | Yes              |                 |             |
| Update Database/Schema | Alter Database, Alter Schema or Alter | Yes              | Yes             | Yes         |
| Create Table           | CREATE TABLE                          | Yes              | Yes             |             |
| Select in Table        | SELECT                                | Yes              | Yes             | Yes         |
| Insert in Table        | INSERT                                | Yes              | Yes             | Yes         |
| Update table data      | UPDATE                                | Yes              | Yes             | Yes         |
| Delete table data      | DELETE                                | Yes              | Yes             | Yes         |
| Alter Table            | ALTER                                 | Yes              | Yes             | Yes         |
| Drop Table             | ALTER                                 | Yes              | Yes             |             |
| Create View            | CREATE VIEW                           | Yes              | Yes             |             |
| Read View              | SELECT                                | Yes              | Yes             | Yes         |
| Alter View             | ALTER                                 | Yes              | Yes             |             |
| Drop View              | ALTER                                 | Yes              | Yes             |             |
| Create References      | REFERENCES                            | Yes              | Yes             |             |
| Update References      | REFERENCES                            | Yes              | Yes             |             |
| Drop References        | REFERENCES                            | Yes              | Yes             |             |
| Create Procedure       | CREATE PROCEDURE                      | Yes              | Yes             |             |
| Update/Alter Procedure | ALTER                                 | Yes              | Yes             |             |
| Execute Procedure      | EXECUTE                               | Yes              | Yes             | Yes         |
| Drop Procedure         | ALTER                                 | Yes              | Yes             |             |

> **Note**: **ALTER** privilege also required along with other privileges for operation such as create table, create view, drop table/view/procedure, references, etc.

Once the installation/up-gradation is complete for normal running of OIM, permissions required only for installation and upgradation can be revoked.

**SQL script to grant/validate/revoke User permission:**

| **Operation** | **When OIM installation/upgaradation is responsible for database creation**                                                                                                                                                                                                     | **When database is created manually**                                                                                                                                                                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Grant         | <p><code>USE master;</code><br><code>grant Create Database, Create Schema, ALTER, CREATE TABLE, SELECT, INSERT, UPDATE, DELETE, CREATE VIEW, REFERENCES, CREATE PROCEDURE, EXECUTE to username;</code></p>                                                                      | <p><code>USE database_name;</code><br><code>GRANT Create Schema, ALTER, CREATE TABLE, SELECT, INSERT, UPDATE, DELETE, CREATE VIEW, REFERENCES, CREATE PROCEDURE, EXECUTE TO username;</code></p>                                                                                       |
| Validate      | <p><code>USE master;</code><br><code>SELECT pr.principal_id, pr.name , pr.type_desc, pe.state_desc, pe.permission_name FROM sys.database_principals AS pr JOIN sys.database_permissions AS pe ON pe.grantee_principal_id = pr.principal_id WHERE pr.name='username';</code></p> | <p><code>USE database_name;</code><br><code>SELECT pr.principal_id, pr.name , pr.type_desc, pe.state_desc, pe.permission_name FROM sys.database_principals AS pr JOIN sys.database_permissions AS pe ON pe.grantee_principal_id = pr.principal_id WHERE pr.name='username';</code></p> |
| Revoke        | <p><code>USE master;</code><br><code>REVOKE Create Database, Create Schema, CREATE TABLE, CREATE VIEW, REFERENCES, CREATE PROCEDURE FROM username;</code></p>                                                                                                                   | <p><code>USE database_name;</code><br><code>REVOKE Create Schema, CREATE TABLE, CREATE VIEW, REFERENCES, CREATE PROCEDURE FROM username;</code></p>                                                                                                                                    |
