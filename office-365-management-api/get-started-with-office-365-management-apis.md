---
ms.TocTitle: Get started with Office 365 Management APIs
title: Erste Schritte mit den Office 365-Verwaltungs-APIs
description: Die APIs verwenden Azure AD, um Authentifizierungsdienste bereitzustellen, mit denen Sie der Anwendung entsprechende Rechte für den Zugriff auf diese Dienste erteilen können.
ms.ContentId: 74137c9a-29e0-b588-6122-26f4d2c5e3fc
ms.topic: reference (API)
ms.date: 09/05/2018
localization_priority: Priority
ms.openlocfilehash: 9732b5a838bdf4c14a6a13af8196704c89dec63d
ms.sourcegitcommit: 5b1eaeb7f262b7b9f7ab30ccb9f10878814153ac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "32224041"
---
# <a name="get-started-with-office-365-management-apis"></a>Erste Schritte mit den Office 365-Verwaltungs-APIs

Wenn Sie eine Anwendung erstellen, die Zugriff auf gesicherte Dienste wie die Office 365-Management-APIs benötigt, müssen Sie dem Dienst mitteilen, dass Ihre Anwendung Zugriffsrechte hat. Die Office 365-Management-APIs verwenden Azure AD, um Authentifizierungsdienste bereitzustellen, mit denen Sie der Anwendung entsprechende Rechte für den Zugriff auf diese Dienste erteilen können. 

Es gibt vier zentrale Schritte:

1. **Registrieren Sie Ihre Anwendung in Azure AD**. Um Ihrer Anwendung den Zugriff auf die Office 365-Management-APIs zu ermöglichen, müssen Sie Ihre Anwendung bei Azure AD registrieren. Dadurch können Sie eine Identität für Ihre Anwendung einrichten und geben die Berechtigungsstufen angeben, die sie für den Zugriff auf die APIs benötigt.
    
2. **Erhalten Sie die Genehmigung durch einen Office 365-Mandanten-Admin**. Ein Office 365-Mandanten-Admin muss eine Genehmigung erteilen, damit Ihre Anwendung auf mittels Office 365-Management-APIs auf Mandantendaten zugreifen kann. Der Genehmigungsprozess ist eine browserbasierte Praxis, bei der sich der Mandantenadministrator in der **Azure AD Genehmigung-Benutzeroberfläche** anmelden und die von Ihrer Anwendung angeforderten Berechtigungen überprüfen muss und diese Anfrage gewährt oder verweigert. Nachdem die Genehmigung erteilt wurde, leitet die Benutzeroberfläche den Benutzer über einen Authentifizierungscode in der URL zurück zu Ihrer Anwendung. Ihre Anwendung führt einen Dienst-zu-Dienst-Anruf zu Azure AD durch, um diesen Autorisierungscode in ein Zugriffs-Token umzuwandeln, das Informationen über den Mandantenadministrator und Ihre Anwendung enthält. Die Mandanten-ID muss aus dem Zugriffstoken entnommen werden und für die zukünftige Nutzung aufbewahrt werden.
    
3. **Fordern Sie ein Zugriffstoken von Azure AD an**. Mit den in Azure Active Directory konfigurierten Anmeldeinformationen Ihrer Anwendung fordert Ihre Anwendung fortlaufend zusätzliche Zugriffstoken für einen genehmigten Mandanten an, ohne dass eine weitere Interaktion mit einem Mandantenadministrator benötigt wird. Diese Zugriffstoken werden als „nur App“-Token bezeichnet, da sie keine Informationen zum Mandantenadministrator beinhalten.
    
4. **Rufen Sie die Office 365-Management-APIs auf**. Die „nur App“-Zugriffstoken werden an die Office 365-Management-APIs übergeben, um Ihre Anwendung zu authentifizieren und zu autorisieren.
    
Das folgende Diagramm zeigt die Abfolge von Genehmigungs- und Zugriffstoken-Anfragen.


![Initialer Authorisierungsvorgang für Verwaltungs-APIs](images/authorization-flow.png)


## <a name="register-your-application-in-azure-ad"></a>Registrieren Sie Ihre Anwendung in Azure AD.

