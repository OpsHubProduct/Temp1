# Migrating Database

Please refer to [Database Prerequisites](../../getting-started/prerequisites.md#database-prerequisites) before proceeding with the migration details.

### Introduction

As HSQL is not suitable for production usage, <code class="expression">space.vars.SITENAME</code> needs to be migrated to one of three databases supported by <code class="expression">space.vars.SITENAME</code>. There is a utility provided with <code class="expression">space.vars.SITENAME</code> installation and packaged in <code class="expression">space.vars.SITENAME</code>'s `<Installation Directory>\OpsHub_Resources\DatabaseMigrator` directory \[Migrator directory].

### Steps to migrate from HSQL to other supported databases

* Keep driver for database for which migration needs to be done in: <code class="expression">space.vars.SITENAME</code>'s `<Installation Directory>\OpsHubServer\lib` directory.
  * For MySQL connector driver jar 5.1.8 is not supported, hence the latest connector driver jar should be used from http://dev.mysql.com/downloads/connector/j/5.1.html
* Change `destinationconnection.properties` and `sourceconnection.properties` in Migrator directory:
  * **sourceconnection.properties**: Change `CONNECTION_HSQL_FILE_PATH` property and replace `<installation path>` with installation path
  *   **destinationconnection.properties**: Provide all properties value as guided in file.

      \* Take back up of database

Refer to Database Backup section on [Taking Application Backup](../upgrade/taking-application-backup.md) page for details.

### Migrating on Windows

Run `migrator.bat` in Migrator directory

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
### Migrating on Linux

Run `migrator.sh` in Migrator directory\
If file execution fails with ^M bad interpreter error, use following steps:

* Execute command in terminal `dos2unix migrator.sh`
* Now execute the sh file in terminal `migrator`
{% endif %}

### Steps to perform after successful migration

Following are the steps to be performed after successful database migration:

* Go to <code class="expression">space.vars.SITENAME</code>'s `<Installation Directory>\OpsHubServer\webapps\OpsHubWS\META-INF` directory
* Delete `war-tracker` file
* Go to <code class="expression">space.vars.SITENAME</code>'s `<Installation Directory>\OpsHubServer\webapps\OpsHubWS` directory
* Select all the files and add to archive with name `OpsHubWS.zip`
* Rename `OpsHubWS.zip` to `OpsHubWS.war`
* Go to <code class="expression">space.vars.SITENAME</code>'s `<Installation Directory>\OpsHubServer\webapps` and replace newly created `OpsHubWS.war` with the existing one
* Delete <code class="expression">space.vars.SITENAME</code>'s `<Installation Directory>\OpsHubServer\webapps\OpsHubWS` directory and start the service.
