---
title: windows-specific-configuration
---

During the installation of <code class="expression">space.vars.SITENAME</code>, few temporary files are placed/copied in the TEMP directory \[i.e., the path which is specified in TEMP environment variable]. This directory path should not contain ";" as well as none of the directory/folder names should end with "!" in this path.

* Example: "C:\Users\xyz!\AppData\Local\Temp" or "C:\Users\xy;z\AppData\Local\Temp" as Temp environment variable value/path is not allowed.
* In such case, the installation will fail with error. Please refer [here](../../help-center/troubleshooting/errors/install/ops-005.md) for more details on this error and steps for its resolution. To check how to set TEMP environment variable, please refer below.

## Setup environment variable

* Open "Edit the system environment variables" from Start.
* Click the "Environment Variables" button.
* Click on environment variable required to be edited.
* Click on Edit button and change the path.
