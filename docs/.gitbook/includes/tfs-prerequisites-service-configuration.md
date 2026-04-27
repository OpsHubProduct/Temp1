---
title: tfs-prerequisites-service-configuration
---

<code class="expression">space.vars.SITENAME</code> requires this service to communicate with the Azure DevOps. It acts as a translation layer between Azure DevOps and <code class="expression">space.vars.SITENAME</code> and must be configured for synchronization with Azure DevOps.

## Service pre-requisites

* Operating System (Tested On): Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows 7, Windows 8, Windows 8.1, Windows 10
* It is recommended to install Service on a machine having quad-core processor and minimum 4 GB RAM.
* Required disk space for the service depends upon the data size of the source control data. It is recommended to have disk space greater than the total data size of source control.
* It is recommended to install Service on different machine where Team Foundation Server is not installed.
* The <code class="expression">space.vars.SITENAME</code> Service requires the machine to have .NET framework 4.7.2 or higher installed on it.

> **Note**: Refer to the table below to check which entity types require this pre-requisite. A check mark indicates a mandatory pre-requisite, while a cross mark indicates an optional one.

| **Entity Type**                                                     | **Azure DevOps Services** | **Azure DevOps Server (version >= 2020)** | **Azure DevOps Server (version < 2020)** |
| ------------------------------------------------------------------- | ------------------------- | ----------------------------------------- | ---------------------------------------- |
| **Work Items**                                                      | ❌                         | ❌                                         | ✅                                        |
| **Test entities (Test Suite, Test Plan, Test Run and Test Result)** | ❌                         | ❌                                         | ✅                                        |
| **Area and Iteration**                                              | ❌                         | ❌                                         | ✅                                        |
| **Group, Team and User**                                            | ❌                         | ✅                                         | ✅                                        |
| **Git Commit Information**                                          | ❌                         | ❌                                         | ✅                                        |
| **Pipeline**                                                        | ❌                         | ❌                                         | ✅                                        |
| **Build**                                                           | ❌                         | ❌                                         | ❌                                        |
| **Other entities**                                                  | ✅                         | ✅                                         | ✅                                        |

Follow the steps given below for installation:

* Navigate to the path `<OPSHUB_INSTALLATION_PATH>\Other_Resources\Resources`.
* Extract the `OpsHubTFSService.zip` package.
* Service will be installed on port **<9090>** by default. Please check the port available for service which you configure for the service (Default port is <9090>). Refer section [How to change the port of service](../../connectors/azure-devops.md#how-to-change-the-port-of-service) to learn how to change the default port of service.
* Open the command prompt as _Run As Administrator_ and navigate to the extracted folder in which the `registerTFSWCFService.bat` is placed and execute `registerTFSWCFService.bat`.
* Once the command is executed, go to Windows Services, and look for a service with the name **OpsHubTFSService**. Check if the service has started or not. If it has not started, then start the service.
* Test the web service by opening this URL in browser: `http://<hostname>:<port>/TFSService`.\
  E.g. `http://localhost:9090/TFSService`. For Troubleshooting, refer [Service Troubleshooting](../../connectors/service-troubleshooting.md) section.

In case the machine on which <code class="expression">space.vars.SITENAME</code> installed is behind the proxy (network proxy), then perform the steps mentioned in the [Proxy settings](../../manage/administrator/proxy-setting.md) section.

It is also required to configure the proxy settings for <code class="expression">space.vars.SITENAME</code> Service, refer to [Proxy settings](../../connectors/azure-devops.md#proxy-settings-for-the-service) in appendix section for the <code class="expression">space.vars.SITENAME</code> Service to learn the configuration steps.
