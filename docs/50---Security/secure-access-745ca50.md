<!-- loio745ca502face47af9adb546a916ce1e8 -->

# Secure Access

The SAP Job Scheduling service provides options to secure job actions with action endpoints as well as to secure Cloud Foundry tasks.



<a name="loio745ca502face47af9adb546a916ce1e8__section_dld_wmm_wnb"/>

## Secure Job Actions with Action Endpoints

The SAP Authorization and Trust Management service is used to secure action endpoints in your application based on OAuth 2.0 authentication.

> ### Note:  
> When you create or update a SAP Job Scheduling service instance, set the `enable-xsuaa-support` parameter as `true`.



### OAuth 2.0 Authentication

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



<a name="loio745ca502face47af9adb546a916ce1e8__section_cwb_btm_wnb"/>

## Secure Cloud Foundry Tasks



The XSUAA isn’t required as Cloud controller. The Cloud Foundry User Account and Authentication \(CFUAA\) is used for creating CF tasks.

**Related Information**  


[Credential Rotation](credential-rotation-ed3bf28.md "")

[Define and Grant Scopes to SAP Job Scheduling Service](define-and-grant-scopes-to-sap-job-scheduling-service-08933d3.md "Create and grant a scope to SAP Job Scheduling service.")

[Web Access Control](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/70a62d12cf91493cb9d1ec3c04d19ff9.html)

[Application Security Descriptor Configuration Syntax](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/517895a9612241259d6941dbf9ad81cb.html)

