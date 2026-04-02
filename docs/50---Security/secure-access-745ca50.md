<!-- loio745ca502face47af9adb546a916ce1e8 -->

# Secure Access

The SAP Job Scheduling service provides options to secure job actions with action endpoints as well as to secure Cloud Foundry tasks.



## Choose an Authentication Method

The SAP Job Scheduling service supports two authentication methods:

-   XSUAA \(default\): Uses the SAP Authorization and Trust Management service \(XSUAA\) with OAuth 2.0 authentication.
-   SAP Cloud Identity Services - Identity Authentication: Uses the Identity Authentication service with OAuth 2.0 authentication.

You choose the authentication method when creating a service instance. For more information, see [Create a Service Instance in SAP BTP Cockpit](../create-a-service-instance-in-sap-btp-cockpit-e267ab6.md).



<a name="loio745ca502face47af9adb546a916ce1e8__section_dld_wmm_wnb"/>

## Secure Job Actions with Action Endpoints

Based on the authentication method you choose, either the SAP Authorization and Trust Management service or the Identity Authentication service secures the action endpoints in your application.



### XSUAA Authentication \(OAuth 2.0\)

**Prerequisites:** The application is bound to an xsuaa service instance and a SAP Job Scheduling service instance.

-   SAP Job Scheduling service invokes the action endpoint, passing an access token obtained from UAA in the **Authorization** header.

    > ### Note:  
    > Within the application which exposes an action endpoint that is called from the SAP Job Scheduling service, you can validate this token using the xsuaa instance bound to this application.

-   SAP Job Scheduling service caches the token for up to twelve hours.

    > ### Note:  
    > Consequently, it may take some time until the updates made to the scopes already granted to the SAP Job Scheduling service take effect, for example, if the application changes the scope name in the `xs-security.json` security descriptor file. During this time, it's possible that a token with the old scope is sent to the application. This may lead to an error, if the application doesn't accept the older scope.

-   The application must grant a scope to the SAP Job Scheduling service instance.

    For this, in the `xs-security.json` security descriptor file that is used from the xsuaa service instance that is bound to the application, specify the following value for the `grant-as-authority-to-apps` property:

    `$XSSERVICENAME(<jobscheduler instance name>)`

    > ### Note:  
    > `$XSAPPNAME.<name>`: A scope name consists of `$XSAPPNAME.` and a name you can choose, for example, `<Jobs>`.

    Add the following to the `scopes` section:

    ```
    {
        "xsappname": "<app name>",
        "scopes": [{
            "name": "$XSAPPNAME.Jobs",
            "description": "SAP Job Scheduling
                                    service Scope",
            "grant-as-authority-to-apps": [
                "$XSSERVICENAME(<jobscheduler instance name>)"
                ]
        }]
    }
    ```


> ### Note:  
> SAP Job Scheduling service uses the content-type application/json for its requests and accepts the response `Content-type` `application/json`.



### Authentication with Identity Authentication Service

**Prerequisites**

-   You've bound the application to an Identity Authentication service instance.

-   You've bound the application an SAP Job Scheduling service instance created with `authentication: "ias"`.

    Example for the Identity Authentication service instance in the configuration JSON file:

    > ### Sample Code:  
    > ```
    > {
    >     "display-name": "My Application",
    >     "consumed-services": [
    >         {
    >             "service-instance-name": "<jobscheduler instance name>"
    >         }
    >     ]
    > }
    > ```

-   The SAP Job Scheduling service is specified in the `consumed-services` property of the Identity Authentication service instance configuration.


**Using the Identity Authentication Service**

When using this authentication method:

-   The SAP Job Scheduling service invokes the action endpoint by passing an access token obtained from the Identity Authentication service.

    > ### Note:  
    > Within the application which exposes an action endpoint called from the SAP Job Scheduling service, you can validate this token using the Identity Authentication service tenant used by the application.

-   The SAP Job Scheduling service caches the token based on the token's expiry time \(typically one hour\).
-   To call the SAP Job Scheduling service REST API, applications must obtain an OAuth token from their Identity Authentication service tenant.

    > ### Note:  
    > Unlike the SAP Authorization and Trust Management service, the SAP Job Scheduling service bindings that use authentication from the Identity Authentication service don't provide credentials for calling the SAP Job Scheduling service directly. Instead, applications use credentials from their own SAP Cloud Identity Services - Identity Authentication service instance binding. For multitenant applications, X.509 client certificate authentication \(mTLS\) is required. Single-tenant applications can use either client credentials or X.509 certificates.




<a name="loio745ca502face47af9adb546a916ce1e8__section_cwb_btm_wnb"/>

## Secure Cloud Foundry Tasks



The XSUAA isn’t required as Cloud controller. The Cloud Foundry User Account and Authentication \(CFUAA\) is used for creating CF tasks.

**Related Information**  


[Credential Rotation](credential-rotation-ed3bf28.md "The credential rotation procedure differs based on the authentication method used by your SAP Job Scheduling service instance.")

[Define and Grant Scopes to SAP Job Scheduling Service](define-and-grant-scopes-to-sap-job-scheduling-service-08933d3.md "Create and grant a scope to SAP Job Scheduling service.")

[Web Access Control](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/70a62d12cf91493cb9d1ec3c04d19ff9.html)

[Application Security Descriptor Configuration Syntax](https://help.sap.com/docs/btp/sap-business-technology-platform/application-security-descriptor-configuration-syntax)

[SAP Cloud Identity Services](https://help.sap.com/docs/cloud-identity-services)

