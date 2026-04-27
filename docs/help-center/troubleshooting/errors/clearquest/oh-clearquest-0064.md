# OH-ClearQuest-0064

### Description

When the user encounters OH-ClearQuest-0064, the following type of error message will appear:

OH-ClearQuest-0064: Invalid Filter `<Filter Fields Name>` encountered for the query `cq.query:Personal Queries/OpsHub_<QueryName><EntityName>`. Expected filter(s) are `<Filter Fields Name>`.

Example: :: OH-ClearQuest-0064: Invalid Filter Owner.login\_name encountered for the query `cq.query:Personal Queries/OpsHub_LastCreatedByIntegration<EntityName>`. Refer OIM product guide for more details on this query configuration. Expected filter(s) are \[history.user\_name, history.action\_timestamp, history.old\_state]

### Cause

_This issue occurs when upgrading_ <code class="expression">space.vars.SITENAME</code> _to version 7.78 or higher. It throws event failure as the query filters format is changed._\
&#xNAN;_&#x54;he **query filters** for the particular query are not correctly selected._

### Solution

Update the **query filters** as mentioned in the IBM ClearQuest Rational connector documentation. Refer to the [Queries Configuration](../../../../connectors/ibm-rational-clearquest.md#queries-configuration) section.
