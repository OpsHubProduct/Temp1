---
title: tfs-release-pipeline-known-limitations-behavior
---

**Pre-requisite:**

Before starting synchronization, please make sure the following items already exist in the target environment. These are required to in target due to Azure DevOps API Restrictions/limitations.

> **Note**: Once the required data exists in the target environment, the synchronization automatically links/refers to the above components during Release Pipeline synchronization, ensuring no references are lost.

* **Azure Artifacts:** The feed and package must pre-exist in the target project.
  * The feed and package name can be the same as the source or a transformed name that OpsHub can use to look up and reference in target project during pipeline synchronization — for example, abc-package or Synced\_abc-package.
  * For TFS versions earlier than 2019, along with pre-existing data, their linkage must be done manually after Release Pipeline sync, as Azure Artifacts APIs are only supported from TFS 2019 onward.
* **Deployment Group:** If a release stage includes a Deployment Group Job, the same deployment group must pre-exist in the target project.
  * The group name can be the same as the source or a transformed name that OpsHub can use to look up and reference in target project during pipeline synchronization — for example, Prod-Deploy or Prod-Deploy-New.
* **Secure Files:** Secure files must pre-exist in the target system.
  * The file name can be the same as the source or a transformed name that OpsHub can use to look up and reference in target project during pipeline synchronization — for example, BuildKey or Synced\_BuildKey
* **Azure Git Repositories** with matching names pre-existing in the target project

> **Note:** If any of the above resources do not exist in the target project, the sync operation will fail because the Release Pipeline depends on these resources for successful execution.

* Release Pipeline may contain reference of Query, Agent Pools, Service Connection, Task Group, Build Pipeline so these dependent entities must be synced before Release Pipeline to avoid the sync failure. <code class="expression">space.vars.SITENAME</code> support all these dependent artifacts sync along with Release Pipeline.
  * For TFS versions earlier than 2020, due to API unavailability, the Agent Pools must pre-exist and be linked manually after Release Pipeline sync.

**Known Behaviour and Limitations:**

* Release Pipeline will be synced TFS version 2018 or above, as APIs are available from that version only.
* Release Pipeline does not have Attachments, Comments, and Inline images, hence Attachments, Comments, and Inline images won't be synchronization.
* End System Criteria Storage is not supported.
  * Reason: Release Pipeline does not have any custom fields.
* Impersonation is not supported.
  * Reason: ADO/TFS API limitation.
* Synchronization of security permissions for individual Release Pipelines is not supported.
