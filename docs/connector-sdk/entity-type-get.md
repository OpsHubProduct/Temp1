# Entity Type Get

### Overview

This API describes the entity type in detail for OpsHub to be able to integrate various basic and complex data for a given entity type.

> **Note**: It is important to return a correct response for this API as OpsHub relies heavily on these inputs to handle multiple connector tasks automatically.

### API URI

This is the URI OpsHub will execute to call this API:

```bash
GET: /entity-types/{entityTypeId}?projectId=<projectId>
```

### URI Parameters

| Name         | In    | Required | Type   | Description                                                                                                                       |
| ------------ | ----- | -------- | ------ | --------------------------------------------------------------------------------------------------------------------------------- |
| entityTypeId | path  | True     | String | ‘id’ of entity type returned as response of Entity Type – List API                                                                |
| projectId    | query | True     | String | Project id for which entity type details need to be returned. ProjectId here will be the same as ‘id’ sent as part of `/projects` |

### Response Payload

```json

{

  "multiStepUpdate": "NO_SUB_STEPS, STATIC_SUB_STEPS, DYNAMIC_SUB_STEPS",

  "recovery": {

    "type": "FIELD_BASED, COMPARISON_BASED, HISTORY_BASED",

    "fieldName": "// If FIELD_BASED, then id of the field to store last update date"

  },

  "history": {

    "type": "FIELD_BASED, FULL_STATE_BASED",

    "revisionDateFormat": "dd/MM/YYYY’T’hh:mm:ss.SSSz",

    "isRevisionIdNumeric": "true/false | datatype: boolean",

    "revisionUserDataType": "USERNAME_AS_USER, EMAIL_AS_USER",

    "separateHistoryApis": "ATTACHMENTS, COMMENTS, LINKS",

    "sortableFields":"CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID"

  },

  "enitytScope": {

    "additionalScopeFieldName": "field id used as additional scope"

  },

  "entityWebUrl": {

    "baseUrl": "https://example.com/",

    "trailingTemplate": "browse/{0}/{1}",

    "substitutes": {

      "0": "field id of the field whose value need to be first replacement",

      "1": "field name of second replacement field"

    }

  },

  "isFieldIdConstantAcrossProjects": "true/false | datatype: boolean",

  "isInternalValueExistForLookupField": "true/false | datatype: boolean",

  "isUpdateAvailable": "true/false | datatype: boolean",

  "waitTimeInMillisIfApiResponseDelayed": "Max delay in API response in milli seconds. | datatype: number",

  "searchEntityInfo": {

    "sortableFields": "CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID",

    "isGroupingSupported": "true / false",

    "isSearchPossibleOnAnyField": "true / false",

    "isCriteriaInSystemNativeFormat": "true / false",

    "dateTimeFormat": "dd/MM/YYYY’T’hh:mm:ss.SSSz",

    "queryFieldNameInfo": {

      "entityIdFieldName": "entity id field id",

      "entityTypeIdFieldName": "entity type field id",

      "projectIdFieldName": "project id’s field id",

      "createdDateFieldName": "created date’s field id",

      "updatedDateFieldName": "updated date’s field id",

      "createdByFieldName": "created By’s field id"

    },

    "batchSizeForInQuery": "number of entities that can be passed in 'IN' or 'OR' query"

  },

  "fieldNameInfo": {

    "entityIdFieldName": "field id of unique and uneditable entity primary id field",

    "entityTitleFieldName": "field id for entity title",

    "entityDisplayIdFieldName": "field id of field that has entity display id (id any)",

    "entityTypeIdFieldName": "field id for entity type",

    "projectIdFieldName": "field id of field that contains project info for entity",

    "createdDateFieldName": "field id of Created date field",

    "updatedDateFieldName": "field id of updated date field",

    "createdByFieldName": "field id of created By field",

    "updatedByFieldName": "field id of updated By field",

    "archiveMetadata" : {
	
	"archivedByFieldName": "field id of archived By field",

	"isArchivedFieldName": "field id of is Archived field"

     }
	

  },

  "fields": [

    {

      "id": "unique id or key for each field",

      "name": "Field name",

      "dataType": "TEXT, HTML, WIKI, LOOKUP, DATE, DATE_TIME, DATE_STRING, BOOLEAN, NUMBER, USERNAME_AS_USER, TIME_UNIT, EMAIL_AS_USER, RTF, HYPERLINK, TEST_STEP, PARAMETER, REFERENCE, IMAGE, HIERARCHY",

      "isMandatory": "true/false | datatype: boolean",

      "isMultiSelect": "true/false | datatype: boolean",

      "isReadOnly": "true/false | datatype: boolean",

      "isHistorySupported": "true/false | datatype: boolean",

      "userMentionSupported": "true/false | datatype: boolean",

      "entityMentionSupported": "true/false | datatype: boolean",

      "timeUnit": "MILLISECOND, SECOND, MINUTE, HOUR, DAY",

      "dateFormat": " yyyy-MM-dd or yyyy-MM-dd’T’HH:mm:ss.SSSz",

      "canBeSetAtEntityCreateTime": "true/false | datatype:boolean",

      "updateStepNumber": "// Number starting with 1,2,3",

      "inlineFileMetadataForComplexFields": "FIELD_LEVEL_STORAGE",
  
      "referenceFieldMetadata": {
	
		"referencedEntityTypeId": "id of the entity type which is referenced through field",

		"idFieldName": "id field name which stores id or URL of the referenced entity in Entity - GET API and History - List API for base entity",

		"referenceUrl": {

			 "baseUrl": "https://example.com/",

			 "trailingTemplate": "browse/{0}/{1}",

   			 "substitutes": {

     	 			"0": "field id of the field whose value need to be first replacement",

      				"1": "field id of the field whose value need to be second replacement"

    			}

		},

		"titleFieldName": "title field name which stores title or equivalent field of the referenced entity in the Entity - GET API and History - List API for base entity"        

       },
      
      "additionalFieldMetaData": {
        
        "richTextDataType": "An additional meta of field to determine rich text data type of field.",
        
        "stepExecutionType": "An additional meta of field to store execution behavior of Test Step field"
      }

    },

    {

      "id": "unique id or key for each field",

      "name": "Field name",

      "dataType": "TEXT, HTML, WIKI, LOOKUP, DATE, DATE_TIME, DATE_STRING, BOOLEAN, NUMBER, USERNAME_AS_USER, TIME_UNIT, EMAIL_AS_USER, RTF, HYPERLINK, TEST_STEP, PARAMETER, REFERENCE, IMAGE, HIERARCHY",

      "isMandatory": "true/false | datatype: boolean",

      "isMultiSelect": "true/false | datatype: boolean",

      "isReadOnly": "true/false | datatype: boolean",

      "isHistorySupported": "true/false | datatype: boolean",

      "userMentionSupported": "true/false | datatype: boolean",

      "timeUnit": "MILLISECOND, SECOND, MINUTE, HOUR, DAY",

      "dateFormat": "yyyy-MM-dd or yyyy-MM-dd’T’HH:mm:ss.SSSz",

      "canBeSetAtEntityCreateTime": "true/false | datatype:boolean",

      "updateStepNumber": "// Number starting with 1,2,3",

      "inlineFileMetadataForComplexFields": "FIELD_LEVEL_STORAGE",
  
      "referenceFieldMetadata": {
	
		"referencedEntityTypeId": "id of the entity type which is referenced through field",

		"idFieldName": "id field name which stores id or URL of the referenced entity in Entity - GET API and History - List API for base entity",

		"referenceUrl": {

			 "baseUrl": "https://example.com/",

			 "trailingTemplate": "browse/{0}/{1}",

   			 "substitutes": {

     	 			"0": "field id of the field whose value need to be first replacement",

      				"1": "field id of the field whose value need to be second replacement"

    			}

		},

		"titleFieldName": "title field name which stores title or equivalent field of the referenced entity in the Entity - GET API and History - List API for base entity"        

       },
      
      "additionalFieldMetaData": {
        
        "richTextDataType": "An additional meta of field to determine rich text data type of field.",
        
        "stepExecutionType": "An additional meta of field to store execution behavior of Test Step field"
      }
      
    }

  ],

  "comments": {

    "userMentionSupported": "true/false | datatype: boolean",

    "entityMentionSupported": "true/false | datatype: boolean",

    "commentBodyDataType": "TEXT, HTML, WIKI",

    "commentIdDataType": "NUMBER, TEXT",

    "createdUpdatedByFieldDataType": "USERNAME_AS_USER, EMAIL_AS_USER"

    "htmlReplacementForNewLine": "<br/> or \n or null",

    "delayInCommentUpdateTimeInMillis": 2000,

    "createUpdateDateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ",

    "typesOfComments": [

      "Private",

      "Public",

      "etc."

    ],

    "fieldNameInfo": {

      "idFieldName": "Field name of comment id as it is received in API by end system",

      "titleFieldName": " Field name of comment title as it is received in API by end system ",

      "bodyFieldName": " Field name of comment body as it is received in API by end system ",

      "createdDateFieldName": " Field name of comment created date as it is received in API by end system ",

      "updatedDateFieldName": " Field name of comment updated date as it is received in API by end system ",

      "createdByFieldName": " Field name of comment created by as it is received in API by end system ",

      "updatedByFieldName": " Field name of comment updated by as it is received in API by end system ",

      "commentTypeFieldName": " Field name of comment type as it is received in API by end system "

    }

  },

  "attachments": {

    "updateSupported": "true/false | datatype: boolean",

    "deleteSupported": "true/false | datatype: boolean",

    "historySupported": "true/false | datatype: boolean",

    "createUpdateDateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ",

    "typesOfAttachments": [

      "Internal",

      "External",

      "etc."

    ],

    "fieldNameInfo": {

      "idFieldName": " Field name of attachment id as it is received in API by end system ",

      "contentUriFieldName": " Field name of attachment content URI as it is received in API by end system ",

      "renderUriFieldName": " Field name of attachment render URI as it is received in API by end system ",

      "fileNameFieldName": " Field name of attachment file name as it is received in API by end system ",

      "contentTypeFieldName": " Field name of attachment content type as it is received in API by end system ",

      "contentLengthFieldName": " Field name of attachment length as it is received in API by end system ",

      "createdOrUpdatedDateFieldName": " Field name of attachment updated as it is received in API by end system ",

      "createdByFieldName": " Field name of attachment created by as it is received in API by end system ",

      "attachmentTypeFieldName": " Field name of attachment type as it is received in API by end system ",

      "fileCommentFieldName": " Field name of the attachment file comment as it is received in API by end system "

    }

  },

  "inlineFiles": {

    "deleteSupported": "true/false | datatype: boolean",

    "inlineFileStorageType": "ENTITY_LEVEL_STORAGE | EXTERNAL_STORAGE",

    "inlineFileUrlPrefix": ""

  },

  "links": {

    "deleteSupported": "true/false | datatype: boolean",

    "historySupported": "true/false | datatype: boolean",

    "createUpdateDateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ",

    "rank": {

        "rankType": "FLAT_SINGLE | FLAT_MULTIPLE | HIERARCHY_SINGLE | HIERARCHY_MULTIPLE",

        "supportedRankOperations": [

            "MOVE_BEFORE",

            "MOVE_AFTER",

            "LAST_IN_LIST",

            "MOVE_BULK_AFTER"
        ],

        "rankFieldName": "If entity stores the rank info in a field, provide that field name.",

        "rankScope": {

            "template": "{0}::{1}",

            "substitutes": {

                "0": "field name of the field whose value needs to be replacement for 0",

                "1": "field name of the field whose value needs to be replacement for 1"

            }

        }

    },

    "linkTypes": [

      {

        "linkType": "Name of the link between current entity and the other entity",
 
        "linkTypeInternalName": "Applicable only if end system returns or expects internal name of the link.",
        
        "linkTypeDirection": "Applicable only if end system supports directions in links. Possible values are FORWARD and BACKWARD.",

        "reverseLinkType": "Name of the link from the other entity to the current entity.",

        "isMultiLinkAllowed": "true/false | datatype: boolean",

        "isLinkMandatory": "true/false | datatype: boolean",

        "isBulkLinkingSupported": "true/false | datatype: boolean",

        "isExternalLink": "true/false | datatype: boolean"

      }

    ],

    "fieldNameInfo": {

      "linkTypeFieldName": "Field name of link type (parent, child, related etc.) as it is received in API by end system ",

      "linkTypeDirectionFieldName": "Field name of link direction(FORWARD, BACKWARD). Applicable only if link direction is supported by end system.",
      
      "linkedEntityIdFieldName": "Field name of linked entity id as it is received in API by end system ",

      "linkedEntityTypeFieldName": "Field name of linked entity type as it is received in API by end system ",

      "linkedEntityScopeIdFieldName": "linkedEntityScopeId | TODO: Revisit this",

      "createdDateFieldName": "Field name of link created date as it is received in API by end system ",

      "createdByFieldName": "Field name of link created by user as it is received in API by end system ",

      "linkCommentFieldName": "Field name of link comment as it is received in API by end system ",

      "externalLinkUrlFieldName": "Field name of link external URL as it is received in API by end system ",

      "isExternalLinkFieldName": "Field name of field which says if it’s an external link or not, as it is received in API by end system "

    }

  },

"userMention": {

    "userMentionDataType": "USERNAME_AS_USER / EMAIL_AS_USER",

    "mentionDetails": [

      {

        "fieldDataType": "HTML",

        "selectorOrRegex": ["Example: a[href]"],

        "mentionTemplate": "Example: <a href=\"https://example.com/users/${username}\" rel=\"${username}\"> ${displayName} </a>",

        "userDataRegex": "",

        "userDataAttributeName": "Example: href / rel / data-mention"

      },

      {

        "fieldDataType": "WIKI",

        "selectorOrRegex": "Example: [~ohusermention:(.*?)]",

        "mentionTemplate": "Example: [~accountId:${username}]"

      },

      {

        "fieldDataType": "TEXT",

        "selectorOrRegex": "Example: @OH_USER@ohusermention:(.*?)@OH_USER@",

        "mentionTemplate": "Example: ${username} <${email}>"

      }

    ]

  },

  "entityMention": {

      "mentionDetails": [

        {

          "fieldDataType": "HTML",

          "selectorOrRegex": ["Example: a[href]"],

          "mentionTemplate": "Example: <a href=\"https://example.com/users/${username}\" rel=\"${username}\"> ${displayName} </a>",

          "entityIdAttribute": {

            "dataAttributeName": "href",

            "dataRegEx": "/browse/([A-Z_a-z0-9-]+)"
          },

          "entityTypeAttribute": {

            "dataAttributeName": "href",

            "dataRegEx": ".*\\?detail=/(.*?)(?=/\\d+)"
          },

          "entityProjectAttribute": {

            "dataAttributeName": "href",

            "dataRegEx": ".*([a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12})/_workitems/edit/.*"
          }

        }

      ],
      "entityURLDetails": [

       {
          "entityWebURLMatcher": "a[href~=/browse/[A-Z_a-z0-9-]+-\\d+]",

          "entityIdDataSelector": ".*\\/browse/([A-Za-z0-9-]+-\\d+)]"
       }

      ]

    }

}
```

