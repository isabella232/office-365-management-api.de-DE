---
ms.TocTitle: Office 365 Management Activity API reference
title: Office 365-Verwaltungsaktivitäts-API – Referenz
description: Verwenden Sie die Office 365-Verwaltungsaktivitäts-API zum Abrufen von Informationen über Benutzer-, Verwaltungs-, System- und Richtlinienaktionen und -ereignisse aus Office 365 und Azure AD-Aktivitätsprotokollen.
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: 01/10/2018
localization_priority: Priority
ms.openlocfilehash: d6cdef5f0445ef0fa551be3080d4ce28595a1e9f
ms.sourcegitcommit: 784b581a699c6d0ab7939ea621d5ecbea71925ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2019
ms.locfileid: "35924826"
---
# <a name="office-365-management-activity-api-reference"></a>Office 365-Verwaltungsaktivitäts-API – Referenz

Verwenden Sie die Office 365-Verwaltungsaktivitäts-API zum Abrufen von Informationen über Benutzer-, Verwaltungs-, System- und Richtlinienaktionen und -ereignisse aus Office 365 und Azure AD-Aktivitätsprotokollen. 

Sie können die Aktionen und Ereignisse aus den Office 365- und Microsoft Azure Active Directory-Überwachungs- und -Aktivitätsprotokollen verwenden, um Lösungen zu erstellen, die Überwachung, Analysen und Datenvisualisierung bereitstellen. Anhand dieser Lösungen haben Organisationen einen besseren Einblick in die Aktionen, die mit ihren Inhalten ausgeführt werden. Diese Aktionen und Ereignisse sind auch in den Office 365-Aktivitätsberichten verfügbar. Weitere Informationen finden Sie unter [Durchsuchen des Überwachungsprotokolls im Office 365 Security & Compliance Center](https://support.office.com/de-DE/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).

Die Office 365-Verwaltungsaktivitäts-API ist ein REST-Webdienst, mit dem Sie Lösungen in einer beliebigen Sprache und mit jeder Hosting-Umgebung, die HTTPS- und X.509-Zertifikate unterstützt, entwickeln können. Die API basiert auf Azure AD und dem OAuth2-Protokoll für Authentifizierung und Autorisierung. Um von Ihrer Anwendung aus auf die API zugreifen zu können, müssen Sie diese zuerst in Azure AD registrieren und dann mit den entsprechenden Berechtigungen konfigurieren. Dadurch kann die Anwendung OAuth2-Zugriffstoken anfordern, die sie zum Aufrufen der API benötigt. Weitere Informationen finden Sie unter [Erste Schritte mit den Office 365-Verwaltungs-APIs](get-started-with-office-365-management-apis.md).

Weitere Informationen über die Daten, die von der Office 365-Verwaltungsaktivitäts-API zurückgegeben werden, finden Sie unter [Office 365-Verwaltungsaktivitäts-API-Schema](office-365-management-activity-api-schema.md).

> [!IMPORTANT]
> Bevor Sie über die Office 365-Verwaltungsaktivitäts-API auf Daten zugreifen können, müssen Sie die einheitliche Überwachungsprotokollierung für Ihre Office 365-Organisation aktivieren. Dazu aktivieren Sie das Office 365-Überwachungsprotokoll. Weitere Anweisungen finden Sie unter [Aktivieren oder Deaktivieren der Office 365-Überwachungsprotokollsuche](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).


## <a name="working-with-the-office-365-management-activity-api"></a>Verwenden der Office 365-Verwaltungsaktivitäts-API

Die Office 365-Verwaltungsaktivitäts-API aggregiert Aktionen und Ereignissen in mandantenspezifische Inhalts-Blobs, die durch den Typ und die Quelle der darin enthaltenen Inhalte klassifiziert werden. Derzeit werden die folgenden Inhaltstypen unterstützt:

- Audit.AzureActiveDirectory
    
- Audit.Exchange
    
- Audit.SharePoint
    
- Audit.General (enthält alle anderen Workloads, die in den vorherigen Inhaltstypen nicht enthalten sind)

- DLP.All (nur DLP-Ereignisse für alle Workloads)
    
Details zu den Ereignissen und Eigenschaften, die mit diesen Inhaltstypen verknüpft sind, finden Sie unter [Office 365-Verwaltungsaktivitäts-API-Schema](office-365-management-activity-api-schema.md).

Um mit dem Abrufen von Inhalts-Blobs für einen Mandanten zu beginnen, erstellen Sie zuerst ein Abonnement für die gewünschten Inhaltstypen. Wenn Sie Inhalts-Blobs für mehrere Mandanten abrufen möchten, erstellen Sie mehrere Abonnements für jeden der gewünschten Inhaltstypen, eines für jeden Mandanten.

Nachdem Sie ein Abonnement erstellt haben, können Sie regelmäßig Abfragen durchführen, um neue Inhalts-Blobs zu finden, die zum Download zur Verfügung stehen. Sie können auch einen Endpunkt-Webhook mit dem Abonnement registrieren, und wir senden dann Benachrichtigungen an diesen Endpunkt, wenn neue Inhalts-Blobs verfügbar sind.


> [!NOTE] 
> Wenn Sie ein Abonnement erstellt wurde, kann es bis zu 12 Stunden dauern, bevor die ersten Inhalts-Blobs für dieses Abonnement verfügbar sind. Die Inhalts-Blobs werden durch das Sammeln und Aggregieren von Aktionen und Ereignissen für mehrere Server und Rechenzentren erstellt. Als Ergebnis dieses verteilten Vorgangs werden die Aktionen und Ereignisse in den Inhalts-Blobs nicht unbedingt in der Reihenfolge angezeigt, in der sie aufgetreten sind. Ein Inhalts-Blob kann Aktionen und Ereignisse enthalten, die vor den Aktionen und Ereignissen aufgetreten sind, die in einem früheren Inhalts-Blob enthalten sind. Wir arbeiten daran, die Zeitverzögerung zwischen dem Auftreten von Aktionen und Ereignissen und deren Verfügbarkeit in einem Inhalts-Blob zu verringern, können jedoch nicht garantieren, dass sie in Reihenfolge angezeigt werden.


> [!NOTE] 
> Vertrauliche DLP-Daten sind nur in der Aktivitätsfeed-API für Benutzer verfügbar, denen die Berechtigung „Lesen vertraulicher DLP-Daten“ erteilt wurde. Weitere Informationen über die Verhinderung von Datenverlust (Data Loss Prevention, DLP) finden Sie unter [Übersicht über die Richtlinien zur Verhinderung von Datenverlust](https://support.office.com/de-DE/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)

## <a name="activity-api-operations"></a>Aktivitäts-API-Vorgänge

Alle API-Vorgänge sind auf einen einzelnen Mandanten beschränkt, und die Stamm-URL der API enthält eine Mandanten-ID, die den Mandantenkontext angibt. Die Mandanten-ID ist eine GUID. Informationen zum Abrufen der GUID finden Sie unter [Erste Schritte mit den Office 365-Verwaltungs-APIs](get-started-with-office-365-management-apis.md).


```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

Da die Benachrichtigungen, die wir an Ihren Webhook senden, die **Mandanten-ID** enthalten, können Sie denselben Webhook zum Empfangen von Benachrichtigungen für alle Mandanten verwenden.

Alle API-Vorgänge erfordern einen Autorisierungs-HTTP-Header mit einem Zugriffstoken von Azure AD. Die Mandanten-ID im Zugriffstoken muss der Mandanten-ID in der Stamm-URL der API entsprechen, und das Zugriffstoken muss den Anspruch „ActivityFeed.Read“ enthalten. (Dies entspricht der Berechtigung [Aktivitätsdaten für eine Organisation lesen], die Sie für die Anwendung in Azure AD konfiguriert haben.)

```json
Authorization: Bearer eyJ0e...Qa6wg
```

Die Aktivitäts-API unterstützt die folgenden Vorgänge:

- **Abonnement starten**, um Benachrichtigungen zu erhalten und Aktivitätsdaten für einen Mandanten abzurufen.
    
- **Abonnement beenden**, um keine Daten für einen Mandanten mehr zu abzurufen.
    
- **Aktuelle Abonnements auflisten**
    
- **Verfügbare Inhalte auflisten**, sowie die entsprechenden Inhalts-URLs.
    
- **Benachrichtigungen erhalten**, die von einem Webhook gesendet werden, wenn neuer Inhalt verfügbar ist.
    
- **Inhalt abrufen** mithilfe der Inhalts-URL.
    
- **Benachrichtigungen auflisten**, die von einem Webhook gesendet werden.

- **Anzeigenamen für Ressourcen abrufen**, für Objekte im Datenfeed, die durch eine GUID identifiziert werden.
    

## <a name="start-a-subscription"></a>Starten eines Abonnements

Dieser Vorgang beginnt mit dem Abonnement für den angegebenen Inhaltstyp. Wenn bereits ein Abonnement für den angegebenen Inhaltstyp vorhanden ist, wird dieser Vorgang für Folgendes verwendet:

- Aktualisieren der Eigenschaften eines aktiven Webhooks
    
- Aktivieren eines Webhooks, der aufgrund von übermäßig vielen fehlgeschlagenen Benachrichtigungen deaktiviert wurde
    
- Erneutes Aktivieren eines abgelaufenen Webhooks durch Angabe eines späteren Ablaufdatums oder Angabe von „null“
    
- Entfernen eines Webhooks
    
||Abonnement|Beschreibung|
|:-----|:-----|:-----|
|**Pfad**| `/subscriptions/start?contentType={ContentType}`||
|**Parameter**|contentType|Muss ein gültiger Inhaltstyp sein.|
||PublisherIdentifier|Die Mandanten-GUID des Herstellers, der mit der API codiert. Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt. Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet. Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten. Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.|
|**Body**|webhook|Optionales JSON-Objekt mit drei Eigenschaften:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>address</b>: Erforderlicher HTTPS-Endpunkt, der Benachrichtigungen empfangen kann.  Es wird eine Testnachricht an den Webhook gesendet, um ihn zu überprüfen, bevor das Abonnements erstellt wird.</p></li><li><p><b>AuthId</b>: Optionale Zeichenfolge, die als WebHook-AuthID-Header in Benachrichtigungen einbezogen wird, die an den Webhook gesendet werden. Dies ist eine Methode zum Erkennen und Autorisieren der Quelle, aus der die Anforderung an den Webhook stammt.</p></li><li><p><b>expiration</b>: Optionale datetime-Angabe, die ein Datum und eine Uhrzeit angibt, nach deren Ablauf keine Benachrichtigungen mehr an den Webhook gesendet werden sollen.</p></li></ul>|
|**Antwort**|contentType|Der im Aufruf angegebene Inhaltstyp.|
||status|Der Status des Abonnements. Wenn ein Abonnement deaktiviert ist, können Sie keine Inhalte auflisten oder abrufen.|
||webhook|Die im Aufruf angegeben Webhook Eigenschaften mit dem Status des Webhooks. Wenn der Webhook deaktiviert ist, erhalten Sie keine Benachrichtigung. Sie können jedoch weiterhin Inhalt auflisten und abrufen, vorausgesetzt, das Abonnement ist  aktiviert.|

#### <a name="sample-request"></a>Beispielanfrage

```json
POST {root}/subscriptions/start?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Content-Type: application/json; utf-8
Authorization: Bearer eyJ0e...Qa6wg

{
    "webhook" : {
        "address": "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": ""
    }
}

```


#### <a name="sample-response"></a>Beispielantwort

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
    "contentType": "Audit.SharePoint",
    "status": "enabled",
    "webhook": {
        "status": "enabled",
        "address":  "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": null
    }
}

```


## <a name="webhook-validation"></a>Webhook-Überprüfung

Wenn der /start-Vorgang aufgerufen wird und ein Webhook angegeben ist, senden wir eine Überprüfungsbenachrichtigung an die angegebene Webhook-Adresse, um zu überprüfen, ob ein aktiver Listener die Benachrichtigungen annehmen und verarbeiten kann. Wenn wir keine „HTTP 200 OK“-Antwort erhalten, wird das Abonnement nicht erstellt. Wenn „/start“ alternativ aufgerufen wird, um einen Webhook zu einem vorhandenen Abonnement hinzuzufügen und die Antwort „HTTP 200 OK“ nicht empfangen wird, wird der Webhook nicht hinzugefügt, und das Abonnement bleibt unverändert.

#### <a name="sample-request"></a>Beispielanfrage

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId, if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a>Beispielantwort

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a>Beenden eines Abonnements

Dieser Vorgang beendet das Abonnement für den angegebenen Inhaltstyp. 

Wenn ein Abonnement beendet wird, erhalten Sie keine Benachrichtigungen mehr und Sie können keine verfügbaren Inhalte mehr abrufen. Wenn Sie das Abonnement später neu starten, haben Sie ab diesem Zeitpunkt Zugriff auf neue Inhalte. Sie können keinen Inhalt abrufen, der zwischen dem Beenden und erneuten Starten des Abonnements verfügbar war.


||Abonnement|Beschreibung|
|:-----|:-----|:-----|
|**Pfad**| `/subscriptions/stop?contentType={ContentType}`||
|**Parameter**|contentType|Muss ein gültiger Inhaltstyp sein.|
||PublisherIdentifier|Die Mandanten-GUID des Herstellers, der mit der API codiert. Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt. Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet. Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten. Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.|
|**Body**|(leer)||
|**Antwort**|(leer)|||

#### <a name="sample-request"></a>Beispielanfrage

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Beispielantwort

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a>Auflisten aktueller Abonnements

Dieser Vorgang gibt eine Sammlung der aktuellen Abonnements zusammen mit den zugehörigen Webhooks zurück.

||Abonnement|Beschreibung|
|:-----|:-----|:-----|
|**Pfad**| `/subscriptions/list`||
|**Parameter**|PublisherIdentifier|Die Mandanten-GUID des Herstellers, der mit der API codiert. Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt. Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet. Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten. Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.|
|**Body**|(leer)||
|**Antwort**|JSON-Array|Jedes Abonnement wird durch ein JSON-Objekt mit drei Eigenschaften dargestellt:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>contentType</b>: Gibt den Inhaltstyp an.</p></li><li><p><b>status</b>: Gibt den Status des Abonnements an.</p></li><li><p><b>webhook</b>: Gibt den konfigurierten Webhook zusammen mit seinem Status an (aktiviert, deaktiviert, abgelaufen).  Wenn ein Abonnement keinen Webhook hat, ist die Webhook-Eigenschaft zwar vorhanden, hat jedoch den Wert „null“.</p></li></ul>|


#### <a name="sample-request"></a>Beispielanfrage

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Beispielantwort

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType" : "Audit.SharePoint",
        "status": "enabled",
        "webhook": {
            "status": "enabled",
            "address": "https://webhook.myapp.com/o365/",
            "authId": "o365activityapinotification",
            "expiration": null
        }
    },

    ...

    {
        "contentType": "Audit.Exchange",
        "webhook": null
    }
]

