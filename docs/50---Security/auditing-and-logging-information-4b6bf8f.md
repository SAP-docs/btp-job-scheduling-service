<!-- loio4b6bf8fad7874e72baa34e332b1bbc7b -->

# Auditing and Logging Information

Here you can find a list of the security events that are logged by SAP Job Scheduling service.



## Overview

SAP Job Scheduling service uses the SAP Audit Log service to persist audit events. If the SAP Audit Log service is not bound at runtime, audit events fall back to standard output.

Here is a brief description of what each column of the table is all about:

-   **Event grouping** - events that share a similar format or relate to the same sources.

-   **What events are logged** - the security, data protection, or privacy-related event that the system logs.

-   **Additional information** - details that may help you interpret the log entry.




## Logged Events

**Security events written in audit logs**


<table>
<tr>
<th valign="top">

Event grouping

</th>
<th valign="top">

What events are logged

</th>
<th valign="top">

Additional information

</th>
</tr>
<tr>
<td valign="top">

Job

</td>
<td valign="top">

A job is created, updated, or deleted.

</td>
<td valign="top">

Emitted as:

-   `Action: JobCreation`

-   `Action: JobConfiguration`

-   `Action: JobDeletion`


Each request is logged twice: once at request start \(phase `START`\) and once at request end \(phase `END`\).

The `Info` object contains the calling user, service instance, authentication metadata, tenant information, and a `resourceContext` with the HTTP method, path, source IP, and the affected job identifier or name.

</td>
</tr>
<tr>
<td valign="top">

Schedule

</td>
<td valign="top">

A schedule of a job is created, updated, deleted, activated or deactivated. Deleting all schedules of a job is logged as a separate action.

</td>
<td valign="top">

Emitted as:

-   `Action: JobCreation`

-   `Action: JobScheduleConfiguration`

-   `Action: JobScheduleDeletion`

-   `Action: JobScheduleActivation`

-   `Action: JobScheduleRemoval` \(delete-all\)


Each request is logged twice: once at request start \(phase `START`\) and once at request end \(phase `END`\).

The `Info` object contains the calling user, service instance, authentication metadata, tenant information, and a `resourceContext` with the HTTP method, path, source IP, and the affected job and schedule identifiers, plus any schedule attributes submitted in the request \(for example, `description`, `active`, `time`, `cron`, `repeatInterval`, `repeatAt`\).

</td>
</tr>
<tr>
<td valign="top">

Global configuration

</td>
<td valign="top">

The global configuration of the service instance is updated. Currently, the only supported configuration parameter is `ASYNC_EXEC_TIMEOUT`, which controls the timeout \(in seconds\) for asynchronous job executions.

</td>
<td valign="top">

Emitted as `Action: GlobalConfigUpdate`.

Each request is logged twice: once at request start \(phase `START`\) and once at request end \(phase `END`\).

The `Info` object contains the calling user, service instance, authentication metadata, tenant information, and a `resourceContext` with the updated configuration parameters.

</td>
</tr>
</table>



## Message Format

Each audit event follows this pattern:

`Action: <ActionName> - Correlation-ID: <uuid> - Request phase: <START|END> - Info: <json>`

If a request fails, the `END` message also contains a `- Request processing failed: <error>` suffix.

When the message is recorded by the SAP Audit Log service, it is wrapped with a timestamp and the details of the user who performed the action. For example:

`Security event message "…" on 2026-01-15T10:23:32Z. Security event was related to user "xxxxxxxx-xxxx-4xxx-8xxx-xxxxxxxxxxxx".`



## Fields in the `Info` Object

**Info Object Fields**


<table>
<tr>
<th valign="top">

Field

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`userId` 

</td>
<td valign="top">

Identifier of the calling user or technical client. For users, this is the UAA user ID. For technical \(client-credentials\) calls, this is the OAuth client ID.

</td>
</tr>
<tr>
<td valign="top">

`userName` 

</td>
<td valign="top">

The user's name or email address as reported by the identity provider.

</td>
</tr>
<tr>
<td valign="top">

`serviceInstance` 

</td>
<td valign="top">

The globally unique identifier \(GUID\) of the SAP Job Scheduling service instance that received the request.

</td>
</tr>
<tr>
<td valign="top">

`authType` 

</td>
<td valign="top">

Authentication type of the request, for example: `oauth`, `basic`, or `ias-oauth`.

</td>
</tr>
<tr>
<td valign="top">

`grantType` 

</td>
<td valign="top">

OAuth grant type used to obtain the token. For example: `authorization_code`, `client_credentials`, `password`, `user_token`, or `urn:ietf:params:oauth:grant-type:jwt-bearer`.

