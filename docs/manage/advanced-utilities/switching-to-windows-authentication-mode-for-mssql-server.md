# Switching to Windows authentication

Please go through the section [Installation Prerequisites](../../getting-started/prerequisites.md#windows) for Windows Authentication mode before executing steps given below.

Please ensure the Windows user (who is used in MS SQL Windows Authentication) has **Read** and **Write** privileges before executing `databaseManagementUtlity`. You can grant the **Read** and **Write** privileges by executing the steps given below.

* Open properties window of <code class="expression">space.vars.SITENAME</code> installation folder (directory in which you have installed <code class="expression">space.vars.SITENAME</code> i.e. `c:\Program Files\OpsHub`), it will show you the dialogue box shown below.
* Select the user (to whom you want to grant privileges) from the Security tab and check Read and Write checkbox.
* Click OK after checking the Read and Write checkbox.

<div align="center"><img src="../../../.gitbook/assets/Switching_Image_1.png" alt="" width="600"></div>

If the database is on MSSQL SQL Authentication mode and you need to switch to Windows Authentication mode, then follow the steps given below:

* Go to `<Installation Folder>/Other_Resources/Resources`.
* Unzip `OpsHub Database Management utility.zip`.
* Run `DatabaseManagementUtility.bat` for Windows system.
* In case of Linux system, run `DatabaseManagementUtility.sh`.
* Enter path for the installation directory.

<div align="center"><img src="../../../.gitbook/assets/Switching_Image_2.png" alt="" width="1000"></div>

* Press `2` to switch to Windows authentication mode.

<div align="center"><img src="../../../.gitbook/assets/Switching_Image_3.png" alt="" width="1000"></div>

* Provide Microsoft JDBC Driver 4.0 (`tar.gz`) File Path.

<div align="center"><img src="../../../.gitbook/assets/Switching_Image_4.png" alt="" width="1000"></div>

* Provide Windows Service Credentials.

<div align="center"><img src="../../../.gitbook/assets/Switching_Image_5.png" alt="" width="1000"></div>

> **Note:**\
> If Windows credentials are not added correctly during switching, the OpsHub Server service will not be started.\
> To avoid such an occurrence, the user will have to manually set the service log-on credentials for OpsHub Server Service in case wrong Windows credentials are added at the time of switching.

## Follow the below mentioned steps to set the credentials in the OpsHub Server Services:

1. Open the services application and search for `OpsHub Server Service`.
2. Right-click on the service, select **Properties** and go to the **Log On** Tab.
3. Enter Windows credentials in **This account**.

> If the user is registered with a domain, the username format will be "{username}@{domain}" or "{domain}{username}". Otherwise, the username format will be ".\username".

<div align="center"><img src="../../../.gitbook/assets/OpsHubServerService.png" alt="" width="600"></div>
