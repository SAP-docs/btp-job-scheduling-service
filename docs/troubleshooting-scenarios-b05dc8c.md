<!-- loiob05dc8c092fb4ccc9a2ad7efa8ff47b5 -->

# Troubleshooting Scenarios

Find solutions to the most common issues related to SAP Job Scheduling service.



## SAP Job Scheduling Service Is Missing

SAP BTP services are available in many regions around the globe. You can choose between data centers that are hosted by SAP and those that are run by our partner Infrastructure-as-a-Service \(IaaS\) providers: Microsoft Azure, Amazon Web Services, and Google Cloud Platform.

To find out which services are available on a specific data center/region, see [SAP BTP regions and service portfolio](https://help.sap.com/doc/aa1ccd10da6c4337aa737df2ead1855b/Cloud/en-US/3b642f68227b4b1398d2ce1a5351389a.html).

Check if the SAP Job Scheduling service is available in your region.



### The Service Is Running But Deeper Analysis Is Required

-   Check if sufficient quota is assigned.

    It is possible that you don't have quota assigned to view the service.

    For more information, see [Managing Entitlements and Quotas Using the Cockpit](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/c8248745dde24afb91479361de336111.html?q=Managing%20Entitlements%20and%20Quotas%20Using%20the%20Cockpit).

-   Check the required authorizations to view the service.

    It is possible that you don't have the required authorization to view the service.

    Prerequisite: You have the **Space Developer** role for the space.

    For more information, see [Initial Setup](https://help.sap.com/viewer/07b57c2f4b944bcd8470d024723a1631/Cloud/en-US/0adb6552e0914958a7a68f0ddbedfd32.html).




### The Service Is Not Available on a Specific Data Center

According to the [service portfolio](https://help.sap.com/doc/aa1ccd10da6c4337aa737df2ead1855b/Cloud/en-US/3b642f68227b4b1398d2ce1a5351389a.html), it is possible that the SAP Job Scheduling service is not currently available on your data center.

Use an existing subaccount or [create a new subaccount](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/05280a123d3044ae97457a25b3013918.html) in a location where the service is available, and then enable it.



<a name="loiob05dc8c092fb4ccc9a2ad7efa8ff47b5__section_umz_4jc_rcc"/>

## Getting an Error While Invoking REST APIs

-   HTTP Status Code 401

    This status code is returned when a request does not have proper authentication.

    Check if the credentials passed while calling the API are correct. For more information, see [Authentication](40---Using-JOB-SCHDULR-TITLE/authentication-5dca60b.md).




<a name="loiob05dc8c092fb4ccc9a2ad7efa8ff47b5__section_mmz_4jc_rcc"/>

## Processing Schedules

When SAP Job Scheduling service is calling the action endpoint of the application, you might be facing one of the following problems:



### The Granted Scopes Are Not Sent with the Token That the Job Scheduling Service Sends to the Action Endpoint

Possible solution: Check if you have granted the scopes correctly.

SAP Job Scheduling service uses User Account and Authentication \(UAA\) to secure action endpoints based on OAuth 2.0 authentication.

In the `xs-security.json`, the application which exposes an action endpoint that is called from the SAP Job Scheduling service must grant a scope to the SAP Job Scheduling service instance, e.g. "Jobscheduler". Then, the SAP Job Scheduling service sends a token with this scope to the action endpoint.

You have granted scopes to SAP Job Scheduling service using the `xs-security.json` file of your application. However, the access token does not have the required scopes.

Get a token manually via the binding credentials for the Job Scheduling service instance and check if it already contains the scope. If this check is successful, remember that the token is cached for up to 12 hours by the Job Scheduling service. Therefore, even if you see the newly created scope, requests from the the Job Scheduling service to the application may still contain the old scope.

For more information, see [Secure Access](https://help.sap.com/viewer/07b57c2f4b944bcd8470d024723a1631/Cloud/en-US/745ca502face47af9adb546a916ce1e8.html) and [Tutorial: Using Job Scheduler in SAP Cloud Platform \[3\]: enable OAuth Authorization.](https://community.sap.com/t5/technology-blogs-by-sap/using-job-scheduler-in-sap-cloud-platform-3-enable-oauth-authorization/ba-p/13430221)



### Getting the HTTP Status Code 401

Get an access token manually via the binding credentials for the Job Scheduling service instance. Use the access token to call the application endpoint that is specified as action endpoint of the job action.

-   If this is successful, calling the application from the Job Scheduling service should also work.
-   If you receive a 401 message, please check how you can verify the access token in the application using the cloud security services integration library. See [SAP BTP Security Services Node.js Integration Library](https://www.npmjs.com/package/%40sap/xssec) or [cloud-security-services-integration-library](https://github.com/SAP/cloud-security-xsuaa-integration):
    1.  Use the Job Scheduling service binding credentials.

    2.  Use your own SAP Authorization and Trust Management service \(technical name:`xsuaa`\) instance:

        1.  Use the binding credentials from the `xsuaa` service instance for verification.

        2.  Verify that the scope was granted successfully. If this is the case, the scope should be included in the access token.




For more information, see [Secure Access](https://help.sap.com/viewer/07b57c2f4b944bcd8470d024723a1631/Cloud/en-US/745ca502face47af9adb546a916ce1e8.html) and [Monitoring and Troubleshooting](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/1b3e89e915b349c1aa3896ac8c6becd6.html).



<a name="loiob05dc8c092fb4ccc9a2ad7efa8ff47b5__section_dmz_4jc_rcc"/>

## Accessing the Service Dashboard

Prerequisites: You have the **Space Developer** role for the subaccount that allows you to access the Job Scheduling service dashboard.

For more information, see [Manage Jobs, Tasks, and Schedules with Service Dashboard](40---Using-JOB-SCHDULR-TITLE/manage-jobs-tasks-and-schedules-with-service-dashboard-132fd06.md).



<a name="loiob05dc8c092fb4ccc9a2ad7efa8ff47b5__section_zlz_4jc_rcc"/>

## Cloud Foundry Tasks

For more information, see [https://docs.cloudfoundry.org/devguide/using-tasks.html](https://docs.cloudfoundry.org/devguide/using-tasks.html).



### Unable to Create a Cloud Foundry Task

When the creation of a Cloud Foundry \(CF\) task is unsuccessful, check the memory of the task. The memory is allocated when the CF task is executed. At this point, memory issues can occur. The used memory, including both application memory and CF task memory, must be below the organization instance memory quota.

You can proceed as follows:

You can retrieve the organization instance memory quota via the CF CLI commands:

1. Run:

```
cf org <org>
```

2. Find your quota name from the <quota\> property.

3. View your quota:

```
cf quota <quota id>
```

Command output example:

> ### Output Code:  
> ```
> cf quota <quota id>
> Getting org quota <quota id>
> 
> total memory:      19G
> instance memory:     16G
> routes:         190
> service instances:    1900
> paid service plans:   allowed
> app instances:      unlimited
> route ports:       unlimited
> log volume per second:  unlimited
> ```

To get the currently available memory, subtract instance memory from total memory. According to the provided example, there are 3GB of available memory.

 **Next Steps**

After you have checked your quota, it should become clear if there is a memory issue. In case of a memory issue, you can configure the memory for a CF task scheduled by the SAP Job Scheduling service from the *Create Schedule* screen in the Job Scheduling service dashboard by setting the value of the `memory_in_mb` property in the **Options \(JSON\)** text field. For example:

```
{"memory_in_mb": 64}
```

 

### Retrieving Application Logs

The Cloud Foundry task logs are part of the application logs. If you have the Space Developer role, you can view the most recent logs using the command:

```
cf logs <application_name> --recent
```

For more information, see [https://docs.cloudfoundry.org/devguide/using-tasks.html](https://docs.cloudfoundry.org/devguide/using-tasks.html).

