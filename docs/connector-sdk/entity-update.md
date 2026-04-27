# Entity Update

API Name: Entity – Update

## Overview

This API is supposed to update an existing entity in the end system and return the entity object as a response. As part of the request payload, OpsHub will send all the field details with which entity needs to be updated. API must update only the fields that are coming and shouldn’t modify any other field.

## API URI

This is the URI, OpsHub will execute to call this API

```bash
PUT: /entities/{entityTypeId}/{entityId}? 
      projectId=<projectId>
      &subStepNumber=<subStepNumber>
```

## URI Parameters

| Name          | In    | Required | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------- | ----- | -------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| entityTypeId  | path  | True     | String | ‘id’ of the entity type for the given entityId                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| entityId      | path  | True     | String | ‘id’ of the entity that needs to be updated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| projectId     | query | True     | String | Project in which the entity exists                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| subStepNumber | query | True     | String | <p>Step number in which the field/fields can be updated.<br><br>Consider the following if the entity type and project movement is supported and the <code>multiStepUpdate</code> field provided in the <a href="https://github.com/OpsHubProduct/OIM-Documentation/blob/main/docs/connector-sdk/Entity_Type_%E2%80%93_Get/README.md#response_parameters">multiStepUpdate</a> is either <code>STATIC_SUB_STEPS</code> or <code>DYNAMIC_SUB_STEPS</code>:<br><br><strong>"-2"</strong>: Project should be updated to the project passed in the Request Payload corresponding to fields, provided <code>{projectIdFieldName}</code> key.<br><strong>"-3"</strong>: Entity Type should be updated to the Entity Type passed in the Request Payload corresponding to fields, provided <code>{entityTypeIdFieldName}</code> key.<br><strong>"-6"</strong>: Both Project and EntityType should be updated to the Entity Type and project passed respectively in the fields, <code>{entityTypeIdFieldName}</code> and <code>{projectIdFieldName}</code> keys.</p> |

## Request Payload

```json
{
  "fields": {
    "<field1>": "field1_value",
    "<field2>": [
      "<field2_Value1>",
      "<field2_value2>"
    ],
    "<field3>": true,
    "<field4": 1000,
    "<fieldUser>": "userName"
  },
  "mandatoryLinks": [
    {
      "<linkTypeField>": "",
      "<linkedEntityIdField>": "",
      "<linkedEntityTypeField>": "",
      "<linkedEntityScopeIdFieldName>": ""
    }
  ]
}
```

## Request Body

| **Name**       | **Required** | **Type** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| -------------- | ------------ | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fields         | True         | Object   | <p>It will contain a name: value pair for all fields that need to be set while updating entity in the end system, where (name) is the field id of the field to be set and (value) contains the value that needs to be set. For multi-select fields, the value will be a list of strings. For example, for user-type fields, OpsHub will send a username or email, depending on the data type specified for that field in entity-types API. On the other hand, the value will be a string for other fields like text, number, etc.<br>API must only update the values that are coming and shouldn’t modify or add any more fields while updating an entity in the end system.</p> |
| mandatoryLinks | False        | Object   | <p>It will contain only mandatory links that need to be set as part of updating an entity.<br>Note: It won’t contain non-mandatory links. For adding non-mandatory links, a separate add-link API will be called.<br>Note: API must only link to mandatory links coming as part of the request payload and should not add any other link.</p>                                                                                                                                                                                                                                                                                                                                    |

## Response Payload

Please refer to the [Response Payload](entity-get.md#response-payload) section of the Entity-Get API.
