---
title: oim-docker-configurations
---

## Docker Volume Creation (Optional)

* It is optional to create docker volume. By default, docker volume will be created by `<Installer_Folder_Name>_opshubData` name.
*   If user wants to create docker volume with customized name, it can be created using the following command:

    ```
    docker volume create <Volume_Name>
    ```

## Input Variables

The variable values need to be added in `Input.json` to configure OIM as Docker.

**Common input variables for all supported databases \[MYSQL, Oracle, MSSQL, PostgreSQL]:**

| Variable Name              | Description                                                                                                                                                                                                                                                                                                                                                | Possible Value                                                                                                    |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `OIM_DB_TYPE`              | Used for configuring OIM with given database type.                                                                                                                                                                                                                                                                                                         | Provide 'MySQL' or 'MS SQL Server' or 'ORACLE' or 'PostgreSQL' based on database type.                            |
| `OIM_DB_CNNECTOR_JAR_PATH` | Path of connector jar present on the host instance. As per database type and version, connector jar needs to be downloaded. Refer [here](https://github.com/OpsHubProduct/OIM-Documentation/blob/main/docs/.gitbook/includes/installation-prerequisites/README.md#download-database-connector-jar) to get the download link of the database connector jar. |                                                                                                                   |
| `OIM_ADV_CONFIG_FLAG`      | Used for performing the advance configuration in OIM.                                                                                                                                                                                                                                                                                                      | Provide either '0' if you don't want to configure advance configuration or '1' to configure advance configuration |
| `OIM_ADV_ISDBFLAG`         | Flag for advance database configuration. Default value: 0                                                                                                                                                                                                                                                                                                  | 0(false) or 1(true)                                                                                               |
| `OIM_ADV_SEC_CONFIG`       | Flag for advance Security configuration. Default value: 0                                                                                                                                                                                                                                                                                                  | 0(false) or 1(true)                                                                                               |
| `OIM_ADV_HTTP_CONFIG`      | Provide 'HTTP' or 'HTTPS' as per configuration requirement. Default value: HTTP                                                                                                                                                                                                                                                                            | 'HTTP' or 'HTTPS'                                                                                                 |
| `OIM_ADV_OPSHUBDBMAME`     | Opshub db name for advance database configuration. This is mandatory when OIM\_ADV\_ISDBFLAG is 1.                                                                                                                                                                                                                                                         |                                                                                                                   |
| `OIM_ADV_REPORT_DBNAME`    | Reports db name for advance database configuration. This is mandatory when OIM\_ADV\_ISDBFLAG is 1.                                                                                                                                                                                                                                                        |                                                                                                                   |

**When `OIM_DB_TYPE` is MYSQL, following are mandatory options:**

| Variable Name     | Description                                                   |
| ----------------- | ------------------------------------------------------------- |
| `OIM_DB_USER`     | Valid username for database connection.                       |
| `OIM_DB_PASSWORD` | Valid password of the given username for database connection. |
| `OIM_DB_HOST`     | Hostname for database connection.                             |
| `OIM_DB_PORT`     | Port number for database connection.                          |

* Sample `Input.json` for MySQL database is mentioned [here](#).

**When `OIM_DB_TYPE` is MS SQL Server, following are mandatory options:**

| Variable Name                 | Description                                                                    |
| ----------------------------- | ------------------------------------------------------------------------------ |
| `OIM_DB_USER`                 | Valid username for database connection.                                        |
| `OIM_DB_PASSWORD`             | Valid password of the given username for database connection.                  |
| `OIM_DB_HOST`                 | Hostname for database connection.                                              |
| `OIM_DB_PORT`                 | Port number for database connection.                                           |
| `OIM_DB_NAME_TO_TEST_CONNECT` | Provide the database name for testing the connection with the database server. |

**When `OIM_DB_TYPE` is ORACLE, following are mandatory options:**

| Variable Name                | Description                                                             |
| ---------------------------- | ----------------------------------------------------------------------- |
| `OIM_DB_USER`                | Valid username for database connection.                                 |
| `OIM_DB_PASSWORD`            | Valid password of the given username for database connection.           |
| `OIM_DB_HOST`                | Hostname for database connection.                                       |
| `OIM_DB_PORT`                | Port number for database connection.                                    |
| `OIM_ORACLE_DB_TYPE`         | Provide 'CDB' or 'Non CDB' as per the configuration of oracle database. |
| `OIM_ORACLE_CONNECTION_TYPE` | Provide 'Service' or 'SID' as per the configuration of oracle database. |
| `OIM_ORC_INSTANCE`           | Provide oracle database instance name.                                  |

**Following points must be considered while adding inputs:**

* If the database is hosted on the same machine where docker is installed, then the `OIM_DB_HOST` must be `host.docker.internal`. It allows us to communicate with the localhost.
* If `OIM_ADV_CONFIG_FLAG` set to 1, the other inputs like `OIM_ADV_ISDBFLAG`, `OIM_ADV_SEC_CONFIG`, `OIM_ADV_HTTP_CONFIG` should be assigned with valid values.
* If `OIM_ADV_ISDBFLAG` flag is set to 1, it indicates the Database Names given in the ADV\_ISDBFLAG section should be created before the actual run.
* If `OIM_ADV_SEC_CONFIG` is set to 1, the inputs in the SECURITY\_CONFIG section should be added with valid values.
* If `OIM_ADV_HTTP_CONFIG` is set to `HTTPS`, the inputs in the ADV\_HTTP\_CONFIG section should be added with valid values.

***

## YAML Inputs

* `docker-compose-OIM.yml` file is used to get required inputs and starts the docker container using docker-compose.
*   The path of updated `Input.json` file in [Input Variables](#input-variables) needs to be mentioned before the colon(:) in `volumes` section of `oim` service in the `services` section. Keep this as it is if YAML file and `Input.json` are in same directory:

    ```
    - "./Input.json:/home/OpsHub_OIM/Input.json"
    ```
*   User needs to provide the local path of database connector jar in place of `@PATH_TO_LOCAL_CONNECTOR_JAR_FILE@` and replace `@CONNECTOR_JAR_IN_DOCKER@` by name of the jar file according to database type. Options for jar file names are given in YAML file.

    ```
    - "@PATH_TO_LOCAL_CONNECTOR_JAR_FILE@:/home/OpsHub_OIM/@CONNECTOR_JAR_IN_DOCKER@"
    ```
*   An example of MySQL database connector jar:

    ```
    - "C:/download/mysql_Connector_5_0_8.jar:/home/OpsHub_OIM/mysql_connector.jar"
    ```
* If docker volume is created in [Docker Volume Creation](#docker-volume-creation-optional) section:
  *   User needs to update the volume name by docker volume (already created) and set the external flag to `true` in volumes section of YAML file:

      ```yaml
      - <Volume_Name>:/home/OpsHub_OIM/OIM

      volumes:
        <Volume_Name>:
          external: true
      ```