```


## <a name="list-available-content"></a>Verfügbare Laufwerke auflisten

Dieser Vorgang listet den Inhalt auf, der aktuell zum Abrufen für den angegebenen Inhaltstyp zur Verfügung steht. Der Inhalt ist eine Aggregation von Aktionen und Ereignissen, die von mehreren Servern in mehreren Rechenzentren abgerufen wurden. Der Inhalt wird in der Reihenfolge aufgelistet, in der die Aggregationen verfügbar wird. Es kann jedoch nicht gewährleistet werden, dass die Ereignisse und Aktionen in den Aggregationen in der Reihenfolge des Auftretens aufgeführt werden. Wenn der Abonnementstatus deaktiviert ist, wird ein Fehler zurückgegeben.


||Abonnement|Beschreibung|
|:-----|:-----|:-----|
|**Pfad**| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|**Parameter**|contentType|Muss ein gültiger Inhaltstyp sein.|
||PublisherIdentifier|Die Mandanten-GUID des Herstellers, der mit der API codiert. Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt. Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet. Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten. Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.|
||startTime endTime|Optionale Datums- und Uhrzeitangabe (UTC), die den Zeitraum angibt, in dem Inhalte zurückgegeben werden sollen, basierend darauf, wann der Inhalt verfügbar wurde. Der Zeitraum bezieht die Startzeit (startTime < = contentCreated) mit ein, schließt die Endzeit (contentCreated < endTime) jedoch aus, damit nicht überlappende, inkrementierende Zeitintervalle zum Blättern durch den verfügbaren Inhalte verwendet werden können.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>YYYY-MM-DD</p></li><li><p>YYYY-MM-DDTHH:MM</p></li><li><p>YYYY-MM-DDTHH:MM:SS</p></li></ul>Es müssen beide angegeben werden (oder beide nicht angegeben werden), und die Zeitangaben dürfen nicht mehr als 24 Stunden auseinander liegen, wobei die Startzeit nicht mehr als sieben Tagen in der Vergangenheit liegen darf. Wenn „startTime“ und „endTime“ ausgelassen werden, wird standardmäßig der in den letzten 24 Stunden verfügbare Inhalt zurückgegeben.<p>**HINWEIS**: Obwohl es möglich ist, eine Startzeit und Endzeit anzugeben, die mehr als 24 Stunden auseinander liegen, wird dies nicht empfohlen. Wenn Sie länger als 24 Stunden Ergebnisse als Antwort auf eine Anforderung erhalten, kann es sich hierbei außerdem nur um Teilergebnisse handeln, die nicht berücksichtigt werden sollten. Die Anforderung sollte mit einem Intervall von nicht mehr als 24 Stunden zwischen der Startzeit und Endzeit ausgegeben werden.</p>|
|**Antwort**|JSON-Array|Die verfügbare Inhalte werden durch JSON-Objekte mit den folgenden Eigenschaften dargestellt:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>contentType</b>: Gibt den Inhaltstyp an.</p></li><li><p><b>contentId</b>: Eine verdeckte Zeichenfolge, die den Inhalt eindeutig identifiziert.</p></li><li><p><b>contentUri</b>: Die URL zum Abrufen von Inhalt.</p></li><li><p><b>contentCreated</b>: Datum und Uhrzeit, wann der Inhalt verfügbar wurde.</p></li><li><p><b>contentExpiration</b>: Datum und Uhrzeit, nach dem der Inhalt nicht mehr abgerufen werden kann.</p></li></ul>|


#### <a name="sample-request"></a>Beispielanfrage

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Beispielantwort

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z"
    },
    ...
]

```