> **Internal note:** For attachment, comment, link: `readSupported`, `writeSupported` can be derived from sync direction of entityType.

## Response Parameters

| Parent Parameters | Name                 | Required                            | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------- | -------------------- | ----------------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                   | multiStepUpdate      | True                                | Enum        | <p>OpsHub uses this flag to identify if all fields can be updated in single update entity call or multiple update entity calls are required. For example: If all the fields under fields can be updated in single API call in end system, then pass NO_SUB_STEP. But let’s say, if the end system has a separate API to transition entity from one state to another, then connector can pass STATIC_SUB_STEPS or DYNAMIC_SUB_STEPS depending on need. If ‘DYNAMIC_SUB_STEPS‘ is being passed, then /entities/{entityTypeId}/sub-steps-for-update API is mandatory to implement.<br><br>* <em>NO_SUB_STEP</em>: All the fields of an entity can be updated in single update entity API call.<br><br>* <em>STATIC_SUB_STEPS</em>: Step number of the field to be updated is predefined. So, every time when multiple fields are updated in single update, based on updateStepNumber of field, the order of field can be decided for the update.<br><br>* <em>DYNAMIC_SUB_STEPS</em>: The order in which the fields can be passed to the end system for the update is dynamically decided based on field value. E.g., if the entity is getting closed along with few other fields getting updated. In this case, other fields must be updated first and then entity status should be updated to closed.</p> |
| **recovery**      |                      | True                                |             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                   | Type                 | True                                | Enum        | <p>Helps OpsHub determine if the given transaction has already taken place in failure and recovery scenarios.<br><br><em>HISTORY_BASED</em>: (Preferred) Entity History – Get (/entities/{entityTypeId}/history) must be implemented, if this is passed. OpsHub will use the entity revision to identify if a given transaction was completed or not.<br><em>FIELD_BASED</em>: Add a custom field of type text to end system (E.g., oh_last_update) to perform recovery. Ensure this field is passed under ‘fields’ of this API.<br><br><em>COMPARISON_BASED</em>: This is a less reliable recovery mechanism as compared to HISTORY_BASED or FIELD_BASED. OpsHub compares last entity state saved in its database with current state in end system, to determine if last transaction was completed or not.<br><br><strong>Select this recovery mechanism if the pollerType for entity type is NON_TIME_BASED.</strong></p>                                                                                                                                                                                                                                                                                                                                                                              |
|                   | fieldName            | True, if recovery type=FIELD\_BASED | String      | In case of FIELD\_BASED recovery, the field id of the custom field can be used by OpsHub for storing recovery flags. (E.g., oh\_last\_update). Note: This field should not be updated by other users in the end system.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **History**       |                      | False                               |             | Pass this parameter, if the pollerType for entity type is ENTITY\_WISE\_HISTORY                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                   | Type                 | True                                | Enum        | <p>How the end system returns entity history?<br><br><em>FIELD_BASED</em>: In a given revision, the old and new values are obtained only for those fields of an entity that were changed in a given transaction.<br><em>FULL_STATE_BASED</em>: For a given revision, the end system returns the entity field state for all fields as of that revision.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|                   | revisionDateFormat   | True                                | String      | Date format for the field, which contains revision date time                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|                   | isRevisionIdNumeric  | True                                | Boolean     | When true, all the revision sorting will happen considering numeric value of revision id. When false, all the revision sorting will happen considering string value of revision id. Default will be false                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                   | revisionUserDataType | True                                | Enum        | <p>Data type of the revision user.<br><br><em>EMAIL_AS_USER</em>: When the user’s email is provided in the revision user field.<br><br><em>USERNAME_AS_USER</em>: When the username is provided in the revision user field.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                   | separateHistoryApis  | False                               | String      | <p>This is an optional input. Provide only if the end system has a separate history API for attachments, comments and/or links.<br>If separate history APIs is available for attachments, comments and/or links, provide the following as per API availability:<br><br><em>ATTACHMENTS</em>: When separate history API for attachments is available.<br><br><em>COMMENTS</em>: When separate history API for comments is available.<br><br><em>LINKS</em>: When separate history API for links is available.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                   | sortableFields       | False                               | Set`<Enum>` | <p>Send set of fields for which end system supports sorting on history API. The fields can be sent in any order in the list. Connector should sort all the fields provided in the set.<br>Example:<br><code>If end system supports sorting on ENTITY_ID, CREATED_UPDATED_TIME and REVISION_ID:</code> sortableFields = {CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID}<code>&#x3C;br>&#x3C;br> `If end system supports sorting only on CREATED_UPDATED_TIME: `sortableField={CREATED_UPDATED_TIME}</code>.<br>In case of history, CREATED_UPDATED_TIME is same as REVISION_DATE_TIME.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>entityScope</strong></td><td></td><td>False</td><td></td><td>If entity scope is decided based on only entity type and any additionalScopeField (like a project) is not required, this field can be set to null.</td></tr><tr><td></td><td><strong>additionalScopeFieldName</strong></td><td>True, if entityScope is passed.</td><td>Boolean</td><td>If entity scope is decided based on only entity type, this field can be set to null.<br>If entity scope is dependent on entity type as well as any other field of the entity (e.g., projectId, workspaceId, or domainId), provide that field name of the entity.<br>Ensure that this field name matches one of the field names in “entityFieldNameInfo”.</td></tr><tr><td><strong>entityWebUrl</strong></td><td></td><td>False</td><td></td><td>Pass this if you want the Remote Entity Link feature enabled for the connector. Otherwise, do not include entityWebURL in response.</td></tr><tr><td></td><td><strong>baseUrl</strong></td><td>True</td><td>String</td><td>String containing the base URL of the end system.<br>e.g., if the actual URL format is "https://example.com/browse/{0}/{1}" then set baseUrl as "https://example.com/" and trailingTemplate as "browse/{0}/{1}".<br>This URL is used to form the Remote Link. If value for the field "Base URL for Remote Link" is not given in the system configuration form, the baseUrl will be used by default to form Remote Link.</td></tr><tr><td></td><td><strong>trailingTemplate</strong></td><td>True</td><td>String</td><td>String template containing the trailing part of the URL format.<br>Provide all the dynamic parts in the URL as substitute numeric variables, e.g., {0}, {1} etc.<br>e.g., If the projectId is 101 and entity is 10001, the base URL is https://example.com/ and trailingTemplate is browse//.<br>So, the actual web URL will be "https://example.com/browse/101/10001".</td></tr><tr><td></td><td><strong>substitutes</strong></td><td>True</td><td>List</td><td>Map containing all the substitute numeric parameters to the replacement field name of the entity.<br>e.g., {"0": "projectIdFieldName", "1": "entityIdFieldName"}<br><br>In the “trailingTemplate":<br>* The value of parameter {0} will be replaced with actual value coming in field project id for the entity.<br>* The value of parameter {1} will be replaced with actual value coming in entity id for the entity.<br>Ensure that this field name matches one of the field names in “fieldNameInfo”.</td></tr><tr><td><strong>isFieldIdConstantAcrossProjects</strong></td><td></td><td>True</td><td>Boolean</td><td>Set to 'True' if the field id for the same field is same in different projects; else, set to 'False'.<br>e.g., If for a field with the display name 'Priority', field id in Project A is '100' and for Project B is '101', then send 'False'.<br>On the other hand, if the field id is the same (say 'priority' or '100') for all projects, then send 'True'.<br><br>If this is 'True', in FieldsMeta, we will use Field Id; otherwise, we will use Field Name.</td></tr><tr><td><strong>isInternalValueExistForLookupField</strong></td><td></td><td></td><td>Boolean</td><td><p>Set to 'True' if the lookup fields have different internal and display values.<br>Set to 'False' if the lookup fields have only one value, the display value.<br><br>Example 1:<br></p><pre><code>"isInternalValueExistForLookupField": true
 [ { "id": "low", "value": "Low" }, { "id": "medium", "value": "Medium" }, { "id": "high", "value": "High" } ]
