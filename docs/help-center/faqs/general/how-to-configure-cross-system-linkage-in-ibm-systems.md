# How to configure cross system linkages between IBM systems?

## Overview

This document outlines the implementation of advanced mapping techniques to enable cross-system linkage between IBM tools (such as IBM Rational Doors and IBM Engineering Test Management). The solution supports bidirectional integration and maintains traceability across systems by leveraging advanced XSLT logic.

## Use Case Description

Suppose a user wants to integrate or migrate between IBM systems to other external system with cross systems linkage.\
For example, there are two main integrations:

| Source System | Source Artifact    | Target System | Target Artifact | Integration Type                              |
| ------------- | ------------------ | ------------- | --------------- | --------------------------------------------- |
| DNG           | System Requirement | Jira          | Epic            | Unidirectional \[Requirement to Epic mapping] |
| ETM           | Test Case          | Jira          | Bug             | Unidirectional \[Test Case to Bug mapping]    |

## For IBM Engineering Test Management

### **ETM as a Source**

* Read side of External Link \[a.k.a Requirement Links] given in Test Plan and Test Case.
* In ETM External Links can be given as:

<p align="center"><br><em>Select the System</em></p>

* The use case involves linking a **System Requirement** from IBM DNG as an external link within ETM. Additionally, the goal is to link a **Jira Epic** to a **Jira Bug** using a defined link type within Jira.
* For this below advance XSL is needed:

**OHEntityReferences XSLT Advance Mapping**

