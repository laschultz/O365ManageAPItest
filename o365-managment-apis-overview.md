
# Office 365 Management APIs overview


 **Last modified:** January 26, 2016

 _**Applies to:** Office 365_



The Office 365 Management APIs will provide a single extensibility platform for all Office 365 customers' and partners' management tasks, including service communications, security, compliance, reporting, and auditing.
All of the Office 365 Management APIs will be consistent in design and implementation with the current suite of Office 365 REST APIs, using common industry-standard approaches, including OAuth v2, OData v4, and JSON. Like the other Office 365 APIs, applications are registered in Azure Active Directory, giving developers a consistent way to authenticate and authorize their apps.
If you have questions about the Office 365 Management APIs, post your question on [Stack Overflow](http://stackoverflow.com/tags/office365), using the [office365] tag.

## Office 365 Service Communications API (preview)

The Office 365 Service Communications API has been released in preview mode. It will replace the current [Office 365 Service Communications API](https://msdn.microsoft.com/library/office/dn776043.aspx) to provide service health information to tenant administrators and partners. Unlike the previous version, the new Service Communications API will deliver a cohesive platform experience, with REST APIs built in a consistent fashion including URL naming, data format, and authentication.

New features will only be added to the new version of the API, encouraging early adoption by legacy customers. When the General Announcement of Office 365 Service Communications API is made, the older version of the Service Communications API will begin a period of deprecation. For operations reference, see [Office 365 Service Communications API reference (preview)](https://msdn.microsoft.com/EN-US/library/dn707386.aspx).


## Office 365 Management Activity API

The Office 365 Management Activity API provides information about various user, admin, system, and policy actions and events from Office 365 and Azure Active Directory activity logs. Customers and partners can use this information to create new or enhance existing operations, security, and compliance-monitoring solutions for the enterprise. For operations reference, see [Office 365 Management Activity API reference](https://msdn.microsoft.com/EN-US/library/dn707386.aspx).

