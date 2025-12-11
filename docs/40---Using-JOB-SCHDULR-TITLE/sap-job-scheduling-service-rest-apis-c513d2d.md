<!-- loioc513d2de49b140d08da694fa263698f8 -->

# SAP Job Scheduling Service REST APIs

Use SAP Job Scheduling service REST APIs to create, manage, and monitor jobs and job schedules.



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

**Related Information**  


[REST APIs](rest-apis-3dcd04a.md "SAP Job Scheduling service REST APIs")

[Java Client Library for XS Advanced \(java-js-client\)](https://help.sap.com/docs/SAP_HANA_PLATFORM/4505d0bdaf4948449b7f7379d24d0f0d/6511bc054b0e48369a625a8019fefd53.html?version=2.0.07#loio6511bc054b0e48369a625a8019fefd53__section_ctf_5w4_dz)

