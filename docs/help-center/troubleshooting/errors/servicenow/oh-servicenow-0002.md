# OH-ServiceNow-0002

## Description

OH-ServiceNow-0002: Error occurred while updating an entity in ServiceNow. Because no field values changed.

## Cause

This generally occurs when 'Copy empty fields' function is not enabled in the 'Transform map' setting of an entity.

## Solution

* Please navigate to 'Transform map' setting from ServiceNow navigator and select the 'Transform map' setting of the entity that you are synchronizing.
* Enable 'Copy empty fields' check as shown below.

<div align="center"><img src="../../../../../.gitbook/assets/SNow_Image_94a.png" alt="" width="700"></div>

As 'Import set table' and 'Transform map' configuration are a part of [pre-requisites](../../../../connectors/servicenow.md#prerequisites) for ServiceNow connector, we would advise you to relook into the pre-requisites and fulfill all of them to avoid such issues in the future.
