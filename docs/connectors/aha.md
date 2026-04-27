# Aha

## Prerequisites

### User privileges

* Create one user in Aha! that is dedicated for <code class="expression">space.vars.SITENAME</code>. This user shouldn't perform any other action from Aha!'s user interface. This user is referred as 'Integration User' in the document.
  * Please refer to [Add User](aha.md#add-user) section to create a user in Aha!.
* To synchronize entities to and from any systems to Aha!, Integration User must have **Contributor** permission at project level and **Customizations** role \[which needs be selected from project's Administrator roles]. Refer to [Grant permissions to Aha! user](aha.md#grant-permissions-to-aha-user) section for step-wise details on how to grant permissions to a Aha! user.

### API Rate Limiting

* Due to Aha! rate limit issues, for more details, refer to the [API Rate Limitation in Aha!](aha.md#api-rate-limitation-in-aha) section, it is recommended to use the Fetch Mapped Data Only feature (available as an <code class="expression">space.vars.SITENAME</code> add-on) to optimize the API calls. Contact your sales or support representative to enable it.

## System Configuration

* As you kickstart with the integration, you must first configure Aha! system in <code class="expression">space.vars.SITENAME</code>.
* Click [System Configuration](../integrate/system-configuration.md) to learn the step-by-step process to configure a system.

Refer to the following screenshot for reference:

<div align="center"><img src="../../.gitbook/assets/Aha_System_Config.png" alt="" width="1000"></div>

**Aha! System form details**

| **Field Name**               | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **System Name**              | Provide the system's name                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Instance URL**             | Provide Instance URL of the Aha! instance. This URL will be used for communicating to Aha! API. The format of the URL is: https:// .aha.io Example: https://opshub-inc.aha.io                                                                                                                                                                                                                                                         |
| **User Email**               | Provide the email Id of a dedicated user who will be used for communicating with Aha! API. This user should have the required privileges to use the Aha! API. For more details on the required privileges, please refer to [User privileges](aha.md#user-privileges) section.                                                                                                                                                         |
| **API Token**                | Provide the bearer API Token generated in Aha! for the user given in "User Email" field. Please refer to [Steps for generating the API token](aha.md#steps-for-generating-the-api-token) section for generating the API token.                                                                                                                                                                                                        |
| **Metadata Details**         | The user can edit entity types based on his/her Aha! instance details for system metadata. For the format and guidance related to filling these details in JSON form, please refer to [Understanding JSON Input](aha.md#understanding-json-input) section.                                                                                                                                                                            |
| **Base URL for Remote Link** | Provide different Instance URL of the Aha! instance. This URL is used for generating the Remote Link. E.g., if the Instance URL is https://opshubTest33.aha.io/ or any API node URL, but Remote Link needs to be generated with a different Instance URL such as https://opshubTest.aha.io/. **Note** : If "Base URL for Remote Link" is empty, it will use Instance/Server URL to generate Remote Link if configured on Integration. |

**Understanding JSON Input**

* The entity metadata details can be provided at the time of system configuration in the field 'Metadata details' \[in the form of JSON] in the below mentioned use case:
  * Use case: In Aha!, the entity display name can be changed. Hence, if this is the case at your end, then changes are needed to be performed in the entity display name of JSON input. Below is the example of the JSON input:

```json
{
  "entities": [
    {
      "internalName": "capabilities",
      "displayName": "Capability"
    },
    {
      "internalName": "features",
      "displayName": "Feature"
    },
    {
      "internalName": "requirements",
      "displayName": "Requirement"
    },
    {
      "internalName": "pages",
      "displayName": "Note"
    },
    {
      "internalName": "releases",
      "displayName": "Release"
    },
    {
      "internalName": "tasks",
      "displayName": "To-do"
    },
    {
      "internalName": "initiatives",
      "displayName": "Initiative"
    }
  ]
}
```

## Mapping Configuration

Map the fields between Aha! and the other system to be integrated to ensure that the data between both the systems synchronize correctly.

<div align="center"><img src="../../.gitbook/assets/aha_entity_mapping.png" alt="" width="1000"></div>

Click [Mapping Configuration](../integrate/mapping-configuration.md) to learn the step-by-step process to configure mapping between the systems.

In Aha!, entity type selection in mapping configuration depends on the project/product selection. For more details, please refer to [Project Selection](aha.md#project-selection) section.

> **Note**: In <code class="expression">space.vars.SITENAME</code>, for the sync of Parking lots, the Release entity needs to be seleted at mapping level {as Parking lots are considered as Release by <code class="expression">space.vars.SITENAME</code> }.

### Comments Configuration

* Aha! as source system:
  * If comments are mapped in Mapping Configuration, then all the comments will be synchronized to target system. Additionally, the attachments & inline images from the comment will sync to the target system based on its attachment behaviour. For example, if the target conatins the comment with attachment functionality, then attachment will sync to attachment section and the reference to that attachment will be added inside the comment.
* Aha! as target system:
  * If comments are mapped in Mapping Configuration, then comments will be synced to Aha! system. Here, the inline images and attachments will be synced to Aha! description field and reference to those attachements will be added in the comment.

### Attachments Configuration

* Each Rich Text type field supports attchements in Aha!.
* Aha! as source system:
  * Attachments from all rich text and attachment type fields will sync to the target system.
* Aha! as target system:
  * Attachment mapping can be configured to decide the field of Aha! to which the attachment needs to be synced.
    * If only attachment mapping toggle is enabled but the attachment type mapping is not configured, then attachment will sync to description field of Aha! as a part of default attachment behavior sync.

<div align="center"><img src="../../.gitbook/assets/aha_attachment_mapping.png" alt="" width="1000"></div>

### Relationship Configuration

In Aha!, Record links and Reference fields will be supported as relationships.

#### Mandatory Links

* For Feature and Epic type of entities, the Release is a mandatory relationship linkage as feature and epic can only be created inside the release/parking lot.
* For Requirement type of entities, Feature is a mandatory relationship linkage as requirements can only be created inside the feature.
* For To-do type of entities, the Parent is a mandatory relationship linkage as we support the creation of a to-do entity inside the other entity only. Here, the parent entity can be any other entity.

### Reference Fields

* Reference fields are the fields that refer to some other Aha! entity we support.
* Reference fields \[System/Custom fields] will be synchronized through relationships. For references, the names of the Reference fields will be shown in link type mapping of the Relationship Configuration, as shown in the screenshot below:

<div align="center"><img src="../../.gitbook/assets/aha_reference_field_relation.png" alt="" width="1000"></div>

## Integration Configuration

Set a time to synchronize data between Aha! and the other system to be integrated. Also, define parameters and conditions (if any) for integration. Refer to [Integration Configuration](../integrate/integration-configuration.md) to learn the step-by-step process to configure the integration between two systems. Refer to the screenshot given below:

<div align="center"><img src="../../.gitbook/assets/aha_integration.png" alt="" width="1000"></div>

In Aha!, the entity type selection in integration configuration depends on the project selection. For more details, please refer to [Project Selection](aha.md#project-selection) section.

### Criteria Configuration

If the user wants to specify conditions for synchronizing an entity from Aha! as source system to the other system, the criteria must be configured. Navigate to Criteria Configuration section on [Integration Configuration](../integrate/integration-configuration.md) page to learn in detail about Criteria Configuration. Set the **Query** as per Aha! encoded query format. Criteria is only applicable to given four fields. Given below are the sample snippets of how the Aha! queries can be used as criteria query in <code class="expression">space.vars.SITENAME</code>:

**Criteria samples:**

| **Field Type**           | **Criteria Description**                                              | **Criteria snippet**                                                                                                                                                                                          |
| ------------------------ | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `q`                      | Synchronize all entities named as 'test feature'                      | q=test%20feature                                                                                                                                                                                              |
| `updated_since`          | Synchronize all entities updated after 10 March 2021                  | <p>updated_since=2021-03-10T00%3A00%3A00.000Z<br>Format: yyyy-MM-dd'T'HH:mm:ss.SSS'Z'</p>                                                                                                                     |
| `tag`                    | Synchronize all entities associated with the tag 'need review'        | tag=need%20review                                                                                                                                                                                             |
| `assigned_to_user`       | Synchronize all entities assigned to user 'ABC'                       | <p>Filter can be applied on User ID or User email.<br>For an example, assigned_to_user=7163902316942030700 /assigned_to_user=email%40opshub.com<br>Here, 7163902316942030700 is the id of the user 'ABC'.</p> |
| `updated_since` + `name` | Synchronize entities named 'test r \&d' and updated after 10 Mar 2021 | updated \_since=2021-03-10T00%3A00%3A00.000Z \&q=test%20r%26d                                                                                                                                                 |

### Target LookUp Configuration

* Provide Query in Target Search Query field such that it is possible to search the entity in the Aha! as the target system. In the target search query field, the user can provide a placeholder for the source system's field value in the '@'
* Go to **Search in Target Before Sync** section on [Integration Configuration](../integrate/integration-configuration.md) page to learn in detail about how to configure Target LookUp.
* Overall, Target LookUp Query is similar to [Criteria Configuration](aha.md#criteria-configuration), except that the value part contains a field name with '@' instead of static value.

**Target LookUp query samples:**

| **Field Type** | **Target lookup usecase**                                       | **Snippet**                |
| -------------- | --------------------------------------------------------------- | -------------------------- |
| `q`            | Target lookup on entity having source entity's id in name field | q='@source \_system \_id@' |

## Known Behaviour

* From Aha! UI, issue type can be changed for entity. Currently, such conversions will create a new entity in the target and the previous one will be orphaned.
* From Aha! UI, the entity can be deleted. However, for Aha! as the source system, the deleted entity will not sync by <code class="expression">space.vars.SITENAME</code>. The corresponding target entity will remain orphan in target system on Aha! entity deletion. Also, Aha! entity deletion is not supported by <code class="expression">space.vars.SITENAME</code>, when Aha! is the target system.
* To update the "Progress" field through synchronization, the progress source must be set to "manual" (from Aha! UI or field mapping of <code class="expression">space.vars.SITENAME</code>) due to Aha! API behavior.
* Goals and Initiative System fields will be available as lookup fields in the field mapping, even though they are not available in Aha! Develop UI.
  * **The above fields are available in Aha! Develop UI when the Aha! Develop instance is combined with Aha! Roadmap.**
  * **Note** The above fields will be deprecated in future releases and replaced with link-based support.
* Hierarchy sync is not supported. Hence, the synchronization of ranking the requirements and to-dos will not be supported.
* Entity mention is not supported for the following entities in the given scenarios:
  * **When Aha! is configured as the target system,** Entity mention is not supported for Goals, Notes, and To-Do entities.
  * **When Aha! is configured as the source system,** Entity mention through source URL configuration is not supported for the Goals entity.
* **Scorecard parameter values require additional configuration in OIM to sync.**
  * Refer to [Configuring Scorecard Parameter For Synchronization](aha.md#configuring-scorecard-parameter-for-synchronization)
  * Reason: Aha APIs do not provide scorecard parameter details.
* **Advanced XSLT configuration is required** to synchronize complex fields (such as table and worksheet types).
  * Refer to [Configure Advance XSLT For Complex Fields](aha.md#configure-advance-xslt-for-complex-fields) section.
* **Only read-only synchronization is supported** for the following fields
  * Scorecard fields
  * Table fields
  * Worksheet field
  * Custom choice field
  * Detailed estimate source for **Epic** entity
  * **Note**: Write support for these fields is planned for future releases.

### Project Selection

* For Aha! system, users can organize their data at different types of workspaces, i.e., Project, Products or Teams. Different entities can reside in different workspaces, for e.g., the Feature can belong to the Product while Activity can belong to the Project.

### API Rate Limitation in Aha!

* Aha! has limitation on API access per minute for a single user. Due to this, <code class="expression">space.vars.SITENAME</code> can access Aha! API within a limit. When the limit exceeds, the Aha! API stops responding for certain amount of time, and no API calls can be done by <code class="expression">space.vars.SITENAME</code> during that time until Aha! resets the limit for that user.
  * **Up to 300 requests per minute and 20 requests per second are allowed in Aha!.**
* To address this issue, wait time (given by Aha! API) will be considered for entity synchronization. Thus, there might be some delay in synchronization in case of API rate limit issue.
* **Note:** To avoid hitting rate limits, do not set the integration schedule to run every minute. Instead, adjust the cache timeout in <code class="expression">space.vars.SITENAME</code>(for example, 24 hours) and the integration schedule interval (for example, 15 minutes in production) to ensure smooth operation without exceeding rate limit
* **Recommendation:** To reduce the number of API calls, consider using the Fetch Mapped Data Only feature, which is available as an additional license add-on. To enable this feature, please contact your sales or support representative.

## Known Limitations

* Limitations due to the lack of Aha! API:
  * Audit/History Sync
    * **History is synced for the last 12 months only from current date.**
      * Reason: Aha APIs provide history data limited to the past 12 months.
      * Reference: [Aha Audits API](https://www.aha.io/api/resources/audits)
    * **Some fields support only current value sync (history is not available).**
      * Due to Aha's historical behavior(UI and API limitations): Scorecard parameters, Watchers, Custom brief type field, Actual vote count, Proxy voters and Submission portal details
      * Due to Aha's API limitations: Custom tables, Tags, Rich text fields, goals/initiatives and Estimate-related fields.
    * During history synchronization, changes in user fields may be synced as the wrong user in target, if multiple users share the same display name in Aha!.
      * Example:
        * User 1 in Aha!: Display Name = X, Email = a@gmail.com.
        * User 2 in Aha!: Display Name = X, Email = b@gmail.com.
        * If an update is made to “X” like X -> X in Aha!, the system may sync it to the wrong user in the target system.
        * Reason: The Aha! end system does not distinguish between users with identical display names through the UI/API.
    * **A 5-minute delay is applied to history based sync**
      * Reason: Aha consolidates audit records within a 5-minute interval. To avoid discrepancies or inconsistencies in history sync, this delay is introduced.
      * **Additional delay depends on polling/scheduling interval:**
        * Total delay = 5 minutes (processing) + configured polling interval.
        * Example: If polling is set to 5 minutes, creations/updates may reflect after approximately 10 minutes.
        * **Note:** To avoid dependency on the delay, you may run sync the current state and sync history separately in a tabular format in target system.
  * Metadata is not available for the system fields. So, we are providing static metadata in the system itself. Here, the user can change the display name of the entity. User can provide the entity name using the JSON input, and if any user doesn't provide any JSON input, an inbuild entity display name will be considered.
  * In Aha! Develop instance, for **Epic & Feature** type of entities, **Workspace** field is not available for synchronization.
  * In Aha! Develop instance, for **Requirement** type of entity, **Initial estimate, Detailed estimate & Actual effort** fields will not be synced.
  * State transition is not supported as API doesn't give the information about state transitions.
  * For synchronizing updates of **Proxy votes** and **Submission portal details** fields for Idea entities, an additional field update is required. This is because changes to these fields do not update the entity's last modified time.
  * **Custom Key Result** field is treated as a **text** field due to API unavailability.
  * Attachment field: If Aha! is the target system and the attachment mapping is configured to use field-type attachments, at least one attachment should be present in the corresponding field.
* For Aha! as the target system, the fields below will not unset via <code class="expression">space.vars.SITENAME</code> due to Aha!'s API limitation: **Effort, Value, Duration Source, Progress Source, Status, Type, Complete by date (internal), Round date to, Complete by date (external), Presented, and Description.**
* **To-dos** present at user level will not synced by <code class="expression">space.vars.SITENAME</code>. **To-dos** present in other entities can only be synchronized.

### Troubleshooting Guide

If you are getting an **Internal Server Error** with **Status Code: 500**, then you should retry the failures. There is a limitation of the Aha! API that if we perform updates on entities from same project at the same time, deadlocks occur in their database. It can cause the above-mentioned error.

## Appendix

### Add User

1. Login to Aha! using the user with privileges to create a new user.
2. Navigate to Settings given at the top right corner and go to Account section.

<div align="center"><img src="../../.gitbook/assets/aha_add_user_1.png" alt=""></div>

3 . Navigate to Users

<div align="center"><img src="../../.gitbook/assets/aha_add_user_2.png" alt=""></div>

4 . Click on the Add User button given at the top right corner of the users' list.

<div align="center"><img src="../../.gitbook/assets/aha_add_user_3.png" alt=""></div>

5 . Fill the details regarding the user. For the Administration Role and Permissions for different workspaces, select the roles having permissions mentioned in \[User privileges] (#user-privileges) section.

<div align="center"><img src="../../.gitbook/assets/aha_add_user_4.png" alt=""></div>

6 . Save changes

### Grant permissions to Aha! user

1. Login to Aha! using the user with privileges to grant permissions to any user.
2. Navigate to Settings and go to **Account->Users** section.
3. Navigate to **Users** and select the user for which you want to change the permissions.

<div align="center"><img src="../../.gitbook/assets/aha_change_user_permission_1.png" alt=""></div>

4 . Select Administrator roles and Permissions for different workspaces you want to give to integration user.

<div align="center"><img src="../../.gitbook/assets/aha_change_user_permission_2.png" alt=""></div>

5 . Save changes

### Add Custom Fields

1. Navigate to Settings given at the top right corner and go to Personal section.

<div align="center"><img src="../../.gitbook/assets/aha_api_token_1.png" alt=""></div>

2 . Navigate to Custom fields section.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_field_1.png" alt=""></div>

3 . Select the entity for which you want to create the custom field, and click Add custom field.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_field_2.png" alt=""></div>

4 . Choose custom field type from the list and click Next.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_field_3.png" alt=""></div>

5 . Fill the details for creating the selected custom field.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_field_4.png" alt=""></div>

### Add Custom Layout

1. Navigate to Settings given at the top right corner and go to Personal section.

<div align="center"><img src="../../.gitbook/assets/aha_api_token_1.png" alt=""></div>

2 . Navigate to Custom layouts section.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_layout_1.png" alt=""></div>

3 . Select the entity for which you want to create the custom layout, and click Add custom layout.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_layout_2.png" alt=""></div>

4 . You can choose to create a new custom field or select from the existing custom field from the list.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_layout_3.png" alt=""></div>

5 . If you choose to use an existing custom field, you can drag and drop it to the fields list given on the right side.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_layout_4.png" alt=""></div>

6 . If you choose to create a custom field, you can drag and drop it to the fields list given on the right side. Fill the details for creating the custom fields.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_layout_5.png" alt=""></div>

7 . Give the name to the layout and save it.

### Steps for generating the API token

1. Navigate to Settings given at the top right corner and go to Personal section.

<div align="center"><img src="../../.gitbook/assets/aha_api_token_1.png" alt=""></div>

2 . Navigate to the Developer section.

<div align="center"><img src="../../.gitbook/assets/aha_api_token_2.png" alt=""></div>

3 . In the API keys section, click Generate API key.

<div align="center"><img src="../../.gitbook/assets/aha_api_token_3.png" alt=""></div>

4 . Give name to the key and click on Generate API key.

<div align="center"><img src="../../.gitbook/assets/aha_api_token_4.png" alt=""></div>

5 . Copy the generated API key and save it for future reference.

### Configuring Scorecard Parameter For Synchronization

To synchronize **scorecard parameter values from Aha**, additional configuration is required in OIM because Aha APIs do not return these values by default.

#### 1. System Scorecard Fields

*   Use the following format for `internalName`: Product value.\<Parameter name>. Example json:

    ```json
    {
      "internalName": "Product Value.Need",
      "displayName": "Need",
      "dataType": "numeric",
      "mandatory": false,
      "historyEnabled": false
    }
    ```

#### 2. Custom Scorecard parameter fields:

*   Use the following format for `internalName`: custom\_\<CustomFieldKey>.\<Parameter Name>. Example json:

    ```json
     {
        "internalName": "custom_customscorecard.Sales increase",
        "displayName": "Sales increase",
        "dataType": "numeric",
        "mandatory": false,
        "historyEnabled": false
     }
    ```

3. The display name for the scorecard parameter field is configurable. The value specified as the display name will be reflected in the <code class="expression">space.vars.SITENAME</code> mapping configuration screen.
4. The last three parameters in the JSON configuration remain consistent across all scorecard parameters.
5.  The \<Parameter name> specified in the internalName field corresponds to the name displayed in the UI for the respective scorecard. Refer to screenshot below for illustration.

    <div align="center"><img src="../../.gitbook/assets/Aha_ParameterName.png" alt=""></div>
6. The \<Custom Scorecard fieldKey> represents the unique key of the custom field. For details on identifying the custom field key, refer to [Get Custom Field Unique Key](aha.md#get-custom-field-unique-key).

### Configure Advance XSLT For Complex Fields

#### 1. Table Field → Rich Text (e.g., Jira Description)

To synchronize a table type field(for example `oh_table_field`) that contains three columns: **Name**, **Primary customer contact**, **Email address** to rich text type field like Description in Jira in table format, refer to the following sample advance XSLT:

```xml
       <description xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
        <xsl:text>||*Name*||*Primary customer contact*||*Email address*||</xsl:text>
        <xsl:variable name="nodes" select="/SourceXML/updatedFields/Property/custom__oh__table__field/list"/>
        <xsl:for-each select="$nodes[position() mod 3 = 1]">
            <xsl:variable name="start" select="((position() - 1) * 3) + 1"/>
            <xsl:text>&amp;#10;|</xsl:text>
            <xsl:choose>
                <xsl:when test="normalize-space($nodes[$start]/Property/value) != ''">
                    <xsl:value-of select="$nodes[$start]/Property/value"/>
                </xsl:when>
            </xsl:choose>
            <xsl:text>|</xsl:text>
            <xsl:choose>
                <xsl:when test="normalize-space($nodes[$start + 1]/Property/value) != ''">
                    <xsl:value-of select="$nodes[$start + 1]/Property/value"/>
                </xsl:when>
            </xsl:choose>
            <xsl:text>|</xsl:text>
            <xsl:choose>
                <xsl:when test="normalize-space($nodes[$start + 2]/Property/value) != ''">
                    <xsl:value-of select="$nodes[$start + 2]/Property/value"/>
                </xsl:when>
            </xsl:choose>
            <xsl:text>|</xsl:text>
        </xsl:for-each>
    </description>
```

1.  The table field in aha is illustrated in the image below:

    <div align="center"><img src="../../.gitbook/assets/Aha_Table.png" alt=""></div>
2.  The data after transformation and synchronization to Jira is shown in the following image:

    <div align="center"><img src="../../.gitbook/assets/Jira_Table.png" alt=""></div>

#### 2. Worksheet Field → Rich Text

To synchronize complex type worksheet field(for example, `custom_worksheet`) that contains two columns: **Column Name** and **Value** to a rich text field like Custom Description in Jira, refer to below sample advance XSLT:

```xml
       <customDescription xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
        <xsl:text>||*Column Name*||*Value*||</xsl:text>
        <xsl:for-each select="/SourceXML/updatedFields/Property/custom__customworksheet/Property/values/Property">
            <xsl:text>&amp;#10;|</xsl:text>
            <xsl:value-of select=".//Property[name][1]/name"/>
            <xsl:text>|</xsl:text>
            <xsl:choose>
                <xsl:when test="normalize-space(.//Property/value) != ''">
                    <xsl:value-of select=".//Property[value][1]/value"/>
                </xsl:when>
                <xsl:otherwise>
                    <xsl:text/>
                </xsl:otherwise>
            </xsl:choose>
            <xsl:text>|</xsl:text>
        </xsl:for-each>
    </customDescription>
```

1.  The worksheet field in aha is illustrated in the image below:

    <div align="center"><img src="../../.gitbook/assets/Aha_Worksheet.png" alt=""></div>
2.  The data, after transformation and synchronization to Jira, is illustrated in the following image:

    <div align="center"><img src="../../.gitbook/assets/Jira_Worksheet.png" alt=""></div>

### Get Custom Field Unique Key

#### Getting Custom Field Unique Key Using API.

* To retrieve custom fields via the API, use the following endpoint: \<aha-instance>/api/v1/custom\_field\_definitions. This can be accessed through browser or tools such as Postman.
*   Sample JSON response is shown below:

    ```json
        {
          "custom_field_definitions": [
              {
                  "name": "Custom Attachment",
                  "id": "7174752533322023770",
                  "key": "custom_attachment_feature",
                  "type": "CustomFieldDefinitions::AttachmentField",
                  "custom_fieldable_type": "Feature",
                  "internal_name": null
              },
              {
                  "name": "Custom Attachment",
                  "id": "7624035087472118759",
                  "key": "custom_attachment_initiative",
                  "type": "CustomFieldDefinitions::AttachmentField",
                  "custom_fieldable_type": "Initiative",
                  "internal_name": null
              }
          ]
        }
    ```
* The value in the **key** field represents the unique identifier for a specific custom field.
* **Note** Multiple custom fields across different entity types may share the same name. Ensure that the key is interpreted in the context of its corresponding entity type (`custom_fieldable_type`).

#### Getting Custom Field Unique From UI.

add after login go to user profile and find the value

1. Navigate to the User Personal section under Settings by clicking on the user profile icon located in the top-right corner after logging in

<div align="center"><img src="../../.gitbook/assets/Aha_User_Profile.png" alt=""></div>

2 . Navigate to Custom fields section.

<div align="center"><img src="../../.gitbook/assets/aha_add_custom_field_1.png" alt=""></div>

3 . Select the entity for which you want to identify the custom field key, and locate the relevant custom field.

<div align="center"><img src="../../.gitbook/assets/Aha_CustomField.png" alt=""></div>

4. Open the Advanced Configuration settings for the selected custom field.

<div align="center"><img src="../../.gitbook/assets/Aha_CustomAdvanceOptions.png" alt=""></div>

5. Retrieve the value displayed in the Key field.

<div align="center"><img src="../../.gitbook/assets/Aha_CustomFieldKey.png" alt=""></div>
