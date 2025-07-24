<!-- loio972ef35ae47a40b7817415afd19ec934 -->

# Integration with SAP Alert Notification Service for SAP BTP

You can integrate SAP Job Scheduling service with SAP Alert Notification service for SAP BTP to help you maintain high levels of operational reliability, efficiency, and control.



<a name="loio972ef35ae47a40b7817415afd19ec934__section_h5t_jng_xfc"/>

## Overview

When creating a job or task in the dashboard or the REST API of the SAP Job Scheduling service, you can use the integration with SAP Alert Notification service so that the job or task sends an event in case of *Error* or *Success* upon completion.



<a name="loio972ef35ae47a40b7817415afd19ec934__section_agd_1fq_vfc"/>

## Benefits

Integrating SAP Job Scheduling service with SAP Alert Notification service for SAP BTP can offer several benefits, enhancing operational efficiency and responsiveness. Here are two main benefits:

-   Proactive monitoring and response

    By integrating these services, you can set up alerts for various critical events in the job scheduling process. These events include job success, errors when making requests, application failures, timeouts, and others. This proactive monitoring allows for immediate notification to relevant stakeholders, enabling quick response and resolution of issues before they impact business operations. This reduces downtime and ensures that scheduled jobs and tasks are completed on time.

-   Improved operational efficiency

    The integration facilitates automated workflows where alerts can trigger predefined actions or workflows with the help of the SAP Automation Pilot. For example, if a scheduled job fails, an alert can automatically initiate a recovery process or notify the support team to take corrective action. This automation reduces manual intervention, streamlines operations, and enhances overall efficiency in managing scheduled tasks.




<a name="loio972ef35ae47a40b7817415afd19ec934__section_qzy_4mg_xfc"/>

## Prerequisites

You've enabled SAP Alert Notification service. For more information, see [Initial Setup](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/initial-setup).

> ### Remember:  
> For this setup, make sure you've entered one of the available values of the `eventType` property:
> 
> -   ***JobSchedulerJobExecution***
> -   ***JobSchedulerTaskExecution***
> 
> For more information, see [SAP Job Scheduling Service Events](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/jobscheduler-events).



<a name="loio972ef35ae47a40b7817415afd19ec934__section_qh2_tmg_xfc"/>

## Setup

To enable the SAP Job Scheduling service to trigger an event for the SAP Alert Notification service, do the following:

1.  Navigate to your subaccount in the cockpit.

2.  Go to *Services* \> *Instances and Subscriptions*.

3.  If there is no SAP Alert Notification service instance, create a new one.

4.  Select the SAP Alert Notification service instance and open its dashboard.

5.  Use the SAP BTP cockpit to create, edit, and delete actions, conditions, and subscriptions to an event for which you want to get notified. For more information, see [Configuration Management Using the SAP BTP Cockpit](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/configuration-management-using-sap-btp-cockpit).




<a name="loio972ef35ae47a40b7817415afd19ec934__section_sb5_dng_xfc"/>

## Testing the Integration

1.  Schedule a job execution:

    1.  Open the SAP Job Scheduling service dashboard.

    2.  Go to *Jobs*.

    3.  To test the subscription, schedule the execution of a job. Choose *Create Job*.

    4.  Fill in all the relevant fields with their corresponding values.

    5.  Depending on the use case, make sure you've switched on the *Error* or *Success* toggles of *SAP Alert Notification Service Events*.

    6.  Choose *Save*.


2.  Check if:

    -   The job is executed as expected according to the job execution logs.

    -   You've received an e-mail about the outcome of the job execution.



**Related Information**  


[SAP Job Scheduling Service Job Execution](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/jobscheduler-job-execution)

[SAP Job Scheduling Service Task Execution](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/jobscheduler-task-execution)

