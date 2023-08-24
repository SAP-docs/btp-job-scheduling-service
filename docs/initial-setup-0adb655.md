<!-- loio0adb6552e0914958a7a68f0ddbedfd32 -->

# Initial Setup

You can get started with the SAP Job Scheduling service by following the steps.



<a name="loio0adb6552e0914958a7a68f0ddbedfd32__section_wkn_wmn_sjb"/>

## Prerequisites

-   You've set up your global account and subaccount on SAP BTP.

    For an overview of the required steps, see [Getting Started in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/b328cc89ea14484d9655b8cfb8efb508.html "Get onboarded in the Cloud Foundry environment of SAP BTP. Follow the workflows for trial or customer accounts or subscribe to business applications.") :arrow_upper_right: and [Get a Global Account](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/d61c2819034b48e68145c45c36acba6e.html).

-   You’re a global account administrator.

-   You've purchased quota for the SAP Job Scheduling service and for the SAP Authorization and Trust Management service.

-   Cloud Foundry: You’ve created a space within a subaccount in which the SAP BTP, Cloud Foundry environment is enabled.

    For more information, see [Managing Orgs and Spaces Using the Cockpit](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/c4c25cc63ac845779f76202360f98694.html) and [Account Administration in the Cloud Foundry Command Line Interface](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/927377f33f9b42be9f1b610ef5c33355.html).

-   Kyma: You have enabled the Kyma environment and created a Kyma cluster.

-   Cloud Foundry: Within that space, your user is assigned to the `Space Developer` role for the subaccount. You need this role to execute the configuration steps.

    For more information, see [Managing Authorization in Global Accounts and Subaccounts \[Feature Set B\]](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/0039cf082d3d43eba9200fe15647922a.html) and [Assign Role Collections](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/9e1bf57130ef466e8017eab298b40e5e.html).

-   To start the dashboard, you need the following roles:

    -   Cloud Foundry: `Space Developer`

    -   Kyma: One of the following roles:

        -   `SAP_Job_Scheduling_Service_Admin`

        -   `SAP_Job_Scheduling_Service_Viewer`



-   You've deployed an application on SAP BTP.

-   You've exposed an action endpoint in your application that can be called from the SAP Job Scheduling service.

-   The application and the SAP Job Scheduling service are in the same space.




<a name="loio0adb6552e0914958a7a68f0ddbedfd32__section_q4q_wmn_sjb"/>

## Enabling the Service

To enable the SAP Job Scheduling service and the SAP Authorization and Trust Management service, distribute entitlements and quotas across subaccounts within your global account.

Distribute the quota for the service plan *standard* of the SAP Job Scheduling service to your subaccount.

For more information, see [Managing Entitlements and Quotas Using the Cockpit](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/c8248745dde24afb91479361de336111.html "When you purchase an enterprise account, you are entitled to use a specific set of resources, such as the amount of memory that can be allocated to your applications.") :arrow_upper_right: and [Configure Entitlements and Quotas for Subaccounts](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/5ba357b4fa1e4de4b9fcc4ae771609da.html "Assign entitlements to subaccounts by adding service plans and distribute the quotas available in your global account to your subaccounts using the SAP BTP cockpit.") :arrow_upper_right:.

> ### Remember:  
> You must also enable the SAP Authorization and Trust Management service.



<a name="loio0adb6552e0914958a7a68f0ddbedfd32__section_bys_bnn_sjb"/>

## Setting Up Roles and Authorization

-   To create and bind Cloud Foundry service instances to applications, you must be assigned the **Space Manager** or the **Space Developer** role in the space.

    For more information, see [About Roles in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/09076385086b4da3bd1808d5ef572862.html "Roles determine which features users can view and access, and which actions they can initiate.") :arrow_upper_right:.

-   Kyma: To access the service dashboard, you must be assigned the `SAP_Job_Scheduling_Service_Admin` or the `SAP_Job_Scheduling_Service_Viewer` role.

    For more information, see [Roles and Role Collections](https://help.sap.com/viewer/ae8e8427ecdf407790d96dad93b5f723/Cloud/en-US/14a877c6e2f14832999df500ffa6e05e.html "Usually a role collection consists of one or multiple roles. You can use the SAP BTP cockpit to add or remove roles.") :arrow_upper_right:.




<a name="loio0adb6552e0914958a7a68f0ddbedfd32__section_fj2_g45_sjb"/>

## Getting Started

Once you've completed the initial setup, see:

-   Cloud Foundry: [Getting Started with Cloud Foundry](30---Getting-Started/getting-started-with-cloud-foundry-02e4e8b.md) and our [tutorial](https://blogs.sap.com/2019/11/25/using-job-scheduler-in-sap-cloud-platform-0-intro-and-prep/) for beginners

-   Kyma: [Getting Started with Kyma](getting-started-with-kyma-8d30095.md)


.

**Related Information**  


[Getting Started with Cloud Foundry](30---Getting-Started/getting-started-with-cloud-foundry-02e4e8b.md "Once you've completed the initial setup for SAP Job Scheduling service, to use the service you create a Cloud Foundry service instance and bind it to your application.")

[Getting Started with Kyma](getting-started-with-kyma-8d30095.md "Create a service instance in Kyma.")

[Using SAP Job Scheduling Service](40---Using-JOB-SCHDULR-TITLE/using-sap-job-scheduling-service-9d48597.md "Define and manage one-time and recurring jobs using flexible schedules.")

