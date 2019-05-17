---
ms.TocTitle: Office 365 Service Communications API reference (Preview)
title: Office 365-Dienstkommunikations-API – Referenz (Vorschau)
description: Verwenden Sie diese API, um Zugriff auf die folgenden Daten zu erhalten – Get Services, Get Current Status, Get Historical Status und Get Messages.
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 728cf632baa1f4a45b626677b1da862438562d90
ms.sourcegitcommit: 490310e2718a7f9d827c945a78e940d936d15386
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2019
ms.locfileid: "34102311"
---
# <a name="office-365-service-communications-api-reference-preview"></a>Office 365-Dienstkommunikations-API – Referenz (Vorschau)

> [!NOTE] 
> Diese Dokumentation umfasst Features, die sich aktuell in der Vorschau befinden.

Sie können die Office 365-Dienstkommunikations-API V2 verwenden, um Zugriff auf die folgenden Daten zu erhalten:

- **Get Services**: Erhalt der Liste der abonnierten Dienste.
    
- **Get Current Status**: Erhalt einer Echtzeitansicht der aktuellen und laufenden Dienstincidents und Wartungsereignisse
    
- **Get Historical Status**: Erhalt einer historischen Ansicht der Dienstintegrität, einschließlich Dienstincidents und Wartungsereignisse.
    
- **Get Messages**: Suche nach Kommunikation zu Incidents, geplanter Wartung und Nachrichtencenter.
    
Aktuell umfasst die Office 365-Dienstkommunikations-API Daten für die folgenden Dienste: Dynamics CRM, Dynamics Marketing, Exchange Online, Exchange Online Protection, Identity Service, Mobile Device Management, Office 365 Partner Admin Center, OneDrive for Business, Parature, OneDrive for Business, Power BI for Office 365, Rights Management Service, SharePoint Online, SHD Admin, Skype for Business, Social Engagement und Yammer Enterprise.

## <a name="the-fundamentals"></a>Die Grundlagen

Die Stamm-URL der API enthält einen Mandantenbezeichner, der die Operationen einem einzigen Mandanten zuordnet:

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

Die **Office 365 Dienstkommunikations-API** ist ein REST-Dienst, mit dem Sie Lösungen mit einer beliebigen Websprache und Hosting-Umgebung entwickeln können, die HTTPS- und X.509-Zertifikate unterstützt. Die API basiert auf **Microsoft Azure Active Directory** und dem **OAuth2**-Protokoll für Authentifizierung und Autorisierung. Um von Ihrer Anwendung aus auf die API zugreifen zu können, müssen Sie diese zuerst in Azure AD registrieren und dann mit Berechtigungen im entsprechenden Bereich konfigurieren. Dadurch kann die Anwendung OAuth2-Zugriffstoken anfordern, die für das Aufrufen der API erforderlich sind. Weitere Informationen über das Registrieren und Konfigurieren einer Anwendung in Azure AD finden Sie unter [Office 365-Verwaltungs-APIs – erste Schritte](get-started-with-office-365-management-apis.md).

Alle API-Anforderungen erfordern einen HTTP-Header für die Autorisierung mit einem gültigen OAuth2-JWT-Zugriffstoken von Azure AD, das den **ServiceHealth.Read**-Anspruchenthält; der Mandantenbezeichner muss dem Mandantenbezeichner in der Stamm-URL entsprechen.

```json
Authorization: Bearer {OAuth2 token}
```

**Anforderungsheader**

Dies sind die unterstützten Anforderungsheader für alle Office 365-Dienstkommunikations-API-Operationen.

|Header|Beschreibung|
|:-----|:-----|
|**Annehmen (Optional)**|Im Folgenden finden Sie die zulässigen Darstellungen für die Antwort:<br/>**application/json;odata.metadata=full**<br/>**application/json;odata.metadata=minimal**<br/>[Standard, wenn kein Header angegeben] **application/json;odata.metadata=none**|
|**Autorisierung (erforderlich)**|Autorisierungstoken (Bearer JWT Azure AD Token) für die Anforderung.|


