<!-- loio0adb6552e0914958a7a68f0ddbedfd32 -->

# Initial Setup

You can get started with the SAP Job Scheduling service by following the steps.



<a name="loio0adb6552e0914958a7a68f0ddbedfd32__section_wkn_wmn_sjb"/>

## Prerequisites

-   You've set up your global account and at least one subaccount on SAP BTP.

    For an overview of the required steps, see [Getting Started in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/b328cc89ea14484d9655b8cfb8efb508.html "Get onboarded in the Cloud Foundry environment of SAP BTP. Follow the workflows for trial or customer accounts or subscribe to business applications.") :arrow_upper_right: and [Getting a Global Account](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/d61c2819034b48e68145c45c36acba6e.html#loiod61c2819034b48e68145c45c36acba6e "SAP BTP offers two types of global accounts: Trial accounts (completely free of charge) and enterprise accounts. Within an enterprise account, you can use both free and paid plans.") :arrow_upper_right:.

-   You’re a global account administrator.

-   You've purchased quota for the SAP Job Scheduling service and for the SAP Authorization and Trust Management service and distributed it to your subaccount.

    For the SAP Job Scheduling service, distribute the quota for the service plan *standard*.

    For more information, see [Configure Entitlements and Quotas for Subaccounts](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/5ba357b4fa1e4de4b9fcc4ae771609da.html "Assign entitlements to subaccounts by adding service plans and distribute the quotas available in your global account to your subaccounts using the SAP BTP cockpit.") :arrow_upper_right: and [SAP Authorization and Trust Management Service in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/6373bb7a96114d619bfdfdc6f505d1b9.html "The global account and subaccounts get their users from identity providers. Administrators make sure that users can only access their dedicated subaccount by making sure that there is a dedicated trust relationship only between the identity providers and the respective subaccounts. Developers configure and deploy application-based security artifacts containing authorizations, and administrators assign these authorizations using the SAP BTP cockpit.") :arrow_upper_right:.

-   Cloud Foundry: You’ve created a space within a subaccount in which the SAP BTP, Cloud Foundry environment is enabled.

    For more information, see [Managing Orgs and Spaces Using the Cockpit](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/c4c25cc63ac845779f76202360f98694.html) and [Account Administration in the Cloud Foundry Command Line Interface](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/927377f33f9b42be9f1b610ef5c33355.html).

-   Kyma: You've enabled the Kyma environment and created a Kyma cluster.

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

To use the SAP Job Scheduling service, you must create a service instance using either the SAP BTP cockpit, Kyma dashboard, or the corresponding command line interface \(CLI\). You can then bind the service instance to your application.

A service instance is a single instantiation of a service running on SAP BTP. For more information, see [About Services](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/d1d0fc8e78474494a59caad02259ec7e.html).

To enable the application to consume the created SAP Job Scheduling service instance, the application must be bound to an instance of the SAP Authorization and Trust Management service.

> ### Remember:  
> You must also enable the SAP Authorization and Trust Management service.

The following section provides an overview of the main steps you must follow:

> ### Remember:  
> You must perform the following steps in the given order for the SAP Job Scheduling service to work.

1.  Create an instance of the SAP Job Scheduling service.

2.  Proceed as needed:

    -   Make sure you have an xsuaa service instance. For this, you create an xsuaa service instance or you update an existing one.

        For more information, see [SAP Authorization and Trust Management Service in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/6373bb7a96114d619bfdfdc6f505d1b9.html "The global account and subaccounts get their users from identity providers. Administrators make sure that users can only access their dedicated subaccount by making sure that there is a dedicated trust relationship only between the identity providers and the respective subaccounts. Developers configure and deploy application-based security artifacts containing authorizations, and administrators assign these authorizations using the SAP BTP cockpit.") :arrow_upper_right:.

        > ### Note:  
        > The instance must be configured using the corresponding security descriptor syntax. For more information, see [Application Security Descriptor Configuration Syntax](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/517895a9612241259d6941dbf9ad81cb.html "The syntax required to set the properties and values defined in the xs-security.json application security descriptor file.") :arrow_upper_right:.

        > ### Note:  
        > If you already have an xsuaa service instance, remember to update it first with the updated `xs-security.json` file. This is necessary as the content in the `xs-security.json` where the scope is granted to the SAP Job Scheduling service with the `grant-as-authority-to-apps` has changed.


3.  Make sure that you have a deployed application.

    For more information, see [Developing with the SAP Cloud Application Programming Model](https://help.sap.com/docs/btp/sap-business-technology-platform/developing-with-sap-cloud-application-programming-model?version=Cloud).

4.  Make sure that you've bound the xsuaa service instance to your application.

    For more information about how to bind applications, see [Binding Service Instances to Applications](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/e98280a71f17413088f8a10838a1e4cc.html) \(Cloud Foundry\) and [Using SAP BTP Services in the Kyma Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/ea4dd81e49254dd482d32e3c20f4477a.html "With the Kyma environment, you can connect SAP BTP services to your cluster and manage them using SAP BTP Service Operator.") :arrow_upper_right: \(Kyma\).

5.  Bind the SAP Job Scheduling service instance to your application.

    > ### Note:  
    > If you don't bind your application to the SAP Job Scheduling service instance, you can't call the SAP Job Scheduling service from your own application.




<a name="loio0adb6552e0914958a7a68f0ddbedfd32__section_lyc_ckw_pyb"/>

## Enabling the Service in the Cloud Foundry Runtime

For more information, see [Create a Service Instance in SAP BTP Cockpit](create-a-service-instance-in-sap-btp-cockpit-e267ab6.md) and [Create a Service Instance Using CF CLI](create-a-service-instance-using-cf-cli-cb56f9e.md).



<a name="loio0adb6552e0914958a7a68f0ddbedfd32__section_kwr_bkw_pyb"/>

## Enabling the Service in the Kyma Runtime

For more information, see [Create a Service Instance in the Kyma Dashboard](create-a-service-instance-in-the-kyma-dashboard-224a49a.md).



<a name="loio0adb6552e0914958a7a68f0ddbedfd32__section_bys_bnn_sjb"/>

## Setting Up Roles and Authorization

-   To create and bind Cloud Foundry service instances to applications, you must be assigned the **Space Manager** or the **Space Developer** role in the space.

    For more information, see [About Roles in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/09076385086b4da3bd1808d5ef572862.html "Roles determine which features users can view and access, and which actions they can initiate.") :arrow_upper_right:.

-   Kyma: To access the service dashboard, you must be assigned the `SAP_Job_Scheduling_Service_Admin` or the `SAP_Job_Scheduling_Service_Viewer` role.

    For more information, see [Roles and Role Collections](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/14a877c6e2f14832999df500ffa6e05e.html "Usually a role collection consists of one or multiple roles. You can use the SAP BTP cockpit to add or remove roles.") :arrow_upper_right:.


**Related Information**  


[Using SAP Job Scheduling Service](40---Using-JOB-SCHDULR-TITLE/using-sap-job-scheduling-service-9d48597.md "Define and manage one-time and recurring jobs using flexible schedules.")

[Define and Grant Scopes to SAP Job Scheduling Service](50---Security/define-and-grant-scopes-to-sap-job-scheduling-service-08933d3.md "Create and grant a scope to SAP Job Scheduling service.")

[Update a Service Instance](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/7f926eb79a7746fd996363118cd2c2aa.html "You can update a service instance from the xsuaa service using the service broker.") :arrow_upper_right:

