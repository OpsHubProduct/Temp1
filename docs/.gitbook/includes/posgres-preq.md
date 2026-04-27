---
title: posgres-preq
---

* **Supported versions:** From 15 or above
* The user must have **CREATEDB** permission for creating database.

In the advanced installation, if <code class="expression">space.vars.SITENAME</code> is installed with the option of the [manual creation of the database](../../getting-started/installation.md#manual-creation-of-the-databases), then:

* The user must have permission for **CREATE ON SCHEMA** for both the schemas (`opshub` and `reportsdb`) for creating tables, index, references, and views.
* The manually created database and schema should only contain **lowercase alphanumeric characters**, with `$`, `_` and **no spaces**.
