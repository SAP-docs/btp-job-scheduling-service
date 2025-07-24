<!-- loiof82790e12a9d44c1b679212577898adc -->

<link rel="stylesheet" type="text/css" href="css/sap-icons.css"/>

# Integration with SAP Cloud ALM

You can integrate SAP Job Scheduling service with SAP Cloud ALM.



<a name="loiof82790e12a9d44c1b679212577898adc__section_jvz_qk2_3fc"/>

## Overview

When creating a job, you can enable monitoring for specific jobs managed by SAP Job Scheduling service. Once enabled, all events related to a job and its schedules are visible within SAP Cloud ALM, providing visibility into job activities and status. This integration allows you to track the status of your job processes directly from the interface of SAP Cloud ALM. For more information about SAP Cloud ALM, see [SAP Cloud ALM - Application Help](https://help.sap.com/docs/cloud-alm/applicationhelp/about).



<a name="loiof82790e12a9d44c1b679212577898adc__section_w5q_rzd_3fc"/>

## Prerequisites

For more information, see [Job & Automation Monitoring Setup & Configuration](https://support.sap.com/en/alm/sap-cloud-alm/operations/expert-portal/job-monitoring/job-automation-monitoring-details.html).



<a name="loiof82790e12a9d44c1b679212577898adc__section_r4c_dl2_3fc"/>

## How to Enable Job Monitoring with SAP Cloud ALM

There are currently two ways to enable job monitoring with SAP Cloud ALM:

-   Using the Job Scheduling service dashboard

    1.  Open the Job Scheduling service dashboard.

    2.  In the navigation area, choose either *Jobs* or *Tasks*.

    3.  There are three ways to enable SAP Cloud ALM in the dashboard:

        -   In the *Actions* column, choose :desktop_computer:. Use the toggle button to enable SAP Cloud ALM, and choose *Save*.

        -   Choose *Create Job* or *Create Task*, respectively. Use the toggle button to enable SAP Cloud ALM.

        -   Choose a job or a task from the list. On the *Overview* page of the job or task, choose *Edit Job* or *Edit Task*, respectively. Use the toggle button to enable SAP Cloud ALM, and choose *Save*.



-   Using the Job Scheduling service REST API

    When creating or editing a job, add the following property to the body of the request:

    ```
    "calmConfig": {  
          "enabled": true 
    }
    ```

    > ### Remember:  
    > You cannot create CF tasks using the REST API because they are bound to a specific application. For more information, see [Can I create a CF task using the REST API?](https://help.sap.com/docs/job-scheduling/sap-job-scheduling-service/frequently-asked-questions?version=Cloud#rest-api).

    For more information, see [Create Job](40---Using-JOB-SCHDULR-TITLE/create-job-2c1ecb6.md).


After you choose one of these two enabling options and complete its steps, you can start monitoring jobs, tasks, and their schedules in the SAP Cloud ALM dashboard.



<a name="loiof82790e12a9d44c1b679212577898adc__section_zsy_jdf_3fc"/>

## How Both Dashboards Display Job Execution Statuses

-   Job Scheduling service dashboard:

    Both *Status* and *State* are displayed in a single column.

-   SAP Cloud ALM dashboard:

    -   *Status* is shown as *Execution Status*.

    -   *State* is shown as *Application Status*.



**Related Information**  


[Supported Solutions](https://help.sap.com/docs/cloud-alm/setup-administration/supported-solutions)

[Job & Automation Monitoring](https://support.sap.com/en/alm/sap-cloud-alm/operations/expert-portal/job-monitoring.html)

[Integration Scenarios](integration-scenarios-faeec3a.md "You can integrate SAP Job Scheduling service with other solutions and services for improved flexibility, scalability, and efficiency.")

