# OH-ClearQuest-0065

### Description

When the user encounters OH-ClearQuest-0065, the following type of error message will appear:

OH-ClearQuest-0065: Expected display field(s) `<Display Fields Name>` of Query Presentation encountered as empty or null, Verify the display field(s) of this query `Personal Queries/OpsHub_<QueryName><EntityName>` on end system.

Example:\
\
OH-ClearQuest-0065: Expected display field(s) id,action\_timestamp of Query Presentation encountered as empty or null, Verify the display field(s) of this query `Personal Queries/OpsHub_LastCreatedByIntegrationBaseCMActivity` on end system.

### Cause

_This issue occurs when upgrading_ <code class="expression">space.vars.SITENAME</code> _to version 7.78 or higher. It throws event failure as the query filters format is changed._\
&#xNAN;_&#x54;he **query presentation fields** or their names for the particular query are not correct._

### Solution

Update the **query presentation fields** as mentioned in the IBM Rational ClearQuest connector documentation. Refer to the [Queries Configuration](../../../../connectors/ibm-rational-clearquest.md#queries-configuration) section.
