---
ms.technology: o365-service-communications
ms.TocTitle: Troubleshooting the Office 365 Management Activity API
title: Problembehandlung bei der Office 365-Verwaltungsaktivitäts-API
description: Enthält eine Zusammenfassung der am häufigsten gestellten Fragen, die der Microsoft-Support zu dieser API erhält.
ms.ContentId: 50822603-a1ec-a754-e7dc-67afe36bb1b0
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: a5661cd1650ac6412bf6723a5ffc27c3a81c11b1
ms.sourcegitcommit: e7f345710dc63003704399419f784c4a9b5fc529
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/02/2020
ms.locfileid: "48830476"
---
# <a name="office-365-management-activity-api-faqs-and-troubleshooting"></a>Häufig gestellte Fragen und Problembehandlung der Office 365-Verwaltungsaktivitäts-API

Die Office 365-Verwaltungsaktivitäts-API (auch bekannt als *einheitliche Überwachungs-API* ) ist Teil der Office 365-Sicherheits- und Complianceangebote, die:

- Ermöglicht den programmgesteuerten Zugriff auf mehrere Überwachungspipeline-Arbeitslasten (wie SharePoint und Exchange)

- Ist die wichtigste Schnittstelle, die von einer Vielzahl von Drittanbieterprodukten zum Aggregieren und Indexieren von Überwachungsdaten verwendet wird

Die Verwaltungsaktivitäts-API sollte nicht mit der Office 365-Dienstkommunikations-API verwechselt werden. Die Verwaltungsaktivitäts-API ist für die Überwachung der Endbenutzeraktivitäten in den verschiedenen Arbeitslasten gedacht. Die Dienstkommunikations-API ist für die Überwachung von Status und Nachrichten gedacht, die von den Diensten gesendet werden, die in Office 365 zur Verfügung stehen (z. B. Dynamics CRM oder Identity Service).
 
> [!NOTE]
> Wir arbeiten derzeit an einem Problem, bei dem Ereignisse mit dem Inhaltstyp Audit.AzureActiveDirectory nicht verfügbar sind, wenn Sie die Office 365-Verwaltungsaktivitäts-API verwenden. Dieses Problem wurde um den 26. Oktober 2020 festgestellt. Azure AD -Anmeldeereignisse sind von diesem Problem nicht betroffen. Wenn das Problem behoben ist, wird ein Update bereitgestellt.

## <a name="frequently-asked-questions-about-the-office-365-management-activity-api"></a>Häufig gestellte Fragen zur Office 365-Verwaltungsaktivitäts-API

**Wie kann ich die Verwaltungsaktivitäts-API nutzen?**

Informationen zu den ersten Schritten mit der Office 365-Verwaltungsaktivitäts-API finden Sie unter [Erste Schritte mit den Office 365-Verwaltungs-APIs](get-started-with-office-365-management-apis.md).

**Was geschieht, wenn ich die Überwachung meiner Office 365-Organisation deaktivieren möchte? Erhalte ich weiterhin Ereignisse über die Verwaltungsaktivitäts-API?**

