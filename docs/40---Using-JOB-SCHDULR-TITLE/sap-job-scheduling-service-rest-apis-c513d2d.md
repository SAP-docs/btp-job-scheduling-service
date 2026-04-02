<!-- loioc513d2de49b140d08da694fa263698f8 -->

# SAP Job Scheduling Service REST APIs

Use SAP Job Scheduling service REST APIs to create, manage, and monitor jobs and job schedules.



> ### Note:  
> The REST API of the SAP Job Scheduling service is available on the SAP Business Accelerator Hub: [https://api.sap.com/api/sap-btpjss-admin-v1/overview](https://api.sap.com/api/sap-btpjss-admin-v1/overview). You can use this resource to explore the API, interact with its endpoints, and generate client libraries for your desired programming language. Refer to and bookmark the API documentation of this service on the SAP Business Accelerator Hub as the API documentation on the SAP Help Portal is planned to be removed in the coming months.



<a name="loioc513d2de49b140d08da694fa263698f8__section_wlp_b2y_vz"/>

## Pagination

All SAP Job Scheduling service APIs support pagination. You can retrieve all data if you don’t pass any optional query parameters.

For more information, see [Understanding Offset and Cursor Pagination](understanding-offset-and-cursor-pagination-96ebd22.md).



<a name="loioc513d2de49b140d08da694fa263698f8__section_esp_d2y_vz"/>

## Time Zone

Run the SAP Job Scheduling service only in the UTC time zone.

> ### Caution:  
> Currently, no other time zones than UTC are supported.



<a name="loioc513d2de49b140d08da694fa263698f8__section_lgr_4vr_4tb"/>

## POST Request Body Size Limit

The POST request body size is limited by 100 KB. If this limit is exceeded, the HTTP response code 413 “request entity too large” is returned.



## Client Libraries



### Node.js Client Library \(Deprecated\)

For jobs that support action endpoints \(HTTP jobs\), the SAP Job Scheduling service provides an API client library in the Node.js language. This library allows you to directly access Node.js APIs and reduce the code required to consume the service.

For more information, see [Node.js Client Library \(Deprecated\)](node-js-client-library-deprecated-9b86127.md).

> ### Caution:  
> The Node.js library is deprecated on 2 April 2026. The library is planned to receive security updates for one year after deprecation. For more information, see [What's New for SAP Job Scheduling Service](../10---What-s-New/what-s-new-for-sap-job-scheduling-service-35dd2f8.md).
> 
> Use the REST API published on the SAP Business Accelerator Hub instead. You can use it to generate a client library for your preferred programming language that contains all up-to-date APIs and features. For more information, see [https://api.sap.com/api/sap-btpjss-admin-v1/overview](https://api.sap.com/api/sap-btpjss-admin-v1/overview).



### Java Client Library for XS Advanced

This java-js-client library is a Java wrapper that enables convenient access to the XS advanced REST API endpoints of SAP Job Scheduling service.

For more information, see [Java Client Library for XS Advanced \(java-js-client\)](https://help.sap.com/docs/SAP_HANA_PLATFORM/4505d0bdaf4948449b7f7379d24d0f0d/6511bc054b0e48369a625a8019fefd53.html).

**Related Information**  


[SAP Job Scheduling Service REST API](https://api.sap.com/api/sap-btpjss-admin-v1/overview)

