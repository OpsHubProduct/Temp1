# Get Element Type

### Overview

This API describes the element type in detail for OpsHub to be able to integrate various basic and complex data for a given element type.

> **Note**: It is important to return a complete and accurate response for this API, as OpsHub relies heavily on these inputs to automatically handle multiple connector tasks.

### API URI

This is the URI OpsHub will execute to call this API:

```bash
GET: /mbse/api/1.0/element-types?projectId=<projectId>&elementTypeId=<elementTypeId>
```

### URI Parameters

| Name          | In    | Required | Type   | Description                                                                                                                                               |
| ------------- | ----- | -------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| projectId     | query | True     | String | ID of the project for which element type details must be returned. The projectId here will be the same as the id provided in the `/projects` API response |
| elementTypeId | query | True     | String | ‘id’ of element type provided in the 'Element Type Metadata' json.                                                                                        |

### Response Payload

```json

{

  "multiStepUpdate": "NO_SUB_STEPS, STATIC_SUB_STEPS, DYNAMIC_SUB_STEPS",

  "commitStrategy": "COMMIT_TO_MAIN_BRANCH, COMMIT_TO_TEMP_BRANCH_AND_MERGE",

  "history": {

    "type": "FIELD_BASED, FULL_STATE_BASED",

    "revisionDateFormat": "dd/MM/YYYY’T’hh:mm:ss.SSSz",
    
    "revisionUserDataType": "USERNAME_AS_USER, EMAIL_AS_USER",

    "isRevisionIdNumeric": "true/false | datatype: boolean",
    
    "sortableFields":"CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID"

  },

  "elementScope": {

    "additionalScopePropertyName": "property id used as additional scope"

  },
  
  "isTagIdConstantAcrossProjects": "true/false | datatype: boolean",

  "isInternalValueExistForEnumeration": "true/false | datatype: boolean",
  
  "searchElementInfo": {

    "isRecursiveSearchSupported" : "true/false | datatype: boolean",
    
    "sortableFields": "CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID",

    "isGroupingSupported": "true / false",

    "isSearchPossibleOnAnyField": "true / false",

    "isCriteriaInSystemNativeFormat": "true / false",

    "dateTimeFormat": "dd/MM/YYYY’T’hh:mm:ss.SSSz",
    
    "batchSizeForInQuery": "number of entities that can be passed in 'IN' or 'OR' query"

  },

  "comments": {

    "commentElementMetadata": {
      
      "elementTypeId": "id of the element type",
              
      "titlePropertyName": "property name of element in which title of comment is stored",
      
      "bodyPropertyName": "property name of the element in which body of the comment is stored"
      
    },
    
    "commentBodyDataType": "TEXT, HTML, WIKI",
    
    "authorDataType": "USERNAME_AS_USER, EMAIL_AS_USER",
    
    "typesOfComments": [

      "Private",

      "Public",

      "etc."

    ]

  },

  "files": {
    
    "deleteSupported": "true/false | datatype: boolean"
    
  },

  "relations": {

    "deleteSupported": "true/false | datatype: boolean",

    "relationTypes": [

      {

        "relationType": "Name of the relation between current element and the other element",

        "reverseRelationType": "Name of the relation from the other element to the current element.",

        "isMultiRelationAllowed": "true/false | datatype: boolean",

        "isMandatory": "true/false | datatype: boolean"
      }

    ]

  },
  
  "updateLockScope": "ELEMENT, PROJECT, NONE"

}
```

## Response Parameters

