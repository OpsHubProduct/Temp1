# OpsHub Query Format

## Overview

<code class="expression">space.vars.SITENAME</code> has defined a specific query format which can be used in place of native query of end system. The query can be used for doing criteria-based synchronization and target lookup synchronization if the connector supports this format of querying. Kindly visit the connector page to know whether it supports this format of querying in end system for criteria-based polling and target lookup instead of native query format.

The query format is a JSON format. The JSON has pre-defined keys and input formats which needs to be followed for steady synchronization of data.

## Query Format

The JSON query syntax has following keys: **field**, **condition**, **value**, **values**, **criterias**. Any key input other than these will result in wrong syntax error.

The query can be applied only on the conditions that are supported by connector. For knowing the supported conditions for querying, kindly refer to the connector documentation.

Below is the JSON syntax for the criteria query.

The JSON query syntax can accommodate simple queries as well as complex queries using nested JSON criterias. In the above JSON query, the **Leaf Criteria Sections** denotes the simple queries that can be grouped together into complex queries (nested queries). The **Criteria Section 1** groups together the criterias denoted by **Criteria sub section 1**.

A query can be a **simple query** or a **complex query**. A simple query has only a single criteria on one field. A complex query has multiple criterias over same field or different fields grouped together.

## Query Format breakdown

### Key - field

* The **field** key represents the name of the field or attribute in end system for which the criteria needs to be specified.
* The field name can be display name or internal name. Refer to connector document to know whether connector supports query on internal name or display name.
* The **field** key is mandatory when doing simple queries. With respect to the above image, the Leaf criteria section must contain the field name (simple queries).

```json
{
  "field": "<field name>"
}
```

* For example - Considering an example query **Severity=Low** that needs to be formed using JSON query, then in the JSON query, the field key will be equal to **Severity**.

```json
{
  "field": "Severity"
}
```

> **Note** : For valid usages of **field** key with other keys, refer to section [Valid Query Usages](opshub-query-format.md#valid-query-usages).

### Key - condition

* The **condition** key represents the criteria operator which should be met by entities. It defines the operator which needs to be evaluated while searching for value(s) in the field.
* This key only takes the conditions that are supported by the connector.
* The **condition** key is mandatory when doing simple queries or complex queries.

```json
{
  "condition": "<operator>"
}
```

* Example: **Severity=Low**

```json
{
  "condition": "="
}
```

* Example: complex query **Severity=Low and Sync=True**

```json
{
  "condition": "and"
}
```

> **Note** : For valid usages of **condition** key with other keys, refer to section [Valid Query Usages](opshub-query-format.md#valid-query-usages).

### Key - value

* The **value** key represents the static value or name of the lookup value in end system which is matched with the field value on the basis of the criteria given.
* The **value** key is mandatory when single value needs to be checked against a field.

```json
{
  "value": "<value>"
}
```

* Example: **Severity=Low**

```json
{
  "value": "Low"
}
```

> **Note**: For valid usages of **value** key with other keys, refer to section [Valid Query Usages](opshub-query-format.md#valid-query-usages).

### Key - values

* The **values** key represents the multiple static values or display name of multiple lookup values in end system which are to be matched with the field value.
* The **values** key is mandatory when multiple values needs to be checked against a single field.

```json
{
  "values": [<value1>, <value2>...<value n>]
}
```

* Example: **Severity=Low or Medium**

```json
{
  "values": ["Low", "Medium"]
}
```

> **Note** : For valid usages of **values** key with other keys, refer to section [Valid Query Usages](opshub-query-format.md#valid-query-usages).

### Key - criterias

* The **criterias** key takes multiple criterias which needs to be applied in end system.
* This key can only be used along with key **condition**.
* The **criterias** key is mandatory when simple queries need to be combined (nested queries).

```json
{
  "criterias": [<criteria1>, <criteria2>,..<criteria n>]
}
```

* Example: **Severity=Low and Sync=True**

```json
{
  "criterias": [
    {
      "field": "Severity",
      "condition": "=",
      "value": "Low"
    },
    {
      "field": "Sync",
      "condition": "=",
      "value": "True"
    }
  ]
}
```

> **Note** : For valid usages of **criterias** key with other keys, refer to section [Valid Query Usages](opshub-query-format.md#valid-query-usages).

## Valid Query Usages

### Simple Queries

```json
{
  "field": "<field name>",
  "condition": "<operator>",
  "value": "<value>"
}
```

```json
{
  "field": "<field name>",
  "condition": "<operator>",
  "values": ["<value1>", "<value2>"]
}
```

### Complex Queries

```json
{
  "condition": "<operator>",
  "criterias": [<criteria1>, <criteria2>]
}
```

## Sample Queries

### Simple Queries with single value search

```json
{
  "field": "Severity",
  "condition": "=",
  "value": "Major"
}
```

```json
{
  "field": "Title",
  "condition": "contains",
  "value": "Test"
}
```

### Simple Queries with multiple values search

```json
{
  "field": "Priority",
  "condition": "in",
  "values": ["Low", "High"]
}
```

```json
{
  "field": "Severity",
  "condition": "in",
  "values": ["Major", "Blocker"]
}
```

### Complex Queries with multiple criterias

```json
{
  "condition": ";",
  "criterias": [
    {
      "field": "Severity",
      "condition": "is",
      "value": "Major"
    },
    {
      "field": "Title",
      "condition": "contains",
      "value": "Test"
    }
  ]
}
```

```json
{
  "condition": ";",
  "criterias": [
    {
      "condition": ",",
      "criterias": [
        {
          "field": "Severity",
          "condition": "is",
          "value": "Major"
        },
        {
          "field": "Severity",
          "condition": "is",
          "value": "Minor"
        }
      ]
    },
    {
      "field": "Title",
      "condition": "contains",
      "value": "Test"
    }
  ]
}
```

```json
{
  "condition": ";",
  "criterias": [
    {
      "field": "Severity",
      "condition": "is",
      "value": "Major"
    },
    {
      "field": "Title",
      "condition": "contains",
      "value": "Test"
    },
    {
      "field": "SyncField",
      "condition": "=",
      "value": true
    }
  ]
}
```

```json
{
  "condition": ";",
  "criterias": [
    {
      "condition": ",",
      "criterias": [
        {
          "field": "Test Case Count",
          "condition": ">",
          "value": 10
        },
        {
          "field": "Test Case Count",
          "condition": "<",
          "value": 20
        }
      ]
    },
    {
      "field": "Title",
      "condition": "contains",
      "value": "Test"
    }
  ]
}
```
