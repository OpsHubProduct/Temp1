---
title: database_metadata_input
---

```json
"link": {
  "tableName": "LINKS",
  "linkIdColumn": "LINK_ID",
  "entityIdColumn": "ENTITY_ID",
  "entityTypeColumn": "ENTITY_TYPE",
  "linkedRecordIdColumn": "LINKED_ENTITY_ID",
  "linkedEntityTypeColumn": "LINKED_ENTITY_TYPE",
  "linkTypeColumn": "LINK_TYPE",
  "linkCreatedTimeColumn": "LINK_ADDED_TIME",
  "linkCreatedByColumn": "LINK_ADDED_BY",
  "supportedLinkTypes": {"Parent": "Child", "Related": "Related"}
},
"comment": {
  "tableName": "COMMENTS",
  "commentIdColumn": "COMMENT_ID",
  "entityIdColumn": "RECORD_ID",
  "entityTypeColumn": "TABLE_NAME",
  "commentTitleColumn": "TITLE",
  "commentBodyColumn ": "CONTENT",
  "commentAuthorColumn": "AUTHOR",
  "commentTypeColumn": "COMMENT_TYPE",
  "commentAddedTimeColumn": "COMMENTS_ADDED_TIME"
},
"attachment": {
  "tableName": "ATTACHMENTS",
  "attachmentIdColumn": "ATTACHMENT_ID",
  "entityIdColumn": "RECORD_ID",
  "entityTypeColumn": "TABLE_NAME",
  "fileNameColumn": "FILE_NAME",
  "fileContentLengthColumn":"FILE_LENGTH",
  "fileTypeColumn ": "FILE_TYPE",
  "fileURIColumn ": "FILE_URI",
  "attachmentAddedByColumn ": "ATTACHMENT_ADDED_BY",
  "attachmentAddedTimeColumn": "ATTACHMENT_ADDED_TIME",
  "attachmentFolderPath ": "D:/OpsHub/attachments"
 }

```

* To store the links, comments and attachments information of data records, a separate table will be used in the same database/schema. Provide the table name and field details for this table.

**Links/Relationships**

| **Field Name**           | **Expected Input Value**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `tableName`              | Name of the table storing link information among different data records                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `linkIdColumn`           | Column name storing unique ID of the link record                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `entityIdColumn`         | Column name storing entity Id (primary ID value of the record) having link information                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `entityTypeColumn`       | Column name storing table name of the record mentioned in entityIdColumn                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `linkedRecordIdColumn`   | Column name storing linked entity Id (primary ID value of the linked record)                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `linkedEntityTypeColumn` | Column name storing linked table name of the record mentioned in linkedRecordIdColumn                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `linkTypeColumn`         | Column name storing link type                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `linkCreatedTimeColumn`  | Column name storing link added time                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `linkCreatedByColumn`    | Column name storing username storing the link information                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `supportedLinkTypes`     | <p>Provide metadata for link types along with their corresponding reverse link types in a JSON sub-block. Each link type and its reverse counterpart will be supported for linking.<br>For example, if the JSON contains <code>"Parent": "Child"</code>, then both <code>Parent</code> and <code>Child</code> will be valid link types, with <code>Parent</code> being the reverse of <code>Child</code> and vice versa.<br>If a link type has no reverse, use an empty string (<code>""</code>) as its reverse link type.</p> |

**Comments**

| **Field Name**           | **Expected Input Value**                                                                  |
| ------------------------ | ----------------------------------------------------------------------------------------- |
| `tableName`              | Name of the table storing comment information of data records                             |
| `commentIdColumn`        | Column name storing unique ID of the comment record                                       |
| `entityIdColumn`         | Column name storing entity Id (primary ID value of the record) having comment information |
| `entityTypeColumn`       | Column name storing table name of the record mentioned in entityIdColumn                  |
| `commentBodyColumn`      | Column name storing comment body or content of the comment                                |
| `commentAuthorColumn`    | Column name storing comment author                                                        |
| `commentAddedTimeColumn` | Column name storing comment added time                                                    |
| `commentTypeColumn`      | Column name storing comment type                                                          |
| `commentTitleColumn`     | Column name storing comment title                                                         |

**Attachments**

| **Field Name**              | **Expected Input Value**                                                                          |
| --------------------------- | ------------------------------------------------------------------------------------------------- |
| `tableName`                 | Name of the table storing attachments information of data records                                 |
| `attachmentIdColumn`        | Column name storing unique ID of the attachment record                                            |
| `entityIdColumn`            | Column name storing entity Id (primary ID value of the record) having file attachment information |
| `entityTypeColumn`          | Column name storing table name of the record mentioned in entityIdColumn                          |
| `fileNameColumn`            | Column name storing file name attached to data record                                             |
| `fileContentLengthColumn`   | Column name storing file content length                                                           |
| `fileTypeColumn`            | Column name storing file type                                                                     |
| `fileURIColumn`             | Column name storing local file URI                                                                |
| `attachmentAddedByColumn`   | Column name storing attachment added by user name                                                 |
| `attachmentAddedTimeColumn` | Column name storing attachment added time                                                         |
| `attachmentFolderPath`      | Local folder path (accessible to OIM user) where all attachment files will be stored              |
