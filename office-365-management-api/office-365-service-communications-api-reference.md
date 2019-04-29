---
ms.TocTitle: Office 365 Service Communications API reference (preview)
title: Office 365-Dienstkommunikations-API – Referenz (Vorschau)
description: Verwenden Sie diese API, um Zugriff auf die folgenden Daten zu erhalten – Get Services, Get Current Status, Get Historical Status und Get Messages.
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 9b38c4ee73f18bf10c7fa7cbb5b323740dfb5a7e
ms.sourcegitcommit: 336f901a6ed8eb75d99baa4af37d838aeec905c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2019
ms.locfileid: "33440052"
---
# <a name="office-365-service-communications-api-reference-preview"></a><span data-ttu-id="bd4cc-103">Office 365-Dienstkommunikations-API – Referenz (Vorschau)</span><span class="sxs-lookup"><span data-stu-id="bd4cc-103">Office 365 Service Communications API reference (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="bd4cc-104">Diese Dokumentation umfasst Features, die sich aktuell in der Vorschau befinden.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-104">This documentation covers features that are currently in preview.</span></span>

<span data-ttu-id="bd4cc-105">Sie können die Office 365-Dienstkommunikations-API V2 verwenden, um Zugriff auf die folgenden Daten zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="bd4cc-105">You can use the Office 365 Service Communications API V2 to access the following data:</span></span>

- <span data-ttu-id="bd4cc-106">**Get Services**: Erhalt der Liste der abonnierten Dienste.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-106">**Get Services**: Get the list of subscribed services.</span></span>
    
- <span data-ttu-id="bd4cc-107">**Get Current Status**: Erhalt einer Echtzeitansicht der aktuellen und laufenden Dienstincidents und Wartungsereignisse</span><span class="sxs-lookup"><span data-stu-id="bd4cc-107">**Get Current Status**: Get a real-time view of current and ongoing service incidents and maintenance events</span></span>
    
- <span data-ttu-id="bd4cc-108">**Get Historical Status**: Erhalt einer historischen Ansicht der Dienstintegrität, einschließlich Dienstincidents und Wartungsereignisse.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-108">**Get Historical Status**: Get a historical view of service health, including service incidents and maintenance events.</span></span>
    
- <span data-ttu-id="bd4cc-109">**Get Messages**: Suche nach Kommunikation zu Incidents, geplanter Wartung und Nachrichtencenter.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-109">**Get Messages**: Find Incident, Planned Maintenance, and Message Center communications.</span></span>
    
<span data-ttu-id="bd4cc-110">Aktuell umfasst die Office 365-Dienstkommunikations-API Daten für die folgenden Dienste: Dynamics CRM, Dynamics Marketing, Exchange Online, Exchange Online Protection, Identity Service, Mobile Device Management, Office 365 Partner Admin Center, OneDrive for Business, Parature, OneDrive for Business, Power BI for Office 365, Rights Management Service, SharePoint Online, SHD Admin, Skype for Business, Social Engagement und Yammer Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-110">Currently, the Office 365 Service Communications API contains data for the following services: Dynamics CRM, Dynamics Marketing, Exchange Online, Exchange Online Protection, Identity Service, Mobile Device Management, Office 365 Partner Admin Center, OneDrive for Business, Parature, OneDrive for Business, Power BI for Office 365, Rights Management Service, SharePoint Online, SHD Admin, Skype for Business, Social Engagement, and Yammer Enterprise.</span></span>

## <a name="the-fundamentals"></a><span data-ttu-id="bd4cc-111">Die Grundlagen</span><span class="sxs-lookup"><span data-stu-id="bd4cc-111">The fundamentals</span></span>

<span data-ttu-id="bd4cc-112">Die Stamm-URL der API enthält einen Mandantenbezeichner, der die Operationen einem einzigen Mandanten zuordnet:</span><span class="sxs-lookup"><span data-stu-id="bd4cc-112">The root URL of the API includes a tenant identifier that scopes the operations to a single tenant:</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

