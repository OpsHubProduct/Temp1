---
title: Common
---

* Impersonation is not supported.

**Entity Specific**

Following are the limitations and behaviors specific to the individual entities in addition to the common:

# Test Case

* Test Parameters having only numeric characters in their name are not supported.
* If Test Case step field like Action or Expected Result contains only image and no text, then Azure DevOps does not render the inline image on user interface. However, the inline image can be seen from history.
* If Test Case step field contains a hyperlink, then Azure DevOps does not allow to click on the link from user interface.
* When updating only test case steps, parameters, and parameter values - Updating only these fields won't be synced to target. To overcome this limitation, it is always recommended to use overwrite option for all these fields while configuring field mapping.

# Test Plan

* REST API–based synchronization is not supported for on-premises instances of Azure DevOps Server prior to version 2020.
* Links of 'Remote Work', 'Release pipeline', 'Build', 'GitHub', 'Git' and 'Wiki' with Test Plan are not supported. Test Run settings, Outcome settings, MTM settings and MTM environments are not supported in Test Plan.
* For TFS version below 2013-Update 3, Test Plan is not supported as a separate entity. Test Plan with few fields will synchronize with Test Suite synchronization. Also, Test Plan with duplicate name will not get synchronized.
* Test Plan as a separate entity is supported from OIM version 7.46. For fresh project synchronization, it is recommended to synchronize Test Plan separately, followed by Test Suite, Test Run and Test Result. After migrating to OIM version >= 7.46 from older version, if you want to synchronize Test Plan separately in running integrations, please refer to [post migration guideline for Test Plan entity support](https://docs.myopshub.com/oim/index.php/Post-Migration_Checklist#Test_Plan_Entity_Support_for_TFS.2FAzure_DevOps).

# Test Suite

* REST API–based synchronization is not supported for on-premises instances of Azure DevOps Server prior to version 2020.
* Test Suite will migrate current state for on-premise instance with version equal and below version 2013 (Update 3) .
* Synchronization of Test Case chart and Test Result chart created within test suite is not supported.
* Query-Based Suite or Requirement-Based Suite.
  * Once a Query-Based Suite or Requirement-Based Suite synced to target system, then after any new linkage of Test-Case with test suite added due to modification in test case. Hence newly added Test-Case linkage of Test Suite will not sync to the target system and any Test Run with corresponding test point will resulted into processing failure. In such case do following click [here](../../connectors/azure-devops.md#troubleshoot) for troubleshoot.
* Any update in Test Suite Configuration will only migrate when test suite is updated.
* Any update in Test Suite Configuration will only synchronize when test suite is updated.
* Ordering in Test Cases which are added to Test Suite is supported only for version 2019 onwards for on-premise deployments (i.e. Team Foundation Server) and all cloud deployments (i.e. Azure DevOps). In addition to that, ordering is only possible when the user has selected authentication type as Personal Access Token in the system configuration. Refer section [Create Personal Access Token](../../connectors/azure-devops.md#create-personal-access-token).
* If source endpoint is Team Foundation Server with version lower than 2017 or target endpoint is not an Azure DevOps, all types of Test Suite (Static/Query based/Requirement) will be migrated as Static Suite.
* If source endpoint is Azure DevOps or on-premise deployment (i.e Team Foundation Server) with version 2017 onwards and target endpoint is Azure DevOps, then the Static suite is migrated as Static Test Suite. The Requirement-based test suite is migrated as Requirement-based test suite and Query-based test suite is migrated as Query-based test suite.
* If source endpoint is Azure DevOps or on-premise deployment (i.e Team Foundation Server) with version 2017 onwards and target endpoint is Azure DevOps, then the Static suite is synchronized as Static Test Suite. The Requirement-based test suite is synchronized as Requirement-based test suite and Query-based test suite is synchronized as Query-based test suite.
* The user of source and target endpoint requires desired access level Basic + Test Plans in end system to synchronize query-based and requirement-based suite. Refer [Access Level](https://docs.microsoft.com/en-us/azure/devops/organizations/security/access-levels?view=azure-devops) to know more about this access level or subscription for the sync user. Otherwise, Test Suite synchronization will be resulted in to job error/sync failure as "You are not authorized to access this API. Please contact your project administrator".
* Synchronization Behavior of **Query Text** field of Query based Test Suite:
  *   The Query based test suite has a field **Query Text** that represents the actual criteria that has been given in the Query Suite entity. The **Query Text** follows a specific format for which you can refer to [WIQL syntax](https://docs.microsoft.com/en-us/azure/devops/boards/queries/wiql-syntax?view=azure-devops).

      * Refer to the section [Synchronization Behavior of fields with WIQL format](https://github.com/OpsHubProduct/OIM-Documentation/blob/main/docs/.gitbook/..connectors/team-foundation-server.md#synchronization-behavior-of-fields-with-wiql-format) to know general synchronization behavior applicable to this type of field. Following are the behavior specific to Query Text field of Test Suite entity:
        * It is recommended to have both source and target endpoints having identical templates (fields, lookups, iteration, areas, etc.) to synchronize the Query Text field of the Query-based suite. Any differences in the template could lead to a mismatch in Test Case association and cause the Test Suite sync failure. It may require the end-user to manually correct the Query Text field of Test Suite in the source or target end system to retry the failure.
          * **User values mentioned in Query Text**
            * Query Text Field with a user type of field clause will be restricted to transform the user(s) not the Group or Team present as part of clause value.
            * The user will be transformed to corresponding target end system user as per user mapping of migration.
            * The user will be transformed to corresponding target end system user as per user mentions mapping of field **Query Text** .
          * **Id values mentioned in Query Text**
            * In the **Query Text** field, an id clause can refer to a particular or set of a work item of type Test Case.
            * The synchronized test case will have a different id in target system than the source entity. Henceforth it is required to transform the id clause as per the target end system to avoid mismatch in the association of Test Case(s) with Test Suite between the source system and target system. By default, the Query Text field with ID field clause will not be changed as per target entity id. Perform following configuration(s) in order to transform ID as per the target end system.
            * Create a custom field with any name but type as Integer for the Test Case entity in the target system.
            * Configure the Remote Id field for Test Case integration using above created custom field prior to synchronize Test Case(s).
            * Configure the following advance mapping for field Query Text to replace ID field with created custom field. Later in this documentation the sample advance mapping to replace ID field with custom field named "Source Workitem ID" is given.
            * If the Type of the above created custom field is "String" then
              * The synchronization of Query Text field with ID clause is restricted to synchronize certain operators which are compatible with String type of field. For example, >, <, =, <=, >=, <>, In, Not In etc. The operator(s) which are only compatible with the Integer type of field and not compatible with the String type of field will cause the sync failure for Test Suite. Such incompatible operators are \[=Field], \[>Filed], \[>=Field], \[<=Field], \[<>Field], etc. The custom field used to replace ID field is of?String?type requires compatible operator and value.
              * It is requires to use the advance workflow of **Default Integration Workflow For TFS to TFS Test Suit.xml** to synchronize the Query Text with ID clause when target end system has custom field "Source Workitem ID" is of String type.
          * **Sample Advance Mapping to replace ID field to custom id field name Source Workitem ID**

      ```xml
      <Query-space-Text  xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
        <xsl:value-of select="utils:transformIdMentioned('Query Text',SourceXML/updatedFields/Property/Query-space-Text,'(\\[ID\\])','[Source Workitem ID]')"/>
      </Query-space-Text>
      ```
  *   **Transform the field clause of Query Text field having different source and target field value(s)**

      * Scenario: Different lookups of field in source and target end system for test case entity.
      * Example, Suppose valid lookups of priority field of source system are 1,2,3,4. whereas priority lookups of target system are 1,2,3. As per the test case mapping the missing look up 4 in target system is mapped to 3.
      * **Sample Query Text of test suite entity of source system** Following is the sample mapping which will transform the Priority field clause of query text field of Test Suite entity as per the given Test Case mapping. After transformation using the below sample mapping, the field clause of **\[Priority] = 4** will be transformed as **\[Priority] = 3**.

      ```sql
      select [System.Id], [System.Title], [System.AssignedTo], [System.AreaPath] 
      from WorkItems 
      where [System.TeamProject] = @project 
        and [System.WorkItemType] in group 'Test Case Category' 
        and [Microsoft.VSTS.Common.Priority] = 4 
        and [System.Id] >= 1 
        and [System.State] = 'Closed' 
        and [System.Reason] = 'Duplicate' 
      order by [System.Id]
      ```
  *   **Expected Query Text to be synchronized in target system**

      ```sql
      select [System.Id], [System.Title], [System.AssignedTo], [System.AreaPath] 
      from WorkItems 
      where [System.TeamProject] = @project 
        and [System.WorkItemType] in group 'Test Case Category' 
        and [Microsoft.VSTS.Common.Priority] = 3 
        and [System.Id] >= 1 
        and [System.State] = 'Closed' 
        and [System.Reason] = 'Duplicate' 
      order by [System.Id]
      ```
  * **Sample Advance mapping for query text for above transformation**
    *   Following is the sample mapping which will transformed Priority field clause of query text field of test suite entity as per the given test case mapping.After transformation using below sample mapping the field clause of \[Priority] = 4 will be transformed as \[Priority] = 3.

        ```xml
        <Query-space-Text>
          <xsl:variable name="xpathQueryText" select="SourceXML/updatedFields/Property/Query-space-Text"/>
          <xsl:variable name="xapthFieldPriority" select="utils:transformWIQLClauseAsPerMapping($xpathQueryText,'Priority','\\[Priority\\] = ([0-9]+),\\[Priority\\] in ([0-9]+)','Test Case Mapping',false(),$sourceSystemId,$targetSystemId)"/>
          <xsl:value-of select="$xapthFieldPriority"/>
        </Query-space-Text>
        ```
  * **About utility method `transformWIQLClauseAsPerMapping`** This method requires the following inputs as mentioned in the following sequence:
  * **Query Text:** Source value of Query Text field which field clause is required to transform as per the target system.
  * **Clause Field Name:** Name of the field which clause needs to match against the following RegEx input.
  * **Clause Match RegExSet:** Comma-separated RegEx to match the possible value part of the given field clause to extract the value from the source query and replace it as per the test case mapping input.
  * **Mapping Name:** Name of valid test case mapping to transform given field clause. This mapping is expected to have mapping for the field name given as part of the second input parameter.
  * **Enclosed Value With Quote:** Boolean parameter indicating whether to have the transformed value within single quotes or not. If invoked as `true()`, the value will be enclosed in single quotes in the resulting query text. If `false()`, then the transformed value will not be enclosed.
  * **Source System Id:** System id of the source end system.
  * **Target System Id:** System id of the target end system.

# **Test Result and Test Run**

* REST API–based synchronization is not supported for on-premises instances of Azure DevOps Server prior to version 2020.
* Test Run and Test Result will migrate current state. Any changes in the target system after synchronization may show inconsistency in data in both end points.
* Following Test Result and Test Run will not synchronize (these Run and Result are logged in <code class="expression">space.vars.SITENAME</code> logs).
  * Run and Result created with Test Suite not existing in the source.
  * Run and Result created with Test Case not associated with the Test Suite while synchronization was performed.
  * Any Run and Result created with Test Case/Configuration, associated with Test Suite after synchronization.
  * Run and Result existing in Plan (e) Automated Run and Result are not supported.
* Below are only for Test Result:
* Synchronization of video format attachment of Result Steps and Result is not supported.
* Synchronization of Parameter Values for Step Results is not happening.
  * Reason: ADO/TFS API limitations. \*'Duration' field will get synchronized only when the value of 'Status' field is 'completed'.
