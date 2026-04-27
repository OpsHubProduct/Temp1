# Upgrading Application Version

Migration is required from current version to higher version as it includes support and feature enhancement from the older version.

### Migration Pre-requiste for Windows and Linux

Provide the permissions to database user as mentioned in the [Database Selection](../../getting-started/installation.md#database-selection) section on the Installation Steps page.

Follow instruction as mentioned in [Pre-Migration Checklist](pre-migration-checklist.md) before starting the upgradation process based on current version of <code class="expression">space.vars.SITENAME</code> installed and version to which <code class="expression">space.vars.SITENAME</code> will be upgraded. (If you do not have access to the [Pre-Migration Checklist](pre-migration-checklist.md), log a ticket on our customer portal if you have the access or get in touch with your point of contact (POC) for integration.)

#### Best Practices for Memory Allocation in the Upgrade Process

To ensure a smooth and successful migration, especially when handling larger data sets, it is essential to manually configure memory allocation. The default memory allocation might not be sufficient, potentially causing heap memory issues. Follow these best practices to optimize memory settings during the upgrade process:

**1. Review Default Memory Allocation**

By default, the migration process automatically allocates **one-fourth** of the total available RAM. This allocation works for most use cases but might not be enough for larger datasets, leading to potential memory issues.

For example, if the machine has 16GB RAM available and 8GB RAM is allocated to <code class="expression">space.vars.SITENAME</code> at the time of the upgrade, Java will still pick the default 4GB RAM (1/4th of total).

**2. Check Memory Settings in OIM Configuration File**

To confirm that the memory settings align with your requirements, review the following file: `<installation path>\OpsHubServer\conf\OIM_Config.properties`

This file contains the allocated memory settings for running <code class="expression">space.vars.SITENAME</code>.

**3. Set JAVA\_OPTS for Optimal Memory Allocation**

For better stability and performance during migration, manually set the `JAVA_OPTS` environment variable before starting the upgrade process. This allows you to define the initial and maximum memory allocated to the process, ensuring it can handle larger datasets.

**Recommended Configuration (Same as Allocated to** <code class="expression">space.vars.SITENAME</code>**)**

**Where:**

* -Xms2g – Sets the initial memory allocation to 2GB.
* -Xmx8g – Sets the maximum memory allocation to 8GB.

### Migration Steps for Windows

Given below are the migration steps:

* Inactivate all the integrations.
* Stop Server Service from services.ms
* Take back up of the database (refer to the [Taking Application Backup](taking-application-backup.md#database-backup) page).
* Take back up of the application folder (refer to the [Taking Application Backup](taking-application-backup.md#application-backup) page).
* Extract `OpsHubV<version>_Migrator_<OS>.zip` and execute the migration file
* It will ask for existing installation path, give the same installation path where you have installed the application.
* Click Next.
* If you are migrating to version 7.12 or above, you need to register by following the steps mentioned [here](../../getting-started/registration.md).
* Once you click Next, it will show the upgrade information "Product is already installed on given path".
* Click Next to start the product upgrade process.
* Refer [Post Migration Steps](upgrade-application.md#post-migration-steps-for-windows-and-linux) for further steps.

### Migration Steps for Linux

Given below are the migration steps:

#### Pre Migration Steps

* Inactivate all the integrations.
* To stop the Server service, run this command on command prompt **ps -ef | grep "java"** to get the PID and then execute **kill -9 .**
* If you are running <code class="expression">space.vars.SITENAME</code> without service or without root access stop server as described below:
  * Go to "/OpsHubServer/bin" directory and run shutdown.sh file. It will take some time to stop server.
* Take back up of the database (refer to the [Taking Application Backup](taking-application-backup.md) page).
* Take back up of the application folder (refer to the [Taking Application Backup](taking-application-backup.md) page).
* Extract `OpsHubV<version>_Migrator_<OS>.zip.`
* For Silent Migration user needs to register using external utility as described [here](../../getting-started/registration.md#silent-registration-for-linux).
* If you are migrating to version 7.19 or above, Please follow steps described in **Before Installation** section [here](https://github.com/OpsHubProduct/OIM-Documentation/blob/main/docs/getting-started/install/installation-steps.md#launch-the-installer-in-different-operating-systems).

#### Migrate with GUI Access

* Make sure, you have performed the pre-migration steps as described [here](upgrade-application.md#pre-migration-steps).
* Execute the migration file using command **sudo -E sh install.sh**
* You will be prompted to enter the existing installation path. Give the same installation path where you have installed the application.
* If you are migrating to version 7.12 or above, you need to register by following the steps mentioned [here](../../getting-started/registration.md).
* Click Next.
* Refer [Post Migration Steps](upgrade-application.md#post-migration-steps-for-windows-and-linux) for further steps.

#### Migrate without GUI Access (Silent Migration)

To upgrade <code class="expression">space.vars.SITENAME</code> through terminal connection (i.e. Putty), follow the steps given below:

* Make sure, you have performed the pre-migration steps as described [here](upgrade-application.md#pre-migration-steps).
* Modify the external configuration file and export OPSHUB\_AUTO\_INSTALL variable as described at **To Run sh File from External File** section [here](../../getting-started/installation.md#launch-the-installer-in-different-operating-systems).
* Execute the migration file using command **sudo -E sh install.sh**
* Please refer [Possible Error](../../getting-started/installation.md#possible-error-during-silent-installationupgradation) section for trouble shooting error(s) occurred during Upgradation.
* Refer [Post Migration Steps](upgrade-application.md#post-migration-steps-for-windows-and-linux) for further steps.

### Post Migration Steps for Windows and Linux

* After the successful migration, server will start automatically.
* After loading <code class="expression">space.vars.SITENAME</code> UI, please refresh the browser before doing any operation. Verify the version at the bottom of UI.
* Follow the guidelines given in the [Post-Migration-Checklist](post-migration-checklist.md) once the migration process is complete.
* Activate all the integrations.

**Note** : For systems like Azure DevOps Server, OpenText ALM, or Enterprise Architect that require proxy, replace proxy files and re-register services. Refer to Section 2, "Upgrade system proxy," in the Post Migration Checklist.
