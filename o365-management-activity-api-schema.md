
# Office 365 Management Activity API schema


 **Last modified:** June 2, 2016
 
 _**Applies to: Office 365**_
 
 **In this article**<br>
[Office 365 Management API schemas](#top)<br>
[Common Schema](#common)<br>
[Sway Schema](#sway)<br>
[SharePoint Base Schema](#spbase)<br>
[SharePoint File Operations](#SPFileOperations)<br>
[SharePoint Sharing Schema](#SPShare)<br>
[SharePoint Schema](#sp)<br>
[Exchange Admin Schema](#ExchangeAdminSchema)<br>
[Exchange Mailbox Schema](#ExchangeMailboxSchema)<br>
[Azure Active Directory Base Schema](#AzureActiveDirectoryBaseSchema)<br>
[Azure Active Directory Account Logon Schema](#AzureActiveDirectoryAccountLogonSchema)<br>
[Azure Active Directory Schema](#AzureActiveDirectorySchema)<br>
[Azure Active Directory STS Logon Schema](#AzureActiveDirectorySTSSchema)<br>
[Data Center Security Base Schema](#DataCenterSecurityBaseSchema)<br>
[Data Center Security Cmdlet Schema](#DataCenterSecurityCmdletSchema)


The Office 365 Management Activity API schema is provided as a data service in two layers:


-  **Common Schema** - The interface to access core Office 365 auditing concepts such as Record Type, Creation Time, User Type, and Action as well as to provide core dimensions (such as User ID), location specifics (such as Client IP address), and product-specific properties (such as Object ID). It establishes consistent and uniform views for users to extract all Office 365 audit data in a few top level views with the appropriate parameters, and provides a fixed schema for all the data sources, which significantly reduces the cost of learning. Common schema is sourced from product data that is owned by each product team, such as Exchange, SharePoint, Azure Active Directory, Yammer, and OneDrive for Business. The Object ID field can be extended by product teams to add product specific properties.
    
-  **Product-specific schema** - Built on top of the Common Schema to provide a set of product-specific attributes; for example, Sway schema, SharePoint schema, OneDrive for Business schema, and Exchange admin schema.
    
 **Which layer should you use for your scenario?**
In general, if the data is available in a higher layer, don't go back to a lower layer. In other words, if the data requirement can be fit in a product-specific schema, you don't need to go back to the Common Schema. 

## Office 365 Management API schemas
<a name="top"> </a>

This article provides details on the Common Schema as well as each of the product specific schemas. The following table describes the available schemas. 



|**Name of schema**|**Description**|
|:-----|:-----|
|[Common Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#common)|The view to extract Record Type, User ID, Client IP, User type and Action along with core dimensions such as user properties (such as UserID), location properties (such as Client IP), and product-specific properties (such as Object Id).|
|[Sway Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#sway)|Extends the Common Schema with properties specific to all spnv.|
|[SharePoint Base Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#spbase)|Extends the Common Schema with properties specific to all SharePoint audit data.|
|[SharePoint File Operations](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#SPFileOperations)|Extends the SharePoint Base Schema with properties specific to file access and manipulation in SharePoint.|
|[SharePoint Sharing Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#SPShare)|Extends the SharePoint Base Schema with properties specific to file sharing.|
|[SharePoint Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#sp)|Extends the SharePoint Base Schema with the properties specific to SharePoint, but unrelated to file access and manipulation.|
|[Exchange Admin Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeAdminSchema)|Extends the Common Schema with the properties, specific to all Exchange admin audit data.|
|[Exchange Mailbox Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeMailboxSchema)|Extends the Common Schema with the properties, specific to all Exchange mailbox audit data.|
|[Azure Active Directory Base Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#AzureActiveDirectoryBaseSchema)|Extends the Common Schema with the properties specific to all Azure Active Directory audit data.|
|[Azure Active Directory Account Logon Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#AzureActiveDirectoryAccountLogonSchema)|Extends the Azure Active Directory Base Schema with the properties specific to all Azure Active Directory logon events.|
|[Azure Active Directory Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#AzureActiveDirectorySchema)|Extends the Common Schema with the properties specific to all Azure Active Directory audit data.|
|[Data Center Security Base Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#DataCenterSecurityBaseSchema)|Extends the Azure Active Directory Base Schema with the properties specific to all Azure Active Directory STS logon events.|
|[Data Center Security Base Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#DataCenterSecurityBaseSchema)|Extends the Common Schema with the properties specific to all data center security audit data.|
|[Data Center Security Cmdlet Schema](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#DataCenterSecurityCmdletSchema)|Extends the Data Center Security Base Schema with the properties specific to all data center security cmdlet audit data.|

## Common Schema
<a name="common"> </a>

EntityType Name: AuditRecord



|**Parameter**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|Id|Combination GUIDEdm.Guid|Yes|Unique identifier of an audit record.|
|RecordType|Self.[AuditLogRecordType](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#AuditLogRecordType)|Yes|The type of operation indicated by the record. See the [AuditLogRecordType](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#AuditLogRecordType) table for details on the types of audit log records.|
|CreationTime|Edm.Date|Yes|The date and time in Coordinated Universal Time (UTC) when the user performed the activity.|
|Operation|Edm.String|Yes|The name of the user or admin activity. For a description of the most common operations/activities, see [Search the audit log in the Office 365 Protection Center](http://go.microsoft.com/fwlink/p/?LinkId=708432). For Exchange admin activity, this property identifies the name of the cmdlet that was run.|
|OrganizationId|Edm.Guid|Yes|The GUID for your organization's Office 365 service where the event occurred. For example, an event in SharePoint event will have a different OrganizationId than an event in Exchange. The service that the event occurs in is identified by the EventSource property.|
|UserType|Self.[User Type](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#UserType)|Yes|The type of user that performed the operation. See the [User Type](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#UserType) table for details on the types of users.|
|UserKey|Edm.String|Yes|An alternative ID for the user identified in the UserId property. For example, this property is populated with the passport unique ID (PUID) for events performed by users in SharePoint, OneDrive for Business, and Exchange. This property may also specify the same value as the UserID property for events occurring in other services and events performed by system accounts.|
|Workload|Edm.String|No|The Office 365 service where the activity occurred in the Workload string. The possible values for this property are:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Exchange</p></li><li><p>SharePoint</p></li><li><p>OneDrive for Business</p></li><li><p>Azure Active Directory</p></li></ul>|
|ResultStatus|Edm.String|No|Indicates whether the action (specified in the Operation property) was successful or not. Possible values are  **Succeeded**, **PartiallySucceded**, or **Failed**. For Exchange admin activity, the value is either  **True** or **False**.|
|ObjectId|Edm.string|No|For SharePoint and OneDrive for Business activity, the full path name of the file or folder accessed by the user.For Exchange admin audit logging, the name of the object that was modified by the cmdlet.|
|UserId|Edm.string|Yes|The UPN (User Principal Name) of the user who performed the action (specified in the Operation property) that resulted in the record being logged; for example, my_name@my_domain_name. Note that records for activity performed by system accounts (such as SHAREPOINT\system or NT AUTHORITY\SYSTEM) are also included.|
|ClientIp|Edm.String|No|The IP address of the device that was used when the activity was logged. The IP address is displayed in either an IPv4 or IPv6 address format.|

### Enum: AuditLogRecordType - Type: Edm.Int32
<a name="AuditLogRecordType"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|1|ExchangeAdmin|Events from the Exchange admin audit log.|
|2|ExchangeItem|Events from an Exchange mailbox audit log for actions that are performed on a single item, such as creating or receiving an email message.|
|3|ExchangeItemGroup|Events from an Exchange mailbox audit log for actions that can be performed on multiple items, such as moving or deleted one or more email messages.|
|4|SharePoint|SharePoint events.|
|6|SharePointFileOperation|SharePoint file operation events.|
|8|AzureActiveDirectory|Azure Active Directory events.|
|9|AzureActiveDirectoryAccountLogon|Azure Active Directory OrgId logon events (deprecating).|
|10|DataCenterSecurityCmdlet|Data Center security cmdlet events.|
|11|ComplianceDLPSharePoint|Data loss protection (DLP) events in SharePoint.|
|12|Sway|Events from the Sway service and clients.|
|14|SharePointSharingOperation|SharePoint sharing events.|
|15|AzureActiveDirectoryStsLogon|Secure Token Service (STS) logon events in Azure Active Directory.|

### Enum: User Type - Type: Edm.Int32
<a name="UserType"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|0|Regular|A regular user.|
|1|Reserved|A reserved user.|
|2|Admin|An administrator.|
|3|DcAdmin|A Microsoft datacenter operator.|
|4|System|A system account.|
|5|Application|An application.|
|6|ServicePrincipal|A service principal.|

 **Note**  Only Exchange operations include a user type. SharePoint operations don't specify a user type. 


## Sway Schema
<a name="sway"> </a>

The Sway events listed in[Search the audit log in the Office 365 Protection Center](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&amp;rs=en-US&amp;ad=US) (excluding the file and folder events) use this schema.



|**Parameter**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|ObjectType|Self.ObjectType|No|The access point for the triggered event. Access points include: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>A Sway</p></li><li><p>A Sway that is embedded within a host</p></li><li><p>Sway settings within the Office 365 admin portal</p></li></ul>|
|Endpoint|Self.Endpoint|No|The Sway client endpoint for the triggered event. The Sway client endpoint can be web, iOS, Windows, or Android. |
|BrowserName|Edm.String|No|The browser used to access Sway for the triggered event. |
|DeviceType|Self.DeviceType|No|The device type used to access Sway for the triggered event. The device type can be desktop, mobile, or tablet.|
|SwayLookupId|Edm.String|No|The Sway ID. |
|SiteUrl|Edm.String|No|The URL for the Sway.|
|OperationResult|Self.OperationResult|No|Either success or fail.|


### Enum: ObjectType - Type Edm.Int32
<a name="ObjectType"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|0|Sway|The event was triggered from a Sway.|
|1|SwayEmbedded|The event was triggered from a Sway, which is embedded in a host.|
|2|SwayAdminPortal|The event was triggered from Sway service settings in Office 365 admin portal.|

### Enum: OperationResult - Type Edm.Int32
<a name="OperationResult"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|0|Succeeded|The event was successful.|
|1|Failed|The event failed.|

### Enum: Endpoint - Type Edm.Int32
<a name="Endpoint"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|0|SwayWeb|The event was triggered using the Web client of Sway.|
|1|SwayIOS|The event was triggered using the iOS client of Sway.|
|2|SwayWindows|The event was triggered using the Windows client of Sway.|
|3|SwayAndroid|The event was triggered using the Android client of Sway.|


### Enum: DeviceType - Type Edm.Int32
<a name="Devicetype"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|0|Desktop|The event was triggered using the desktop.|
|1|Mobile|The event was triggered using a mobile device.|
|2|Tablet|The event was triggered using a tablet device.|



### Enum: SwayAuditOperation - Type Edm.Int32
<a name="AuditOperation"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|1|Create|The user creates a Sway.|
|2|Delete|The user deletes a Sway.|
|3|View|The user views a Sway.|
|4|Edit|The user edits a Sway.|
|5|Duplicate|The user duplicates a Sway.|
|7|Share|The user initiates sharing a Sway. This event captures the user action of clicking on a specific share destination within the Sway share menu. The event does not indicate whether the user actually follows through and completes the share action.|
|8|ChangeShareLevel|The user changes the share level of a Sway. This event captures the user changing the scope of sharing associated with a Sway. For example, public as compared to from within the organization.|
|9|RevokeShare|The user stops sharing a Sway by revoking access. Revoking access changes the links associated with a Sway.|
|10|EnableDuplication|The user enables duplication of a Sway (on by default).|
|11|DisableDuplication|The user disables duplication of a Sway (off by default).|
|12|ServiceOn|The user enables Sway for the entire organization via the Office 365 admin center (on by default).|
|13|ServiceOff|The user disables Sway for the entire organization via the Office 365 admin center (off by default).|
|14|ExternalSharingOn|The user enables external sharing for the entire organization via the Office 365 admin center.|
|15|ExternalSharingOff|The user disables external sharing for the entire organization via the Office 365 admin center.|

## SharePoint Base Schema
<a name="spbase"> </a>



|**Parameter**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|Site|Edm.Guid|No|The GUID of the site where the file or folder accessed by the user is located.|
|ItemType|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[ItemType](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ItemType)"|No|The type of object that was accessed or modified. See the [ItemType](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ItemType) table for details on the types of objects.|
|EventSource|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[EventSource](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#EventSource)"|No|Identifies that an event occurred in SharePoint. Possible values are  **SharePoint** or **ObjectModel**.|
|SourceName|Edm.String|No|The entity that triggered the audited operation. Possible values are SharePoint or  **ObjectModel**.|
|UserAgent|Edm.String|No|Information about the user's client or browser. This information is provided by the client or browser.|
|MachineDomainInfo|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|No|Information about device sync operations. This information is reported only if it's present in the request.|
|MachineId|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|No|Information about device sync operations. This information is reported only if it's present in the request.|

### Enum: ItemType - Type: Edm.Int32
<a name="ItemType"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|0|Invalid|The item is none of the other item types (that are listed in this table).|
|1|File|The item is a file.|
|5|Folder|The item is a folder.|
|6|Web|The item is a Web page.|
|7|Site|The item is a site.|
|8|Tenant|The item is a tenant.|
|9|DocumentLibrary|The item is a document library.|

### Enum: EventSource - Type: Edm.Int32
<a name="EventSource"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|0|SharePoint|The event source is SharePoint.|
|1|ObjectModel|The event source is ObjectModel.|

### Enum: SharePointAuditOperation - Type: Edm.Int32
<a name="SharePointAuditOperations"> </a>



|**Member name**|**Description**|
|:-----|:-----|
|AccessInvitationAccepted*|The recipient of an invitation to view or edit a shared file (or folder) has accessed the shared file by clicking on the link in the invitation.|
|AccessInvitationCreated*|User sends an invitation to another person (inside or outside their organization) to view or edit a shared file or folder on a SharePoint or OneDrive for Business site. The details of the event entry identifies the name of the file that was shared, the user the invitation was sent to, and the type of the sharing permission selected by the person who sent the invitation.|
|AccessInvitationExpired*|An invitation sent to an external user expires. By default, an invitation sent to a user outside of your organization expires after 7 days if the invitation isn't accepted.|
|AccessInvitationRevoked*|The site administrator or owner of a site or document in SharePoint or OneDrive for Business withdraws an invitation that was sent to a user outside your organization. An invitation can be withdrawn only before it's accepted.|
|AccessInvitationUpdated*|The user who created and sent an invitation to another person to view or edit a shared file (or folder) on a SharePoint or OneDrive for Business site resends the invitation.|
|AccessRequestApproved|The site administrator or owner of a site or document in SharePoint or OneDrive for Business approves a user request to access the site or document.|
|AccessRequestCreated*|User requests access to a site or document in SharePoint or OneDrive for Business that they don't have permission to access. |
|AccessRequestRejected*|The site administrator or owner of a site or document in SharePoint declines a user request to access the site or document.|
|ActivationEnabled*|Users can browser-enable form templates that don't contain form code, require full trust, enable rendering on a mobile device, or use a data connection managed by a server administrator.|
|AdministratorAddedToTermStore*|Term store administrator added.|
| AdministratorDeletedFromTermStore*|Term store administrator deleted.|
|AllowGroupCreationSet*|Site administrator or owner adds a permission level to a SharePoint or OneDrive for Business site that allows a user assigned that permission to create a group for that site.|
| AppCatalogCreated*|App catalog created to make custom business apps available for your SharePoint Environment.|
|AuditPolicyRemoved*|Document LifeCycle Policy has been removed for a site collection.|
|AuditPolicyUpdate*|Document LifeCycle Policy has been updated for a site collection.|
| AzureStreamingEnabledSet*|A video portal owner has allowed video streaming from Azure.|
|CollaborationTypeModified*|The type of collaboration allowed on sites (for example, intranet, extranet, or public) has been modified.|
|CreateSSOApplication*|Target application created in Secure store service.|
|CustomizeExemptUsers*|Global administrator customized the list of exempt user agents in SharePoint admin center. You can specify which user agents to exempt from receiving an entire Web page to index. This means when a user agent you've specified as exempt encounters an InfoPath form, the form will be returned as an XML file instead of an entire Web page. This makes indexing InfoPath forms faster.|
|DefaultLanguageChangedInTermStore*|Language setting changed in the terminology store.|
|DeleteSSOApplication*|An SSO application was deleted.|
|eDiscoveryHoldApplied*|An In-Place Hold was placed on a content source. In-Place Holds are managed by using an eDiscovery site collection (such as the eDiscovery Center) in SharePoint.|
|eDiscoveryHoldRemoved*|An In-Place Hold was removed from a content source. In-Place Holds are managed by using an eDiscovery site collection (such as the eDiscovery Center) in SharePoint.|
|eDiscoverySearchPerformed*|An eDiscovery search was performed using an eDiscovery site collection in SharePoint.|
|ExemptUserAgentSet*|Global administrator adds a user agent to the list of exempt user agents in the SharePoint admin center.|
|FileAccessed|User or system account accesses a file on a SharePoint or OneDrive for Business site. System accounts can also generate FileAccessed events.|
|FileCheckOutDiscarded*|User discards (or undos) a checked out file. That means any changes they made to the file when it was checked out are discarded, and not saved to the version of the document in the document library.|
|FileCheckedIn*|User checks in a document that they checked out from a SharePoint or OneDrive for Business document library.|
|FileCheckedOut*|User checks out a document located in a SharePoint or OneDrive for Business document library. Users can check out and make changes to documents that have been shared with them.|
|FileCopied|User copies a document from a SharePoint or OneDrive for Business site. The copied file can be saved to another folder on the site.|
|FileDeleted|User deletes a document from a SharePoint or OneDrive for Business site.|
|FileDownloaded|User downloads a document from a SharePoint or OneDrive for Business site.|
|FileFetched|This event has been replaced by the FileAccessed event, and has been deprecated.|
|FileModified|User or system account modifies the content or the properties of a document located on a SharePoint or OneDrive for Business site.|
|FileMoved|User moves a document from its current location on a SharePoint or OneDrive for Business site to a new location..|
|FileRenamed|User renames a document on a SharePoint or OneDrive for Business site.|
|FileRestored|User restores a document from the recycle bin of a SharePoint or OneDrive for Business site. |
|FileSyncDownloadedFull|User establishes a sync relationship and successfully downloads files for the first time to their computer from a SharePoint or OneDrive for Business document library.|
|FileSyncDownloadedPartial|User successfully downloads any changes to files from SharePoint or OneDrive for Business document library. This event indicates that any changes that were made to files in the document library were downloaded to the user's computer. Only changes were downloaded because the document library was previously downloaded by the user (as indicated by the FileSyncDownloadedFull event).|
|FileSyncUploadedFull*|User establishes a sync relationship and successfully uploads files for the first time from their computer to a SharePoint or OneDrive for Business document library.|
|FileSyncUploadedPartial*|User successfully uploads changes to files on a SharePoint or OneDrive for Business document library. This event indicates that any changes made to the local version of a file from a document library are successfully uploaded to the document library. Only changes are unloaded because those files were previously uploaded by the user (as indicated by the FileSyncUploadedFull event).|
|FileUploaded|User uploads a document to a folder on a SharePoint or OneDrive for Business site. |
|FileViewed|This event has been replaced by the FileAccessed event, and has been deprecated.|
|GroupAdded*|Site administrator or owner creates a group for a SharePoint or OneDrive for Business site, or performs a task that results in a group being created. For example, the first time a user creates a link to share a file, a system group is added to the user's OneDrive for Business site. This event can also be a result of a user creating a link with edit permissions to a shared file.|
|GroupRemoved*|User deletes a group from a SharePoint or OneDrive for Business site. |
|GroupUpdated*|Site administrator or owner changes the settings of a group for a SharePoint or OneDrive for Business site. This can include changing the group's name, who can view or edit the group membership, and how membership requests are handled.|
|LanguageAddedToTermStore*|Language added to the terminology store.|
|LanguageRemovedFromTermStore*|Language removed from the terminology store.|
|LegacyWorkflowEnabledSet*|Site administrator or owner adds theSharePoint Workflow Task content type to the site. Global administrators can also enable work flows for the entire organization in theSharePoint admin center.|
|ManagedSyncClientAllowed|User successfully establishes a sync relationship with a SharePoint or OneDrive for Business site. The sync relationship is successful because the user's computer is a member of a domain that's been added to the list of domains (called the safe recipients list) that can access document libraries in your organization.For more information about this feature, see [Use Windows PowerShell cmdlets to enable OneDrive sync for domains that are on the safe recipients list](http://go.microsoft.com/fwlink/p/?LinkID=534609).|
|MaxQuotaModified*|The maximum quota for a site has been modified.|
|MaxResourceUsageModified*|The maximum allowable resource usage for a site has been modified.|
|MySitePublicEnabledSet*|The flag enabling users to have public MySites has been set by the SharePoint administrator.|
|NewsFeedEnabledSet*|Site administrator or owner enables RSS feeds for a SharePoint or OneDrive for Business site. Global administrators can enable RSS feeds for the entire organization in the SharePoint admin center.|
|ODBNextUXSettings*|New UI for OneDrive for Business has been enabled.|
|OfficeOnDemandSet*|Site administrator enables Office on Demand, which lets users access the latest version of Office desktop applications. Office on Demand is enabled in the SharePoint admin center and requires an Office 365 subscription that includes full, installed Office applications.|
|PeopleResultsScopeSet*|Site administrator creates or changes the result source for People Searches for a SharePoint site.|
|PreviewModeEnabledSet*|Site administrator enables document preview for a SharePoint site.|
|QuotaWarningEnabledModified*|Storage quota warning modified.|
|RenderingEnabled*|Browser-enabled form templates will be rendered by InfoPath forms services.|
|ResourceWarningEnabledModified*|Resource quota warning modified.|
|SSOGroupCredentialsSet*|Group credentials set in Secure store service.|
|SSOUserCredentialsSet*|User credentials set in Secure store service.|
|SearchCenterUrlSet*|Search center URL set.|
|SecondaryMySiteOwnerSet*|A user has added a secondary owner to their MySite.|
|SendToConnectionAdded*|Global administrator creates a new Send To connection on the Records management page in the SharePoint admin center. A Send To connection specifies settings for a document repository or a records center. When you create a Send To connection, a Content Organizer can submit documents to the specified location.|
|SendToConnectionRemoved*|Global administrator deletes a Send To connection on the Records management page in the SharePoint admin center.|
|SharedLinkCreated|User creates a link to a shared file in SharePoint or OneDrive for Business. This link can be sent to other people to give them access to the file. A user can create two types of links: a link that allows a user to view and edit the shared file, or a link that allows the user to just view the file.|
|SharedLinkDisabled*|User disables (permanently) a link that was created to share a file.|
|SharingRevoked*|User unshares a file or folder that was previously shared with other users. This event is logged when a user stops sharing a file with other users.|
|SharingSet|User shares a file or folder located in SharePoint or OneDrive for Business with another user inside their organization.|
|SiteAdminChangeRequest*|User requests to be added as a site collection administrator for a SharePoint site collection. Site collection administrators have full control permissions for the site collection and all subsites.|
|SiteCollectionAdminAdded*|Site collection administrator or owner adds a person as a site collection administrator for a SharePoint or OneDrive for Business site. Site collection administrators have full control permissions for the site collection and all subsites.|
|SiteCollectionCreated*| Global administrator creates a new site collection in your SharePoint organization.|
|SitePermissionsModified*|Site administrator or owner (or system account) changes the permission level that are assigned to a group on a SharePoint or OneDrive for Business site. This event is also logged if all permissions are removed from a group.|
|SiteRenamed*|Site administrator or owner renames a SharePoint or OneDrive for Business site|
|SyncGetChanges*|User clicks  **Sync** in the action tray on in SharePoint or OneDrive for Business to synchronize any changes to file in a document library to their computer.|
|UnmanagedSyncClientBlocked|User tries to establish a sync relationship with a SharePoint or OneDrive for Business site from a computer that isn't a member of your organization's domain or is a member of a domain that hasn't been added to the list of domains (called the safe recipients list) that can access document libraries in your organization. The sync relationship is not allowed, and the user's computer is blocked from syncing, downloading, or uploading files on a document library.For information about this feature, see [Use Windows PowerShell cmdlets to enable OneDrive sync for domains that are on the safe recipients list](http://go.microsoft.com/fwlink/p/?LinkID=534609).|
|UpdateSSOApplication*|Target application updated in Secure store service.|
|UserAddedToGroup*|Site administrator or owner adds a person to a group on a SharePoint or OneDrive for Business site. Adding a person to a group grants the user the permissions that were assigned to the group. |
|UserRemovedFromGroup*|Site administrator or owner removes a person from a group on a SharePoint or OneDrive for Business site. After the person is removed, they no longer are granted the permissions that were assigned to the group. |

 **Note**  * This operation is in Preview.


## SharePoint File Operations
<a name="SPFileOperations"> </a>

The file-related SharePoint events listed in the "File and folder activities" section in [Search the audit log in the Office 365 Protection Center](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&amp;rs=en-US&amp;ad=US) use this schema.



|**Parameter**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|SiteUrl|Edm.String|Yes|The URL of the site where the file or folder accessed by the user is located.|
|SourceRelativeUrl|Edm.String|No|The URL of the folder that contains the file accessed by the user. The combination of the values for the  _SiteURL_,  _SourceRelativeURL_, and  _SourceFileName_ parameters is the same as the value for the **ObjectID** property, which is the full path name for the file accessed by the user.|
|SourceFileName|Edm.String|Yes|The name of the file or folder accessed by the user.|
|SourceFileExtension|Edm.String|No|The file extension of the file that was accessed by the user. This property is blank if the object that was accessed is a folder.|
|DestinationRelativeUrl|Edm.String|No|The URL of the destination folder where a file is copied or moved. The combination of the values for  _SiteURL_,  _DestinationRelativeURL_, and  _DestinationFileName_ parameters is the same as the value for the **ObjectID** property, which is the full path name for the file that was copied. This property is displayed only for FileCopied and FileMoved events.|
|DestinationFileName|Edm.String|No|The name of the file that is copied or moved. This property is displayed only for FileCopied and FileMoved events.|
|DestinationFileExtension|Edm.String|No|The file extension of a file that is copied or moved. This property is displayed only for FileCopied and FileMoved events.|
|UserSharedWith|Edm.String|No|The user that a resource was shared with.|
|SharingType|Edm.String|No|The type of sharing permissions that were assigned to the user that the resource was shared with. This user is identified by the  _UserSharedWith_ parameter.|


## SharePoint Sharing Schema
<a name="SPShare"> </a>

 The file share-related SharePoint events. They are different from file- and folder-related events in that a user is taking an action that has some effect on another user. For information about the SharePoint Sharing Schema, see[Use sharing auditing in the Office 365 audit log](https://support.office.com/en-us/article/Use-sharing-auditing-in-the-Office-365-audit-log-50bbf89f-7870-4c2a-ae14-42635e0cfc01?ui=en-US&amp;rs=en-US&amp;ad=US).



|**Parameter**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|||||
|||||
|TargetUserOrGroupName |Edm.String|No|Stores the UPN or name of the target user or group that a resource was shared with.|
|TargetUserOrGroupType|Edm.String|No|Identifies whether the target user or group is a Member, Guest, Group, or Partner. |
|EventData|XML code|No|Conveys follow-up information about the sharing action that has occurred, such as adding a user to a group or granting edit permissions.|

## SharePoint Schema
<a name="sp"> </a>

The SharePoint events listed in t[Search the audit log in the Office 365 Protection Center](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&amp;rs=en-US&amp;ad=US) (excluding the file and folder events) use this schema.



|**Parameter**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|CustomEvent|Edm.String|No|Optional string for custom events.|
|EventData|Edm.String|No|Optional payload for custom events.|
|ModifiedProperties|Collection(ModifiedProperty)|No|The property is included for admin events, such as adding a user as a member of a site or a site collection admin group. The property includes the name of the property that was modified (for example, the Site Admin group), the new value of the modified property (such the user who was added as a site admin), and the previous value of the modified object.|

## Exchange Admin Schema
<a name="ExchangeAdminSchema"> </a>



|**Parameters**|**Type**|**Mandatory**|**Description**|
|:-----|:-----|:-----|:-----|
|ModifiedObjectResolvedName|Edm.String|No|This is the user friendly name of the object that was modified by the cmdlet. This is logged only if the cmdlet modifies the object.|
|Parameters|Collection(Common.NameValuePair)|No|The name and value for all parameters that were used with the cmdlet that is identified in the Operations property.|
|ModifiedProperties|Collection(Common.ModifiedProperty)|No|The property is included for admin events. The property includes the name of the property that was modified, the new value of the modified property, and the previous value of the modified object.|
|ExternalAccess|Edm.Boolean|Yes|Specifies whether the cmdlet was run by a user in your organization, by Microsoft datacenter personnel or a datacenter service account, or by a delegated administrator. The value  **False** indicates that the cmdlet was run by someone in your organization. The value **True** indicates that the cmdlet was run by datacenter personnel, a datacenter service account, or a delegated administrator.|
|OriginatingServer|Edm.String|No|The name of the server from which the cmdlet was executed.|
|OrganizationName|Edm.String|No|The name of the tenant.|


## Exchange Mailbox Schema
<a name="ExchangeMailboxSchema"> </a>



|**Parameters**|**Type**|**Mandatory**|**Description**|
|:-----|:-----|:-----|:-----|
|LogonType|Self.[LogonType](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeLogonType)|No| Indicates the type of user who accessed the mailbox and performed the operation that was logged.|
|InternalLogonType|Self.[LogonType](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeLogonType)|No|Reserved for internal use.|
|MailboxGuid|Edm.String|No|The Exchange GUID of the mailbox that was accessed.|
|MailboxOwnerUPN|Edm.String|No|The email address of the person who owns the mailbox that was accessed.|
|MailboxOwnerSid|Edm.String|No|The SID of the mailbox owner.|
|MailboxOwnerMasterAccountSid|Edm.String|No|Mailbox owner account's master account SID.|
|LogonUserSid|Edm.String|No|The SID of the user who performed the operation.|
|LogonUserDisplayName|Edm.String|No|The user-friendly name of the user who performed the operation.|
|ExternalAccess|Edm.Boolean|Yes|This is true if the logon user's domain is different from the mailbox owner's domain.|
|OriginatingServer |Edm.String|No|This is from where the operation originated.|
|OrganizationName|Edm.String|No|The name of the tenant.|
|ClientInfoString|Edm.String|No|Information about the email client that was used to perform the operation, such as a browser version, Outlook version, and mobile device information.|
|ClientIPAddress|Edm.String|No|The IP address of the device that was used when the operation was logged. The IP address is displayed in either an IPv4 or IPv6 address format.|
|ClientMachineName|Edm.String|No|The machine name that hosts the Outlook client.|
|ClientProcessName|Edm.String|No|The email client that was used to access the mailbox. |
|ClientVersion|Edm.String|No|The version of the email client .|


### Enum: LogonType - Type: Edm.Int32
<a name="ExchangeLogonType"> </a>



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|0|Owner|The mailbox owner.|
|1|Admin|A person with administrative privileges for someone's mailbox.|
|2|Delegated|A person with the delegate privileges for someone's mailbox.|
|3|Transport|A transport service in the Microsoft datacenter.|
|4|SystemService|A service account in the Microsoft datacenter|
|5|BestAccess|Reserved for internal use.|
|6|DelegatedAdmin|A delegated administrator.|


### ExchangeMailboxAuditGroupRecord schema
<a name="ExchangeLogonType"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|Folder|Self.[ExchangeFolder](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeFolderType)|No|The folder where a group of items is located.|
|CrossMailboxOperations|Edm.Boolean|No|Indicates if the operation involved more than one mailbox.|
|DestMailboxId|Edm.Guid|No|Set only if the CrossMailboxOperations parameter is  **True**. Specifies the target mailbox GUID.|
|DestMailboxOwnerUPN|Edm.String|No|Set only if the CrossMailboxOperations parameter is  **True**. Specifies the UPN of the owner of the target mailbox.|
|DestMailboxOwnerSid|Edm.String|No|Set only if the CrossMailboxOperations parameter is  **True**. Specifies the SID of the target mailbox.|
|DestMailboxOwnerMasterAccountSid|Edm.String|No|Set only if the CrossMailboxOperations parameter is  **True**. Specifies the SID for the master account SID of the target mailbox owner.|
|DestFolder|Self.[ExchangeFolder](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeFolderType)|No|The destination folder, for operations such as Move.|
|Folders|Collection(Self.[ExchangeFolder](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeFolderType))|No|Information about the source folders involved in an operation; for example, if folders are selected and then deleted.|
|AffectedItems|Collection(Self.[ExchangeItem](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeItemType))|No|Information about each item in the group.|


### ExchangeMailboxAuditRecord schema
<a name="ExchangeLogonType"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|Item|Self.[ExchangeItem](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeItemType)|No|Represents the item upon which the operation was performed|
|ModifiedProperties|Collection(Edm.String)|No|TBD|
|SendAsUserSmtp|Edm.String|No|SMTP address of the user who is being impersonated.|
|SendAsUserMailboxGuid|Edm.Guid|No|The Exchange GUID of the mailbox that was accessed to send email as.|
|SendOnBehalfOfUserSmtp|Edm.String|No|SMTP address of the user on whose behalf the email is sent.|
|SendonBehalfOfUserMailboxGuid|Edm.Guid|No|The Exchange GUID of the mailbox that was accessed to send mail on behalf of.|


### ExchangeItem complex type
<a name="ExchangeItemType"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|Id|Edm.String|Yes|The store ID.|
|Subject|Edm.String|No|The subject line of the message that was accessed.|
|ParentFolder|Edm.[ExchangeFolder](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#ExchangeFolderType)|No|The name of the folder where the item is located.|
|Attachments|Edm.String|No|A list of the names and file size of all items that are attached to the message.|

### ExchangeFolder complex type
<a name="ExchangeFolderType"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|Id|Edm.String|Yes|The store ID of the folder object.|
|Path|Edm.String|No|The name of the mailbox folder where the message that was accessed is located.|


## Azure Active Directory Base Schema
<a name="AzureActiveDirectoryBaseSchema"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|AzureActiveDirectoryEventType|Self.[AzureActiveDirectoryEventType](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#AADEventType)|Yes|The type of Azure AD event. |
|ExtendedProperties|Collection(Common.NameValuePair)|No|The extended properties of the Azure AD event.|
|ModifiedProperties|Collection(Common.ModifiedProperty)|No|This property is included for admin events. The property includes the name of the property that was modified, the new value of the modified property, and the previous value of the modified property.|

### Enum: AzureActiveDirectoryEventType - Type -Edm.Int32
<a name="AADEventType"> </a>



|**Member name**|**Description**|
|:-----|:-----|
|AccountLogon|The account login event.|
|AzureApplicationAuditEvent|The Azure application security event.|

## Azure Active Directory Account Logon Schema
<a name="AzureActiveDirectoryAccountLogonSchema"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|Application|Edm.String|No|The application that triggers the account login event, such as Office 15.|
|Client|Edm.String|No|Details about the client device, device OS, and device browser that was used for the of the account login event.|
|LoginStatus|Edm.Int32|Yes|This property is from OrgIdLogon.LoginStatus directly. The mapping of various interesting logon failures could be done by alerting algorithms.|
|UserDomain|Edm.String|Yes|The Tenant Identity Information (TII).|


### Enum: CredentialType - Type: Edm.Int32



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|-1|Other|Other authentication.|
|0|Password|User credential is username and password.|
|1|MobilePhone|User credential is mobile phone.|
|2|SecretQuestion|User credential is secret question.|
|3|SecurePin|User credential is secure PIN.|
|4|SecurePinReset|User credential is secure PIN reset.|
|11|EasyID|User credential is EasyID.|
|14|PasswordIndexCredentialType|User credential is PasswordIndexCredentialType.|
|16|Device|User credential is a device.|
|17|ForeignRealmIndex|User credential is ForeignRealmIndex.|

### Enum: LoginType - Type: Edm.Int32



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|-1|Other|Other i type.|
|1|InitialAuth|Login with initial authentication|
|2|CookieCopy|Login with cookie.|
|3|SilentReAuth|Login with silent re-authentication.|


### Enum: AuthenticationMethod - Type: Edm.Int32



|**Value**|**Member name**|**Description**|
|:-----|:-----|:-----|
|0|Min|The authentication method is a Min|
|1|Password|The authentication method is a password.|
|2|Digest|The authentication method is a digest.|
|3|ProxyAuth|The authentication method is a ProxyAuth.|
|4|InfoCard|The authentication method is an InfoCard|
|5|DAToken|The authentication method is a DAToken.|
|6|Sha1RememberMyPassword|The authentication method is a Sha1RememberMyPassword.|
|7|LMPasswordHash|The authentication method is an LMPasswordHash.|
|8|ADFSFederatedToken|The authentication method is an ADFSFederatedToken.|
|9|EID|The authentication method is an EID.|
|10|DeviceID|The authentication method is a DeviceID. |
|11|MD5|The authentication method is MD5.|
|12|EncProxyPasswordHash|The authentication method is a EncProxyPasswordHash.|
|13|LWAFederation|The authentication method is a LWAFederation.|
|14|Sha1HashedPassword|The authentication method is a Sha1HashedPassword.|
|15|SecurePin|The authentication method is a secure Pin.|
|16|SecurePinReset|The authentication method is a secure PIN reset.|
|17|SAML20PostSimpleSign|The authentication method is a SAML20PostSimpleSign.|
|18|SAML20Post|The authentication method is a SAML20Post.|
|19|OneTimeCode|The authentication method is a one-time code.|


## Azure Active Directory Schema
<a name="AzureActiveDirectorySchema"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|Actor|Collection(Self.[IdentityTypeValuePair](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#IdentityTypeValuePair))|No|The user or service principal that performed the action.|
|ActorContextId|Edm.String|No|The GUID of the organization that the actor belongs to.|
|ActorIpAddress|Edm.String|No|The actor's IP address in IPV4 or IPV6 address format.|
|InterSystemsId|Edm.String|No|The GUID that track the actions across components within the Office 365 service.|
|IntraSystemsId|Edm.String|No|The GUID that's generated by Azure Active Directory to track the action.|
|SupportTicketId|Edm.String|No|The customer support ticket ID for the action in "act-on-behalf-of" situations.|
|Target|Collection(Self.[IdentityTypeValuePair](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#IdentityTypeValuePair))|No|The user that the action (identified by the Operation property) was performed on.|
|TargetContextId|Edm.String|No|The GUID of the organization that the targeted user belongs to.|



### Complex Type: IdentityTypeValuePair
<a name="IdentityTypeValuePair"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|ID|Edm.String|Yes|The value of the identity given the type.|
|Type|Self.[IdentityType](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#IdentityType)|Yes|The type of the identity.|

### Enum: IdentityType - Type: Edm.Int32
<a name="IdentityType"> </a>



|**Member name**|**Description**|
|:-----|:-----|
|Claim|The identity is a claim for authorization purpose.|
|Name|The audit action actor or target identity display name.|
|Other|The identity of the actor is other type, such as the ObjectId in GUID generated by the Office 365 service.|
|PUID|The audit action actor or the target passport unique ID (PUID).|
|SPN|The identity of a service principal if the action is performed by the Office 365 service.|
|UPN|The user principal name.|


## Azure Active Directory STS Logon Schema
<a name="AzureActiveDirectorySTSSchema"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|ApplicationId|Edm.String|No|The GUID that represents the application that is requesting the login. The display name can be looked up via the Azure Active Directory Graph API.|
|Client|Edm.String|No|Client device information, provided by the browser performing the login.|
|LogonError|Edm.String|No|For failed logins, contains the reason why the login failed.|


## Data Center Security Base Schema
<a name="DataCenterSecurityBaseSchema"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|DataCenterSecurityEventType|Self.[DataCenterSecurityEventType ](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#DataCenterSecurityEventType)|Yes|The type of dmdlet event in lock box.|

### Enum: DataCenterSecurityEventType - Type: Edm.Int32
<a name="DataCenterSecurityEventType"> </a>



|**Member name**|**Description**|
|:-----|:-----|
|DataCenterSecurityCmdletAuditEvent|This is the enum value for cmdlet audit type event.|


## Data Center Security Cmdlet Schema
<a name="DataCenterSecurityCmdletSchema"> </a>



|**Parameters**|**Type**|**Mandatory?**|**Description**|
|:-----|:-----|:-----|:-----|
|StartTime|Edm.Date|Yes|The start time of the cmdlet execution.|
|EffectiveOrganization|Edm.String|Yes|The name of the tenant that the elevation/cmdlet was targeted at.|
|ElevationTime|Edm.Date|Yes|The start time of the elevation.|
|ElevationApprover|Edm.String|Yes|The name of a Microsoft manager.|
|ElevationApprovedTime|Edm.Date|No|The timestamp for when the elevation was approved.|
|ElevationRequestId|Edm.Guid|Yes|A unique identifier for the elevation request.|
|ElevationRole|Edm.String|No|The role the elevation was requested for.|
|ElevationDuration|Edm.Int32|Yes|The duration for which the elevation was active.|
|GenericInfo|Edm.String|No|Used for comments and other generic information.|
[Return to top](75c668bf-d9aa-4cc1-8b51-ed7dbc2314bf.md#top)

