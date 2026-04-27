---
title: aras-installtion-steps
---

Follow the steps for installation given below:

1. Locate the path `<OPSHUB_INSTALLATION_PATH>\Other_Resources\Resources`
2. Extract the `OpsHubArasService.zip` package
3. Check the availability of port 9494 as OpsHubArasService will be using port 9494. Refer to section [Check Availability of Port](../../connectors/aras.md#how-to-check-availability-for-port-9494-for-aras-service) to learn how to check if particular port is available. Refer section [How to change the port of service](../../connectors/aras.md#how-to-change-the-port-of-service) to learn how to change the default port of service.
4. Open the command prompt with Administrator Privileges and navigate to the folder extracted in Step -2, where the user can find `registerArasService.bat`
5. Now, execute `"registerArasService.bat"`
6. Once the command is executed, go to Windows Services and look for a service with the name `'OpsHubArasService'`.
   * Please start the service in case the service has not started yet.
7. Test the web service by opening the URL in browser: `http://<hostname>:<9494>/ArasService`, for example: `http://localhost:9494/ArasService`
