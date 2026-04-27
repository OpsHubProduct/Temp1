# Attachment-naming-convention-related-errors

### Description

When the user encounters attachment naming convention related error, then the following error message will appear:\
&#xNAN;**"URLDecoder: Illegal hex characters in escape (%) pattern - For input string: "^&""**

### Cause

When any system is selected as the target system, if the attachment file name contains **Invalid file name characters** (`%`, `:`) or **Non-ascii characters** like (`样`, `品`, `テ`, `ス`, `ト`, `フ`, `ァ`, `イ`, `ル`, `★`, `✓`, `♛`, `Ω`), then the file will not be added in end system. Consequently, the user will encounter a processing failure.

### Solution

* If the attachment file name contains Windows invalid characters (`%`, `:`) or Non-ascii characters like (`样`, `品`, `テ`, `ス`, `ト`, `フ`, `ァ`, `イ`, `ル`, `★`, `✓`, `♛`, `Ω`), then add advance mapping for attachments to replace special characters with any of the supported characters.
*   Refer to the snippet below for a sample advance mapping for attachments in which all the earlier specified invalid characters are being replaced by an underscore (`_`) in the attachment file name:

    ```xml
    <OHAttachments>
        <xsl:for-each xmlns:xsl="http://www.w3.org/1999/XSL/Transform" select="SourceXML/updatedFields/Property/OHAttachments/OHAttachment">
            <xsl:element name="{concat('attachment_',position())}">
                <filename>
                    <xsl:value-of select="translate(fileName, '%:name', '__name')"/>
                </filename>
                <addedByUser>
                    <xsl:value-of select="addedByUser"/>
                </addedByUser>
                <contentLength>
                    <xsl:value-of select="contentLength"/>
                </contentLength>
                <contentType>
                    <xsl:value-of select="contentType"/>
                </contentType>
                <contentBase64>
                    <xsl:value-of select="contentBase64"/>
                </contentBase64>
                <attachmentURI>
                    <xsl:value-of select="attachmentURI"/>
                </attachmentURI>
                <updateTimeStamp>
                    <xsl:value-of select="updateTimeStamp"/>
                </updateTimeStamp>
                <label>
                    <xsl:value-of select="label"/>
                </label>
                <fileComment>
                    <xsl:value-of select="fileComment"/>
                </fileComment>
                <attachmentReferenceType>
                    <xsl:value-of select="attachmentReferenceType"/>
                </attachmentReferenceType>
                <uniqueCode>
                    <xsl:value-of select="uniqueCode"/>
                </uniqueCode>
                <attachmentType>
                    <xsl:variable name="xPathVariable" select="attachmentType"/>
                    <xsl:value-of select="attachmentType"/>
                </attachmentType>
            </xsl:element>
        </xsl:for-each>
    </OHAttachments>
    ```