<span data-ttu-id="bd4cc-113">Die **Office 365 Dienstkommunikations-API** ist ein REST-Dienst, mit dem Sie Lösungen mit einer beliebigen Websprache und Hosting-Umgebung entwickeln können, die HTTPS- und X.509-Zertifikate unterstützt.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-113">The **Office 365 Service Communications API** is a REST service that allows you to develop solutions using any web language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="bd4cc-114">Die API basiert auf **Microsoft Azure Active Directory** und dem **OAuth2**-Protokoll für Authentifizierung und Autorisierung.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-114">The API relies on **Microsoft Azure Active Directory** and the **OAuth2** protocol for authentication and authorization.</span></span> <span data-ttu-id="bd4cc-115">Um von Ihrer Anwendung aus auf die API zugreifen zu können, müssen Sie diese zuerst in Azure AD registrieren und dann mit Berechtigungen im entsprechenden Bereich konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-115">To access the API from your application, you'll need to first register it in Azure AD and configure it with permissions at the appropriate scope.</span></span> <span data-ttu-id="bd4cc-116">Dadurch kann die Anwendung OAuth2-Zugriffstoken anfordern, die für das Aufrufen der API erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-116">This will enable your application to request OAuth2 access tokens necessary for calling the API.</span></span> <span data-ttu-id="bd4cc-117">Weitere Informationen über das Registrieren und Konfigurieren einer Anwendung in Azure AD finden Sie unter [Office 365-Verwaltungs-APIs – erste Schritte](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-117">You can find more information about registering and configuring an application in Azure AD at [Office 365 Management APIs getting started](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="bd4cc-118">Alle API-Anforderungen erfordern einen HTTP-Header für die Autorisierung mit einem gültigen OAuth2-JWT-Zugriffstoken von Azure AD, das den **ServiceHealth.Read**-Anspruchenthält; der Mandantenbezeichner muss dem Mandantenbezeichner in der Stamm-URL entsprechen.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-118">All API requests require an Authorization HTTP header that has a valid OAuth2 JWT access token obtained from Azure AD that contains the **ServiceHealth.Read** claim; and the tenant identifier must match the tenant identifier in the root URL.</span></span>

```json
Authorization: Bearer {OAuth2 token}
```

<span data-ttu-id="bd4cc-119">**Anforderungsheader**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-119">**Request headers**</span></span>

<span data-ttu-id="bd4cc-120">Dies sind die unterstützten Anforderungsheader für alle Office 365-Dienstkommunikations-API-Operationen.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-120">These are the supported request headers for all Office 365 Service Communications API operations.</span></span>

|<span data-ttu-id="bd4cc-121">Header</span><span class="sxs-lookup"><span data-stu-id="bd4cc-121">Header</span></span>|<span data-ttu-id="bd4cc-122">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="bd4cc-122">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="bd4cc-123">**Annehmen (Optional)**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-123">**Accept (Optional)**</span></span>|<span data-ttu-id="bd4cc-124">Im Folgenden finden Sie die zulässigen Darstellungen für die Antwort:</span><span class="sxs-lookup"><span data-stu-id="bd4cc-124">The following are acceptable representations for the response:</span></span><br/><span data-ttu-id="bd4cc-125">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-125">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="bd4cc-126">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-126">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="bd4cc-127">[Standard, wenn kein Header angegeben] **application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-127">[The default if header not specified] **application/json;odata.metadata=none**</span></span>|
|<span data-ttu-id="bd4cc-128">**Autorisierung (erforderlich)**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-128">**Authorization (Required)**</span></span>|<span data-ttu-id="bd4cc-129">Autorisierungstoken (Bearer JWT Azure AD Token) für die Anforderung.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-129">Authorization token (Bearer JWT Azure AD Token) for the request.</span></span>|


<br/>

<span data-ttu-id="bd4cc-130">**Antwortheader**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-130">**Response headers**</span></span>

<span data-ttu-id="bd4cc-131">Dies sind die Antwortheader für alle Office 365-Dienstkommunikations-API-Operationen:</span><span class="sxs-lookup"><span data-stu-id="bd4cc-131">These are the response headers returned for all Office 365 Service Communications API operations:</span></span>

|<span data-ttu-id="bd4cc-132">Header</span><span class="sxs-lookup"><span data-stu-id="bd4cc-132">Header</span></span>|<span data-ttu-id="bd4cc-133">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="bd4cc-133">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="bd4cc-134">**Content-Length**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-134">**Content-Length**</span></span>|<span data-ttu-id="bd4cc-135">Die Länge des Antworttextes.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-135">The length of the response body.</span></span>|
|<span data-ttu-id="bd4cc-136">**Content-Type**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-136">**Content-Type**</span></span>|<span data-ttu-id="bd4cc-137">Darstellung der Antwort:</span><span class="sxs-lookup"><span data-stu-id="bd4cc-137">Representation of the response:</span></span><br/><span data-ttu-id="bd4cc-138">**application/json**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-138">**application/json**</span></span><br/><span data-ttu-id="bd4cc-139">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-139">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="bd4cc-140">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-140">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="bd4cc-141">**application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-141">**application/json;odata.metadata=none**</span></span><br/><span data-ttu-id="bd4cc-142">**odata.streaming=true**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-142">**odata.streaming=true**</span></span>|
|<span data-ttu-id="bd4cc-143">**Cache-Control**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-143">**Cache-Control**</span></span>|<span data-ttu-id="bd4cc-144">Wird verwendet, um Direktiven anzugeben, die alle Caching-Mechanismen in der Anforderungs-/Antwortkette einhalten müssen.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-144">Used to specify directives that all caching mechanisms along the request/response chain must obey.</span></span>|
|<span data-ttu-id="bd4cc-145">**Pragma**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-145">**Pragma**</span></span>|<span data-ttu-id="bd4cc-146">Implementierungsspezifische Verhaltensweisen.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-146">Implementation-specific behaviors.</span></span>|
|<span data-ttu-id="bd4cc-147">**Expires**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-147">**Expires**</span></span>|<span data-ttu-id="bd4cc-148">Wenn der Client dafür sorgen soll, dass die Ressource abläuft.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-148">When the client should make the resource expire.</span></span>|
|<span data-ttu-id="bd4cc-149">**X-Activity-Id**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-149">**X-Activity-Id**</span></span>|<span data-ttu-id="bd4cc-150">Die vom Server generierte Aktivitäts-ID.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-150">The server-generated activity Id.</span></span>|
|<span data-ttu-id="bd4cc-151">**OData-Version**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-151">**OData-Version**</span></span>|<span data-ttu-id="bd4cc-152">Die unterstützte OData-Version (4.0).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-152">The supported OData Version (4.0).</span></span>|
|<span data-ttu-id="bd4cc-153">**Date**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-153">**Date**</span></span>|<span data-ttu-id="bd4cc-154">Das Datum in UTC, als die Antwort vom Server gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-154">The date in UTC when the response was sent from the server.</span></span>|
|<span data-ttu-id="bd4cc-155">**X-Time-Taken**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-155">**X-Time-Taken**</span></span>|<span data-ttu-id="bd4cc-156">Die Zeit zum Generieren der Antwort (ms).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-156">The time it took to generate the response (ms).</span></span>|
|<span data-ttu-id="bd4cc-157">**X-Instance-Name**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-157">**X-Instance-Name**</span></span>|<span data-ttu-id="bd4cc-158">Der Bezeichner für die Azure-Instanz, um die Antwort zu generieren (für Debugging-Zwecke).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-158">The identifier of the Azure instance used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="bd4cc-159">**Server**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-159">**Server**</span></span>|<span data-ttu-id="bd4cc-160">Der Server, um die Antwort zu generieren (für Debugging-Zwecke).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-160">The server used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="bd4cc-161">**X-ASPNET-Version**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-161">**X-ASPNET-Version**</span></span>|<span data-ttu-id="bd4cc-162">Die Version von ASP.Net, die vom Server verwendet wird, der die Antwort generiert hat (für Debugging-Zwecke).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-162">The version of ASP.Net used by the server that generated the response (for debugging purposes).</span></span>|
|<span data-ttu-id="bd4cc-163">**X-Powered-By**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-163">**X-Powered-By**</span></span>|<span data-ttu-id="bd4cc-164">Die Technologien, die vom Server verwendet werden, der die Antwort generiert hat (für Debugging-Zwecke).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-164">The technologies used in the server that generated the response (for debugging purposes).</span></span>|

<br/>

<span data-ttu-id="bd4cc-165">Im Folgenden sind die Operationen der Office 365-Dienstkommunikations-API aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-165">Following are the Office 365 Service Communications API operations.</span></span>


## <a name="get-services"></a><span data-ttu-id="bd4cc-166">Get Services</span><span class="sxs-lookup"><span data-stu-id="bd4cc-166">Get Services</span></span>

<span data-ttu-id="bd4cc-167">Gibt die Liste der abonnierten Dienste zurück.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-167">Returns the list of subscribed services.</span></span>

||<span data-ttu-id="bd4cc-168">Dienst</span><span class="sxs-lookup"><span data-stu-id="bd4cc-168">Service</span></span>|<span data-ttu-id="bd4cc-169">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="bd4cc-169">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="bd4cc-170">**Path**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-170">**Path**</span></span>| `/Services`||
|<span data-ttu-id="bd4cc-171">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-171">**Query-option**</span></span>|<span data-ttu-id="bd4cc-172">$select</span><span class="sxs-lookup"><span data-stu-id="bd4cc-172">$select</span></span>|<span data-ttu-id="bd4cc-173">Wählen Sie eine Teilmenge der Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-173">Pick a subset of properties.</span></span>|
|<span data-ttu-id="bd4cc-174">**Response**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-174">**Response**</span></span>|<span data-ttu-id="bd4cc-175">Liste der „Service“-Entitäten</span><span class="sxs-lookup"><span data-stu-id="bd4cc-175">List of "Service" entities</span></span>|<span data-ttu-id="bd4cc-176">„Service"-Entität enthält „Id“ (Zeichenfolge), „DisplayName“ (Zeichenfolge) und „FeatureNames“ (Liste mit Zeichenfolgen).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-176">"Service" entity contains "Id" (String), "DisplayName" (String), and "FeatureNames" (list of Strings).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="bd4cc-177">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="bd4cc-177">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

#### <a name="sample-response"></a><span data-ttu-id="bd4cc-178">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="bd4cc-178">Sample response</span></span>

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


## <a name="get-current-status"></a><span data-ttu-id="bd4cc-179">Get Current Status</span><span class="sxs-lookup"><span data-stu-id="bd4cc-179">Get Current Status</span></span>

<span data-ttu-id="bd4cc-180">Gibt den Status des Diensts in den vorherigen 24 Stunden zurück.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-180">Returns the status of the service over the previous 24 hours.</span></span>

||<span data-ttu-id="bd4cc-181">Dienst</span><span class="sxs-lookup"><span data-stu-id="bd4cc-181">Service</span></span>|<span data-ttu-id="bd4cc-182">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="bd4cc-182">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="bd4cc-183">**Path**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-183">**Path**</span></span>| `/CurrentStatus`||
|<span data-ttu-id="bd4cc-184">**Filter**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-184">**Filter**</span></span>|<span data-ttu-id="bd4cc-185">Arbeitslast</span><span class="sxs-lookup"><span data-stu-id="bd4cc-185">Workload</span></span>|<span data-ttu-id="bd4cc-186">Filtern nach Arbeitslast (Zeichenfolge, Standard: alle).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-186">Filter by workload (String, default: all).</span></span>|
|<span data-ttu-id="bd4cc-187">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-187">**Query-option**</span></span>|<span data-ttu-id="bd4cc-188">$select</span><span class="sxs-lookup"><span data-stu-id="bd4cc-188">$select</span></span>|<span data-ttu-id="bd4cc-189">Wählen Sie eine Teilmenge der Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-189">Pick a subset of properties.</span></span>|
|<span data-ttu-id="bd4cc-190">**Response**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-190">**Response**</span></span>|<span data-ttu-id="bd4cc-191">Liste der „WorkloadStatus“-Entitäten.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-191">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="bd4cc-192">„WorkloadStatus“-Entität enthält „Id“ (Zeichenfolge), „Workload“ (Zeichenfolge), „StatusTime“ (DateTimeOffset), „WorkloadDisplayName“ (Zeichenfolge), „Status“ (Zeichenfolge), „IncidentIds“ (Liste mit Zeichenfolgen) und „FeatureGroupStatusCollection“ (Liste mit „FeatureStatus“).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-192">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="bd4cc-193">„FeatureStatus“-Entität enthält „Feature“ (Zeichenfolge), „FeatureGroupDisplayName“ (Zeichenfolge) und „FeatureStatus“ (Zeichenfolge).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-193">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="bd4cc-194">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="bd4cc-194">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="bd4cc-195">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="bd4cc-195">Sample response</span></span>

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


## <a name="get-historical-status"></a><span data-ttu-id="bd4cc-196">Get Historical Status</span><span class="sxs-lookup"><span data-stu-id="bd4cc-196">Get Historical Status</span></span>

<span data-ttu-id="bd4cc-197">Gibt den Verlaufsstatus des Dienstes nach Tag über einen bestimmten Zeitraum zurück.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-197">Returns the historical status of the service, by day, over a certain time range.</span></span>

||<span data-ttu-id="bd4cc-198">Dienst</span><span class="sxs-lookup"><span data-stu-id="bd4cc-198">Service</span></span>|<span data-ttu-id="bd4cc-199">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="bd4cc-199">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="bd4cc-200">**Path**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-200">**Path**</span></span>| `/HistoricalStatus`||
|<span data-ttu-id="bd4cc-201">**Filters**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-201">**Filters**</span></span>|<span data-ttu-id="bd4cc-202">Arbeitslast</span><span class="sxs-lookup"><span data-stu-id="bd4cc-202">Workload</span></span>|<span data-ttu-id="bd4cc-203">Filtern nach Arbeitslast (Zeichenfolge, Standard: alle).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-203">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="bd4cc-204">StatusTime</span><span class="sxs-lookup"><span data-stu-id="bd4cc-204">StatusTime</span></span>|<span data-ttu-id="bd4cc-205">Filtern Sie nach Tagen größer als StatusTime (DateTimeOffset, Standard: ge CurrentTime - 7 Tage).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-205">Filter by days greater than StatusTime (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
|<span data-ttu-id="bd4cc-206">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-206">**Query-option**</span></span>|<span data-ttu-id="bd4cc-207">$select</span><span class="sxs-lookup"><span data-stu-id="bd4cc-207">$select</span></span>|<span data-ttu-id="bd4cc-208">Wählen Sie eine Teilmenge der Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-208">Pick a subset of properties.</span></span>|
|<span data-ttu-id="bd4cc-209">**Response**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-209">**Response**</span></span>|<span data-ttu-id="bd4cc-210">Liste der „WorkloadStatus“-Entitäten.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-210">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="bd4cc-211">„WorkloadStatus“-Entität enthält „Id“ (Zeichenfolge), „Workload“ (Zeichenfolge), „StatusTime“ (DateTimeOffset), „WorkloadDisplayName“ (Zeichenfolge), „Status“ (Zeichenfolge), „IncidentIds“ (Liste mit Zeichenfolgen) und „FeatureGroupStatusCollection“ (Liste mit „FeatureStatus“).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-211">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="bd4cc-212">„FeatureStatus“-Entität enthält „Feature“ (Zeichenfolge), „FeatureGroupDisplayName“ (Zeichenfolge) und „FeatureStatus“ (Zeichenfolge).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-212">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="bd4cc-213">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="bd4cc-213">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="bd4cc-214">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="bd4cc-214">Sample response</span></span>

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


## <a name="get-messages"></a><span data-ttu-id="bd4cc-215">Get Messages</span><span class="sxs-lookup"><span data-stu-id="bd4cc-215">Get Messages</span></span>

<span data-ttu-id="bd4cc-216">Gibt Nachrichten über den Dienst über einen bestimmten Zeitraum zurück.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-216">Returns the messages about the service over a certain time range.</span></span> <span data-ttu-id="bd4cc-217">Verwenden Sie den Typfilter zum Filtern nach Nachrichten des Typs „Dienstincident“, „Geplante Wartung“ oder „Nachrichtencenter“.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-217">Use the type filter to filter for "Service Incident", "Planned Maintenance", or "Message Center" messages.</span></span>

||<span data-ttu-id="bd4cc-218">Dienst</span><span class="sxs-lookup"><span data-stu-id="bd4cc-218">Service</span></span>|<span data-ttu-id="bd4cc-219">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="bd4cc-219">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="bd4cc-220">**Path**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-220">**Path**</span></span>| `/Messages`||
|<span data-ttu-id="bd4cc-221">**Filters**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-221">**Filters**</span></span>|<span data-ttu-id="bd4cc-222">Arbeitslast</span><span class="sxs-lookup"><span data-stu-id="bd4cc-222">Workload</span></span>|<span data-ttu-id="bd4cc-223">Filtern nach Arbeitslast (Zeichenfolge, Standard: alle).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-223">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="bd4cc-224">StartTime</span><span class="sxs-lookup"><span data-stu-id="bd4cc-224">StartTime</span></span>|<span data-ttu-id="bd4cc-225">Filter Sie nach Startzeit (DateTimeOffset, Standard: ge CurrentTime - 7 Tage).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-225">Filter by Start Time (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
||<span data-ttu-id="bd4cc-226">EndTime</span><span class="sxs-lookup"><span data-stu-id="bd4cc-226">EndTime</span></span>|<span data-ttu-id="bd4cc-227">Filter Sie nach Endzeit (DateTimeOffset, Standard: le CurrentTime).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-227">Filter by End Time (DateTimeOffset, default: le CurrentTime).</span></span>|
||<span data-ttu-id="bd4cc-228">MessageType</span><span class="sxs-lookup"><span data-stu-id="bd4cc-228">MessageType</span></span>|<span data-ttu-id="bd4cc-229">Filtern Sie nach MessageType (Zeichenfolge, Standard: alle).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-229">Filter by MessageType (String, default: all).</span></span>|
||<span data-ttu-id="bd4cc-230">ID</span><span class="sxs-lookup"><span data-stu-id="bd4cc-230">ID</span></span>|<span data-ttu-id="bd4cc-231">Filtern Sie nach ID (Zeichenfolge, Standard: alle).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-231">Filter by ID (String, default: all).</span></span>|
|<span data-ttu-id="bd4cc-232">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-232">**Query-option**</span></span>|<span data-ttu-id="bd4cc-233">$select</span><span class="sxs-lookup"><span data-stu-id="bd4cc-233">$select</span></span>|<span data-ttu-id="bd4cc-234">Wählen Sie eine Teilmenge der Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-234">Pick a subset of properties.</span></span>|
||<span data-ttu-id="bd4cc-235">$top</span><span class="sxs-lookup"><span data-stu-id="bd4cc-235">$top</span></span>|<span data-ttu-id="bd4cc-236">Wählen Sie die wichtigsten Ergebnisse (default und max $top=100).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-236">Pick the top number of results (default and max $top=100).</span></span>|
||<span data-ttu-id="bd4cc-237">$skip</span><span class="sxs-lookup"><span data-stu-id="bd4cc-237">$skip</span></span>|<span data-ttu-id="bd4cc-238">Überspringen Sie die Anzahl der Ergebnisse (Standard: $skip=0).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-238">Skip number of results (default: $skip=0).</span></span>|
|<span data-ttu-id="bd4cc-239">**Response**</span><span class="sxs-lookup"><span data-stu-id="bd4cc-239">**Response**</span></span>|<span data-ttu-id="bd4cc-240">Liste der „Message“-Entitäten.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-240">List of "Message" entities.</span></span>|<span data-ttu-id="bd4cc-241">Die „Message“-Entität enthält „Id“ (Zeichenfolge), „StartTime“ (DateTimeOffset), „EndTime“ (DateTimeOffset), „Status“ (Zeichenfolge), "Messages" (Liste mit „MessageHistory“-Entität), „LastUpdatedTime“ (DateTimeOffset), „Workload“ (String), „WorkloadDisplayName“ (String), „Feature“ (String), „FeatureDisplayName“ (String), „MessageType“ (Enum, Standard: alle).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-241">"Message" entity contains "Id" (String), "StartTime" (DateTimeOffset), "EndTime" (DateTimeOffset), "Status" (String), "Messages" (list of "MessageHistory" entity), "LastUpdatedTime" (DateTimeOffset), "Workload" (String), "WorkloadDisplayName" (String), "Feature" (String), "FeatureDisplayName" (String), "MessageType" (Enum, default: all).</span></span><br/><br/><span data-ttu-id="bd4cc-242">„MessageHistory“-Entität enthält „PublishedTime“ (DateTimeOffset), „MessageText“ (Zeichenfolge).</span><span class="sxs-lookup"><span data-stu-id="bd4cc-242">"MessageHistory" entity contains "PublishedTime" (DateTimeOffset), "MessageText" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="bd4cc-243">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="bd4cc-243">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="bd4cc-244">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="bd4cc-244">Sample response</span></span>

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


## <a name="errors"></a><span data-ttu-id="bd4cc-245">Fehler</span><span class="sxs-lookup"><span data-stu-id="bd4cc-245">Errors</span></span>

<span data-ttu-id="bd4cc-246">Wenn der Dienst einen Fehler feststellt, meldet er den Fehlerantwortcode an den Aufrufer, mithilfe der standardmäßigen HTTP-Fehlercodesyntax.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-246">When the service encounters an error, it reports the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="bd4cc-247">Gemäß der [OData V4-Spezifikation](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html) sind zusätzliche Informationen im Text des fehlgeschlagenen Aufrufs als einzelnes JSON-Objekt enthalten.</span><span class="sxs-lookup"><span data-stu-id="bd4cc-247">As per [OData V4 specification](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="bd4cc-248">Nachfolgend finden Sie ein Beispiel für einen vollständigen JSON-Fehlertext:</span><span class="sxs-lookup"><span data-stu-id="bd4cc-248">The following is an example of a full JSON error body:</span></span>


```json

{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}

```

