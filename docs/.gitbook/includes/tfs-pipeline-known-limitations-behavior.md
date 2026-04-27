---
title: tfs-pipeline-known-limitations-behavior
---

* Attachments, Comments, and Inline images' synchronization is not supported.
  * Reason: Build Pipeline does not have Attachments, Comments, and Inline images.
* End System Criteria Storage is not supported.
  * Reason: Build Pipeline does not have any custom fields.
* Secure Files and Azure Git Repositories with the same names in the source system must be present in the target system to avoid any sync failures.
* Impersonation is not supported.
* For on-premise deployment, there is a Retention tab in the Build Pipeline entity \[not available in cloud deployment]. This Retention tab synchronization is not supported.
* Process parameters are not supported.
* During the Build Pipeline entity synchronization, the processing failure may come while syncing the Service Connection for the below mentioned use case. For more details around the next steps, refer to [this](../../help-center/faqs/tfs/pipelineserviceconnectionfailure.md) section.
  * Use case: Service Connection 1 was associated with some steps of any job in the Pipeline entity. The user changed the Service Connection from Service Connection 1 to Service Connection 2 and deleted the Service Connection 1 from the end system.

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}
- Actual revision time and user email are suffixed to the comment of that particular revision.
{% endif %}