### <a name="pagination"></a>Paginierung

Beim Auflisten des Inhalts für einen Zeitraum wird die Anzahl der zurückgegebenen Ergebnisse beschränkt, um Zeitüberschreitungen bei der Antwort zu vermeiden. Wenn im angegebenen Zeitraum mehr Ergebnisse vorliegen, als in einer einzelnen Antwort zurückgegeben werden können, werden die Ergebnisse abgeschnitten und es wird ein Header zur Antwort hinzugefügt, der die URL zum Abrufen der nächsten Seite mit Ergebnissen angibt. Die URL enthält dieselben _startTime_- und _endTime_-Parameter, die in der ursprünglichen Anforderung angegeben wurden, zusammen mit einem Parameter, der die interne ID der nächsten Seite angibt. Wenn _startTime_ und _endTime_ in der ursprünglichen Anforderung nicht angegeben werden, werden sie auf ein 24-Stunden-Intervall festgelegt, das der ursprünglichen Anforderung voranging.


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

Um den gesamten verfügbaren Inhalt für einen angegebenen Zeitraum aufzulisten, müssen Sie möglicherweise mehrere Seiten abrufen, bis eine Antwort ohne den Header **NextPageUri** empfangen wird.


## <a name="receiving-notifications"></a>Empfangen von Benachrichtigungen

