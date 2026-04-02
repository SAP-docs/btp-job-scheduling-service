<!-- loioed3bf285065e4d42b95926589c36d39a -->

# Credential Rotation

The credential rotation procedure differs based on the authentication method used by your SAP Job Scheduling service instance.



<a name="loioed3bf285065e4d42b95926589c36d39a__section_obh_bhm_hvb"/>

## Binding Level Secrets

New clientsecrets are created every time you bind a service.

> ### Note:  
> The `clientsecret` included in the `VCAP_SERVICES` section of your application is specific to the binding.

This allows you to rotate secrets by unbinding and then binding the SAP Job Scheduling service instance again to the application.

The `clientsecret` assigned to the service instance becomes invalid if you unbind the service and the access token requests to the SAP Job Scheduling service REST API using it fail.

> ### Note:  
> Before this change, service instances using instance level secrets continue to use these and they remain valid. It's possible to rotate these out for binding level secrets by rebinding the service instance to the application.



## Using XSUAA Authentication

For service instances using SAP Authorization and Trust Management service \(XSUAA\) authentication \(the default\), credentials are managed at the binding level.



## Using Authentication with Identity Authentication Service

For service instances using authentication with Identity Authentication service, credentials are managed through the SAP Cloud Identity Services - Identity Authentication service instance.

> ### Note:  
> The SAP Job Scheduling service binding with the Identity Authentication service authentication doesn't contain authentication credentials. Instead, your application uses credentials from its SAP Cloud Identity Services - Identity Authentication service binding. The binding does include the Identity Authentication client ID of the SAP Job Scheduling service for callback token validation.

This allows you to rotate credentials by unbinding and then binding the Identity Authentication service instance again to the application:

1.  Unbind the SAP Cloud Identity Services - Identity Authentication service instance from your application.
2.  Bind the Identity Authentication service instance to your application again. New credentials are generated automatically.
3.  Restage the application.

For single-tenant applications, you can use either client credentials or X.509 certificates.

For multitenant applications, X.509 certificates are required.

Example parameters for Identity Authentication service binding with X.509 certificates \(required for multitenant applications, optional for single-tenant applications\):

> ### Sample Code:  
> ```
> {
>    "credential-type": "X509_GENERATED",
>    "key-length": 2048,
>    "validity": 365,
>    "validity-type": "DAYS",
>    "app-identifier": "<your-app-name>"
> }
> ```

**Related Information**  


[Secure Access](secure-access-745ca50.md "The SAP Job Scheduling service provides options to secure job actions with action endpoints as well as to secure Cloud Foundry tasks.")

[Create a Service Instance Using CF CLI](../create-a-service-instance-using-cf-cli-cb56f9e.md "To use the SAP Job Scheduling service with action endpoints in your application or with Cloud Foundry tasks, you create an instance of the SAP Job Scheduling service with the service plan standard using the Cloud Foundry Command Line Interface (CF CLI) and bind the service instance to your application.")

[Using SAP Job Scheduling Service](../40---Using-JOB-SCHDULR-TITLE/using-sap-job-scheduling-service-9d48597.md "Define and manage one-time and recurring jobs using flexible schedules.")

[SAP Cloud Identity Services](https://help.sap.com/docs/cloud-identity-services)