| Parent Parameters | Name                 | Required | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------- | -------------------- | -------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                   | multiStepUpdate      | True     | Enum        | <p>Determines whether all properties/tags of an element can be updated in a single update API call or require multiple update calls.<br>If all properties/tags can be updated in a single API call in the end system, pass NO_SUB_STEPS. If the end system provides a separate API to transition an element from one state to another, the connector should pass STATIC_SUB_STEPS or DYNAMIC_SUB_STEPS, depending on the requirement..<br><br>* <em>NO_SUB_STEP</em>: All the fields of an element can be updated in single update element API call.<br><br>* <em>STATIC_SUB_STEPS</em>: Step number of the field to be updated is predefined. So, every time when multiple fields are updated in single update, based on updateStepNumber of field, the order of field can be decided for the update.<br><br>* <em>DYNAMIC_SUB_STEPS</em>: The order in which the fields can be passed to the end system for the update is dynamically decided based on field value. E.g., if the element is getting closed along with few other fields getting updated. In this case, other fields must be updated first and then element status should be updated to closed.</p> |
|                   | commitStrategy       | True     | Enum        | <p>OpsHub uses this flag to identify how changes should be committed in the end system repository. Based on the repository workflow and branching model, the connector specifies whether the changes should be committed directly to the main branch or first committed to a temporary branch and then merged.<br><br>* COMMIT_TO_MAIN_BRANCH: Commits the changes directly to the main branch. This is suitable when direct commits are allowed and revisions can be added to the main branch without additional governance, review, or merge steps.<br><br>* COMMIT_TO_TEMP_BRANCH_AND_MERGE: Changes are first committed to a temporary branch and then merged into the main branch. This is suitable when the end system creates a new revision for every update and revisions need to be introduced into the main branch in a governed or review-based flow.</p>                                                                                                                                                                                                                                                                                               |
| **History**       |                      | False    |             | Pass this parameter, if the pollerType for element type is ENTITY\_WISE\_HISTORY                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|                   | Type                 | True     | Enum        | <p>Specifies how the end system returns element history.<br><br><em>FIELD_BASED</em>: For a given revision, only the properties/tags that changed in that transaction are returned, along with their old and new value.<br><em>FULL_STATE_BASED</em>: For a given revision, the end system returns the element field state for all fields as of that revision.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                   | revisionDateFormat   | True     | String      | Date format for the property/tag, which contains revision date time                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                   | revisionUserDataType | True     | Enum        | <p>Data type of the revision user.<br><br><em>EMAIL_AS_USER</em>: When the user’s email is provided in the revision user property/tag.<br><br><em>USERNAME_AS_USER</em>: When the username is provided in the revision user property/tag.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|                   | isRevisionIdNumeric  | True     | Boolean     | When set to true, revision sorting is performed using the numeric value of the revision ID. When set to false, revision sorting is performed using the string value of the revision ID. Default value is false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                   | sortableFields       | False    | Set`<Enum>` | <p>Set of properties/tags on which the end system supports sorting in the History API. The properties/tags may be provided in any order. The connector must support sorting on all fields specified in this set.<br>Example:<br><code>If end system supports sorting on ENTITY_ID, CREATED_UPDATED_TIME and REVISION_ID:</code> sortableFields = {CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID}<code>&#x3C;br>&#x3C;br> `If end system supports sorting only on CREATED_UPDATED_TIME: `sortableField={CREATED_UPDATED_TIME}</code>.<br>In case of history, CREATED_UPDATED_TIME is same as REVISION_DATE_TIME.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>elementScope</strong></td><td></td><td>False</td><td></td><td>If element scope is decided based on only element type and any additionalScopeField (like a project) is not required, this property can be set to null.</td></tr><tr><td></td><td><strong>additionalScopePropertyName</strong></td><td>True, if elementScope is passed.</td><td>Boolean</td><td>Name of the property that determines additional scope for the element.<br>If the scope depends only on the element type, this value can be set to null.<br>If the scope depends on both the element type and another element property (e.g., projectId, workspaceId, or domainId), provide the name of that property.</td></tr><tr><td></td><td>isTagIdConstantAcrossProjects</td><td>True</td><td>Boolean</td><td>Indicates whether the Tag ID remains the same for the same Tag across different projects.<br><br>Set to true if the Tag ID is consistent across projects.<br>Set to false if the Tag ID differs across projects.<br><br><em>Example</em>:If a Tag with display name Text has ID 100 in Project A and 101 in Project B, set this value to false.<br>If the Tag ID is the same (e.g., Text or 100) across all projects, set this value to true.<br>If set to true, OpsHub will use the Tag ID for mapping. Otherwise, it will use the Tag name.</td></tr><tr><td></td><td>isInternalValueExistForEnumeration</td><td>True</td><td>Boolean</td><td><p>Indicates whether enumeration literals have separate internal and display values.<br><br>Set to 'True' if the enumeration literals have different internal and display values.<br>Set to 'False' if the enumeration literals have only one value, the display value.<br><br>Example 1:<br></p><pre><code>"isInternalValueExistForEnumeration": true
 [ { "id": "low", "value": "Low" }, { "id": "medium", "value": "Medium" }, { "id": "high", "value": "High" } ]
