# Custom Conflict Resolution Strategy

Custom Conflict Resolution Strategy assists user in making complex resolution decisions based on the run time values in the source and target systems. With this strategy, users can resolve conflict by considering which end point was updated last or which end point was updated first. User can also make the master/slave decision at run time, based on the current state of the end systems. For example, whether the end system in which a workitem is still open becomes the master or a system in which workitem was not created by sync becomes the master and so on.

***

## Steps to provide XSLT for defining Custom Strategy

Given below are steps to provide XSLT for custom strategy:

* Click the edit adjacent to the **Custom Strategy** drop-down option.

<div align="center"><img src="../../.gitbook/assets/XSLT1.png" alt="" width="1000"></div>

* Remove comments and provide XSLT in the open box.

<div align="center"><img src="../../.gitbook/assets/XSLT.png" alt="" width="400"></div>

***

### Field Value Access Table

| Description                              | Example                                                                                                                                    |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **You can access the source old value:** | <p><code>SourceXML/sourceSystemOld/Property/$FieldName$</code><br><em>$FieldName$ is the internal name of the source system field</em></p> |
| **You can access the source new value:** | <p><code>SourceXML/sourceSystemNew/Property/$FieldName$</code><br><em>$FieldName$ is the internal name of the source system field</em></p> |
| **You can access the target value:**     | <p><code>SourceXML/targetSystem/Property/$FieldName$</code><br><em>$FieldName$ is the internal name of the target system field</em></p>    |

***

### Example

For example, take that resolution strategy for Title field is 'master system is selected based on originated-in system.'\
We can provide the script:

```xml
<Title>
  <xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="xPathVariable" select="SourceXML/sourceSystemNew/Property/Created-space-By/userEmail"/>
  <xsl:choose xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:when test="$xPathVariable='test@opshub.com'">
      <xsl:value-of select="SourceXML/targetSystem/Property/Title"/>
    </xsl:when>
    <xsl:otherwise>
      <xsl:value-of select="SourceXML/sourceSystemNew/Property/Title"/>
    </xsl:otherwise>
  </xsl:choose>
</Title>
```
