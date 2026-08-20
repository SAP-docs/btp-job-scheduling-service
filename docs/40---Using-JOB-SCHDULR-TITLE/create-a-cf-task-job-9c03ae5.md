<!-- loio9c03ae51c97944509c59650f814ea1ca -->

# Create a CF Task Job

Learn how to create a Cloud Foundry \(CF\) task job via the dashboard of SAP Job Scheduling service.



## Context

A job that runs an app or script as a Cloud Foundry \(CF\) task. The code runs independently in its own short-lived container as part of a deployed application, making it suited for long-running or resource-intensive processes. CF task jobs always run asynchronously.



## Procedure

1.  Open the dashboard. In the left navigation menu, choose *CF Task Jobs*.

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
    
    Name of the CF task job. Must not contain special characters or only numbers.
    
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
    
    *Application* 
    
    </td>
    <td valign="top">
    
    Yes
    
    </td>
    <td valign="top">
    
    Name of the application deployed in the SAP BTP, Cloud Foundry environment
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Command* 
    
    </td>
    <td valign="top">
    
    Yes
    
    </td>
    <td valign="top">
    
    The command to execute when the job runs within the application container.
    
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


[Create an HTTP Job](create-an-http-job-315a407.md "Learn how to create an HTTP job via the dashboard of SAP Job Scheduling service.")

[Manage Jobs, Tasks, and Schedules with Service Dashboard](manage-jobs-tasks-and-schedules-with-service-dashboard-132fd06.md "The SAP Job Scheduling service dashboard enables you to manage jobs and tasks for a service instance.")