</code></pre><p><br>Here, priority field has values having different internal value and display value.<br><br>Example 2:<br></p><pre><code>"isInternalValueExistForLookupField": false, [ { "id": "Low", "value": "Low" }, { "id": "Medium", "value": "Medium" }, { "id": "High", "value": "High" } ]
</code></pre><p>Here, the priority field does not have a different value for internal value.</p></td></tr></tbody></table>

| Parent Parameter                         | Name | Required | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------------------------- | ---- | -------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **isUpdateAvailable**                    |      | False    | Boolean | <p>Set to 'True' if update is possible on the entity.<br>Set to 'False' if entity is create only.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **waitTimeInMillisIfApiResponseDelayed** |      | False    | Number  | <p>In some systems, there is a delay in API returning updated data in response.<br><br>e.g., If an entity is updated:<br>* If within next second we try to fetch list of entities, the system might not return the last updated entity.<br>But if we get the list of updated entities after 2 seconds, the system will start returning the entities.<br>This delay might be due to indexing in the end system.<br><br>* Similarly, for history based systems, if we update an entity:<br>The last revision might not be available in the audit API within a second or two.<br>But if we query the revisions after 3 seconds, the system will start returning the revision.<br>This delay might be due to system inserting audit records separately than the actual entity update.<br><br>OIM handles this type of delays for update up to 2 seconds (2000 milliseconds).<br>* If the end system has delay of up to 2 seconds, the value can be kept null.<br>* If the end system has delay of more than 2 seconds, provide the maximum delay value in milliseconds in this field.</p> |

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>searchEntityInfo</strong></td><td></td><td>True</td><td></td><td>All the metadata for querying end system to search entities.</td></tr><tr><td></td><td><strong>sortableFields</strong></td><td>False</td><td>Set<code>&#x3C;Enum></code></td><td>Send set of fields for which end system supports sorting. For searchEntityInfo no need to pass REVISION_ID in sortableFields set.<br><em>E.g. If end system supports sorting on both ENTITY_ID and CREATED_UPDATED_TIME,</em><br><code>sortableFields = {ENTITY_ID, CREATED_UPDATED_TIME}</code></td></tr><tr><td></td><td><strong>isGroupingSupported</strong></td><td>True</td><td>Boolean</td><td>True (Preferred) if end system support order by for both created/updated time and entity id fields, otherwise false. If it is false, OpsHub will sort the results.</td></tr><tr><td></td><td><strong>isSearchPossibleOnAnyField</strong></td><td>True</td><td>Boolean</td><td>If criteria storage needs to be in the end system, then only set the field to true.<br><em>The field selected for end system criteria should be queryable. If that's true, pass true here.</em><br>To get more details on end system criteria storage, refer [[ Integration_Configuration#Criteria_Configuration</td></tr><tr><td></td><td><strong>isCriteriaInSystemNativeFormat</strong></td><td>True</td><td>Boolean</td><td>Send 'True' if configured criteria in OIM will be in the end system native query format.<br>If 'Yes', the criteria can be the exact query that the end system supports.<br>If 'No', the criteria should be OpsHub standard JSON format query.</td></tr><tr><td></td><td><strong>dateTimeFormat</strong></td><td>True</td><td>String</td><td>Date time format supported within the query.<br>E.g., (where updatedDate > ‘2021-12-31 00:00:00’). Here, dateTimeFormat should be set as <code>yyyy-MM-dd HH:mm:ss</code></td></tr><tr><td></td><td><strong>queryFieldNameInfo</strong></td><td>False</td><td></td><td><p>Query field names should be provided for entity id, entity type id, project id, created date, updated date and created by field.<br>If the query field name for the above fields is the same as their field id given in 'fieldNameInfo', then set this field as 'Null'. Otherwise, provide the end system field names used for querying. If these field names are provided, they will be used to generate queries. Here is a sample format of data to be passed under this parameter:<br></p><pre><code>"entityIdFieldName": "entity id field id",
  "entityTypeIdFieldName": "entity type field id",
  "projectIdFieldName": "project id’s field id",
  "createdDateFieldName": "created date’s field id",
  "updatedDateFieldName": "updated date’s field id",
  "createdByFieldName": "created by field id"
