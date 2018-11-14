---
ms.TocTitle: Get started with Office 365 Management APIs
title: Erste Schritte mit den Office 365-Verwaltungs-APIs
description: Die APIs verwenden Azure AD, um Authentifizierungsdienste bereitzustellen, mit denen Sie der Anwendung entsprechende Rechte für den Zugriff auf diese Dienste erteilen können.
ms.ContentId: 74137c9a-29e0-b588-6122-26f4d2c5e3fc
ms.topic: reference (API)
ms.date: 09/05/2018
ms.openlocfilehash: 87abfbe89f60710dc6c9981fa57bde4238790b1f
ms.sourcegitcommit: 525c0d0e78cc44ea8cb6a4bdce1858cb4ef91d57
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/27/2018
ms.locfileid: "25834858"
---
# <a name="get-started-with-office-365-management-apis"></a><span data-ttu-id="f34ed-103">Erste Schritte mit den Office 365-Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="f34ed-103">Get started with Office 365 APIs in apps</span></span>

<span data-ttu-id="f34ed-104">Wenn Sie eine Anwendung erstellen, die Zugriff auf gesicherte Dienste wie die Office 365-Management-APIs benötigt, müssen Sie dem Dienst mitteilen, dass Ihre Anwendung Zugriffsrechte hat.</span><span class="sxs-lookup"><span data-stu-id="f34ed-104">When you create an application that needs access to the Office 365 API services, you need to provide a way to let the service know your application has rights to access it.</span></span> <span data-ttu-id="f34ed-105">Die Office 365-Management-APIs verwenden Azure AD, um Authentifizierungsdienste bereitzustellen, mit denen Sie der Anwendung entsprechende Rechte für den Zugriff auf diese Dienste erteilen können.</span><span class="sxs-lookup"><span data-stu-id="f34ed-105">The Office 365 APIs use Azure AD to provide authentication services that you can use to grant rights for the application to access those services.</span></span> 

<span data-ttu-id="f34ed-106">Es gibt vier zentrale Schritte:</span><span class="sxs-lookup"><span data-stu-id="f34ed-106">There are four key steps:</span></span>

1. <span data-ttu-id="f34ed-107">**Registrieren Sie Ihre Anwendung in Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-107">\*\*\*\* Register your web application with Azure AD</span></span> <span data-ttu-id="f34ed-108">Um Ihrer Anwendung den Zugriff auf die Office 365-Management-APIs zu ermöglichen, müssen Sie Ihre Anwendung bei Azure AD registrieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-108">To allow your application access to the Office 365 APIs, you need to register your application with Azure AD.</span></span> <span data-ttu-id="f34ed-109">Dadurch können Sie eine Identität für Ihre Anwendung einrichten und geben die Berechtigungsstufen angeben, die sie für den Zugriff auf die APIs benötigt.</span><span class="sxs-lookup"><span data-stu-id="f34ed-109">This allows you to establish an identity for your application and specify the permission levels it needs to access the APIs.</span></span>
    
2. <span data-ttu-id="f34ed-110">**Erhalten Sie die Genehmigung durch einen Office 365-Mandanten-Admin**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-110">**Get Office 365 tenant admin consent**.</span></span> <span data-ttu-id="f34ed-111">Ein Office 365-Mandanten-Admin muss eine Genehmigung erteilen, damit Ihre Anwendung auf mittels Office 365-Management-APIs auf Mandantendaten zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="f34ed-111">An Office 365 tenant admin must explicitly grant consent to allow your application to access their tenant data by means of the Office 365 Management APIs.</span></span> <span data-ttu-id="f34ed-112">Der Genehmigungsprozess ist eine browserbasierte Praxis, bei der sich der Mandantenadministrator in der **Azure AD Genehmigung-Benutzeroberfläche** anmelden und die von Ihrer Anwendung angeforderten Berechtigungen überprüfen muss und diese Anfrage gewährt oder verweigert.</span><span class="sxs-lookup"><span data-stu-id="f34ed-112">The consent process is a browser-based experience that requires the tenant admin to sign in to the **Azure AD consent UI** and review the access permissions that your application is requesting, and then either grant or deny the request.</span></span> <span data-ttu-id="f34ed-113">Nachdem die Genehmigung erteilt wurde, leitet die Benutzeroberfläche den Benutzer über einen Authentifizierungscode in der URL zurück zu Ihrer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="f34ed-113">After consent is granted, the UI redirects the user back to your application with an authorization code in the URL.</span></span> <span data-ttu-id="f34ed-114">Ihre Anwendung führt einen Dienst-zu-Dienst-Anruf zu Azure AD durch, um diesen Autorisierungscode in ein Zugriffs-Token umzuwandeln, das Informationen über den Mandantenadministrator und Ihre Anwendung enthält.</span><span class="sxs-lookup"><span data-stu-id="f34ed-114">Your application makes a service-to-service call to Azure AD to exchange this authorization code for an access token, which contains information about both the tenant admin and your application.</span></span> <span data-ttu-id="f34ed-115">Die Mandanten-ID muss aus dem Zugriffstoken entnommen werden und für die zukünftige Nutzung aufbewahrt werden.</span><span class="sxs-lookup"><span data-stu-id="f34ed-115">The tenant ID must be extracted from the access token and stored for future use.</span></span>
    
3. <span data-ttu-id="f34ed-116">**Fordern Sie ein Zugriffstoken von Azure AD an**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-116">\*\*\*\* Request and acquire an access token from Azure AD</span></span> <span data-ttu-id="f34ed-117">Mit den in Azure Active Directory konfigurierten Anmeldeinformationen Ihrer Anwendung fordert Ihre Anwendung fortlaufend zusätzliche Zugriffstoken für einen genehmigten Mandanten an, ohne dass eine weitere Interaktion mit einem Mandantenadministrator benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="f34ed-117">Using your application's credentials as configured in Azure AD, your application requests additional access tokens for a consented tenant on an ongoing basis, without the need for further tenant admin interaction.</span></span> <span data-ttu-id="f34ed-118">Diese Zugriffstoken werden als „nur App“-Token bezeichnet, da sie keine Informationen zum Mandantenadministrator beinhalten.</span><span class="sxs-lookup"><span data-stu-id="f34ed-118">These access tokens are called app-only tokens because they do not include information about the tenant admin.</span></span>
    
4. <span data-ttu-id="f34ed-119">**Rufen Sie die Office 365-Management-APIs auf**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-119">**Call the Office 365 Management APIs**.</span></span> <span data-ttu-id="f34ed-120">Die „nur App“-Zugriffstoken werden an die Office 365-Management-APIs übergeben, um Ihre Anwendung zu authentifizieren und zu autorisieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-120">The app-only access tokens are passed to the Office 365 Management APIs to authenticate and authorize your application.</span></span>
    
<span data-ttu-id="f34ed-121">Das folgende Diagramm zeigt die Abfolge von Genehmigungs- und Zugriffstoken-Anfragen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-121">The following diagram shows the sequence of consent and access token requests.</span></span>


![Initialer Authorisierungsvorgang für Verwaltungs-APIs](images/authorization-flow.png)


## <a name="register-your-application-in-azure-ad"></a><span data-ttu-id="f34ed-123">Registrieren Sie Ihre Anwendung in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f34ed-123">Register your web application with Azure AD</span></span>