```xml
<OHEntityReferences xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:entityRef="http://com.opshub.eai.EAIEntityRefrences" xmlns:entityInfo="http://com.opshub.dao.eai.OIMEntityInfo">
  <xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="nonDefaultLinks" as="item()*">
    <Item targetLinkType="Is-space-Tested-space-By">Requirement</Item>
  </xsl:variable>
  <xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="entityTypeMapping" as="item()*"/>
  <xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="defaultLinkWithSourceLinks" as="item()*"/>
  <xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="defaultLinkWithOH_DEFAULT" as="item()*"/>
  <xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="entityReferencecontext" select="/SourceXML/updatedFields/Property/OHEntityReferences/OHEntityReference"/>
  <xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="linksToBeCarriedFromSourceEvent" as="item()*">
    <xsl:for-each select="$nonDefaultLinks">
      <xsl:variable name="currentLinkType" select="."/>
      <xsl:if test="$entityReferencecontext/linkType[text()=$currentLinkType]">
        <xsl:if test="$entityReferencecontext[linkType[text()=$currentLinkType]]/links/EAILinkEntityItem">
          <Item targetLinkType="{@targetLinkType}">
            <xsl:value-of select="."/>
          </Item>
        </xsl:if>
      </xsl:if>
    </xsl:for-each>
  </xsl:variable>
  <xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="linksToBeAddedAsDefault" as="item()*">
    <xsl:for-each select="$defaultLinkWithOH_DEFAULT">
      <Item lookupQuery="{@lookupQuery}" entityType="{@entityType}">
        <xsl:value-of select="."/>
      </Item>
    </xsl:for-each>
    <xsl:for-each select="$defaultLinkWithSourceLinks">
      <xsl:variable name="currentLinkType" select="."/>
      <xsl:if test="not($linksToBeCarriedFromSourceEvent[text() = $currentLinkType] = $currentLinkType)">
        <Item lookupQuery="{@lookupQuery}" entityType="{@entityType}">
          <xsl:value-of select="./@targetLinkType"/>
        </Item>
      </xsl:if>
    </xsl:for-each>
  </xsl:variable>

  <xsl:for-each xmlns:xsl="http://www.w3.org/1999/XSL/Transform" select="$linksToBeCarriedFromSourceEvent">
    <xsl:variable name="currentLinkType" select="."/>
    <op_list>
      <xsl:element name="{@targetLinkType}">
        <xsl:for-each select="$entityReferencecontext[linkType=$currentLinkType]/links/EAILinkEntityItem">
          <xsl:choose>
            <!-- Changes from here -->
            <xsl:when test="isExternalLink = 'true'">
              <xsl:element name="{concat('_',position())}">
                <xsl:element name="GlobalId">
                  <!-- Storing the current linked entity's internal ID -->
                  <xsl:variable name="currentLinkedEntityid" select="entityInternalId"/>
                  <!-- Defining system IDs for IBM Rational Doors (source) and Jira (target) -->
                  <xsl:variable name="externalSourceSystemId" select="'333'"/>
                  <xsl:variable name="externalTargetSystemId" select="'332'"/>
                  <!-- Fetching the target entity information from other-system based on the current RTC entity ID -->
                  <xsl:variable name="entityInTarget" select="utils:getTargetEntityInfoBySourceEntityId($externalSourceSystemId, $currentLinkedEntityid, $externalTargetSystemId,'','')"/>
                  <!-- Only set Global ID if entityInTarget is being found -->
                  <xsl:if test="$entityInTarget">
                    <xsl:variable name="globalId" select="entityInfo:getGlobalId($entityInTarget)"/>
                    <xsl:value-of select="$globalId"/>
                  </xsl:if>
                </xsl:element>
                <xsl:element name="LinkAddedDate">
                  <xsl:value-of select="linkAddedDate"/>
                </xsl:element>
                <xsl:element name="LinkedID">
                  <xsl:value-of select="entityInternalId"/>
                </xsl:element>
                <xsl:if test="order!=''">
                  <xsl:element name="order">
                    <xsl:value-of select="order"/>
                  </xsl:element>
                </xsl:if>
                <xsl:if test="id!=''">
                  <xsl:element name="id">
                    <xsl:value-of select="id"/>
                  </xsl:element>
                </xsl:if>
                <xsl:for-each select="linkProps/Property">
                  <xsl:for-each select="*">
                    <xsl:element name="{name(.)}">
                      <xsl:value-of select="."/>
                    </xsl:element>
                  </xsl:for-each>
                </xsl:for-each>
              </xsl:element>
            </xsl:when>
            <xsl:otherwise>
              <xsl:element name="{concat('_',position())}">
                <xsl:element name="EntityType">
                  <xsl:variable name="sourceEntityType" select="entityType"/>
                  <xsl:value-of select="$entityTypeMapping[text()=$sourceEntityType]/@targetEntityType"/>
                </xsl:element>
                <xsl:element name="GlobalId">
                  <xsl:value-of select="linkGlobalId"/>
                </xsl:element>
                <xsl:element name="LinkAddedDate">
                  <xsl:value-of select="linkAddedDate"/>
                </xsl:element>
                <xsl:element name="LinkedID">
                  <xsl:value-of select="entityInternalId"/>
                </xsl:element>
                <xsl:element name="IsExternalLink">
                  <xsl:value-of select="isExternalLink"/>
                </xsl:element>
                <xsl:element name="ExternalLinkUrl">
                  <xsl:value-of select="externalLinkUrl"/>
                </xsl:element>
                <xsl:element name="EntityLinkComment">
                  <xsl:value-of select="linkComment"/>
                </xsl:element>
                <xsl:if test="order!=''">
                  <xsl:element name="order">
                    <xsl:value-of select="order"/>
                  </xsl:element>
                </xsl:if>
                <xsl:if test="id!=''">
                  <xsl:element name="id">
                    <xsl:value-of select="id"/>
                  </xsl:element>
                </xsl:if>
                <xsl:for-each select="linkProps/Property">
                  <xsl:for-each select="*">
                    <xsl:element name="{name(.)}">
                      <xsl:value-of select="."/>
                    </xsl:element>
                  </xsl:for-each>
                </xsl:for-each>
              </xsl:element>
            </xsl:otherwise>
          </xsl:choose>
        </xsl:for-each>
      </xsl:element>
    </op_list>
  </xsl:for-each>

  <xsl:for-each xmlns:xsl="http://www.w3.org/1999/XSL/Transform" select="$linksToBeAddedAsDefault">
    <op_list>
      <xsl:element name="{.}">
        <xsl:element name="_1">
          <xsl:element name="EntityType">
            <xsl:value-of select="@entityType"/>
          </xsl:element>
          <xsl:element name="LookupQuery">
            <xsl:value-of select="@lookupQuery"/>
          </xsl:element>
        </xsl:element>
      </xsl:element>
    </op_list>
  </xsl:for-each>
</OHEntityReferences>
```

