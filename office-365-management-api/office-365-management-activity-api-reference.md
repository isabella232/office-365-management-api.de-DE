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
# <a name="office-365-management-activity-api-reference"></a><span data-ttu-id="7984a-103">Office 365-Verwaltungsaktivitäts-API – Referenz</span><span class="sxs-lookup"><span data-stu-id="7984a-103">Office 365 Management Activity API reference</span></span>

<span data-ttu-id="7984a-104">Verwenden Sie die Office 365-Verwaltungsaktivitäts-API zum Abrufen von Informationen über Benutzer-, Verwaltungs-, System- und Richtlinienaktionen und -ereignisse aus Office 365 und Azure AD-Aktivitätsprotokollen.</span><span class="sxs-lookup"><span data-stu-id="7984a-104">Use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Office 365 and Azure AD activity logs.</span></span> 

<span data-ttu-id="7984a-105">Sie können die Aktionen und Ereignisse aus den Office 365- und Microsoft Azure Active Directory-Überwachungs- und -Aktivitätsprotokollen verwenden, um Lösungen zu erstellen, die Überwachung, Analysen und Datenvisualisierung bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="7984a-105">You can use the actions and events from the Office 365 and Microsoft Azure Active Directory audit and activity logs to create solutions that provide monitoring, analysis, and data visualization.</span></span> <span data-ttu-id="7984a-106">Anhand dieser Lösungen haben Organisationen einen besseren Einblick in die Aktionen, die mit ihren Inhalten ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-106">These solutions give organizations greater visibility into actions taken on their content.</span></span> <span data-ttu-id="7984a-107">Diese Aktionen und Ereignisse sind auch in den Office 365-Aktivitätsberichten verfügbar.</span><span class="sxs-lookup"><span data-stu-id="7984a-107">These actions and events are also available in the Office 365 Activity Reports.</span></span> <span data-ttu-id="7984a-108">Weitere Informationen finden Sie unter [Durchsuchen des Überwachungsprotokolls im Office 365 Security & Compliance Center](https://support.office.com/de-DE/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span><span class="sxs-lookup"><span data-stu-id="7984a-108">For more information, see [Search the audit log in the Office 365 Security & Compliance Center](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span></span>

<span data-ttu-id="7984a-109">Die Office 365-Verwaltungsaktivitäts-API ist ein REST-Webdienst, mit dem Sie Lösungen in einer beliebigen Sprache und mit jeder Hosting-Umgebung, die HTTPS- und X.509-Zertifikate unterstützt, entwickeln können.</span><span class="sxs-lookup"><span data-stu-id="7984a-109">The Office 365 Management Activity API is a REST web service that you can use to develop solutions using any language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="7984a-110">Die API basiert auf Azure AD und dem OAuth2-Protokoll für Authentifizierung und Autorisierung.</span><span class="sxs-lookup"><span data-stu-id="7984a-110">The API relies on Azure AD and the OAuth2 protocol for authentication and authorization.</span></span> <span data-ttu-id="7984a-111">Um von Ihrer Anwendung aus auf die API zugreifen zu können, müssen Sie diese zuerst in Azure AD registrieren und dann mit den entsprechenden Berechtigungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7984a-111">To access the API from your application, you'll need to first register it in Azure AD and configure it with appropriate permissions.</span></span> <span data-ttu-id="7984a-112">Dadurch kann die Anwendung OAuth2-Zugriffstoken anfordern, die sie zum Aufrufen der API benötigt.</span><span class="sxs-lookup"><span data-stu-id="7984a-112">This will enable your application to request the OAuth2 access tokens it needs to call the API.</span></span> <span data-ttu-id="7984a-113">Weitere Informationen finden Sie unter [Erste Schritte mit den Office 365-Verwaltungs-APIs](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="7984a-113">For more information, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="7984a-114">Weitere Informationen über die Daten, die von der Office 365-Verwaltungsaktivitäts-API zurückgegeben werden, finden Sie unter [Office 365-Verwaltungsaktivitäts-API-Schema](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7984a-114">For information about the schema of the data that the Office 365 Management Activity API returns, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7984a-115">Bevor Sie über die Office 365-Verwaltungsaktivitäts-API auf Daten zugreifen können, müssen Sie die einheitliche Überwachungsprotokollierung für Ihre Office 365-Organisation aktivieren.</span><span class="sxs-lookup"><span data-stu-id="7984a-115">Before you can access data through the Office 365 Management Activity API, you must enable unified audit logging for your Office 365 organization.</span></span> <span data-ttu-id="7984a-116">Dazu aktivieren Sie das Office 365-Überwachungsprotokoll.</span><span class="sxs-lookup"><span data-stu-id="7984a-116">You do this by turning on the Office 365 audit log.</span></span> <span data-ttu-id="7984a-117">Weitere Anweisungen finden Sie unter [Aktivieren oder Deaktivieren der Office 365-Überwachungsprotokollsuche](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span><span class="sxs-lookup"><span data-stu-id="7984a-117">[Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off)</span></span>


## <a name="working-with-the-office-365-management-activity-api"></a><span data-ttu-id="7984a-118">Verwenden der Office 365-Verwaltungsaktivitäts-API</span><span class="sxs-lookup"><span data-stu-id="7984a-118">Working with the Office 365 Management Activity API</span></span>

<span data-ttu-id="7984a-119">Die Office 365-Verwaltungsaktivitäts-API aggregiert Aktionen und Ereignissen in mandantenspezifische Inhalts-Blobs, die durch den Typ und die Quelle der darin enthaltenen Inhalte klassifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-119">The Office 365 Management Activity API aggregates actions and events into tenant-specific content blobs, which are classified by the type and source of the content they contain.</span></span> <span data-ttu-id="7984a-120">Derzeit werden die folgenden Inhaltstypen unterstützt:</span><span class="sxs-lookup"><span data-stu-id="7984a-120">Currently, these content types are supported:</span></span>

- <span data-ttu-id="7984a-121">Audit.AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="7984a-121">Audit.AzureActiveDirectory</span></span>
    
- <span data-ttu-id="7984a-122">Audit.Exchange</span><span class="sxs-lookup"><span data-stu-id="7984a-122">Audit.Exchange</span></span>
    
- <span data-ttu-id="7984a-123">Audit.SharePoint</span><span class="sxs-lookup"><span data-stu-id="7984a-123">Audit.SharePoint</span></span>
    
- <span data-ttu-id="7984a-124">Audit.General (enthält alle anderen Workloads, die in den vorherigen Inhaltstypen nicht enthalten sind)</span><span class="sxs-lookup"><span data-stu-id="7984a-124">Audit.General (includes all other workloads not included in the previous content types)</span></span>

- <span data-ttu-id="7984a-125">DLP.All (nur DLP-Ereignisse für alle Workloads)</span><span class="sxs-lookup"><span data-stu-id="7984a-125">DLP.All (DLP events only for all workloads)</span></span>
    
