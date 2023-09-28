<!-- loioed3bf285065e4d42b95926589c36d39a -->

# Credential Rotation



<a name="loioed3bf285065e4d42b95926589c36d39a__section_obh_bhm_hvb"/>

## Binding Level Secrets

New clientsecrets are created every time you bind a service.

> ### Note:  
> The `clientsecret` included in the `VCAP_SERVICES` section of your application is specific to the binding.

This allows you to rotate secrets by unbinding and then binding the SAP Job Scheduling service instance again to the application.

The `clientsecret` assigned to the service instance becomes invalid if you unbind the service and the access token requests to the SAP Job Scheduling service REST API using it fail.

> ### Note:  
> Before this change, service instances using instance level secrets continue to use these and they remain valid. It's possible to rotate these out for binding level secrets by rebinding the service instance to the application.

**Related Information**  


[Secure Access](secure-access-745ca50.md "The SAP Job Scheduling service provides options to secure job actions with action endpoints as well as to secure Cloud Foundry tasks.")

[Create a Service Instance Using CF CLI](../create-a-service-instance-using-cf-cli-cb56f9e.md "To use the SAP Job Scheduling service with action endpoints in your application or with Cloud Foundry tasks, you create an instance of the SAP Job Scheduling service with the service plan standard using the Cloud Foundry Command Line Interface (CF CLI) and bind the service instance to your application.")

