# Entity Types List

### API URI

This is the URI, OpsHub will execute to call this API:

```bash
GET: /entity-types?projectId=<projectId>
```

### URI Parameters

| **Name**      | **In** | **Required** | **Type** | **Description**                                                                                                                        |
| ------------- | ------ | ------------ | -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **projectId** | Query  | True         | String   | Project id for which list of entity types available need to be returned. ProjectId here will be same as ‘id’ sent as part of /projects |

### Response Payload

```json
[ 

  { 

    "id": "unique identifier for each entity type", 

    "name": "Entity type name that will be visible to user on OpsHub UI", 

          "direction": "SOURCE_ONLY, TARGET_ONLY, BOTH" 

    "pollerType": "CURRENT_STATE, NON_TIME_BASED, ENTITY_WISE_HISTORY" ,

    "isSoftDeleteSupported": "true / false" ,

    "belongsToCategories": "List of Categories in which given Entity Type belongs to" ,

    "projectMovementSupported": "Indicates if movement of the Entity type across projects is supported through API.",

    "isArchiveSupported": "true / false"

  } 

] 
```

### Entity Type Response Parameters

<table data-header-hidden><thead><tr><th></th><th width="100"></th><th width="100"></th><th width="322"></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td><strong>Required</strong></td><td><strong>Type</strong></td><td><strong>Description</strong></td></tr><tr><td><strong>id</strong></td><td>True</td><td>String</td><td>Internal name of the entity. If end system does not have different internal name for an entity type, pass display name here too.</td></tr><tr><td><strong>name</strong></td><td>True</td><td>String</td><td>Display name of the entity.</td></tr><tr><td><strong>direction</strong></td><td>True</td><td>Enum</td><td>In which direction can we sync the data in end system?<br>- <strong>SOURCE_ONLY</strong>: End system is read only<br>- <strong>TARGET_ONLY</strong>: End system is write only<br>- <strong>BOTH</strong>: End system allows both read and write</td></tr><tr><td><strong>pollerType</strong></td><td>True</td><td>Enum</td><td>Types of poller:<br>- <strong>CURRENT_STATE</strong>: Current state will be synced. Set this pollerType if it is possible from API to query entities based on their create and update time.<br>- <strong>NON_TIME_BASED</strong>: Current state will be synced. Set this pollerType if it is not possible from API to query entities based on their create and update time.<br>- <strong>ENTITY_WISE_HISTORY</strong>: Complete entity history will be integrated. Set this pollerType if the end system has APIs to query history (audits) of entities.</td></tr><tr><td><strong>isSoftDeleteSupported</strong></td><td>False</td><td>Boolean</td><td>Set to <strong>true</strong> if end system supports soft delete for the given entity type; else, set it to <strong>false</strong>.</td></tr><tr><td><strong>isArchiveSupported</strong></td><td>False</td><td>Boolean</td><td>Set to <strong>true</strong> if the end system supports archive operation for the given entity type; else, set it to <strong>false</strong>.</td></tr><tr><td><strong>belongsToCategories</strong></td><td>False</td><td>List</td><td>List of categories in which the given entity type belongs.<br>Each category indicates interconvertibility between entity types.<br>For instance, if both "Bug" and "Story" are assigned to the "WorkItems" category, it indicates that these two entity types can be converted mutually.<br>A bug can be transformed into a story, and a story can likewise be converted into a bug.<br><br>There is flexibility to define any category names necessary for sets of entity types that are convertible to each other, with no limit on the number of categories.<br>Category names are case-insensitive (e.g., "workitems" and "WorkItems" are treated as the same).<br>Each category name can have a maximum of 50 characters and can only consists of uppercase letters [A-Z], lowercase letters [a-z], digits [0-9], and underscores [_].<br>However, spaces are not permitted.<br><br><strong>Behavior when belongsToCategories is either null, empty, or has no other entity types in the same category</strong>:<br><br>If the belongsToCategories list is either null or empty, or if a given category has no other associated entity types (for example, if "category1" only has one entity type), and entity type movement is detected, the following actions will take place:<br>the old entity type will be marked as deprecated, and a new entity with the updated entity type will be created in the end system.<br><br><strong>Note</strong>: To assign the belongsToCategories list, all categories that an Entity Type may belong to must be specified from the defined categories.<br>Example:<br><br>Project1: bug, feature,task,story<br>Project2: requirement, task, testplan<br><br>Both conversion of project and Entity type is detected like:<br><br>Old: project1, bug<br>New: project2, requirement<br><br>Since the entity type 'bug' of project1 can be converted to entity type 'requirement' of project2, both these entity types must have at least one category in common.</td></tr><tr><td><strong>projectMovementSupported</strong></td><td>False</td><td>Boolean</td><td>Indicates if the movement of the entity type across projects is supported through API.<br><br><strong>If the given entity type can be moved to any project across instance through API, then this should be true.In other case, this should be false</strong>.<br><br>By default, it will be treated as false.<br><br>Behavior when projectMovementSupported is false:<br>If the <code>projectMovementSupported</code> is false with a given category, and project movement is detected, the following will occur:<br>the old entity present in the old project will be marked as deprecated, and a new entity in the new project will be created in the end system.</td></tr></tbody></table>