</code></pre></td></tr><tr><td></td><td><strong>batchSizeForInQuery</strong></td><td>False</td><td>Integer</td><td>Number of entities end system supports in "IN" or "OR" query. Default will be 250.<br><em>E.g. for IN query:</em> <code>entityId IN (1, 2, 3)</code><br><em>E.g. for OR query:</em> <code>(entityId = 1) OR (entityId = 2) OR (entityId = 3)</code></td></tr></tbody></table>

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>fieldNameInfo</strong></td><td></td><td>True</td><td></td><td>Provide the end system field details for all the fields that need to be integrated</td></tr><tr><td></td><td></td><td></td><td></td><td>For below fields, specify name of the field under which OpsHub will get or send given information for an entity from SDK</td></tr><tr><td></td><td><strong>entityIdFieldName</strong></td><td>True</td><td>String</td><td>Name of the field that contains a unique and uneditable primary id of the entity</td></tr><tr><td></td><td><strong>entityTitleFieldName</strong></td><td>False</td><td>String</td><td>Name of the field that contains title of the entity (For e.g. name, title, summary). Provide this input only if field is to be synchronized as reference field.</td></tr><tr><td></td><td><strong>entityDisplayIdFieldName</strong></td><td>True</td><td>String</td><td>Name of the field that contains a user friendly id of the entity (For e.g. in Jira Issue Key will be entity display field and Issue Id will be entity id)</td></tr><tr><td></td><td><strong>entityTypeIdFieldName</strong></td><td>True</td><td>String</td><td>Name of the field that contains type (Requirement, Bug, etc.) of the entity</td></tr><tr><td></td><td><strong>projectIdFieldName</strong></td><td>True</td><td>String</td><td>Name of the field that contains the project id in which the entity exists</td></tr><tr><td></td><td><strong>createdDateFieldName</strong></td><td>True</td><td>String</td><td>Name of the field that contains the created date of the entity</td></tr><tr><td></td><td><strong>updatedDateFieldName</strong></td><td>True</td><td>String</td><td>Name of the field that contains the last updated date of the entity</td></tr><tr><td></td><td><strong>createdByFieldName</strong></td><td>True</td><td>String</td><td>Name of the field that contains the created by user details of the entity</td></tr><tr><td></td><td><strong>updatedByFieldName</strong></td><td>True</td><td>String</td><td>Name of the field that contains the updated by user details of the entity</td></tr><tr><td></td><td><strong>archiveMetadata</strong></td><td>False</td><td>Object</td><td><p>Pass this metadata if the entity supports archive operation.<br></p><pre><code>"archiveMetadata": {
  "archivedByFieldName": "Name of the field that contains Archived by User details of the entity",
  "isArchivedFieldName": "Name of the field that contains If Entity is Archived details of the entity"
}
</code></pre></td></tr></tbody></table>

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>fieldNameInfo.fields</strong></td><td></td><td>True</td><td></td><td>Details of all the fields that user want to integrate via SDK</td></tr><tr><td></td><td><strong>id</strong></td><td>True</td><td>String</td><td>Internal name of the field. Always pass internal name only even if field meta is different across projects. OIM will handle the different internal names for the field having the same display name in different projects</td></tr><tr><td></td><td><strong>name</strong></td><td>True</td><td>String</td><td>Display name of the field</td></tr><tr><td></td><td><strong>dataType</strong></td><td>True</td><td>Enum</td><td>Data Type of the field which OIM understands. TEXT, HTML, WIKI, LOOKUP, DATE, DATE_TIME, DATE_STRING, BOOLEAN, NUMBER, USERNAME_AS_USER, TIME_UNIT, EMAIL_AS_USER, RTF, HYPERLINK, TEST_STEP, PARAMETER, REFERENCE, IMAGE, HIERARCHY<br>For example, the end system data type is 'string' but for OIM it's 'TEXT'. So, set dataType as 'TEXT'<br><br>If a field contains sub-fields that can have attachments, inline images, or files at the sub-field level, then it is classified as 'Complex Field' and the data type of this field is considered a 'Complex Data Type'.<br>For example, the Test Step field contains multiple sub-fields, and these sub-fields can have attachments, inline images or files. Hence, TEST_STEP is considered a 'Complex Data Type'.<br><br>Current Complex Data Types: TEST_STEP</td></tr><tr><td></td><td><strong>additionalFieldMetaData</strong></td><td>False</td><td>Object</td><td><p>This property can be used to set additional meta data of field.<br>For example, the 'Test Step' field is a complex field with nested fields, such as 'Description,' 'Expected Result,' etc. If the 'Description' is of the 'HTML' type, then set the richTextDataType of the 'Test Step' field to 'HTML' inside 'additionalFieldMetaData'.<br></p><pre><code>"additionalFieldMetaData" : {
  "richTextDataType" : "An additional meta of field to determine rich text data type of field."
  "stepExecutionType" : "An additional meta of field to store execution behavior of Test Step field."
}

Possible values of stepExecutionType:
1) ALL_STEP: provide if all the steps are required in request body while editing steps 
2) SINGLE_STEP: provide if the request can be executed for a single step (other steps remain un-changed)

Example 1: If all steps are required in request body,
{
  ...,
  "additionalFieldMetaData":{
    "richTextDataType":"HTML"
    "stepExecutionType":"ALL_STEP"
  },
  ...,
}

