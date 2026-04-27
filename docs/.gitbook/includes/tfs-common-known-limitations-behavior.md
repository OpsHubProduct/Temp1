---
title: tfs-common-known-limitations-behavior
---

* For the user type of fields synchronization, make sure all the users have signed in the organization at least once or are assigned to any work-item.
  * Reason: ADO\TFS API Limitations.
  * The above behavior has been confirmed with Microsoft. Please refer to the thread for more information: https://developercommunity2.visualstudio.com/t/all-aad-users-not-coming-in-response/1243303?from=email\&viewtype=all#T-ND1246993
* For Team Foundation Server as the target system, if the attachment file name contains **Windows invalid file name characters** (`<`, `>`, `:`, `"`, `/`, `\`, `|`, `?`, `*`), then the invalid Windows characters will be replaced by an underscore (`_`).
  * Reason: ADO\TFS API Limitations.
  * To avoid this replacement, it is recommended to follow file naming conventions as mentioned in [Microsoft File Naming Conventions](https://docs.microsoft.com/en-us/windows/win32/fileio/naming-a-file#naming-conventions).
* For the rich text type of field (HTML) or comments:
  * Entity mention synchronization is not supported for entity type(s) Test Suite, and Test Plan.
  * Entity mention synchronization is not supported for the Team Foundation Server ALM with version < 2015.
  * Default entity mention synchronization option is **Sync source id**. So, migration will migrate source mentioned entity as source id in target.

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}
\* Default entity mention synchronization option is \*\*Sync source id\*\*. So, migration will migrate source mentioned entity as source id in target.
{% endif %}

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
\* Refer \["\*\*Mention Sync Option\*\*"]\(../../integrate/mapping-configuration.md#mention-configuration) for more details.
{% endif %}

* Following fields are read-only, and can be synced from Azure DevOps to other systems.
  * Area Id, Attached File Count, Authorized As, Authorized Date, Board Lane, External Link Count, Hyperlink Count, ID, Iteration Id, Node Name, Related Link Count,Rev, Revised Date, Team Project, Work Item Type, Board Column, Board Column Done
* If a pull request is mentioned in any rich text field or comment of work items or test entities, it may lead to processing failures. In such cases, update the mention settings to use the **Source entity id**.

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}
\* To maintain correct relationships and references \[available among the source data] into target \[through migration], \{{SITENAME\}} migration follows a specific sequence in which the migration is undertaken. The below list will help understand this sequence.

```
1. Meta Entities [User, Group and Team, Area, Iteration]
2. Work Item Entities [Bug, User Story, Task, etc., Test Case, Shared Steps]
3. Test Plan
4. Test Suite
5. Test Run
6. Test Result
7. Query, Dashboard
8. Widgets
9. Commit Information [Changesets] for TFVC (Team Foundation Version Control) Repos

**Note**: Above sequence will also consider the processing failures. The below example will help you understand it.

* If there is any processing failure for 4. [Test Suite migration], then the migration for 5. [Test Run] and 6. [Test Result] will not be started until failures of Test Suite migration are resolved.</div>
```

# Specific Authentication Mode

## Service Principal - Client Secret & Service Principal - Client Certificate

* When these authentication modes are selected, the supported entity types are: Work Items, Build, Pipeline, Areas, Iterations, Test Entities (Test Plan, Test Suite, Test Run, Test Result), Shared Parameter, Git Commit Information.
  * Reason: At present, only these entities use REST APIs. Other entities make use of both REST APIs and the Object Model.
  * > **Note**: Entities not yet supported with Service Principal authentication: Pull Request, Query, Dashboard, Widget, User, Group, and Team.
* The User Mention functionality can be used to mention User, but it does not work for Service Principal.
  * Reason: Azure DevOps does not allow to mention **Service Principal** on UI.
  * > **Note**: When Azure DevOps is configured as the target system, it is recommended that the default user is mapped instead of the Service Principal for **User Mention**. If the Service Principal is mapped, it will not result in failure. However, an email will be sent by Azure DevOps, saying "**ServicePrincipalName** cannot be mentioned. The identity is not configured to receive notifications.
{% endif %}