<br/>

**Antwortheader**

Dies sind die Antwortheader für alle Office 365-Dienstkommunikations-API-Operationen:

|Header|Beschreibung|
|:-----|:-----|
|**Content-Length**|Die Länge des Antworttextes.|
|**Content-Type**|Darstellung der Antwort:<br/>**application/json**<br/>**application/json;odata.metadata=full**<br/>**application/json;odata.metadata=minimal**<br/>**application/json;odata.metadata=none**<br/>**odata.streaming=true**|
|**Cache-Control**|Wird verwendet, um Direktiven anzugeben, die alle Caching-Mechanismen in der Anforderungs-/Antwortkette einhalten müssen.|
|**Pragma**|Implementierungsspezifische Verhaltensweisen.|
|**Expires**|Wenn der Client dafür sorgen soll, dass die Ressource abläuft.|
|**X-Activity-Id**|Die vom Server generierte Aktivitäts-ID.|
|**OData-Version**|Die unterstützte OData-Version (4.0).|
|**Date**|Das Datum in UTC, als die Antwort vom Server gesendet wurde.|
|**X-Time-Taken**|Die Zeit zum Generieren der Antwort (ms).|
|**X-Instance-Name**|Der Bezeichner für die Azure-Instanz, um die Antwort zu generieren (für Debugging-Zwecke).|
|**Server**|Der Server, um die Antwort zu generieren (für Debugging-Zwecke).|
|**X-ASPNET-Version**|Die Version von ASP.Net, die vom Server verwendet wird, der die Antwort generiert hat (für Debugging-Zwecke).|
|**X-Powered-By**|Die Technologien, die vom Server verwendet werden, der die Antwort generiert hat (für Debugging-Zwecke).|

<br/>

Im Folgenden sind die Operationen der Office 365-Dienstkommunikations-API aufgelistet.


## <a name="get-services"></a>Get Services

Gibt die Liste der abonnierten Dienste zurück.

||Dienst|Beschreibung|
|:-----|:-----|:-----|
|**Path**| `/Services`||
|**Query-option**|$select|Wählen Sie eine Teilmenge der Eigenschaften.|
|**Response**|Liste der „Service“-Entitäten|„Service"-Entität enthält „Id“ (Zeichenfolge), „DisplayName“ (Zeichenfolge) und „FeatureNames“ (Liste mit Zeichenfolgen).|

#### <a name="sample-request"></a>Beispielanfrage

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

#### <a name="sample-response"></a>Beispielantwort

```json
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


## <a name="get-current-status"></a>Get Current Status

Gibt den Status des Diensts in den vorherigen 24 Stunden zurück.

> [!NOTE] 
> Der Status in der Dienstantwort bezieht sich auf den Zeitpunkt 24 Stunden nach der Anforderung. Der zurückgegebene StatusDate- oder StatusTime-Wert liegt genau 24 Stunden in der Vergangenheit. 

||Dienst|Beschreibung|
|:-----|:-----|:-----|
|**Path**| `/CurrentStatus`||
|**Filter**|Arbeitslast|Filtern nach Arbeitslast (Zeichenfolge, Standard: alle).|
|**Query-option**|$select|Wählen Sie eine Teilmenge der Eigenschaften.|
|**Response**|Liste der „WorkloadStatus“-Entitäten.|„WorkloadStatus“-Entität enthält „Id“ (Zeichenfolge), „Workload“ (Zeichenfolge), „StatusTime“ (DateTimeOffset), „WorkloadDisplayName“ (Zeichenfolge), „Status“ (Zeichenfolge), „IncidentIds“ (Liste mit Zeichenfolgen) und „FeatureGroupStatusCollection“ (Liste mit „FeatureStatus“).<br/><br/>„FeatureStatus“-Entität enthält „Feature“ (Zeichenfolge), „FeatureGroupDisplayName“ (Zeichenfolge) und „FeatureStatus“ (Zeichenfolge).|

#### <a name="sample-request"></a>Beispielanfrage

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a>Beispielantwort

```json
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


