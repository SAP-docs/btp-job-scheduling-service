<!-- loio315a4072bf864e808c326a4ae7f43259 -->

# Create an HTTP Job

Learn how to create an HTTP job via the dashboard of SAP Job Scheduling service.



## Context

An HTTP job is a collection of schedules with an action endpoint called URL. This means that your HTTP job invokes this URL, for example, every night.

Synchronous requests are used when the service calls the action endpoint of the application and the application logic executes in a short time span. For job runs with a large time span, you can execute jobs in asynchronous \(or batch\) mode.

Your service plan determines the number of schedules you can have within an HTTP job. For more information, see [SAP Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/job-scheduling-service?region=all&tab=service_plan).

You can create HTTP jobs either using the REST API or the dashboard of the SAP Job Scheduling service.

-   For instructions on how to create an HTTP job with the API, see [https://api.sap.com/api/sap-btpjss-admin-v1/path/createJob](https://api.sap.com/api/sap-btpjss-admin-v1/path/createJob).

-   To create an HTTP job in the dashboard, do the following:




## Procedure

1.  Open the dashboard. In the left navigation menu, choose *HTTP Jobs*.

2.  Choose *Create Job*.

3.  Complete the required fields. The remaining fields are optional.


    <table>
    <tr>
    <th valign="top">

    Field
    
    </th>
    <th valign="top">

    Required
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    *Name* 
    
    </td>
    <td valign="top">
    
    Yes
    
    </td>
    <td valign="top">
    
    Name of the HTTP job. Must not contain special characters or only numbers.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Description* 
    
    </td>
    <td valign="top">
    
    No
    
    </td>
    <td valign="top">
    
    Provides more details about the job.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Target Application* 
    
    </td>
    <td valign="top">
    
    Yes
    
    </td>
    <td valign="top">
    
    Name of the application called by the HTTP job. This application must be part of your Cloud Foundry space or Kyma namespace.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *URL* 
    
    </td>
    <td valign="top">
    
    Yes
    
    </td>
    <td valign="top">
    
    The HTTP or REST endpoint that the job calls when it runs. Must be an endpoint exposed by an application bound to the same SAP Job Scheduling service instance in the same Cloud Foundry space or Kyma namespace.

    Every request carries an `Authorization` header \(JWT token\) which your application must validate against the service binding.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *HTTP Method* 
    
    </td>
    <td valign="top">
    
    Yes
    
    </td>
    <td valign="top">
    
    The HTTP method used when calling the job's endpoint. Supported values are *GET*, *POST*, *PUT*, and *DELETE*.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Start Time \(UTC\)* 
    
    </td>
    <td valign="top">
    
    No
    
    </td>
    <td valign="top">
    
    Start time for the job in UTC.

    Supported format: YYYY-MM-DD HH:mm:ss

    -   YYYY: 4-digit year

    -   MM: month \(01-12\)

    -   DD: day \(01-31\)

    -   HH: hour \(00-23\)

    -   mm: minutes \(00-59\)

    -   ss: seconds \(00-59\)



    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *End Time \(UTC\)* 
    
    </td>
    <td valign="top">
    
    No
    
    </td>
    <td valign="top">
    
    End time for the job in UTC.

    Supported format: YYYY-MM-DD HH:mm:ss

    -   YYYY: 4-digit year

    -   MM: month \(01-12\)

    -   DD: day \(01-31\)

    -   HH: hour \(00-23\)

    -   mm: minutes \(00-59\)

    -   ss: seconds \(00-59\)



    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Send ANS Error Events* 
    
    </td>
    <td valign="top">
    
    No
    
    </td>
    <td valign="top">
    
    Switching on this toggle button enables the following feature:

    If the job execution fails, you send an error event using SAP Alert Notification service.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Send ANS Success Events* 
    
    </td>
    <td valign="top">
    
    No
    
    </td>
    <td valign="top">
    
    Switching on this toggle button enables the following feature:

    If the job execution is completed, you send a success event using SAP Alert Notification service.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Enable SAP Cloud ALM* 
    
    </td>
    <td valign="top">
    
    No
    
    </td>
    <td valign="top">
    
    Switching on this toggle button enables the following feature:

    Allows you to track the status of your job processes directly from the interface of SAP Cloud ALM.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Activate Job* 
    
    </td>
    <td valign="top">
    
    No
    
    </td>
    <td valign="top">
    
    Creates the job in *Active* status. A job must also have a schedule before it can run.

    Selected by default.
    
    </td>
    </tr>
    </table>
    
4.  Choose *Create*.


**Related Information**  


[Create a CF Task Job](create-a-cf-task-job-9c03ae5.md "Learn how to create a Cloud Foundry (CF) task job via the dashboard of SAP Job Scheduling service.")

[Manage Jobs, Tasks, and Schedules with Service Dashboard](manage-jobs-tasks-and-schedules-with-service-dashboard-132fd06.md "The SAP Job Scheduling service dashboard enables you to manage jobs and tasks for a service instance.")

