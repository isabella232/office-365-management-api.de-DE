---
ms.technology: o365-service-communications
ms.TocTitle: Get started with Office 365 Management APIs
title: Erste Schritte mit den Office 365-Verwaltungs-APIs
description: Die APIs verwenden Azure AD, um Authentifizierungsdienste bereitzustellen, mit denen Sie der Anwendung entsprechende Rechte für den Zugriff auf diese Dienste erteilen können.
ms.ContentId: 74137c9a-29e0-b588-6122-26f4d2c5e3fc
ms.topic: reference (API)
ms.date: ''
ms.localizationpriority: high
ms.openlocfilehash: ef4ea62f03eb9d536bf42234d9a9f5b28de005e8
ms.sourcegitcommit: 6c9efd49e6406ee72edc7450afa811d6c660992c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/08/2021
ms.locfileid: "60235894"
---
# <a name="get-started-with-office-365-management-apis"></a>Erste Schritte mit den Office 365-Verwaltungs-APIs

Wenn Sie eine Anwendung erstellen, die Zugriff auf gesicherte Dienste wie die Office 365-Management-APIs benötigt, müssen Sie dem Dienst mitteilen, dass Ihre Anwendung Zugriffsrechte hat. Die Office 365-Management-APIs verwenden Azure AD, um Authentifizierungsdienste bereitzustellen, mit denen Sie der Anwendung entsprechende Rechte für den Zugriff auf diese Dienste erteilen können. 

Es gibt vier zentrale Schritte:

1. **Registrieren Sie Ihre Anwendung in Azure AD**. Um Ihrer Anwendung den Zugriff auf die Office 365-Management-APIs zu ermöglichen, müssen Sie Ihre Anwendung bei Azure AD registrieren. Dadurch können Sie eine Identität für Ihre Anwendung einrichten und geben die Berechtigungsstufen angeben, die sie für den Zugriff auf die APIs benötigt.
    
2. **Erhalten Sie die Genehmigung durch einen Office 365-Mandanten-Admin**. Ein Office 365-Mandanten-Admin muss eine Genehmigung erteilen, damit Ihre Anwendung auf mittels Office 365-Management-APIs auf Mandantendaten zugreifen kann. Der Genehmigungsprozess ist eine browserbasierte Praxis, bei der sich der Mandantenadministrator in der **Azure AD Genehmigung-Benutzeroberfläche** anmelden und die von Ihrer Anwendung angeforderten Berechtigungen überprüfen muss und diese Anfrage gewährt oder verweigert. Nachdem die Genehmigung erteilt wurde, leitet die Benutzeroberfläche den Benutzer über einen Authentifizierungscode in der URL zurück zu Ihrer Anwendung. Ihre Anwendung führt einen Dienst-zu-Dienst-Anruf zu Azure AD durch, um diesen Autorisierungscode in ein Zugriffs-Token umzuwandeln, das Informationen über den Mandantenadministrator und Ihre Anwendung enthält. Die Mandanten-ID muss aus dem Zugriffstoken entnommen werden und für die zukünftige Nutzung aufbewahrt werden.
    
3. **Fordern Sie ein Zugriffstoken von Azure AD an**. Mit den in Azure Active Directory konfigurierten Anmeldeinformationen Ihrer Anwendung fordert Ihre Anwendung fortlaufend zusätzliche Zugriffstoken für einen genehmigten Mandanten an, ohne dass eine weitere Interaktion mit einem Mandantenadministrator benötigt wird. Diese Zugriffstoken werden als „nur App“-Token bezeichnet, da sie keine Informationen zum Mandantenadministrator beinhalten.
    
4. **Aufruf der Office 365-Management-APIs**. Die Nur-App-Zugriffstoken werden an die Office 365-Management-APIs übergeben, um Ihre Anwendung zu authentifizieren und zu autorisieren.
    
Das folgende Diagramm zeigt die Abfolge von Genehmigungs- und Zugriffstoken-Anfragen.

![Initialer Authorisierungsvorgang für Verwaltungs-APIs](images/authorization-flow.png)