Example 2: If the request can be executed for a single step (other steps remain un-changed),
{
  ...,
  "additionalFieldMetaData":{
    "richTextDataType":"HTML"
    "stepExecutionType":"SINGLE_STEP"
  },
  ...,
}
</code></pre></td></tr><tr><td></td><td><strong>timeUnit</strong></td><td>True</td><td></td><td>If the dataType is TIME_UNIT, this field is required. "MILLISECOND, SECOND, MINUTE, HOUR, DAY"</td></tr><tr><td></td><td><strong>dateFormat</strong></td><td>True</td><td></td><td>If the dataType is DATE, this field should only have the date format. E.g., yyyy-MM-dd<br>If dataType is DATE_TIME, this field should have date time format. E.g., yyyy-MM-dd HH:mm:ss.SSS z</td></tr><tr><td></td><td><strong>isMandatory</strong></td><td>True</td><td>Boolean</td><td>Send true if the field is mandatory, otherwise send false</td></tr><tr><td></td><td><strong>isMultiSelect</strong></td><td>True</td><td>Boolean</td><td>Send true if the field is of type lookup or user and multiple values can be selected, otherwise send false</td></tr><tr><td></td><td><strong>isReadOnly</strong></td><td>True</td><td>Boolean</td><td>Send true if the field is read only and cannot be written, otherwise send false</td></tr><tr><td></td><td><strong>isHistorySupported</strong></td><td>True</td><td>Boolean</td><td>Send true, if for /entity-types request, pollerType is ‘ENTITY_WISE_HISTORY’ and end system tracks changes on this field, under revisions. E.g., if the Entity Title/Name is updated and the end system track history like Name updated from ‘oldName’ to ‘New title’, then send True. Send false, otherwise.</td></tr><tr><td></td><td><strong>userMentionSupported</strong></td><td>False</td><td>Boolean</td><td>Send true if users can be mentioned (@Smith) in the given field, otherwise return false</td></tr><tr><td></td><td><strong>entityMentionSupported</strong></td><td>False</td><td>Boolean</td><td>Send true if entities can be mentioned (@entity) in the given field, otherwise return false</td></tr><tr><td></td><td><strong>canBeSetAtEntityCreateTime</strong></td><td>True</td><td>Boolean</td><td>Send true if the field value can be set at the time of entity creation, otherwise false</td></tr><tr><td></td><td><strong>inlineFileMetadataForComplexFields</strong></td><td>False</td><td>Enum</td><td>set FIELD_LEVEL_STORAGE if the field stores attachment at field level; otherwise, the storage type mentioned in inline file data will be used by default.</td></tr><tr><td></td><td><strong>updateStepNumber</strong></td><td>False</td><td>Number</td><td>Required only if you are returning ‘STATIC_SUB_STEPS’ in ‘multiStepUpdate’ from this API. Step number in which the field can be updated. Field group number – where group is for update groups. Number starting with 1,2,3....<br>For example, if there is separate API to transition Status from one state to another and all other fields can be updated in single update request to the end system, then send 1 for all fields except Status. For Status, send 2. For any update request, OpsHub will call update entity SDK API twice, once with payload for all other fields and second time only with Status field<br><br>If the end System allows the Entity Type movement and Project movement then this will be required if you are returning 'STATIC_SUB_STEPS' or 'DYNAMIC_SUB_STEPS' in 'multiStepUpdate' from this API:<br><br><strong>updateStepNumber for entityTypeIdFieldName:</strong><br>- "-3": In case the end system have different API for Entity Type and Project Movement. Or the end system doesn't support Project Movement.<br>- "-6": In case the end system have same API for Entity Type and Project Movement.<br><br><strong>updateStepNumber for projectIdFieldName:</strong><br>- "-2": In case the end system have different API for Project and Entity Type Movement. Or the end system doesn't support Entity Type Movement.<br>- "-6": In case the end system have same API for Entity Type and Project Movement.<br><br><em>If no metadata for the updateStepNumber for either entityTypeIdFieldName or projectIdFieldName is provided then by default they will be treated as having separate API for Entity Type and Project Movement.</em><br><em>In case of different updateStepNumber of entityType and project, If both entityType and project movement is found supported then the order for update operation will first be Project Movement and then Entity Type movement.</em></td></tr><tr><td></td><td><strong>referenceFieldMetadata</strong></td><td>False</td><td>Object</td><td><p>Pass this metadata if the field is to be synchronized as reference field.<br></p><pre><code>referenceFieldMetadata: {
  referencedEntityTypeId: id of the entity type which is referenced through field. For e.g., if in Bug Entity, release is a reference field, provide id of the release entity type.

  idFieldName: Provide the field name which stores id or URL of the referenced entity in Entity - GET API and History - List API for base entity. If end system provides both id and url of the referenced entity, provide the name of the field which stores id.

  Example 1: If the response of the getting Bug API is as follows:
  {
    "id": "391",
    "fields": {
      "release": {
        "releaseId": "100",
        "description": "This release addresses major customer escalations and some critical defects",
        "releaseName": "Release 1",
        "archived": false
      }
    }
  }
  Here, id field name of the referenced entity is "releaseId".

  Example 2: If the response of getting base entity API is as follows:
  {
    "bugRef": "https://example.com/bug/391",
    "fields": {
      "release": {
        "releaseRef": "https://example.com/project1/release/100",
        "description": "This release addresses major customer escalations and some critical defects",
        "releaseName": "Release 1",
        "archived": false
      }
    }
  }

  Here, id field name of the referenced entity is "releaseRef".

  referenceUrl: Provide this input if end system's API provides link to url of the referenced entity instead of id. If end system provides both id and url of the referenced entity, do not include referenceUrl in response.
  For example 2, if link to url is: "https://example.com/{0}/{1}/{2}" then referenceURl.baseUrl: https://example.com/,  referenceURl.trailingTemplate: {0}/{1}/{2}
  And referenceUrl.substitutes would be {0, "projectIdFieldName", 1, "entityTypeIdFieldName", 2, "entityIdFieldName"}

  titleFieldName: Provide the field name which stores title or equivalent field of the referenced entity in the Entity - GET API and History - List API for base entity. If end system's APIs' do not have name of the referenced entity in Entity - GET API and History - List API, set this input to null.
  For example 2, titleFieldName would be releaseName.
}
</code></pre></td></tr></tbody></table>

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>comment</strong></td><td></td><td>False</td><td></td><td>Pass this parameter if you want to integrate comments for a given entity type. Otherwise, do not send the comment parameter at all. If this parameter is passed, SDK must implement all the Comment APIs.</td></tr><tr><td></td><td><strong>fieldNameInfo</strong></td><td>True</td><td>Object</td><td><p>If the comment parameter is sent back, then it is mandatory to send fieldNameInfo. The user needs to send the field names as they will be sent by SDK to OpsHub when reading comments and from OpsHub to SDK when adding comments. OpsHub will try to find the given information in the field name specified as part of the data sent here.<br></p><pre><code>{
  "idFieldName": "id",
  "titleFieldName": "title",
  "bodyFieldName": "body",
  "createdDateFieldName": "created",
  "updatedDateFieldName": "updated",
  "createdByFieldName": "createdBy",
  "updatedByFieldName": "updatedBy",
  "commentTypeFieldName": "commentType"
}
</code></pre></td></tr><tr><td></td><td><strong>userMentionSupported</strong></td><td>False</td><td>Boolean</td><td>Send true if the user mention supported within comments; otherwise, false.</td></tr><tr><td></td><td><strong>entityMentionSupported</strong></td><td>False</td><td>Boolean</td><td>Send true if the user mention supported within comments; otherwise, false.</td></tr><tr><td></td><td><strong>commentBodyDataType</strong></td><td>True</td><td>Enum</td><td>TEXT, HTML, WIKI</td></tr><tr><td></td><td><strong>commentIdDataType</strong></td><td>True</td><td>Enum</td><td>NUMBER, TEXT</td></tr><tr><td></td><td><strong>createdUpdatedByFieldDataType</strong></td><td>False</td><td>Enum</td><td>Pass this parameter if you need user data while creating comment. Example, you want to create comment with same user as source endpoint. If you require username send USERNAME_AS_USER, if you require email address send EMAIL_AS_USER.</td></tr><tr><td></td><td><strong>htmlReplacementForNewLine</strong></td><td>True</td><td>String</td><td>Exact value for new line character in the comment.<br>Possible values are: ‘<br>’, ‘\n’ or null.</td></tr><tr><td></td><td><strong>createUpdateDateFormat</strong></td><td>True</td><td>String</td><td>Date format for created and updated dates of the comment.</td></tr><tr><td></td><td><strong>delayInCommentUpdateTimeInMillis</strong></td><td>False</td><td>Number</td><td>Expected delay between entity update time and comment update time.<br>There are systems in which comment update is delayed after entity update time. In such systems, identify the maximum delay that may be there in comment update time after entity update time.<br>If there is no delay in the system, the below value can be set as 0.<br>If there is delay of let say up to 2 seconds, set the value to 2000 (in millis). If the delay is up to 5 seconds, set the value to 5000.</td></tr><tr><td></td><td><strong>typesOfComments</strong></td><td>True</td><td>List<code>&#x3C;String></code></td><td>The supported list of comment types. E.g., Internal, External, Work Notes, Additional etc. OpsHub will display these comment types under comment mapping. The user can map comment types across connectors to decide the type of comments they want to integrate.</td></tr></tbody></table>

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>attachment</strong></td><td></td><td>False</td><td></td><td>Pass this parameter if you want to integrate attachments for a given entity type. Otherwise, do not send the attachment parameter at all.<br>If this parameter is passed, SDK must implement all the Attachment APIs.</td></tr><tr><td></td><td><strong>fieldNameInfo</strong></td><td>True</td><td>Object</td><td><p>If the attachment parameter is sent back, then it is mandatory to send fieldNameInfo. The user needs to send field names as they will be sent by SDK to OpsHub when reading attachments and from OpsHub to SDK when adding or updating attachments. OpsHub will try to find the given information in the field name specified as part of the data sent here.<br><br></p><pre><code>{
  "idFieldName": "id",
  "contentUriFieldName": "uri",
  "renderUriFieldName": "renderUri",
  "fileNameFieldName": "fileName",
  "contentTypeFieldName": "contentType",
  "contentLengthFieldName": "contentLength",
  "createdOrUpdatedDateFieldName": "updated",
  "createdByFieldName": "createdBy",
  "attachmentTypeFieldName": "attachmentType"
}
</code></pre><p><br><strong>contentUriFieldName:</strong> The field which has the value as the URL to get/download the content of the attachment. If there's no such field in the end system, keep the fieldName as 'contentUri' and set the download link in that field in the actual attachment object.<br><br><strong>renderUriFieldName:</strong> The field which has value as the URI to render/display the content of the attachment.<br><br><strong>Note:</strong> This URI is not used to download an attachment. For downloading the attachment URI, refer to <strong>contentUriFieldName</strong>.<br><br>Example: If an inline image is shown with the <code>&#x3C;img></code> tag, render URI is the value of the <code>src</code> attribute of the <code>&#x3C;img></code> tag.</p></td></tr><tr><td></td><td><strong>updateSupported</strong></td><td>True</td><td>Boolean</td><td>Send true if the end system supports updating attachment via API; otherwise, false. If false, OpsHub will simulate update attachment behaviour by deleting the attachment and adding a new version.</td></tr><tr><td></td><td><strong>deleteSupported</strong></td><td>True</td><td>Boolean</td><td>Send true if the end system has an API to delete the attachment; otherwise, false.</td></tr><tr><td></td><td><strong>historySupported</strong></td><td>True</td><td>Boolean</td><td>Does the system support history for attachment? True if yes, else false.</td></tr><tr><td></td><td><strong>createUpdateDateFormat</strong></td><td>True</td><td>String</td><td>Date format for created and updated dates of the attachment.</td></tr><tr><td></td><td><strong>typesOfAttachments</strong></td><td>True</td><td>List&#x3C;String></td><td>Types of attachments supported by the system: INTERNAL, EXTERNAL, etc.</td></tr></tbody></table>