Benachrichtigungen werden an den für ein Abonnement konfigurierten Webhook gesendet, sobald neuer Inhalt verfügbar ist. Da die Benachrichtigung die Mandanten-ID enthält, können Sie denselben Webhook zum Empfangen von Benachrichtigungen für alle Mandanten verwenden, für die Sie Abonnements haben.

Die Benachrichtigung erfolgt als HTTP POST über TLS (TLS 1.0 und höher) an die angegebenen Webhookadresse. Wenn die Webhookkonfiguration eine Auth-ID beinhaltet, wird sie als HTTP-Header gesendet: Webhook-AuthID. Andere Antworten als „HTTP 200 OK“ werden als Fehler betrachtet, und die Benachrichtigung wird wiederholt. Sie können den Webhook aus so konfigurieren, dass er eine auf Clientzertifikaten basierende Authentifizierung erfordert. Die Authentifizierung erfolgt dann über das manage.office.com-Zertifikat.

Der Text der Anforderung enthält ein Array mit einem oder mehreren JSON-Objekten, die die verfügbaren Inhalts-Blobs darstellen. Die Anzahl der Inhalts-Blobs in den Benachrichtigungen ist beschränkt, um die Größe der Benachrichtigung relativ klein zu halten. Da sich diese Beschränkung ändern kann, sollte die Implementierung die Länge des Arrays abfragen, anstatt eine feste Größe zu erwarten. Jedes Objekt enthält die gleichen, vom /content-Vorgang zurückgegebenen Eigenschaften zusammen mit der GUID des Mandanten, zu dem die Daten gehören, und der GUID der Anwendung, die die Abonnements erstellt hat. Dadurch kann der Webhook einen Kontext herstellen, wenn er mit mehreren Mandanten und Anwendungen verwendet wird.

