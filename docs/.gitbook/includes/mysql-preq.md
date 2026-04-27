---
title: mysql-preq
---

* **Supported versions:** From 5.7.18 or above
* **Wait time for connection pool** should be set to 8 hours.

**User permission pre-requisites list:**

| **Privileges**          | **Context**                           | **Installation** | **Upgradation** | **Running** |
| ----------------------- | ------------------------------------- | ---------------- | --------------- | ----------- |
| Alter                   | Tables                                | Yes              | Yes             |             |
| Alter Routine           | Stored routines                       | Yes              | Yes             |             |
| Create                  | Databases, tables, or indexes         | Yes              | Yes             |             |
| Create routine          | Stored routines                       | Yes              | Yes             |             |
| Create tablespace       | Server administration                 | Yes              | Yes             |             |
| Create temporary tables | Tables                                | Yes              | Yes             |             |
| Create view             | Views                                 | Yes              | Yes             |             |
| Delete                  | Tables                                | Yes              | Yes             | Yes         |
| Drop                    | Databases, tables, or views           | Yes              | Yes             |             |
| Execute                 | Stored routines                       | Yes              | Yes             | Yes         |
| File                    | File access on server host            | Yes              | Yes             |             |
| Grant option            | Databases, tables, or stored routines | Yes              | Yes             |             |
| Index                   | Tables                                | Yes              | Yes             |             |
| Insert                  | Tables or columns                     | Yes              | Yes             | Yes         |
| Lock tables             | Databases                             | Yes              | Yes             | Yes         |
| References              | Databases or tables                   | Yes              | Yes             |             |
| Select                  | Tables or columns                     | Yes              | Yes             | Yes         |
| Show view               | Views                                 | Yes              | Yes             | Yes         |
| Update                  | Tables or columns                     | Yes              | Yes             | Yes         |

Once the installation/up-gradation is complete for normal running of OIM, permissions required only for installation and upgradation can be revoked.

**SQL script to grant/validate/revoke User permission:**

| **Operation** | **When OIM installation/upgaradation is responsible for database creation**                                                                                                                                                                                                                                                                                         | **When database is created manually**                                                                                                                                                                                                                                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Grant         | <p><code>GRANT ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES ,CREATE TABLESPACE, FILE, CREATE VIEW, DELETE, DROP, EXECUTE, GRANT OPTION, INDEX, INSERT, LOCK TABLES, REFERENCES, SELECT, SHOW VIEW, UPDATE ON *.* TO 'username'@'localhost';</code><br><br><code>GRANT CREATE TABLESPACE, FILE ON *.* TO 'username'@'localhost';</code></p> | <p><code>GRANT ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE VIEW, DELETE, DROP, EXECUTE, GRANT OPTION, INDEX, INSERT, LOCK TABLES, REFERENCES, SELECT, SHOW VIEW, UPDATE ON database_name.* TO 'username'@'localhost';</code><br><br><code>GRANT CREATE TABLESPACE, FILE ON *.* TO 'username'@'localhost';</code></p> |
| Validate      | `SHOW GRANTS FOR 'username'@'localhost';`                                                                                                                                                                                                                                                                                                                           | `SHOW GRANTS FOR 'username'@'localhost';`                                                                                                                                                                                                                                                                                                              |
| Revoke        | `REVOKE ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE TABLESPACE, FILE, CREATE VIEW, DROP, GRANT OPTION, INDEX, REFERENCES ON *.* FROM 'username'@'localhost';`                                                                                                                                                                     | <p><code>REVOKE ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE VIEW, DROP, GRANT OPTION, INDEX, REFERENCES ON database_name.* FROM 'username'@'localhost';</code><br><br><code>REVOKE CREATE TABLESPACE, FILE ON *.* FROM 'username'@'localhost';</code></p>                                                            |