| Parent Parameter | Name                      | Required | Type          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ---------------- | ------------------------- | -------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **inlineFile**   |                           | False    |               | <p>Pass this parameter if you want to integrate inline files for a given entity type. Otherwise, do not send this parameter at all.<br>Attachment APIs must be implemented to integrate inline files.</p>                                                                                                                                                                                                                                                                                                                                        |
|                  | **deleteSupported**       | True     | Boolean       | Does the system allow deleting inline files?                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                  | **inlineFileStorageType** | True     | Enum          | <p>Is the inline file/attachment stored at the entity or global level in the system?<br><br>Possible values:<br>1) ENTITY_LEVEL_STORAGE: When inline files are stored in the entity itself<br>2) EXTERNAL_STORAGE: When inline files are stored at the system level<br>3) FIELD_LEVEL_STORAGE: When inline files are stored in the field itself</p>                                                                                                                                                                                              |
|                  | **inlineFileUrlPrefix**   | True     | List\<String> | <p>What is the prefix of inline files?<br>This is used to identify if an inline file or image URL is the URL to some external site or the system's URL.<br><br>Provide the common initial part of the inline files URL. E.g., If the system has inline file URLs like these:<br>- https://media.example-system.com/files/file1.png<br>- https://media.example-system.com/files/file2.docx<br>- https://media.example-system.com/files/file3.pdf<br><br>In this case, the inline file URL prefix is: "https://media.example-system.com/files"</p> |

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>link</strong></td><td></td><td>False</td><td></td><td>Pass this parameter if you want to integrate entity relationship for a given entity type. Otherwise, do not send this parameter at all. Links APIs must be implemented to integrate links</td></tr><tr><td></td><td><strong>fieldNameInfo</strong></td><td>True</td><td>Object</td><td><pre><code>{
  "linkTypeFieldName": "linkType",
  "linkTypeDirectionFieldName": "linkDirection",
  "linkedEntityIdFieldName": "linkedEntityId",
  "linkedEntityTypeFieldName": "linkedEntityType",
  "linkedEntityScopeIdFieldName": "linkedEntityScopeId",
  "createdDateFieldName": "createdDate",
  "createdByFieldName": "createdBy",
  "linkCommentFieldName": "linkComment",
  "externalLinkUrlFieldName": "externalLinkUrl",
  "isExternalLinkFieldName": "isExternalLink"
}
</code></pre></td></tr><tr><td></td><td>deleteSupported</td><td>True</td><td>Boolean</td><td>Does the system allow to delete link?</td></tr><tr><td></td><td>historySupported</td><td>True</td><td>Boolean</td><td>Does the system support history for link?</td></tr><tr><td></td><td>createUpdateDateFormat</td><td>True</td><td>String</td><td>Date format for created and updated dates of link</td></tr><tr><td></td><td><strong>linkTypes</strong></td><td>True</td><td></td><td></td></tr><tr><td></td><td>linkType</td><td>True</td><td>String</td><td>Name of link type: Parent, Child, Relates To, Blocked By, etc</td></tr><tr><td></td><td>linkTypeInternalName</td><td>False</td><td>Sring</td><td>Specifies the unique system identifier for the link relationship: parent, relates_to etc. This value is used for interactions with end system and is not intended for display purposes.</td></tr><tr><td></td><td>linkTypeDirection</td><td>False</td><td>Enum</td><td>This field is required when same linkTypeInternalName is used for two different link relationships in the end system. For example, <code>parent</code> is internal link name for <code>is parent of</code> and <code>has parent</code>. In such cases, you must provide <code>linkTypeDirection</code> to specify how the link should be created relative to the current entity.<br><br>Possible values:<br>1) FORWARD: Use this value when the <code>linkType</code> defines the relationship from the current entity to the other entity. For example, if the linkType is <code>is parent of</code> and the current entity is the parent of the other entity, select <code>FORWARD</code> value.<br>2) BACKWARD: Use this value when the <code>reverselinkType</code> defines the relationship from the other entity to the current entity. For example, if the reverseLinkType is <code>has parent</code> and the current entity is the child entity, select <code>BACKWARD</code> value.</td></tr><tr><td></td><td>reverseLinkType</td><td>True</td><td>String</td><td>Name of its reverse link. E.g., if the link type is Parent, then the opposite linkType is Child, i.e. Entity E1 is the parent of entity E2, and E2 is the child of E1</td></tr><tr><td></td><td>isMultiLinkAllowed</td><td>True</td><td>Boolean</td><td>True: If multiple links of this type can be created. False: if only one link of this type can be created. For example: Adding only one parent is allowed to be added for any entity, so set multiLinkAllowed to false for Parent Type. On the other hand, for the ‘Related’ link type, any number of links can be added, so send true</td></tr><tr><td></td><td>isLinkMandatory</td><td>True</td><td>Boolean</td><td>True: If link of this type is mandatory for entity create or update. False: If link of this type is not mandatory for entity create or update. For example, it might be mandatory to have a Parent link to another work item for sub-task or task entity type. In this case, send true for the Parent link type for Task</td></tr><tr><td></td><td>isBulkLinkingSupported</td><td>True</td><td>Boolean</td><td>True: If bulk linking is supported via API. False: If bulk linking is not supported via API. For example, Bug and task can be linked by relates link type. Multiple tasks (with link type - relates) can be added and removed via a single API. In this case, send true for relates link type for Bug</td></tr></tbody></table>

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>link.rank</strong></td><td><strong>rank</strong></td><td>False</td><td></td><td><p>If entity type supports keeping ordering / ranking of entities, provide metadata for that.<br>e.g., If entities can be ranked and the rank is preserved in the end system, it supports rank.<br><br>In below example, order of 1.1, 1.2, 1.3 are stored and can also be changed and preserved.<br>Similarly order of 2.1 and 2.2 is also preserved.<br></p><pre><code>- 1
  - 1.1
  - 1.2
  - 1.3
- 2
  - 2.1
  - 2.2
</code></pre><p><br>The order can be stored in a field, e.g., rank.<br>The order can also be maintained through siblings (before and after).<br><br>Pass null if rank is not supported by entity type in the end system.</p></td></tr><tr><td></td><td>rankType</td><td>True</td><td>Enum</td><td><p>The way entities are ranked in the end system.<br><br>* <strong>FLAT_SINGLE</strong>: Entities of same type can only be ranked together.<br></p><pre><code>Bug1
Bug2
Bug3
</code></pre><p><br>* <strong>FLAT_MULTIPLE</strong>: Entities of different types can be ranked together.<br><br>Bug1<br>Story1<br>Bug2<br>Story<br><br>* <strong>HIERARCHY_SINGLE</strong>: Entities of same type can be ranked in a tree structure.<br></p><pre><code>Bug1
Bug2
  - Bug3
  - Bug4