- **tenantId**: Die GUID des Mandanten, zu dem der Inhalt gehört.
    
- **clientId**: Die GUID der Anwendung, die das Abonnement erstellt hat.
    
- **contentType**: Gibt den Inhaltstyp an.
    
- **contentId**: Eine verdeckte Zeichenfolge, die den Inhalt eindeutig identifiziert.
    
- **contentUri**: Die URL zum Abrufen von Inhalt.
    
- **contentCreated**: Datum und Uhrzeit, wann der Inhalt verfügbar wurde.
    
- **contentExpiration**: Datum und Uhrzeit, nach dem der Inhalt nicht mehr abgerufen werden kann.
    
Nachfolgend ist ein Beispiel für eine Benachrichtigung angegeben.

```json
POST https://webhook.myapp.com/o365/ 
Content-Type: application/json; utf-8
Webhook-AuthID: o365activityapinotification

[
    {
        "tenantId": "{GUID}"
        "clientId": "{GUID}"
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z"
    },
    ...
]

```


## <a name="notification-failure-and-retry"></a>Fehler bei Benachrichtigungen und Wiederholen

Das Benachrichtigungssystem sendet Benachrichtigungen, sobald neuer Inhalt verfügbar ist. Wenn wir beim Senden von Benachrichtigungen übermäßig viele Fehler auftreten, vergrößert unser Wiederholungsmechanismus die Zeit zwischen den Wiederholungsversuche beträchtlich. Wenn weiterhin Fehler auftreten, behalten wir uns das Recht vor, den Webhook zu deaktivieren und keine Benachrichtigungen mehr zu senden. Der /start-Vorgang kann verwendet werden, um einen deaktivierten Webhook wieder zu aktivieren.


## <a name="retrieving-content"></a>Abrufen von Inhalten

Um einen Inhalts-Blob abzurufen, führen Sie eine GET-Anforderung für den entsprechenden Inhalts-URI durch, der in der Liste der verfügbaren Inhalten und in den Benachrichtigungen, die an einen Webhook gesendet wurden, enthalten ist. Der zurückgegebene Inhalt ist eine Sammlung von Aktionen oder Ereignissen im JSON-Format.

