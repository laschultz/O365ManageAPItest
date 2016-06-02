
# Office 365 Service Communications API reference (preview)

 **Last modified:** June 2, 2016

 _**Applies to:** Office 365_

 **Note**  This documentation covers features that are currently in preview. For information about working with preview features, see [Preview developer features on the Office 365 platform](https://msdn.microsoft.com/en-us/office/office365/howto/platform-development-preview-features-overview).

You can use the Office 365 Service Communications API V2 to access the following data:

-  **[Get Services](#ServicesMethod)**: Get the list of subscribed services.
    
-  **[Get Current Status](#GetCurrentStatus)**: Get a real-time view of current and ongoing service incidents and maintenance events
    
-  **[Get Historical Status](#GetHistoricalStatus)**: Get a historical view of service health, including service incidents and maintenance events.
    
-  **[Get Messages](#GetMessages)**: Find Incident, Planned Maintenance, and Message Center communications.
    
Currently, the Office 365 Service Communications API contains data for the following services: Dynamics CRM, Dynamics Marketing, Exchange Online, Exchange Online Protection, Identity Service, Mobile Device Management, Office 365 Partner Admin Center, OneDrive for Business, Parature, OneDrive for Business, Power BI for Office 365, Rights Management Service, SharePoint Online, SHD Admin, Skype for Business, Social Engagement, and Yammer Enterprise.

### The Fundamentals

The root URL of the API includes a tenant identifier that scopes the operations to a single tenant:


```
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

The  **Office 365 Service Communications API** is a REST service that allows you to develop solutions using any web language and hosting environment that supports HTTPS and X.509 certificates. The API relies on **Microsoft Azure Active Directory** and the **OAuth2** protocol for authentication and authorization. To access the API from your application, you'll need to first register it in Azure AD and configure it with permissions at the appropriate scope. This will enable your application to request OAuth2 access tokens necessary for calling the API. You can find more information about registering and configuring an application in Azure AD at[Office 365 Management APIs getting started](https://msdn.microsoft.com/EN-US/library/dn707385.aspx).

All API requests require an Authorization HTTP header that has a valid OAuth2 JWT access token obtained from Azure AD that contains the  **ServiceHealth.Read** claim; and the tenant identifier must match the tenant identifier in the root URL.




```
Authorization: Bearer {OAuth2 token}
```

 **Request Header:**

These are the supported request headers for all Office 365 Service Communications API operations:



|**Header**|**Description**|
|:-----|:-----|
|**Accept (Optional)**|The following are acceptable representations for the response: **application/json;odata.metadata=full** **application/json;odata.metadata=minimal** [The default if header not specified] **application/json;odata.metadata=none**|
|**Authorization (Required)**|Authorization token (Bearer JWT AAD Token) for the request.|
 **Response Headers:**

These are the response headers returned for all Office 365 Service Communications API operations:



|**Header**|**Description**|
|:-----|:-----|
|**Content-Length**|The length of the response body.|
|**Content-Type**|Representation of the response:  **application/json** **application/json;odata.metadata=full** **application/json;odata.metadata=minimal** **application/json;odata.metadata=none** **odata.streaming=true**|
|**Cache-Control**|Used to specify directives that all caching mechanisms along the request/response chain must obey.|
|**Pragma**|Implementation-specific behaviors.|
|**Expires**|When the client should make the resource expire.|
|**X-Activity-Id**|The server-generated activity Id.|
|**OData-Version**|The supported OData Version (4.0).|
|**Date**|The date in UTC when the response was sent from the server.|
|**X-Time-Taken**|The time it took to generate the response (ms).|
|**X-Instance-Name**|The identifier of the Azure instance used to generate the response (for debugging purposes).|
|**Server**|The server used to generate the response (for debugging purposes).|
|**X-ASPNET-Version**|The version of ASP.Net used by the server that generated the response (for debugging purposes).|
|**X-Powered-By**|The technologies used in the server that generated the response (for debugging purposes).|

### Office 365 Service Communications API operations




#### Get Services
<a name="ServicesMethod"> </a>

Returns the list of subscribed services.


||||
|:-----|:-----|:-----|
|**Path**| `/Services`||
|**Query-option**|$select|Pick a subset of properties.|
|**Response**|List of "Service" entities|"Service" entity contains "Id" (String), "DisplayName" (String), and "FeatureNames" (list of Strings).|
 **Sample Request:**




```

GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

 **Sample Response:**




```

{
    "value": [
        {
            "Id": "Exchange",
            "DisplayName": "Exchange Online",
            "FeatureNames": [
                "Sign-in",
                "E-Mail and calendar access",
                "E-Mail timely delivery",
                "Management and Provisioning",
                "Voice mail"
            ]
        },
        {
            "Id": "Lync",
            "DisplayName": "Lync Online",
            "FeatureNames": [
                "Audio and Video",
                "Federation",
                "Management and Provisioning",
                "Sign-In",
                "All Features",
                "Dial-In Conferencing",
                "Online Meetings",
                "Instant Messaging",
                "Presence",
                "Mobility"
            ]
        }
    ]
}

```


### Get Current Status
<a name="GetCurrentStatus"> </a>

Returns the current status of the service.


||||
|:-----|:-----|:-----|
|**Path**| `/CurrentStatus`||
|**Filter**|Workload|Filter by workload (String, default: all).|
|**Query-option**|$select|Pick a subset of properties.|
|**Response**|List of "WorkloadStatus" entities.|"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus")."FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String) and "FeatureStatus" (String).|
 **Sample Request:**




```
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

 **Sample Response:**




```

{
    "value": [
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        },
        {
            "Id": "Lync",
            "Workload": "Lync",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Lync Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "AudioVideo",
                    "FeatureGroupDisplayName": "Audio and Video",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Federation",
                    "FeatureGroupDisplayName": "Federation",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "ManagementandProvisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Sign-In",
                    "FeatureGroupDisplayName": "Sign-In",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "All",
                    "FeatureGroupDisplayName": "All Features",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "DialInConferencing",
                    "FeatureGroupDisplayName": "Dial-In Conferencing",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "OnlineMeetings",
                    "FeatureGroupDisplayName": "Online Meetings",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "InstantMessaging",
                    "FeatureGroupDisplayName": "Instant Messaging",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Presence",
                    "FeatureGroupDisplayName": "Presence",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Mobility",
                    "FeatureGroupDisplayName": "Mobility",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        }
    ]
}


```


### Get Historical Status
<a name="GetHistoricalStatus"> </a>

Returns the historical status of the service, by day, over a certain time range.


||||
|:-----|:-----|:-----|
|**Path**| `/HistoricalStatus`||
|**Filters**|Workload|Filter by workload (String, default: all).|
||StatusTime|Filter by days greater than StatusTime (DateTimeOffset, default: ge CurrentTime - 7 days).|
|**Query-option**|$select|Pick a subset of properties.|
|**Response**|List of "WorkloadStatus" entities.|"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus")."FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String) and "FeatureStatus" (String).|
 **Sample Request:**




```
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

 **Sample Response:**




```
{
    "value": [
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        },
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-10T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "InformationAvailable",
            "IncidentIds": [
                "EX20870"
            ],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "InformationAvailable"
                }
            ]
        }
    ]
}


```


### Get Messages
<a name="GetMessages"> </a>

 **Description:**

Returns the messages about the service over a certain time range. Use the type filter to filter for "Service Incident", "Planned Maintenance", or "Message Center" messages.


||||
|:-----|:-----|:-----|
|**Path**| `/Messages`||
|**Filters**|Workload|Filter by workload (String, default: all).|
||StartTime|Filter by Start Time (DateTimeOffset, default: ge CurrentTime - 7 days).|
||EndTime|Filter by End Time (DateTimeOffset, default: le CurrentTime).|
||MessageType|Filter by MessageType (String, default: all).|
||ID|Filter by ID (String, default: all).|
|**Query-option**|$select|Pick a subset of properties.|
||$top|Pick the top number of results (default and max $top=100).|
||$skip|Skip number of results (default: $skip=0).|
|**Response**|List of "Message" entities.|"Message" entity contains "Id" (String), "StartTime" (DateTimeOffset), "EndTime" (DateTimeOffset), "Status" (String), "Messages" (list of "MessagHistory" entity), "LastUpdatedTime" (DateTimeOffset), "Workload" (String), "WorkloadDisplayName" (String), "Feature" (String), "FeatureDisplayName" (String), "MessageType" (Enum, default: all)."MessageHistory" entity contains "PublishedTime" (DateTimeOffset), "MessageText" (String).|
 **Sample Request:**




```
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

 **Sample Response:**




```
{
 {
    "value": [
        {
            "Id": "EX20119",
            "Name": "EX20119",
            "Title": null,
            "StartTime": "2015-04-01T22:25:00Z",
            "EndTime": "2015-04-07T21:48:00Z",
            "Status": "Service restored",
            "Messages": [
                {
                    "PublishedTime": "2015-04-01T22:34:28.76Z",
                    "MessageText": "Current Status: Engineers are investigating an issue in which some customers may be experiencing problems accessing or using Exchange Online services or features. This event is actively being investigated. More information will be provided shortly."
                },
                {
                    "PublishedTime": "2015-04-03T18:45:32.56Z",
                    "MessageText": "Current Status: Engineers are implementing a fix within the affected infrastructure to remediate Exchange Online archive access issues. \n\nUser Experience: Affected users are unable to access online archives when using Outlook Web App (OWA). As a workaround, users may be able to access online archives via the Outlook client.\n\nCustomer Impact: Customer impact appears to be limited at this time. This issue only affects hybrid customers.\n\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues.  \n\nNext Update by: Monday, April 6, 2015, at 9:00 PM UTC\n"
                },
                {
                    "PublishedTime": "2015-04-06T21:17:34.007Z",
                    "MessageText": "Current Status: Deployment of the fix is almost complete. Engineers are monitoring service health to ensure the issue has been remediated. \n\nUser Experience: Affected users are unable to access online archives when using Outlook Web App (OWA). As a workaround, users may be able to access online archives via the Outlook client. \n\nCustomer Impact: Customer impact appears to be limited at this time. This issue only affects hybrid customers.\n\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues. \n\nNext Update by: Tuesday, April 7, 2015, at 10:00 PM UTC "
                },
                {
                    "PublishedTime": "2015-04-08T21:54:49.06Z",
                    "MessageText": "Final Status: Engineers have implemented a fix which remediated end-user impact. \r\n\r\nUser Experience: Affected users were unable to access online archives when using Outlook Web App (OWA).\r\n\r\nCustomer Impact: Customer impact appears to have been limited. This issue only affected hybrid customers.\r\n\r\nIncident Start Time: Monday, March 30, 2015, at 9:28 AM UTC\r\n\r\nIncident End Time: Tuesday, April 7, 2015, at 8:00 PM UTC\r\n\r\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues.  \r\n\r\nNext Steps: The following is a list of known action item(s) associated with this incident. As part of the Office 365 problem management process, additional engineering actions may be identified to improve the overall service.\r\n- Action: Review the monitoring infrastructure for improvements as this event was reported by customers before an alert prompted a high priority investigation. \r\n\r\nA post-incident report will be available on the Service Health Dashboard within five business days."
                }
            ],
            "LastUpdatedTime": "2015-04-08T21:54:49.55Z",
            "Workload": "Exchange Online",
            "WorkloadDisplayName": "Exchange",
            "Feature": "Access",
            "FeatureDisplayName": "E-Mail and calendar access"
        },
        {
            "Id": "EX20789",
            "Name": "EX20789",
            "Title": null,
            "StartTime": "2015-04-06T20:00:00Z",
            "EndTime": "2015-04-07T23:00:00Z",
            "Status": "Service restored",
            "Messages": [
                {
                    "PublishedTime": "2015-04-07T23:26:44.643Z",
                    "MessageText": "Final Status: Engineers have validated that the deployed fix has resolved the issue and that service is restored.\r\n\r\nUser Experience: Affected users were unable to send or receive email while using Exchange Web Services (EWS) on their mobile devices.\r\n\r\nCustomer Impact: Customer impact appeared to be limited during this event. This issue was only affecting customers that use third-party Mobile Device Management software from Good Technology. As a workaround to provide immediate relief from impact, engineers implemented a configuration change for customers who reported this issue to Microsoft Support.\r\n\r\nIncident Start Time: Wednesday, April 1, 2015, at 2:00 PM UTC\r\n\r\nIncident End Time: Tuesday, April 7, 2015, at 10:00 PM UTC\r\n\r\nPreliminary Root Cause: As part of our ongoing efforts to improve service resiliency, an update was deployed to the infrastructure that facilitates connections from multiple Exchange Online protocols to mailbox databases. The update, however, contained a code issue that caused connectivity issues in some scenarios. \r\n\r\nNext Steps: The following is a list of known action item(s) associated with this incident. As part of the Office 365 problem management process, additional engineering actions may be identified to improve the overall service.\r\n- Action: Review the infrastructure update process to prevent reoccurrences of this scenario.\r\n\r\nPlease consider this service notification the final update on the event."
               }
            ],
            "LastUpdatedTime": "2015-04-07T23:26:45.08Z",
            "Workload": "Exchange Online",
            "WorkloadDisplayName": "Exchange",
            "Feature": "Access",
            "FeatureDisplayName": "E-Mail and calendar access"
        }
    ]
}

```


### Errors
<a name="GetMessages"> </a>

When the service encounters an error, it reports the error response code to the caller, using standard HTTP error-code syntax. As per [OData V4 specification](http://docs.oasis-open.org/odata/odata-json-format/v4.0/os/odata-json-format-v4.0-os.mdl), additional information is included in the body of the failed call as a single JSON object. The following is an example of a full JSON error body:


```

{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}

```