Die Office 365-Management-APIs verwenden Azure AD zur sicheren Authentifizierung der Office 365-Mandantendaten. Für den Zugriff auf die Office 365-Management-APIs müssen Sie die Anwendung in Azure Active Directory registrieren, und als Teil der Konfiguration die Berechtigungsstufen, die Ihre Anwendung für den Zugriff auf die APIs benötigt, angeben.


### <a name="prerequisites"></a>Voraussetzungen

Wenn Sie die Anwendung in Azure AD registriert haben, benötigen Sie ein Abonnement für Office 365 und ein Abonnement für Azure, das mit Ihrem Office 365-Abonnement verknüpft ist. Für den Anfang können Sie Testabonnements sowohl für Office 365 als auch für Azure verwenden. Weitere Informationen finden Sie unter [Willkommen beim Office 365-Entwicklerprogramm](https://docs.microsoft.com/de-DE/office/developer-program/office-365-developer-program).


### <a name="use-the-azure-management-portal-to-register-your-application-in-azure-ad"></a>Nutzen Sie das Azure-Verwaltungsportal, um Ihre Anwendung in Azure AD zu registrieren.

Nachdem Sie einen Microsoft-Mandanten mit den entsprechenden Abonnements haben, können Sie Ihre Anwendung in Azure AD registrieren.

1. Melden Sie sich im [Azure-Verwaltungsportal](https://manage.windowsazure.com/) an, und verwenden Sie dabei die Anmeldeinformationen Ihres Microsoft-Mandanten, der über das Office 365-Abonnement verfügt, das Sie verwenden möchten. Sie können auf das Azure-Verwaltungsportal auch über einen Link zugreifen, der im linken Navigationsbereich im [Office Admin-Portal](https://portal.office.com/) erscheint.
    
2. Klicken Sie im linken Navigationsbereich auf Active Directory (1). Stellen Sie sicher, dass die Registerkarte Verzeichnis (2) ausgewählt ist, und klicken Sie dann auf den Verzeichnisnamen (3).
    
   ![Anmeldeseite für Office 365](images/o365-sign-up-page.png)
    
    
3. Wählen Sie auf der Verzeichnisseite **Anwendungen**. Azure AD zeigt eine Liste der Anwendungen, die aktuell in Ihrem Mandanten installiert sind.
    
4. Wählen Sie **Hinzufügen** aus.
    
   ![Verwaltungsseite für Office 365](images/o365-admin-page.png)
    
    
5. Wählen Sie **Add an application my organization is developing** aus.
    
6. Geben Sie den **Namen** Ihrer Anwendung ein, und geben Sie für den **Typ** WEB-ANWENDUNG UND/ODER WEB-API an.
    
7. Geben Sie die entsprechenden Eigenschaften der App ein:
    
   - **Anmelde-URL**. Die URL, mit der Benutzer sich anmelden und Ihre Anwendung verwenden können. Sie können dies später bei Bedarf ändern.
    
   - **App-ID-URI**. Der URI, der als ein eindeutiger logischer Identifikator verwendet wird. Der URI muss sich in einer überprüften benutzerdefinierten Domäne für einen externen Benutzer befinden, um Ihrer Anwendung Zugriff auf seine Daten in Windows Azure Active Directory zu gewähren. Wenn Ihr Microsoft-Mandant z. B. **contoso.onmicrosoft.com** ist, könnte die APP-ID URI **https://app.contoso.onmicrosoft.com** sein.
    
8. Die app ist jetzt mitIhre Anwendung ist jetzt für Azure AD registriert und wurde einer Client-ID zugewieden. Es gibt jedoch weitere wichtige Aspekte Ihrer Anwendung, die konfiguriert werden müssen.
    

### <a name="configure-your-application-properties-in-azure-ad"></a>Konfigurieren Sie Ihre Anwendungseigenschaften in Azure AD

Nachdem Ihre Anwendung registriert ist, gibt es mehrere wichtige Eigenschaften, die Sie angeben müssen, die bestimmen, wie Ihre Anwendung in Azure AD funktioniert und wie Mandantenadministratoren Ihrer Anwendung die Genehmigung für den Zugriff auf ihre Daten mittels den Office 365-Management-APIs erteilen.

Weitere Informationen zur Anwensungskonfiguration in Azure AD im Allgemeinen finden Sie unter [Anwendungs-Objekteigenschaften](https://docs.microsoft.com/de-DE/azure/active-directory/develop/active-directory-application-objects).


1. **CLIENT-ID**. Dieser Wert wird von Azure AD automatisch generiert. Ihre Anwendung wird diesen Wert beim Anfordern von Genehmigungen von Mandantenadministratoren und beim Anfordern von „Nur App“-Token aus Azure AD verwenden.
    
2. **ANWENDUNG HAT MEHRERE MANDANTEN**. Für diese Eigenschaft muss **Ja** ausgewählt werden, damit Mandantenadministratoren Ihrer Anwendung die Genehmigung erteilen können, mit den Office 365-Management-APIs auf ihre Daten zuzugreifen. Wenn für diese Eigenschaft **Nein** ausgewählt ist, kann Ihre Anwendung ausschließlich auf Daten Ihres eigenen Mandanten zugreifen.
    
3. **ANTWORT-URL**. Dies ist die URL, zu der ein Mandantenadministrator weitergeleitet wird, nachdem er Ihrer Anwendung die Genehmigung für den Zugriff auf seine Daten mittels den Office 365 Management-APIs erteilt hat. Sie können bei Bedarf mehrere Antwort-URLs konfigurieren. Azure legt automatisch die erste so fest, dass sie mit der Anmelde-URL übereinstimmt, die Sie beim Erstellen der Anwendung angegeben haben, aber Sie können diesen Wert wenn nötig ändern.
    
Wählen Sie unbedingt **Speichern**, nachdem Sie Änderungen an dieser Eigenschaften vorgenommen haben.


### <a name="generate-a-new-key-for-your-application"></a>Erstellen Sie einen neuen Schlüssel für Ihre Anwendung

Schlüssel werden auch als geheime Clientschlüssel bezeichnet und werden verwendet, ein Autorisierungscode gegen eine Zugriffstoken ausgetauscht wird.


1. Wählen Sie im Azure Verwaltungsportal Ihre Anwendung und wählen Sie **konfigurieren** im oberen Menü. Blättern Sie nach unten zu **Schlüssel**.
    
2. Wählen Sie die Gültigkeitsdauer Ihres Schlüssels, und wählen Sie **Speichern**.
    
   ![Azure-Seite "Abonnieren"](images/azure-subscription-page.png)
    
    
3. Azure zeigt den App-Schlüssel nur nach dem Speichern an. Klicken Sie auf das Symbol Zwischenablage, um das Client-Geheimnis in die Zwischenablage zu kopieren.
    
   ![Azure-Seite "Portal"](images/azure-portal-page.png)

   > [!IMPORTANT] 
   > Azure zeigt das Client-Geheimnis nur zum Zeitpunkt der ersten Generierung an. Sie können nicht zu dieser Seite zurücknavigieren und den geheimen Clientschlüssel später abrufen.

### <a name="configure-an-x509-certificate-to-enable-service-to-service-calls"></a>Konfigurieren eines x. 509-Zertifikats, um Dienst-zu-Dienst-Aufrufe zu ermöglichen

Eine Anwendung, die im Hintergrund ausgeführt wird, wie ein Dämonprozess oder ein Dienst, kann Client-Anmeldeinformationen nutzen, um ein „Nur App“-Zugriffstoken anzufordern, ohne fortlaufend eine Genehmigung vom Mandantenadministrator anzufordern, nachdem eine erste Genehmigung erteilt wurde. 

Weitere Informationen finden Sie unter [Dienst-zu-Dienst-Anrufe mithilfe von Client-Anmeldeinformationen](https://msdn.microsoft.com/de-DE/library/azure/dn645543.aspx).

Sie müssen ein X.509-Zertifikat für Ihre Anwendung erstellen, das als Client-Anmeldedaten dient, wenn ein „Nur App“-Token von Azure AD angefordert wird. Dieser Prozess besteht aus zwei Schritten:

- Abrufen eines X.509-Zertifikats. Sie können ein selbstsigniertes Zertifikat oder ein von einer öffentlichen, vertrauenswürdigen Zertifizierungsstelle ausgestelltes Zertifikat verwenden..
    
- Ändern Sie Ihr Anwendungsmanifest, um den Fingerabdruck und den öffentlichen Schlüssel Ihres Zertifikats einzuschließen.
    
Die folgenden Anweisungen zeigen Ihnen, wie Sie das Visual Studio oder das Windows SDK _Makecert_tool verwenden, um ein selbstsigniertes Zertifikat zu erstellen und den öffentlichen Schlüssel in eine base64-codierte Datei zu exportieren.


1. Führen Sie in der Befehlszeile Folgendes aus:
    
   ```
    makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 03/15/2015 -e 03/15/2017 -ss my -len 2048
   ```

   > [!NOTE] 
   > Wenn Sie das x. 509-Zertifikat generieren, stellen Sie sicher, dass die Länge des Schlüssels mindestens 2048 beträgt. Kürzere Schlüssellängen werden nicht als gültige Schlüssel akzeptiert.

2. Öffnen Sie die Snap-In MMC-Zertifikate und verbinden Sie sich mit Ihrem Benutzerkonto. 
    
3. Suchen Sie das neue Zertifikat im Persönlichen Ordner und exportieren Sie den öffentlichen Schlüssel in eine base64-codierte Datei (z. B. mycompanyname.cer). Ihre Anwendung verwendet dieses Zertifikat zum Kommunizieren mit Azure AD. Stellen Sie daher sicher, dass Sie auch Zugriff auf den privat Schlüssel erhalten.
    
   > [!NOTE] 
   > Sie können Windows PowerShell verwenden, um den Fingerabdruck und den base64-codierten öffentlichen Schlüssel zu extrahieren. Andere Plattformen bieten ähnliche Tools zum Abrufen der Eigenschaften von Zertifikaten.

4. Geben Sie in der Windows PowerShell-Eingabeaufforderung Folgendes ein und führen Sie es aus:
    
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
    
6. Wählen Sie im Azure Verwaltungsportal Ihre Anwendung und wählen Sie **konfigurieren** im oberen Menü.
    
7. Wählen Sie in der Befehlsleiste **Manifest verwalten **, und wählen Sie dann **Manifest herunterladen**.
    
   ![Anzeige des Kommandozeilenzertifikats](images/command-line-certificate-display.png)
    
    
8. Öffnen Sie das heruntergeladene Manifest zur Bearbeitung und ersetzen Sie die leere KeyCredentials -Eigenschaft durch die folgende JSON:
    
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

9. Speichern Sie Ihre Änderungen und laden Sie die aktualisierte App-Manifestdatei hoch, indem Sie auf **Manifest verwalten** in der Befehlsleiste klicken, **Manifest hochladen**wählen, zu Ihrer aktualisierten Manifestdatei navigieren und diese dann auswählen.
    

### <a name="specify-the-permissions-your-app-requires-to-access-the-office-365-management-apis"></a>Geben Sie die Berechtigungen, die Ihre Anwnedung benötigt, um auf die Office 365-Management-APIs zuzugreifen, an.

Schließlich müssen Sie genau angeben, welche Berechtigungen Ihre Anwendung für die Office 365 Management-APIs benötigt. Zu diesem Zweck müssen Sie einen Zugriff auf die Office 365-Management-APIs zu Ihrer Anwendung hinzufügen und dann die Berechtigung(en) auswählen, die Sie benötigen.


1. Wählen Sie im Azure Verwaltungsportal Ihre Anwendung und wählen Sie **konfigurieren** im oberen Menü. Scrollen Sie nach unten zu **Berechtigungen für andere Anwendungen** und wählen Sie **Anwendung hinzufügen** aus.
    
   ![Azure AD-Seite](images/azure-ad-page.png)
    
    
2. Wählen Sie die **Office 365-Management-APIs** (1) so, dass sie in der **ausgewählter** Spalte (2) angezeigt werden, und wählen Sie dann das Häkchen unteren rechts (3), um Ihre Auswahl zu speichern und zurück zu Haupt-Konfigurationsseite Ihrer Anwendung zu gelangen.
    
   ![Azure AD-Seite "Apps"](images/azure-ad-apps-page.png)
    
    
3. Die Office-Management-APIs werden jetzt in der Liste der Anwendungen angezeigt, für die Ihre Anwendung Berechtigungen benötigt. Wählen Sie sowohl unter **Anwendungsberechtigungen** als auch unter **delegierte Berechtigungen** die Berechtigungen aus, die Ihre Anwendung benötigt. Weitere Informationen zu den einzelnen Berechtigungen finden Sie unter den jeweiligen API-Referenzen.  

   > [!NOTE] 
   > Vier Berechtigungen für Aktivitätsberichte und Informationen zu Bedrohungen werden derzeit nicht verwendet und werden zukünftig entfernt. Aktivieren Sie keine der folgenden Berechtigungen, da sie nicht erforderlich sind.
    
   ![Dialogfeld "Eine Anwendung hinzufügen"](images/add-an-application-dialog.png)
    
    
4. Klicken Sie auf **Speichern**, um die Konfiguration zu speichern.
    

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


![Azure AD-Seite "App hinzugefügt"](images/azure-ad-app-added-page.png)

Nachdem Sie **Annehmen** ausgewählt haben, werden Sie zu der angegebenen Seite weitergeleitet und die Abfrage-Zeichenfolge wird einen Code enthalten. 

Beispiel:

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

Ihre Anwendung verwendet diesen Autorisierungscode, um ein Zugriffstoken von Azure AD zu erhalten, aus dem die Mandanten-ID extrahiert werden kann. Nachdem Sie die Mandanten-ID extrahiert und gespeichert haben, können Sie nachfolgende Zugriffstoken beziehen, ohne dass eine Anmeldung als Mandantenadministrator notwendig ist.


## <a name="request-access-tokens-from-azure-ad"></a>Fordern Sie ein Zugriffstoken von Azure AD an.

Es gibt zwei Methoden, um Zugriffstoken von Azure AD anzufordern:

- Der [Genehmigungsprozess mit Autorisierungscode](https://msdn.microsoft.com/en-us/library/azure/dn645542.aspx) beinhaltet, dass eine Mandantenadministrator seine ausdrückliche Genehmigung erteilt, wodurch ein Autorisierungscode an Ihre Anwendung zurückgegeben wird. Ihre Anwendung tauscht dann den Autorisierungscode gegen ein Zugriffstoken aus. Diese Methode ist erforderlich, um die erste Zustimmung dafür zu erhalten, die Ihre Anwendung benötigt, um mittels der API auf Mandantendaten zuzugreifen. Dieses erste Zugriffstoken ist erforderlich, um die Mandanten-ID zu erhalten und zu speichern.
    
- Die [Genehmigungsprozess mit Client-Anmeldedaten](https://msdn.microsoft.com/de-DE/library/azure/dn645543.aspx) ermöglicht es Ihrer Anwendung, nachfolgende Zugriffstoken anzufordern, wenn alte ihre Gültigkeit verlieren, ohne dass der Mandantenadministrator sich anmelden und seine ausdrückliche Zustimmung erteilen muss. Diese Methode muss für Anwendungen verwendet werden, die fortlaufend im Hintergrund ausgeführt werden, und APIs aufrufen, nachdem die erste Zustimmung durch den Mandantenadministrator erteilt wurde.
    

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

Wenn Sie die Anwendung in .NET entwickeln, können Sie mithilfe der [Azure Active Directory Authentication Library (ADAL)](https://docs.microsoft.com/de-DE/azure/active-directory/develop/active-directory-authentication-libraries) Client Assertions erstellen. Andere Entwicklungsplattformen sollten ähnliche Bibliotheken haben.

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
    
- **Speichern Sie die Mandanten-ID in Ihrem System**. Diese wird beim Anfordern des Zugriffstoken von Azure AD und beim Aufrufen der Office-Management-APIs benötigt.
    
- **Verwalten von Zugriffstoken**. Sie benötigen eine Komponente, die nach Bedarf Zugriffstoken anfordert und verwaltet. Wenn Ihre App in regelmäßigen Abständen die APIs aufruft, kann sie Token nach Bedarf anfordern. Wenn sie die APIs ständig zum Abrufen von Daten aufruft, kann sie Token in regelmäßigen Abständen (z. B. alle 45 Minuten) anfordern.
    
- **Implementieren eines Webhook-Listener** je nach Bedarf der jeweiligen-API, die Sie verwenden.
    
- **Abrufen und Speichern von Daten**. Sie benötigen eine Komponente, die Daten für jeden Mandanten, abruft, entweder kontinuierlich oder als Reaktion auf Webhook-Benachrichtigungen, je nach der bestimmten-API, die Sie verwenden.
    