</code></pre><p><br>Here, enumeration literals of priority has values having different internal value and display value.<br><br>Example 2:<br></p><pre><code>"isInternalValueExistForEnumeration": false, [ { "id": "Low", "value": "Low" }, { "id": "Medium", "value": "Medium" }, { "id": "High", "value": "High" } ]
</code></pre><p>Here, the enumeration literals of priority field does not have a different value for internal value.</p></td></tr></tbody></table>

| Parent Parameter      | Name                               | Required | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------------------- | ---------------------------------- | -------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **searchElementInfo** |                                    | True     |             | Contains metadata required for querying the end system to search elements.                                                                                                                                                                                                                                                                                                                                            |
|                       | **isRecursiveSearchSupported**     | False    | Boolean     | Indicates whether the end system supports recursive search functionality. Set this flag to True if the end system allows searching across hierarchical levels (for example, retrieving items from nested folders, child containers, or substructures within a single search operation). Set it to False if recursive or hierarchical search is not supported and only direct-level search is possible.                |
|                       | **sortableFields**                 | False    | Set`<Enum>` | <p>Set of fields for which the end system supports sorting in search operations. Fields may be provided in any order. For searchElementInfo no need to pass REVISION_ID in sortableFields set.<br><em>E.g. If end system supports sorting on both ENTITY_ID and CREATED_UPDATED_TIME,</em><br><code>sortableFields = {ENTITY_ID, CREATED_UPDATED_TIME}</code></p>                                                     |
|                       | **isSearchPossibleOnAnyField**     | True     | Boolean     | <p>Indicates whether the configured search criteria can be stored and executed directly in the end system. Set to true only if the field selected for criteria storage is queryable in the end system. Set to false if search criteria cannot be stored or executed natively in the end system.*<br>To get more details on end system criteria storage, refer [[ Integration_Configuration#Criteria_Configuration</p> |
|                       | **isCriteriaInSystemNativeFormat** | True     | Boolean     | Set to true if the configured criteria in OpsHub will be provided in the end system’s native query format. In this case, the criteria must exactly match the query syntax supported by the end system. Set to false if the criteria will be provided in the standard OpsHub JSON query format.                                                                                                                        |
|                       | **dateTimeFormat**                 | True     | String      | <p>Date time format supported within the query.<br>E.g., (where updatedDate > ‘2021-12-31 00:00:00’). Here, dateTimeFormat should be set as <code>yyyy-MM-dd HH:mm:ss</code></p>                                                                                                                                                                                                                                      |
|                       | **batchSizeForInQuery**            | False    | Integer     | <p>Number of entities end system supports in "IN" or "OR" query. Default will be 250.<br><em>E.g. for IN query:</em> <code>entityId IN (1, 2, 3)</code><br><em>E.g. for OR query:</em> <code>(entityId = 1) OR (entityId = 2) OR (entityId = 3)</code></p>                                                                                                                                                            |

| Parent Parameter | Name                                     | Required | Type           | Description                                                                                                                                                                                                                                                       |
| ---------------- | ---------------------------------------- | -------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **comments**     |                                          | False    |                | Provide this parameter if the end system supports comments as elements for a given element type. If this parameter is included, the MBSE SDK must implement all required Comment APIs. If comments are not supported, this parameter should not be sent.          |
|                  | **commentElementMetadata**               | True     |                | Metadata configuration required when comments are treated as elements in the end system. Defines how comment information is stored and mapped                                                                                                                     |
|                  | commentElementMetadata.elementTypeId     | True     | String         | Identifier of the element type that represents comments in the end system.                                                                                                                                                                                        |
|                  | commentElementMetadata.titlePropertyName | True     | String         | Name of the property of the comment element in which the comment title is stored. If the end system does not support a separate title field, this may be set to null.                                                                                             |
|                  | commentElementMetadata.bodyPropertyName  | True     | String         | Name of the property of the comment element in which the comment body/content is stored                                                                                                                                                                           |
|                  | **commentBodyDataType**                  | True     | Enum           | Data type of the comment body. Supported values: TEXT, HTML, WIKI.                                                                                                                                                                                                |
|                  | **authorDataType**                       | False    | Enum           | Defines how user information should be provided when creating or syncing comments. Use USERNAME\_AS\_USER if the end system expects a username. Use EMAIL\_AS\_USER if the end system expects an email address.                                                   |
|                  | **htmlReplacementForNewLine**            | True     | String         | <p>Exact value for new line character in the comment.<br>Possible values are: ‘<br>’, ‘\n’ or null.</p>                                                                                                                                                           |
|                  | **typesOfComments**                      | True     | List`<String>` | The supported list of comment types. E.g., Internal, External, Work Notes, Additional etc. OpsHub will display these comment types under comment mapping. The user can map comment types across connectors to decide the type of comments they want to integrate. |

| Parent Parameter | Name                | Required | Type    | Description                                                                                                                                                                                                        |
| ---------------- | ------------------- | -------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **files**        |                     | False    |         | <p>Pass this parameter if you want to integrate files for a given element type. Otherwise, do not send the files parameter at all.<br>If this parameter is passed, MBSE SDK must implement all the Files APIs.</p> |
|                  | **deleteSupported** | True     | Boolean | Send true if the end system has an API to delete the file; otherwise, false.                                                                                                                                       |

| Parent Parameter | Name                   | Required | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ---------------- | ---------------------- | -------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **relations**    |                        | False    |         | Provide this parameter if the end system supports element relationships for a given element type. If this parameter is included, all required Relations APIs must be implemented. If relationships are not supported, this parameter should not be sent.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|                  | deleteSupported        | True     | Boolean | Indicates whether the end system allows deletion of an existing relation between elements.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                  | **relationTypes**      | True     |         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                  | relationType           | True     | String  | Name of relation type: Parent, Child, Relates To, Satisfies, Association, etc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                  | reverseRelationType    | True     | String  | Name of its reverse relation. E.g., if the relation type is Parent, then the opposite relationType is Child, i.e. Entity E1 is the parent of element E2, and E2 is the child of E1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|                  | isMultiRelationAllowed | True     | Boolean | <p>Indicates whether multiple relations of this type can be created for a single element.<br><br>True: If multiple relations of this type can be created.<br>False: if only one relation of this type can be created.<br><br>For example: Adding only one parent is allowed to be added for any element, so set multiRelationAllowed to false for Parent Type. On the other hand, for the ‘Related’ relation type, any number of relations can be added, so send true</p>                                                                                                                                                                                                                                      |
|                  | isMandatory            | True     | Boolean | <p>Indicates whether this relation type is mandatory during element creation or update.<br><br>Set to true if at least one relation of this type must exist.<br>Set to false if the relation is optional.<br><br>For example, it might be mandatory to have a Parent relation to another work item for sub-task or task element type. In this case, send true for the Parent relation type for Task</p>                                                                                                                                                                                                                                                                                                        |
|                  | updateLockScope        | True     | Enum    | <p>OpsHub uses this flag to determine the scope at which a lock should be applied during an update operation. This helps prevent concurrent modification conflicts based on how the end system manages updates.<br><br>* ELEMENT: A lock is applied only at the individual element level during update. Other elements within the same project can still be updated concurrently.<br><br>* PROJECT: A lock is applied at the project level. While an element is being updated, other elements within the same project cannot be updated simultaneously.<br><br>* NONE: No explicit lock is applied during update operations. The end system handles concurrency independently or does not require locking.</p> |