Bug5
</code></pre><p><br>* <strong>HIERARCHY_MULTIPLE</strong>: Entities of different types can be ranked together in a tree structure.<br></p><pre><code>Epic 1
Story 1
  - Bug 2
  - Story 2
  - Story 3
Epic 3
</code></pre></td></tr><tr><td></td><td>supportedRankOperations</td><td>True</td><td>List<code>&#x3C;String></code></td><td>List of rank operations supported by the system for ranking entities.<br>* MOVE_BEFORE: Moves current entity before its sibling under a linked entity<br>* MOVE_AFTER: Moves current entity after its sibling under a linked entity<br>* LAST_IN_LIST: Move current entity at the end of the list under its linked entity.<br>* MOVE_BULK_AFTER: Reorders multiple child entities under a parent after a specific sibling.<br><br>Example:<br>Consider the below scenario, where entity type for entities Epic 1 and Epic 2 is Epic and entity type for entities Story 1, Story 2, Story 3, Story 4 and Story 5 is Story<br>Epic 1<br>  - Story 1<br>  - Story 2<br>  - Story 3<br>  - Story 4<br>  - Story 5<br>Epic 2<br><br>MOVE_BEFORE: Story 3 is moved before Story 2.<br>Here, current entity is Story 3, siblingEntity is Story 2, and linked entity is Epic 1<br><br><br>MOVE_AFTER: Story 2 is moved after Story 4.<br>Here, current entity is Story 2, siblingEntity is Story 4, and linked entity is Epic 1<br><br>LAST_IN_LIST: Story 2 is moved at the last of the list under Epic 1.<br>Here, current entity is Story 2, and linked entity is Epic 1<br><br><br>MOVE_BULK_AFTER: The position of Story 3 and Story 5 are swapped. Now entities under Epic 1 are in following order - Story 1, Story 2, Story 5, Story 4, Story 3<br>Here, current entity is Epic 1, sibling entity is Story 2, and linked entities are Story 5, Story 4 and Story 3<br><br>Note:<br>* MOVE_BULK_AFTER should be provided for the entity under which links can be ordered in bulk manner. In the above example, MOVE_BULK_AFTER should be provided for entity type Epic.<br>* MOVE_BEFORE, MOVE_AFTER, and LAST_IN_LIST should be provided for the entity whose order is being changed. In the above example, these should be provided for entity type Story.<br>* If MOVE_BULK_AFTER is supported for an entity (e.g., Epic), it is not required to configure MOVE_BEFORE, MOVE_AFTER, or LAST_IN_LIST in the linked entity's (e.g., Story) metadata.</td></tr><tr><td></td><td>rankFieldName</td><td>False</td><td>String</td><td>If entity stores the rank information in a field, provide that field name. Example: stack rank in Azure DevOps, rank in Jira</td></tr><tr><td></td><td>rankScope</td><td>False</td><td>Object</td><td>A scope in which the rank of an entity can be uniquely identified.<br><br>e.g., If the rank is uniquely identified under a project, the project id will be the scope of the rank.<br><br>If the rank is uniquely identified under a project and a module, the '{projectId} {moduleId}' will be the scope of the rank.<br><br>If the rank is always unique in the system (across projects, across modules, across components), the scope can be set as null.</td></tr></tbody></table>

<table><thead><tr><th>Parent Parameter</th><th>Name</th><th>Required</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>link.rank.scope</strong></td><td></td><td></td><td></td><td></td></tr><tr><td></td><td>template</td><td>True</td><td>String</td><td><p>String template for rank scope.<br><br>What is the scope made of?<br><br>* If scope is just projectId, provide template as <code>{0}</code> and provide substitutes for projectId field name.<br>* If scope is projectId and entityType, provide template as <code>{0}{1}</code> and provide substitutes for projectId and entityTypeId field names.<br><br></p><pre><code>e.g., "{0}", "{0}{1}", "{0}::{1}", etc.
</code></pre><p><br>If the projectId is 101 and entityType is 10001,<br><br>* If "{0}::{1}" is provided as template and substitutes are provided for projectId and entityTypeId, the actual scope will be "101::10001".</p></td></tr><tr><td></td><td>substitutes</td><td>True</td><td>Object</td><td>Map containing all the substitute numbers used in template and field name that needs to be replaced against given substitute.<br>The substitute field name can be any field in the entity object.<br><br><strong>e.g.,</strong><br>If a template is "{0}::{1}", substitute map can be as follows:<br><code>{"0": "projectIdFieldName", "1": "entityTypeIdFieldName"}</code><br><br>In the template:<br>* The value of parameter {0} will be replaced with actual value of project id for the entity.<br>* The value of parameter {1} will be replaced with actual value of entity type id for the entity.</td></tr></tbody></table>

| Parent Parameter | Name                  | Required | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ---------------- | --------------------- | -------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **userMention**  |                       | False    |        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                  | userMentionDataType   | True     | Enum   | <p>In the case of a given user mentioned, what data will SDK send for that user?<br><em>USERNAME_AS_USER</em>: user's username<br><em>EMAIL_AS_USER</em>: user's email address<br><br>Depending on the data type, OpsHub will search for required user information from the user API.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                  | **mentionDetails**    | True     |        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                  | fieldDataType         | True     | Enum   | <p>Type of usermention detection system for field or comment. Each type correlates with a data type of field or comment.<br>For e.g., HTML, WIKI, MARKDOWN, TEXT, HTML_REGEX (If mention containing field is HTML type and all mentions are not detected with html selector, instead provide HTML_REGEX enum and provide a regex in selectorOrRegex that can detect the mention).</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                  | selectorOrRegex       | True     | List   | <p>If the usermention detection system used is of type WIKI or TEXT, return regex to search usermention.<br>Example: return <code>\\[~accountId:([a-z0-9.]+)\\]</code> for searching <code>[~accountId:john.doe]</code> tags.<br><br>The regex should have 3 parts but only 1 group.<br>The regex must have only 1 group, corresponding to the user field's value as per userMentionDataType.<br><br><em>Prefix:</em> \[~accountId:<br><em>Infix:</em> ([a-z0-9.]+)<br><em>This part will be replaced with username or email</em><br><em>Only part for username/email should be provided as the group '()'</em><br><em>Postfix:</em> \]<br><br>If the usermention detection system used is of type HTML, return HTML tag selector to search usermention.<br><br>Example:<br>If the usermention tag is <code>&#x3C;a></code> tag having 'href' attribute, return <code>a[href]</code> to search for usermention.<br>Return <code>a[href]</code> for <code>&#x3C;a href="https://example.com/users/john.doe" rel="john.doe"> John Doe &#x3C;/a></code> as the mention tag.<br><br>If HTML tag selector didn't work, use HTML_REGEX as fieldDataType and return regex to search usermention.<br>Example: return <code>"mentionUser\s(\w+)"</code> for searching john_doe and jane_doe from data such as:<br><code>mentionUser john_doe is working with mentionUser jane_doe</code><br><br><em>It's important that regex has only 1 group and that 1 group captures the user data corresponding to the user field's value as per userMentionDataType.</em></p> |
|                  | mentionTemplate       | True     | String | <p>Usermention template that will be used to create a usermention tag for the target system. As template variables, following variables can be used:<br><br>${id} : id of the user.<br>${username} : Username of the user.<br>${email} : Email of the user.<br>${displayName} : Display name of the user.<br><br>If null value is expected and default template variable value needs to be provided, ':-' operator can be used.<br><br>Examples:<br>${displayName:-Display Name}: This will replace this template variable with 'Display Name' if value of displayName is not present.<br>${displayName:-}: This will replace this template variable with '' (empty string) if value of displayName is not present.<br><br>As per various data types, mention templates can vary.<br><br><strong>Examples:</strong><br>HTML: <code>&#x3C;a href="https://example.com/users/${username}" rel="${username}"> ${displayName} &#x3C;/a></code><br>Resolved: <code>&#x3C;a href="https://example.com/users/john.doe" rel="john.doe"> John Doe &#x3C;/a></code><br><br>Wiki: <code>[~accountId:${username}]</code><br>Resolved: <code>[~accountId:john.doe]</code><br><br>Text: <code>${username} &#x3C;${email}></code><br>Resolved: <code>john.doe &#x3C;john.doe@email.com></code></p>                                                                                                                                                                                                                                                                        |
|                  | userDataRegex         | False    |        | <p>Regex to extract user data out of HTML tag attribute or inner text of tag.<br><br>This field is only needed when #fieldDataType is HTML and user data has to be extracted from HTML tag attribute or inner text.<br>This field can be null when #fieldDataType is not HTML.<br>It can also be null if one of the user field values is exact HTML attribute value or inner text.<br>This regex must have only 1 group which corresponds to the value of the user field as per #userMentionDataType.<br><br><strong>Examples:</strong><br>1. <code>&#x3C;a href="https://example.com/users?name=john.doe"> John Doe &#x3C;/a></code><br>To extract the username from <code>href</code>, set <code>userDataRegex</code> to <code>".*[?&#x26;]name=([a-z.]+)"</code>.<br><br>2. <code>&#x3C;a href="https://example.com/users/101"> @john.doe &#x3C;/a></code><br>To extract the username from inner text, set <code>userDataRegex</code> to <code>"@([a-z.]+)"</code>.<br><br>3. <code>&#x3C;a href="https://example.com/users/101" rel="john.doe"> John Doe &#x3C;/a></code><br>Here, <code>rel</code> attribute's exact value is username. So, no need to provide regex. The userDataRegex can be null.<br><br>4. <code>&#x3C;a href="https://example.com/users/101"> john.doe &#x3C;/a></code><br>Here, the inner text's exact value is username. So, no need to provide regex. Hence, the userDataRegex can be null.</p>                                                                                                                               |
|                  | userDataAttributeName | False    | String | <p>Name of the HTML tag attribute which contains user field value as per #userMentionDataType.<br>This field is only needed when #fieldDataType is HTML.<br>This field can be null when #fieldDataType is not HTML.<br>If for HTML data type, userDataAttributeName is null, HTML tag's inner text will be considered to have user field value.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

