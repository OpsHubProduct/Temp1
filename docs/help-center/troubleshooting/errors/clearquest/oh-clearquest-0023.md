# OH-ClearQuest-0023

### Description

When the user encounters OH-ClearQuest-0023, the following type of error message will appear:

OH-ClearQuest-0023: Query Parameter(s) not matched, Expected query parameter(s) are `<Filter Fields Name>` for the query Personal `Queries\OpsHub_<Query Name><EntityName>`.

Example:\
OH-ClearQuest-0023: Query Parameter(s) not matched, Expected query parameter(s) are \[history.user\_name, history.action\_timestamp, history.old\_state] for the query Personal Queries`\OpsHub_LastCreatedByIntegration<EntityName>`.

### Cause

_This issue occurs when upgrading_ <code class="expression">space.vars.SITENAME</code> _to version 7.78 or higher. It throws event failure as the query filters format is changed._\
&#xNAN;_&#x41;ll the required **query filters** for this particular query are not added to the end-system query._

### Solution

Update the **query filters** as mentioned in the IBM ClearQuest Rational connector documentation. Refer to the [Queries Configuration](../../../../connectors/ibm-rational-clearquest.md#queries-configuration) section.
