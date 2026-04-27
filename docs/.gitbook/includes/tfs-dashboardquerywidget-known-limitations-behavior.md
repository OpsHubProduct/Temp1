---
title: tfs-dashboardquerywidget-known-limitations-behavior
---

**Common**

* Impersonation is not supported.
* These entities do not have Attachments, Comments, and Inline images, hence these details are not supported.
* These entities do not have historical data, hence historical data synchronization is not supported.

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
\* Criteria based synchronization and target lookup is not supported for Dashboard and Query entity. Refer to \[Criteria Configuration in integration]\(../../integrate/integration-configuration.md#criteria-configuration) and \[Search in Target Before Sync]\(../../integrate/integration-configuration.md#search-in-target-before-sync) to know more on these features. \* Criteria based synchronization is not supported for Query entity. Target lookup is only supported for 'Folder' field, please refer to \[Target lookup query format]\(../../connectors/azure-devops.md#supported-target-lookup-query-for-query-entity) for its target lookup query format.
{% endif %}

**Entity Specific** Following are the limitations and behaviors specific to the individual entities in addition to the common:

**Dashboard Entity**

* Dashboard can be marked as **Favorite**. Synchronization of this **Favorite** attribute is not supported.
  * Reason: ADO/TFS API unavailability

{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
\* Dashboard can be created with \*\*Dashboard Type\*\* as \*\*Project Dashboard\*\* or a \*\*Team Dashboard\*\*. \* For Team Dashboard, \*\*Owned by team\*\* will be applicable and for \*\*Project Dashboard\*\*, \*\*Owner\*\* field will be applicable. \* When Azure DevOps is source: \* Dashboard type details will be available in \*\*Dashboard Type\*\* field (read-only field) \* In case of Project Dashboard, owner details will be available in \*\*Owner\*\* field and \*\*Owned by team\*\* field will contain no value. \* In case of Team Dashboard, owner details will be available in \*\*Owned by team\*\* field and \*\*Owner\*\* field will contain no value. \* When Azure DevOps is target: \* If \*\*Owner\*\* field contains a value, then the dashboard will be created with type \*\*Project Dashboard\*\*. \* If \*\*Owned by team\*\* field contains a value, then the dashboard will be created with type \*\*Team Dashboard\*\*. \* If both fields contain value, then you will get a processing error \[OH-TFS/AzureDevOps-1119]\(../../help-center/troubleshooting/errors/tfs/oh-tfs-azure-devops-1119.md).
{% endif %}

**Query Entity**

* The Queries can contain Fields, Lookup Values, Users, Ids etc. Hence for Query synchronization, please make sure the source and target projects have the same template \[Same fields, lookup values, Users etc ..].
* Synchronization of **Personal Queries** of user is not supported. Only the queries within **Shared Queries** folder & its sub-folders to which integration user has access to will be synchronized.
* A query can be marked as **Favorite**. Synchronization of this **Favorite** attribute is not supported. **Reason:** ADO/TFS API unavailability.
* TFS Query Charts synchronization is not supported. **Reason:** ADO/TFS API unavailability.
* Synchronization Behavior of **WIQL** field:
  * The Query entity has a field WIQL that represents the actual criteria that are given in the Query. The WIQL follows a specific format for which you can refer to [WIQL syntax](https://docs.microsoft.com/en-us/azure/devops/boards/queries/wiql-syntax?view=azure-devops).
  *   Refer to section [Synchronization Behavior of fields with WIQL format](../../connectors/azure-devops.md#synchronization-behavior-of-fields-with-wiql-format) to know general sync behavior applicable to this type of field. Following are the behavior specific to the WIQL field of the Query entity. **User values mentioned in WIQL**

      * Azure DevOps End point Format - User Display Name . **Example:** demouser1 [demouser1@opshub.com](mailto:demouser1@opshub.com)
      * Format being used for processing/synchronization - User Display Name . **Example:** demouser1 [demouser1@opshub.com](mailto:demouser1@opshub.com) \[No change is done here and hence it's expected that User Display Name is same in Source and Target End Point and based on that the user values will be synchronized/visible in the target end point] In case the user with same display name is not available in target end point then the source user display name will be synchronized as text in the WIQL field in the target end system. **For example -** Consider a WIQL: `select [System.ID], [System.WorkItemType] from WorkItems where [System.State] = 'Active' and [System.AssignedTo] in ('demouser1 <demouser1@opshub.com>', 'demouser2 <demouser2@opshub.com>')` This will be synchronized as: `select [System.ID], [System.WorkItemType] from WorkItems where [System.State] = 'Active' and [System.AssignedTo] in ('demouser1 <demouser1@opshub.com>', demouser2)` if no user with user name **demouser2** exists in target end system.

      **Id values mentioned in WIQL**

      * In WIQL, an id of a work item can be referred in the field value.
      * Azure DevOps End point Format - `[ID] [=, <, >, <=, >=, <>, in] [Source entity id].` **Example:** `[ID] = [12345]`
      * Format being used for processing/synchronization - `[ID] = [12345]` \[No change is done here and hence the source work item id will be synchronized/visible in the target end point]
        * In case, you want the Source workitem id to be replaced with its corresponding target id \[Which is synchronized by <code class="expression">space.vars.SITENAME</code>], please use a customized workflow - **Default Integration Workflow - TFS to TFS - Query.xml** \*\*For example \*\* Consider a WIQL: `select [System.ID], [System.WorkItemType] from WorkItems where [System.ID] = 1234 and [System.AssignedTo]` This will be synchronized as: `select [System.ID], [System.WorkItemType] from WorkItems where [System.ID] = 6789 and [System.AssignedTo]` Here, "1234" is the source workitem id and "6789" is the corresponding target work item id.
* Azure DevOps is configured as target:
  * **Folder synchronization**
    * In Azure DevOps, **Query** entities can be organized in different folders.
    * In <code class="expression">space.vars.SITENAME</code>, the field **Folder** corresponds to the folders present in the end system.
    * While Query synchronization, if the Query's folder is not available in target, then <code class="expression">space.vars.SITENAME</code> will first create the folder and then the query will be synchronized to that folder.

## Widget Entity

* **Remote Entity Link** is not supported for Widget entity because in Azure DevOps itself there is no independent URL to access a widget. Refer to [Tracking Link of Entities Across Systems](../../integrate/integration-configuration.md#tracking-id-and-link-of-entities-across-systems) for more information on this feature.
* When Azure DevOps is configured as target:
  * In Azure DevOps, a widget can be only created within a dashboard. Hence, configuring a relationship of type **Dashboard** is mandatory so that widget gets created within that dashboard.
    * A failure [OH-Connector-0059](../../help-center/troubleshooting/errors/common/oh-connector-0059.md) will be generated in case a dashboard is not synchronized and its widget is getting synchronized. In such cases, dashboard must be synchronized first and then widget creation failure should be retried.
* **Configuration field behavior**
  * There can be variety of widgets and each widget can have its own configuration. Widget configuration can be synchronized using **Configuration** field in <code class="expression">space.vars.SITENAME</code>.
* **Widgets re-positioning behavior**
  * A Dashboard has pre-defined number of tiles where widgets can be added or re-positioned.
  * As long as the source and target dashboard have same widgets positioning i.e same position and size, the synchronization will work as per expectation. If the widget positioning differs, synchronization will fail with "widget collision" exception.

**Synchronization behavior when source widgets are re-positioned**

| **Target Widgets operation**                                                                  | **Synchronization Behavior**                                                                 |
| --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| Target widgets are not re-positioned                                                          | Source changes will be synchronized to target                                                |
| Target widgets are re-positioned and any target change is not conflicting with source changes | Source changes will be synchronized to target                                                |
| Target widgets are re-positioned and any target change is conflicting with source changes     | Re-positioning will fail with widget collision exception                                     |
| When target has some new widgets added at non-conflicting positions with source changes       | Sources changed will be synchronized to target and the target added widgets will be retained |
| When target has some new widgets added at conflicting positions with source changes           | Re-positioning will fail with widget collision exception                                     |

*   **Handling widget collisions:**

    * When widgets are re-positioned in source, the dashboard in target needs to be re-positioned as well using following configuration:
      * The **Widget** link must be configured in Dashboard mapping.
    * The dashboard must be re-synchronized through <code class="expression">space.vars.SITENAME</code>.
    * In case of widget collision failure, the user will have to move the existing widget in target to another position, and then retry the processing failure of Dashboard integration in <code class="expression">space.vars.SITENAME</code> to synchronize the widget re-positioning.

    > **Note** Any update on fields - **Position Row, Position Column, Size Row Span and Size Column Span** will be ignored during widget update synchronization.
* **Query Charts used as Dashboard Widgets:**
  * When a chart created using a query is directly added to dashboard without any additional configuration, then the widget will be synchronized without any query link.
    * **Reason:** The API for widget does not provide the required query link information in the above use case.
    * **Solution:** The issue can be resolved by saving these type of widgets on source side without any changes. This will unlink the widget from the chart and link to the original query, providing the correct query link information.
* For accurate ID transformation using [Transformation JSON](../../connectors/azure-devops.md#json-structure-overview), these items must have corresponding target items with the same name - Release, Project, Team, Repository. If not present, those configurations will be synchronized with empty values.
* For widgets with team configurations where the selected teams belong to projects different from the one being synchronized, values for these cross-project teams will be synchronized only in version 2018 and above. **Reason:** API to fetch teams across-project teams is available from version 2018.
* From the widgets provided by Azure DevOps out-of-the-box, following widgets synchronization have some limitations:
  * The Cumulative Flow Diagram widget will be synchronized with empty values in Backlog, Swimlane, and Column fields.
  * The following widgets are not supported by default:
    * Requirements Quality
    * Test Results Trend
    * Test Results Trend (Advanced)
    *   Deployment Status

        > **Note** Since the JSON path for some referenced IDs is not fixed in the above widgets, it is recommended to use regex-based search as given in [Transformation JSON](../../connectors/azure-devops.md#json-structure-overview) section for more accurate results.