## <a name="get-historical-status"></a>Get Historical Status

Gibt den Verlaufsstatus des Dienstes nach Tag über einen bestimmten Zeitraum zurück.

||Dienst|Beschreibung|
|:-----|:-----|:-----|
|**Path**| `/HistoricalStatus`||
|**Filters**|Arbeitslast|Filtern nach Arbeitslast (Zeichenfolge, Standard: alle).|
||StatusTime|Filtern Sie nach Tagen größer als StatusTime (DateTimeOffset, Standard: ge CurrentTime - 7 Tage).|
|**Query-option**|$select|Wählen Sie eine Teilmenge der Eigenschaften.|
|**Response**|Liste der „WorkloadStatus“-Entitäten.|„WorkloadStatus“-Entität enthält „Id“ (Zeichenfolge), „Workload“ (Zeichenfolge), „StatusTime“ (DateTimeOffset), „WorkloadDisplayName“ (Zeichenfolge), „Status“ (Zeichenfolge), „IncidentIds“ (Liste mit Zeichenfolgen) und „FeatureGroupStatusCollection“ (Liste mit „FeatureStatus“).<br/><br/>„FeatureStatus“-Entität enthält „Feature“ (Zeichenfolge), „FeatureGroupDisplayName“ (Zeichenfolge) und „FeatureStatus“ (Zeichenfolge).|

#### <a name="sample-request"></a>Beispielanfrage

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a>Beispielantwort

```json
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


## <a name="get-messages"></a>Get Messages

Gibt Nachrichten über den Dienst über einen bestimmten Zeitraum zurück. Verwenden Sie den Typfilter zum Filtern nach Nachrichten des Typs „Dienstincident“, „Geplante Wartung“ oder „Nachrichtencenter“.

||Dienst|Beschreibung|
|:-----|:-----|:-----|
|**Path**| `/Messages`||
|**Filters**|Arbeitslast|Filtern nach Arbeitslast (Zeichenfolge, Standard: alle).|
||StartTime|Filter Sie nach Startzeit (DateTimeOffset, Standard: ge CurrentTime - 7 Tage).|
||EndTime|Filter Sie nach Endzeit (DateTimeOffset, Standard: le CurrentTime).|
||MessageType|Filtern Sie nach MessageType (Zeichenfolge, Standard: alle).|
||ID|Filtern Sie nach ID (Zeichenfolge, Standard: alle).|
|**Query-option**|$select|Wählen Sie eine Teilmenge der Eigenschaften.|
||$top|Wählen Sie die wichtigsten Ergebnisse (default und max $top=100).|
||$skip|Überspringen Sie die Anzahl der Ergebnisse (Standard: $skip=0).|
|**Response**|Liste der „Message“-Entitäten.|Die „Message“-Entität enthält „Id“ (Zeichenfolge), „StartTime“ (DateTimeOffset), „EndTime“ (DateTimeOffset), „Status“ (Zeichenfolge), "Messages" (Liste mit „MessageHistory“-Entität), „LastUpdatedTime“ (DateTimeOffset), „Workload“ (String), „WorkloadDisplayName“ (String), „Feature“ (String), „FeatureDisplayName“ (String), „MessageType“ (Enum, Standard: alle).<br/><br/>„MessageHistory“-Entität enthält „PublishedTime“ (DateTimeOffset), „MessageText“ (Zeichenfolge).|

#### <a name="sample-request"></a>Beispielanfrage

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a>Beispielantwort

```json
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


## <a name="errors"></a>Fehler

Wenn der Dienst einen Fehler feststellt, meldet er den Fehlerantwortcode an den Aufrufer, mithilfe der standardmäßigen HTTP-Fehlercodesyntax. Gemäß der [OData V4-Spezifikation](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html) sind zusätzliche Informationen im Text des fehlgeschlagenen Aufrufs als einzelnes JSON-Objekt enthalten. Nachfolgend finden Sie ein Beispiel für einen vollständigen JSON-Fehlertext:


```json

{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}

```