* Refer to the comments starting from `<!-- Changes from here -->` in the XSL for the custom logic implementation.
* A mechanism is provided to handle scenarios where `isExternalLink = 'true'`. In this case:
  * The linked entity ID is extracted.
  * It is used to fetch the corresponding synced entity from the target system (e.g., Jira).
  * The Global ID of the synced entity is retrieved and included in the output.
* When `isExternalLink = 'false'`, the default XSLT logic is applied, and the existing Global ID is used directly without cross-system lookup.

### **ETM as a Target**

* XSLT handles parsing of incoming other system's data.
* Refer to the XML for writing External Links to ETM below.
* The use case is to sync DNG link to ETM \[If a Jira's Test entity is synced to a DOORS NG's System Requirement entity and another Jira's Test entity to an ETM's Test Script, linking the two in Jira will add the DNG item to ETM].

```xml
<OHEntityReferences xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:entityInfo="http://com.opshub.dao.eai.OIMEntityInfo">
 	<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="nonDefaultLinks" as="item()*">
 		<Item targetLinkType="Requirement">parent</Item>
 	</xsl:variable>
 	<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="entityTypeMapping" as="item()*">
 		<Item targetEntityType="testcase">Epic</Item>
 	</xsl:variable>
 	<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="externalLinks" as="item()*">
 		<Item>parent</Item>
 	</xsl:variable>
 	<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="defaultLinkWithSourceLinks" as="item()*"/>
 	<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="defaultLinkWithOH_DEFAULT" as="item()*"/>
 	<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="entityReferencecontext" select="/SourceXML/updatedFields/Property/OHEntityReferences/OHEntityReference"/>
 	<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="linksToBeCarriedFromSourceEvent" as="item()*">
 		<xsl:for-each select="$nonDefaultLinks">
 			<xsl:variable name="currentLinkType" select="."/>
 			<xsl:if test="$entityReferencecontext/linkType[text()=$currentLinkType]">
 				<xsl:if test="$entityReferencecontext[linkType[text()=$currentLinkType]]/links/EAILinkEntityItem">
 					<Item targetLinkType="{@targetLinkType}">
 						<xsl:value-of select="."/>
 					</Item>
 				</xsl:if>
 			</xsl:if>
 		</xsl:for-each>
 	</xsl:variable>
 	<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="linksToBeAddedAsDefault" as="item()*">
 		<xsl:for-each select="$defaultLinkWithOH_DEFAULT">
 			<Item lookupQuery="{@lookupQuery}" entityType="{@entityType}">
 				<xsl:value-of select="."/>
 			</Item>
 		</xsl:for-each>
 		<xsl:for-each select="$defaultLinkWithSourceLinks">
 			<xsl:variable name="currentLinkType" select="."/>
 			<xsl:if test="not($linksToBeCarriedFromSourceEvent[text() = $currentLinkType] = $currentLinkType)">
 				<Item lookupQuery="{@lookupQuery}" entityType="{@entityType}">
 					<xsl:value-of select="./@targetLinkType"/>
 				</Item>
 			</xsl:if>
 		</xsl:for-each>
 	</xsl:variable>
 	<xsl:for-each xmlns:xsl="http://www.w3.org/1999/XSL/Transform" select="$linksToBeCarriedFromSourceEvent">
 		<xsl:variable name="currentLinkType" select="."/>
 		<op_list>
 			<xsl:element name="{@targetLinkType}">
 				<xsl:for-each select="$entityReferencecontext[linkType=$currentLinkType]/links/EAILinkEntityItem">
 					<xsl:element name="{concat('_',position())}">
 						<xsl:element name="EntityType">
 							<xsl:variable name="sourceEntityType" select="entityType"/>
 							<xsl:value-of select="$entityTypeMapping[text()=$sourceEntityType]/@targetEntityType"/>
 						</xsl:element>
 						<xsl:element name="GlobalId">
 							<xsl:value-of select="linkGlobalId"/>
 						</xsl:element>
 						<xsl:element name="sourceEntityType">
 							<xsl:value-of select="entityType"/>
 						</xsl:element>
 						<xsl:element name="LinkAddedDate">
 							<xsl:value-of select="linkAddedDate"/>
 						</xsl:element>
 						<xsl:element name="LinkedID">
 							<xsl:value-of select="entityInternalId"/>
 						</xsl:element>
 						<xsl:element name="IsExternalLink">
 							<xsl:choose>
 								<xsl:when test="$externalLinks[. = $currentLinkType]">
 									<xsl:value-of select="'true'"/>
 								</xsl:when>
 								<xsl:otherwise>
 									<xsl:value-of select="'false'"/>
 								</xsl:otherwise>
 							</xsl:choose>
 						</xsl:element>
 						<xsl:element name="ExternalLinkUrl">
 							<xsl:choose>
 								<!-- Check if the current link type is considered external -->
 								<xsl:when test="$externalLinks[. = $currentLinkType]">
 									<!-- Get the internal ID of the linked entity -->
 									<xsl:variable name="currentLinkedEntityid" select="entityInternalId"/>
 									<!-- Defining system IDs for DNG (source) and other-system (target) -->
 									<xsl:variable name="externalTargetSystemId" select="'50'"/>
 									<xsl:variable name="externalSourceSystemId" select="'374'"/>
 									<!-- Fetching the target entity information from other-system based on the current DNG entity ID -->
 									<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="entityInTarget" select="utils:getTargetEntityInfoBySourceEntityId($externalSourceSystemId, $currentLinkedEntityid, $externalTargetSystemId, '', '')"/>
 									<!-- Get the internal ID of the target entity -->
 									<xsl:variable name="targetEntityId" select="entityInfo:getEntityInternalId($entityInTarget)"/>
 									<!-- Get the base DNG URL from system extensions -->
 									<xsl:variable name="BaseUrl" select="'<<endSystemUrl>>'"/>
 									<xsl:variable xmlns:xsl="http://www.w3.org/1999/XSL/Transform" name="baseURL" select="utils:getSystemExtensionValueFromSystem($externalTargetSystemId, $BaseUrl)"/>
 									<!-- Construct the full resource URL pointing to the DNG work item -->
 									<xsl:variable name="resourceUrl" select="concat($baseURL,'<<unique_Resource_Url>>', $targetEntityId)"/>
 									<!-- Output the final DNG resource URL -->
 									<xsl:value-of select="$resourceUrl"/>
 								</xsl:when>
 								<xsl:otherwise>
 									<xsl:value-of select="ExternalLinkUrl"/>
 								</xsl:otherwise>
 							</xsl:choose>
 						</xsl:element>
 						<xsl:element name="EntityLinkComment">
 							<xsl:value-of select="linkComment"/>
 						</xsl:element>
 						<xsl:if test="order!=''">
 							<xsl:element name="order">
 								<xsl:value-of select="order"/>
 							</xsl:element>
 						</xsl:if>
 						<xsl:if test="id!=''">
 							<xsl:element name="id">
 								<xsl:value-of select="id"/>
 							</xsl:element>
 						</xsl:if>
 						<xsl:for-each select="linkProps/Property">
 							<xsl:for-each select="*">
 								<xsl:element name="{name(.)}">
 									<xsl:value-of select="."/>
 								</xsl:element>
 							</xsl:for-each>
 						</xsl:for-each>
 					</xsl:element>
 				</xsl:for-each>
 			</xsl:element>
 		</op_list>
 	</xsl:for-each>
 	<xsl:for-each xmlns:xsl="http://www.w3.org/1999/XSL/Transform" select="$linksToBeAddedAsDefault">
 		<op_list>
 			<xsl:element name="{.}">
 				<xsl:element name="_1">
 					<xsl:element name="EntityType">
 						<xsl:value-of select="@entityType"/>
 					</xsl:element>
 					<xsl:element name="LookupQuery">
 						<xsl:value-of select="@lookupQuery"/>
 					</xsl:element>
 				</xsl:element>
 			</xsl:element>
 		</op_list>
 	</xsl:for-each>
 </OHEntityReferences>
```

## Appendix

### How to know System ID

* Log in to <code class="expression">space.vars.SITENAME</code> (`<OIM URL>//OIM`).
* Navigate to Configure Systems Page.
* Click on the System that is configured Externally for the Source and Target.
* From the endpoint URL in OIM, locate the value after `system-detail:` in the path.
* For example, in:\
  `.../endpoints/(system-detail:332/endpoints/view)`\
  the **System Detail ID** is `332`.
