# How to put default value for any mandatory field of destination system?

## Description

* In destination system, there is a mandatory field for which suitable field does not exist on source side. If this mandatory field is not mapped, then it will result into failure.
* Fields are being mapped, but there are chances that source side field value may come empty and the target side field is mandatory, in such cases sync will fail.

## Solution

There are multiple use cases. Based on the use case applicable to you, choose the correct solution.

### Mapping 'None' Field for destination mandatory fields

In destination system, there is a mandatory field for which no suitable source side field is available. If the mandatory field is not mapped, then it will result into failure.

Using 'None' field, default value can be set for mandatory field of destination system. In above situations, select 'None' field from the source side and appropriate destination field for which you want to set the default value. You can also click ![defaultemapping.png](../../../../.gitbook/assets/defaultemapping.png) to change the default value for this field mapping later.

### Setting default value by using 'Default mapping configuration'

Fields are being mapped, but there are chances that source side field value may come empty and the target side field is mandatory, in such cases sync will fail.

To handle such case, in the field mapping, click on ![defaultemapping.png](../../../../.gitbook/assets/defaultemapping.png) icon to set default value. For more information, please refer [Mapping Configuration - Default Mapping](https://github.com/OpsHubProduct/OIM-Documentation/blob/main/docs/mapping-configuration.md#default-mapping).