Nein. Die einheitliche Überwachung von Office 365 muss für Ihre Organisation aktiviert sein, damit Datensätze über die Verwaltungsaktivitäts-API abgerufen werden können. Weitere Anweisungen finden Sie unter [Die Überwachungsprotokollsuche ein- oder ausschalten](https://docs.microsoft.com/microsoft-365/compliance/turn-audit-log-search-on-or-off).

**Welche Ereignisse werden für einen bestimmten Office 365-Dienst überwacht?**

Die Dokumentation für das Office 365-Verwaltungsaktivitäts-API-Schema enthält eine umfassende Liste der Ereignisse. Einzelheiten hierzu finden Sie unter „Office 365-Verwaltungsaktivitäts-API – Schema“. Eine Liste der Ereignisse für die meisten Office 365-Dienste, die überwacht werden, finden Sie auch im Abschnitt „Überwachte Aktivitäten“ in [Durchsuchen des Überwachungsprotokolls im Security & Compliance Center](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#audited-activities).

**Gibt es Unterschiede in den Datensätzen, die von der Verwaltungsaktivitäts-API abgerufen werden, und den Datensätzen, die mit dem Überwachungsprotokoll-Suchtool im Microsoft 365 Compliance Center zurückgegeben werden?**

Von beiden Methoden werden identische Daten zurückgegeben. Der einzige Unterschied besteht darin, dass Sie mit der API nur Daten für die letzten 7 Tage abrufen können (weitere Details finden Sie in den nachfolgenden Fragen). Wenn Sie das Überwachungsprotokoll im Security & Compliance Center durchsuchen (oder das entsprechende Cmdlet **Search-UnifiedAuditLog** im Exchange Online PowerShell verwenden), können Sie Daten für den Aufbewahrungszeitraum abrufen, der bei der Generierung der Daten gültig war (z. B. 90 Tage oder ein Jahr).

**Wie lange muss ich maximal warten, bevor eine Benachrichtigung zu einem bestimmten Office 365-Ereignis gesendet wird?**

Es gibt keine garantierte maximale Wartezeit für die Bereitstellung von Benachrichtigungen (es gibt kein SLA). Normalerweise werden die meisten Benachrichtigungen innerhalb einer Stunde nach dem Ereignis gesendet. Häufig ist die Wartezeit viel kürzer, aber es kann länger dauern, da dies von der Arbeitsauslastung abhängt.

**Sind Webhook-Benachrichtigungen unmittelbarer?**

Nein. In letzter Zeit gab es längere Wartezeiten für Benachrichtigungen bei Verwendung eines Webhook als bei direkter Abfrage der API mit der `/content`-Operation.

**Wie lange bleibt der Inhalt zum Abruf über die API verfügbar?**

Inhalte können während sieben Tagen nach Benachrichtigung über die Verfügbarkeit von Inhalten über die API abgerufen werden. Auch wenn sich die Benachrichtigung ungewöhnlich lange verzögert (beispielsweise bei einer Serviceunterbrechung), haben Sie dennoch 7 Tage nach der ersten Verfügbarkeit der Benachrichtigung, um das mit dem ursprünglichen Ereignis verknüpfte Inhalts-Blob herunterzuladen.

**Kann ich die Verwaltungsaktivitäts-API für eine bestimmte Ereignis-ID oder einen bestimmten RecordType oder andere Eigenschaften im Inhalts-Blob abfragen?**

Nein. Die Verwaltungsaktivitäts-API bietet alle Ereignisdetails für ein bestimmtes Protokoll. Es kann zum Herunterladen der gesamten Details verwendet werden, und dann können Sie Ihre eigene Abfragelogik für die heruntergeladenen Daten implementieren. Verwenden Sie dazu beispielsweise eine benutzerdefinierte Anwendung oder ein Tool eines Drittanbieters.

**Wie kann ich feststellen, ob die Daten aus meiner vorhandenen Überwachungslösung, die Daten von der Verwaltungsaktivitäts-API sammelt, präzise und vollständig sind?**

Die kurze Antwort lautet, dass Microsoft kein Protokoll zur Verfügung stellt, mit dem Sie eine bestimmte Anwendung oder Anwendung von Drittanbietern (ISV) überprüfen können. Es gibt andere Microsoft-Sicherheitsprodukte, die ihre Daten aus derselben Pipeline erhalten, aber diese Produkte werden hier nicht behandelt und können nicht verwendet werden, um die Verwaltungsaktivitäts-API direkt zu prüfen. Wenn Sie sich Sorgen über Diskrepanzen zwischen Ihrer vorhandenen Lösung und Ihren Erwartungen machen, sollten Sie die oben skizzierten Operationen implementieren. Jedoch kann dies schwierig sein, je nachdem, wie Ihr vorhandenes Tool oder Ihre vorhandene Lösung Daten auflistet und indiziert. Wenn Ihre vorhandene Lösung nur Daten darstellt, die sortiert sind nach Erstellungszeit des tatsächlichen Ereignisses, dann gibt es keine Möglichkeit, die API nach Ereigniserstellungszeit abzufragen, um Ergebnissätze zu vergleichen. In diesem Szenario müssten Sie die Inhalts-Blobs mit Benachrichtigungen mehrere Tage sammeln, sie manuell indizieren oder sortieren und dann einen manuellen Vergleich durchführen.

**Was ist der Einschränkungsgrenzwert für die Verwaltungsaktivitäts-API?**

Allen Organisationen ist anfänglich eine Baseline von 2 000-Anforderungen pro Minute zugeordnet. Das Einschränkungslimit wird dann basierend auf einer Kombination von Faktoren angepasst, einschließlich der Anzahl der Arbeitsplätze in der Organisation. Zusätzlich erhalten Office 365 E5 and Microsoft 365 E5-Organisationen erhalten ungefähr doppelt so viel Bandbreite wie Nicht-E5-Organisationen. Zum Schutz des Diensts gibt es auch eine Obergrenze für die maximale Bandbreite.

> [!NOTE]
> Zwar kann jeder Mandant anfänglich bis zu 2.000 Anforderungen pro Minute senden, Microsoft kann aber keine Antwortrate garantieren. Die Antwortrate hängt von verschiedenen Faktoren ab, z. B. der Leistung des Clientsystems, der Netzwerkkapazität und der Geschwindigkeit des Netzwerks.

**In der Verwaltungsaktivitäts-API tritt ein Einschränkungsfehler auf. Was soll ich tun?**

Öffnen Sie ein Ticket beim Microsoft-Support, fordern Sie einen neuen Einschränkungsgrenzwert an, und geben Sie dabei eine geschäftliche Begründung für die Erhöhung des Grenzwerts an. Die Anforderung wird ausgewertet, und wenn sie akzeptiert wird, wird der Einschränkungsgrenzwert erhöht.

**Warum werden in den Auditprotokollen für Azure Active Directory-Aktivitäten "TargetUpdatedProperties" nicht mehr in "ExtendedProperties" enthalten?**

"TargetUpdatedProperties" wurden in "ExtendedProperties" angezeigt. Sie wurden jedoch aus ExtendedProperties entfernt und werden nun in ModifiedProperties angezeigt.

## <a name="troubleshooting-the-office-365-management-activity-api"></a>Problembehandlung bei der Office 365-Verwaltungsaktivitäts-API

Jeder, der die Office 365-Verwaltungsaktivitäts-API verwendet, sollte wissen, dass es keine Abfrage nach Ereignisspezifika gibt, wie Datum des Ereignisses, von welcher Websitesammlung ein Ereignis ausgelöst wurde oder Ereignistyp. Stattdessen erstellen Sie Abonnements für spezielle Arbeitslasten (beispielsweise SharePoint oder Azure AD), und jedes Abonnement ist mandantenspezifisch.

In den folgenden Abschnitten werden die am häufigsten gestellten Fragen zusammengefasst, die Kunden über die Office 365-Verwaltungsaktivitäts-API haben:

- [Fragen zu Drittanbietertools und -clients](#questions-about-third-party-tools-and-clients)

- [Aktivieren der einheitliche Überwachungsprotokollierung in Office 365](#enabling-unified-audit-logging-in-office-365)

- [Herstellen einer Verbindung mit der API](#connecting-to-the-api)

- [Prüfen Ihrer Abonnements](#checking-your-subscriptions)

- [Erstellen eines neuen Abonnements](#creating-a-new-subscription)

- [Verwenden von Webhooks](#using-webhooks)

- [Anfordern von Inhalts-Blobs und Drosselung](#requesting-content-blobs-and-throttling)

Wir zeigen eine Auswahl einfacher PowerShell-Skripts, mit denen Sie die gängigsten Fragen von Kunden beantworten oder eine benutzerdefinierte Lösung durch Demonstration der wichtigsten Operationen implementieren können. Nicht alle Operationen sind in diesen Abschnitten beschrieben, aber sie sind alle unter Office 365-Verwaltungsaktivitäts-API – Referenz aufgelistet.

### <a name="questions-about-third-party-tools-and-clients"></a>Fragen zu Drittanbietertools und -clients

Die häufigsten Fragen stammen von Kunden, die Drittanbieterprodukte zum Herunterladen und Aggregieren von Überwachungsdaten verwenden. Je nach Drittanbieterprodukt haben Kunden Probleme mit der Einrichtung oder sind mit Unterbrechungen oder Inkonsistenzen in Bezug auf die Daten in diesen Produkten konfrontiert. Solche Kunden sollten sich zunächst an den Support des Anbieters wenden. Normalerweise ist eine mandantenspezifische Lieferantenkonfiguration oder ein Dienstproblem die Ursache von Kundenreklamationen.

### <a name="enabling-unified-audit-logging-in-office-365"></a>Aktivieren der einheitliche Überwachungsprotokollierung in Office 365

Wenn Sie gerade eine App eingerichtet haben, die versucht, die Verwaltungsaktivitäts-API zu verwenden, und dies nicht funktioniert, stellen Sie sicher, dass Sie die einheitliche Überwachungsprotokollierung für Ihre Office 365-Organisation aktiviert haben. Dazu aktivieren Sie das Office 365-Überwachungsprotokoll. Weitere Anweisungen finden Sie unter [Aktivieren oder Deaktivieren der Office 365-Überwachungsprotokollsuche](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).

Wenn die einheitliche Überwachung nicht aktiviert ist, wird in der Regel eine Fehlermeldung angezeigt, die folgende Zeichenfolge enthält: `Microsoft.Office.Compliance.Audit``.DataServiceException: Tenant <tenantID> does not exist.`

### <a name="connecting-to-the-api"></a>Herstellen einer Verbindung mit der API

Die meisten Anwendungen stellen mit einem einfachen OAuth2-Fluss mit Client-Anmeldeinformationen eine Verbindung zur API her. Daher ist der erste Schritt das Erstellen einer Azure AD-Anwendung, die die Berechtigungen für den Zugriff auf die Daten der Verwaltungsaktivitäts-API hat. In diesem Artikel werden nicht die Schritte zum Erstellen einer Azure AD-App-Registrierung erläutert. Weitere Informationen finden Sie unter [Registrieren Ihrer Anwendung mit Ihrem Azure Active Directory-Mandanten](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).

#### <a name="azure-application-permissions"></a>Azure-Anwendungsberechtigungen

Die drei Berechtigungen, die derzeit für die Office 365-Verwaltungsaktivitäts-API verwendet werden, sind:

1. Lesen der Aktivitätsdaten für Ihre Organisation

2. Lesen der Dienstintegritätsinformationen für Ihre Organisation

3. Lesen der Data Loss Prevention(DLP)-Richtlinienereignisse, einschließlich der erkannten vertraulichen Informationen

> [!NOTE]
> Sie sollten die Anwendungsberechtigungen und die delegierten Berechtigungen für mindestens die ersten beiden der obigen Berechtigungsgruppen aktivieren. Das Lesen der DLP-Richtlinienereignisse ist nur erforderlich, wenn Sie an den DLP-Arbeitslasten interessiert sind.

#### <a name="getting-an-access-token"></a>Abrufen eines Zugriffstokens

Das folgende PowerShell-Skript verwendet die App-ID und einen geheimen Clientschlüssel, um das OAuth2-Token vom Authentifizierungsendpunkt der Verwaltungsaktivitäts-API abzurufen. Es platziert dann das Zugriffstoken in der `$headerParams`-Array-Variable, die Sie an Ihre HTTP-Anforderung anhängen. Verwenden Sie für den Wert für den API-Endpunkt (in der $resource-Variable) einen der folgenden Werte basierend auf dem Microsoft 365- oder Office 365-Abonnementplan Ihrer Organisation:

- Enterprise-Plan: `manage.office.com`

- GCC-Government-Plan: `manage-gcc.office.com`

- GCC High Government-Plan: `manage.office365.us`

- DoD Government-Plan: `manage.protection.apps.mil`

```powershell
# Create app of type Web app / API in Azure AD, generate a Client Secret, and update the client id and client secret here
$ClientID = "<YOUR_APPLICATION_ID"
$ClientSecret = "<YOUR_CLIENT_SECRET>"
$loginURL = "https://login.microsoftonline.com/"
$tenantdomain = "<YOUR_DOMAIN>.onmicrosoft.com"
# Get the tenant GUID from Properties | Directory ID under the Azure Active Directory section. For $resource, use one of these endpoint values based on your subscription plan: Enterprise - manage.office.com; GCC - manage-gcc.office.com; GCC High: manage.office365.us; DoD: manage.protection.apps.mil
$TenantGUID = "<YOUR_TENANT_GUID>"
$resource = "https://<YOUR_API_ENDPOINT>"
# auth
$body = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
$headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"} 
```

Die `$oauth`-Variable enthält das Antwortobjekt, das mehrere Eigenschaften einschließlich des Zugriffstokens umfasst. Beispiel für eine Antwort:

```json
token_type     : Bearer
expires_in     : 3599
ext_expires_in : 0
expires_on     : 1508285860
not_before     : 1508281960
resource       : https://manage.office.com
access_token   : eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyIsImtpZCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyJ9.eyJhdWQiOiJodHRwczov…
```

### <a name="checking-your-subscriptions"></a>Prüfen Ihrer Abonnements

Wenn eine Unterbrechung im Datenfluss zu einem vorhandenen Client oder einer vorhandenen Lösung der Verwaltungsaktivitäts-API auftritt, gibt es evtl. ein Problem mit Ihrem Abonnement. Wenn Sie Ihre aktiven Abonnements prüfen möchten, fügen Sie Folgendes zum vorherigen Skript hinzu:

```powershell
Invoke-WebRequest -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/list" 
```

#### <a name="sample-response"></a>Beispielantwort

```json
StatusCode        : 200
Status Description : OK
Content           : [{"contentType":"Audit.Exchange","status":"enabled","webhook":null},{"contentType":"Audit.SharePoint","status":"enabled","webhook":{"authId":"","address":"https://mvcwebapiwebhookreceiver.azurewebsite...
RawContent        : HTTP/1.1 200 OK
                    Pragma: no-cache
                    Content-Length: 266
                    Cache-Control: no-cache
                    Content-Type: application/json; charset=utf-8
                    Expires: -1
                    Server: Microsoft-IIS/8.5,Microsoft-IIS/8.5
                    X-AspNet-Versi...
Forms             : {}
Headers           : {[Pragma, no-cache], [Content-Length, 266], [Cache-Control, no-cache], [Content-Type, application/json; charset=utf-8]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 266
```

Das bedeutet, dass für den Mandanten sowohl Audit.Exchange- als auch Audit.SharePoint-Abonnements aktiviert sind. Das Exchange-Abonnement verfügt nicht über einen aktivierten Webhook (null), und das SharePoint-Abonnement hat einen aktivierten Webhook, wobei die Adresse des registrierten Endpunkts angezeigt wird.

### <a name="creating-a-new-subscription"></a>Erstellen eines neuen Abonnements

Um ein neues Abonnement zu erstellen, verwenden Sie die /start-Operation. Verwenden Sie für den API-Endpunkt einen der folgenden Werte basierend auf Ihrem Abonnementplan:

- Enterprise-Plan: `manage.office.com`

- GCC-Government-Plan: `manage-gcc.office.com`

- GCC High Government-Plan: `manage.office365.us`

- DoD Government-Plan: `manage.protection.apps.mil`

```powershell
Invoke-WebRequest -Method Post -Headers $headerParams -Uri "https://<YOUR_API_ENDPOINT>/api/v1.0/$tenantGUID/activity/feed/subscriptions/start?contentType=Audit.AzureActiveDirectory"

> [!NOTE]
> Remember that `$headerParams` was populated in the first part of the script listed in the [Connecting to the API](#connecting-to-the-api) section in this article.

The previous code will create a new subscription to the Audit.AzureActiveDirectory content type, with a webhook that is null. You can then check your subscriptions using the code in the [Checking your subscriptions](#checking-your-subscriptions) section in this article.

## Checking content availability

To check what content blobs were created during a certain period, you can add the following line to the script in the “Connecting to the API” section.

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint"
```

Im vorherigen Beispiel werden alle Benachrichtigungen empfangen, die heute verfügbar wurden, das heißt, von 12:00 Uhr UTC bis jetzt. Wenn Sie einen anderen Zeitraum angeben möchten (unter Berücksichtigung der Tatsache, dass der maximale Abfragezeitraum 24 Stunden beträgt), fügen Sie die Parameter *starttime* und *endtime* zum URI hinzu; beispielsweise:

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint&startTime=2017-10-13T00:00&endTime=2017-10-13T11:59"
```

> [!NOTE]
> Sie müssen die Parameter *starttime* und *endtime* gemeinsam verwenden.

```json
[{      "contentUri" : "https://<your_API_endpoint>/api/v1.0/<your_tenant_guid>/activity/feed/audit/20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentId" : "20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentType" : "Audit.SharePoint",
        "contentCreated" : "2017-10-13T18:00:51.748Z",
        "contentExpiration" : "2017-10-20T18:00:51.748Z",
}]
```

> [!IMPORTANT]
>
> - Die *ContentUri* -Eigenschaft ist der URI, von dem Sie das Inhalts-Blob abrufen können. Das Blob selbst enthält die Ereignisdetails; es enthält Details zu 1 – N-Ereignissen. Selbst wenn 30 JSON-Objekte in der Sammlung vorhanden sind, sind evtl. viel mehr Ereignisse in diesen 30 Inhalts-URIs aufgeführt.
>
> - Die *ContentCreated* -Eigenschaft ist nicht das Datum, an dem das Ereignis mit der Benachrichtigung erstellt wurde. Dies ist das Datum, an dem die Benachrichtigung erstellt wurde. Die Ereignisse in diesem Blob wurden möglicherweise deutlich vor dem Inhalts-Blob erstellt. Daher können Sie die API niemals direkt für Ereignisse abfragen, die in einem bestimmten Zeitraum aufgetreten sind.

#### <a name="paging-contents-for-busy-tenants"></a>Auslagern von Inhalten für aktive Mandanten

Für viele größere Office 365-Mandanten werden Tausende von Ereignissen pro Stunde generiert. Wenn dies bei Ihrer Organisation der Fall ist und Sie versuchen, eine Abfrage für einen 24-Stunden-Zeitraum wie im vorstehenden Beispiel auszuführen, müssen Sie evtl. mehr Benachrichtigungen abrufen als in einer Antwort zurückgegeben werden können. In diesem Fall müssen Sie eine logische Schleife eines bestimmten Typs implementieren, wenn Sie die Antwortheader für den Headerwert **NextPageUrl:** prüfen. Im Abschnitt „Paginierung“ in der Referenz zur Office 365-Verwaltungsaktivitäts-API finden Sie weitere Details.

```powershell
IF the NextPageUrl header is present in the response... 

THEN issue a new request substituting the Uri parameter in the above Invoke-WebRequest example for the value of the NextPageUrl header...
 
ELSE exit the loop
```

Es ist schwierig, diesen Schleifencode zu testen, wenn Sie keinen aktiven Mandanten haben. In unseren Tests haben wir versucht, verschiedene Tausende Update-Operationen in einem Skript auszuführen und konnten keine ausreichende Anzahl an Benachrichtigungen generieren, um das Senden des **NextPageUrl** -Headers anzufordern.

### <a name="using-webhooks"></a>Verwenden von Webhooks

Es gibt zwei Möglichkeiten, eine Benachrichtigung zu erhalten, dass Inhalts-Blobs erstellt wurden. Der *Push* -Ansatz wird mit einem Webhook-Endpunkt implementiert. Bei diesem handelt es sich um eine Webanwendung, die Sie erstellen und selbst oder auf einer Cloudplattform hosten. Sie registrieren den Webhook beim Erstellen eines Abonnements für einen überwachten Inhaltstyp. Sie können auch die Registrierung eines Webhook zu einem vorhandenen Abonnement mit dem unten dargestellten Ansatz hinzufügen. Der *Pull* -Ansatz erfordert die Abfrage einer bestimmten Zeitspanne (nicht mehr als 24 Stunden) mit der /content-Operation. Die Antwort informiert sie, welche Inhalts-Blobs während des angegebenen Zeitraums erstellt wurden.

Bevor Sie einen Webhook hinzufügen, sollten Sie Folgendes beachten:

1. Webhooks haben bei Microsoft an Bedeutung verloren, da Debugging und Fehlerbehebung schwierig sind. In der Regel hosten Sie einen WebApi-Endpunkt, der auf eingehende Anforderungen antwortet. Viele Kunden verwenden entweder Hosting-Umgebungen (über die sie keine vollständige Kontrolle haben) oder lokale Umgebungen (die Probleme haben, eingehende HTTP-Anforderungen zuzulassen). Der Support hat viele Probleme beobachtet, bei denen eingehende Anforderungen von der Office 365-Überwachungspipeline durch eine Firewall oder einen Router blockiert wurden. In diesem Fall implementiert die API einen Backoff-Algorithmus, was verwirrend sein kann und evtl. zur Deaktivierung des Webhook im Abonnement führt.

2. Der Webhook muss sofort auf eine Validierungsanforderung reagieren, nachdem der Startvorgang ausgeführt wird. Wenn ein Bug in der Webhook-Anwendung vorhanden ist, schlägt die Validierung fehl, und der Webhook wird nicht aktiviert. Informationen zum Schema der Validierungsanforderung finden Sie im Abschnitt „Webhook-Validierung“ in der Referenz zur Office 365-Verwaltungsaktivitäts-API. Sie sollten sich die Herausforderungen der Erstellung eines produktionsbereiten Webhook zur Reaktion auf Benachrichtigungen der Verwaltungsaktivitäts-API klar machen.

Wenn Sie einen Webhook implementieren, sollte er getestet werden, um zu verifizieren, dass der Endpunkt mit einer HTTP 200-Antwort auf die Validierungsanforderung und die normalen Benachrichtigungsanforderungen antwortet, bevor zum ersten Mal eine /start-Operation aufgerufen wird, die einen Webhook-Endpunkt angibt. In der Regel verwenden Sie eine Testanforderung von der API, um diese Bereitschaft zu testen. Lesen Sie sorgfältig die Abschnitte Webhook-Validierung und Abrufen von Inhalt in der Referenz zur Office 365-Verwaltungsaktivitäts-API, um das Schema dieser beiden Anforderungstypen zu verstehen.

Wenn Sie ein Abonnement mit einem Webhook-Endpunkt hinzufügen möchten, fügen Sie einen Textparameter zum POST zum /start-Endpunkt hinzu; zum Beispiel:

```json
$body = '{
    "webhook" : {
        "address": "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": ""
    }}'
$uri = "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed//subscriptions/start?contentType=Audit.SharePoint"
Invoke-RestMethod -Method Post -uri $uri -Headers $headerParams -Body $body
```

Unmittelbar nach diesem Aufruf wird eine Validierungsanforderung an `https://webhook.myapp.com/o365/ …` gesendet, und es sollte ein Listener zum Antworten vorhanden sein, gemäß Beschreibung im Abschnitt Webhook-Validierung in der Referenz zur Office 365-Verwaltungsaktivitäts-API. Ihr Listener muss mit HTTP 200 antworten. Wenn Sie die /list-Operation an diesem Punkt sofort ausführen, wird der Webhook als „null“ angezeigt, bis die Validierung erfolgreich war.

#### <a name="checking-notifications-to-webhooks"></a>Prüfen von Benachrichtigungen an Webhooks

Es ist wichtig, zwischen der /notifications- und der /content-Operation zu unterscheiden. Die Prüfung der Benachrichtigungen ist nur relevant, wenn Sie mit einem Webhook-Endpunkt abonniert haben. Diese Operation teilt Ihnen mit, ob Versuche zum Senden von Benachrichtigungen an Ihren Webhook erfolgreich waren. Diese Operation sollte nicht zum Auflisten der verfügbaren Inhalte verwendet werden. Um die Verfügbarkeit von Inhalten mit dem zu prüfen, was Sie bereits in Ihrem Webhook erhalten haben, verwenden Sie die /content-Operation. Prüfen Sie jedoch erst mit der /notifications-Operation auf fehlgeschlagene Benachrichtigungen.

### <a name="requesting-content-blobs-and-throttling"></a>Anfordern von Inhalts-Blobs und Drosselung

Nachdem Sie eine Liste von Inhalts-URLs erhalten haben, müssen Sie die Blobs anfordern, die von den URLs angegeben werden. Im Folgenden finden Sie ein Beispiel für die Anforderung eines Inhalts-Blobs (unter Verwendung des API-Endpunkts manage.office.com für Unternehmen) mit PowerShell. In diesem Beispiel wird davon ausgegangen, dass Sie bereits das vorherige Beispiel im Abschnitt [Abrufen eines Zugriffstoken](#getting-an-access-token) in diesem Artikel verwendet haben, um ein Zugriffstoken zu erhalten, und die `$headerParams`-Variable entsprechend gefüllt haben.

```powershell
# Get a content blob
$uri = 'https://manage.office.com/api/v1.0/<<your-tenant-guid>>/activity/feed/audit/<<ContentID>$audit_sharepoint$Audit_SharePoint'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

Beachten Sie die folgenden Punkte zur *$uri* -Variablen im vorherigen Beispiel:

- Wir haben einzelne Anführungszeichen verwendet, sodass die *$* -Symbole nicht als Variablen in PowerShell interpretiert werden.

- Die gesamte URI wird in der *ContentUri* -Eigenschaft der Antwort auf Ihren vorherigen Aufruf des /content-Endpunkts zurückgegeben. Die dargestellten Platzhaltertoken dienen nur zur Veranschaulichung.

Wenn Sie versuchen, die verfügbaren Inhalts-Blobs abzurufen, sind bei vielen Kunden (die hauptsächlich mit aktiven Mandanten arbeiten) Fehler wie folgende aufgetreten:

```json
Response Code 403: {'error':{'code':'AF429','message':'Too many requests. Method=GetBlob, PublisherId=00000000-0000-0000-0000-000000000000'}}
```

Dies liegt wahrscheinlich an der Drosselung. Beachten Sie, das der Wert des PublisherId-Parameters wahrscheinlich darauf hinweist, dass der Client *PublisherIdentifier* in der Anforderung nicht angegeben hat. Darüber hinaus sollten Sie berücksichtigen, dass der richtige Parametername *PublisherIdentifier* lautet, auch wenn *PublisherId* in den 403-Fehlerantworten aufgeführt ist.

> [!NOTE]
> In der API-Referenz ist der *PublisherIdentifier* -Parameter in jeder Operation der API aufgelistet, sollte jedoch auch beim Abruf des Inhalts-Blob in der GET-Anforderung zur contentUri-URL eingeschlossen werden.

Wenn Sie einfache API-Aufrufe zur Problembehebung ausführen (beispielsweise Prüfung, ob ein vorhandenes Abonnement aktiv ist), können Sie den *PublisherIdentifier* -Parameter auslassen. Jeder Code, der für die Produktion gedacht ist, sollte den *PublisherIdentifier* -Parameterjedoch bei jedem Aufruf aufweisen.

Wenn Sie einen Client für den Mandanten Ihres Unternehmens implementieren, ist *PublisherIdentifier* die GUID des Mandanten. Wenn Sie eine ISV-Anwendung oder ein Add-In für mehrere Kunden erstellen, sollte *PublisherIdentifier* die Mandanten-GUID des ISVs und nicht die Mandanten-GUID des Endbenutzerunternehmens sein.

Wenn Sie die gültige *PublisherIdentifier* einschließen, befinden Sie sich in einem Pool, dem 60.000 Anforderungen pro Minute und Mandant zugewiesen werden. Dies ist eine außergewöhnlich große Anzahl von Anforderungen. Wenn Sie den *PublisherIdentifier* -Parameter jedoch nicht einschließen, befinden Sie sich im allgemeinen Pool, dem 60.000 Anforderungen pro Minute für alle Mandanten zugewiesen werden. In diesem Fall werden Sie sehr wahrscheinlich feststellen, dass Ihre Aufrufe gedrosselt werden. Um dies zu verhindern, fordern Sie ein Inhalts-Blob mit *PublisherIdentifier* wie folgt an:

```json
$contentUri = ($response.Content | ConvertFrom-Json).contentUri[0]
$uri = $contentUri + '?PublisherIdentifier=82b24b6d-0591-4604-827b-705d55d0992f'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

Das vorherige Beispiel setzt voraus, dass die *$response* -Variable mit der Antwort auf eine Anforderung beim /content-Endpunkt gefüllt wurde und dass die *$headerParams* -Variable ein gültiges Zugriffstoken enthält. Das Skript verwendet das erste Element im Array von Inhalts-URIs aus der Antwort und ruft dann GET auf, um dieses Blob herunterzuladen und es in der *$contents* -Variable zu platzieren. Der Code wird in der contentUri-Sammlung in einer Schleife ausgeführt, wobei GET für *contentUri* ausgegeben wird.
