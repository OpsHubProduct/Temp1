# How to map Jira's Wiki type of field for getting proper formatting?

### Description

How to map Jira's Wiki type of field for getting proper formatting?

Are you facing formatting issue while synchronizing these field cases:

* Case 1: HTML field (Any source system) to Wiki field (Jira)
* Case 2: Wiki field (Jira) to HTML field (Any target system)
* Case 3: Wiki field (Jira) to Text field (Any target system)

This page will guide you through the cause and solution for the same.

### Cause

If <code class="expression">space.vars.SITENAME</code> is able to decide whether the source or target Jira field is of type text or wiki then <code class="expression">space.vars.SITENAME</code> would be able to handle the formatting by itself. But the formatting cannot be handled by default by <code class="expression">space.vars.SITENAME</code> as the Jira API doesn't provide the information whether a text field is a simple text field or wiki type of field.

Therefore, irrespective of whether the field is wiki or text type of field in Jira, it is by default considered as text type of field during the field mapping.

### Solution

By default, **Description** field in Jira is considered as Wiki field and you will not face any such issue while synchronizing to or from this field. But for other fields, you need to change the default XSLT configuration.

**Steps for solving the issue:**

1. Go to the mapping for which you are facing the formatting issue.
2. For expanding the advance mapping settings, click ![AdvanceMappingExpandv2.png](../../../../.gitbook/assets/AdvanceMappingExpandv2.png) on the frame separator.
3. [View/Edit XSLT Configurations](../../../integrate/mapping-configuration.md#view-edit-xslt-configurations-options) can be used to change the default mapping XSLT. Click ![XSLT\_icon\_blue.png](../../../../.gitbook/assets/XSLT_icon_blue.png) to change the default behaviour of the field for which you are facing this formatting issue.
4. You can find the values for the Source and Target fields' names in the xslt format, which you can use to substitute in the snippets given below.
5. Find your snippet in cases given below. In these snippets, we have considered the source and target fields as `Source Field` and `Target Field` respectively. Before using a snippet, replace the `Source-space-Field` and `Target-space-Field` with the value that you receive during advance mapping.

**Cases:**

#### Case 1: HTML field (Any source system) to Wiki field (Jira) formatting issue

**Problem faced:**\
If you have mapped a source HTML field with target Wiki field (any field other than Description) in Jira, while synchronizing the entity, Jira's Wiki type of field will not have rich text format. Instead, in Jira, you will observe that the text is in simple text format.

**XSLT snippet for solving the issue:**

```xml
<Target-space-Field>
  <xsl:value-of xmlns:xsl="http://www.w3.org/1999/XSL/Transform" 
    select="utils:convertHTMLToWikiKeepImgTag(SourceXML/updatedFields/Property/Source-space-Field)"/>
</Target-space-Field>
```

#### Case 2: Wiki field (Jira) to HTML field (Any target system) formatting issue

**Problem faced:**\
If you have mapped a source Wiki field(Any field other than Description) with target HTML field in Jira, while synchronizing the entity, the target system's HTML field will not have rich text format. Instead in the target system, you will observe that the HTML field has some additional unwanted text.

**XSLT snippet for solving the issue:**

```xml
<Target-space-Field>
  <xsl:value-of xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                select="utils:convertWikiToHTML(SourceXML/updatedFields/Property/Source-space-Field)"/>
</Target-space-Field>
```

#### Case 3: Wiki field (Jira) to Text field (Any target system) formatting issue

**Problem faced:**\
If you are synchronizing the Wiki field from Jira to any simple Text field (non-rich text field) in the target system, you would observe that the text field has some additional unwanted text.

**XSLT snippet for solving the issue:**

```xml
<Target-space-Field>
  <xsl:value-of xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                select="utils:convertWikiToText(SourceXML/updatedFields/Property/Source-space-Field)"/>
</Target-space-Field>
```