</td>
</tr>
<tr>
<td valign="top">

`origin` 

</td>
<td valign="top">

Identity provider that issued the user's token, for example: `sap.ids`. This field is only populated for user tokens.

</td>
</tr>
<tr>
<td valign="top">

`tenantInfo` 

</td>
<td valign="top">

Child object with tenant details. This field is only populated when the request carries tenant context.

</td>
</tr>
<tr>
<td valign="top">

`tenantInfo.type` 

</td>
<td valign="top">

Indicates whether the request runs in the provider tenant \(PaaS\) or a subscriber tenant \(SaaS\).

</td>
</tr>
<tr>
<td valign="top">

`tenantInfo.subDomain` 

</td>
<td valign="top">

Subdomain of the acting tenant.

</td>
</tr>
<tr>
<td valign="top">

`tenantInfo.providerTenant` 

</td>
<td valign="top">

GUID of the provider tenant, which is the subaccount that owns the SAP Job Scheduling service instance.

</td>
</tr>
<tr>
<td valign="top">

`tenantInfo.consumerTenant` 

</td>
<td valign="top">

GUID of the consumer tenant, which is the subaccount that made the call. In single-tenant cases, this value is the same as `providerTenant`.

</td>
</tr>
<tr>
<td valign="top">

`tenantInfo.clientId` 

</td>
<td valign="top">

Client ID of the token used for the request.

</td>
</tr>
<tr>
<td valign="top">

`tenantInfo.zoneId` 

</td>
<td valign="top">

Identity zone of the acting tenant.

</td>
</tr>
<tr>
<td valign="top">

`resourceContext` 

</td>
<td valign="top">

Child object with request details. This field is only populated when non-empty.

</td>
</tr>
<tr>
<td valign="top">

`resourceContext.httpMethod` 

</td>
<td valign="top">

HTTP method of the request. For example: `POST`, `PUT`, or `DELETE`.

</td>
</tr>
<tr>
<td valign="top">

`resourceContext.path` 

</td>
<td valign="top">

Path of the affected resource. For example: `/jobs/8/schedules`.

</td>
</tr>
<tr>
<td valign="top">

`resourceContext.sourceIp` 

</td>
<td valign="top">

Source IP address of the request.

</td>
</tr>
<tr>
<td valign="top">

`resourceContext.jobId`, `resourceContext.scheduleId` 

</td>
<td valign="top">

Identifiers of the affected job and schedule, when present.

</td>
</tr>
<tr>
<td valign="top">

`resourceContext.jobName`, `resourceContext.description`, `resourceContext.active`, `resourceContext.activationStatus`, `resourceContext.schedules`, `resourceContext.cron`, `resourceContext.repeatInterval`, `resourceContext.repeatAt`, `resourceContext.time` 

</td>
<td valign="top">

Attributes submitted with the request, when present.

</td>
</tr>
<tr>
<td valign="top">

`resourceContext.configParams` 

</td>
<td valign="top">

Configuration parameters updated by a `GlobalConfigUpdate` request.

</td>
</tr>
</table>

> ### Note:  
> A field appears only when it has a value. The audit logs omit `tenantInfo` and `resourceContext` when there is no data.



## Where Are the Logs Stored?

Audit events are written under the tenant to which the request applies:

-   For calls made in the context of a subscriber tenant \(multitenant applications\), events are written under that subscriber tenant.

-   For calls made in the provider tenant \(single-tenant service instances, technical calls with client credentials without a consumer tenant\), events are written under the provider tenant of the application that consumes SAP Job Scheduling service.


To access the audit log entries, use the SAP Audit Log Viewer in the corresponding subaccount, or retrieve them via the Audit Log Retrieval API.

**Related Information**  


[Secure Access](secure-access-745ca50.md "The SAP Job Scheduling service provides options to secure job actions with action endpoints as well as to secure Cloud Foundry tasks.")

[Credential Rotation](credential-rotation-ed3bf28.md "The credential rotation procedure differs based on the authentication method used by your SAP Job Scheduling service instance.")

[SAP Audit Log Viewer service for the Cloud Foundry Environment](https://help.sap.com/docs/btp/sap-business-technology-platform/audit-log-viewer-for-cloud-foundry-environment)

[Audit Log Retrieval API \(Cloud Foundry environment\)](https://api.sap.com/api/CFAuditLogRetrievalAPI/resource/AuditlogRetrievalAPI)

[Troubleshooting Scenarios](../troubleshooting-scenarios-b05dc8c.md "Find solutions to the most common issues related to SAP Job Scheduling service.")

