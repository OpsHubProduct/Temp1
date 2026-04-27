---
title: manual-mssqldatabase-creation
---

**Collation Considerations**

* For Multiple Language Systems:
  * If your end systems support multiple language characters, it's essential to choose a collation that supports **UTF** characters.
  * To enable UTF character support in <code class="expression">space.vars.SITENAME</code>, install it on **Microsoft SQL Server 2019 or above**.
  * Select a collation with a `UTF` postfix, for example: `Latin1_General_100_CS_AS_SC_UTF8`
* For Single Language Systems:
  * If your end systems utilize a single language and your selected collation includes all the necessary characters and is supported in SQL Server versions below 2019, you can proceed with the installation on SQL Server version below 2019. Select an appropriate collation that suits your end systems \[which are going to be configured in <code class="expression">space.vars.SITENAME</code>].
  * Select an appropriate collation that suits your end systems (which will be configured in <code class="expression">space.vars.SITENAME</code>).
  * Here is [guide](https://learn.microsoft.com/en-us/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver16) that may help you decide the right collation for your database.

> **Note:**\
> We need **1 database** and **2 schemas** to be created manually, out of which The **database and schema name must be the same** for the OpsHub database, and another schema should be created for **reportsdb**.

```sql
drop database IF EXISTS db1
db1 database: create database db1 COLLATE Latin1_General_CS_AS;
db1 schema: create schema db1;
Reports schema: create schema reportsdb;
```