#### <a name="sample-request"></a>Beispielanfrage

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a>Beispielantwort

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "CreationTime": "2015-06-29T20:03:19",
        "Id": "80c76bd2-9d81-4c57-a97a-accfc3443dca",
        "Operation": "PasswordLogonInitialAuthUsingPassword",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 9,
        "ResultStatus": "failed",
        "UserKey": "1153977025279851686@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ClientIP": "134.170.188.221",
        "ObjectId": "admin@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "ExtendedProperties": [
            {
                "Name": "LoginError",
                "Value": "-2147217390;PP_E_BAD_PASSWORD;The entered and stored passwords do not match."
            }
        ],
        "Client": "Exchange",
        "LoginStatus": -2147217390,
        "UserDomain": "contoso.onmicrosoft.com"
    },
    {
        "CreationTime": "2015-06-29T20:03:34",
        "Id": "4e655d3f-35fa-42e0-b050-264b2d255c7a",
        "Operation": "PasswordLogonInitialAuthUsingPassword",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 9,
        "ResultStatus": "success",
        "UserKey": "1153977025279851686@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ClientIP": "134.170.188.221",
        "ObjectId": "admin@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "Client": "Exchange",
        "LoginStatus": 0,
        "UserDomain": "contoso.onmicrosoft.com"
    },
    {
        "CreationTime": "2015-06-29T20:04:55",
        "Id": "b567caf0-088e-4c1c-a4ea-633a1e3d66c8",
        "Operation": "Add User.",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 8,
        "ResultStatus": "success",
        "UserKey": "1003BFFD8EC47CA6@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ObjectId": "user001@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "Actor": [
            {
                "ID": "1cef1fdb-ff52-48c4-8e4e-dfb5ea83d357",
                "Type": 2
            },
            {
                "ID": "admin@contoso.onmicrosoft.com",
                "Type": 5
            },
            {
                "ID": "1003BFFD8EC47CA6",
                "Type": 3
            }
        ],
        "ActorContextId": "41463f53-8812-40f4-890f-865bf6e35190",
        "InterSystemsId": "c2ced078-ad57-4079-a743-5c37f5284790",
        "IntraSystemId": "d1497f7e-15b4-49aa-83ad-11a17ca4a2f4",
        "Target": [
            {
                "ID": "user001@contoso.onmicrosoft.com",
                "Type": 5
            },
            {
                "ID": "10037FFE91510806",
                "Type": 3
            }
        ],
        "TargetContextId": "41463f53-8812-40f4-890f-865bf6e35190"
    }
]

```


## <a name="list-notifications"></a>Auflisten von Benachrichtigungen

Dieser Vorgang listet alle Benachrichtigungsversuche für den angegebenen Inhaltstyp auf. Wenn Sie beim Starten des Abonnements für den Inhaltstyp keinen Webhook angegeben haben, sind keine abzurufenden Benachrichtigungen verfügbar. Da bei Fehlern das Abrufen von Benachrichtigungen wiederholt wird, kann dieser Vorgang mehrere Benachrichtigungen für denselben Inhalt zurückgeben. Außerdem entspricht die Reihenfolge, in der die Benachrichtigungen gesendet werden, nicht unbedingt der Reihenfolge, in der die Inhalte verfügbar wurden (insbesondere dann, wenn Fehler und Wiederholungen vorliegen). 

Sie können diesen Vorgang verwenden, um Probleme im Zusammenhang mit Webhooks und Benachrichtigungen zu untersuchen. Verwenden Sie ihn jedoch nicht, um zu ermitteln, welcher Inhalt derzeit abgerufen werden kann. Verwenden Sie stattdessen den /content-Vorgang. Wenn der Abonnementstatus deaktiviert ist, wird ein Fehler zurückgegeben.


||Abonnement|Beschreibung|
|:-----|:-----|:-----|
|**Pfad**| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|**Parameter**|contentType|Muss ein gültiger Inhaltstyp sein.|
||PublisherIdentifier|Die Mandanten-GUID des Herstellers, der mit der API codiert. Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt. Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet. Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten. Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.|
||startTime endTime|Optionale Datums- und Uhrzeitangabe (UTC), die den Zeitraum angibt, in dem Inhalte zurückgegeben werden sollen, basierend darauf, wann der Inhalt verfügbar wurde. Der Zeitraum bezieht _startTime_ (_startTime_ < = contentCreated) mit ein, schließt die _endTime_ (_contentCreated_ < endTime) jedoch aus, damit nicht überlappende, inkrementierende Zeitintervalle zum Blättern durch den verfügbaren Inhalte verwendet werden können.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>YYYY-MM-DD</p></li><li><p>YYYY-MM-DDTHH:MM</p></li><li><p>YYYY-MM-DDTHH:MM:SS</p></li></ul>Es müssen beide angegeben werden (oder beide nicht angegeben werden), und die Zeitangaben dürfen nicht mehr als 24 Stunden auseinander liegen, wobei die Startzeit nicht mehr als sieben Tagen in der Vergangenheit liegen darf. Wenn _startTime_ und _endTime_ ausgelassen werden, wird standardmäßig der in den letzten 24 Stunden verfügbare Inhalt zurückgegeben.|
|**Antwort**|JSON-Array|Die Benachrichtigungen werden durch JSON-Objekte mit den folgenden Eigenschaften dargestellt: <ul><li>**contentType**: Gibt den Inhaltstyp an.</li><li>**contentId**: Eine verdeckte Zeichenfolge, die den Inhalt eindeutig identifiziert.</li><li>**contentUri**: Die URL zum Abrufen von Inhalt. </li><li>**contentCreated**: Datum und Uhrzeit, wann der Inhalt verfügbar wurde.</li><li>**contentExpiration**: Datum und Uhrzeit, nach dem der Inhalt nicht mehr abgerufen werden kann.</li><li>**notificationSent**: Datum und Uhrzeit des Sendens der Benachrichtigung.</li><li>**notificationStatus**: Gibt an, ob das Senden der Benachrichtigung erfolgreich war oder fehlgeschlagen ist.</li></ul>|

#### <a name="sample-request"></a>Beispielanfrage

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Beispielantwort

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z",
        "notificationSent": "2015-05-23T17:36:00.000Z",
        "notificationStatus": "success"

    },
    ...
]

```


