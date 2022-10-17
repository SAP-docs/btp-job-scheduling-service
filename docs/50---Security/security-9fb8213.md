<!-- loio9fb8213dd9a54ac68357c6112c671671 -->

# Security

Get an overview of the security-relevant information that applies to the SAP Job Scheduling service.



For information on the security features of SAP BTP, see [Security Guide for SAP BTP](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/e129aa20c78c4a9fb379b9803b02e5f6.html).



<a name="loio9fb8213dd9a54ac68357c6112c671671__section_c35_4hr_fpb"/>

## Identity and Access Management

This section describes how to secure action endpoints based on OAuth 2.0 authentication. For more information, see [Secure Access](secure-access-745ca50.md).



<a name="loio9fb8213dd9a54ac68357c6112c671671__section_jw1_f3l_fpb"/>

## Data Protection and Privacy

Governments place legal requirements on industry to protect data and privacy. We provide features and functions to help you meet these requirements.

> ### Note:  
> SAP does not provide legal advice in any form. SAP software supports data protection compliance by providing security features and data protection-relevant functions, such as blocking and deletion of personal data. In many cases, compliance with applicable data protection and privacy laws is not covered by a product feature. Furthermore, this information should not be taken as advice or a recommendation regarding additional features that would be required in specific IT environments. Decisions related to data protection must be made on a case-by-case basis, taking into consideration the given system landscape and the applicable legal requirements. Definitions and other terms used in this documentation are not taken from a specific legal source.

For general information about data protection and privacy on SAP BTP, see the SAP BTP documentation under [Data Protection and Privacy](https://help.sap.com/viewer/ea72206b834e4ace9cd834feed6c0e09/Cloud/en-US/7e513d31704a4a87831191e504ca850a.html).

> ### Caution:  
> The SAP Job Scheduling service does not provide the technical capabilities to support the collection, processing, and storage of personal data.

> ### Caution:  
> This service contains entry fields, which are not intended for storing personal data without additional technical and organizational measure to safeguard data protection and privacy. For example, the job name, schedule description, or the message text send back in the response payload from the action endpoint of the application to the SAP Job Scheduling service are stored in the run log.

**Related Information**  


[SAP Authorization and Trust Management Service in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/6373bb7a96114d619bfdfdc6f505d1b9.html)

[Secure Access](secure-access-745ca50.md "The SAP Job Scheduling service provides options to secure job actions with action endpoints as well as to secure Cloud Foundry tasks.")