> [!IMPORTANT]
> Bevor Sie über die Office 365-Verwaltungsaktivitäts-API auf Daten zugreifen können, müssen Sie die einheitliche Überwachungsprotokollierung für Ihre Office 365-Organisation aktivieren. Dazu aktivieren Sie das Office 365-Überwachungsprotokoll. Anweisungen hierzu finden Sie unter [Aktivieren und Deaktivieren der Office 365-Überwachungsprotokollsuche](/office365/securitycompliance/turn-audit-log-search-on-or-off). <br/><br/>Wenn Sie nur die Office 365-Dienstkommunikations-API verwenden, ist die Aktivierung der einheitlichen Überwachungsprotokollierung nicht nötig.

## <a name="register-your-application-in-azure-ad"></a>Registrieren Sie Ihre Anwendung in Azure AD.

Die Office 365-Management-APIs verwenden Azure AD zur sicheren Authentifizierung der Office 365-Mandantendaten. Für den Zugriff auf die Office 365-Management-APIs müssen Sie die Anwendung in Azure Active Directory registrieren, und als Teil der Konfiguration die Berechtigungsstufen, die Ihre Anwendung für den Zugriff auf die APIs benötigt, angeben.

### <a name="prerequisites"></a>Voraussetzungen

Wenn Sie die Anwendung in Azure AD registriert haben, benötigen Sie ein Abonnement für Office 365 und ein Abonnement für Azure, das mit Ihrem Office 365-Abonnement verknüpft ist. Für den Anfang können Sie Testabonnements sowohl für Office 365 als auch für Azure verwenden. Weitere Informationen finden Sie unter [Willkommen beim Office 365-Entwicklerprogramm](/office/developer-program/office-365-developer-program).

### <a name="use-the-azure-portal-to-register-your-application-in-azure-ad"></a>Nutzen Sie das Azure-Portal, um Ihre Anwendung in Azure AD zu registrieren.

Nachdem Sie einen Microsoft-Mandanten mit den entsprechenden Abonnements haben, können Sie Ihre Anwendung in Azure AD registrieren.

