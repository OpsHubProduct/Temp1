---
title: docker-update-oim
---

* Stop the existing container, if running:\
  `docker stop CONTAINER <CONTAINER_NAME>`
* Remove the container using the following command:\
  `docker rm -f CONTAINER <CONTAINER_NAME>`
* Take the backup of the database. For more details, refer to [DataBase Backup](../../manage/upgrade/taking-application-backup.md#database-backup) section.
* Take the backup of the docker volume:\
  `docker volume create <BackUp_VolumeName>`\
  `docker run --rm -t -v <Base_VolumeName>:/from -v <BackUp_VolumeName>:/to alpine ash -c "cd /from ; cp -av . /to"`
* Ensure that the backup has been taken correctly.
* Ensure that the OIM\_DB\_TYPE in Input.json is empty.
* Comment out the line mounting the database connector jar by adding `#` symbol before the line in `docker-compose-OIM.yml` file:\
  `# - "@PATH_TO_LOCAL_CONNECTOR_JAR_FILE@:/home/OpsHub_OIM/@CONNECTOR_JAR_IN_DOCKER@"`
*   Update volume name in `docker-compose-OIM.yml` file by `<Base_VolumeName>` and change the value of the external flag to **true**:

    ```
    - <Base_VolumeName>:/home/OpsHub_OIM/OIM

    volumes:
      <Base_VolumeName>:
        external: true
    ```