<span data-ttu-id="7984a-126">Details zu den Ereignissen und Eigenschaften, die mit diesen Inhaltstypen verknüpft sind, finden Sie unter [Office 365-Verwaltungsaktivitäts-API-Schema](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7984a-126">For details about the events and properties associated with these content types, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

<span data-ttu-id="7984a-127">Um mit dem Abrufen von Inhalts-Blobs für einen Mandanten zu beginnen, erstellen Sie zuerst ein Abonnement für die gewünschten Inhaltstypen.</span><span class="sxs-lookup"><span data-stu-id="7984a-127">To begin retrieving content blobs for a tenant, you first a create subscription to the desired content types.</span></span> <span data-ttu-id="7984a-128">Wenn Sie Inhalts-Blobs für mehrere Mandanten abrufen möchten, erstellen Sie mehrere Abonnements für jeden der gewünschten Inhaltstypen, eines für jeden Mandanten.</span><span class="sxs-lookup"><span data-stu-id="7984a-128">If you are retrieving content blobs for multiple tenants, you create multiple subscriptions to each of the desired content types, one for each tenant.</span></span>

<span data-ttu-id="7984a-129">Nachdem Sie ein Abonnement erstellt haben, können Sie regelmäßig Abfragen durchführen, um neue Inhalts-Blobs zu finden, die zum Download zur Verfügung stehen. Sie können auch einen Endpunkt-Webhook mit dem Abonnement registrieren, und wir senden dann Benachrichtigungen an diesen Endpunkt, wenn neue Inhalts-Blobs verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="7984a-129">After you create a subscription, you can poll regularly to discover new content blobs that are available for download, or you can register a webhook endpoint with the subscription and we will send notifications to this endpoint as new content blobs are available.</span></span>


> [!NOTE] 
> <span data-ttu-id="7984a-130">Wenn Sie ein Abonnement erstellt wurde, kann es bis zu 12 Stunden dauern, bevor die ersten Inhalts-Blobs für dieses Abonnement verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="7984a-130">When a subscription is created, it can take up to 12 hours for the first content blobs to become available for that subscription.</span></span> <span data-ttu-id="7984a-131">Die Inhalts-Blobs werden durch das Sammeln und Aggregieren von Aktionen und Ereignissen für mehrere Server und Rechenzentren erstellt.</span><span class="sxs-lookup"><span data-stu-id="7984a-131">The content blobs are created by collecting and aggregating actions and events across multiple servers and datacenters.</span></span> <span data-ttu-id="7984a-132">Als Ergebnis dieses verteilten Vorgangs werden die Aktionen und Ereignisse in den Inhalts-Blobs nicht unbedingt in der Reihenfolge angezeigt, in der sie aufgetreten sind.</span><span class="sxs-lookup"><span data-stu-id="7984a-132">As a result of this distributed process, the actions and events contained in the content blobs will not necessarily appear in the order in which they occurred.</span></span> <span data-ttu-id="7984a-133">Ein Inhalts-Blob kann Aktionen und Ereignisse enthalten, die vor den Aktionen und Ereignissen aufgetreten sind, die in einem früheren Inhalts-Blob enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="7984a-133">One content blob can contain actions and events that occurred prior to the actions and events contained in an earlier content blob.</span></span> <span data-ttu-id="7984a-134">Wir arbeiten daran, die Zeitverzögerung zwischen dem Auftreten von Aktionen und Ereignissen und deren Verfügbarkeit in einem Inhalts-Blob zu verringern, können jedoch nicht garantieren, dass sie in Reihenfolge angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-134">We are working to decrease the latency between the occurrence of actions and events and their availability within a content blob, but we can't guarantee that they appear sequentially.</span></span>


> [!NOTE] 
> <span data-ttu-id="7984a-135">Vertrauliche DLP-Daten sind nur in der Aktivitätsfeed-API für Benutzer verfügbar, denen die Berechtigung „Lesen vertraulicher DLP-Daten“ erteilt wurde.</span><span class="sxs-lookup"><span data-stu-id="7984a-135">DLP sensitive data is only available in the activity feed API to users that have been granted “Read DLP sensitive data” permissions.</span></span> <span data-ttu-id="7984a-136">Weitere Informationen über die Verhinderung von Datenverlust (Data Loss Prevention, DLP) finden Sie unter [Übersicht über die Richtlinien zur Verhinderung von Datenverlust](https://support.office.com/de-DE/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span><span class="sxs-lookup"><span data-stu-id="7984a-136">For more on Data Loss Prevention (DLP) see [Overview of Data Loss Prevention Policies](https://support.office.com/en-us/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span></span>

## <a name="activity-api-operations"></a><span data-ttu-id="7984a-137">Aktivitäts-API-Vorgänge</span><span class="sxs-lookup"><span data-stu-id="7984a-137">Activity API operations</span></span>

<span data-ttu-id="7984a-138">Alle API-Vorgänge sind auf einen einzelnen Mandanten beschränkt, und die Stamm-URL der API enthält eine Mandanten-ID, die den Mandantenkontext angibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-138">All API operations are scoped to a single tenant and the root URL of the API includes a tenant ID that specifies the tenant context.</span></span> <span data-ttu-id="7984a-139">Die Mandanten-ID ist eine GUID.</span><span class="sxs-lookup"><span data-stu-id="7984a-139">The tenant ID is a GUID.</span></span> <span data-ttu-id="7984a-140">Informationen zum Abrufen der GUID finden Sie unter [Erste Schritte mit den Office 365-Verwaltungs-APIs](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="7984a-140">For information about how to get the GUID, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>


```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="7984a-141">Da die Benachrichtigungen, die wir an Ihren Webhook senden, die **Mandanten-ID** enthalten, können Sie denselben Webhook zum Empfangen von Benachrichtigungen für alle Mandanten verwenden.</span><span class="sxs-lookup"><span data-stu-id="7984a-141">Because the notifications we send to your webhook include the **tenant ID**, you can use the same webhook to receive notifications for all tenants.</span></span>

<span data-ttu-id="7984a-142">Alle API-Vorgänge erfordern einen Autorisierungs-HTTP-Header mit einem Zugriffstoken von Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7984a-142">All API operations require an Authorization HTTP header with an access token obtained from Azure AD.</span></span> <span data-ttu-id="7984a-143">Die Mandanten-ID im Zugriffstoken muss der Mandanten-ID in der Stamm-URL der API entsprechen, und das Zugriffstoken muss den Anspruch „ActivityFeed.Read“ enthalten. (Dies entspricht der Berechtigung [Aktivitätsdaten für eine Organisation lesen], die Sie für die Anwendung in Azure AD konfiguriert haben.)</span><span class="sxs-lookup"><span data-stu-id="7984a-143">The tenant ID in the access token must match the tenant ID in the root URL of the API and the access token must contain the ActivityFeed.Read claim (this corresponds to the permission [Read activity data for an organization] that you configured for you application in Azure AD).</span></span>

```json
Authorization: Bearer eyJ0e...Qa6wg
```

<span data-ttu-id="7984a-144">Die Aktivitäts-API unterstützt die folgenden Vorgänge:</span><span class="sxs-lookup"><span data-stu-id="7984a-144">The Activity API supports the following operations:</span></span>

- <span data-ttu-id="7984a-145">**Abonnement starten**, um Benachrichtigungen zu erhalten und Aktivitätsdaten für einen Mandanten abzurufen.</span><span class="sxs-lookup"><span data-stu-id="7984a-145">**Start a subscription** to begin receiving notifications and retrieving activity data for a tenant.</span></span>
    
- <span data-ttu-id="7984a-146">**Abonnement beenden**, um keine Daten für einen Mandanten mehr zu abzurufen.</span><span class="sxs-lookup"><span data-stu-id="7984a-146">**Stop a subscription** to discontinue retrieving data for a tenant.</span></span>
    
- <span data-ttu-id="7984a-147">**Aktuelle Abonnements auflisten**</span><span class="sxs-lookup"><span data-stu-id="7984a-147">**List current subscriptions**</span></span>
    
- <span data-ttu-id="7984a-148">**Verfügbare Inhalte auflisten**, sowie die entsprechenden Inhalts-URLs.</span><span class="sxs-lookup"><span data-stu-id="7984a-148">**List available content** and the corresponding content URLs.</span></span>
    
- <span data-ttu-id="7984a-149">**Benachrichtigungen erhalten**, die von einem Webhook gesendet werden, wenn neuer Inhalt verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="7984a-149">**Receiving notifications** sent by a webhook when new content is available.</span></span>
    
- <span data-ttu-id="7984a-150">**Inhalt abrufen** mithilfe der Inhalts-URL.</span><span class="sxs-lookup"><span data-stu-id="7984a-150">**Retrieving content** by using the content URL.</span></span>
    
- <span data-ttu-id="7984a-151">**Benachrichtigungen auflisten**, die von einem Webhook gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-151">**List notifications** sent by a webhook.</span></span>

- <span data-ttu-id="7984a-152">**Anzeigenamen für Ressourcen abrufen**, für Objekte im Datenfeed, die durch eine GUID identifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-152">**Retrieve resource friendly names** for objects in the data feed identified by guids.</span></span>
    

## <a name="start-a-subscription"></a><span data-ttu-id="7984a-153">Starten eines Abonnements</span><span class="sxs-lookup"><span data-stu-id="7984a-153">Start a subscription</span></span>

<span data-ttu-id="7984a-154">Dieser Vorgang beginnt mit dem Abonnement für den angegebenen Inhaltstyp.</span><span class="sxs-lookup"><span data-stu-id="7984a-154">This operation starts a subscription to the specified content type.</span></span> <span data-ttu-id="7984a-155">Wenn bereits ein Abonnement für den angegebenen Inhaltstyp vorhanden ist, wird dieser Vorgang für Folgendes verwendet:</span><span class="sxs-lookup"><span data-stu-id="7984a-155">If a subscription to the specified content type already exists, this operation is used to:</span></span>

- <span data-ttu-id="7984a-156">Aktualisieren der Eigenschaften eines aktiven Webhooks</span><span class="sxs-lookup"><span data-stu-id="7984a-156">Update the properties of an active webhook.</span></span>
    
- <span data-ttu-id="7984a-157">Aktivieren eines Webhooks, der aufgrund von übermäßig vielen fehlgeschlagenen Benachrichtigungen deaktiviert wurde</span><span class="sxs-lookup"><span data-stu-id="7984a-157">Enable a webhook that was disabled because of excessive failed notifications.</span></span>
    
- <span data-ttu-id="7984a-158">Erneutes Aktivieren eines abgelaufenen Webhooks durch Angabe eines späteren Ablaufdatums oder Angabe von „null“</span><span class="sxs-lookup"><span data-stu-id="7984a-158">Re-enable an expired webhook by specifying a later or null expiration date.</span></span>
    
- <span data-ttu-id="7984a-159">Entfernen eines Webhooks</span><span class="sxs-lookup"><span data-stu-id="7984a-159">Remove a webhook.</span></span>
    
||<span data-ttu-id="7984a-160">Abonnement</span><span class="sxs-lookup"><span data-stu-id="7984a-160">Subscription</span></span>|<span data-ttu-id="7984a-161">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7984a-161">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7984a-162">**Pfad**</span><span class="sxs-lookup"><span data-stu-id="7984a-162">**Path**</span></span>| `/subscriptions/start?contentType={ContentType}`||
|<span data-ttu-id="7984a-163">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="7984a-163">**Parameters**</span></span>|<span data-ttu-id="7984a-164">contentType</span><span class="sxs-lookup"><span data-stu-id="7984a-164">contentType</span></span>|<span data-ttu-id="7984a-165">Muss ein gültiger Inhaltstyp sein.</span><span class="sxs-lookup"><span data-stu-id="7984a-165">Must be a valid content type.</span></span>|
||<span data-ttu-id="7984a-166">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="7984a-166">PublisherIdentifier</span></span>|<span data-ttu-id="7984a-167">Die Mandanten-GUID des Herstellers, der mit der API codiert.</span><span class="sxs-lookup"><span data-stu-id="7984a-167">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="7984a-168">Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-168">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="7984a-169">Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet.</span><span class="sxs-lookup"><span data-stu-id="7984a-169">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="7984a-170">Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="7984a-170">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="7984a-171">Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.</span><span class="sxs-lookup"><span data-stu-id="7984a-171">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="7984a-172">**Body**</span><span class="sxs-lookup"><span data-stu-id="7984a-172">**Body**</span></span>|<span data-ttu-id="7984a-173">webhook</span><span class="sxs-lookup"><span data-stu-id="7984a-173">webhook</span></span>|<span data-ttu-id="7984a-174">Optionales JSON-Objekt mit drei Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="7984a-174">Optional JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-175"><b>address</b>: Erforderlicher HTTPS-Endpunkt, der Benachrichtigungen empfangen kann.</span><span class="sxs-lookup"><span data-stu-id="7984a-175"><b>address</b>: Required HTTPS endpoint that can receive notifications.</span></span>  <span data-ttu-id="7984a-176">Es wird eine Testnachricht an den Webhook gesendet, um ihn zu überprüfen, bevor das Abonnements erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="7984a-176">A test message will be sent to the webhook to validate the webhook before creating the subscription.</span></span></p></li><li><p><span data-ttu-id="7984a-177"><b>AuthId</b>: Optionale Zeichenfolge, die als WebHook-AuthID-Header in Benachrichtigungen einbezogen wird, die an den Webhook gesendet werden. Dies ist eine Methode zum Erkennen und Autorisieren der Quelle, aus der die Anforderung an den Webhook stammt.</span><span class="sxs-lookup"><span data-stu-id="7984a-177"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span></span></p></li><li><p><span data-ttu-id="7984a-178"><b>expiration</b>: Optionale datetime-Angabe, die ein Datum und eine Uhrzeit angibt, nach deren Ablauf keine Benachrichtigungen mehr an den Webhook gesendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="7984a-178"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span></span></p></li></ul>|
|<span data-ttu-id="7984a-179">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="7984a-179">**Response**</span></span>|<span data-ttu-id="7984a-180">contentType</span><span class="sxs-lookup"><span data-stu-id="7984a-180">contentType</span></span>|<span data-ttu-id="7984a-181">Der im Aufruf angegebene Inhaltstyp.</span><span class="sxs-lookup"><span data-stu-id="7984a-181">The content type specified in the call.</span></span>|
||<span data-ttu-id="7984a-182">status</span><span class="sxs-lookup"><span data-stu-id="7984a-182">status</span></span>|<span data-ttu-id="7984a-183">Der Status des Abonnements.</span><span class="sxs-lookup"><span data-stu-id="7984a-183">The status of the subscription.</span></span> <span data-ttu-id="7984a-184">Wenn ein Abonnement deaktiviert ist, können Sie keine Inhalte auflisten oder abrufen.</span><span class="sxs-lookup"><span data-stu-id="7984a-184">If a subscription is disabled, you will not be able to list or retrieve content.</span></span>|
||<span data-ttu-id="7984a-185">webhook</span><span class="sxs-lookup"><span data-stu-id="7984a-185">webhook</span></span>|<span data-ttu-id="7984a-186">Die im Aufruf angegeben Webhook Eigenschaften mit dem Status des Webhooks.</span><span class="sxs-lookup"><span data-stu-id="7984a-186">The webhook properties specified in the call together with the status of the webhook.</span></span> <span data-ttu-id="7984a-187">Wenn der Webhook deaktiviert ist, erhalten Sie keine Benachrichtigung. Sie können jedoch weiterhin Inhalt auflisten und abrufen, vorausgesetzt, das Abonnement ist  aktiviert.</span><span class="sxs-lookup"><span data-stu-id="7984a-187">If the webhook is disabled, you will not receive notification, but you will still be able to list and retrieve content, provided the subscription is enabled.</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="7984a-188">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="7984a-188">Sample request</span></span>

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


#### <a name="sample-response"></a><span data-ttu-id="7984a-189">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="7984a-189">Sample response</span></span>

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


## <a name="webhook-validation"></a><span data-ttu-id="7984a-190">Webhook-Überprüfung</span><span class="sxs-lookup"><span data-stu-id="7984a-190">Webhook validation</span></span>

<span data-ttu-id="7984a-191">Wenn der /start-Vorgang aufgerufen wird und ein Webhook angegeben ist, senden wir eine Überprüfungsbenachrichtigung an die angegebene Webhook-Adresse, um zu überprüfen, ob ein aktiver Listener die Benachrichtigungen annehmen und verarbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="7984a-191">When the /start operation is called and a webhook is specified, we will send a validation notification to the specified webhook address to validate that an active listener can accept and process notifications.</span></span> <span data-ttu-id="7984a-192">Wenn wir keine „HTTP 200 OK“-Antwort erhalten, wird das Abonnement nicht erstellt.</span><span class="sxs-lookup"><span data-stu-id="7984a-192">If we do not receive an HTTP 200 OK response, the subscription will not be created.</span></span> <span data-ttu-id="7984a-193">Wenn „/start“ alternativ aufgerufen wird, um einen Webhook zu einem vorhandenen Abonnement hinzuzufügen und die Antwort „HTTP 200 OK“ nicht empfangen wird, wird der Webhook nicht hinzugefügt, und das Abonnement bleibt unverändert.</span><span class="sxs-lookup"><span data-stu-id="7984a-193">Or, if /start is being called to add a webhook to an existing subscription and a response of HTTP 200 OK is not received, the webhook will not be added and the subscription will remain unchanged.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="7984a-194">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="7984a-194">Sample request</span></span>

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId, if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a><span data-ttu-id="7984a-195">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="7984a-195">Sample response</span></span>

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a><span data-ttu-id="7984a-196">Beenden eines Abonnements</span><span class="sxs-lookup"><span data-stu-id="7984a-196">Stop a subscription</span></span>

<span data-ttu-id="7984a-197">Dieser Vorgang beendet das Abonnement für den angegebenen Inhaltstyp.</span><span class="sxs-lookup"><span data-stu-id="7984a-197">This operation stops a subscription to the specified content type.</span></span> 

<span data-ttu-id="7984a-198">Wenn ein Abonnement beendet wird, erhalten Sie keine Benachrichtigungen mehr und Sie können keine verfügbaren Inhalte mehr abrufen.</span><span class="sxs-lookup"><span data-stu-id="7984a-198">When a subscription is stopped, you will no longer receive notifications and you will not be able to retrieve available content.</span></span> <span data-ttu-id="7984a-199">Wenn Sie das Abonnement später neu starten, haben Sie ab diesem Zeitpunkt Zugriff auf neue Inhalte.</span><span class="sxs-lookup"><span data-stu-id="7984a-199">If the subscription is later restarted, you will have access to new content from that point forward.</span></span> <span data-ttu-id="7984a-200">Sie können keinen Inhalt abrufen, der zwischen dem Beenden und erneuten Starten des Abonnements verfügbar war.</span><span class="sxs-lookup"><span data-stu-id="7984a-200">You will not be able to retrieve content that was available between the time the subscription was stopped and restarted.</span></span>


||<span data-ttu-id="7984a-201">Abonnement</span><span class="sxs-lookup"><span data-stu-id="7984a-201">Subscription</span></span>|<span data-ttu-id="7984a-202">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7984a-202">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7984a-203">**Pfad**</span><span class="sxs-lookup"><span data-stu-id="7984a-203">**Path**</span></span>| `/subscriptions/stop?contentType={ContentType}`||
|<span data-ttu-id="7984a-204">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="7984a-204">**Parameters**</span></span>|<span data-ttu-id="7984a-205">contentType</span><span class="sxs-lookup"><span data-stu-id="7984a-205">contentType</span></span>|<span data-ttu-id="7984a-206">Muss ein gültiger Inhaltstyp sein.</span><span class="sxs-lookup"><span data-stu-id="7984a-206">Must be a valid content type.</span></span>|
||<span data-ttu-id="7984a-207">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="7984a-207">PublisherIdentifier</span></span>|<span data-ttu-id="7984a-208">Die Mandanten-GUID des Herstellers, der mit der API codiert.</span><span class="sxs-lookup"><span data-stu-id="7984a-208">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="7984a-209">Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-209">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="7984a-210">Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet.</span><span class="sxs-lookup"><span data-stu-id="7984a-210">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="7984a-211">Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="7984a-211">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="7984a-212">Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.</span><span class="sxs-lookup"><span data-stu-id="7984a-212">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="7984a-213">**Body**</span><span class="sxs-lookup"><span data-stu-id="7984a-213">**Body**</span></span>|<span data-ttu-id="7984a-214">(leer)</span><span class="sxs-lookup"><span data-stu-id="7984a-214">(empty)</span></span>||
|<span data-ttu-id="7984a-215">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="7984a-215">**Response**</span></span>|<span data-ttu-id="7984a-216">(leer)</span><span class="sxs-lookup"><span data-stu-id="7984a-216">(empty)</span></span>|||

#### <a name="sample-request"></a><span data-ttu-id="7984a-217">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="7984a-217">Sample request</span></span>

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="7984a-218">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="7984a-218">Sample response</span></span>

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a><span data-ttu-id="7984a-219">Auflisten aktueller Abonnements</span><span class="sxs-lookup"><span data-stu-id="7984a-219">List current subscriptions</span></span>

<span data-ttu-id="7984a-220">Dieser Vorgang gibt eine Sammlung der aktuellen Abonnements zusammen mit den zugehörigen Webhooks zurück.</span><span class="sxs-lookup"><span data-stu-id="7984a-220">This operation returns a collection of the current subscriptions together with the associated webhooks.</span></span>

||<span data-ttu-id="7984a-221">Abonnement</span><span class="sxs-lookup"><span data-stu-id="7984a-221">Subscription</span></span>|<span data-ttu-id="7984a-222">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7984a-222">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7984a-223">**Pfad**</span><span class="sxs-lookup"><span data-stu-id="7984a-223">**Path**</span></span>| `/subscriptions/list`||
|<span data-ttu-id="7984a-224">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="7984a-224">**Parameters**</span></span>|<span data-ttu-id="7984a-225">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="7984a-225">PublisherIdentifier</span></span>|<span data-ttu-id="7984a-226">Die Mandanten-GUID des Herstellers, der mit der API codiert.</span><span class="sxs-lookup"><span data-stu-id="7984a-226">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="7984a-227">Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-227">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="7984a-228">Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet.</span><span class="sxs-lookup"><span data-stu-id="7984a-228">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="7984a-229">Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="7984a-229">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="7984a-230">Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.</span><span class="sxs-lookup"><span data-stu-id="7984a-230">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="7984a-231">**Body**</span><span class="sxs-lookup"><span data-stu-id="7984a-231">**Body**</span></span>|<span data-ttu-id="7984a-232">(leer)</span><span class="sxs-lookup"><span data-stu-id="7984a-232">(empty)</span></span>||
|<span data-ttu-id="7984a-233">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="7984a-233">**Response**</span></span>|<span data-ttu-id="7984a-234">JSON-Array</span><span class="sxs-lookup"><span data-stu-id="7984a-234">JSON array</span></span>|<span data-ttu-id="7984a-235">Jedes Abonnement wird durch ein JSON-Objekt mit drei Eigenschaften dargestellt:</span><span class="sxs-lookup"><span data-stu-id="7984a-235">Each subscription will be represented by a JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-236"><b>contentType</b>: Gibt den Inhaltstyp an.</span><span class="sxs-lookup"><span data-stu-id="7984a-236"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="7984a-237"><b>status</b>: Gibt den Status des Abonnements an.</span><span class="sxs-lookup"><span data-stu-id="7984a-237"><b>status</b>: Indicates the status of the subscription.</span></span></p></li><li><p><span data-ttu-id="7984a-238"><b>webhook</b>: Gibt den konfigurierten Webhook zusammen mit seinem Status an (aktiviert, deaktiviert, abgelaufen).</span><span class="sxs-lookup"><span data-stu-id="7984a-238"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.</span></span>  <span data-ttu-id="7984a-239">Wenn ein Abonnement keinen Webhook hat, ist die Webhook-Eigenschaft zwar vorhanden, hat jedoch den Wert „null“.</span><span class="sxs-lookup"><span data-stu-id="7984a-239">If a subscription does not have a webhook, the webhook property will be present but with null value.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="7984a-240">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="7984a-240">Sample request</span></span>

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="7984a-241">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="7984a-241">Sample response</span></span>

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


## <a name="list-available-content"></a><span data-ttu-id="7984a-242">Verfügbare Laufwerke auflisten</span><span class="sxs-lookup"><span data-stu-id="7984a-242">List available content</span></span>

<span data-ttu-id="7984a-243">Dieser Vorgang listet den Inhalt auf, der aktuell zum Abrufen für den angegebenen Inhaltstyp zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="7984a-243">This operation lists the content currently available for retrieval for the specified content type.</span></span> <span data-ttu-id="7984a-244">Der Inhalt ist eine Aggregation von Aktionen und Ereignissen, die von mehreren Servern in mehreren Rechenzentren abgerufen wurden.</span><span class="sxs-lookup"><span data-stu-id="7984a-244">The content is an aggregation of actions and events harvested from multiple servers across multiple datacenters.</span></span> <span data-ttu-id="7984a-245">Der Inhalt wird in der Reihenfolge aufgelistet, in der die Aggregationen verfügbar wird. Es kann jedoch nicht gewährleistet werden, dass die Ereignisse und Aktionen in den Aggregationen in der Reihenfolge des Auftretens aufgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-245">The content will be listed in the order in which the aggregations become available, but the events and actions within the aggregations are not guaranteed to be sequential.</span></span> <span data-ttu-id="7984a-246">Wenn der Abonnementstatus deaktiviert ist, wird ein Fehler zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="7984a-246">An error is returned if the subscription status is disabled.</span></span>


||<span data-ttu-id="7984a-247">Abonnement</span><span class="sxs-lookup"><span data-stu-id="7984a-247">Subscription</span></span>|<span data-ttu-id="7984a-248">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7984a-248">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7984a-249">**Pfad**</span><span class="sxs-lookup"><span data-stu-id="7984a-249">**Path**</span></span>| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="7984a-250">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="7984a-250">**Parameters**</span></span>|<span data-ttu-id="7984a-251">contentType</span><span class="sxs-lookup"><span data-stu-id="7984a-251">contentType</span></span>|<span data-ttu-id="7984a-252">Muss ein gültiger Inhaltstyp sein.</span><span class="sxs-lookup"><span data-stu-id="7984a-252">Must be a valid content type.</span></span>|
||<span data-ttu-id="7984a-253">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="7984a-253">PublisherIdentifier</span></span>|<span data-ttu-id="7984a-254">Die Mandanten-GUID des Herstellers, der mit der API codiert.</span><span class="sxs-lookup"><span data-stu-id="7984a-254">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="7984a-255">Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-255">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="7984a-256">Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet.</span><span class="sxs-lookup"><span data-stu-id="7984a-256">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="7984a-257">Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="7984a-257">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="7984a-258">Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.</span><span class="sxs-lookup"><span data-stu-id="7984a-258">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="7984a-259">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="7984a-259">startTime endTime</span></span>|<span data-ttu-id="7984a-260">Optionale Datums- und Uhrzeitangabe (UTC), die den Zeitraum angibt, in dem Inhalte zurückgegeben werden sollen, basierend darauf, wann der Inhalt verfügbar wurde.</span><span class="sxs-lookup"><span data-stu-id="7984a-260">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="7984a-261">Der Zeitraum bezieht die Startzeit (startTime < = contentCreated) mit ein, schließt die Endzeit (contentCreated < endTime) jedoch aus, damit nicht überlappende, inkrementierende Zeitintervalle zum Blättern durch den verfügbaren Inhalte verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="7984a-261">The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-262">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="7984a-262">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="7984a-263">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="7984a-263">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="7984a-264">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="7984a-264">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="7984a-265">Es müssen beide angegeben werden (oder beide nicht angegeben werden), und die Zeitangaben dürfen nicht mehr als 24 Stunden auseinander liegen, wobei die Startzeit nicht mehr als sieben Tagen in der Vergangenheit liegen darf.</span><span class="sxs-lookup"><span data-stu-id="7984a-265">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="7984a-266">Wenn „startTime“ und „endTime“ ausgelassen werden, wird standardmäßig der in den letzten 24 Stunden verfügbare Inhalt zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="7984a-266">By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span></span><p><span data-ttu-id="7984a-267">**HINWEIS**: Obwohl es möglich ist, eine Startzeit und Endzeit anzugeben, die mehr als 24 Stunden auseinander liegen, wird dies nicht empfohlen.</span><span class="sxs-lookup"><span data-stu-id="7984a-267">**NOTE**: Even though it is possible to specify a startTime and endTime more than 24 hours apart, this is not recommended.</span></span> <span data-ttu-id="7984a-268">Wenn Sie länger als 24 Stunden Ergebnisse als Antwort auf eine Anforderung erhalten, kann es sich hierbei außerdem nur um Teilergebnisse handeln, die nicht berücksichtigt werden sollten.</span><span class="sxs-lookup"><span data-stu-id="7984a-268">Furthermore, if you do get any results in response to a request for more than 24 hours, these could be partial results and should not be taken into account.</span></span> <span data-ttu-id="7984a-269">Die Anforderung sollte mit einem Intervall von nicht mehr als 24 Stunden zwischen der Startzeit und Endzeit ausgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-269">The request should be issued with an interval of no more than 24 hours between the startTime and endTime.</span></span></p>|
|<span data-ttu-id="7984a-270">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="7984a-270">**Response**</span></span>|<span data-ttu-id="7984a-271">JSON-Array</span><span class="sxs-lookup"><span data-stu-id="7984a-271">JSON array</span></span>|<span data-ttu-id="7984a-272">Die verfügbare Inhalte werden durch JSON-Objekte mit den folgenden Eigenschaften dargestellt:</span><span class="sxs-lookup"><span data-stu-id="7984a-272">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-273"><b>contentType</b>: Gibt den Inhaltstyp an.</span><span class="sxs-lookup"><span data-stu-id="7984a-273"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="7984a-274"><b>contentId</b>: Eine verdeckte Zeichenfolge, die den Inhalt eindeutig identifiziert.</span><span class="sxs-lookup"><span data-stu-id="7984a-274"><b>contentId</b>: An opaque string that uniquely identifies the content.</span></span></p></li><li><p><span data-ttu-id="7984a-275"><b>contentUri</b>: Die URL zum Abrufen von Inhalt.</span><span class="sxs-lookup"><span data-stu-id="7984a-275"><b>contentUri</b>: The URL to use when retrieving the content.</span></span></p></li><li><p><span data-ttu-id="7984a-276"><b>contentCreated</b>: Datum und Uhrzeit, wann der Inhalt verfügbar wurde.</span><span class="sxs-lookup"><span data-stu-id="7984a-276"><b>contentCreated</b>: The datetime when the content was made available.</span></span></p></li><li><p><span data-ttu-id="7984a-277"><b>contentExpiration</b>: Datum und Uhrzeit, nach dem der Inhalt nicht mehr abgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="7984a-277"><b>contentExpiration</b>: The datetime after which the content will no longer be available for retrieval.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="7984a-278">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="7984a-278">Sample request</span></span>

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="7984a-279">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="7984a-279">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="7984a-280">Paginierung</span><span class="sxs-lookup"><span data-stu-id="7984a-280">Pagination</span></span>

<span data-ttu-id="7984a-281">Beim Auflisten des Inhalts für einen Zeitraum wird die Anzahl der zurückgegebenen Ergebnisse beschränkt, um Zeitüberschreitungen bei der Antwort zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="7984a-281">When listing available content for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="7984a-282">Wenn im angegebenen Zeitraum mehr Ergebnisse vorliegen, als in einer einzelnen Antwort zurückgegeben werden können, werden die Ergebnisse abgeschnitten und es wird ein Header zur Antwort hinzugefügt, der die URL zum Abrufen der nächsten Seite mit Ergebnissen angibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-282">If there are more results in the specified time range than can be returned in single response, the results will be truncated and a header will be added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="7984a-283">Die URL enthält dieselben _startTime_- und _endTime_-Parameter, die in der ursprünglichen Anforderung angegeben wurden, zusammen mit einem Parameter, der die interne ID der nächsten Seite angibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-283">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="7984a-284">Wenn _startTime_ und _endTime_ in der ursprünglichen Anforderung nicht angegeben werden, werden sie auf ein 24-Stunden-Intervall festgelegt, das der ursprünglichen Anforderung voranging.</span><span class="sxs-lookup"><span data-stu-id="7984a-284">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="7984a-285">Um den gesamten verfügbaren Inhalt für einen angegebenen Zeitraum aufzulisten, müssen Sie möglicherweise mehrere Seiten abrufen, bis eine Antwort ohne den Header **NextPageUri** empfangen wird.</span><span class="sxs-lookup"><span data-stu-id="7984a-285">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>


## <a name="receiving-notifications"></a><span data-ttu-id="7984a-286">Empfangen von Benachrichtigungen</span><span class="sxs-lookup"><span data-stu-id="7984a-286">Receiving notifications</span></span>

<span data-ttu-id="7984a-287">Benachrichtigungen werden an den für ein Abonnement konfigurierten Webhook gesendet, sobald neuer Inhalt verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="7984a-287">Notifications are sent to the configured webhook for a subscription as new content becomes available.</span></span> <span data-ttu-id="7984a-288">Da die Benachrichtigung die Mandanten-ID enthält, können Sie denselben Webhook zum Empfangen von Benachrichtigungen für alle Mandanten verwenden, für die Sie Abonnements haben.</span><span class="sxs-lookup"><span data-stu-id="7984a-288">Because the notification includes the tenant identifier, you can use the same webhook to receive notifications for all tenants for which you have subscriptions.</span></span>

<span data-ttu-id="7984a-289">Die Benachrichtigung erfolgt als HTTP POST über TLS (TLS 1.0 und höher) an die angegebenen Webhookadresse.</span><span class="sxs-lookup"><span data-stu-id="7984a-289">The notification is made as an HTTP POST over TLS (TLS 1.0 and later versions) to the specified webhook address.</span></span> <span data-ttu-id="7984a-290">Wenn die Webhookkonfiguration eine Auth-ID beinhaltet, wird sie als HTTP-Header gesendet: Webhook-AuthID.</span><span class="sxs-lookup"><span data-stu-id="7984a-290">If the webhook configuration includes an auth ID, we will send it as an HTTP header: Webhook-AuthID.</span></span> <span data-ttu-id="7984a-291">Andere Antworten als „HTTP 200 OK“ werden als Fehler betrachtet, und die Benachrichtigung wird wiederholt.</span><span class="sxs-lookup"><span data-stu-id="7984a-291">Any response other than HTTP 200 OK will be considered a failure and the notification will be retried.</span></span> <span data-ttu-id="7984a-292">Sie können den Webhook aus so konfigurieren, dass er eine auf Clientzertifikaten basierende Authentifizierung erfordert. Die Authentifizierung erfolgt dann über das manage.office.com-Zertifikat.</span><span class="sxs-lookup"><span data-stu-id="7984a-292">You can also configure your webhook to require client certificate-based authentication and we will authenticate using the manage.office.com certificate.</span></span>

<span data-ttu-id="7984a-293">Der Text der Anforderung enthält ein Array mit einem oder mehreren JSON-Objekten, die die verfügbaren Inhalts-Blobs darstellen.</span><span class="sxs-lookup"><span data-stu-id="7984a-293">The body of the request will contain an array of one or more JSON objects that represent the available content blobs.</span></span> <span data-ttu-id="7984a-294">Die Anzahl der Inhalts-Blobs in den Benachrichtigungen ist beschränkt, um die Größe der Benachrichtigung relativ klein zu halten.</span><span class="sxs-lookup"><span data-stu-id="7984a-294">The number of content blobs in each notification is limited to keep the size of the notification relatively small.</span></span> <span data-ttu-id="7984a-295">Da sich diese Beschränkung ändern kann, sollte die Implementierung die Länge des Arrays abfragen, anstatt eine feste Größe zu erwarten.</span><span class="sxs-lookup"><span data-stu-id="7984a-295">Because this limit might change, your implementation should query for the length of the array instead of expecting a fixed size.</span></span> <span data-ttu-id="7984a-296">Jedes Objekt enthält die gleichen, vom /content-Vorgang zurückgegebenen Eigenschaften zusammen mit der GUID des Mandanten, zu dem die Daten gehören, und der GUID der Anwendung, die die Abonnements erstellt hat.</span><span class="sxs-lookup"><span data-stu-id="7984a-296">Each object will include the same properties returned by the /content operation, together with the GUID of the tenant to which the data belongs and the GUID of your application that created the subscriptions.</span></span> <span data-ttu-id="7984a-297">Dadurch kann der Webhook einen Kontext herstellen, wenn er mit mehreren Mandanten und Anwendungen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7984a-297">This allows the webhook to establish context when it is being used with multiple tenants and applications.</span></span>

- <span data-ttu-id="7984a-298">**tenantId**: Die GUID des Mandanten, zu dem der Inhalt gehört.</span><span class="sxs-lookup"><span data-stu-id="7984a-298">**tenantId**: The GUID of the tenant to which the content belongs.</span></span>
    
- <span data-ttu-id="7984a-299">**clientId**: Die GUID der Anwendung, die das Abonnement erstellt hat.</span><span class="sxs-lookup"><span data-stu-id="7984a-299">**clientId**: The GUID of your application that created the subscription.</span></span>
    
- <span data-ttu-id="7984a-300">**contentType**: Gibt den Inhaltstyp an.</span><span class="sxs-lookup"><span data-stu-id="7984a-300">**contentType**: Indicates the content type.</span></span>
    
- <span data-ttu-id="7984a-301">**contentId**: Eine verdeckte Zeichenfolge, die den Inhalt eindeutig identifiziert.</span><span class="sxs-lookup"><span data-stu-id="7984a-301">**contentId**: An opaque string that uniquely identifies the content.</span></span>
    
- <span data-ttu-id="7984a-302">**contentUri**: Die URL zum Abrufen von Inhalt.</span><span class="sxs-lookup"><span data-stu-id="7984a-302">**contentUri**: The URL to use when retrieving the content.</span></span>
    
- <span data-ttu-id="7984a-303">**contentCreated**: Datum und Uhrzeit, wann der Inhalt verfügbar wurde.</span><span class="sxs-lookup"><span data-stu-id="7984a-303">**contentCreated**: The datetime when the content was made available.</span></span>
    
- <span data-ttu-id="7984a-304">**contentExpiration**: Datum und Uhrzeit, nach dem der Inhalt nicht mehr abgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="7984a-304">**contentExpiration**: The datetime after which the content will no longer be available for retrieval.</span></span>
    
<span data-ttu-id="7984a-305">Nachfolgend ist ein Beispiel für eine Benachrichtigung angegeben.</span><span class="sxs-lookup"><span data-stu-id="7984a-305">The following is an example of a notification.</span></span>

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


## <a name="notification-failure-and-retry"></a><span data-ttu-id="7984a-306">Fehler bei Benachrichtigungen und Wiederholen</span><span class="sxs-lookup"><span data-stu-id="7984a-306">Notification failure and retry</span></span>

<span data-ttu-id="7984a-307">Das Benachrichtigungssystem sendet Benachrichtigungen, sobald neuer Inhalt verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="7984a-307">The notification system sends notifications as new content becomes available.</span></span> <span data-ttu-id="7984a-308">Wenn wir beim Senden von Benachrichtigungen übermäßig viele Fehler auftreten, vergrößert unser Wiederholungsmechanismus die Zeit zwischen den Wiederholungsversuche beträchtlich.</span><span class="sxs-lookup"><span data-stu-id="7984a-308">If we encounter excessive failures when sending notifications, our retry mechanism will exponentially increase the time between retries.</span></span> <span data-ttu-id="7984a-309">Wenn weiterhin Fehler auftreten, behalten wir uns das Recht vor, den Webhook zu deaktivieren und keine Benachrichtigungen mehr zu senden.</span><span class="sxs-lookup"><span data-stu-id="7984a-309">If we continue to encounter failures, we reserve the right to disable the webhook and stop sending notifications to it altogether.</span></span> <span data-ttu-id="7984a-310">Der /start-Vorgang kann verwendet werden, um einen deaktivierten Webhook wieder zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="7984a-310">The /start operation can be used to re-enable a disabled webhook.</span></span>


## <a name="retrieving-content"></a><span data-ttu-id="7984a-311">Abrufen von Inhalten</span><span class="sxs-lookup"><span data-stu-id="7984a-311">Retrieving content</span></span>

<span data-ttu-id="7984a-312">Um einen Inhalts-Blob abzurufen, führen Sie eine GET-Anforderung für den entsprechenden Inhalts-URI durch, der in der Liste der verfügbaren Inhalten und in den Benachrichtigungen, die an einen Webhook gesendet wurden, enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="7984a-312">To retrieve a content blob, make a GET request against the corresponding content URI that is included in the list of available content and in the notifications sent to a webhook.</span></span> <span data-ttu-id="7984a-313">Der zurückgegebene Inhalt ist eine Sammlung von Aktionen oder Ereignissen im JSON-Format.</span><span class="sxs-lookup"><span data-stu-id="7984a-313">The returned content will be a collection of one more actions or events in JSON format.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="7984a-314">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="7984a-314">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a><span data-ttu-id="7984a-315">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="7984a-315">Sample response</span></span>

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


## <a name="list-notifications"></a><span data-ttu-id="7984a-316">Auflisten von Benachrichtigungen</span><span class="sxs-lookup"><span data-stu-id="7984a-316">List notifications</span></span>

<span data-ttu-id="7984a-317">Dieser Vorgang listet alle Benachrichtigungsversuche für den angegebenen Inhaltstyp auf.</span><span class="sxs-lookup"><span data-stu-id="7984a-317">This operation lists all notification attempts for the specified content type.</span></span> <span data-ttu-id="7984a-318">Wenn Sie beim Starten des Abonnements für den Inhaltstyp keinen Webhook angegeben haben, sind keine abzurufenden Benachrichtigungen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="7984a-318">If you did not include a webhook when starting the subscription to the content type, there will be no notifications to retrieve.</span></span> <span data-ttu-id="7984a-319">Da bei Fehlern das Abrufen von Benachrichtigungen wiederholt wird, kann dieser Vorgang mehrere Benachrichtigungen für denselben Inhalt zurückgeben. Außerdem entspricht die Reihenfolge, in der die Benachrichtigungen gesendet werden, nicht unbedingt der Reihenfolge, in der die Inhalte verfügbar wurden (insbesondere dann, wenn Fehler und Wiederholungen vorliegen).</span><span class="sxs-lookup"><span data-stu-id="7984a-319">Because we retry notifications in the event of failure, this operation can return multiple notifications for the same content, and the order in which the notifications are sent will not necessarily match the order in which the content became available (especially when there are failures and retries).</span></span> 

<span data-ttu-id="7984a-320">Sie können diesen Vorgang verwenden, um Probleme im Zusammenhang mit Webhooks und Benachrichtigungen zu untersuchen. Verwenden Sie ihn jedoch nicht, um zu ermitteln, welcher Inhalt derzeit abgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="7984a-320">You can use this operation to help investigate issues related to webhooks and notifications, but you should not use it to determine what content is currently available for retrieval.</span></span> <span data-ttu-id="7984a-321">Verwenden Sie stattdessen den /content-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="7984a-321">Use the /content operation instead.</span></span> <span data-ttu-id="7984a-322">Wenn der Abonnementstatus deaktiviert ist, wird ein Fehler zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="7984a-322">We return an error if the subscription status is disabled.</span></span>


||<span data-ttu-id="7984a-323">Abonnement</span><span class="sxs-lookup"><span data-stu-id="7984a-323">Subscription</span></span>|<span data-ttu-id="7984a-324">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7984a-324">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7984a-325">**Pfad**</span><span class="sxs-lookup"><span data-stu-id="7984a-325">**Path**</span></span>| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="7984a-326">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="7984a-326">**Parameters**</span></span>|<span data-ttu-id="7984a-327">contentType</span><span class="sxs-lookup"><span data-stu-id="7984a-327">contentType</span></span>|<span data-ttu-id="7984a-328">Muss ein gültiger Inhaltstyp sein.</span><span class="sxs-lookup"><span data-stu-id="7984a-328">Must be a valid content type.</span></span>|
||<span data-ttu-id="7984a-329">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="7984a-329">PublisherIdentifier</span></span>|<span data-ttu-id="7984a-330">Die Mandanten-GUID des Herstellers, der mit der API codiert.</span><span class="sxs-lookup"><span data-stu-id="7984a-330">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="7984a-331">Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-331">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="7984a-332">Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet.</span><span class="sxs-lookup"><span data-stu-id="7984a-332">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="7984a-333">Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="7984a-333">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="7984a-334">Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.</span><span class="sxs-lookup"><span data-stu-id="7984a-334">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="7984a-335">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="7984a-335">startTime endTime</span></span>|<span data-ttu-id="7984a-336">Optionale Datums- und Uhrzeitangabe (UTC), die den Zeitraum angibt, in dem Inhalte zurückgegeben werden sollen, basierend darauf, wann der Inhalt verfügbar wurde.</span><span class="sxs-lookup"><span data-stu-id="7984a-336">Optional datetimes (UTC) that indicate the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="7984a-337">Der Zeitraum bezieht _startTime_ (_startTime_ < = contentCreated) mit ein, schließt die _endTime_ (_contentCreated_ < endTime) jedoch aus, damit nicht überlappende, inkrementierende Zeitintervalle zum Blättern durch den verfügbaren Inhalte verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="7984a-337">The time range is inclusive with respect to  _startTime_ ( _startTime_ <= contentCreated) and exclusive with respect to _endTime_ (_contentCreated_ < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-338">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="7984a-338">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="7984a-339">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="7984a-339">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="7984a-340">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="7984a-340">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="7984a-341">Es müssen beide angegeben werden (oder beide nicht angegeben werden), und die Zeitangaben dürfen nicht mehr als 24 Stunden auseinander liegen, wobei die Startzeit nicht mehr als sieben Tagen in der Vergangenheit liegen darf.</span><span class="sxs-lookup"><span data-stu-id="7984a-341">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="7984a-342">Wenn _startTime_ und _endTime_ ausgelassen werden, wird standardmäßig der in den letzten 24 Stunden verfügbare Inhalt zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="7984a-342">By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span></span>|
|<span data-ttu-id="7984a-343">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="7984a-343">**Response**</span></span>|<span data-ttu-id="7984a-344">JSON-Array</span><span class="sxs-lookup"><span data-stu-id="7984a-344">JSON array</span></span>|<span data-ttu-id="7984a-345">Die Benachrichtigungen werden durch JSON-Objekte mit den folgenden Eigenschaften dargestellt:</span><span class="sxs-lookup"><span data-stu-id="7984a-345">The notifications will be represented by JSON objects with the following properties:</span></span> <ul><li><span data-ttu-id="7984a-346">**contentType**: Gibt den Inhaltstyp an.</span><span class="sxs-lookup"><span data-stu-id="7984a-346">**contentType**: indicates the content type.</span></span></li><li><span data-ttu-id="7984a-347">**contentId**: Eine verdeckte Zeichenfolge, die den Inhalt eindeutig identifiziert.</span><span class="sxs-lookup"><span data-stu-id="7984a-347">**contentId**: an opaque string that uniquely identifies the content.</span></span></li><li><span data-ttu-id="7984a-348">**contentUri**: Die URL zum Abrufen von Inhalt.</span><span class="sxs-lookup"><span data-stu-id="7984a-348">**contentUri**: the URL to use when retrieving the content.</span></span> </li><li><span data-ttu-id="7984a-349">**contentCreated**: Datum und Uhrzeit, wann der Inhalt verfügbar wurde.</span><span class="sxs-lookup"><span data-stu-id="7984a-349">**contentCreated**: the datetime when the content was made available.</span></span></li><li><span data-ttu-id="7984a-350">**contentExpiration**: Datum und Uhrzeit, nach dem der Inhalt nicht mehr abgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="7984a-350">**contentExpiration**: the datetime after which the content will no longer be available for retrieval.</span></span></li><li><span data-ttu-id="7984a-351">**notificationSent**: Datum und Uhrzeit des Sendens der Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="7984a-351">**notificationSent**: the datetime when the notification was sent.</span></span></li><li><span data-ttu-id="7984a-352">**notificationStatus**: Gibt an, ob das Senden der Benachrichtigung erfolgreich war oder fehlgeschlagen ist.</span><span class="sxs-lookup"><span data-stu-id="7984a-352">**notificationStatus**: indicates the success or failure of the notification attempt.</span></span></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="7984a-353">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="7984a-353">Sample request</span></span>

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="7984a-354">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="7984a-354">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="7984a-355">Paginierung</span><span class="sxs-lookup"><span data-stu-id="7984a-355">Pagination</span></span>

<span data-ttu-id="7984a-356">Beim Auflisten des Benachrichtigungsverlaufs für einen Zeitraum wird die Anzahl der zurückgegebenen Ergebnisse beschränkt, um Zeitüberschreitungen bei der Antwort zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="7984a-356">When listing notification history for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="7984a-357">Wenn im angegebenen Zeitraum mehr Ergebnisse vorliegen, als in einer einzelnen Antwort zurückgegeben werden können, werden die Ergebnisse abgeschnitten und es wird ein Header zur Antwort hinzugefügt, der die URL zum Abrufen der nächsten Seite mit Ergebnissen angibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-357">If there are more results in the specified time range than can be returned in a single response, the results are truncated and a header is added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="7984a-358">Die URL enthält dieselben _startTime_- und _endTime_-Parameter, die in der ursprünglichen Anforderung angegeben wurden, zusammen mit einem Parameter, der die interne ID der nächsten Seite angibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-358">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="7984a-359">Wenn _startTime_ und _endTime_ in der ursprünglichen Anforderung nicht angegeben werden, werden sie auf ein 24-Stunden-Intervall festgelegt, das der ursprünglichen Anforderung voranging.</span><span class="sxs-lookup"><span data-stu-id="7984a-359">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="7984a-360">Um den gesamten verfügbaren Inhalt für einen angegebenen Zeitraum aufzulisten, müssen Sie möglicherweise mehrere Seiten abrufen, bis eine Antwort ohne den Header **NextPageUrl** empfangen wird.</span><span class="sxs-lookup"><span data-stu-id="7984a-360">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUrl** header is received.</span></span>

## <a name="retrieve-resource-friendly-names"></a><span data-ttu-id="7984a-361">Abrufen von Ressourcen-Anzeigenamen</span><span class="sxs-lookup"><span data-stu-id="7984a-361">Retrieve resource friendly names</span></span>

<span data-ttu-id="7984a-362">Dieser Vorgang ruft Anzeigenamen für Objekte im Datenfeed ab, die durch GUIDs identifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-362">This operation retrieves friendly names for objects in the data feed identified by guids.</span></span> <span data-ttu-id="7984a-363">Derzeit wird nur das Objekt „DlpSensitiveType“ unterstützt.</span><span class="sxs-lookup"><span data-stu-id="7984a-363">Currently "DlpSensitiveType" is the only supported object.</span></span> 


||<span data-ttu-id="7984a-364">Abonnement</span><span class="sxs-lookup"><span data-stu-id="7984a-364">Subscription</span></span>|<span data-ttu-id="7984a-365">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7984a-365">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7984a-366">**Pfad**</span><span class="sxs-lookup"><span data-stu-id="7984a-366">**Path**</span></span>| `/resources/dlpSensitiveTypes`||
|<span data-ttu-id="7984a-367">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="7984a-367">**Parameters**</span></span>|<span data-ttu-id="7984a-368">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="7984a-368">PublisherIdentifier</span></span>|<span data-ttu-id="7984a-369">Die Mandanten-GUID des Herstellers, der mit der API codiert.</span><span class="sxs-lookup"><span data-stu-id="7984a-369">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="7984a-370">Dies ist **nicht** die Anwendungs-GUID oder die GUID des Kunden, der die Anwendung nutzt, sondern die GUID des Unternehmens, das den Code schreibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-370">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="7984a-371">Dieser Parameter wird zum Drosseln der Anforderungsrate verwendet.</span><span class="sxs-lookup"><span data-stu-id="7984a-371">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="7984a-372">Stellen Sie sicher, dass dieser Parameter in allen ausgegebenen Anforderungen angegeben ist, um ein dediziertes Kontingent zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="7984a-372">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="7984a-373">Alle Anforderungen, die ohne diesen Parameter empfangen werden, teilen sich dasselbe Kontingent.</span><span class="sxs-lookup"><span data-stu-id="7984a-373">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="7984a-374">**Headers**</span><span class="sxs-lookup"><span data-stu-id="7984a-374">**Headers**</span></span>|<span data-ttu-id="7984a-375">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="7984a-375">Accept-Language</span></span>|<span data-ttu-id="7984a-376">Header, der die gewünschte Sprache für lokalisierte Namen angibt.</span><span class="sxs-lookup"><span data-stu-id="7984a-376">Header to specify the desired language for localized names.</span></span> <span data-ttu-id="7984a-377">Verwenden Sie zum Beispiel „en-US“ für Englisch oder „es“ für Spanisch.</span><span class="sxs-lookup"><span data-stu-id="7984a-377">For example, use "en-US" for English or "es" for Spanish.</span></span> <span data-ttu-id="7984a-378">Die Standardsprache (en-US) wird zurückgegeben, wenn dieser Header nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="7984a-378">The default language (en-US) will be returned if this header is not present.</span></span>|
|<span data-ttu-id="7984a-379">**Body**</span><span class="sxs-lookup"><span data-stu-id="7984a-379">**Body**</span></span>|<span data-ttu-id="7984a-380">(leer)</span><span class="sxs-lookup"><span data-stu-id="7984a-380">(empty)</span></span>||
|<span data-ttu-id="7984a-381">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="7984a-381">**Response**</span></span>|<span data-ttu-id="7984a-382">JSON-Array</span><span class="sxs-lookup"><span data-stu-id="7984a-382">JSON array</span></span>|<span data-ttu-id="7984a-383">Die verfügbare Inhalte werden durch JSON-Objekte mit den folgenden Eigenschaften dargestellt:</span><span class="sxs-lookup"><span data-stu-id="7984a-383">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-384"><b>id</b>: Gibt die GUID des Typs für vertrauliche Informationen an.</span><span class="sxs-lookup"><span data-stu-id="7984a-384"><b>id</b>: Indicates the guid of the sensitive information type.</span></span></p></li><li><p><span data-ttu-id="7984a-385"><b>name</b>: Der Anzeigename des Typs für vertrauliche Informationen.</span><span class="sxs-lookup"><span data-stu-id="7984a-385"><b>name</b>: The friendly name of the sensitive information type.</span></span></p></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="7984a-386">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="7984a-386">Sample request</span></span>

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a><span data-ttu-id="7984a-387">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="7984a-387">Sample response</span></span>

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

## <a name="api-throttling"></a><span data-ttu-id="7984a-388">API-Drosselung</span><span class="sxs-lookup"><span data-stu-id="7984a-388">API throttling</span></span>

<span data-ttu-id="7984a-389">Jeder Hersteller, der mit der API codiert, hat ein dediziertes Kontingent für die Anforderungsdrosselung bei 60.000 pro Minute.</span><span class="sxs-lookup"><span data-stu-id="7984a-389">Each vendor coding against the API has a dedicated quota for request throttling at 60K per minute.</span></span> <span data-ttu-id="7984a-390">Um das dedizierte Kontingent zu erhalten, geben Sie den Parameter „PublisherIdentifier“ in allen Anforderungen an.</span><span class="sxs-lookup"><span data-stu-id="7984a-390">To get the dedicated quota, specify the parameter PublisherIdentifier in all your requests.</span></span> <span data-ttu-id="7984a-391">Anforderungen mit demselben „PublisherIdentifier“ verwenden gemeinsam dasselbe Kontingent.</span><span class="sxs-lookup"><span data-stu-id="7984a-391">Requests with the same PublisherIdentifier will share the same quota.</span></span> <span data-ttu-id="7984a-392">Alle Anforderungen, für die „PublisherIdentifier“ nicht angegeben ist, verwenden gemeinsam dasselbe Kontingent als GUID 00000000-0000-0000-0000-000000000000.</span><span class="sxs-lookup"><span data-stu-id="7984a-392">All requests without the PublisherIdentifier specified will share the same quota as GUID 00000000-0000-0000-0000-000000000000.</span></span>

<span data-ttu-id="7984a-393">Wenn Office 365 bei bestimmten Problemen eine Eskalation zurück an Sie richten muss, stellen Sie sicher, dass das Abonnement für den Mandanten, dessen GUID Sie als „PublisherIdentifier“ verwenden, aktuell ist und die richtigen Kontaktinformationen aufweist.</span><span class="sxs-lookup"><span data-stu-id="7984a-393">If Office 365 needs to reverse escalate to you in certain issues, make sure the subscription for the tenant whose GUID is used as your PublisherIdentifier is current and updated with the correct contact information.</span></span> <span data-ttu-id="7984a-394">Für diesen Mandanten ist kein Abonnement erforderlich.</span><span class="sxs-lookup"><span data-stu-id="7984a-394">There is no subscription requirement for this tenant.</span></span>

<span data-ttu-id="7984a-395">Kunden, die ihre eigenen Lösungen mit dieser API entwickeln, empfehlen wir die Verwendung einer eigenen Mandanten-GUID, damit es bei einem beschränkten gemeinsam genutzten Kontingent nicht zu Engpässen kommt.</span><span class="sxs-lookup"><span data-stu-id="7984a-395">For customers who are developing their own solutions using this API, we recommend using your own tenant GUID to avoid competition caused by a limited shared quota.</span></span>

> [!NOTE] 
> <span data-ttu-id="7984a-396">Obwohl jeder Herausgeber bis zu 60.000 Anforderungen pro Minute senden kann, kann Microsoft keine Antwortrate garantieren.</span><span class="sxs-lookup"><span data-stu-id="7984a-396">Even though each publisher can submit up to 60K requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="7984a-397">Die Antwortrate hängt von verschiedenen Faktoren ab, z. B. der Leistung des Clientsystems, der Netzwerkkapazität und der Geschwindigkeit des Netzwerks.</span><span class="sxs-lookup"><span data-stu-id="7984a-397">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span>  <span data-ttu-id="7984a-398">Ein Herausgeber kann bis zu 60.000 Anforderungen pro Minute senden, kann jedoch nicht erwarten, für alle 60.000 Anforderungen innerhalb derselben Minute eine Antwort zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="7984a-398">A publisher can submit up to 60K requests per minute, but should not expect to receive responses for all 60K requests within that same minute.</span></span> <span data-ttu-id="7984a-399">Sollte ein Herausgeber ein Benchmarking für eine Clientanwendung erstellen wollen, sollte er dies sogar in den jeweiligen Umgebungen einzeln vornehmen, in denen er die Clientanwendung ausführen möchte, da sich die Ergebnisse je nach Umgebung unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="7984a-399">If anything, should a publisher want to benchmark a client application, they should do so in each different environment that they are planning on running the client application in because results will vary from environment to environment.</span></span>

## <a name="errors"></a><span data-ttu-id="7984a-400">Fehler</span><span class="sxs-lookup"><span data-stu-id="7984a-400">Errors</span></span>

<span data-ttu-id="7984a-401">Wenn der Dienst einen Fehler feststellt, meldet er den Fehlerantwortcode an den Aufrufer, und zwar mithilfe der standardmäßigen HTTP-Fehlercodesyntax.</span><span class="sxs-lookup"><span data-stu-id="7984a-401">When the service encounters an error, it will report the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="7984a-402">.</span><span class="sxs-lookup"><span data-stu-id="7984a-402"></span></span> <span data-ttu-id="7984a-403">Zusätzliche Informationen sind im Text des fehlgeschlagenen Aufrufs als einzelnes JSON-Objekt enthalten.</span><span class="sxs-lookup"><span data-stu-id="7984a-403">Additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="7984a-404">Nachfolgend finden Sie ein Beispiel für einen vollständige JSON-Fehlertext:</span><span class="sxs-lookup"><span data-stu-id="7984a-404">An example of a full JSON error body is shown below:</span></span> 

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
|<span data-ttu-id="7984a-405">Code</span><span class="sxs-lookup"><span data-stu-id="7984a-405">Code</span></span>|<span data-ttu-id="7984a-406">Nachricht</span><span class="sxs-lookup"><span data-stu-id="7984a-406">Message</span></span>|
|<span data-ttu-id="7984a-407">AF10001</span><span class="sxs-lookup"><span data-stu-id="7984a-407">AF10001</span></span>|<span data-ttu-id="7984a-408">Der Berechtigungssatz ({0}), der in der Anforderung gesendet wurde, enthielt nicht die erwartete Berechtigung **ActivityFeed.Read**.</span><span class="sxs-lookup"><span data-stu-id="7984a-408">The permission set ({0}) sent in the request did not include the expected permission **ActivityFeed.Read**.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-409">{0} = die im Zugriffstoken festgelegte Berechtigung.</span><span class="sxs-lookup"><span data-stu-id="7984a-409">{0} = the permission set in the access token.</span></span></p></li></ul>|
|<span data-ttu-id="7984a-410">AF20001</span><span class="sxs-lookup"><span data-stu-id="7984a-410">AF20001</span></span>|<span data-ttu-id="7984a-411">Fehlender Parameter: {0}</span><span class="sxs-lookup"><span data-stu-id="7984a-411">Missing parameter: {0}.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-412">{0} = der Name des fehlenden Parameters.</span><span class="sxs-lookup"><span data-stu-id="7984a-412">{0} = the name of the missing parameter.</span></span></p></li></ul>|
|<span data-ttu-id="7984a-413">AF20002</span><span class="sxs-lookup"><span data-stu-id="7984a-413">AF20002</span></span>|<span data-ttu-id="7984a-414">Ungültiger Parametertyp: {0}</span><span class="sxs-lookup"><span data-stu-id="7984a-414">Invalid parameter type: {0}.</span></span> <span data-ttu-id="7984a-415">Erwarteter Typ: {1}</span><span class="sxs-lookup"><span data-stu-id="7984a-415">Expected type: {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-416">{0} = der Name des ungültigen Parameters.</span><span class="sxs-lookup"><span data-stu-id="7984a-416">{0} = the name of the invalid parameter.</span></span></p></li><li><p><span data-ttu-id="7984a-417">{1} = der erwartete Typ (int, datetime, guid).</span><span class="sxs-lookup"><span data-stu-id="7984a-417">{1} = the expected type (int, datetime, guid).</span></span></p></li></ul>|
|<span data-ttu-id="7984a-418">AF20003</span><span class="sxs-lookup"><span data-stu-id="7984a-418">AF20003</span></span>|<span data-ttu-id="7984a-419">Angegebener Ablauf {0} ist auf ein Datum und eine Uhrzeit in der Vergangenheit festgelegt.</span><span class="sxs-lookup"><span data-stu-id="7984a-419">Expiration {0} provided is set to past date and time.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-420">{0} = der im API-Aufruf übergebene Ablauf.</span><span class="sxs-lookup"><span data-stu-id="7984a-420">{0} = the expiration passed in the API call.</span></span></p></li></ul>|
|<span data-ttu-id="7984a-421">AF20010</span><span class="sxs-lookup"><span data-stu-id="7984a-421">AF20010</span></span>|<span data-ttu-id="7984a-422">Die in der URL ({0}) übergebene Mandanten-ID stimmt nicht mit der im Zugriffstoken ({1}) übergebenen Mandanten-ID überein.</span><span class="sxs-lookup"><span data-stu-id="7984a-422">The tenant ID passed in the URL ({0}) does not match the tenant ID passed in the access token ({1}).</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-423">{0} = in der URL übergebene Mandanten-ID.</span><span class="sxs-lookup"><span data-stu-id="7984a-423">{0} = tenant ID passed in the URL</span></span></p></li><li><p><span data-ttu-id="7984a-424">{1} = im Zugriffstoken übergebene Mandanten-ID.</span><span class="sxs-lookup"><span data-stu-id="7984a-424">{1} = tenant ID passed in the access token</span></span></p></li></ul>|
|<span data-ttu-id="7984a-425">AF20011</span><span class="sxs-lookup"><span data-stu-id="7984a-425">AF20011</span></span>|<span data-ttu-id="7984a-426">Angegebene Mandanten-ID ({0}) ist im System nicht vorhanden oder wurde gelöscht.</span><span class="sxs-lookup"><span data-stu-id="7984a-426">Specified tenant ID ({0}) does not exist in the system or has been deleted.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   <span data-ttu-id="7984a-427">{0} = in der URL übergebene Mandanten-ID.</span><span class="sxs-lookup"><span data-stu-id="7984a-427">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="7984a-428">AF20012</span><span class="sxs-lookup"><span data-stu-id="7984a-428">AF20012</span></span>|<span data-ttu-id="7984a-429">Angegebene Mandanten-ID ({0}) ist im System falsch konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="7984a-429">Specified tenant ID ({0}) is incorrectly configured in the system.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    <span data-ttu-id="7984a-430">{0} = in der URL übergebene Mandanten-ID.</span><span class="sxs-lookup"><span data-stu-id="7984a-430">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="7984a-431">AF20013</span><span class="sxs-lookup"><span data-stu-id="7984a-431">AF20013</span></span>|<span data-ttu-id="7984a-432">Die in der URL ({0}) übergebene Mandanten-ID ist keine gültige GUID.</span><span class="sxs-lookup"><span data-stu-id="7984a-432">The tenant ID passed in the URL ({0}) is not a valid GUID.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> <span data-ttu-id="7984a-433">{0} = in der URL übergebene Mandanten-ID.</span><span class="sxs-lookup"><span data-stu-id="7984a-433">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="7984a-434">AF20020</span><span class="sxs-lookup"><span data-stu-id="7984a-434">AF20020</span></span>|<span data-ttu-id="7984a-435">Der angegebene Inhaltstyp ist ungültig.</span><span class="sxs-lookup"><span data-stu-id="7984a-435">The specified content type is not valid.</span></span>|
|<span data-ttu-id="7984a-436">AF20021</span><span class="sxs-lookup"><span data-stu-id="7984a-436">AF20021</span></span>|<span data-ttu-id="7984a-437">Der Webhook-Endpunkt {{0}) konnte nicht überprüft werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-437">The webhook endpoint {{0}) could not be validated.</span></span> <span data-ttu-id="7984a-438">{1}</span><span class="sxs-lookup"><span data-stu-id="7984a-438"></span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-439">{0} = Webhookadresse.</span><span class="sxs-lookup"><span data-stu-id="7984a-439">{0} = webhook address.</span></span></p></li><li><p><span data-ttu-id="7984a-440">{1} = „Der Endpunkt hat nicht HTTP 200 zurückgegeben.“</span><span class="sxs-lookup"><span data-stu-id="7984a-440">{1} = "The endpoint did not return HTTP 200."</span></span> <span data-ttu-id="7984a-441">oder „Die Adresse muss mit HTTPS beginnen.“</span><span class="sxs-lookup"><span data-stu-id="7984a-441">or "The address must begin with HTTPS."</span></span></p></li></ul>|
|<span data-ttu-id="7984a-442">AF20022</span><span class="sxs-lookup"><span data-stu-id="7984a-442">AF20022</span></span>|<span data-ttu-id="7984a-443">Kein Abonnement für den angegebenen Inhaltstyp gefunden.</span><span class="sxs-lookup"><span data-stu-id="7984a-443">No subscription found for the specified content type.</span></span>|
|<span data-ttu-id="7984a-444">AF20023</span><span class="sxs-lookup"><span data-stu-id="7984a-444">AF20023</span></span>|<span data-ttu-id="7984a-445">Das Abonnement wurde von {0} deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="7984a-445">The subscription was disabled by {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-446">{0} = „ein Mandant“ oder „ein Dienstadministrator“.</span><span class="sxs-lookup"><span data-stu-id="7984a-446">{0} = "a tenant admin" or "a service admin"</span></span></p></li></ul>|
|<span data-ttu-id="7984a-447">AF20030</span><span class="sxs-lookup"><span data-stu-id="7984a-447">AF20030</span></span>|<span data-ttu-id="7984a-448">Es muss sowohl die Startzeit als auch die Endzeit angegeben werden (oder beide nicht angegeben werden), und die Zeitangaben dürfen nicht mehr als 24 Stunden auseinander liegen, wobei die Startzeit nicht mehr als sieben Tagen in der Vergangenheit liegen darf.</span><span class="sxs-lookup"><span data-stu-id="7984a-448">Start time and end time must both be specified (or both omitted) and must be less than or equal to 24 hours apart, with the start time no more than 7 days in the past.</span></span>|
|<span data-ttu-id="7984a-449">AF20031</span><span class="sxs-lookup"><span data-stu-id="7984a-449">AF20031</span></span>|<span data-ttu-id="7984a-450">Ungültige nextPage-Eingabe: {0}.</span><span class="sxs-lookup"><span data-stu-id="7984a-450">Invalid nextPage Input: {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-451">{0} = der in der URL übergebene Indikator für die nächste Seite</span><span class="sxs-lookup"><span data-stu-id="7984a-451">{0} = the next page indicator passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="7984a-452">AF20050</span><span class="sxs-lookup"><span data-stu-id="7984a-452">AF20050</span></span>|<span data-ttu-id="7984a-453">Der angegebene Inhalt ({0}) ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="7984a-453">The specified content ({0}) does not exist.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-454">{0} = Ressourcen-ID oder Ressourcen-URL</span><span class="sxs-lookup"><span data-stu-id="7984a-454">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="7984a-455">AF20051</span><span class="sxs-lookup"><span data-stu-id="7984a-455">AF20051</span></span>|<span data-ttu-id="7984a-456">Mit dem Schlüssel {0} angeforderter Inhalt ist bereits abgelaufen.</span><span class="sxs-lookup"><span data-stu-id="7984a-456">Content requested with the key {0} has already expired.</span></span> <span data-ttu-id="7984a-457">Inhalt, der älter als 7 Tage ist, kann nicht abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="7984a-457">Content older than 7 days cannot be retrieved.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-458">•    {0} = Ressourcen-ID oder Ressourcen-URL</span><span class="sxs-lookup"><span data-stu-id="7984a-458">•    {0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="7984a-459">AF20052</span><span class="sxs-lookup"><span data-stu-id="7984a-459">AF20052</span></span>|<span data-ttu-id="7984a-460">Inhalts-ID {0} in der URL ist ungültig.</span><span class="sxs-lookup"><span data-stu-id="7984a-460">Content ID {0} in the URL is invalid.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-461">{0} = Ressourcen-ID oder Ressourcen-URL</span><span class="sxs-lookup"><span data-stu-id="7984a-461">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="7984a-462">AF20053</span><span class="sxs-lookup"><span data-stu-id="7984a-462">AF20053</span></span>|<span data-ttu-id="7984a-463">Im Header „Accept-Language“ darf nur eine Sprache vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="7984a-463">Only one language may be present in the Accept-Language header.</span></span>|
|<span data-ttu-id="7984a-464">AF20054</span><span class="sxs-lookup"><span data-stu-id="7984a-464">AF20054</span></span>|<span data-ttu-id="7984a-465">Ungültige Syntax im Accept-Language-Header.</span><span class="sxs-lookup"><span data-stu-id="7984a-465">Invalid syntax in Accept-Language header.</span></span>|
|<span data-ttu-id="7984a-466">AF429</span><span class="sxs-lookup"><span data-stu-id="7984a-466">AF429</span></span>|<span data-ttu-id="7984a-467">Zu viele Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="7984a-467">Too many requests.</span></span> <span data-ttu-id="7984a-468">Method={0}, PublisherId={1}</span><span class="sxs-lookup"><span data-stu-id="7984a-468">Method={0}, PublisherId={1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="7984a-469">{0} = HTTP-Methode</span><span class="sxs-lookup"><span data-stu-id="7984a-469">{0} = HTTP Method</span></span></p></li><li><p><span data-ttu-id="7984a-470">{1} = Mandanten-GUID, die als PublisherIdentifier verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7984a-470">{1} = Tenant GUID used as PublisherIdentifier</span></span></p></li></ul>|
|<span data-ttu-id="7984a-471">AF50000</span><span class="sxs-lookup"><span data-stu-id="7984a-471">AF50000</span></span>|<span data-ttu-id="7984a-472">Ein interner Fehler ist aufgetreten.</span><span class="sxs-lookup"><span data-stu-id="7984a-472">An internal error occurred.</span></span> <span data-ttu-id="7984a-473">Wiederholen Sie die Anforderung.</span><span class="sxs-lookup"><span data-stu-id="7984a-473">Retry the request.</span></span>|