1. Melden Sie sich im [Azure-Portal](https://portal.azure.com) an, und verwenden Sie dabei die Anmeldeinformationen Ihres Microsoft-Mandanten, der über das Office 365-Abonnement verfügt, das Sie verwenden möchten. Sie können auch über einen Link auf das Azure-Portal zugreifen, der im linken Navigationsbereich im [Microsoft 365 Admin Center](https://admin.microsoft.com/) angezeigt wird.

2. Wählen Sie im linken Navigationsbereich **Azure Active Directory** (1) aus.

   ![Hauptseite des Azure-Portals](images/AzurePortal1.png)

3. Wählen Sie auf der Seite **Azure Active Directory** die Option **App-Registrierungen** (2) und dann **Neue Registrierung** (3) aus.

   ![Seite „App-Registrierungen“ in Azure Active Directory](images/AzureAppRegistration2.png)

4. Wählen Sie auf der Seite **App-Registrierungen** die Option **Neue Registrierung** aus.

   Es wird eine neue Seite angezeigt, auf der Sie die Registrierung Ihrer App starten können.

5. Führen Sie auf der Seite **Registrierung einer Anwendung** folgende Schritte aus:

   ![App-Registrierungsprozess](images/AzureAppRegistration3.png)

   1. Benennen Sie Ihre App.

   2. Wählen Sie aus, wer die App verwenden und auf die API zugreifen kann.

   3. Geben Sie bei Bedarf eine Umleitungs-URL für die Benutzerumleitung nach der Authentifizierung an.

6. Klicken Sie auf **Registrieren**, um die neue App zu registrieren.

### <a name="configure-your-application-properties-in-azure-ad"></a>Konfigurieren Sie Ihre Anwendungseigenschaften in Azure AD

Nachdem Ihre Anwendung registriert ist, gibt es mehrere wichtige Eigenschaften, die Sie angeben müssen, die bestimmen, wie Ihre Anwendung in Azure AD funktioniert und wie Mandantenadministratoren Ihrer Anwendung die Genehmigung für den Zugriff auf ihre Daten mittels den Office 365-Management-APIs erteilen.

Weitere Informationen zur Anwensungskonfiguration in Azure AD im Allgemeinen finden Sie unter [Anwendungs-Objekteigenschaften](/azure/active-directory/develop/active-directory-application-objects).

1. **Client-ID**. Dieser Wert wird von Azure AD automatisch generiert. Ihre Anwendung wird diesen Wert beim Anfordern von Genehmigungen von Mandantenadministratoren und beim Anfordern von „Nur App“-Token aus Azure AD verwenden.

2. **Die Anwendung hat mehrere Mandanten**. Für diese Eigenschaft muss **Ja** ausgewählt werden, damit Mandantenadministratoren Ihrer Anwendung die Genehmigung erteilen können, mit den Office 365-Management-APIs auf ihre Daten zuzugreifen. Wenn für diese Eigenschaft **Nein** ausgewählt ist, kann Ihre Anwendung ausschließlich auf Daten Ihres eigenen Mandanten zugreifen.

3. **Antwort-URL**. Dies ist die URL, zu der ein Mandantenadministrator weitergeleitet wird, nachdem er Ihrer Anwendung die Genehmigung für den Zugriff auf seine Daten mittels den Office 365 Management-APIs erteilt hat. Sie können bei Bedarf mehrere Antwort-URLs konfigurieren. Azure legt automatisch die erste so fest, dass sie mit der Anmelde-URL übereinstimmt, die Sie beim Erstellen der Anwendung angegeben haben, aber Sie können diesen Wert wenn nötig ändern.

Wählen Sie unbedingt **Speichern**, nachdem Sie Änderungen an dieser Eigenschaften vorgenommen haben.

### <a name="generate-a-new-key-for-your-application"></a>Erstellen Sie einen neuen Schlüssel für Ihre Anwendung

Schlüssel, auch als *geheime Clientschlüssel* bezeichnet, werden verwendet, wenn ein Autorisierungscode gegen eine Zugriffstoken ausgetauscht wird.

1. Wählen Sie auf der Seite **Azure Active Directory** im Azure-Portal **App-Registrierungen** und dann Ihre Anwendung aus.

    ![Auswahl der App, die Sie gerade registriert haben](images/AzureAppRegistration4.png)

2. Nachdem die Seite für Ihre App angezeigt wurde, wählen Sie **Zertifikate & Geheimnisse** (1) im linken Bereich aus. Auf dieser Seite können Sie Zertifikate hochladen und neue geheime Clientschlüssel (2) erstellen.

    ![Die Seite „Zertifikate und Geheimnisse“ der App](images\AzureAppRegistrationCertificatesSecrets.png)

3. Auf der Seite **Zertifikate und Geheimnisse** (1) wählen Sie **Neuer geheimer Clientschlüssel** (2) aus, geben eine Beschreibung ein, wählen die Dauer für Ihren Schlüssel (3) aus, und wählen dann **Hinzufügen** (4) aus.

   ![Erstellen eines geheimen Clientschlüssels](images\AzureAppRegistration5.png)

4. Nach dem Erstellen des geheimen Clientschlüssels wird der Wert unter **geheimer Clientschlüssel** (2) angezeigt. Klicken Sie auf das Symbol „Zwischenablage“ (3), um den Wert des geheimen Clientschlüssels in die Zwischenablage zu kopieren.

   ![Kopieren Sie den Wert des geheimen Clientschlüssels in die Zwischenablage, und speichern Sie ihn zur späteren Verwendung.](images\AzureAppRegistration6.png)

   > [!IMPORTANT]
   > Azure zeigt den Wert des geheimen Clientschlüssels nur zum Zeitpunkt der ersten Generierung an. Sie können nicht zu dieser Seite zurückkehren und den Wert des geheimen Clientschlüssels später abrufen. Stellen Sie sicher, dass Sie ihn kopieren und an einem sicheren Ort speichern, damit Sie ihn später verwenden können.

### <a name="configure-an-x509-certificate-to-enable-service-to-service-calls"></a>Konfigurieren eines x. 509-Zertifikats, um Dienst-zu-Dienst-Aufrufe zu ermöglichen

Eine Anwendung, die im Hintergrund ausgeführt wird, wie ein Dämonprozess oder ein Dienst, kann Client-Anmeldeinformationen nutzen, um ein „Nur App“-Zugriffstoken anzufordern, ohne fortlaufend eine Genehmigung vom Mandantenadministrator anzufordern, nachdem eine erste Genehmigung erteilt wurde.

Weitere Informationen finden Sie unter [Dienst-zu-Dienst-Anrufe mithilfe von Client-Anmeldeinformationen](https://msdn.microsoft.com/library/azure/dn645543.aspx).

Sie müssen ein X.509-Zertifikat für Ihre Anwendung erstellen, das als Client-Anmeldedaten dient, wenn ein „Nur App“-Token von Azure AD angefordert wird. Dieser Prozess besteht aus zwei Schritten:

- Rufen Sie ein X.509-Zertifikat ab. Sie können ein selbstsigniertes Zertifikat oder ein von einer öffentlichen, vertrauenswürdigen Zertifizierungsstelle ausgestelltes Zertifikat verwenden..

- Ändern Sie Ihr Anwendungsmanifest, um den Fingerabdruck und den öffentlichen Schlüssel Ihres Zertifikats einzuschließen.

Die folgenden Anweisungen zeigen Ihnen, wie Sie das Visual Studio oder das Windows SDK _Makecert_ tool verwenden, um ein selbstsigniertes Zertifikat zu erstellen und den öffentlichen Schlüssel in eine base64-codierte Datei zu exportieren.

1. Führen Sie in der Befehlszeile Folgendes aus:

   ```powershell
    makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 03/15/2015 -e 03/15/2017 -ss my -len 2048
   ```

   > [!NOTE]
   > Wenn Sie das x. 509-Zertifikat generieren, stellen Sie sicher, dass die Länge des Schlüssels mindestens 2048 beträgt. Kürzere Schlüssellängen werden nicht als gültige Schlüssel akzeptiert.

2. Öffnen Sie die Snap-In MMC-Zertifikate und verbinden Sie sich mit Ihrem Benutzerkonto.

3. Suchen Sie das neue Zertifikat im Ordner „Persönlich“, und exportieren Sie den öffentlichen Schlüssel in eine base64-codierte Datei (z. B. `mycompanyname.cer`). Ihre Anwendung verwendet dieses Zertifikat zum Kommunizieren mit Azure AD. Stellen Sie daher sicher, dass Sie auch Zugriff auf den privat Schlüssel erhalten.

   > [!NOTE]
   > Sie können Windows PowerShell verwenden, um den Fingerabdruck und den base64-codierten öffentlichen Schlüssel zu extrahieren. Andere Plattformen bieten ähnliche Tools zum Abrufen der Eigenschaften von Zertifikaten.

4. Geben Sie in einer Windows PowerShell-Eingabeaufforderung Folgendes ein und führen Sie es aus:

   ```powershell
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $cer.Import("mycer.cer")
    $bin = $cer.GetRawCertData()
    $base64Value = [System.Convert]::ToBase64String($bin)
    $bin = $cer.GetCertHash()
    $base64Thumbprint = [System.Convert]::ToBase64String($bin)
    $keyid = [System.Guid]::NewGuid().ToString()
   ```

5. Speichern Sie die Werte für `$base64Thumbprint`, `$base64Value`, und `$keyid`, die verwendet werden, wenn Sie Ihr Anwendungsmanifest in den nächsten Schritten aktualisieren.

   Mit den aus dem Zertifikat extrahierten Werten und der generierten Schlüssel-ID müssen Sie nun Ihr Anwendungsmanifest in Azure AD aktualisieren.

6. Wechseln Sie im Azure-Portal zu **App-Registrierungen** > **Alle Anwendungen**, wählen Sie Ihre Anwendung und dann **Manifest** im linken Bereich aus.

7. Wählen Sie in der oberen Navigationsleiste auf der Seite **Manifest** (1) die Option **Download** (2) aus.

   ![Herunterladen des Manifests zum Bearbeiten](images/AzureAppRegistration7.png)

8. Öffnen Sie das heruntergeladene Manifest in einem Editor, und ersetzen Sie die leere Eigenschaft *keyCredentials* durch die folgende JSON:
    
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
   > Die [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType)-Eigenschaft ist eine Sammlung, die es ermöglicht, mehrere X.509-Zertifikate für Rollover-Szenarien hochzuladen oder Zertifikate für Kompromiss-Szenarien zu löschen.

9. Speichern Sie Ihre Änderungen und laden Sie die aktualisierte App-Manifestdatei hoch, indem Sie auf **Manifest verwalten** in der Befehlsleiste klicken, **Manifest hochladen** wählen, zu Ihrer aktualisierten Manifestdatei navigieren und diese dann auswählen.

### <a name="specify-the-permissions-your-app-requires-to-access-the-office-365-management-apis"></a>Geben Sie die Berechtigungen, die Ihre Anwnedung benötigt, um auf die Office 365-Management-APIs zuzugreifen, an.

Schließlich müssen Sie genau angeben, welche Berechtigungen Ihre Anwendung für die Office 365 Management-APIs benötigt. Zu diesem Zweck müssen Sie einen Zugriff auf die Office 365-Management-APIs zu Ihrer Anwendung hinzufügen und dann die Berechtigung(en) auswählen, die Sie benötigen.

1. Wechseln Sie im Azure-Portal zu **App-Registrierungen** > **Alle Anwendungen**, wählen Sie Ihre Anwendung und dann **API-Berechtigungen** (1) im linken Bereich aus. Klicken Sie auf **Eine Berechtigung hinzufügen** (2), um die **Anforderungs-API-Berechtigung** (3) anzuzeigen.

   ![API-Berechtigungen hinzufügen](images/AzureAppRegistration8.png)

2. Wählen Sie auf der Registerkarte **Microsoft-APIs** die Option **Office 365-Management-APIs** (4) aus.

   ![Auswählen von Office 365-Management-APIs auf der Registerkarte „Microsoft-APIs“](images/AzureAppRegistration9.png)

3. Wählen Sie auf der Flyoutseite die folgenden Berechtigungstypen (3) aus, die für Ihre App erforderlich sind, und klicken Sie dann auf **Berechtigungen hinzufügen**.

   ![Auswählen von Berechtigungstypen für Ihre App](images/AzureAppRegistration10.png)

   1. **Delegierte Berechtigungen**. Ermöglicht Ihrer Client-App das Ausführen von Vorgängen im Namen des angemeldeten Benutzers, z. B. das Lesen von E-Mails oder das Ändern des Benutzerprofils.

   2. **Anwendungsberechtigungen**. Berechtigungen, die es der Client-App ermöglichen, sich selbst ohne Benutzerinteraktion oder -zustimmung zu authentifizieren, z. B. eine App, die von Hintergrunddiensten oder Daemon-Apps verwendet wird.

4. Office-Management-APIs werden jetzt in der Liste der Anwendungen angezeigt, für die Ihre App Berechtigungen benötigt. Wählen Sie bei Bedarf sowohl unter **Anwendungsberechtigungen** als auch unter **Delegierte Berechtigungen** die Berechtigungen aus, die Ihre Anwendung benötigt. Weitere Informationen zu den einzelnen Berechtigungen finden Sie unter den jeweiligen API-Referenzen.  

   ![API-Berechtigungen für Ihre App](images/AzureAppRegistration11.png)

5. Wählen Sie **Administrator-Zustimmung für „Mandantenname“ gewähren** aus, um den Berechtigungen zuzustimmen, die Ihrer App erteilt wurden.

## <a name="get-office-365-tenant-admin-consent"></a>Erhalten Sie die Genehmigung durch einen Office 365-Mandantenadmin.

Nun, da Ihre Anwendung mit den Berechtigungen konfiguriert ist, die sie für die Verwendung der Office 365-Management APIs benötigt, muss ein Mandantenadministrator diese Berechtigungen ausdrücklich für Ihre Anwendung gewähren, damit Sie mittels der APIs auf dessen Mandantendaten zugreifen können. Um eine Genehmigung zu erteilen, muss sich der Mandantenadministrator in Azure AD anmelden. Dafür verwendet er die folgende eigens konstruierte URL, mittels derer er die von Ihrer Anwendung angefragten Berechtigungen einsehen kann. Dieser Schritt ist nicht erforderlich, wenn Sie APIs verwenden, um auf Daten aus Ihrem eigenen Mandanten zuzugreifen.

```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id={your_client_id}&redirect_uri={your_redirect_url }
```

Die Weiterleitungs-URL muss mit der Antwort-URL übereinstimmen oder ein untergeordneter Pfad einer der Antwort-URLs sein, die für Ihre Anwendung in Azure AD erstellt wurden.

Beispiel:

```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e&redirect_uri=http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F
```

Sie können die genehmigte URL testen, indem Sie diese in einen Browser kopieren und sich mit den Anmeldedaten eines Office 365-Admin für einen anderen Mandanten, als der, den Sie für die Registrierung der Anwendung verwendet haben, anmelden. Ihnen wird die Anfrage zur Berechtigungserteilung zur Nutzung der Office-Management-APIs für Ihre Anwendung angezeigt.

![Seite „Berechtigungszustimmung“](images/AzureAppRegistration12.png)

Nachdem Sie **Annehmen** ausgewählt haben, werden Sie zu der angegebenen Seite weitergeleitet und die Abfrage-Zeichenfolge wird einen Code enthalten.

Beispiel:

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

Ihre Anwendung verwendet diesen Autorisierungscode, um ein Zugriffstoken von Azure AD zu erhalten, aus dem die Mandanten-ID extrahiert werden kann. Nachdem Sie die Mandanten-ID extrahiert und gespeichert haben, können Sie nachfolgende Zugriffstoken beziehen, ohne dass eine Anmeldung als Mandantenadministrator notwendig ist.

## <a name="request-access-tokens-from-azure-ad"></a>Fordern Sie ein Zugriffstoken von Azure AD an.

Es gibt zwei Methoden, um Zugriffstoken von Azure AD anzufordern:

- Der [Genehmigungsprozess mit Autorisierungscode](https://msdn.microsoft.com/library/azure/dn645542.aspx) beinhaltet, dass eine Mandantenadministrator seine ausdrückliche Genehmigung erteilt, wodurch ein Autorisierungscode an Ihre Anwendung zurückgegeben wird. Ihre Anwendung tauscht dann den Autorisierungscode gegen ein Zugriffstoken aus. Diese Methode ist erforderlich, um die erste Zustimmung dafür zu erhalten, die Ihre Anwendung benötigt, um mittels der API auf Mandantendaten zuzugreifen. Dieses erste Zugriffstoken ist erforderlich, um die Mandanten-ID zu erhalten und zu speichern.
    
- Die [Genehmigungsprozess mit Client-Anmeldedaten](https://msdn.microsoft.com/library/azure/dn645543.aspx) ermöglicht es Ihrer Anwendung, nachfolgende Zugriffstoken anzufordern, wenn alte ihre Gültigkeit verlieren, ohne dass der Mandantenadministrator sich anmelden und seine ausdrückliche Zustimmung erteilen muss. Diese Methode muss für Anwendungen verwendet werden, die fortlaufend im Hintergrund ausgeführt werden, und APIs aufrufen, nachdem die erste Zustimmung durch den Mandantenadministrator erteilt wurde.
    

### <a name="request-an-access-token-using-the-authorization-code"></a>Zugriffstoken mithilfe des Autorisierungscodes anfordern

Nachdem ein Mandantenadministrator seine Zustimmung erteilt, erhält Ihre Anwendung einen Autorisierungscode als Abfrage-Zeichenfolgeparameter, wenn Azure AD den Mandantenadministrator an die angegebene URL weiterleitet.

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

Ihre Anwendung stelle einen HTTP REST POST an Azure AD, um den Autorisierungscode gegen ein Zugriffstoken auszutauschen. Da die Mandanten-ID noch nicht bekannt ist, wird der POST an den „herkömmlichen“ Endpunkt gestellt, bei dem die Mandanten-ID nicht in der URL enthalten ist:

```http
https://login.windows.net/common/oauth2/token
```

Der Inhalt des POST enthält Folgendes:

```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code= AAABAAAAvPM1KaPlrEqdFSB...
```

#### <a name="sample-request"></a>Beispielanfrage

```json
POST https://login.windows.net/common/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 944

resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code=AAABAAAAvPM1KaPlrEqdFSB...
```

<br/>

Der Inhalt der Antwort wird einige Eigenschaften enthalten, darunter das Zugriffstoken.

#### <a name="sample-response"></a>Beispielantwort

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 3265

{"expires_in":"3599","token_type":"Bearer","scope":"ActivityFeed.Read ActivityReports.Read ServiceHealth.Read","expires_on":"1438290275","not_before":"1438286375","resource":"https://manage.office.com","access_token":"eyJ0eX...","refresh_token":"AAABAAA...","id_token":"eyJ0eXAi..."}
```

Das zurückgegebene Zugriffstoken ist ein JWT-Token und enthält Informationen über den Administrator, der seine Zustimmung erteilt hat, und die Anwendung, die Zugriff angefordert hat. Es folgt ein Beispiel für ein uncodiertes Token. Ihre Anwendung muss die Mandanten-ID „tid“ aus diesem Token extrahieren und diese speichern, damit sie verwendet werden kann, um weitere Zugriffstoken anzufordern, wenn vorhandene ihre Gültigkeit verlieren, ohne dass eine weitere Interaktion eines Administrators erforderlich ist.

#### <a name="sample-token"></a>Beispieltoken

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

### <a name="request-an-access-token-by-using-client-credentials"></a>Fordern Sie mit Client-Anmeldeinformationen ein Zugriffstoken an

Sobald die Mandanten-ID bekannt ist, kann Ihre Anwendung Dienst-zu-Dienst-Anrufe zu Azure AD durchführen, um weitere Zugriffstoken anzufordern, wenn vorhandene ihre Gültigkeit verlieren. Diese Token enthalten ausschließlich Informationen über die anfragende Anwendung und nicht über den Administrator, der die erste Zustimmung erteilt hat. Dienst-zu-Dienst-Aufrufe erfordern, dass Ihre Anwendung ein X.509-Zertifikat verwendet, um Client Assertion in Form eines base64-codierten, SHA256-signierten JWT Bearer-Token zu erstellen.

Wenn Sie Ihre Anwendung in .NET entwickeln, können Sie die [Azure AD-Authentifizierungsbibliothek](/azure/active-directory/develop/active-directory-authentication-libraries) (Azure AD Authentication Library, ADAL) verwenden, um Clientzusicherungen zu erstellen. Andere Entwicklungsplattformen sollten über ähnliche Bibliotheken verfügen.

Ein nicht codiertes JWT-Token besteht aus einer Kopfzeile und einer Nutzlast, die die folgenden Eigenschaften haben.

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

#### <a name="sample-jwt-token"></a>Beispiel JWT-Token


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

Die Client Assertion wird dann an Azure AD übergeben als Teil eines Dienst-zu-Dienst-Anrufs, um ein Zugriffstoken anzufordern. Bei Verwendung der Client-Anmeldeinformationen zur Anforderung eines Zugriffstoken verwenden Sie ein HTTP POST für einen mandantenspezifischen Endpunkt, wo die zuvor extrahierten und gespeicherte Mandanten-ID in der URL eingebettet ist.


```http
https://login.windows.net/{tenantid}/oauth2/token
```

Der Inhalt des POST enthält Folgendes:


```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id={your_app_client_id}&amp;grant_type=client_credentials&amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion={encoded_signed_JWT_token}
```

#### <a name="sample-request"></a>Beispielanfrage

```json
POST https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 994

resource=https%3A%2F%2Fmanage.office.com&amp;client_id= a6099727-6b7b-482c-b509-1df309acc563&amp;grant_type=client_credentials &amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Ill5ZnNoSkMzclBRLWtwR281ZFVhaVk1dDNpVSJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ud2luZG93cy5uZXRcLzQxNDYzZjUzLTg4MTItNDBmNC04OTBmLTg2NWJmNmUzNTE5MFwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQyNzI0ODY0OCwiaXNzIjoiYTYwOTk3MjctNmI3Yi00ODJjLWI1MDktMWRmMzA5YWNjNTYzIiwianRpIjoiMGNlMjU0YzQtODFiMS00YTJlLTg0MzYtOWE4YzNiNDlkZmI5IiwibmJmIjoxNDI3MjQ4MDQ4LCJzdWIiOiJhNjA5OTcyNy02YjdiLTQ4MmMtYjUwOS0xZGYzMDlhY2M1NjMifQ.vfDrmCjiXgoj2JrTkwyOpr-NOeQTzlXQcGlKGNpLLe0oh4Zvjdcim5C7E0UbI3Z2yb9uKQdx9G7GeqS-gVc9kNV_XSSNP4wEQj3iYNKpf_JD2ikUVIWBkOg41BiTuknRJAYOMjiuBE2a6Wyk-vPCs_JMd7Sr-N3LiNZ-TjluuVzWHfok_HWz_wH8AzdoMF3S0HtrjNd9Ld5eI7MVMt4OTpRfh-Syofi7Ow0HN07nKT5FYeC_ThBpGiIoODnMQQtDA2tM7D3D6OlLQRgLfI8ir73PVXWL7V7Zj2RcOiooIeXx38dvuSwYreJYtdphmrDBZ2ehqtduzUZhaHL1iDvLlw
```

Die Antwort wird die gleiche sein wie zuvor, aber das Token wird nicht dieselben Eigenschaften haben, da es keine Eigenschaften des Administrators enthält, der die Zustimmung erteilt hat. 

#### <a name="sample-response"></a>Beispielantwort

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 1276

{"token_type":"Bearer","expires_in":"3599","expires_on":"1431659094","not_before":"1431655194","resource":"https://manage.office.com","access_token":"eyJ0eXAiOiJKV1QiL..."}
```

#### <a name="sample-access-token"></a>Beispiel für Zugriffstoken

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


## <a name="build-your-app"></a>Erstellen Sie Ihre Anwendung

Nachdem Sie die Anwendung in Azure AD registriert und die erforderlichen Berechtigungen konfiguriert haben, können Sie Ihre Anwendung erstellt. Folgend finden Sie einige der wichtigsten Aspekte, die beim Entwerfen und Erstellen Ihrer App zu berücksichtigen sind:

- **Die Zustimmungsfunktionalität**. Um die Zustimmung Ihrer Kunden zu erhalten, müssen Sie diese in einem Browser zur Azure AD-Webseite weiterleiten, indem Sie die speziell erstellte URL verwenden, die vorher hier beschrieben wurde. Sie müssen zudem über eine Webseite verfügen, zu der Azure AD den Administrator weiterleitet, wenn dieser seine Zustimmung erteilt hat. Diese Webseite muss den Autorisierungscode aus der URL extrahieren und diesen verwenden, um ein Zugriffstoken anzufordern, von dem sie die Mandanten-ID erält.
    
- **Speichern der Mandanten-ID in Ihrem System**. Diese wird beim Anfordern des Zugriffstoken von Azure AD und beim Aufrufen der Office-Management-APIs benötigt.
    
- **Verwaltung von Zugriffstoken**. Sie werden eine Komponente benötigen, die Zugriffstoken bei Bedarf anfordert und verwaltet. Wenn Ihre App die APIs regelmäßig aufruft, kann sie Token bei Bedarf anfordern, oder wenn sie die APIs kontinuierlich aufruft, um Daten abzurufen, kann sie Token in regelmäßigen Abständen anfordern (z. B. alle 45 Minuten).
    
- **Implementieren eines Webhook-Listener** je nach Bedarf der jeweiligen-API, die Sie verwenden.
    
- **Datenabruf und Speicherung**. Sie werden eine Komponente benötigen, die Daten für jeden Mandanten abruft, entweder durch kontinuierliches Abrufen oder als Reaktion auf Webhook-Benachrichtigungen, abhängig von der jeweiligen API, die Sie verwenden.
    
