<!-- loioe267ab64be174995b1c23b737d9981d4 -->

# Create a Service Instance in SAP BTP Cockpit

To use the SAP Job Scheduling service with action endpoints in your application or with Cloud Foundry tasks, you create an instance of the SAP Job Scheduling service using the SAP BTP cockpit and bind the service instance to your application.



<a name="loioe267ab64be174995b1c23b737d9981d4__prereq_kbr_wzt_vz"/>

## Prerequisites

You've logged on to the SAP BTP cockpit. For more information, see [Navigate to Orgs and Spaces](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/5bf87353bf994819b8803e5910d8450f.html "To administer your Cloud Foundry environment, navigate to orgs, and spaces in the SAP BTP cockpit.") :arrow_upper_right:.



## Procedure

1.  In the *Service Marketplace*, choose *Job Scheduling Service*.

2.  From the *Job Scheduling Service* tile, open the *Actions* menu and choose *Create*.

    The *New Instance* wizard appears.

3.  Choose the service plan *standard*.

4.  Choose a name for your service instance, then choose *Next*.

5.  To enable User Account and Authentication \(xsuaa\), in *Configure instance parameters* specify the `enable-xsuaa-support` parameter as true.

    You can specify a JSON file to upload containing the parameter or enter details in JSON format as follows :

    `{"enable-xsuaa-support":true}`.

6.  Choose *Next* and verify the instance details. Then choose *Create*.

    You've created a service instance in your Cloud Foundry Space that's now available in the service instances section.

7.  Choose a deployed application that you want to bind to the new instance of SAP Job Scheduling service.

    For more information, see [Binding Service Instances to Cloud Foundry Applications](https://help.sap.com/viewer/09cc82baadc542a688176dce601398de/Cloud/en-US/0e6850de6e7146c3a17b86736e80ee2e.html?q=Binding%20service%20instances%20to%20cloud%20foundry%20applications).




<a name="loioe267ab64be174995b1c23b737d9981d4__result_oy1_1gp_n4b"/>

## Results

Your service instance is now bound to your application and you can start using the SAP Job Scheduling service.

**Related Information**  


[Deploy Business Applications in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/4946ea5421374924963ce8575a5f3d05.html "When an application for the Cloud Foundry environment resides in a folder on your local machine, you can deploy it and start it by executing the command line interface (CLI) command push. To deploy business applications bundled in a multitarget application archive, you have to use the command deploy-mta.") :arrow_upper_right:

[Creating Service Instances in Cloud Foundry](https://help.sap.com/viewer/09cc82baadc542a688176dce601398de/Cloud/en-US/6d6846def3c443aa9f83d127353147ce.html "The service instances that you create in your Cloud Foundry environment instance enable your Cloud Foundry apps to consume services natively from Cloud Foundry.") :arrow_upper_right:

