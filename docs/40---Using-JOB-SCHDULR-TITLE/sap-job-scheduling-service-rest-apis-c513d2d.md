<!-- loioc513d2de49b140d08da694fa263698f8 -->

# SAP Job Scheduling Service REST APIs

Use SAP Job Scheduling service REST APIs to create, manage, and monitor jobs and job schedules.



<a name="loioc513d2de49b140d08da694fa263698f8__section_gfx_tp5_ljb"/>

## Authentication



### Service Plan `lite`

The SAP Job Scheduling service REST APIs are guarded by HTTP Basic authentication, which requires a user name and a password. Both are fetched from the `VCAP_SERVICES` section of the application environment after binding it to the SAP Job Scheduling service.

Use the following command to view the `VCAP_SERVICES` content:

```
$ cf env <application-name>
{
    "VCAP_SERVICES": {
        "jobscheduler": [
            {
                "credentials": {
                    "clientid": "PRIVATE_DATA_HIDDEN",
                    "identityzone": "PRIVATE_DATA_HIDDEN",
                    "password": "PRIVATE_DATA_HIDDEN",
                    "url": "https://jobscheduler-rest.cfapps.stagingaws.hanavlab.ondemand.com",
                    "user": "PRIVATE_DATA_HIDDEN",
                    "xsappname": "PRIVATE_DATA_HIDDEN"
                },
                "label": "jobscheduler",
                "name": "js-instance",
                "plan": "default",
                "provider": null,
                "syslog_drain_url": null,
                "tags": [
                    "jobscheduler"
                ]
            }
        ]
    }
}
```

All APIs are accessed through HTTPS.

> ### Note:  
> All data is sent and received in the JSON format. When sending data through API requests, make sure that the HTTP header `Content-type` is set to `application/json`.



### Service Plan `standard`

You can access the REST API for a `standard` instance by providing an OAuth token.

In the `VCAP_SERVICES` of your application, you can find the following section:

```
{
    "jobscheduler": [
        {
            "..": "..",
            "credentials": {
                "uaa": {
                    "apiurl": "<apiurl>",
                    "clientid": "<clientid>",
                    "clientsecret": "<clientsecret>",
                    "identityzone": "<identityzone>",
                    "identityzoneid": "<identityzoneid>",
                    "sburl": "<sburl>",
                    "tenantid": "<tenantid>",
                    "tenantmode": "dedicated",
                    "uaadomain": "<uaadomain>",
                    "url": "<url>",
                    "verificationkey": "<key>",
                    "xsappname": "<xsappname>"
                },
                "url": "https://jobscheduler-rest.<landscape-domain>"
            },
            "...": "..."
        }
    ]
}
```

1.  Fetch an OAuth token from xsuaa by using the provided `clientid` and `clientsecret`:

    ```
    Method: POST
    Url: <value from credentials.uaa.url>/oauth/token
    Header:
        Content-Type: application/x-www-form-urlencoded
        Authorization: Basic <Base64 encoded clientid:clientsecret>
        Cache-Control: no-cache
    Body:
        grant_type=client_credentials
    ```

    The response should look as follows:

    ```
    {
        "access_token": "<token>",
        "token_type": "bearer",
        "expires_in": 43199,
        "scope": "<scope(s)>",
        "jti": "<hidden>"
    }
    ```

2.  Use the `access_token` in your request to the SAP Job Scheduling service REST API:

    ```
    ...
    Url: <value from credentials.url>/scheduler/
    Header:
        Authorization: Bearer <access_token>
    ...
    ```




<a name="loioc513d2de49b140d08da694fa263698f8__section_c2w_st2_wnb"/>

## Binding Level Secrets

New clientsecrets are created every time you bind a service.

> ### Note:  
> The `clientsecret` included in the `VCAP_SERVICES` section of your application is specific to the binding.

This allows you to rotate secrets by unbinding and then binding the SAP Job Scheduling service instance again to the application.

The `clientsecret` assigned to the service instance becomes invalid if you unbind the service and the access token requests to the SAP Job Scheduling service REST API using it fail.

> ### Note:  
> Before this change, service instances using instance level secrets continue to use these and they remain valid. It's possible to rotate these out for binding level secrets by rebinding the service instance to the application.



<a name="loioc513d2de49b140d08da694fa263698f8__section_wlp_b2y_vz"/>

## Pagination

All SAP Job Scheduling service APIs support pagination. You can retrieve all data if you don’t pass any query parameter.



<a name="loioc513d2de49b140d08da694fa263698f8__section_esp_d2y_vz"/>

## Time Zone

Run the SAP Job Scheduling service only in the UTC time zone.

> ### Caution:  
> Currently, no other time zones than UTC are supported.



<a name="loioc513d2de49b140d08da694fa263698f8__section_lgr_4vr_4tb"/>

## POST Request Body Size Limit

The POST request body size is limited by 100 KB. If this limit is exceeded, the HTTP response code 400 “request entity too large” is returned.



<a name="loioc513d2de49b140d08da694fa263698f8__section_t3y_22r_mjb"/>

## Overview of All SAP Job Scheduling service REST APIs

