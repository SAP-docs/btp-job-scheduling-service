<!-- loio132fd06caa75451caab9aad00fd0bc1b -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Manage Jobs with Service Dashboard

The SAP Job Scheduling service dashboard enables you to manage jobs and tasks for a service instance.



<a name="loio132fd06caa75451caab9aad00fd0bc1b__prereq_wbc_hfm_d4b"/>

## Prerequisites

You've the `SpaceDeveloper` role. It allows you to access the dashboard, and to create, update or delete jobs, schedules and configuration.

> ### Note:  
> With only one of the BTP roles `SpaceAuditor` or `SpaceManager`, you set read-only access to the SAP Job Scheduling service dashboard for a user. All change operations in the dashboard aren’t visible.



## Context

The service dashboard lists the available jobs. Choose a job or a task to create a schedule or to view existing schedules. You can use the dashboard to perform the following tasks:

-   Create a schedule
-   Update a job/task or a schedule
-   View the history for a job/task or schedule
-   View run logs

The SAP Job Scheduling service supports the use of custom identity providers with platform users. The IdP provider can be used to access the service dashboard. For more information, see [Supported Tools and Services When Using Custom Identity Providers for Platform Users\[Feature Set A\]](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/94ef5154e384408796c035a82b043f82.html) .

The screens available on the dashboard and their description are as below:

 *Configurations:*
 :   Edit global configurations required for a specific SAP Job Scheduling service instance to work.

    -   *Asynchronous Execution Timeout \(s\):* This value indicates how long \(in seconds\) the SAP Job Scheduling service awaits response for the asynchronous job from the action endpoint as well as from the CF task. If the application doesn't provide a response in the specified duration, or if the CF task isn't complete in the specified duration, the run status is set to COMPLETED/UNKNOWN. For CF tasks, the task is stopped when the timeout is reached.

        You can enter any number that's below or is equal to 604800 seconds.


  *Jobs/Tasks:*
 :   View the jobs/tasks for a specific service instance. You can create a job/task and deactivate or delete an existing job/task.

    -   *Schedules:* Create and configure schedules for a job/task. To access schedules, choose a job/task listed on the dashboard. For more information, see Schedule Types in the related information section.

        Choose a schedule to view its history and logs. To display the run logs of a schedule, choose *Run Logs*. You can download the run logs.

        For more information, see [Action on Job Run Logs](https://help.sap.com/docs/JOB_SCHEDULER/07b57c2f4b944bcd8470d024723a1631/d09664b7ae9d453e8b8a3a6e09449916.html?version=Cloud#action-on-job-run-logs).

    -   *Events:* View the history for a job/task or a schedule.


 > ### Tip:  
> You've the following options to adjust the table columns to your preferences:
> 
> -   Sort Ascending/Descending
> -   Resize column width
> -   For the job name column only
> 
>     -   :arrow_left:
>     -   :arrow_right:
>     -   <span class="SAP-icons"></span> View Full Name
> 
>     Some jobs have long names that aren't displayed fully by default. You can choose to view the first or last part only, depending on what’s most relevant to you, or to display the full name, without changing the column width.



## Procedure

Use one of the options to access the service dashboard:


<table>
<tr>
<th valign="top">

Access the Dashboard



</th>
<th valign="top">

Actions



</th>
</tr>
<tr>
<td valign="top">

Using SAP BTP cockpit



</td>
<td valign="top">

1.  From the navigation area of the SAP BTP cockpit, choose *Services* \> *Instances and Subscriptions*.
2.  Choose *View Dashboard* from the *Actions* menu for the relevant service instance.

    The service dashboard appears on a new tab.

3.  In the navigation area, choose *Jobs*.
4.  From the *Names* column, choose a job.

    This takes you to the *Overview* page. You can view the details for the selected job and edit it.




</td>
</tr>
<tr>
<td valign="top">

Using Command Line Interface \(CLI\)



</td>
<td valign="top">

1.  Enter the command to fetch service instance details `cf service <service-instance-name>`.
2.  Copy the URL form the *Dashboard* field.
3.  Paste the URL in a web browser of your choice.
4.  Enter the SAP BTP credentials to log on.



</td>
</tr>
</table>

**Related Information**  


[Schedule Types](../20---Concepts/schedule-types-9cf8c14.md#loio9cf8c14da0144c84aac628dc56b00ffd "SAP Job Scheduling service runs one-time and recurring jobs or Cloud Foundry tasks.")