### Examples

#### 1) When Entity Type or Project Movement is not supported

```json
[
  {
    "id": "100",
    "name": "Requirement",
    "direction": "BOTH",
    "pollerType": "CURRENT_STATE",
    "isSoftDeleteSupported": "true",
    "isArchiveSupported": "true"
  },
  {
    "id": "BUG",
    "name": "Defect",
    "direction": "BOTH",
    "pollerType": "ENTITY_WISE_HISTORY",
    "isSoftDeleteSupported": "false",
    "isArchiveSupported": "true"
  },
  {
    "id": "200",
    "name": "Feature",
    "direction": "SOURCE_ONLY",
    "pollerType": "CURRENT_STATE",
    "isSoftDeleteSupported": "true",
    "isArchiveSupported": "true"
  }
]
```

#### 2) When Entity Type or Project Movement is supported

In the below example, for Entity Type and project movement scenario is like:

**Requirement**:\
Can be converted to Bug and Feature.\
Can be moved to another project.

**Bug**:\
Can be converted to Requirement only.\
Cannot be moved to another project.

**Feature**:\
Can be converted to Requirement only.\
Can be moved to another project.

**Test Run**:\
Cannot be converted to any other Entity Type.\
Can be moved to another project.

**Story**:\
Cannot be converted to any other Entity Type.\
Cannot be moved to another project.

In this scenario, since there is no Category in common between Bug and Feature, they cannot be converted to each other.

```json
[
  {
    "id": "100",
    "name": "Requirement",
    "direction": "BOTH",
    "pollerType": "CURRENT_STATE",
    "isSoftDeleteSupported": "true",
    "isArchiveSupported": "false",
    "belongsToCategories": ["WorkItemsC1","WorkItemsC2"],
    "projectMovementSupported": "true"
  },
  {
    "id": "BUG",
    "name": "Defect",
    "direction": "BOTH",
    "pollerType": "ENTITY_WISE_HISTORY",
    "isSoftDeleteSupported": "false",
    "isArchiveSupported": "true",
    "belongsToCategories": ["WorkItemsC1"],
    "projectMovementSupported": "false"
  },
  {
    "id": "200",
    "name": "Feature",
    "direction": "SOURCE_ONLY",
    "pollerType": "CURRENT_STATE",
    "isSoftDeleteSupported": "true",
    "isArchiveSupported": "false",
    "belongsToCategories": ["WorkItemsC2"],
    "projectMovementSupported": "true"
  },
  {
    "id": "Test Run",
    "name": "Test Run",
    "direction": "WRITE_ONLY",
    "pollerType": "CURRENT_STATE",
    "isSoftDeleteSupported": "true",
    "isArchiveSupported": "false",
    "belongsToCategories": [],
    "projectMovementSupported": "true"
  },
  {
    "id": "Story",
    "name": "Story",
    "direction": "BOTH",
    "pollerType": "CURRENT_STATE",
    "isSoftDeleteSupported": "true",
    "isArchiveSupported": "false",
    "belongsToCategories": null
  }
]
```
