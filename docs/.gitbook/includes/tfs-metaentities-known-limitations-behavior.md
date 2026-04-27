---
title: tfs-metaentities-known-limitations-behavior
---

* Impersonation is not supported.
* Synchronization of Meta Entities for Team Foundation Server 2010 or lower is not supported.
* <code class="expression">space.vars.SITENAME</code> will not sync the following two permissions at collection level for Group and Users due to lack of API:
  * Delete team project
  * Delete team project collection However, the first permissions for a group or a user will be set at the project level.
* Synchronization of the groups with reserved name is only possible if they are present in the target system. If such groups are not present in the target system, processing failures will be observed in <code class="expression">space.vars.SITENAME</code>.
  * Reason: Groups cannot be created with reserved names, i.e., Group name 'Endpoint Creators' is reserved by the end system. While trying to create this group, a failure error message will be generated, 'Cannot complete the operation because the group name 'Endpoint Creators' is reserved by the system.'
  * User needs to manually delete this failure and start the synchronization again.
* If integration user is not a member of Project Collection Administrators group, collection level permissions will not be synchronized.
* Following are the limitations of <code class="expression">space.vars.SITENAME</code>, if you are syncing Area or Iteration:
  * Target Lookup Query is supported for only one field i.e. Path and the query must be Path=@Path@ for Team Foundation Server to Team Foundation Server integration.
  * Recovery functionality is effective only when Manual Conflict Detection is put off for field Path. It could be set to 'disable conflict detection' or enabled with either 'Source Wins' or 'Target Wins'.
  * Restart Team Foundation Server and OpsHubTFSService.