### <a name="pagination"></a>Paginierung

Beim Auflisten des Benachrichtigungsverlaufs für einen Zeitraum wird die Anzahl der zurückgegebenen Ergebnisse beschränkt, um Zeitüberschreitungen bei der Antwort zu vermeiden. Wenn im angegebenen Zeitraum mehr Ergebnisse vorliegen, als in einer einzelnen Antwort zurückgegeben werden können, werden die Ergebnisse abgeschnitten und es wird ein Header zur Antwort hinzugefügt, der die URL zum Abrufen der nächsten Seite mit Ergebnissen angibt. Die URL enthält dieselben _startTime_- und _endTime_-Parameter, die in der ursprünglichen Anforderung angegeben wurden, zusammen mit einem Parameter, der die interne ID der nächsten Seite angibt. Wenn _startTime_ und _endTime_ in der ursprünglichen Anforderung nicht angegeben werden, werden sie auf ein 24-Stunden-Intervall festgelegt, das der ursprünglichen Anforderung voranging.

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

Um den gesamten verfügbaren Inhalt für einen angegebenen Zeitraum aufzulisten, müssen Sie möglicherweise mehrere Seiten abrufen, bis eine Antwort ohne den Header **NextPageUrl** empfangen wird.

## <a name="retrieve-resource-friendly-names"></a>Abrufen von Ressourcen-Anzeigenamen

Dieser Vorgang ruft Anzeigenamen für Objekte im Datenfeed ab, die durch GUIDs identifiziert werden. Derzeit wird nur das Objekt „DlpSensitiveType“ unterstützt. 


||Abonnement|Beschreibung|
|:-----|:-----|:-----|
|**Pfad**| `/resources/dlpSensitiveTypes`||
|**Parameter**|PublisherIdentifier|Die Mandanten-GUID des Herstellers, der mit der API codiert. Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt. Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet. Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten. Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.|
|**Headers**|Accept-Language|Header, der die gewünschte Sprache für lokalisierte Namen angibt. Verwenden Sie zum Beispiel „en-US“ für Englisch oder „es“ für Spanisch. Die Standardsprache (en-US) wird zurückgegeben, wenn dieser Header nicht vorhanden ist.|
|**Body**|(leer)||
|**Antwort**|JSON-Array|Die verfügbare Inhalte werden durch JSON-Objekte mit den folgenden Eigenschaften dargestellt:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>id</b>: Gibt die GUID des Typs für vertrauliche Informationen an.</p></li><li><p><b>name</b>: Der Anzeigename des Typs für vertrauliche Informationen.</p></li></ul>|

#### <a name="sample-request"></a>Beispielanfrage

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a>Beispielantwort

```json
HTTP/1.1 200 OK

[
    {
        "id": "50842eb7-edc8-4019-85dd-5a5c1f2bb085",
        "name": "CreditCardNumber"
    }, 
    {
        "id": "0e9b3178-9678-47dd-a509-37222ca96b42",
        "name": "EUDebitCardNumber"
    }, 
    ...
    {
    }
]

```

## <a name="api-throttling"></a>API-Drosselung

Jeder Hersteller, der mit der API codiert, hat ein dediziertes Kontingent für die Anforderungsdrosselung bei 60.000 pro Minute. Um das dedizierte Kontingent zu erhalten, geben Sie den Parameter „PublisherIdentifier“ in allen Anforderungen an. Anforderungen mit demselben „PublisherIdentifier“ verwenden gemeinsam dasselbe Kontingent. Alle Anforderungen, für die „PublisherIdentifier“ nicht angegeben ist, verwenden gemeinsam dasselbe Kontingent als GUID 00000000-0000-0000-0000-000000000000.

Wenn Office 365 bei bestimmten Problemen eine Eskalation zurück an Sie richten muss, stellen Sie sicher, dass das Abonnement für den Mandanten, dessen GUID Sie als „PublisherIdentifier“ verwenden, aktuell ist und die richtigen Kontaktinformationen aufweist. Für diesen Mandanten ist kein Abonnement erforderlich.

Kunden, die ihre eigenen Lösungen mit dieser API entwickeln, empfehlen wir die Verwendung einer eigenen Mandanten-GUID, damit es bei einem beschränkten gemeinsam genutzten Kontingent nicht zu Engpässen kommt.

