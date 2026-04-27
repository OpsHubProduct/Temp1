# Changing MSSQL Server Host

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}
\* Close OM4ADO application before execution of the utility.
{% endif %}

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
* Stop OpsHub Server Service before execution of the utility.
{% endif %}

* Go to <code class="expression">space.vars.SITENAME</code>'s `<Installation Folder>/Other_Resources/Resources`
* Unzip `HostChange.zip`

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
- Open Command Prompt with administrator privileges and go to <code class="expression">space.vars.SITENAME</code>'s directory `<Installation Folder or OpsHub>/Other_Resources/Resources/HostChange` using command **`cd <Installation Folder or OpsHub>/Other_Resources/Resources/HostChange`**
{% endif %}

\* Run \`HostChange.bat\` for Windows system.

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
* In case of linux system, run `HostChange.sh`
{% endif %}

* Enter the path for <code class="expression">space.vars.SITENAME</code>'s Installation Directory

<div align="center"><img src="../../../.gitbook/assets/initial.png" alt=""></div>

### HostChange with MYSQL

* Enter the new Host Name for MYSQL:

<div align="center"><img src="../../../.gitbook/assets/Mysql1.png" alt=""></div>

* If the Host Name input is not entered in the above step, then user will get the notification mentioned in the screen shot below. As the Host Name is a mandatory input that defines the new Host Name you want <code class="expression">space.vars.SITENAME</code> database to refer to:

<div align="center"><img src="../../../.gitbook/assets/Mysql2.png" alt=""></div>

* Enter the Port for MYSQL:

<div align="center"><img src="../../../.gitbook/assets/Mysql3.png" alt=""></div>

* If the Port input is not entered in the above step, then utility will use the existing Port \[entered at a time of <code class="expression">space.vars.SITENAME</code> installation]. If that is not the case, then enter the Port here:

<div align="center"><img src="../../../.gitbook/assets/Mysql4.png" alt=""></div>

* Utility will check the connection with new Host Name:

<div align="center"><img src="../../../.gitbook/assets/Mysql5.png" alt=""></div>

### HostChange with ORACLE

* Enter the new Host Name for ORACLE:

<div align="center"><img src="../../../.gitbook/assets/Oracle21.png" alt=""></div>

* If the Host Name input is not entered in the above step, then user will get the notification mentioned in the screen shot below. As the Host Name is a mandatory input that defines the new Host Name you want <code class="expression">space.vars.SITENAME</code> database to refer to:

<div align="center"><img src="../../../.gitbook/assets/Oracle22.png" alt=""></div>

* Enter the Port for ORACLE:

<div align="center"><img src="../../../.gitbook/assets/Oracle33.png" alt=""></div>

* If the Port input is not entered in the above step, then utility will use the existing Port \[entered at the time of <code class="expression">space.vars.SITENAME</code> installation]. If that is not the case, then enter the Port here:

<div align="center"><img src="../../../.gitbook/assets/Oracle44.png" alt=""></div>

* Utility will check the connection with new Host Name:

<div align="center"><img src="../../../.gitbook/assets/Oracle55.png" alt=""></div>

### HostChange with MSSQL Server

* **Note**: If <code class="expression">space.vars.SITENAME</code> is installed with Windows Authentication mode, then before running the utility, the user needs to make sure that the user who is logged into the Windows \[where the <code class="expression">space.vars.SITENAME</code> is installed] also logs into the new host's MSSQL instance with the same credentials.
* Enter the new Host Name for MSSQL Server:

<div align="center"><img src="../../../.gitbook/assets/MssqlSer1.png" alt=""></div>

* If the Host Name input is not entered in the above step, then user will get the notification mentioned in the screen shot below. As the Host Name is a mandatory input that defines the new Host Name you want <code class="expression">space.vars.SITENAME</code> database to refer to:

<div align="center"><img src="../../../.gitbook/assets/MssqlSer2.png" alt=""></div>

* If the new Host Name is a named instance, then there is no input required for the Port. Hence, after entering the Host Name, utility will check the connection with the new Host:

<div align="center"><img src="../../../.gitbook/assets/MssqlSer3.png" alt=""></div>

* If the new Host Name is a non-named instance, then enter the Port for MSSQL:

<div align="center"><img src="../../../.gitbook/assets/MssqlSer4.png" alt=""></div>

* If the Port input is not entered in the above step, then utility will use the existing Port \[entered at the time of <code class="expression">space.vars.SITENAME</code> installation]. If that is not the case, then enter the Port here:

<div align="center"><img src="../../../.gitbook/assets/MssqlSer5.png" alt=""></div>

* Utility will check the connection with new Host Name \[In the case of SQL Authentication]:

<div align="center"><img src="../../../.gitbook/assets/MssqlSer6.png" alt=""></div>

* Utility will check the connection with new Host Name \[In the case of Windows Authentication]:

<div align="center"><img src="../../../.gitbook/assets/MssqlSer7.png" alt=""></div>

### HostChange with PostgreSQL

* Enter the new Host Name for PostgreSQL:

<div align="center"><img src="../../../.gitbook/assets/postgresql1.png" alt=""></div>

* If the Host Name input is not entered in the above step, then user will get the notification mentioned in the screenshot below. The Host Name is a mandatory input that defines the new Host Name user wants <code class="expression">space.vars.SITENAME</code> database to refer to:

<div align="center"><img src="../../../.gitbook/assets/postgresql2.png" alt=""></div>

* Enter the Port for PostgreSQL:

<div align="center"><img src="../../../.gitbook/assets/postgresql3.png" alt=""></div>

* If the Port's input is not entered in the above step, then the utility will use the existing Port \[entered at the time of <code class="expression">space.vars.SITENAME</code> installation]. If that is not the case, enter the Port as shown in the screenshot below:

<div align="center"><img src="../../../.gitbook/assets/postgresql4.png" alt=""></div>

* Utility will check the connection with the new Host Name:

<div align="center"><img src="../../../.gitbook/assets/postgresql5.png" alt=""></div>