<span data-ttu-id="f34ed-124">Die Office 365-Management-APIs verwenden Azure AD zur sicheren Authentifizierung der Office 365-Mandantendaten.</span><span class="sxs-lookup"><span data-stu-id="f34ed-124">The Office 365 API services use Azure AD to provide secure authentication to users' Office 365 data.</span></span> <span data-ttu-id="f34ed-125">Für den Zugriff auf die Office 365-Management-APIs müssen Sie die Anwendung in Azure Active Directory registrieren, und als Teil der Konfiguration die Berechtigungsstufen, die Ihre Anwendung für den Zugriff auf die APIs benötigt, angeben.</span><span class="sxs-lookup"><span data-stu-id="f34ed-125">To access the Office 365 Management APIs, you need to register your app in Azure AD, and as part of the configuration, you will specify the permission levels your app needs to access the APIs.</span></span>


### <a name="prerequisites"></a><span data-ttu-id="f34ed-126">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="f34ed-126">Prerequisites</span></span>

<span data-ttu-id="f34ed-127">Wenn Sie die Anwendung in Azure AD registriert haben, benötigen Sie ein Abonnement für Office 365 und ein Abonnement für Azure, das mit Ihrem Office 365-Abonnement verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="f34ed-127">To register your app in Azure AD, you need a subscription to Office 365 and a subscription to Azure that has been associated with your Office 365 subscription.</span></span> <span data-ttu-id="f34ed-128">Für den Anfang können Sie Testabonnements sowohl für Office 365 als auch für Azure verwenden.</span><span class="sxs-lookup"><span data-stu-id="f34ed-128">You can use trial subscriptions to both Office 365 and Azure to get started.</span></span> <span data-ttu-id="f34ed-129">Weitere Informationen finden Sie unter [Willkommen beim Office 365-Entwicklerprogramm](https://docs.microsoft.com/de-DE/office/developer-program/office-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="f34ed-129">For more information, see [Join the Office 365 Developer Program](https://docs.microsoft.com/de-DE/office/developer-program/office-365-developer-program).</span></span>


### <a name="use-the-azure-management-portal-to-register-your-application-in-azure-ad"></a><span data-ttu-id="f34ed-130">Nutzen Sie das Azure-Verwaltungsportal, um Ihre Anwendung in Azure AD zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-130">Use the Azure Management Portal to register your application in Azure AD</span></span>

<span data-ttu-id="f34ed-131">Nachdem Sie einen Microsoft-Mandanten mit den entsprechenden Abonnements haben, können Sie Ihre Anwendung in Azure AD registrieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-131">After you have a Microsoft tenant with the proper subscriptions, you can register your application in Azure AD.</span></span>

1. <span data-ttu-id="f34ed-132">Melden Sie sich im [Azure-Verwaltungsportal](https://manage.windowsazure.com/) an, und verwenden Sie dabei die Anmeldeinformationen Ihres Microsoft-Mandanten, der über das Office 365-Abonnement verfügt, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="f34ed-132">Sign into the [Azure management portal](https://manage.windowsazure.com/), using the credential of your Microsoft tenant that has the subscription to Office 365 you wish to use.</span></span> <span data-ttu-id="f34ed-133">Sie können auf das Azure-Verwaltungsportal auch über einen Link zugreifen, der im linken Navigationsbereich im [Office Admin-Portal](https://portal.office.com/) erscheint.</span><span class="sxs-lookup"><span data-stu-id="f34ed-133">You can also access the Azure Management Portal via a link that appears in the left navigation pane in the [Office admin portal](https://portal.office.com/).</span></span>
    
2. <span data-ttu-id="f34ed-134">Klicken Sie im linken Navigationsbereich auf Active Directory (1).</span><span class="sxs-lookup"><span data-stu-id="f34ed-134">In the left navigation panel, choose Active Directory (1).</span></span> <span data-ttu-id="f34ed-135">Stellen Sie sicher, dass die Registerkarte Verzeichnis (2) ausgewählt ist, und klicken Sie dann auf den Verzeichnisnamen (3).</span><span class="sxs-lookup"><span data-stu-id="f34ed-135">Make sure the Directory tab is selected, and then click on the directory name.</span></span>
    
   ![Anmeldeseite für Office 365](images/o365-sign-up-page.png)
    
    
3. <span data-ttu-id="f34ed-137">Wählen Sie auf der Verzeichnisseite **Anwendungen**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-137">On the directory page, select Applications.</span></span> <span data-ttu-id="f34ed-138">Azure AD zeigt eine Liste der Anwendungen, die aktuell in Ihrem Mandanten installiert sind.</span><span class="sxs-lookup"><span data-stu-id="f34ed-138">Azure AD displays a list of the applications currently installed in your tenancy.</span></span>
    
4. <span data-ttu-id="f34ed-139">Wählen Sie **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="f34ed-139">Choose **Add**.</span></span>
    
   ![Verwaltungsseite für Office 365](images/o365-admin-page.png)
    
    
5. <span data-ttu-id="f34ed-141">Wählen Sie **Add an application my organization is developing** aus.</span><span class="sxs-lookup"><span data-stu-id="f34ed-141">On the dialog that opens, choose  **Add an application my organization is developing**.</span></span>
    
6. <span data-ttu-id="f34ed-142">Geben Sie den **Namen** Ihrer Anwendung ein, und geben Sie für den **Typ** WEB-ANWENDUNG UND/ODER WEB-API an.</span><span class="sxs-lookup"><span data-stu-id="f34ed-142">Enter the **NAME** of your application and specify the **Type** as WEB APPLICATION AND/OR WEB API.</span></span>
    
7. <span data-ttu-id="f34ed-143">Geben Sie die entsprechenden Eigenschaften der App ein:</span><span class="sxs-lookup"><span data-stu-id="f34ed-143">Enter the appropriate App properties:</span></span>
    
   - <span data-ttu-id="f34ed-144">**Anmelde-URL**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-144">Sign-on URL</span></span> <span data-ttu-id="f34ed-145">Die URL, mit der Benutzer sich anmelden und Ihre Anwendung verwenden können.</span><span class="sxs-lookup"><span data-stu-id="f34ed-145">The Sign-on URL is the address of a web page where users can sign in and use your app.</span></span> <span data-ttu-id="f34ed-146">Sie können dies später bei Bedarf ändern.</span><span class="sxs-lookup"><span data-stu-id="f34ed-146">You can change this later as needed.</span></span>
    
   - <span data-ttu-id="f34ed-147">**App-ID-URI**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-147">App ID URI</span></span> <span data-ttu-id="f34ed-148">Der URI, der als ein eindeutiger logischer Identifikator verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f34ed-148">The URI used as a unique logical identifier for your app.</span></span> <span data-ttu-id="f34ed-149">Der URI muss sich in einer überprüften benutzerdefinierten Domäne für einen externen Benutzer befinden, um Ihrer Anwendung Zugriff auf seine Daten in Windows Azure Active Directory zu gewähren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-149">The URI must be in a verified custom domain for an external user to grant your app access to their data in Windows Azure AD.</span></span> <span data-ttu-id="f34ed-150">Wenn Ihr Microsoft-Mandant z. B. **contoso.onmicrosoft.com** ist, könnte die APP-ID URI **https://app.contoso.onmicrosoft.com** sein.</span><span class="sxs-lookup"><span data-stu-id="f34ed-150">For example, if your Microsoft tenant is **contoso.onmicrosoft.com**, the APP ID URI could be **https://app.contoso.onmicrosoft.com**.</span></span>
    
8. <span data-ttu-id="f34ed-151">Die app ist jetzt mitIhre Anwendung ist jetzt für Azure AD registriert und wurde einer Client-ID zugewieden.</span><span class="sxs-lookup"><span data-stu-id="f34ed-151">Your app is now registered with Azure AD, and has been assigned a client ID.</span></span> <span data-ttu-id="f34ed-152">Es gibt jedoch weitere wichtige Aspekte Ihrer Anwendung, die konfiguriert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-152">However, there are several important aspects of your app left to configure.</span></span>
    

### <a name="configure-your-application-properties-in-azure-ad"></a><span data-ttu-id="f34ed-153">Konfigurieren Sie Ihre Anwendungseigenschaften in Azure AD</span><span class="sxs-lookup"><span data-stu-id="f34ed-153">Configure your application properties in Azure AD</span></span>

<span data-ttu-id="f34ed-154">Nachdem Ihre Anwendung registriert ist, gibt es mehrere wichtige Eigenschaften, die Sie angeben müssen, die bestimmen, wie Ihre Anwendung in Azure AD funktioniert und wie Mandantenadministratoren Ihrer Anwendung die Genehmigung für den Zugriff auf ihre Daten mittels den Office 365-Management-APIs erteilen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-154">Now that your application is registered, there are several important properties you must specify that determine how your application functions within Azure AD and how tenant admins will grant consent to allow your application to access their data by using the Office 365 Management APIs.</span></span>

<span data-ttu-id="f34ed-155">Weitere Informationen zur Anwensungskonfiguration in Azure AD im Allgemeinen finden Sie unter [Anwendungs-Objekteigenschaften](https://docs.microsoft.com/de-DE/azure/active-directory/develop/active-directory-application-objects).</span><span class="sxs-lookup"><span data-stu-id="f34ed-155">For more information about Azure AD application configuration in general, see [Application Object Properties](https://docs.microsoft.com/de-DE/azure/active-directory/develop/active-directory-application-objects).</span></span>


1. <span data-ttu-id="f34ed-156">**CLIENT-ID**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-156">Client ID</span></span> <span data-ttu-id="f34ed-157">Dieser Wert wird von Azure AD automatisch generiert.</span><span class="sxs-lookup"><span data-stu-id="f34ed-157">This value is automatically generated by Azure AD.</span></span> <span data-ttu-id="f34ed-158">Ihre Anwendung wird diesen Wert beim Anfordern von Genehmigungen von Mandantenadministratoren und beim Anfordern von „Nur App“-Token aus Azure AD verwenden.</span><span class="sxs-lookup"><span data-stu-id="f34ed-158">Your application will use this value when requesting consent from tenant admins and when requesting app-only tokens from Azure AD.</span></span>
    
2. <span data-ttu-id="f34ed-159">**ANWENDUNG HAT MEHRERE MANDANTEN**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-159">**APPLICATION IS MULTI-TENANT**.</span></span> <span data-ttu-id="f34ed-160">Für diese Eigenschaft muss **Ja** ausgewählt werden, damit Mandantenadministratoren Ihrer Anwendung die Genehmigung erteilen können, mit den Office 365-Management-APIs auf ihre Daten zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-160">This property must be set to **YES** to allow tenant admins to grant consent to your app to access their data by using the Office 365 Management APIs.</span></span> <span data-ttu-id="f34ed-161">Wenn für diese Eigenschaft **Nein** ausgewählt ist, kann Ihre Anwendung ausschließlich auf Daten Ihres eigenen Mandanten zugreifen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-161">If this property is set to **NO**, your application will only be able to access your own tenant's data.</span></span>
    
3. <span data-ttu-id="f34ed-162">**ANTWORT-URL**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-162">Reply URL</span></span> <span data-ttu-id="f34ed-163">Dies ist die URL, zu der ein Mandantenadministrator weitergeleitet wird, nachdem er Ihrer Anwendung die Genehmigung für den Zugriff auf seine Daten mittels den Office 365 Management-APIs erteilt hat.</span><span class="sxs-lookup"><span data-stu-id="f34ed-163">This is the URL that a tenant admin will be redirected to after granting consent to allow your application to access their data by using the Office 365 Management APIs.</span></span> <span data-ttu-id="f34ed-164">Sie können bei Bedarf mehrere Antwort-URLs konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-164">You can configure multiple reply URLs as needed.</span></span> <span data-ttu-id="f34ed-165">Azure legt automatisch die erste so fest, dass sie mit der Anmelde-URL übereinstimmt, die Sie beim Erstellen der Anwendung angegeben haben, aber Sie können diesen Wert wenn nötig ändern.</span><span class="sxs-lookup"><span data-stu-id="f34ed-165">Azure automatically sets the first one to match the sign-on URL you specified when you created the application, but you can change this value as needed.</span></span>
    
<span data-ttu-id="f34ed-166">Wählen Sie unbedingt **Speichern**, nachdem Sie Änderungen an dieser Eigenschaften vorgenommen haben.</span><span class="sxs-lookup"><span data-stu-id="f34ed-166">Be sure to choose **Save** after making any changes to these properties.</span></span>


### <a name="generate-a-new-key-for-your-application"></a><span data-ttu-id="f34ed-167">Erstellen Sie einen neuen Schlüssel für Ihre Anwendung</span><span class="sxs-lookup"><span data-stu-id="f34ed-167">Generate a new app secret for your web application</span></span>

<span data-ttu-id="f34ed-168">Schlüssel werden auch als geheime Clientschlüssel bezeichnet und werden verwendet, ein Autorisierungscode gegen eine Zugriffstoken ausgetauscht wird.</span><span class="sxs-lookup"><span data-stu-id="f34ed-168">Keys, also known as client secrets, are used when exchanging an authorization code for an access token.</span></span>


1. <span data-ttu-id="f34ed-169">Wählen Sie im Azure Verwaltungsportal Ihre Anwendung und wählen Sie **konfigurieren** im oberen Menü.</span><span class="sxs-lookup"><span data-stu-id="f34ed-169">In the Azure Management Portal, select your application and choose **Configure** in the top menu.</span></span> <span data-ttu-id="f34ed-170">Blättern Sie nach unten zu **Schlüssel**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-170">Scroll down to **keys**.</span></span>
    
2. <span data-ttu-id="f34ed-171">Wählen Sie die Gültigkeitsdauer Ihres Schlüssels, und wählen Sie **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-171">Select the duration for your key, and choose **Save**.</span></span>
    
   ![Azure-Seite "Abonnieren"](images/azure-subscription-page.png)
    
    
3. <span data-ttu-id="f34ed-173">Azure zeigt den App-Schlüssel nur nach dem Speichern an.</span><span class="sxs-lookup"><span data-stu-id="f34ed-173">Azure displays the app secret only after saving it.</span></span> <span data-ttu-id="f34ed-174">Klicken Sie auf das Symbol Zwischenablage, um das Client-Geheimnis in die Zwischenablage zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-174">Click the Clipboard icon to copy the client secret to the Clipboard.</span></span>
    
   ![Azure-Seite "Portal"](images/azure-portal-page.png)

   > [!IMPORTANT] 
   > <span data-ttu-id="f34ed-176">Azure zeigt das Client-Geheimnis nur zum Zeitpunkt der ersten Generierung an.</span><span class="sxs-lookup"><span data-stu-id="f34ed-176">Important Azure only displays the client secret at the time you initially generate it.</span></span> <span data-ttu-id="f34ed-177">Sie können nicht zu dieser Seite zurücknavigieren und den geheimen Clientschlüssel später abrufen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-177">You cannot navigate back to this page and retrieve the client secret later.</span></span>

### <a name="configure-an-x509-certificate-to-enable-service-to-service-calls"></a><span data-ttu-id="f34ed-178">Konfigurieren eines x. 509-Zertifikats, um Dienst-zu-Dienst-Aufrufe zu ermöglichen</span><span class="sxs-lookup"><span data-stu-id="f34ed-178">Configure an X.509 certificate to enable service-to-service calls</span></span>

<span data-ttu-id="f34ed-179">Eine Anwendung, die im Hintergrund ausgeführt wird, wie ein Dämonprozess oder ein Dienst, kann Client-Anmeldeinformationen nutzen, um ein „Nur App“-Zugriffstoken anzufordern, ohne fortlaufend eine Genehmigung vom Mandantenadministrator anzufordern, nachdem eine erste Genehmigung erteilt wurde.</span><span class="sxs-lookup"><span data-stu-id="f34ed-179">An application that is running in the background, such as a daemon or service, can use client credentials to request app-only access tokens without repeatedly requesting consent from the tenant admin after initial consent is granted.</span></span> 

<span data-ttu-id="f34ed-180">Weitere Informationen finden Sie unter [Dienst-zu-Dienst-Anrufe mithilfe von Client-Anmeldeinformationen](https://msdn.microsoft.com/de-DE/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="f34ed-180">For details about the authentication flow, see [Service to Service Calls Using Client Credentials](https://msdn.microsoft.com/de-DE/library/azure/dn645543.aspx).</span></span>

<span data-ttu-id="f34ed-181">Sie müssen ein X.509-Zertifikat für Ihre Anwendung erstellen, das als Client-Anmeldedaten dient, wenn ein „Nur App“-Token von Azure AD angefordert wird.</span><span class="sxs-lookup"><span data-stu-id="f34ed-181">You must configure an X.509 certificate with your application to be used as client credentials when requesting app-only access tokens from Azure AD.</span></span> <span data-ttu-id="f34ed-182">Dieser Prozess besteht aus zwei Schritten:</span><span class="sxs-lookup"><span data-stu-id="f34ed-182">There are two main components to the IRM migration process:</span></span>

- <span data-ttu-id="f34ed-183">Abrufen eines X.509-Zertifikats.</span><span class="sxs-lookup"><span data-stu-id="f34ed-183">Obtain an X.509 certificate.</span></span> <span data-ttu-id="f34ed-184">Sie können ein selbstsigniertes Zertifikat oder ein von einer öffentlichen, vertrauenswürdigen Zertifizierungsstelle ausgestelltes Zertifikat verwenden..</span><span class="sxs-lookup"><span data-stu-id="f34ed-184">You can use a self-signed certificate or a certificate issued by publicly trusted certificate authority.</span></span>
    
- <span data-ttu-id="f34ed-185">Ändern Sie Ihr Anwendungsmanifest, um den Fingerabdruck und den öffentlichen Schlüssel Ihres Zertifikats einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-185">Modify your application manifest to include the thumbprint and public key of your certificate.</span></span>
    
<span data-ttu-id="f34ed-186">Die folgenden Anweisungen zeigen Ihnen, wie Sie das Visual Studio oder das Windows SDK _Makecert_tool verwenden, um ein selbstsigniertes Zertifikat zu erstellen und den öffentlichen Schlüssel in eine base64-codierte Datei zu exportieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-186">The following instructions show you how to use the Visual Studio or Windows SDK _makecert_ tool to generate a self-signed certificate and export the public key to a base64-encoded file.</span></span>


1. <span data-ttu-id="f34ed-187">Führen Sie in der Befehlszeile Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="f34ed-187">On the command line, run the following command:</span></span>
    
   ```
    makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 03/15/2015 -e 03/15/2017 -ss my -len 2048
   ```

   > [!NOTE] 
   > <span data-ttu-id="f34ed-188">Wenn Sie das x. 509-Zertifikat generieren, stellen Sie sicher, dass die Länge des Schlüssels mindestens 2048 beträgt.</span><span class="sxs-lookup"><span data-stu-id="f34ed-188">When you are generating the X.509 certificate, make sure the key length is at least 2048.</span></span> <span data-ttu-id="f34ed-189">Kürzere Schlüssellängen werden nicht als gültige Schlüssel akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="f34ed-189">Shorter key length are not accepted as valid keys.</span></span>

2. <span data-ttu-id="f34ed-190">Öffnen Sie die Snap-In MMC-Zertifikate und verbinden Sie sich mit Ihrem Benutzerkonto.</span><span class="sxs-lookup"><span data-stu-id="f34ed-190">Open the Certificates management console snap-in and connect to your user account.</span></span> 
    
3. <span data-ttu-id="f34ed-191">Suchen Sie das neue Zertifikat im Persönlichen Ordner und exportieren Sie den öffentlichen Schlüssel in eine base64-codierte Datei (z. B. mycompanyname.cer).</span><span class="sxs-lookup"><span data-stu-id="f34ed-191">Find the new certificate in the Personal folder and export the public key to a base64-encoded file (for example, mycompanyname.cer).</span></span> <span data-ttu-id="f34ed-192">Ihre Anwendung verwendet dieses Zertifikat zum Kommunizieren mit Azure AD. Stellen Sie daher sicher, dass Sie auch Zugriff auf den privat Schlüssel erhalten.</span><span class="sxs-lookup"><span data-stu-id="f34ed-192">Your application will use this certificate to communicate with Azure AD, so make sure you retain access to the private key as well.</span></span>
    
   > [!NOTE] 
   > <span data-ttu-id="f34ed-193">Sie können Windows PowerShell verwenden, um den Fingerabdruck und den base64-codierten öffentlichen Schlüssel zu extrahieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-193">You can use Windows PowerShell to extract the thumbprint and base64-encoded public key.</span></span> <span data-ttu-id="f34ed-194">Andere Plattformen bieten ähnliche Tools zum Abrufen der Eigenschaften von Zertifikaten.</span><span class="sxs-lookup"><span data-stu-id="f34ed-194">Other platforms provide similar tools to retrieve properties of certificates.</span></span>

4. <span data-ttu-id="f34ed-195">Geben Sie in der Windows PowerShell-Eingabeaufforderung Folgendes ein und führen Sie es aus:</span><span class="sxs-lookup"><span data-stu-id="f34ed-195">From the Windows PowerShell prompt, type and run the following cmdlets:</span></span>
    
   ```powershell
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $cer.Import("mycer.cer")
    $bin = $cer.GetRawCertData()
    $base64Value = [System.Convert]::ToBase64String($bin)
    $bin = $cer.GetCertHash()
    $base64Thumbprint = [System.Convert]::ToBase64String($bin)
    $keyid = [System.Guid]::NewGuid().ToString()
   ```

5. <span data-ttu-id="f34ed-196">Speichern Sie die Werte für `$base64Thumbprint`, `$base64Value`, und `$keyid`, die verwendet werden, wenn Sie Ihr Anwendungsmanifest in den nächsten Schritten aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-196">Store the values for `$base64Thumbprint`, `$base64Value`, and `$keyid` to be used when you update your application manifest in the next set of steps.</span></span>
    
   <span data-ttu-id="f34ed-197">Mit den aus dem Zertifikat extrahierten Werten und der generierten Schlüssel-ID müssen Sie nun Ihr Anwendungsmanifest in Azure AD aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-197">Using the values extracted from the certificate and the generated key ID, you must now update your application manifest in Azure AD.</span></span>
    
6. <span data-ttu-id="f34ed-198">Wählen Sie im Azure Verwaltungsportal Ihre Anwendung und wählen Sie **konfigurieren** im oberen Menü.</span><span class="sxs-lookup"><span data-stu-id="f34ed-198">In the Azure Management Portal, select your application and choose **Configure** in the top menu.</span></span>
    
7. <span data-ttu-id="f34ed-199">Wählen Sie in der Befehlsleiste \*\*Manifest verwalten \*\*, und wählen Sie dann **Manifest herunterladen**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-199">In the command bar, choose **Manage manifest**, and then choose **Download Manifest**.</span></span>
    
   ![Anzeige des Kommandozeilenzertifikats](images/command-line-certificate-display.png)
    
    
8. <span data-ttu-id="f34ed-201">Öffnen Sie das heruntergeladene Manifest zur Bearbeitung und ersetzen Sie die leere KeyCredentials -Eigenschaft durch die folgende JSON:</span><span class="sxs-lookup"><span data-stu-id="f34ed-201">Open the downloaded file for editing and replace the empty KeyCredentials property with the following JSON:</span></span>
    
   ```json
      "keyCredentials": [
        {
            "customKeyIdentifier" : "$base64Thumbprint_from_above",
            "keyId": "$keyid_from_above",
            "type": "AsymmetricX509Cert",
            "usage": "Verify",
            "value": "$base64Value_from_above"
        }
    ],
   ```


   > [!NOTE] 
   > <span data-ttu-id="f34ed-202">Die [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType)-Eigenschaft ist eine Sammlung, die es ermöglicht, mehrere X.509-Zertifikate für Rollover-Szenarien hochzuladen oder Zertifikate für Kompromiss-Szenarien zu löschen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-202">The [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) property is a collection, making it possible to upload multiple X.509 certificates for rollover scenarios or delete certificates for compromise scenarios.</span></span>

9. <span data-ttu-id="f34ed-203">Speichern Sie Ihre Änderungen und laden Sie die aktualisierte App-Manifestdatei hoch, indem Sie auf **Manifest verwalten** in der Befehlsleiste klicken, **Manifest hochladen**wählen, zu Ihrer aktualisierten Manifestdatei navigieren und diese dann auswählen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-203">Save your changes, and upload the updated app manifest file by clicking **Manage manifest** in the command bar, selecting **Upload manifest**, browsing to your updated manifest file and then selecting it.</span></span>
    

### <a name="specify-the-permissions-your-app-requires-to-access-the-office-365-management-apis"></a><span data-ttu-id="f34ed-204">Geben Sie die Berechtigungen, die Ihre Anwnedung benötigt, um auf die Office 365-Management-APIs zuzugreifen, an.</span><span class="sxs-lookup"><span data-stu-id="f34ed-204">Specify the permissions your app requires to access the Office 365 Management APIs</span></span>

<span data-ttu-id="f34ed-205">Schließlich müssen Sie genau angeben, welche Berechtigungen Ihre Anwendung für die Office 365 Management-APIs benötigt.</span><span class="sxs-lookup"><span data-stu-id="f34ed-205">Finally, you'll need to specify exactly what permissions your app requires of the Office 365 APIs.</span></span> <span data-ttu-id="f34ed-206">Zu diesem Zweck müssen Sie einen Zugriff auf die Office 365-Management-APIs zu Ihrer Anwendung hinzufügen und dann die Berechtigung(en) auswählen, die Sie benötigen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-206">To do so, you add access to the Office 365 service containing the API you require to your app, and then specify the permission(s) you need from the APIs in that service.</span></span>


1. <span data-ttu-id="f34ed-207">Wählen Sie im Azure Verwaltungsportal Ihre Anwendung und wählen Sie **konfigurieren** im oberen Menü.</span><span class="sxs-lookup"><span data-stu-id="f34ed-207">In the Azure Management Portal, select your application and choose **Configure** in the top menu.</span></span> <span data-ttu-id="f34ed-208">Scrollen Sie nach unten zu **Berechtigungen für andere Anwendungen** und wählen Sie **Anwendung hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="f34ed-208">Scroll down to **permissions to other applications**, and choose **Add application**.</span></span>
    
   ![Azure AD-Seite](images/azure-ad-page.png)
    
    
2. <span data-ttu-id="f34ed-210">Wählen Sie die **Office 365-Management-APIs** (1) so, dass sie in der **ausgewählter** Spalte (2) angezeigt werden, und wählen Sie dann das Häkchen unteren rechts (3), um Ihre Auswahl zu speichern und zurück zu Haupt-Konfigurationsseite Ihrer Anwendung zu gelangen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-210">Select the **Office 365 Management APIs** (1) so that it appears in the **Selected** column (2), and then select the check mark in the lower right (3) to save your selection and return to the main configuration page for your application.</span></span>
    
   ![Azure AD-Seite "Apps"](images/azure-ad-apps-page.png)
    
    
3. <span data-ttu-id="f34ed-212">Die Office-Management-APIs werden jetzt in der Liste der Anwendungen angezeigt, für die Ihre Anwendung Berechtigungen benötigt.</span><span class="sxs-lookup"><span data-stu-id="f34ed-212">The Office Management APIs now appear in the list of applications to which your application requires permissions.</span></span> <span data-ttu-id="f34ed-213">Wählen Sie sowohl unter **Anwendungsberechtigungen** als auch unter **delegierte Berechtigungen** die Berechtigungen aus, die Ihre Anwendung benötigt.</span><span class="sxs-lookup"><span data-stu-id="f34ed-213">Under both **Application Permissions** and **Delegated Permissions**, select the permissions your application requires.</span></span> <span data-ttu-id="f34ed-214">Weitere Informationen zu den einzelnen Berechtigungen finden Sie unter den jeweiligen API-Referenzen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-214">Refer to the specific API reference for more details about each permission.</span></span>  

   > [!NOTE] 
   > <span data-ttu-id="f34ed-215">Vier Berechtigungen für Aktivitätsberichte und Informationen zu Bedrohungen werden derzeit nicht verwendet und werden zukünftig entfernt.</span><span class="sxs-lookup"><span data-stu-id="f34ed-215">There are currently four unused permissions related to activity reports and threat intelligence that will be removed in the future.</span></span> <span data-ttu-id="f34ed-216">Aktivieren Sie keine der folgenden Berechtigungen, da sie nicht erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="f34ed-216">Do not select any of these permissions because they are unnecessary.</span></span>
    
   ![Dialogfeld "Eine Anwendung hinzufügen"](images/add-an-application-dialog.png)
    
    
4. <span data-ttu-id="f34ed-218">Klicken Sie auf **Speichern**, um die Konfiguration zu speichern.</span><span class="sxs-lookup"><span data-stu-id="f34ed-218">Choose **Save** to save the rule.</span></span>
    

## <a name="get-office-365-tenant-admin-consent"></a><span data-ttu-id="f34ed-219">Erhalten Sie die Genehmigung durch einen Office 365-Mandantenadmin.</span><span class="sxs-lookup"><span data-stu-id="f34ed-219">Get Office 365 tenant admin consent</span></span>

<span data-ttu-id="f34ed-220">Nun, da Ihre Anwendung mit den Berechtigungen konfiguriert ist, die sie für die Verwendung der Office 365-Management APIs benötigt, muss ein Mandantenadministrator diese Berechtigungen ausdrücklich für Ihre Anwendung gewähren, damit Sie mittels der APIs auf dessen Mandantendaten zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="f34ed-220">Now that your application is configured with the permissions it needs to use the Office 365 Management APIs, a tenant admin must explicitly grant your application these permissions in order to access their tenant's data by using the APIs.</span></span> <span data-ttu-id="f34ed-221">Um eine Genehmigung zu erteilen, muss sich der Mandantenadministrator in Azure AD anmelden. Dafür verwendet er die folgende eigens konstruierte URL, mittels derer er die von Ihrer Anwendung angefragten Berechtigungen einsehen kann.</span><span class="sxs-lookup"><span data-stu-id="f34ed-221">To grant consent, the tenant admin must sign in to Azure AD by using the following specially constructed URL, where they can review your application's requested permissions.</span></span> <span data-ttu-id="f34ed-222">Dieser Schritt ist nicht erforderlich, wenn Sie APIs verwenden, um auf Daten aus Ihrem eigenen Mandanten zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-222">This step is not required when using the APIs to access data from your own tenant.</span></span>


```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id={your_client_id}&redirect_uri={your_redirect_url }
```

<span data-ttu-id="f34ed-223">Die Weiterleitungs-URL muss mit der Antwort-URL übereinstimmen oder ein untergeordneter Pfad einer der Antwort-URLs sein, die für Ihre Anwendung in Azure AD erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="f34ed-223">The redirect URL must match or be a sub-path under one of the Reply URLs configured for your application in Azure AD.</span></span>

<span data-ttu-id="f34ed-224">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f34ed-224">For example:</span></span>

```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e&redirect_uri=http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F
```

<span data-ttu-id="f34ed-225">Sie können die genehmigte URL testen, indem Sie diese in einen Browser kopieren und sich mit den Anmeldedaten eines Office 365-Admin für einen anderen Mandanten, als der, den Sie für die Registrierung der Anwendung verwendet haben, anmelden.</span><span class="sxs-lookup"><span data-stu-id="f34ed-225">You can test the consent URL by pasting it into a browser and signing in using the credentials of an Office 365 admin for a tenant other than the tenant that you used to register the application.</span></span> <span data-ttu-id="f34ed-226">Ihnen wird die Anfrage zur Berechtigungserteilung zur Nutzung der Office-Management-APIs für Ihre Anwendung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f34ed-226">You will see the request to grant your application permission to use the Office Management APIs.</span></span>


![Azure AD-Seite "App hinzugefügt"](images/azure-ad-app-added-page.png)

<span data-ttu-id="f34ed-228">Nachdem Sie **Annehmen** ausgewählt haben, werden Sie zu der angegebenen Seite weitergeleitet und die Abfrage-Zeichenfolge wird einen Code enthalten.</span><span class="sxs-lookup"><span data-stu-id="f34ed-228">After choosing **Accept**, you are redirected to the specified page, and there will be a code in the query string.</span></span> 

<span data-ttu-id="f34ed-229">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f34ed-229">For example:</span></span>

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

<span data-ttu-id="f34ed-230">Ihre Anwendung verwendet diesen Autorisierungscode, um ein Zugriffstoken von Azure AD zu erhalten, aus dem die Mandanten-ID extrahiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="f34ed-230">Your application uses this authorization code to obtain an access token from Azure AD, from which the tenant ID can be extracted.</span></span> <span data-ttu-id="f34ed-231">Nachdem Sie die Mandanten-ID extrahiert und gespeichert haben, können Sie nachfolgende Zugriffstoken beziehen, ohne dass eine Anmeldung als Mandantenadministrator notwendig ist.</span><span class="sxs-lookup"><span data-stu-id="f34ed-231">After you have extracted and stored the tenant ID, you can obtain subsequent access tokens without requiring the tenant admin to sign in.</span></span>


## <a name="request-access-tokens-from-azure-ad"></a><span data-ttu-id="f34ed-232">Fordern Sie ein Zugriffstoken von Azure AD an.</span><span class="sxs-lookup"><span data-stu-id="f34ed-232">Request and acquire an access token from Azure AD</span></span>

<span data-ttu-id="f34ed-233">Es gibt zwei Methoden, um Zugriffstoken von Azure AD anzufordern:</span><span class="sxs-lookup"><span data-stu-id="f34ed-233">There are two methods for requesting access tokens from Azure AD:</span></span>

- <span data-ttu-id="f34ed-234">Der [Genehmigungsprozess mit Autorisierungscode](https://msdn.microsoft.com/en-us/library/azure/dn645542.aspx) beinhaltet, dass eine Mandantenadministrator seine ausdrückliche Genehmigung erteilt, wodurch ein Autorisierungscode an Ihre Anwendung zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="f34ed-234">The [Authorization Code Grant Flow](https://msdn.microsoft.com/en-us/library/azure/dn645542.aspx) involves a tenant admin granting explicit consent, which returns an authorization code to your application.</span></span> <span data-ttu-id="f34ed-235">Ihre Anwendung tauscht dann den Autorisierungscode gegen ein Zugriffstoken aus.</span><span class="sxs-lookup"><span data-stu-id="f34ed-235">Your application then exchanges the authorization code for an access token.</span></span> <span data-ttu-id="f34ed-236">Diese Methode ist erforderlich, um die erste Zustimmung dafür zu erhalten, die Ihre Anwendung benötigt, um mittels der API auf Mandantendaten zuzugreifen. Dieses erste Zugriffstoken ist erforderlich, um die Mandanten-ID zu erhalten und zu speichern.</span><span class="sxs-lookup"><span data-stu-id="f34ed-236">This method is required to obtain the initial consent that your application needs to access the tenant data by using the API, and this first access token is needed in order to obtain and store the tenant ID.</span></span>
    
- <span data-ttu-id="f34ed-237">Die [Genehmigungsprozess mit Client-Anmeldedaten](https://msdn.microsoft.com/de-DE/library/azure/dn645543.aspx) ermöglicht es Ihrer Anwendung, nachfolgende Zugriffstoken anzufordern, wenn alte ihre Gültigkeit verlieren, ohne dass der Mandantenadministrator sich anmelden und seine ausdrückliche Zustimmung erteilen muss.</span><span class="sxs-lookup"><span data-stu-id="f34ed-237">The [Client Credentials Grant Flow](https://msdn.microsoft.com/de-DE/library/azure/dn645543.aspx) allows your application to request subsequent access tokens as old ones expire, without requiring the tenant admin to sign in and explicitly grant consent.</span></span> <span data-ttu-id="f34ed-238">Diese Methode muss für Anwendungen verwendet werden, die fortlaufend im Hintergrund ausgeführt werden, und APIs aufrufen, nachdem die erste Zustimmung durch den Mandantenadministrator erteilt wurde.</span><span class="sxs-lookup"><span data-stu-id="f34ed-238">This method must be used for applications that run continuously in the background calling the APIs once the initial tenant admin consent has been granted.</span></span>
    

### <a name="request-an-access-token-using-the-authorization-code"></a><span data-ttu-id="f34ed-239">Zugriffstoken mithilfe des Autorisierungscodes anfordern</span><span class="sxs-lookup"><span data-stu-id="f34ed-239">Request an access token using the authorization code</span></span>

<span data-ttu-id="f34ed-240">Nachdem ein Mandantenadministrator seine Zustimmung erteilt, erhält Ihre Anwendung einen Autorisierungscode als Abfrage-Zeichenfolgeparameter, wenn Azure AD den Mandantenadministrator an die angegebene URL weiterleitet.</span><span class="sxs-lookup"><span data-stu-id="f34ed-240">After a tenant admin grants consent, your application receives an authorization code as a query string parameter when Azure AD redirects the tenant admin to your designated URL.</span></span>

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

<span data-ttu-id="f34ed-241">Ihre Anwendung stelle einen HTTP REST POST an Azure AD, um den Autorisierungscode gegen ein Zugriffstoken auszutauschen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-241">Your application makes an HTTP REST POST to Azure AD to exchange the authorization code for an access token.</span></span> <span data-ttu-id="f34ed-242">Da die Mandanten-ID noch nicht bekannt ist, wird der POST an den „herkömmlichen“ Endpunkt gestellt, bei dem die Mandanten-ID nicht in der URL enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="f34ed-242">Because the tenant ID is not yet known, the POST will be to the "common" endpoint, which does not have the tenant ID embedded in the URL:</span></span>

```http
https://login.windows.net/common/oauth2/token
```

<span data-ttu-id="f34ed-243">Der Inhalt des POST enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="f34ed-243">The body of the POST contains the following:</span></span>

```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code= AAABAAAAvPM1KaPlrEqdFSB...
```

#### <a name="sample-request"></a><span data-ttu-id="f34ed-244">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="f34ed-244">Sample request</span></span>

```json
POST https://login.windows.net/common/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 944

resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code=AAABAAAAvPM1KaPlrEqdFSB...
```

<br/>

<span data-ttu-id="f34ed-245">Der Inhalt der Antwort wird einige Eigenschaften enthalten, darunter das Zugriffstoken.</span><span class="sxs-lookup"><span data-stu-id="f34ed-245">The body of the response will include several properties, including the access token.</span></span> 

#### <a name="sample-response"></a><span data-ttu-id="f34ed-246">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="f34ed-246">Sample response</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 3265

{"expires_in":"3599","token_type":"Bearer","scope":"ActivityFeed.Read ActivityReports.Read ServiceHealth.Read","expires_on":"1438290275","not_before":"1438286375","resource":"https://manage.office.com","access_token":"eyJ0eX...","refresh_token":"AAABAAA...","id_token":"eyJ0eXAi..."}
```

<span data-ttu-id="f34ed-247">Das zurückgegebene Zugriffstoken ist ein JWT-Token und enthält Informationen über den Administrator, der seine Zustimmung erteilt hat, und die Anwendung, die Zugriff angefordert hat.</span><span class="sxs-lookup"><span data-stu-id="f34ed-247">The access token that is returned is a JWT token that includes information about both the admin that granted consent and the application requesting access.</span></span> <span data-ttu-id="f34ed-248">Es folgt ein Beispiel für ein uncodiertes Token.</span><span class="sxs-lookup"><span data-stu-id="f34ed-248">The following code shows an example of a token file.</span></span> <span data-ttu-id="f34ed-249">Ihre Anwendung muss die Mandanten-ID „tid“ aus diesem Token extrahieren und diese speichern, damit sie verwendet werden kann, um weitere Zugriffstoken anzufordern, wenn vorhandene ihre Gültigkeit verlieren, ohne dass eine weitere Interaktion eines Administrators erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="f34ed-249">Your application must extract the tenant ID "tid" from this token and store it so that it can be used to request additional access tokens as they expire, without further admin interaction.</span></span>

#### <a name="sample-token"></a><span data-ttu-id="f34ed-250">Beispieltoken</span><span class="sxs-lookup"><span data-stu-id="f34ed-250">Sample token</span></span>

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1427246416,
  "nbf": 1427246416,
  "exp": 1427250316,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "amr": [
    "pwd"
  ],
  "oid": "1cef1fdb-ff52-48c4-8e4e-dfb5ea83d357",
  "upn": "admin@contoso.onmicrosoft.com",
  "puid": "1003BFFD8EC47CA6",
  "sub": "7XpD5OWAXM1OWmKiVKh1FOkKXV4N3OSRol6mz1pxxhU",
  "given_name": "John",
  "family_name": "Doe",
  "name": "Contoso, Inc.",
  "unique_name": "admin@contoso.onmicrosoft.com",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1",
  "scp": "ActivityFeed.Read ServiceHealth.Read",
  "acr": "1"
}
```


### <a name="request-an-access-token-by-using-client-credentials"></a><span data-ttu-id="f34ed-251">Fordern Sie mit Client-Anmeldeinformationen ein Zugriffstoken an</span><span class="sxs-lookup"><span data-stu-id="f34ed-251">Request an access token by using client credentials</span></span>

<span data-ttu-id="f34ed-252">Sobald die Mandanten-ID bekannt ist, kann Ihre Anwendung Dienst-zu-Dienst-Anrufe zu Azure AD durchführen, um weitere Zugriffstoken anzufordern, wenn vorhandene ihre Gültigkeit verlieren.</span><span class="sxs-lookup"><span data-stu-id="f34ed-252">After the tenant ID is known, your application can make service-to-service calls to Azure AD to request additional access tokens as they expire.</span></span> <span data-ttu-id="f34ed-253">Diese Token enthalten ausschließlich Informationen über die anfragende Anwendung und nicht über den Administrator, der die erste Zustimmung erteilt hat.</span><span class="sxs-lookup"><span data-stu-id="f34ed-253">These tokens include information only about the requesting application and not about the admin that originally granted consent.</span></span> <span data-ttu-id="f34ed-254">Dienst-zu-Dienst-Aufrufe erfordern, dass Ihre Anwendung ein X.509-Zertifikat verwendet, um Client Assertion in Form eines base64-codierten, SHA256-signierten JWT Bearer-Token zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-254">Service-to-service calls require that your application use an X.509 certificate to create client assertion in the form of a base64-encoded, SHA256 signed JWT bearer token.</span></span>

<span data-ttu-id="f34ed-255">Wenn Sie die Anwendung in .NET entwickeln, können Sie mithilfe der [Azure Active Directory Authentication Library (ADAL)](https://docs.microsoft.com/de-DE/azure/active-directory/develop/active-directory-authentication-libraries) Client Assertions erstellen.</span><span class="sxs-lookup"><span data-stu-id="f34ed-255">When you are developing your application in .NET, you can use the [Azure AD Authentication Library (ADAL)](https://docs.microsoft.com/de-DE/azure/active-directory/develop/active-directory-authentication-libraries) to create client assertions.</span></span> <span data-ttu-id="f34ed-256">Andere Entwicklungsplattformen sollten ähnliche Bibliotheken haben.</span><span class="sxs-lookup"><span data-stu-id="f34ed-256">Other development platforms should have similar libraries.</span></span>

<span data-ttu-id="f34ed-257">Ein nicht codiertes JWT-Token besteht aus einer Kopfzeile und einer Nutzlast, die die folgenden Eigenschaften haben.</span><span class="sxs-lookup"><span data-stu-id="f34ed-257">An un-encoded JWT token consists of a header and payload that have the following properties.</span></span>

```json
HEADER:

{
  "alg": "RS256",
  "x5t": "{thumbprint of your X.509 certificate used to sign the token",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/{tenantid}/oauth2/token",
  "iss": "{your app client ID}",
  "sub": "{your app client ID}"
  "jti": "{random GUID}",
  "nbf": {epoch time, before which the token is not valid},
  "exp": {epoch time, after which the token is not valid},
}

```

#### <a name="sample-jwt-token"></a><span data-ttu-id="f34ed-258">Beispiel JWT-Token</span><span class="sxs-lookup"><span data-stu-id="f34ed-258">Sample JWT token</span></span>


```json
HEADER:

{
  "alg": "RS256",
  "x5t": "YyfshJC3rPQ-kpGo5dUaiY5t3iU",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token",
  "iss": "a6099727-6b7b-482c-b509-1df309acc563",
  "sub": "a6099727-6b7b-482c-b509-1df309acc563"
  "jti": "0ce254c4-81b1-4a2e-8436-9a8c3b49dfb9",
  "nbf": 1427248048,
  "exp": 1427248648,
}
```

<span data-ttu-id="f34ed-259">Die Client Assertion wird dann an Azure AD übergeben als Teil eines Dienst-zu-Dienst-Anrufs, um ein Zugriffstoken anzufordern.</span><span class="sxs-lookup"><span data-stu-id="f34ed-259">The client assertion is then passed to Azure AD as part of a service-to-service call to request an access token.</span></span> <span data-ttu-id="f34ed-260">Bei Verwendung der Client-Anmeldeinformationen zur Anforderung eines Zugriffstoken verwenden Sie ein HTTP POST für einen mandantenspezifischen Endpunkt, wo die zuvor extrahierten und gespeicherte Mandanten-ID in der URL eingebettet ist.</span><span class="sxs-lookup"><span data-stu-id="f34ed-260">When using client credentials to request an access token, use an HTTP POST to a tenant-specific endpoint, where the previously extracted and stored tenant ID is embedded in the URL.</span></span>


```http
https://login.windows.net/{tenantid}/oauth2/token
```

<span data-ttu-id="f34ed-261">Der Inhalt des POST enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="f34ed-261">The body of the POST contains the following:</span></span>


```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id={your_app_client_id}&amp;grant_type=client_credentials&amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion={encoded_signed_JWT_token}
```

#### <a name="sample-request"></a><span data-ttu-id="f34ed-262">Beispielanfrage</span><span class="sxs-lookup"><span data-stu-id="f34ed-262">Sample request</span></span>

```json
POST https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 994

resource=https%3A%2F%2Fmanage.office.com&amp;client_id= a6099727-6b7b-482c-b509-1df309acc563&amp;grant_type=client_credentials &amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Ill5ZnNoSkMzclBRLWtwR281ZFVhaVk1dDNpVSJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ud2luZG93cy5uZXRcLzQxNDYzZjUzLTg4MTItNDBmNC04OTBmLTg2NWJmNmUzNTE5MFwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQyNzI0ODY0OCwiaXNzIjoiYTYwOTk3MjctNmI3Yi00ODJjLWI1MDktMWRmMzA5YWNjNTYzIiwianRpIjoiMGNlMjU0YzQtODFiMS00YTJlLTg0MzYtOWE4YzNiNDlkZmI5IiwibmJmIjoxNDI3MjQ4MDQ4LCJzdWIiOiJhNjA5OTcyNy02YjdiLTQ4MmMtYjUwOS0xZGYzMDlhY2M1NjMifQ.vfDrmCjiXgoj2JrTkwyOpr-NOeQTzlXQcGlKGNpLLe0oh4Zvjdcim5C7E0UbI3Z2yb9uKQdx9G7GeqS-gVc9kNV_XSSNP4wEQj3iYNKpf_JD2ikUVIWBkOg41BiTuknRJAYOMjiuBE2a6Wyk-vPCs_JMd7Sr-N3LiNZ-TjluuVzWHfok_HWz_wH8AzdoMF3S0HtrjNd9Ld5eI7MVMt4OTpRfh-Syofi7Ow0HN07nKT5FYeC_ThBpGiIoODnMQQtDA2tM7D3D6OlLQRgLfI8ir73PVXWL7V7Zj2RcOiooIeXx38dvuSwYreJYtdphmrDBZ2ehqtduzUZhaHL1iDvLlw
```

<span data-ttu-id="f34ed-263">Die Antwort wird die gleiche sein wie zuvor, aber das Token wird nicht dieselben Eigenschaften haben, da es keine Eigenschaften des Administrators enthält, der die Zustimmung erteilt hat.</span><span class="sxs-lookup"><span data-stu-id="f34ed-263">The response will be the same as before, but the token will not have the same properties, because it does not contain properties of the admin that granted consent.</span></span> 

#### <a name="sample-response"></a><span data-ttu-id="f34ed-264">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="f34ed-264">Sample response</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 1276

{"token_type":"Bearer","expires_in":"3599","expires_on":"1431659094","not_before":"1431655194","resource":"https://manage.office.com","access_token":"eyJ0eXAiOiJKV1QiL..."}
```

#### <a name="sample-access-token"></a><span data-ttu-id="f34ed-265">Beispiel für Zugriffstoken</span><span class="sxs-lookup"><span data-stu-id="f34ed-265">Sample access token</span></span>

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1431655194,
  "nbf": 1431655194,
  "exp": 1431659094,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "roles": [
    "ServiceHealth.Read",
    "ActivityFeed.Read"
  ],
  "oid": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "sub": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "idp": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1"
}
```


## <a name="build-your-app"></a><span data-ttu-id="f34ed-266">Erstellen Sie Ihre Anwendung</span><span class="sxs-lookup"><span data-stu-id="f34ed-266">Build your app</span></span>

<span data-ttu-id="f34ed-267">Nachdem Sie die Anwendung in Azure AD registriert und die erforderlichen Berechtigungen konfiguriert haben, können Sie Ihre Anwendung erstellt.</span><span class="sxs-lookup"><span data-stu-id="f34ed-267">Now that you have registered your app in Azure AD and configured it with the necessary permissions, you're ready to build your app.</span></span> <span data-ttu-id="f34ed-268">Folgend finden Sie einige der wichtigsten Aspekte, die beim Entwerfen und Erstellen Ihrer App zu berücksichtigen sind:</span><span class="sxs-lookup"><span data-stu-id="f34ed-268">The following are some of the key aspects to consider when designing and building your app:</span></span>

- <span data-ttu-id="f34ed-269">**Die Zustimmungsfunktionalität**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-269">**The consent experience**.</span></span> <span data-ttu-id="f34ed-270">Um die Zustimmung Ihrer Kunden zu erhalten, müssen Sie diese in einem Browser zur Azure AD-Webseite weiterleiten, indem Sie die speziell erstellte URL verwenden, die vorher hier beschrieben wurde. Sie müssen zudem über eine Webseite verfügen, zu der Azure AD den Administrator weiterleitet, wenn dieser seine Zustimmung erteilt hat.</span><span class="sxs-lookup"><span data-stu-id="f34ed-270">To obtain consent from your customers, you must direct them in a browser to the Azure AD website, using the specially constructed URL described previously, and you must have a website to which Azure AD will redirect the admin once they grant consent.</span></span> <span data-ttu-id="f34ed-271">Diese Webseite muss den Autorisierungscode aus der URL extrahieren und diesen verwenden, um ein Zugriffstoken anzufordern, von dem sie die Mandanten-ID erält.</span><span class="sxs-lookup"><span data-stu-id="f34ed-271">This website must extract the authorization code from the URL and use it to request an access token from which it can obtain the tenant ID.</span></span>
    
- <span data-ttu-id="f34ed-272">**Speichern Sie die Mandanten-ID in Ihrem System**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-272">**Store the tenant ID in your system**.</span></span> <span data-ttu-id="f34ed-273">Diese wird beim Anfordern des Zugriffstoken von Azure AD und beim Aufrufen der Office-Management-APIs benötigt.</span><span class="sxs-lookup"><span data-stu-id="f34ed-273">This will be needed when requesting access tokens from Azure AD and when calling the Office Management APIs.</span></span>
    
- <span data-ttu-id="f34ed-274">**Verwalten von Zugriffstoken**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-274">**Managing access tokens**.</span></span> <span data-ttu-id="f34ed-275">Sie benötigen eine Komponente, die nach Bedarf Zugriffstoken anfordert und verwaltet.</span><span class="sxs-lookup"><span data-stu-id="f34ed-275">You will need a component that requests and manages access tokens as needed.</span></span> <span data-ttu-id="f34ed-276">Wenn Ihre App in regelmäßigen Abständen die APIs aufruft, kann sie Token nach Bedarf anfordern. Wenn sie die APIs ständig zum Abrufen von Daten aufruft, kann sie Token in regelmäßigen Abständen (z. B. alle 45 Minuten) anfordern.</span><span class="sxs-lookup"><span data-stu-id="f34ed-276">If your app calls the APIs periodically, it can request tokens on demand, or if it calls the APIs continuously to retrieve data, it can request tokens at regular intervals (for example, every 45 minutes).</span></span>
    
- <span data-ttu-id="f34ed-277">**Implementieren eines Webhook-Listener** je nach Bedarf der jeweiligen-API, die Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="f34ed-277">**Implement a webhook listener** as needed by the particular API you are using.</span></span>
    
- <span data-ttu-id="f34ed-278">**Abrufen und Speichern von Daten**.</span><span class="sxs-lookup"><span data-stu-id="f34ed-278">**Data retrieval and storage**.</span></span> <span data-ttu-id="f34ed-279">Sie benötigen eine Komponente, die Daten für jeden Mandanten, abruft, entweder kontinuierlich oder als Reaktion auf Webhook-Benachrichtigungen, je nach der bestimmten-API, die Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="f34ed-279">You'll need a component that retrieves data for each tenant, either by using continuous polling or in response to webhook notifications, depending on the particular API you are using.</span></span>
    
