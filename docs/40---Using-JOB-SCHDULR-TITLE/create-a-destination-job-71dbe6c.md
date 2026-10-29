<!-- loio71dbe6c17ba14c4eae58055861f7134e -->

# Create a Destination Job

Learn how to create a destination job via the dashboard of SAP Job Scheduling service.



## Context

A destination job is a type of job that allows you to call external applications. This means that these applications are not part of your Cloud Foundry space or Kyma namespace.

You can only use destinations created via the SAP Destination service. There are several methods to choose from. For more information, see [Managing Destinations](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/managing-destinations).



## Procedure

1.  Open the dashboard. In the left navigation menu, choose *Destination Jobs*.

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
    
    Name of the destination job. Must not contain special characters or only numbers.
    
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
    
    *Destination* 
    
    </td>
    <td valign="top">
    
    Yes
    
    </td>
    <td valign="top">
    
    Name of the destination created in the same Cloud Foundry space or Kyma namespace.

    Select a destination from the drop-down menu or create a new destination in the same Cloud Foundry space or Kyma namespace.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Resource Path* 
    
    </td>
    <td valign="top">
    
    No
    
    </td>
    <td valign="top">
    
    The path appended to the destination URL. Must begin with [/\] and can't end with [/\].

    Example: /api/v1/jobs/run
    
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


