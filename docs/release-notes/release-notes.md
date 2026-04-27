# Release Notes

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
\*\*\*

## Enhancements

### Jira Data Center

* Added support for the Test Run Status field for the XRay Test entity in Jira Data Center.

## Major Bugs

### Common

* Resolved an issue where the "Search Field" text overflowed from the designated area on the mapping screen due to a UI glitch.
* Resolved an issue causing intermittent UI slowness and request delays when <code class="expression">space.vars.SITENAME</code> was installed on Microsoft SQL Server/Azure SQL Server.

### Azure DevOps Server/Services

* Resolved an issue where a job error occurred with the message "Query WIQL text length exceeded the limit. It should contain no more than 32000 characters" when criteria were configured to fetch items between specific IDs (e.g., \[System.Id] > 235022 and \[System.Id] <= 290238).
  * This occurred because Azure DevOps connector internally generated a large list of IDs using an IN query to retrieve the data, which exceeded the WIQL character limit.
* Resolved an issue where a job error occurred while retrieving Test Run data when more than 200 test cases were attached to a run.
* Resolved an issue where a job error occurred while retrieving test results generated from automated runs, where associating a test case, test plan, or test suite is not required.

### Codebeamer

* Resolved an issue where the existing prebuilt JAR for HTML to JSPWiki conversion caused compatibility issues with Codebeamer version 3.2.x due to Codebeamer's internal Apache Tomcat upgrade.
  * A version-specific JAR has been uploaded to the connector documentation page for [Codebeamer](../connectors/codebeamer.md).

### OpenText ALM Quality Center

* Resolved an issue where processing failed with the message "OH-Connector-0070: Error occurred while creating entity because of java.lang.NullPointerException" when the parent item was not synced, causing the item creation to fail under the root folder.

### ServiceNow/ServiceNow Quick Connect

* Resolved an issue where due to recent change in ServiceNow from 7.217 version of <code class="expression">space.vars.SITENAME</code>, post-synchronization re-executed in cyclic manner even if there is no update on the servicenow side.
{% endif %}

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}
\# Major Bugs \* Resolved an issue where a job error occurred while retrieving Test Run data when more than 200 test cases were attached to a run. \* Resolved an issue where a job error occurred while retrieving test results generated from automated runs, where associating a test case, test plan, or test suite is not required.
{% endif %}
