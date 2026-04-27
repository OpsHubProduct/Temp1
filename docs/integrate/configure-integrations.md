# Integration Setup

Integration is the process of connecting two or more systems in order to enable a seamless exchange of information between the system users. Each system has its own set of prerequisites for successful configuration.\
Please refer to [Integration Prerequisites](integration-prerequisites.md) page to check the pre-requisites of the systems you want to integrate before you proceed.

## Steps to Configure an Integration

### Configure System (s)

* In this video, we will learn how to configure a system onto and how to update the system details after configuration, if required

> **Note**: Jira is the system that has been used for this video demonstration. The steps may vary slightly from one system to another.

{% embed url="https://youtu.be/Po6K9_UXrfM" %}

> **Note**: During configuration or synchronization, connection-related errors might occur. There are couple of reasons for connection-related errors. Checkout the details [Common Error Solutions](../help-center/troubleshooting/errors/common-error-solutions.md).\
> **Note**: If the system is behind a proxy server, then set up [Proxy Setting](../manage/administrator/proxy-setting.md) in <code class="expression">space.vars.SITENAME</code>.\
> **Note**: For details on how to configure systems, refer [System Configuration](system-configuration.md)

### Select Projects and Entities

The next step is to define entities and fields to be integrated and fields that need to be integrated for every entity mapped. But before that, check whether the system is behind proxy or not.\
If the system is on HTTPS, then [Import SSL Certificates](../getting-started/ssl-certificate-configuration.md) onto <code class="expression">space.vars.SITENAME</code>'s Java KeyStore.\
<code class="expression">space.vars.SITENAME</code> fetches entities available in both systems and shows them in the entities list for both systems.\
From the Select Entities to Sync section, select the relevant entities for both systems.\
In this video, we learn to integrate Bug entities between Jira and Azure DevOps Services (VSTS):

{% embed url="https://youtu.be/HMbMW_t5v5w" %}

### Mapping Fields

Mapping is the process of defining the fields that are to be integrated between the given projects and entities of two systems. It is during the mapping stage that the flow of data (From System 1 to System 2, From System 2 to System 1 or bi-directional flow between System 1 and System 2) is also defined.\
In this video, we will see how to map fields between Jira and Azure DevOps Services (VSTS).

{% embed url="https://youtu.be/vbnw92pPLFM" %}

#### Value Mapping for Look-Up Type Fields

Look-up type fields are multi-valued fields.\
During mapping the fields for integration, the values of Look-up fields must be mapped for the mapped entities.\
In this case, for example, we choose Priority and Status as the Look-up type fields to be mapped. We map Priority to Priority and Status to State.

#### Default Mapping

Default Mapping is used to write default value to target field in case there is no value coming from mapped source fields.\
Shown below is the Default Mapping pop-up, which opens on clicking the ![](../../.gitbook/assets/rotate.png) icon.

> **Note**: The default flow is bi-directional. None is generally used to put default values for fields on target side, which do not have relevant source field to be mapped.

1. For user mapping, default value should be configured in form of user name or email as user name as expected by target end-point.
2. For user mapping, the default value will be written to target if
   * The source value is missing or
   * A matching user is not found in the target.

> **Note**: For details on how to configure mappings, refer [Mapping Configuration](mapping-configuration.md)

### Configure Filter(s) (Optional)

Criteria Filter/Configuration helps in integration of subset of entities based on some conditions.\
For example, user can specify that bugs with high priority only are to be synchronized or tickets that are closed should be synchronized.\
Even after the entities are integrated, this synchronization based on defined criteria is retained. It is not mandatory to configure a filter/criterion for each integration.

{% embed url="https://youtu.be/44prb4ssjTY" %}

> **Note**: The format in which you enter condition in the Query field will vary from one system to another.

> **Note**: For details on how to configure integrations, refer [Integration Configuration](integration-configuration.md)

### Save and Activate Integration

You can now save and activate the integration.

{% embed url="https://youtu.be/5bcgNpsfGGU" %}

> **Note**:The Polling time is automatically set for the integration based on the system used for integration.

* For Build systems and Source Control Management systems, last updated created changeset/revision will be set as start polling time. If source system does not have any data created, then by default, it will be set to **0**.
* For Application Lifecycle Management (ALM), Product Lifecycle Management (PLM), and Test Management systems, polling time is set to the last updated time on the selected source projects. If the project does not have data then polling time is set to the CurrentTime -26 hours.
* If user wants to change the default polling time, then click the **Entity Level Mandatory Settings** button given beside entity mapping option.

### Troubleshooting

Create/Update event in the source system and check whether the event synchronizes to the target system.\
If you face any issue, please refer to the [General FAQs](https://github.com/OpsHubProduct/OIM-Documentation/blob/main/docs/help-center/faqs/faqs.md)

You can also see the steps to manage an integration from this page [Managing Integrations](integration-configuration.md#managing-integration)

### Additional Configuration

> **Note**: Please de-activate the integration to make these changes. You can save and activate the integration again after you have made the changes.

* Mapping more fields: Now that you have set the basic integration in place and checked that it is working as expected, you can edit the integration to add more fields.\
  User fields are mapped by email id. If e-mail ids of the users are same in both the systems, it will be mapped automatically, but if the email ids are not same, you will have to update the [Value Mapping using Excel sheet](mapping-configuration.md#value-mapping-using-excel-sheet) for user fields mapping.

> **Note**: For user mapping, the default value should be configured in form of user name or email as user name as expected by target end-point.\
> **Note**: For user mapping, the default value will not be written to target even if the matching user is not found in the target.\
> This will be done only if nothing is coming from the mapped source field.

* At this stage, test the integration by trying to synchronize data between the specified System 1 and System 2 projects.

You should not be using the integration user credentials to create entities in the systems as in this case the integration will not work.\
Create/Update event in the source system and check whether the event synchronizes to the target system.\
Wait for one minute for the data to synchronize.\
If you face any issue, please refer to [Possible Reasons and Fixes](../help-center/faqs/general-faqs.md)
