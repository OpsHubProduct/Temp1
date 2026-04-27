# Updating Database Password

If <code class="expression">space.vars.SITENAME</code> database password has been modified by a user, then this utility would update the new password in <code class="expression">space.vars.SITENAME</code> application.

Follow the steps given below for updating database password in OpsHub:

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
\- Stop OpsHub Server/ Service before execution of this utility.
{% endif %}

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}
\- Close OM4ADO application before execution of the utility.
{% endif %}

\- Go to <code class="expression">space.vars.SITENAME</code> Installation Folder>/Other\_Resources/Resources. - Unzip \`OpsHub Database Management utility.zip\`. - Run \`OpsHubDatabaseManagementUtility.bat\` for Windows system.

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
\- In case of Linux system, run \`OpsHubDatabaseManagementUtility.sh\`.
{% endif %}

* Enter path for OpsHub Installation Directory.

<div align="center"><img src="../../../.gitbook/assets/Updating_Database_Password_Image_1.png" alt="" width="1100"></div>

* Enter the new database password.

<div align="center"><img src="../../../.gitbook/assets/Updating_Database_Password_Image_2.png" alt="" width="1100"></div>

* This would update database password in OpsHub application.

<div align="center"><img src="../../../.gitbook/assets/Updating_Database_Password_Image_3.png" alt="" width="1100"></div>