> [!NOTE] 
> Obwohl jeder Herausgeber bis zu 60.000 Anforderungen pro Minute senden kann, kann Microsoft keine Antwortrate garantieren. Die Antwortrate hängt von verschiedenen Faktoren ab, z. B. der Leistung des Clientsystems, der Netzwerkkapazität und der Geschwindigkeit des Netzwerks.  Ein Herausgeber kann bis zu 60.000 Anforderungen pro Minute senden, kann jedoch nicht erwarten, für alle 60.000 Anforderungen innerhalb derselben Minute eine Antwort zu erhalten. Sollte ein Herausgeber ein Benchmarking für eine Clientanwendung erstellen wollen, sollte er dies sogar in den jeweiligen Umgebungen einzeln vornehmen, in denen er die Clientanwendung ausführen möchte, da sich die Ergebnisse je nach Umgebung unterscheiden.

## <a name="errors"></a>Fehler

Wenn der Dienst einen Fehler feststellt, meldet er den Fehlerantwortcode an den Aufrufer, und zwar mithilfe der standardmäßigen HTTP-Fehlercodesyntax. . Zusätzliche Informationen sind im Text des fehlgeschlagenen Aufrufs als einzelnes JSON-Objekt enthalten. Nachfolgend finden Sie ein Beispiel für einen vollständige JSON-Fehlertext: 

```json

{ 
    "error":{ 
        "code":"AF50000",
        "message": "An internal server error occurred. Retry the request."
    } 
}

```


|||
|:-----|:-----|
|Code|Nachricht|
|AF10001|Der Berechtigungssatz ({0}), der in der Anforderung gesendet wurde, enthielt nicht die erwartete Berechtigung **ActivityFeed.Read**.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = die im Zugriffstoken festgelegte Berechtigung.</p></li></ul>|
|AF20001|Fehlender Parameter: {0} <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = der Name des fehlenden Parameters.</p></li></ul>|
|AF20002|Ungültiger Parametertyp: {0} Erwarteter Typ: {1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = der Name des ungültigen Parameters.</p></li><li><p>{1} = der erwartete Typ (int, datetime, guid).</p></li></ul>|
|AF20003|Angegebener Ablauf {0} ist auf ein Datum und eine Uhrzeit in der Vergangenheit festgelegt.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = der im API-Aufruf übergebene Ablauf.</p></li></ul>|
|AF20010|Die in der URL ({0}) übergebene Mandanten-ID stimmt nicht mit der im Zugriffstoken ({1}) übergebenen Mandanten-ID überein.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = in der URL übergebene Mandanten-ID.</p></li><li><p>{1} = im Zugriffstoken übergebene Mandanten-ID.</p></li></ul>|
|AF20011|Angegebene Mandanten-ID ({0}) ist im System nicht vorhanden oder wurde gelöscht. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   {0} = in der URL übergebene Mandanten-ID.</p></li></ul>|
|AF20012|Angegebene Mandanten-ID ({0}) ist im System falsch konfiguriert. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    {0} = in der URL übergebene Mandanten-ID.</p></li></ul>|
|AF20013|Die in der URL ({0}) übergebene Mandanten-ID ist keine gültige GUID.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> {0} = in der URL übergebene Mandanten-ID.</p></li></ul>|
|AF20020|Der angegebene Inhaltstyp ist ungültig.|
|AF20021|Der Webhook-Endpunkt {{0}) konnte nicht überprüft werden. {1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = Webhookadresse.</p></li><li><p>{1} = „Der Endpunkt hat nicht HTTP 200 zurückgegeben.“ oder „Die Adresse muss mit HTTPS beginnen.“</p></li></ul>|
|AF20022|Kein Abonnement für den angegebenen Inhaltstyp gefunden.|
|AF20023|Das Abonnement wurde von {0} deaktiviert.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = „ein Mandant“ oder „ein Dienstadministrator“.</p></li></ul>|
|AF20030|Es muss sowohl die Startzeit als auch die Endzeit angegeben werden (oder beide nicht angegeben werden), und die Zeitangaben dürfen nicht mehr als 24 Stunden auseinander liegen, wobei die Startzeit nicht mehr als sieben Tagen in der Vergangenheit liegen darf.|
|AF20031|Ungültige nextPage-Eingabe: {0}.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = der in der URL übergebene Indikator für die nächste Seite</p></li></ul>|
|AF20050|Der angegebene Inhalt ({0}) ist nicht vorhanden.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = Ressourcen-ID oder Ressourcen-URL</p></li></ul>|
|AF20051|Mit dem Schlüssel {0} angeforderter Inhalt ist bereits abgelaufen. Inhalt, der älter als 7 Tage ist, kann nicht abgerufen werden.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>•    {0} = Ressourcen-ID oder Ressourcen-URL</p></li></ul>|
|AF20052|Inhalts-ID {0} in der URL ist ungültig.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = Ressourcen-ID oder Ressourcen-URL</p></li></ul>|
|AF20053|Im Header „Accept-Language“ darf nur eine Sprache vorhanden sein.|
|AF20054|Ungültige Syntax im Accept-Language-Header.|
|AF429|Zu viele Anforderungen. Method={0}, PublisherId={1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = HTTP-Methode</p></li><li><p>{1} = Mandanten-GUID, die als PublisherIdentifier verwendet wird.</p></li></ul>|
|AF50000|Ein interner Fehler ist aufgetreten. Wiederholen Sie die Anforderung.|