| Parent Parameter  | Name                       | Required | Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ----------------- | -------------------------- | -------- | --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **entityMention** |                            | False    |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                   | **mentionDetails**         | True     |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                   | **fieldDataType**          | True     | Enum            | <p>Type of entity mention detection system for field or comment. Each type correlates with a data type of field or comment.<br><br>For example: <strong>HTML</strong>, <strong>WIKI</strong>, <strong>MARKDOWN</strong>, <strong>TEXT</strong>, <strong>HTML_REGEX</strong> (If mention containing field is HTML type and all mentions are not detected with HTML selector, instead provide <strong>HTML_REGEX</strong> enum and a regex in <code>selectorOrRegex</code> that can detect the mention).</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                   | **selectorOrRegex**        | True     | List `<String>` | <p>If the entity mention detection system used is of type <strong>WIKI</strong> or <strong>TEXT</strong>, return regex for which entity mention needs to be checked.<br><br>The regex must have only one group, corresponding to the entity mention’s value as per <code>fieldDataType</code>.<br><strong>Example:</strong> <code>\[~([a-z0-9.]+)\]</code> would search for all <code>~entitymention</code> tags.<br><br>If the detection system is <strong>HTML</strong>, return the selector for which entity mention needs to be checked.<br><strong>Example:</strong> <code>doc.select("a[href]")</code> will search for all anchor tags having an <code>href</code> attribute.<br><br>If the HTML tag selector didn’t work, use <strong>HTML_REGEX</strong> as <code>fieldDataType</code> and return regex to search entity mention.<br><strong>Example:</strong> return <code>"workitem\s(\d+)"</code> for searching entity with id <code>123</code> and <code>456</code> from data such as <code>workitem 123 depends on workitem 456</code>.<br><br><em>It's important that the regex has only one group, and that group captures the entity id of the mention.</em></p>                     |
|                   | **mentionTemplate**        | True     | String          | <p>The <code>entityMention</code> template that will be used to create an entity mention tag for the target system.<br><br>As template variables, the following variables can be used:<br>${entityId} – id of the entity<br>${entityDisplayId} – display id of the entity<br>${entityProject} – project name of the mention scope<br>${entityProjectId} – project id of the mention scope<br>${entityType} – entity type of the mention scope<br><br>As per various data types, mention templates can vary.<br><br><strong>Examples:</strong><br>HTML: <code>&#x3C;a href="https://example.com/${projectId}/_entity/edit/${entityId}" data-vss-mention="version:1.0">#${entityDisplayId}&#x3C;/a></code><br>Resolved: <code>&#x3C;a href="https://example.com/Prj-101/_entity/edit/101" data-vss-mention="version:1.0">#Bug-101&#x3C;/a></code><br><br>Wiki: <code>https://example.com/browse/${entityId}|smart-link</code><br>Resolved: <code>https://example.com/browse/DCPA3-7 |smart-link</code><br><br>Text: <code>${entityId} &#x3C;${entityDisplayId}></code><br>Resolved: <code>101 &#x3C;Bug-101></code></p>                                                                                |
|                   | **entityIdAttribute**      | True     |                 | <p>Parameters to specify the entity id to be read from text, regex, or HTML attribute name.<br>For HTML tag element, attribute name is required.<br>For Wiki, regex is required.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                   | **dataAttributeName**      | False    | String          | <p>This field is only required when <code>fieldDataType</code> is <strong>HTML</strong>. It can be null otherwise.<br>This field contains the name of the HTML tag attribute which contains the entity field value.<br>If <code>fieldDataType</code> is <strong>HTML</strong> and this field is null, the HTML tag’s inner text will be considered to have the entity field value.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|                   | **dataRegEx**              | False    | String          | <p>This field is used to extract entity information such as entity id, entity type, project id, or project name from the text.<br><br>In case of HTML, this extracts data from an HTML tag attribute or inner text, based on the selector in <code>selectorOrRegex</code>.<br>In case of WIKI, this extracts data from matched text using the selector provided.<br><br>This field is only required when <code>fieldDataType</code> is HTML and Id data has to be extracted from HTML tag attribute or inner text. It can be null otherwise or when the id value directly matches HTML content.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                   | **entityTypeAttribute**    | False    |                 | <p>If end system provide entity type corresponds to mentioned entity along with the mentioned entity id then it is recommended to provide the meta information to extract or read entity type information from mentioned tag.<br><br>If this parameter is not given then OpsHub will search mentioned entity using mentioned id parameter without the entity type and it would be considered that entity id is sufficient, otherwise OpsHub will search mentioned entity using entity type along with id. Examples:<br><br><strong>Examples:</strong><br>HTML: <code>&#x3C;a class="cke-link-popover-active" href="https://www.example.com/#/23468038167ud/defects?detail=/defect/669232438245">Entity101&#x3C;/a></code><br>WIKI: <code>[DCPA3-7|https://www.example.com/browse/DEFECT/DCPA3-7] [displayText|url]</code><br>For above entity mentioned tag the text 'defect' in html example and 'DEFECT' in wiki example is entity type.<br><br>WIKI: <code>[DCPA3-7|https://opshub.atlassian.net/browse/DCPA3-7][displayText|url]</code>, For above tag: entity type does not exist as part of the mentioned tag, so end system do not require to provide this parameter entityTypeAttribute.</p> |
|                   | **entityProjectAttribute** | False    |                 | <p>If end system provide project corresponds to mentioned entity along with the mentioned entity id then it is recommended to provide the meta information to extract or read project information from mentioned tag.<br><br>If this parameter is not given then OpsHub will search mentioned entity using mentioned id parameter without the project and it would be considered that entity id is sufficient, otherwise OpsHub will search mentioned entity using project along with entity id.<br><br><strong>Examples:</strong><br>HTML: <code>&#x3C;a href="https://www.example.com/40723eb0-0857-4970-a4f4-8cf657085847/_entity/edit/101" data-vss-mention="version:1.0">#Bug-101&#x3C;/a></code><br>WIKI: [DCPA3-7|https://www.example.com/browse/TESTP/DCPA3-7][displayText|url]<br>For above entity mentioned tag the text '40723eb0-0857-4970-a4f4-8cf657085847' in HTML example and 'TESTP' in WIKI example is project of mentioned entity.<br><br>WIKI: [DCPA3-7|https://www.example.com/browse/DCPA3-7][displayText|url], For above tag: project does not exist as part of the mentioned tag, so end system do not require to provide this parameter entityProjectAttribute.</p>         |
|                   | **entityURLDetails**       | False    |                 | <p>This field supports reverse sync for source URL/target URL option.<br><br>Provide the matcher or selector for the matching entity URL of the end system.<br>If the system supports HTML mentions, provide a JSoup matcher for URLs within <code>href</code>.<br>If the system supports Wiki, provide a regex for URLs.<br>If both HTML and Wiki mentions are supported, provide a list of entity URL details in mention metadata.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|                   | **entityWebURLMatcher**    | False    | String          | This field contains regex or selector to match entity web url                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|                   | **entityIdDataSelector**   | False    | String          | This field contains regex to read the entity id from web url                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
