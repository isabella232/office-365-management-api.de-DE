---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Management Activity API schema
title: Office 365-Verwaltungsaktivitäts-API-Schema
description: Das Office 365-Verwaltungsaktivitäts-API-Schema wird als Datendienst auf zwei Ebenen bereitgestellt – einem allgemeinen Schema und einem dienstspezifischem Schema.
ms.ContentId: 1c2bf08c-4f3b-26c0-e1b2-90b190f641f5
ms.topic: reference (API)
ms.date: ''
ms.localizationpriority: high
ms.openlocfilehash: 57c9fb5adcb92d2fd04c6377b7f9a320bbcc8a83
ms.sourcegitcommit: 13b50617b1a73f5890414087d8eabe6b2240cfb4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2021
ms.locfileid: "58510160"
---
# <a name="office-365-management-activity-api-schema"></a>Office 365-Verwaltungsaktivitäts-API-Schema

Das Office 365-Verwaltungsaktivitäts-API-Schema wird als Datendienst auf zwei Ebenen bereitgestellt:

- **Allgemeines Schema**. Die Schnittstelle für den Zugriff auf wichtige Office 365-Überwachungskonzepte wie z. B. Datensatztyp, Zeitpunkt der Erstellung, Benutzertyp und Aktion sowie für die Bereitstellung wichtiger Dimensionen (z. B. Benutzer-ID), Speicherortspezifikationen (z. B. Client-IP-Adresse) und dienstspezifischer Eigenschaften (z. B. Objekt-ID). Es werden konsistente und einheitliche Ansichten für Benutzer eingerichtet, um alle Office 365-Überwachungsdaten in wenigen Ansichten auf oberster Ebene mit den entsprechenden Parametern zu extrahieren, und es entsteht ein festes Schema für alle Datenquellen, was die Kosten des Lernens erheblich reduziert. Das allgemeine Schema wird aus den Produktdaten jedes Produktteams abgeleitet, z. B. Exchange, SharePoint, Azure Active Directory, Yammer und OneDrive for Business. Das Feld "Objekt-ID" kann von Microsoft 365-Produktteams um dienstspezifische Eigenschaften erweitert werden.

- **Dienstspezifisches Schema**. Baut auf das allgemeine Schema auf, um eine Reihe von Microsoft 365-dienstspezifischen Attributen bereitzustellen; z. B. SharePoint-Schema, OneDrive for Business-Schema und Exchange-Administrator-Schema.

## <a name="office-365-management-api-schemas"></a>Office 365-Verwaltungs-API-Schemas

Dieser Artikel enthält Details zum allgemeinen Schema sowie zu dienstspezifischen Schemas. In der folgenden Tabelle werden die verfügbaren Schemas beschrieben.

|Name des Schemas|Beschreibung|
|:-----|:-----|
|[Allgemeines Schema](#common-schema)|Die Ansicht, um den Datensatztyp, die Benutzer-ID, die Client-IP, den Benutzertyp und die Aktion zusammen mit grundlegenden Dimensionen wie Benutzereigenschaften (z. B. Benutzer-ID), Speichereigenschaften (z. B. Client-IP) und dienstspezifischen Eigenschaften (z. B. Objekt-ID) zu extrahieren.|
|[SharePoint-Basisschema](#sharepoint-base-schema)|Das allgemeine Schema wird mit den Eigenschaften für alle SharePoint-Überwachungsdaten erweitert.|
|[SharePoint-Dateivorgänge](#sharepoint-file-operations)|Das SharePoint-Basisschema wird mit den Eigenschaften für den Dateizugriff und die Dateibearbeitung in SharePoint erweitert.|
|[SharePoint-Freigabeschema](#sharepoint-sharing-schema)|Das SharePoint-Basisschema wird mit den Eigenschaften für die Dateifreigabe erweitert.|
|[SharePoint-Schema](#sharepoint-schema)|Das SharePoint-Basisschema wird mit den für SharePoint spezifischen Eigenschaften erweitert, allerdings nicht in Bezug auf Dateizugriff und -bearbeitung.|
|[Projektschema](#project-schema)|Das SharePoint-Basisschema wird mit den projektspezifischen Eigenschaften erweitert.|
|[Exchange-Verwaltungsschema](#exchange-admin-schema)|Das allgemeine Schema wird mit den für alle Exchange-Verwaltungsüberwachungsdaten spezifischen Eigenschaften erweitert.|
|[Exchange-Postfachschema](#exchange-mailbox-schema)|Das allgemeine Schema wird mit den für alle Exchange-Postfachüberwachungsdaten spezifischen Eigenschaften erweitert.|
|[Azure Active Directory-Basisschema](#azure-active-directory-base-schema)|Das allgemeine Schema wird mit den für alle Azure Active Directory-Überwachungsdaten spezifischen Eigenschaften erweitert.|
|[Azure Active Directory-Kontoanmeldeschema](#azure-active-directory-account-logon-schema)|Das Azure Active Directory-Basisschema wird mit den für alle Azure Active Directory-Anmeldeereignisse spezifischen Eigenschaften erweitert.|
|[Azure Active Directory-STS-Anmeldeschema](#azure-active-directory-secure-token-service-sts-logon-schema)|Das Azure Active Directory-Basisschema wird mit den für alle Azure Active Directory-Secure Token Service (STS)-Anmeldeereignisse spezifischen Eigenschaften erweitert.|
|[Azure Active Directory-Schema](#azure-active-directory-schema)|Das allgemeine Schema wird mit den für alle Azure Active Directory-Überwachungsdaten spezifischen Eigenschaften erweitert.|
|[DLP-Schema](#dlp-schema)|Das allgemeine Schema wird mit den für Verhinderung von Datenverlust-Ereignisse spezifischen Eigenschaften erweitert.|
|[Security & Compliance Center-Schema](#security-and-compliance-center-schema)|Das allgemeine Schema wird mit den für alle Security and Compliance Center-Ereignisse spezifischen Eigenschaften erweitert.|
|[Security &Compliance-Warnung-Schema](#security-and-compliance-alerts-schema)|Das alle Schema wird mit den für alle Office 365-Security & Compliance-Warnungen spezifischen Eigenschaften erweitert.|
|[Yammer-Schema](#yammer-schema)|Das allgemeine Schema wird mit den für alle Yammer-Ereignisse spezifischen Eigenschaften erweitert.|
|[Rechenzentrum-Sicherheitsbasis-Schema](#data-center-security-base-schema)|Erweitert das allgemeine Schema mit den für alle Rechenzentrum-Sicherheitsüberwachungsdaten spezifischen Eigenschaften.|
|[Rechenzentrum-Sicherheits-Cmdlet-Schema](#data-center-security-cmdlet-schema)|Das Datenzentrum-Sicherheitsbasis-Schema wird mit den für alle Rechenzentrum-Sicherheits-Cmdlet-Überwachungsdaten spezifischen Eigenschaften erweitert.|
|[Microsoft Teams-Schema](#microsoft-teams-schema)|Das allgemeine Schema wird mit den für alle Microsoft Teams-Ereignisse spezifischen Eigenschaften erweitert.|
|[Microsoft Defender für Office 365 und Threat Investigation and Response-Schema](#microsoft-defender-for-office-365-and-threat-investigation-and-response-schema)|Das allgemeine Schema wird mit den für Defender für Office 365 spezifischen Eigenschaften und Daten von Threat Investigation and Response erweitert.|
|[Übermittlungsschema](#submission-schema)|Das allgemeine Schema wird mit den für Benutzer- und Administratorübermittlungen in Microsoft Defender für Office 365 spezifischen Eigenschaften erweitert.|
|[Schema "Automatisierte Untersuchungs- und Reaktionsereignisse"](#automated-investigation-and-response-events-in-office-365)|Das allgemeine Schema wird um die für ‚Automatisierte Untersuchungs- und Reaktionsereignisse‘ (AIR, Automated investigation and response) in Office 365 spezifischen Eigenschaften erweitert. Ein Beispiel dazu finden Sie im [Tech Community-Blog: Improve the Effectiveness of your SOC with Microsoft Defender for Office 365 and the O365 Management API](https://techcommunity.microsoft.com/t5/microsoft-security-and/improve-the-effectiveness-of-your-soc-with-office-365-atp-and/ba-p/1525185) (Verbessern der Effektivität Ihres SOC mit Microsoft Defender für Office 365 und der O365 Management-API).|
|[Nachrichtenschutzereignis-Schema](#hygiene-events-schema)|Das allgemeine Schema wird mit den für Ereignisse in Exchange Online Protection und Microsoft Defender für Office 365 spezifischen Eigenschaften erweitert.|
|[Power BI-Schema](#power-bi-schema)|Erweitert das allgemeine Schema um die für alle Power BI-Ereignisse spezifischen Eigenschaften.|
|[Dynamics 365-Schema](#dynamics-365-schema)|Das allgemeine Schema wird mit den für Dynamics 365-Ereignisse spezifischen Eigenschaften erweitert.|
|[Workplace Analytics-Schema](#workplace-analytics-schema)|Das allgemeine Schema wird mit den für alle Microsoft Workplace Analytics-Ereignisse spezifischen Eigenschaften erweitert.|
|[Quarantäne-Schema](#quarantine-schema)|Erweitert das allgemeine Schema um die für alle Quarantäne-Ereignisse spezifischen Eigenschaften.|
|[Microsoft Forms-Schema](#microsoft-forms-schema)|Das allgemeine Schema wird mit den für alle Microsoft Forms-Ereignisse spezifischen Eigenschaften erweitert.|
|[MIP-Bezeichnungsschema](#mip-label-schema)|Erweitert das allgemeine Schema um die für Vertraulichkeitsbezeichnungen spezifischen Eigenschaften, die manuell oder automatisch auf E-Mail-Nachrichten angewendet werden.|
|[Exchange-Schema der Kommunikationscompliance](#communication-compliance-exchange-schema)|Erweitert das allgemeine Schema um die Eigenschaften, die speziell für das Kommunikationscompliance-Modell anstößiger Sprache gelten.|
|||

## <a name="common-schema"></a>Allgemeines Schema

**EntityType Name**: AuditRecord

|Parameter|Typ|Erforderlich?|Beschreibung|
|:-----|:-----|:-----|:-----|
|Id|Kombination aus GUIDEdm.Guid|Ja|Der eindeutige Bezeichner eines Überwachungsdatensatzes.|
|RecordType|Self.[AuditLogRecordType](#auditlogrecordtype)|Ja|Der vom Datensatz angegebene Vorgangstyp. In der Tabelle [AuditLogRecordType](#auditlogrecordtype) finden Sie weitere Informationen zu den Typen von Überwachungsprotokolldatensätzen.|
|CreationTime|Edm.Date|Ja|Das Datum und die Uhrzeit in koordinierter Weltzeit (UTC), wann der Benutzer die Aktivität ausgeführt hat.|
|Vorgang|Edm.String|Ja|Der Name der Benutzer- oder Verwaltungsaktivität. Eine Beschreibung der am häufigsten verwendeten Vorgänge und Aktivitäten, finden Sie unter [Durchsuchen des Überwachungsprotokolls im Office 365-Schutzcenter](https://go.microsoft.com/fwlink/p/?LinkId=708432). Für Exchange-Administratoraktivitäten gibt diese Eigenschaft den Namen des Cmdlets an, das ausgeführt wurde. Für Dlp-Ereignisse kann dies "DlpRuleMatch", "DlpRuleUndo" oder "DlpInfo" sein. Eine Beschreibung finden Sie unten unter "DLP-Schema".|
|OrganizationId|Edm.Guid|Ja|Die GUID für den Office 365-Mandanten Ihrer Organisation. Dieser Wert ist für Ihre Organisation, unabhängig vom Office 365-Dienst, in dem er verwendet wird, immer gleich.|
|UserType|Self.[UserType](#user-type)|Ja|Der Typ des Benutzers, der den Vorgang ausgeführt hat. In der Tabelle [UserType](#user-type) finden Sie Informationen zu den Typen von Benutzern.|
|UserKey|Edm.String|Ja|Eine alternative ID für den in der UserId-Eigenschaft identifizierten Benutzer. Diese Eigenschaft wird z. B. mit der Passport Unique ID (PUID) bei Ereignissen ausgefüllt, die von Benutzern in SharePoint, OneDrive for Business und Exchange ausgeführt werden. Diese Eigenschaft kann den gleichen Wert spezifizieren wie die Eigenschaft "UserID" für Ereignisse, die in anderen Diensten auftreten, und Ereignisse, die von Systemkonten durchgeführt werden.|
|Arbeitslast|Edm.String|Nein|Der Office 365-Dienst, in dem die Aktivität stattgefunden hat. 
|ResultStatus|Edm.String|Nein|Gibt an, ob die Aktion (in der Eigenschaft "Operation" angegeben) erfolgreich war oder nicht. Mögliche Werte sind **Succeeded**, **PartiallySucceeded** oder **Failed**. Für Exchange-Verwaltungsaktivitäten ist der Wert entweder **True** oder **False**.<br/><br/>**Wichtig**: Unterschiedliche Workloads können den Wert der ResultStatus-Eigenschaft außer Kraft setzen. Beispielsweise zeigt ein Wert **Succeeded** für "ResultStatus" bei Azure Active Directory STS-Anmeldeereignissen nur an, dass die HTTP-Operation erfolgreich war; er bedeutet nicht, dass die Anmeldung erfolgreich war. Um festzustellen, ob die eigentliche Anmeldung erfolgreich war oder nicht, ziehen Sie die LogonError-Eigenschaft im [Azure Active Directory-STS-Anmeldeschema](#azure-active-directory-secure-token-service-sts-logon-schema) zurate. Wenn die Anmeldung fehlgeschlagen ist, enthält diese Eigenschaft den Grund für den fehlgeschlagenen Anmeldeversuch. |
|ObjectId|Edm.string|Nein|Für SharePoint- und OneDrive for Business-Aktivitäten der vollständige Pfadname der Datei oder des Ordners, auf die bzw. den der Benutzer zugegriffen hat. Für Exchange-Verwaltungsüberwachungsprotokolle der Name des Objekts, das vom Cmdlet geändert wurde.|
|UserId|Edm.string|Ja|Der UPN (User Principal Name) des Benutzers, der die Aktion (in der Eigenschaft "Operation" angegeben), die zu einem Eintrag geführt hat, ausgeführt hat, zum Beispiel `my_name@my_domain_name`. Beachten Sie, dass auch von Systemkonten ausgeführte Datensätze (wie SHAREPOINT\system oder NT AUTHORITY\SYSTEM) enthalten sind. In SharePoint ist eine weitere Wertanzeige in der UserId-Eigenschaft "app@sharepoint". Dies zeigt an, dass es sich bei dem "Benutzer", der die Aktivität ausgeführt hat, um eine Anwendung handelt, die in SharePoint über die erforderlichen Berechtigungen verfügt, organisationsweite Aktionen (z. B. das Durchsuchen einer SharePoint-Website oder eines OneDrive-Kontos) im Auftrag eines Benutzers, Administrators oder Diensts auszuführen. Weitere Informationen finden Sie unter [Der "app@sharepoint"-Benutzer in Überwachungsdatensätzen](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#the-appsharepoint-user-in-audit-records). |
|ClientIP|Edm.String|Ja|Die IP-Adresse des Geräts, das verwendet wurde, als die Aktivität protokolliert wurde. Die IP-Adresse wird im Adressformat IPv4 oder IPv6 angezeigt.<br/><br/>Bei einigen Diensten ist der in dieser Eigenschaft angezeigte Wert möglicherweise die IP-Adresse einer vertrauenswürdigen Anwendung (z.B. Office in den Web-Apps), die anstelle eines Benutzers in den Dienst einruft und nicht die IP-Adresse des Geräts, das von der Person, die die Aktivität ausgeführt hat, verwendet wird. <br/><br/>Außerdem wird für Azure Active Directory-bezogene Ereignisse die IP-Adresse nicht protokolliert und der Wert für die ClientIP-Eigenschaft ist `null`.|
|Bereich|Self.[AuditLogScope](#auditlogscope)|Nein|Wurde dieses Ereignis von einem gehosteten Office 365-Dienst oder einem lokalen Server erstellt? Mögliche Werte sind **online** und **onprem**. Beachten Sie, dass SharePoint die einzige Arbeitslast ist, die derzeit Ereignissen aus lokalen Umgebungen an O365 sendet.|
|||||

### <a name="enum-auditlogrecordtype---type-edmint32"></a>Enum: AuditLogRecordType - Typ: Edm.Int32

#### <a name="auditlogrecordtype"></a>AuditLogRecordType

|Wert|Elementname|Beschreibung|
|:-----|:-----|:-----|
|1|ExchangeAdmin|Ereignisse aus dem Exchange-Administrator-Überwachungsprotokoll.|
|2|ExchangeItem|Ereignisse aus einem Exchange-Postfachüberwachungsprotokoll für Aktionen, die für ein einzelnes Element ausgeführt wurden, z. B. das Erstellen oder Empfangen einer E-Mail-Nachricht.|
|3|ExchangeItemGroup|Ereignisse aus einem Exchange-Postfachüberwachungsprotokoll für Aktionen, die für mehrere Elemente ausgeführt werden können, z. B. das Verschieben oder Löschen einer oder mehrerer E-Mail-Nachrichten.|
|4|SharePoint|SharePoint-Ereignisse.|
|6|SharePointFileOperation|SharePoint-Dateivorgangsereignisse.|
|7|OneDrive|OneDrive for Business-Ereignisse.|
|8|AzureActiveDirectory|Azure Active Directory-Ereignisse.|
|9|AzureActiveDirectoryAccountLogon|Azure Active Directory OrgId-Anmeldeereignisse (veraltet).|
|10|DataCenterSecurityCmdlet|Rechenzentrum-Sicherheits-Cmdlet-Ereignisse.|
|11|ComplianceDLPSharePoint|DLP-Ereignisse (Data Loss Prevention, Schutz vor Datenverlust) in SharePoint und OneDrive for Business.|
|13|ComplianceDLPExchange|DLP-Ereignisse (Data Loss Prevention, Schutz vor Datenverlust) bei Konfiguration über die Unified DLP-Richtlinie. Auf Exchange-Transportregeln basierende DLP-Ereignisse werden nicht unterstützt.|
|14|SharePointSharingOperation|SharePoint-Freigabeereignisse.|
|15|AzureActiveDirectoryStsLogon|Secure Token Service (STS)-Anmeldeereignisse in Azure Active Directory.|
|16|SkypeForBusinessPSTNUsage|Public Switched Telephone Network (PSTN)-Ereignisse aus Skype for Business.|
|17|SkypeForBusinessUsersBlocked|Blockierte Benutzerereignisse aus Skype for Business.|
|18|SecurityComplianceCenterEOPCmdlet|Administratoraktionen aus dem Security & Compliance Center.|
|19|ExchangeAggregatedOperation|Aggregierte Exchange-Postfachüberwachungsereignisse.|
|20|PowerBIAudit|Power BI-Ereignisse.|
|21|CRM|Dynamics 365-Ereignisse.|
|22|Yammer|Yammer-Ereignisse.|
|23|SkypeForBusinessCmdlets|Skype for Business-Ereignisse.|
|24|Discovery|Ereignisse für eDiscovery-Aktivitäten, die durch die Ausführung von Inhaltssuchen und die Verwaltung von eDiscovery-Fällen im Security & Compliance Center durchgeführt werden.|
|25|MicrosoftTeams|Ereignisse von Microsoft-Teams.|
|28|ThreatIntelligence|Phishing- und Schadsoftwareereignisse aus Exchange Online Protection und Microsoft Defender für Office 365.|
|29|MailSubmission|Übermittlungsereignisse aus Exchange Online Protection und Microsoft Defender für Office 365.|
|30|MicrosoftFlow|Microsoft Power Automate-Ereignisse (vormals Microsoft Flow).|
|31|AeD|Advanced eDiscovery-Ereignisse.|
|32|MicrosoftStream|Microsoft Stream-Ereignisse|
|33|ComplianceDLPSharePointClassification|Ereignisse im Zusammenhang mit DLP-Klassifizierung in SharePoint.|
|34|ThreatFinder|Kampagnenbezogene Ereignisse von Microsoft Defender für Office 365.|
|35|Project|Microsoft Project-Ereignisse.|
|36|SharePointListOperation|SharePoint-Listenereignisse.|
|37|SharePointCommentOperation|SharePoint-Kommentarereignisse.|
|38|DataGovernance|Auf Aufbewahrungsrichtlinien und Aufbewahrungsbezeichnungen im Security & Compliance Center bezogene Ereignisse|
|39|Kaizala|Kaizala-Ereignisse.|
|40|SecurityComplianceAlerts|Security & Compliance-Warnsignale.|
|41|ThreatIntelligenceUrl|Zeitblockereignisse für sichere Links und Ereignisse zur Außerkraftsetzung von Blöcken aus Microsoft Defender für Office 365.|
|42|SecurityComplianceInsights|Ereignisse im Zusammenhang mit Einblicken und Berichten im Office 365 Security & Compliance Center.|
|43|MIPLabel|Ereignisse im Zusammenhang mit der Erkennung in der Transportpipeline von E-Mail-Nachrichten, die mithilfe von Vertraulichkeitsbezeichnungen (manuell oder automatisch) gekennzeichnet wurden. |
|44|WorkplaceAnalytics|Workplace Analytics-Ereignisse.|
|45|PowerAppsApp|Power Apps-Ereignisse.|
|46|PowerAppsPlan|Abonnementplan-Ereignisse für Power Apps. |
|47|ThreatIntelligenceAtpContent|Phishing- und Schadsoftwareereignisse für Dateien in SharePoint, OneDrive for Business und Microsoft Teams aus Microsoft Defender für Office 365.|
|48|LabelContentExplorer|Ereignisse im Zusammenhang mit dem [Inhalts-Explorer zur Datenklassifizierung](/microsoft-365/compliance/data-classification-content-explorer).|
|49|TeamsHealthcare|Ereignisse im Zusammenhang mit der [Anwendung "Patienten"](/MicrosoftTeams/expand-teams-across-your-org/healthcare/patients-audit) in Microsoft Teams für das Gesundheitswesen.|
|50|ExchangeItemAggregated|Ereignisse im Zusammenhang mit der [Postfachüberwachungsaktion "MailItemsAccessed"](/microsoft-365/compliance/mailitemsaccessed-forensics-investigations).|
|51|HygieneEvent|Ereignisse im Zusammenhang mit ausgehenden Spamschutzmaßnahmen. |
|52|DataInsightsRestApiAudit|Ereignisse der Datenerkenntnisse-Rest-API.|
|53|InformationBarrierPolicyApplication|Ereignisse im Zusammenhang mit der Anwendung von Richtlinien für Informationsbarrieren.|
|54|SharePointListItemOperation|SharePoint-Listenelementereignisse.|
|55|SharePointContentTypeOperation|SharePoint-Listeninhaltstyp-Ereignisse.|
|56|SharePointFieldOperation|SharePoint-Listenfeldereignisse.|
|57|MicrosoftTeamsAdmin|Teams-Administratorereignisse.|
|58|HRSignal|Ereignisse im Zusammenhang mit HR-Datensignalen, welche die Insider-Risikomanagement-Lösung unterstützen.|
|59|MicrosoftTeamsDevice|Teams-Geräteereignisse.|
|60|MicrosoftTeamsAnalytics|Teams-Analyseereignisse.|
|61|InformationWorkerProtection|Ereignisse im Zusammenhang mit Warnungen über kompromittierte Benutzer.|
|62|Campaign|E-Mail-Kampagnen-Ereignisse von Microsoft Defender für Office 365.|
|63|DLPEndpoint|Endpunkt-DLP-Ereignisse.|
|64|AirInvestigation|Automated incident response (AIR) events – Automatisierte Untersuchungs- und Reaktionsereignisse.|
|65|Quarantine|Quarantäneereignisse.|
|66|MicrosoftForms|Microsoft Forms-Ereignisse.|
|67|ApplicationAudit|Anwendungsprotokoll-Ereignisse.|
|68|ComplianceSupervisionExchange|Ereignisse, die von dem Kommunikationscompliance-Modell anstößiger Sprache nachverfolgt werden.|
|69|CustomerKeyServiceEncryption|Ereignisse im Zusammenhang mit dem Dienst zur Kundenschlüssel-Verschlüsselung.|
|70|OfficeNative|Ereignisse im Zusammenhang mit Vertraulichkeitsbezeichnungen, die auf Office-Dokumente angewendet werden.|
|71|MipAutoLabelSharePointItem|Ereignisse bezüglich automatischer Beschriftung in SharePoint.|
|72|MipAutoLabelSharePointPolicyLocation|Ereignisse bezüglich der Richtlinie für die automatischer Beschriftung in SharePoint.|
|73|MicrosoftTeamsShifts|Teams-Schichtenereignisse.|
|75|MipAutoLabelExchangeItem|Ereignisse bezüglich automatischer Beschriftung in Exchange.|
|76|CortanaBriefing|Briefing E-Mail-Ereignisse.|
|77|Suche|Ereignisse im Zusammenhang mit der Durchführung von Suchabfragen in SharePoint und Exchange.|
|78|WDATPAlerts|Ereignisse im Zusammenhang mit Warnungen, die von Windows Defender für Endpunkt generiert werden.|
|81|MDATPAudit|Microsoft Defender für Endpunkt-Ereignisse.|
|82|SensitivityLabelPolicyMatch|Ereignisse, die generiert werden, wenn die mit einer Vertraulichkeitsbezeichnung beschriftete Datei geöffnet oder umbenannt wird.|
|83|SensitivityLabelAction|Ereignis, das generiert wird, wenn Vertraulichkeitsbezeichnungen angewendet, aktualisiert oder von einer Datei entfernt werden.|
|84|SensitivityLabeledFileAction|Ereignisse, die generiert werden, wenn eine mit einer Vertraulichkeitsbezeichnung beschriftete Datei geöffnet oder umbenannt wird.|
|85|AttackSim|Angriffssimulator-Ereignisse.|
|86|AirManualInvestigation|Ereignisse im Zusammenhang mit manuellen Ermittlungen in „Automatisierte Untersuchung und Antwort (AIR – Automated Investigation and Response)“. |
|87|SecurityComplianceRBAC|Ereignisse aus RBAC-Sicherheit und -Konformität.|
|88|UserTraining|Angriffssimulator-Schulungsereignisse in Microsoft Defender für Office 365.|
|89|AirAdminActionInvestigation|Ereignisse im Zusammenhang mit Administratoraktionen in „Automatisierte Untersuchung und Antwort (AIR – Automated Investigation and Response)“.|
|90|MSTIC|Threat-Intelligence-Ereignisse in Microsoft Defender für Office 365.|
|91|PhysicalBadgingSignal|Ereignisse im Zusammenhang mit physischen Ausweissignalen, welche die Insider-Risikomanagement-Lösung unterstützen.|
|93|AipDiscover|Azure Information Protection (AIP)-Scanner-Ereignisse.|
|94|AipSensitivityLabelAction|AIP-Vertraulichkeitsbezeichnungsereignisse. |
|95|AipProtectionAction|AIP-Schutzereignisse.|
|96|AipFileDeleted|AIP-Dateilöschereignisse.|
|97|AipHeartBeat|AIP-Taktsignalereignisse.|
|98|MCASAlerts|Ereignisse, die Warnungen entsprechen, die von Microsoft Cloud App Security ausgelöst werden.|
|99|OnPremisesFileShareScannerDlp|Ereignisse im Zusammenhang mit der Suche nach vertraulichen Daten in Dateifreigaben.|
|100|OnPremisesSharePointScannerDlp|Ereignisse im Zusammenhang mit der Suche nach vertraulichen Daten in SharePoint.|
|101|ExchangeSearch|Ereignisse im Zusammenhang mit der Verwendung von Outlook im Web (OWA) zur Suche nach Postfachelementen.|
|102|SharePointSearch|Ereignisse im Zusammenhang mit dem Durchsuchen der SharePoint-Startseite einer Organisation.|
|103|PrivacyInsights|Datenschutzerkenntnis-Ereignisse.|
|105|MyAnalyticsSettings|MyAnalytics-Ereignisse.|
|106|SecurityComplianceUserChange|Ereignisse im Zusammenhang mit dem Ändern oder Löschen eines Benutzers.|
|107|ComplianceDLPExchangeClassification|Ereignisse bezüglich Exchange DLP-Klassifizierung.|
|109|MipExactDataMatch|Ereignisse bezüglich der Klassifizierung zur genauen Datenübereinstimmung (EDM – Exact Data Match).|
||||

### <a name="enum-user-type---type-edmint32"></a>Enumeration: Benutzertyp – Typ: Edm.Int32

#### <a name="user-type"></a>Benutzertyp

|Wert|Elementname|Beschreibung|
|:-----|:-----|:-----|
|0|Regular|Ein normaler Benutzer.|
|1|Reserved|Ein reservierter Benutzer.|
|2|Administrator|Ein Administrator.|
|3|DcAdmin|Ein Microsoft-Rechenzentrum-Operator.|
|4|System|Ein Systemkonto.|
|5|Anwendung|Eine Anwendung.|
|6|ServicePrincipal|Ein Dienstprinzipal.|
|7|CustomPolicy|Eine benutzerdefinierte Richtlinie.|
|8|SystemPolicy|Eine Systemrichtlinie.|
||||

### <a name="enum-auditlogscope---type-edmint32"></a>Enumeration: AuditLogScope - Typ: Edm.Int32

#### <a name="auditlogscope"></a>AuditLogScope

|Wert|Elementname|Beschreibung|
|:-----|:-----|:-----|
|0|Online|Dieses Ereignis wurde von einem gehosteten O365-Dienst erstellt.|
|1|Onprem|Dieses Ereignis wurde von einem lokalen Server erstellt.|
||||

## <a name="sharepoint-base-schema"></a>SharePoint-Basisschema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Website|Edm.Guid|Nein|Die GUID der Website, auf der sich die Datei oder der Ordner, auf die bzw. den der Benutzer zugegriffen hat, befindet.|
|ItemType|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[ItemType](#itemtype)"|Nein|Der Typ des Objekts, auf das zugegriffen bzw. das geändert wurde. In der Tabelle [ItemType](#itemtype) finden Sie Informationen zu den Typen von Objekten.|
|EventSource|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[EventSource](#eventsource)"|Nein|Gibt an, dass ein Ereignis in SharePoint eingetreten ist. Mögliche Werte sind **SharePoint** oder **ObjectModel**.|
|SourceName|Edm.String|Nein|Die Entität, die den überwachten Vorgang ausgelöst hat. Mögliche Werte sind SharePoint oder **ObjectModel**.|
|UserAgent|Edm.String|Nein|Informationen zum Client oder Browser des Benutzers. Diese Informationen werden vom Client oder Browser bereitgestellt.|
|MachineDomainInfo|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|Nein|Informationen zu Synchronisierungsvorgängen von Geräten. Diese Informationen werden nur angezeigt, wenn sie in der Anforderung vorhanden sind.|
|MachineId|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|Nein|Informationen zu Synchronisierungsvorgängen von Geräten. Diese Informationen werden nur angezeigt, wenn sie in der Anforderung vorhanden sind.|
|||||

### <a name="enum-itemtype---type-edmint32"></a>Enumeration: ItemType - Typ: Edm.Int32

#### <a name="itemtype"></a>ItemType

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|0|Ungültig|Das Element ist keines der anderen Elementtypen (die in dieser Tabelle aufgeführt sind).|
|1|Datei|Das Element ist eine Datei.|
|5|Ordner|Das Element ist ein Ordner.|
|6|Netz|Das Element ist ein Netz.|
|7|Website|Das Element ist eine Website.|
|8|Mandant|Das Element ist ein Mandant.|
|9|DocumentLibrary|Das Element ist eine Dokumentbibliothek.|
|11|Seite|Das Element ist eine Seite.|
||||

### <a name="enum-eventsource---type-edmint32"></a>Enumeration: EventSource - Typ: Edm.Int32

#### <a name="eventsource"></a>EventSource

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|0|SharePoint|Die Ereignisquelle ist SharePoint.|
|1|ObjectModel|Die Ereignisquelle ist ObjectModel.|
||||

### <a name="enum-sharepointauditoperation---type-edmint32"></a>Enumeration: SharePointAuditOperation - Typ: Edm.Int32

|**Elementname**|**Beschreibung**|
|:-----|:-----|
|AccessInvitationAccepted|Der Empfänger einer Einladung zum Anzeigen oder Bearbeiten einer freigegebenen Datei (oder eines Ordners) hat durch Klicken auf den Link in der Einladung auf die freigegebene Datei zugegriffen.|
|AccessInvitationCreated|Der Benutzer sendet eine Einladung zum Anzeigen oder Bearbeiten einer freigegebenen Datei oder eines freigegebenen Ordners auf einer SharePoint- oder OneDrive for Business-Website an eine andere Person (innerhalb oder außerhalb seiner Organisation). Die Details des Ereigniseintrags geben Folgendes an: den Namen der freigegebenen Datei, den Benutzer, an den die Einladung gesendet wurde, und den Typ der Freigabeberechtigung, der von der Person ausgewählt wurde, die die Einladung gesendet hat.|
|AccessInvitationExpired|Eine an einen externen Benutzer gesendete Einladung läuft ab. Standardmäßig läuft eine Einladung, die an einen Benutzer außerhalb der Organisation gesendet wurde, nach 7 Tagen ab, wenn die Einladung nicht angenommen wird.|
|AccessInvitationRevoked|Der Websiteadministrator oder Besitzer einer Website oder eines Dokuments in SharePoint oder OneDrive for Business zieht eine Einladung zurück, die an einen Benutzer außerhalb Ihrer Organisation gesendet wurde. Eine Einladung kann nur zurückgezogen werden, bevor sie akzeptiert wurde.|
|AccessInvitationUpdated|Der Benutzer, der eine Einladung an eine andere Person zum Anzeigen oder Bearbeiten einer freigegebenen Datei oder eines Ordners auf einer SharePoint- oder OneDrive for Business-Website erstellt hat, sendet die Einladung erneut.|
|AccessRequestApproved|Der Websiteadministrator oder Besitzer einer Website oder eines Dokuments in SharePoint oder OneDrive for Business genehmigt eine Benutzeranforderung für den Zugriff auf die Website oder das Dokument.|
|AccessRequestCreated|Der Benutzer fordert Zugriff auf eine Website oder ein Dokument in SharePoint oder OneDrive for Business, für die bzw. das er nicht über eine Zugriffsberechtigung verfügt. |
|AccessRequestRejected|Der Websiteadministrator oder Besitzer einer Website oder eines Dokuments in SharePoint lehnt eine Benutzeranforderung für den Zugriff auf die Website oder das Dokument ab.|
|ActivationEnabled|Benutzer können Formularvorlagen browserfähig machen, die keinen Formularcode enthalten, keine volle Vertrauenswürdigkeit erfordern, nicht auf einem mobilen Gerät wiedergegeben werden und keine von einem Serveradministrator verwaltete Datenverbindung verwenden.|
|AdministratorAddedToTermStore|Es wurde ein Terminologiespeicheradministrator hinzugefügt.|
|AdministratorDeletedFromTermStore|Es wurde ein Terminologiespeicheradministrator gelöscht.|
|AllowGroupCreationSet|Der Websiteadministrator oder -besitzer fügt eine Berechtigungsstufe zu einer SharePoint oder OneDrive for Business-Website hinzu, die es einem Benutzer mit dieser Berechtigung ermöglicht, eine Gruppe für diese Website zu erstellen.|
|AppCatalogCreated|Der App-Katalog, der erstellt wurde, um benutzerdefinierte Geschäfts-Apps für Ihre SharePoint-Umgebung bereitzustellen.|
|AuditPolicyRemoved|Das Dokument LifeCycle-Richtlinie wurde für eine Websitesammlung entfernt.|
|AuditPolicyUpdate|Das Dokument LifeCycle-Richtlinie wurde für eine Websitesammlung aktualisiert.|
|AzureStreamingEnabledSet|Ein Videoportal-Besitzer hat Videostreaming aus Azure erlaubt.|
|CollaborationTypeModified|Der für die Kollaboration auf Websites zulässige Typ (z. B. Intranet, Extranet oder Öffentlich) wurde geändert.|
|ConnectedSiteSettingModified|Der Benutzer hat die Verknüpfung zwischen einem Projekt und einer Projektwebsite erstellt, geändert oder gelöscht oder der Benutzer ändert die Einstellung der Synchronisierung der Verknüpfung in der Project Web App.|
|CreateSSOApplication|Die Zielanwendung, die im Secure Store Service erstellt wurde.|
|CustomFieldOrLookupTableCreated|Der Benutzer hat ein benutzerdefiniertes Feld oder eine benutzerdefinierte Suchtabelle/ein benutzerdefiniertes Element in der Project Web App erstellt.|
|CustomFieldOrLookupTableDeleted|Der Benutzer hat eine benutzerdefinierte Tabelle oder ein benutzerdefiniertes Element "Feld" oder "Nachschlagen" in der Project Web App gelöscht.|
|CustomFieldOrLookupTableModified|Der Benutzer hat eine benutzerdefinierte Tabelle oder ein benutzerdefiniertes Element "Feld" oder "Nachschlagen" in der Project Web App geändert.|
|CustomizeExemptUsers|Der globale Administrator hat die Liste der ausgenommenen Benutzer-Agents im SharePoint Admin Center angepasst. Sie können angeben, welche Benutzer-Agents vom Empfangen einer gesamten Webseite zum Indizieren ausgenommen werden sollen. Das bedeutet: Wenn ein Benutzer-Agent, den Sie als ausgenommen festgelegt haben, auf ein InfoPath-Formular trifft, wird das Formular als eine XML-Datei und nicht als eine gesamte Webseite zurückgegeben. Dadurch werden InfoPath-Formulare schneller indiziert.|
|DefaultLanguageChangedInTermStore*|Die Einstellung für die Standardsprache im Terminologiespeicher wurde geändert.|
|DelegateModified|Der Benutzer hat einen Sicherheitsbeauftragten in der Project Web App erstellt oder geändert.|
|DelegateRemoved|Der Benutzer hat einen Sicherheitsbeauftragten in der Project Web App gelöscht.|
|DeleteSSOApplication|Eine SSO-Anwendung wurde gelöscht.|
|eDiscoveryHoldApplied|Ein In-Situ-Speicher wurde auf einer Inhaltsquelle platziert. In-Situ-Speicher werden mit einer eDiscovery-Websitesammlung (z. B. das eDiscovery Center) in SharePoint verwaltet.|
|eDiscoveryHoldRemoved|Ein In-Situ-Speicher wurde aus einer Inhaltsquelle entfernt. In-Situ-Speicher werden mit einer eDiscovery-Websitesammlung (z. B. das eDiscovery Center) in SharePoint verwaltet.|
|eDiscoverySearchPerformed|Eine eDiscovery-Suche wurde mit einer eDiscovery-Websitesammlung in SharePoint ausgeführt.|
|EngagementAccepted|Ein Benutzer akzeptiert eine Ressourcenverhandlung in der Project Web App.|
|EngagementModified|Ein Benutzer ändert eine Ressourcenverhandlung in der Project Web App.|
|EngagementRejected|Ein Benutzer lehnt eine Ressourcenverhandlung in der Project Web App ab.|
|EnterpriseCalendarModified|Ein Benutzer kopiert, ändert oder löscht einen Enterprise-Kalender in der Project Web App.|
|EntityDeleted|Der Benutzer löscht eine Arbeitszeittabelle in der Project Web App.|
|EntityForceCheckedIn|Der Benutzer erzwingt die Überprüfung eines Kalenders, eines benutzerdefinierten Felds oder einer Nachschlagetabelle in der Project Web App.|
|ExemptUserAgentSet|Ein globaler Administrator fügt einen Benutzer-Agent zu der Liste der ausgenommenen Benutzer-Agents im SharePoint Admin Center hinzu.|
|FileAccessed|Der Benutzer oder das Systemkonto greift auf eine Datei auf einer SharePoint- oder OneDrive for Business-Website zu. Systemkonten können ebenfalls FileAccessed-Ereignisse generieren.|
|FileCheckOutDiscarded|Der Benutzer verwirft eine ausgecheckte Datei. Das bedeutet, dass alle Änderungen, die an der Datei vorgenommen wurden, während sie ausgecheckt war, verworfen und nicht in der Version des Dokuments in der Dokumentbibliothek gespeichert werden.|
|FileCheckedIn|Ein Benutzer checkt ein Dokument ein, das er aus der SharePoint- oder OneDrive for Business-Dokumentbibliothek ausgecheckt hat.|
|FileCheckedOut|Der Benutzer checkt ein Dokument aus, das sich in einer SharePoint- oder OneDrive for Business-Dokumentbibliothek befindet. Benutzer können Dokumente, die für sie freigegeben wurden, auschecken und Änderungen daran vornehmen.|
|FileCopied|Der Benutzer kopiert ein Dokument von einer SharePoint- oder OneDrive for Business-Website. Die kopierte Datei kann in einem anderen Ordner auf der Website gespeichert werden.|
|FileDeleted|Ein Benutzer löscht ein Dokument von einer SharePoint- oder OneDrive for Business-Website.|
|FileDeletedFirstStageRecycleBin|Ein Benutzer löscht ein Dokument aus dem Papierkorb der SharePoint- oder OneDrive for Business-Website.|
|FileDeletedSecondStageRecycleBin|Ein Benutzer löscht ein Dokument aus dem endgültigen Papierkorb der SharePoint- oder OneDrive for Business-Website.|
|FileDownloaded|Ein Benutzer lädt ein Dokument von einer SharePoint- oder OneDrive for Business-Website herunter.|
|FileFetched|Dieses Ereignis ist veraltet und wurde durch das FileAccessed-Ereignis ersetzt.|
|FileModified|Ein Benutzer oder das Systemkonto ändert den Inhalt oder die Eigenschaften eines Dokuments, das sich auf SharePoint- oder OneDrive for Business-Website befindet.|
|FileMoved|Ein Benutzer verschiebt ein Dokument von seinem aktuellen Speicherort auf einer SharePoint- oder OneDrive for Business-Website an eine neue Position.|
|FilePreviewed|Ein Benutzer zeigt eine Vorschau eines Dokuments auf einer SharePoint- oder OneDrive for Business-Website an.|
|FileRenamed|Ein Benutzer benennt ein Dokument auf einer SharePoint- oder OneDrive for Business-Website um.|
|FileRestored|Ein Benutzer stellt ein Dokument aus dem Papierkorb der SharePoint- oder OneDrive for Business-Website wieder her. |
|FileSyncDownloadedFull|Ein Benutzer richtet eine Synchronisierungsbeziehung ein und lädt zum ersten Mal erfolgreich Dateien aus einer SharePoint- oder OneDrive for Business-Dokumentbibliothek auf seinen Computer.|
|FileSyncDownloadedPartial|Der Benutzer lädt alle Änderungen an Dateien aus der SharePoint- oder OneDrive for Business-Dokumentbibliothek erfolgreich herunter. Dieses Ereignis gibt an, dass alle an Dateien in der Dokumentbibliothek vorgenommenen Änderungen auf den Computer des Benutzers heruntergeladen wurden. Es wurden nur Änderungen heruntergeladen, weil die Dokumentbibliothek vom Benutzer zuvor heruntergeladen wurde (wie durch das Ereignis „FileSyncDownloadedFull“ angegeben).|
|FileSyncUploadedFull|Ein Benutzer richtet eine Synchronisierungsbeziehung ein und lädt zum ersten Mal erfolgreich Dateien von seinem Computer in eine SharePoint- oder OneDrive for Business-Dokumentbibliothek.|
|FileSyncUploadedPartial|Der Benutzer lädt Änderungen an Dateien in eine SharePoint- oder OneDrive for Business-Dokumentbibliothek erfolgreich hoch. Dieses Ereignis gibt an, dass alle Änderungen, die an der lokalen Version einer Datei aus einer Dokumentbibliothek vorgenommen wurden, in diese Bibliothek erfolgreich hochgeladen werden. Es werden nur Änderungen hochgeladen, weil diese Dateien vom Benutzer zuvor hochgeladen wurden (wie durch das Ereignis „FileSyncUploadedFull“ angegeben).|
|FileUploaded|Ein Benutzer lädt ein Dokument auf eine SharePoint- oder OneDrive for Business-Website. |
|FileViewed|Dieses Ereignis ist veraltet und wurde durch das FileAccessed-Ereignis ersetzt.|
|FolderCopied|Ein Benutzer kopiert einen Ordner von einer SharePoint- oder OneDrive for Business-Website in einen anderen Speicherort von SharePoint oder OneDrive for Business.|
|FolderCreated|Ein Benutzer erstellt einen Ordner auf einer SharePoint- oder OneDrive for Business-Website.|
|FolderDeleted|Ein Benutzer löscht einen Ordner von einer SharePoint- oder OneDrive for Business-Website.|
|FolderDeletedFirstStageRecycleBin|Ein Benutzer löscht einen Ordner aus dem Papierkorb der SharePoint- oder OneDrive for Business-Website.|
|FolderDeletedSecondStageRecycleBin|Ein Benutzer löscht einen Ordner aus dem endgültigen Papierkorb der SharePoint- oder OneDrive for Business-Website.|
|FolderModified|Ein Benutzer ändert einen Ordner auf einer SharePoint- oder OneDrive for Business-Website. Dieses Ereignis umfasst Ordner-Metadatenänderungen wie z. B. Tags und Eigenschaften.|
|FolderMoved|Ein Benutzer verschiebt einen Ordner von einer SharePoint- oder OneDrive for Business-Website.|
|FolderRenamed|Ein Benutzer benennt einen Ordner auf einer SharePoint- oder OneDrive for Business-Website um.|
|FolderRestored|Ein Benutzer stellt einen Ordner aus dem Papierkorb auf der SharePoint- oder OneDrive for Business-Website wieder her.|
|GroupAdded|Der Websiteadministrator oder -besitzer erstellt eine Gruppe für eine SharePoint- oder OneDrive for Business-Website oder aber führt eine Aufgabe aus, die zur Erstellung einer Gruppe führt. Wenn ein Benutzer beispielsweise zum ersten Mal einen Link zum Freigeben einer Datei erstellt, wird seiner OneDrive for Business-Website eine Systemgruppe hinzugefügt. Dieses Ereignis kann sich auch dadurch ergeben, dass ein Benutzer einen Link mit Bearbeitungsberechtigungen für eine freigegebene Datei erstellt.|
|GroupRemoved|Ein Benutzer löscht eine Gruppe aus einer SharePoint- oder OneDrive for Business-Website. |
|GroupUpdated|Der Websiteadministrator oder -besitzer ändert die Einstellungen einer Gruppe für eine SharePoint- oder OneDrive for Business-Website. Dies kann das Ändern des Gruppennamens, das Ändern der Personen, die Gruppenmitgliedschaften anzeigen oder bearbeiten können, sowie das Ändern der Handhabung von Mitgliedschaftsanforderungen umfassen.|
|LanguageAddedToTermStore|Eine Sprache wird zum Terminologiespeicher hinzugefügt.|
|LanguageRemovedFromTermStore|Eine Sprache wird aus dem Terminologiespeicher gelöscht.|
|LegacyWorkflowEnabledSet|Der Websiteadministrator oder -besitzer fügt den Inhaltstyp einer SharePoint-Workflowaufgabe zur Website hinzu. Globale Administratoren können auch Workflows für die gesamte Organisation im SharePoint Admin Center aktivieren.|
|LookAndFeelModified|Ein Benutzer ändert Schnellstart-, Gantt-Diagramm- oder Gruppenformate.  Oder ein Benutzer erstellt, ändert oder löscht eine Ansicht in der Project Web App.|
|ManagedSyncClientAllowed|Ein Benutzer richtet erfolgreich eine Synchronisierungsbeziehung mit einer SharePoint- oder OneDrive for Business-Website ein. Die Synchronisierungsbeziehung ist erfolgreich, da der Computer des Benutzers Mitglied einer Domäne ist, die zur Liste der Domänen, die in Ihrer Organisation auf Dokumentbibliotheken zugreifen können (auch Liste der sicheren Empfänger genannt), hinzugefügt wurde. Weitere Informationen finden Sie unter [Verwenden von SharePoint Online PowerShell](https://go.microsoft.com/fwlink/p/?LinkID=534609) zum Aktivieren der OneDrive-Synchronisierung für Domänen, die in der Liste der sicheren Empfänger enthalten sind.|
|MaxQuotaModified|Das maximale Kontingent für eine Website wurde geändert.|
|MaxResourceUsageModified|Der maximal zulässige Ressourceneinsatz für eine Website wurde geändert.|
|MySitePublicEnabledSet|Die Kennzeichnung, die es Benutzern ermöglicht, öffentliche "Meine Websites" zu besitzen, wurde durch den SharePoint-Administrator festgelegt.|
|NewsFeedEnabledSet|Der Websiteadministrator oder -besitzer aktiviert RSS-Feeds für eine SharePoint- oder OneDrive for Business-Website. Globale Administratoren können RSS-Feeds für die gesamte Organisation im SharePoint Admin Center aktivieren.|
|ODBNextUXSettings|Eine neue Benutzeroberfläche für OneDrive for Business wurde aktiviert.|
|OfficeOnDemandSet|Der Websiteadministrator aktiviert Office on Demand, wodurch Benutzer auf die neueste Version von Office-Desktopanwendungen zugreifen können. Office on Demand wird im SharePoint Admin Center aktiviert und erfordert ein Office 365-Abonnement, das vollständige, installierte Office-Anwendungen umfasst.|
|PageViewed|Ein Benutzer zeigt eine Seite auf einer SharePoint- oder OneDrive for Business-Website an. Dies schließt das Anzeigen von Dokumentbibliotheksdateien einer SharePoint- oder OneDrive for Business-Website in einem Browser nicht ein.|
|PeopleResultsScopeSet|Der Websiteadministrator erstellt oder ändert die Ergebnisquelle für Personensuchen für eine SharePoint-Website.|
|PermissionSyncSettingModified|Ein Benutzer ändert die Synchronisierungseinstellungen für Projektberechtigungen in der Project Web App.|
|PermissionTemplateModified|Ein Benutzer erstellt, ändert oder löscht eine Berechtigungsvorlage in der Project Web App.|
|PortfolioDataAccessed|Ein Benutzer greift in der Project Web App auf Portfolioinhalte (Treiberbibliothek, Treiberpriorisierung, Portfolioanalysen) zu.|
|PortfolioDataModified|Ein Benutzer erstellt, ändert oder löscht in der Project Web App Portfoliodaten (Treiberbibliothek, Treiberpriorisierung, Portfolioanalysen).|
|PreviewModeEnabledSet|Der Websiteadministrator aktiviert die Dokumentvorschau für eine SharePoint-Website.|
|ProjectAccessed|Ein Benutzer greift über die Project Web App auf Inhalte zu.|
|ProjectCheckedIn|Ein Benutzer checkt ein Projekt ein, das er aus einer Project Web App hat ausgecheckt.|
|ProjectCheckedOut|Ein Benutzer checkt ein Projekt aus, das sich in der Project Web App befindet. Wenn Benutzer die Berechtigung zum Öffnen einen Projekts besitzen, können sie dieses auch auschecken und ändern.|
|ProjectCreated|Ein Benutzer erstellt ein Projekt in der Project Web App.|
|ProjectDeleted|Ein Benutzer löscht ein Projekt in der Project Web App.|
|ProjectForceCheckedIn|Ein Benutzer erzwingt das Einchecken eines Projekts in der Project Web App.|
|ProjectModified|Ein Benutzer ändert ein Projekt in der Project Web App.|
|ProjectPublished|Ein Benutzer veröffentlicht ein Projekt in der Project Web App.|
|ProjectWorkflowRestarted|Ein Benutzer startet einen Workflow in der Project Web App erneut.|
|PWASettingsAccessed|Ein Benutzer greift über CSOM auf die Project Web App-Einstellungen zu.|
|PWASettingsModified|Ein Benutzer ändert die Project Web App-Konfiguration.|
|QueueJobStateModified|Ein Benutzer bricht einen Auftrag in der Warteschlange der Project Web App ab oder startet einen solchen Auftrag neu.|
|QuotaWarningEnabledModified|Die Speicherkontingent-Warnung wurde geändert.|
|RenderingEnabled|Browserfähige Formularvorlagen werden von InfoPath Forms Services wiedergegeben.|
|ReportingAccessed|Der Benutzer hat auf den Endpunkt für die Berichterstellung in der Project Web App zugegriffen.|
|ReportingSettingModified|Der Benutzer ändert die Konfiguration für die Berichterstellung in der Project Web App.|
|ResourceAccessed|Der Benutzer greift auf einen Enterprise-Ressourceninhalt in der Project Web App zu.|
|ResourceCheckedIn|Ein Benutzer checkt eine Enterprise-Ressource ein, die er aus einer Project Web App ausgecheckt hat.|
|ResourceCheckedOut|Ein Benutzer checkt eine Enterprise-Ressource aus, die sich in einer Project Web App befindet.|
|ResourceCreated|Ein Benutzer erstellt eine Enterprise-Ressource in einer Project Web App.|
|ResourceDeleted|Ein Benutzer löscht eine Enterprise-Ressource aus einer Project Web App.|
|ResourceForceCheckedIn|Ein Benutzer erzwingt das Einchecken einer Enterprise-Ressource in einer Project Web App.|
|ResourceModified|Ein Benutzer ändert eine Enterprise-Ressource in einer Project Web App.|
|ResourcePlanCheckedInOrOut|Ein Benutzer checkt einen Ressourcenplan in der Project Web App ein oder aus.|
|ResourcePlanModified|Ein Benutzer ändert einen Ressourcenplan in der Project Web App.|
|ResourcePlanPublished|Ein Benutzer veröffentlicht einen Ressourcenplan in der Project Web App.|
|ResourceRedacted|Ein Benutzer bearbeitet eine Enterprise-Ressource, indem er alle persönlichen Informationen in der Project Web App löscht.|
|ResourceWarningEnabledModified|Die Ressourcenkontingent-Warnung wurde geändert.|
|SSOGroupCredentialsSet|Die Gruppenanmeldeinformationen in Secure Store Service wurden festgelegt.|
|SSOUserCredentialsSet|Die Benutzeranmeldeinformationen in Secure Store Service wurden festgelegt.|
|SearchCenterUrlSet|Die Suchcenter-URL wurde festgelegt.|
|SecondaryMySiteOwnerSet|Ein Benutzer hat einen sekundären Besitzer zu seiner "Meine Website" hinzugefügt.|
|SecurityCategoryModified|Ein Benutzer erstellt, ändert oder löscht eine Sicherheitskategorie in der Project Web App.|
|SecurityGroupModified|Ein Benutzer erstellt, ändert oder löscht eine Sicherheitsgruppe in der Project Web App.|
|SendToConnectionAdded|Globaler Administrator erstellt auf der Seite „Datensatzverwaltung“ im SharePoint Admin Center eine neue Verbindung vom Typ „Senden an“. Eine Verbindung vom Typ „Senden an“ legt die Einstellungen für ein Dokumentrepository oder Datenarchiv fest. Wenn Sie eine Verbindung vom Typ „Senden an“ erstellen, kann die Inhaltsorganisation Dokumente an den angegebenen Speicherort übermitteln.|
|SendToConnectionRemoved|Der globale Administrator löscht eine Senden-an-Verbindung auf der Verwaltungsseite für Datensätze im SharePoint Admin Center.|
|SharedLinkCreated|Der Benutzer erstellt einen Link zu einer freigegebenen Datei in SharePoint oder OneDrive for Business. Dieser Link kann an andere Personen gesendet werden, um ihnen Zugriff auf die Datei zu gewähren. Ein Benutzer kann zwei Arten von Links erstellen: einen Link, der einem Benutzer das Anzeigen und Bearbeiten der freigegebenen Datei ermöglicht, oder einen Link, der dem Benutzer nur das Anzeigen der Datei gestattet.|
|SharedLinkDisabled|Ein Benutzer deaktiviert (dauerhaft) einen Link, der zum Freigeben einer Datei erstellt wurde.|
|SharingInvitationAccepted*|Ein Benutzer akzeptiert eine Einladung zur Freigabe von Dateien oder Ordnern. Dieses Ereignis wird protokolliert, wenn ein Benutzer eine Datei für andere Benutzer freigibt.|
|SharingRevoked|Der Benutzer hebt die Freigabe einer Datei oder eines Ordners auf, die bzw. der zuvor für andere Benutzer freigegeben wurde. Dieses Ereignis wird protokolliert, wenn ein Benutzer die Freigabe einer Datei für andere Benutzer beendet.|
|SharingSet|Ein Benutzer gibt eine Datei oder einen Ordner in SharePoint oder OneDrive for Business für einen anderen Benutzer in der Organisation frei.|
|SiteAdminChangeRequest|Benutzer fordert, als Websitesammlungsadministrator für eine SharePoint-Websitesammlung hinzugefügt zu werden. Websitesammlungsadministratoren verfügen über Vollzugriffsberechtigungen für die Websitesammlung und alle Unterwebsites.|
|SiteCollectionAdminAdded*|Der Websitesammlungsadministrator oder -besitzer fügt eine Person als Websitesammlungsadministrator für eine SharePoint- oder OneDrive for Business-Website hinzu. Websitesammlungsadministratoren verfügen über Vollzugriff für die Websitesammlung und alle Unterwebsites.|
|SiteCollectionCreated| Der globale Administrator erstellt eine neue Websitesammlung in Ihrer SharePoint-Organisation.|
|SiteRenamed|Der Websiteadministrator oder -besitzer benennt die SharePoint- oder OneDrive for Business-Website um.|
|StatusReportModified|Ein Benutzer erstellt, ändert oder löscht einen Statusbericht in der Project Web App.|
|SyncGetChanges|Ein Benutzer klickt auf **Synchronisieren** in der Taskleiste Aktion in SharePoint oder OneDrive for Business, um alle Änderungen an einer Datei in einer Dokumentbibliothek auf seinem Computer zu synchronisieren.|
|TaskStatusAccessed|Ein Benutzer greift auf den Status einer oder mehrerer Aufgaben in der Project Web App zu.|
|TaskStatusApproved|Ein Benutzer bestätigt ein Statusupdate einer oder mehrerer Aufgaben in der Project Web App.|
|TaskStatusRejected|Ein Benutzer lehnt ein Statusupdate einer oder mehrerer Aufgaben in der Project Web App ab.|
|TaskStatusSaved|Ein Benutzer speichert ein Statusupdate einer oder mehrerer Aufgaben in der Project Web App.|
|TaskStatusSubmitted|Ein Benutzer übermittelt ein Statusupdate einer oder mehrerer Aufgaben in der Project Web App.|
|TimesheetAccessed|Ein Benutzer greift auf eine Arbeitszeittabelle in der Project Web App zu.|
|TimesheetApproved|Ein Benutzer bestätigt eine Arbeitszeittabelle in der Project Web App.|
|TimesheetRejected|Ein Benutzer lehnt eine Arbeitszeittabelle in der Project Web App ab.|
|TimesheetSaved|Ein Benutzer speichert eine Arbeitszeittabelle in der Project Web App.|
|TimesheetSubmitted|Ein Benutzer übermittelt eine Arbeitszeittabelle in der Project Web App.|
|UnmanagedSyncClientBlocked|Ein Benutzer versucht, eine Synchronisierungsbeziehung mit einer SharePoint- oder OneDrive for Business-Website von einem Computer aus herzustellen, der kein Mitglied der Domäne Ihrer Organisation ist oder Mitglied einer Domäne ist, die nicht in die Liste der Domänen übernommen wurde, die in Ihrer Organisation auf Dokumentbibliotheken zugreifen können (auch Liste der sicheren Empfänger genannt). Die Synchronisierungsbeziehung ist nicht zulässig, und der Computer des Benutzers ist für das Synchronisieren, Herunterladen oder Hochladen von Dateien der Dokumentbibliothek gesperrt. Informationen zu dieser Funktion finden Sie unter [Verwenden von Windows PowerShell-Cmdlets zum Aktivieren der OneDrive-Synchronisierung für Domänen, die in der Liste der sicheren Empfänger enthalten sind](/powershell/module/sharepoint-online/index).|
|UpdateSSOApplication|Die Zielanwendung wurde im Secure Store Service aktualisiert.|
|UserAddedToGroup|Der Websiteadministrator oder -besitzer fügt eine Person zu einer Gruppe auf einer SharePoint- oder OneDrive for Business-Website hinzu. Durch das Hinzufügen einer Person zu einer Gruppe werden dem Benutzer die Berechtigungen erteilt, die der Gruppe zugewiesen wurden. |
|UserRemovedFromGroup|Der Websiteadministrator oder -besitzer entfernt eine Person aus einer Gruppe auf einer SharePoint- oder OneDrive for Business-Website. Nachdem die Person entfernt wurde, werden ihr nicht mehr die Berechtigungen erteilt, die der Gruppe zugewiesen wurden. |
|WorkflowModified|Ein Benutzer erstellt, ändert oder löscht einen Enterprise-Projekttyp oder Workflowphasen oder Phasen in der Project Web App.|
|||||

## <a name="sharepoint-file-operations"></a>SharePoint-Dateivorgänge

Die dateibezogenen SharePoint-Ereignisse, die im Abschnitt "Datei- und Ordneraktivitäten" unter [Durchsuchen des Überwachungsprotokolls im Security & Compliance Center](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance) aufgelistet sind, verwenden dieses Schema.

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|SiteUrl|Edm.String|Ja|Die URL der Website, auf der sich die Datei oder der Ordner, auf die bzw. den der Benutzer zugegriffen hat, befindet.|
|SourceRelativeUrl|Edm.String|Nein|Die URL des Ordners, der die Datei enthält, auf die der Benutzer zugegriffen hat. Die Kombination der Werte für die Parameter _SiteURL_, _SourceRelativeURL_ und _SourceFileName_ ist identisch mit dem Wert für die Eigenschaft **ObjektID** und besteht aus dem vollständigen Pfadnamen der Datei, auf die der Benutzer zugegriffen hat.|
|SourceFileName|Edm.String|Ja|Der Name der Datei oder des Ordners, auf die der Benutzer zugegriffen hat.|
|SourceFileExtension|Edm.String|Nein|Die Erweiterung der Datei, auf die der Benutzer zugegriffen hat. Diese Eigenschaft ist leer, wenn das Objekt, auf das zugegriffen wurde, ein Ordner ist.|
|DestinationRelativeUrl|Edm.String|Nein|Die URL des Zielordners, in den eine Datei kopiert oder verschoben wurde. Die Kombination der Werte für die Parameter _SiteURL_, _DestinationRelativeURL_ und _DestinationFileName_ ist identisch mit dem Wert für die Eigenschaft **ObjektID** und besteht aus dem vollständigen Pfadnamen der kopierten Datei. Diese Eigenschaft wird nur bei Ereignissen "filecopied" und "filemoved" angezeigt.|
|DestinationFileName|Edm.String|Nein|Der Name der Datei, die kopiert oder verschoben wurde. Diese Eigenschaft wird nur bei Ereignissen "filecopied" und "filemoved" angezeigt.|
|DestinationFileExtension|Edm.String|Nein|Der Erweiterung der Datei, die kopiert oder verschoben wurde. Diese Eigenschaft wird nur bei Ereignissen "filecopied" und "filemoved" angezeigt.|
|UserSharedWith|Edm.String|Nein|Der Benutzer, für den eine Ressource freigegeben wurde.|
|SharingType|Edm.String|Nein|Der Typ der Freigabeberechtigungen, die dem Benutzer zugewiesen wurden, für den die Ressource freigegeben wurde. Dieser Benutzer wird anhand des Parameters _UserSharedWith_ identifiziert.|
|||||

## <a name="sharepoint-sharing-schema"></a>SharePoint-Freigabeschema

 Die auf die Freigabe der Datei bezogenen SharePoint-Ereignisse. Sie unterscheiden sich von den datei- und ordnerbezogenen Ereignissen dahingehend, dass ein Benutzer eine Aktion ausführt, die sich auf einen anderen Benutzer auswirkt. Informationen zum SharePoint-Freigabeschema finden Sie unter [Verwenden der Freigabeüberwachung im Office 365-Überwachungsprotokoll](/microsoft-365/compliance/use-sharing-auditing
).

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|TargetUserOrGroupName |Edm.String|Nein|Speichert die UPN oder den Namen des Zielbenutzers oder der Gruppe, für den bzw. die eine Ressource freigegeben wurde.|
|TargetUserOrGroupType|Edm.String|Nein|Gibt an, ob der Zielbenutzer oder die Gruppe ein Mitglied, ein Gast, eine Gruppe oder ein Partner ist. |
|EventData|XML-Code|Nein|Bietet nachträgliche Informationen zur stattgefundenen Freigabeaktion, wie z. B. das Hinzufügen eines Benutzers zu einer Gruppe oder das Erteilen von Bearbeitungsberechtigungen.|
|||||

## <a name="sharepoint-schema"></a>SharePoint-Schema

Die SharePoint-Ereignisse, die unter [Durchsuchen des Überwachungsprotokolls im Security & Compliance Center](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance) aufgelistet sind (mit Ausnahme der Datei- und Ordnerereignisse), verwenden dieses Schema.

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|CustomEvent|Edm.String|Nein|Optionale Zeichenfolge für benutzerdefinierte Ereignisse.|
|EventData|Edm.String|Nein|Optionale Nutzlast für benutzerdefinierte Ereignisse.|
|ModifiedProperties|Collection(ModifiedProperty)|Nein|Diese Eigenschaft wird für Administratorereignisse einbezogen, wie z. B. das Hinzufügen eines Benutzers als Mitglied einer Website oder der Administratorgruppe einer Websitesammlung. Die Eigenschaft enthält den Namen der Eigenschaft, die geändert wurde (wie z. B. die Websiteadministratorgruppe), den neuen Wert der geänderten Eigenschaft (wie z. B. den Benutzer, der als Websiteadministrator hinzugefügt wurde) und den vorherigen Wert des geänderten Objekts.|
|||||

## <a name="project-schema"></a>Projektschema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Entität|Edm.String|Ja| [ProjectEntity](#project-entity) für die die Überwachung vorgesehen war.|
|Aktion|Edm.String|Ja|[ProjectAction](#project-action), die durchgeführt wurde.|
|OnBehalfOfResId|Edm.Guid|Nein|Die Ressourcen-ID, für die die Aktion durchgeführt wurde.|
|||||

### <a name="enum-project-action---type-edmint32"></a>Enumeration: Project Action - Typ: Edm.Int32

#### <a name="project-action"></a>Projektaktion

|**Elementname**|**Beschreibung**|
|:-----|:-----|
|Akzeptiert|Ein Benutzer hat ein Ereignis oder einen Workflow akzeptiert.|
|Zugegriffen|Der Benutzer hat auf eine Entität zugegriffen.|
|Aktiviert|Der Benutzer hat eine Entität, ein Ereignis oder einen Workflow aktiviert.|
|Abgebrochen|Der Benutzer hat ein Ereignis oder einen Workflow abgebrochen.|
|Eingecheckt|Der Benutzer hat eine Entität eingecheckt.|
|Ausgecheckt|Der Benutzer hat eine Entität ausgecheckt.|
|Kopiert|Der Benutzer hat eine Entität kopiert.|
|Erstellt|Der Benutzer hat eine Entität erstellt.|
|Deaktiviert|Der Benutzer hat eine Entität deaktiviert.|
|Gelöscht|Der Benutzer hat eine Entität gelöscht.|
|Exportiert|Der Benutzer hat eine Entität exportiert.|
|ForceCheckedIn|Der Benutzer hat das Einchecken einer Entität erzwungen.|
|Geändert|Der Benutzer hat eine Entität geändert.|
|Veröffentlicht|Der Benutzer hat eine Entität veröffentlicht.|
|Unkenntlich gemacht|Der Benutzer hat eine Entität unkenntlich gemacht.|
|Abgelehnt |Der Benutzer hat eine Entität abgelehnt.|
|Neu gestartet|Ein Benutzer hat ein Ereignis oder einen Workflow neu gestartet.|
|Gespeichert|Der Benutzer hat eine Entität gespeichert.|
|Gesendet|Der Benutzer hat eine Entität gesendet.|
|Übermittelt|Der Benutzer hat eine Entität zur Überprüfung oder für den Workflow übermittelt.|
|||||

### <a name="enum-project-entity---type-edmint32"></a>Enumeration: Project Entity - Typ: Edm.Int32

#### <a name="project-entity"></a>Projektentität

|**Elementname**|**Beschreibung**|
|:-----|:-----|
|CustomField|Steht für ein benutzerdefiniertes Enterprise-Feld.|
|Driver|Steht für einen Portfolio-Treiber.|
|DriverPrioritization|Steht für eine Portfolio-Priorisierung.|
|Engagement|Steht für eine Ressourcenverhandlung.|
|EnterpriseCalendar|Steht für einen Enterprise-Ressourcenkalender.|
|EnterpriseProjectType|Steht für einen Enterprise-Projekttyp.|
|FiscalPeriod|Steht für einen Geschäftszeitraum.|
|GanttChartFormat|Steht für ein Gantt-Diagramm-Format.|
|GroupingFormat|Steht für ein Ansicht-Gruppierungsformat.|
|LineClassification|Steht für eine Arbeitszeittabelle-Zeilenklassifikation.|
|LookupTable|Steht für eine Enterprise-Nachschlagetabelle.|
|PermissionTemplate|Steht für eine Sicherheitsberechtigungsvorlage.|
|PortfolioAnalysis|Steht für einen Portfolio-Analyse.|
|Project|Steht für ein Projekt.|
|QueueJob|Steht für einen Auftrag in der Warteschlange.|
|QuickLaunch|Steht für ein Element der Schnellstartleiste.|
|Reporting|Steht für den Endpunkt des Berichtszeitraums.|
|Ressource|Steht für die Enterprise-Ressource.|
|ResourcePlan|Steht für einen mit dem Projekt verknüpften Ressourcenplan.|
|SecurityCategory|Steht für eine Sicherheitskategorie.|
|SecurityGroup|Steht für eine Sicherheitsgruppe.|
|Setting|Steht für eine Project Web App-Einstellung.|
|Statusing|Steht für ein Statusupdate.|
|StatusReport|Steht für einen Statusbericht.|
|TimeReportingPeriod|Steht für einen Zeitraum für eine Arbeitszeittabelle.|
|Timesheet|Steht für eine Arbeitszeittabellen-Entität.|
|TimesheetAuditLog|Steht für ein Arbeitszeittabellen-Überwachungsprotokoll.|
|TimesheetManager|Steht für den Verwalter einer Arbeitszeittabelle.|
|UserDelegate|Steht für die Benutzerdelegierung eines anderen Benutzers.|
|View|Steht für eine Ansichtsdefinition.|
|WorkflowPhase|Steht für eine Phase in einem Workflow.|
|WorkflowStage|Steht für einen Status in einem Workflow.|
|||||

## <a name="exchange-admin-schema"></a>Exchange-Verwaltungsschema

|**Parameter**|**Typ**|**Erforderlich**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|ModifiedObjectResolvedName|Edm.String|Nein|Der benutzerfreundliche Name des Objekts, das vom Cmdlet geändert wurde. Dies wird nur protokolliert, wenn das Cmdlet das Objekt ändert.|
|Parameter|Collection(Common.NameValuePair)|Nein|Der Name und Wert aller Parameter, die mit dem Cmdlet verwendet wurden, das in der Eigenschaft "Vorgänge" bezeichnet wurde.|
|ModifiedProperties|Collection(Common.ModifiedProperty)|Nein|Diese Eigenschaft wird für Administratorereignisse einbezogen. Die Eigenschaft enthält den Namen der Eigenschaft, die geändert wurde, den neuen Wert der geänderten Eigenschaft und den vorherigen Wert des geänderten Objekts.|
|ExternalAccess|Edm.Boolean|Ja|Gibt an, ob das Cmdlet von einem Benutzer Ihrer Organisation, von Mitarbeitern des Microsoft-Rechenzentrums, einem Rechenzentrum-Dienstkonto oder einem delegierten Administrator ausgeführt wurde. Der Wert **False** gibt an, dass das Cmdlet von einer Person in Ihrer Organisation ausgeführt wurde. Der Wert **True** gibt an, dass das Cmdlet von Mitarbeiter des Rechenzentrums, einem Rechenzentrum-Dienstkonto oder einem delegierten Administrator ausgeführt wurde.|
|OriginatingServer|Edm.String|Nein|Der Name des Servers, aus dem das Cmdlet ausgeführt wurde.|
|OrganizationName|Edm.String|Nein|Der Name des Mandanten.|
|||||

## <a name="exchange-mailbox-schema"></a>Exchange-Postfachschema

|**Parameter**|**Typ**|**Erforderlich**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|LogonType|Self.[LogonType](#logontype)|Nein| Gibt den Typ der Benutzers an, der auf das Postfach zugegriffen und die Operation, die protokolliert wurde, ausgeführt hat.|
|InternalLogonType|Self.[LogonType](#logontype)|Nein|Für die interne Verwendung reserviert.|
|MailboxGuid|Edm.String|Nein|Die Exchange-GUID des Postfachs, auf das zugegriffen wurde.|
|MailboxOwnerUPN|Edm.String|Nein|Die E-Mail-Adresse der Person, die das Postfach besitzt, auf das zugegriffen wurde.|
|MailboxOwnerSid|Edm.String|Nein|Die SID des Postfachbesitzers.|
|MailboxOwnerMasterAccountSid|Edm.String|Nein|Die Hauptkonto-SID des Postfachbesitzerkontos.|
|LogonUserSid|Edm.String|Nein|Die SID des Benutzers, der den Vorgang ausgeführt hat.|
|LogonUserDisplayName|Edm.String|Nein|Der benutzerfreundliche Name des Benutzers, der den Vorgang ausgeführt hat.|
|ExternalAccess|Edm.Boolean|Ja|Dies gilt, wenn die Domäne für die Anmeldung des Benutzers von der Domäne des Postfachbesitzers abweicht.|
|OriginatingServer |Edm.String|Nein|Dies ist der Ort, an dem der Vorgang begonnen wurde.|
|OrganizationName|Edm.String|Nein|Der Name des Mandanten.|
|ClientInfoString|Edm.String|Nein|Informationen zum E-Mail-Client, der zum Ausführen des Vorgangs verwendet wurde, z. B. eine Browserversion, eine Outlook-Version und Informationen zu mobilen Geräten.|
|ClientIPAddress|Edm.String|Nein|Die IP-Adresse des Geräts, das verwendet wurde, als der Vorgang protokolliert wurde. Die IP-Adresse wird im Adressformat IPv4 oder IPv6 angezeigt.|
|ClientMachineName|Edm.String|Nein|Der Name des Computers, auf dem der Outlook-Client gehostet wird.|
|ClientProcessName|Edm.String|Nein|Der für den Zugriff auf das Postfach verwendete E-Mail-Client. |
|ClientVersion|Edm.String|Nein|Die Version des E-Mail-Clients.|
|||||

### <a name="enum-logontype---type-edmint32"></a>Enumeration: LogonType - Typ: Edm.Int32

#### <a name="logontype"></a>LogonType

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|0|Besitzer|Der Postfachbesitzer.|
|1|Administrator|Eine Person mit Administratorberechtigungen für das Postfach einer Person.|
|2|Delegiert|Eine Person mit Stellvertretungsberechtigungen für das Postfach einer Person.|
|3|Transport|Ein Transportdienst im Microsoft-Rechenzentrum.|
|4|SystemService|Ein Dienstkonto im Microsoft-Rechenzentrum.|
|5|BestAccess|Für die interne Verwendung reserviert.|
|6|DelegatedAdmin|Ein delegierter Administrator.|
|||||

### <a name="exchangemailboxauditgrouprecord-schema"></a>ExchangeMailboxAuditGroupRecord schema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Ordner|Self.[ExchangeFolder](#exchangefolder-complex-type)|Nein|Ein Ordner, in dem sich eine Gruppe von Elementen befindet.|
|CrossMailboxOperations|Edm.Boolean|Nein|Gibt an, ob der Vorgang mehr als ein Postfach umfasst.|
|DestMailboxId|Edm.Guid|Nein|Legen Sie dies nur fest, wenn der Parameter CrossMailboxOperations **True** ist. Gibt die GUID des Zielpostfachs an.|
|DestMailboxOwnerUPN|Edm.String|Nein|Legen Sie dies nur fest, wenn der Parameter CrossMailboxOperations **True** ist. Gibt die UPN des Besitzers des Zielpostfachs an.|
|DestMailboxOwnerSid|Edm.String|Nein|Legen Sie dies nur fest, wenn der Parameter CrossMailboxOperations **True** ist. Gibt die SID des Zielpostfachs an.|
|DestMailboxOwnerMasterAccountSid|Edm.String|Nein|Legen Sie dies nur fest, wenn der Parameter CrossMailboxOperations **True** ist. Gibt die SID für die Hauptkonto-SID des Besitzers des Zielpostfachs an.|
|DestFolder|Self.[ExchangeFolder](#exchangefolder-complex-type)|Nein|Der Zielordner für Vorgänge wie Verschieben.|
|Ordner|Collection(Self.[ExchangeFolder](#exchangefolder-complex-type))|Nein|Informationen zu den an einem Vorgang beteiligten Quellordnern; wenn z. B. Ordner ausgewählt und dann gelöscht werden.|
|AffectedItems|Collection(Self.[ExchangeItem](#exchangeitem-complex-type))|Nein|Informationen zu jedem Element in der Gruppe.|
|||||

### <a name="exchangemailboxauditrecord-schema"></a>ExchangeMailboxAuditRecord schema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Element|Self.[ExchangeItem](#exchangeitem-complex-type)|Nein|Steht für das Element, für das der Vorgang ausgeführt wurde.|
|ModifiedProperties|Collection(Edm.String)|Nein|Noch nicht festgelegt|
|SendAsUserSmtp|Edm.String|Nein|Die SMTP-Adresse des Benutzers, der imitiert wird.|
|SendAsUserMailboxGuid|Edm.Guid|Nein|Die Exchange-GUID des Postfachs, auf das zum Senden von E-Mails zugegriffen wurde.|
|SendOnBehalfOfUserSmtp|Edm.String|Nein|Die SMTP-Adresse des Benutzers, in dessen Auftrag die E-Mail gesendet wird.|
|SendOnBehalfOfUserMailboxGuid|Edm.Guid|Nein|Die Exchange-GUID des Postfachs, auf das zugegriffen wurde, um die E-Mail im Auftrag zu versenden.|
|||||

### <a name="exchangeitem-complex-type"></a>Komplexer ExchangeItem-Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Id|Edm.String|Ja|Die Store-ID.|
|Betreff|Edm.String|Nein|Die Betreffzeile der Nachricht, auf die zugegriffen wurde.|
|ParentFolder|Edm.ExchangeFolder|Nein|Der Name des Ordners, in dem sich das Element befindet.|
|Anlagen|Edm.String|Nein|Eine Liste mit den Namen und der Dateigröße aller Elemente, die an die Nachricht angefügt werden.|
|||||

### <a name="exchangefolder-complex-type"></a>ExchangeFolder complex type

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Id|Edm.String|Ja|Die Store-ID des Ordnerobjekts.|
|Pfad|Edm.String|Nein|Der Name des Postfachordners, in dem sich die Nachricht, auf die zugegriffen wurde, befindet.|
|||||

## <a name="azure-active-directory-base-schema"></a>Azure Active Directory-Basisschema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|AzureActiveDirectoryEventType|Self.[AzureActiveDirectoryEventType](#azureactivedirectoryeventtype)|Ja|Der Typ des Azure AD-Ereignisses. |
|ExtendedProperties|Collection(Common.NameValuePair)|Nein|Die erweiterten Eigenschaften des Azure AD-Ereignisses.|
|ModifiedProperties|Collection(Common.ModifiedProperty)|Nein|Diese Eigenschaft wird für Administratorereignisse einbezogen. Die Eigenschaft enthält den Namen der Eigenschaft, die geändert wurde, den neuen Wert der geänderten Eigenschaft und den vorherigen Wert.|
|||||

### <a name="enum-azureactivedirectoryeventtype---type--edmint32"></a>Enumeration: AzureActiveDirectoryEventType - Typ -Edm.Int32

#### <a name="azureactivedirectoryeventtype"></a>AzureActiveDirectoryEventType

|**Elementname**|**Beschreibung**|
|:-----|:-----|
|AccountLogon|Das Kontoanmeldeereignis.|
|AzureApplicationAuditEvent|Das Sicherheitsereignis der Azure-Anwendung.|
|||||

## <a name="azure-active-directory-account-logon-schema"></a>Azure Active Directory-Kontoanmeldeschema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Anwendung|Edm.String|Nein|Die Anwendung, die das Kontoanmeldeereignis auslöst, z. B. Office 15.|
|Client|Edm.String|Nein|Details zum Clientgerät, dem Gerätebetriebssystem und dem Gerätebrowser, die für das Kontoanmeldeereignis verwendet wurden.|
|LoginStatus|Edm.Int32|Ja|Diese Eigenschaft wird direkt aus OrgIdLogon.LoginStatus übertragen. Die Zuordnung verschiedener interessanter Anmeldefehler kann durch Warnalgorithmen erfolgen.|
|UserDomain|Edm.String|Ja|Die Mandanten-Identitätsinformationen (TII).|
|||||

### <a name="enum-credentialtype---type-edmint32"></a>Enumeration: CredentialType - Typ: Edm.Int32

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|-1|Andere|Weitere Authentifizierung.|
|0|Kennwort|Die Anmeldung erfolgt über einen Benutzernamen und ein Kennwort.|
|1|MobilePhone|Die Anmeldung erfolgt über ein Mobiltelefon.|
|2|SecretQuestion|Die Anmeldung erfolgt über eine geheime Frage.|
|3|SecurePin|Die Anmeldung erfolgt über eine sichere PIN.|
|4|SecurePinReset|Die Anmeldung erfolgt über das Zurücksetzen einer sicheren PIN.|
|11|EasyID|Die Benutzeranmeldeinformationen bestehen aus einer EasyID.|
|14|PasswordIndexCredentialType|Die Anmeldung erfolgt über PasswordIndexCredentialType.|
|16|Gerät|Die Anmeldung erfolgt über ein Gerät.|
|17|ForeignRealmIndex|Die Anmeldung erfolgt über ForeignRealmIndex.|
|||||

### <a name="enum-logintype---type-edmint32"></a>Enumeration: LoginType - Typ: Edm.Int32

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|-1|Andere|Ein anderer i-Typ.|
|1|InitialAuth|Anmeldung mit anfänglicher Authentifizierung.|
|2|CookieCopy|Anmeldung mit Cookie.|
|3|SilentReAuth|Anmeldung mit automatischer erneuter Authentifizierung.|
|||||

### <a name="enum-authenticationmethod---type-edmint32"></a>Enumeration: AuthenticationMethod - Typ: Edm.Int32

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|0|Min|Die Authentifizierung erfolgt über eine Min.|
|1|Kennwort|Die Authentifizierung erfolgt über ein Kennwort.|
|2|Digest|Die Authentifizierung erfolgt über einen Digest.|
|3|ProxyAuth|Die Authentifizierung erfolgt über ProxyAuth.|
|4|InfoCard|Die Authentifizierung erfolgt über InfoCard.|
|5|DAToken|Die Authentifizierung erfolgt über ein DAToken.|
|6|Sha1RememberMyPassword|Die Authentifizierung erfolgt über Sha1RememberMyPassword.|
|7|LMPasswordHash|Die Authentifizierung erfolgt über LMPasswordHash.|
|8|ADFSFederatedToken|Die Authentifizierung erfolgt über ADFSFederatedToken.|
|9|EID|Die Authentifizierung erfolgt über EID.|
|10|DeviceID|Die Authentifizierung erfolgt über DeviceID. |
|11|MD5|Die Authentifizierung erfolgt über MD5.|
|12|EncProxyPasswordHash|Die Authentifizierung erfolgt über EncProxyPasswordHash.|
|13|LWAFederation|Die Authentifizierung erfolgt über LWAFederation.|
|14|Sha1HashedPassword|Die Authentifizierung erfolgt über Sha1HashedPassword.|
|15|SecurePin|Die Authentifizierung erfolgt über eine sichere Pin.|
|16|SecurePinReset|Die Authentifizierung erfolgt über das Zurücksetzen einer sicheren Pin.|
|17|SAML20PostSimpleSign|Die Authentifizierung erfolgt über SAML20PostSimpleSign.|
|18|SAML20Post|Die Authentifizierung erfolgt über SAML20Post.|
|19|OneTimeCode|Die Authentifizierung erfolgt über einen einmalig verwendbaren Code.|
|||||

## <a name="azure-active-directory-schema"></a>Azure Active Directory-Schema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Akteur|Collection(Self.[IdentityTypeValuePair](#complex-type-identitytypevaluepair))|Nein|Der Benutzer oder Dienstprinzipal, der die Aktion ausgeführt hat.|
|ActorContextId|Edm.String|Nein|Die GUID der Organisation, der der Akteur gehört.|
|ActorIpAddress|Edm.String|Nein|Die IP-Adresse des Akteurs im IPV4- oder IPV6-Adressformat.|
|InterSystemsId|Edm.String|Nein|Die GUID, die die Aktionen in Komponenten innerhalb des Office 365-Dienstes nachverfolgt.|
|IntraSystemsId|Edm.String|Nein|Die GUID, die vom Azure Active Directory zum Nachverfolgen der Aktion generiert wird.|
|SupportTicketId|Edm.String|Nein|Die Kundensupport-Ticket-ID für die Aktion in "Aktionen im Auftrag von"-Situationen.|
|Ziel|Collection(Self.[IdentityTypeValuePair](#complex-type-identitytypevaluepair))|Nein|Der Benutzer, beim dem die Aktion (identifiziert durch die Eigenschaft Vorgang) ausgeführt wurde.|
|TargetContextId|Edm.String|Nein|Die GUID der Organisation, der der Zielbenutzer angehört.|
|||||

### <a name="complex-type-identitytypevaluepair"></a>Complex Type IdentityTypeValuePair

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|ID|Edm.String|Ja|Der Wert der angegebenen Identität.|
|Typ|Self.IdentityType|Ja|Der Typ der Identität.|
|||||

### <a name="enum-identitytype---type-edmint32"></a>Enumeration: IdentityType - Typ: Edm.Int32

#### <a name="identitytype"></a>IdentityType

|**Elementname**|**Beschreibung**|
|:-----|:-----|
|Anspruch|Die Identität ist ein Anspruch zum Zweck der Autorisierung.|
|Name|Der Anzeigename des Akteurs des Überwachungsprotokolls oder der Zielidentität.|
|Andere|Die Identität des Akteurs ist vom Typ Andere, wie z. B. die Objekt-ID, die vom Office 365-Dienst generiert wird.|
|PUID|Der Akteur der Überwachungsaktion oder die Ziel-Passport Unique ID (PUID).|
|SPN|Die Identität eines Dienstprinzipals, wenn die Aktion vom Office 365-Dienst ausgeführt wird.|
|UPN|Der Benutzerprinzipalname.|
|||||

## <a name="azure-active-directory-secure-token-service-sts-logon-schema"></a>Azure Active Directory-Secure Token Service (STS)-Anmeldeschema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|ApplicationId|Edm.String|Nein|Die GUID, die die Anwendung darstellt, von der die Anmeldung angefordert wird. Der Anzeigename kann über die Azure Active Directory Graph-API betrachtet werden.|
|Client|Edm.String|Nein|Client-Geräteinformationen, die von dem Browser bereitgestellt werden, der die Anmeldung ausführt.|
|DeviceProperties|Collection(Common.NameValuePair)|Nein|Diese Eigenschaft enthält verschiedene Gerätedetails, darunter ID, Anzeigename, Betriebssystem, Browser, IsCompliant, IsCompliantAndManaged, SessionId und DeviceTrustType. Die DeliverableType-Eigenschaft kann die folgenden Werte aufweisen:<br/><br/>**0** – in Azure AD registriert<br/> **1** – in Azure AD eingebunden<br/> **2** – hybrid, in Azure AD eingebunden|
|ErrorCode|Edm.String|Nein|Für fehlgeschlagene Anmeldungen (bei denen der Wert für die Operation-Eigenschaft "UserLoginFailed" lautet) enthält diese Eigenschaft den Azure Active Directory STS (AADSTS)-Fehlercode. Beschreibungen dieser Fehlercodes finden Sie unter [Authentifizierungs- und Autorisierungsfehlercodes](/azure/active-directory/develop/reference-aadsts-error-codes#aadsts-error-codes). Der Wert `0` zeigt eine erfolgreiche Anmeldung an.|
|LogonError|Edm.String|Nein|Bei fehlgeschlagenen Anmeldungen enthält diese Eigenschaft eine benutzerlesbare Beschreibung des Grunds für den Anmeldefehler.|
|||||

## <a name="dlp-schema"></a>DLP-Schema

DLP-Ereignisse stehen für Exchange Online, SharePoint Online und OneDrive For Business zur Verfügung. Beachten Sie, dass DLP-Ereignisse in Exchange nur für Ereignisse basierend auf einer einheitlichen DLP-Richtlinie (z. B. über das Security & Compliance Center konfiguriert) verfügbar sind. Auf Exchange-Transportregeln basierende DLP-Ereignisse werden nicht unterstützt.

DLP-Ereignisse (Data Loss Prevention, Verhinderung von Datenverlust) enthalten immer UserKey = "DlpAgent" im allgemeinen Schema. Es gibt drei Arten von DlpEvents, die als Wert für die Operation-Eigenschaft des allgemeinen Schemas gespeichert sind:

- DlpRuleMatch: Zeigt an, dass eine Regel abgeglichen wurde. Diese Ereignisse sind in Exchange, SharePoint Online und OneDrive for Business vorhanden. In Exchange enthalten sie falsch positive Ergebnisse und Informationen zur Außerkraftsetzung. In SharePoint Online und OneDrive for Business generieren falsch positive Ergebnisse und Außerkraftsetzungen separate Ereignisse.

- DlpRuleUndo: Nur in SharePoint Online und OneDrive for Business vorhanden. Gibt an, dass eine zuvor angewendete Richtlinienaktion "rückgängig" gemacht wurde – entweder aufgrund einer Identifizierung falsch positiver Ergebnisse/Außerkraftsetzung durch den Benutzer oder weil das Dokument nicht mehr der Richtlinie unterliegt (entweder aufgrund einer Richtlinienänderung oder einer Änderung des Dokumentinhalts).

- DlpInfo: Nur in SharePoint Online und OneDrive for Business vorhanden. Gibt an, dass falsch positive Ergebnisse identifiziert wurden, aber keine Aktion "Rückgängig" durchgeführt wurde.

|**Parameter**|**Typ**|**Erforderlich**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|SharePointMetaData|Self.[SharePointMetadata](#sharepointmetadata-complex-type)|Nein|Beschreibt Metadaten über das Dokument in SharePoint oder OneDrive for Business, die vertrauliche Informationen enthalten.|
|ExchangeMetaData|Self.[ExchangeMetadata](#exchangemetadata-complex-type)|Nein|Beschreibt Metadaten über die E-Mail-Nachricht, die vertrauliche Informationen enthalten.|
|ExceptionInfo|Edm.String|Nein|Gibt Gründe an, warum eine Richtlinie nicht mehr anwendbar ist und/oder enthält vom Endbenutzer vermerkte Informationen zu falsch positiven Ergebnissen und/oder zur Außerkraftsetzung.|
|PolicyDetails|Sammlung (Self.[ PolicyDetails](#policydetails-complex-type))|Ja|Informationen zu 1 oder mehreren Richtlinien, die das DLP-Ereignis ausgelöst haben.|
|SensitiveInfoDetectionIsIncluded|Boolesch|Ja|Gibt an, ob das Ereignis den Wert des vertraulichen Datentyps und umgebende Kontextinformationen aus dem Quellinhalt enthält. Für den Zugriff auf vertrauliche Daten wird die Berechtigung "Lesen von DLP-Richtlinienereignissen einschließlich vertraulicher Informationen" in Azure Active Directory benötigt.|
|||||

### <a name="sharepointmetadata-complex-type"></a>Komplexer SharePointMetadata-Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Von|Edm.String|Ja|Der Benutzer, der das Ereignis ausgelöst hat. Dies ist entweder der FileOwner, LastModifier oder LastSharer.|
|itemCreationTime|Edm.Date|Ja|Datumzeitstempel in UTC, wann das Ereignis protokolliert wurde.|
|SiteCollectionGuid|Edm.Guid|Ja|Die GUID der Websitesammlung.|
|SiteCollectionUrl|Edm.String|Ja|Die URL der SharePoint-Website.|
|FileName|Edm.String|Ja|Der Name der Pfads.|
|FileOwner|Edm.String|Ja|Der Besitzer des Dokuments.|
|FilePathUrl|Edm.String|Ja|Die URL des Dokuments.|
|DocumentLastModifier|Edm.String|Ja|Der Benutzer, der das Dokument zuletzt geändert hat.|
|DocumentSharer|Edm.String|Ja|Der Benutzer, der das Dokument zuletzt freigegeben hat.|
|UniqueId|Edm.String|Ja|Eine GUID, die die Datei identifiziert.|
|LastModifiedTime|Edm.DateTime|Ja|Zeitstempel in UTC, wann das Dokument zuletzt geändert wurde.|
|IsViewableByExternalUsers|Edm.Boolean|Ja|Bestimmt, ob ein externer Benutzer auf die Datei zugreifen kann.|
|||||

### <a name="exchangemetadata-complex-type"></a>Komplexer ExchangeMetadata-Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|MessageID|Edm.String|Ja|Die Nachrichten-ID der E-Mail, die das Ereignis ausgelöst hat.|
|Von|Edm.String|Ja|Der Benutzer, der die E-Mail-Adresse gesendet hat.|
|An|Collection(Edm.String)|Nein|Eine Sammlung von E-Mail-Adressen, die in der An-Zeile der Nachricht enthalten waren.|
|CC|Collection(Edm.String)|Nein|Eine Sammlung von E-Mail-Adressen, die in der CC-Zeile der Nachricht enthalten waren.|
|BCC|Collection(Edm.String)|Nein|Eine Sammlung von E-Mail-Adressen, die in der BCC-Zeile der Nachricht enthalten waren.|
|Betreff|Edm.String|Ja|Der Betreff der E-Mail-Nachricht.|
|Gesendet|Edm.DateTime|Ja|Die Uhrzeit in UTC, wann die E-Mail gesendet wurde.|
|RecipientCount|Edm.Int32|Ja|Die Gesamtzahl aller Empfänger in den Zeilen An, CC und BCC der Nachricht.|
|||||

### <a name="policydetails-complex-type"></a>Komplexer PolicyDetails-Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|PolicyId|Edm.Guid|Ja|Die Guid der DLP-Richtlinie für dieses Ereignis.|
|PolicyName|Edm.String|Ja|Die Anzeigename der DLP-Richtlinie für dieses Ereignis.|
|Regeln|Sammlung (Self.[Rules](#rules-complex-type))|Ja|Informationen zu den Regeln in der Richtlinie, die für dieses Ereignis abgeglichen wurden.|
|||||

### <a name="rules-complex-type"></a>Komplexer Rules-Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|RuleId|Edm.Guid|Ja|Die Guid der DLP-Richtlinie für dieses Ereignis.|
|RuleName|Edm.String|Ja|Der Anzeigename der DLP-Richtlinie für dieses Ereignis.|
|Aktionen|Collection(Edm.String)|Nein|Eine Liste der Aktionen, die als Ergebnis eines RuleMatch DLP-Ereignisses durchgeführt wurden.|
|OverriddenActions|Collection(Edm.String)|Nein|Eine Liste der zuvor ausgeführten Aktionen, die jetzt aufgrund eines DLPRuleUndo-Ereignisses rückgängig gemacht wurden. |
|Severity|Edm.String|Nein|Der Schweregrad (Niedrig, Mittel und Hoch) der Regelentsprechung.|
|RuleMode|Edm.String|Ja|Gibt an, ob die DLP-Regel auf Erzwingen, Überwachen mit Benachrichtigen oder Nur Überwachen festgelegt wurde.|
|ConditionsMatched|Self.[ConditionsMatched](#conditionsmatched-complex-type)|Nein|Details, welche Bedingungen der Regel für dieses Ereignis erfüllt wurden.|
|||||

### <a name="conditionsmatched-complex-type"></a>Komplexer ConditionsMatched-Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|SensitiveInformation|Sammlung (Self.[ SensitiveInformation](#sensitiveinformation-complex-type))|Nein|Informationen über die Art der erkannten vertraulichen Informationen.|
|DocumentProperties|Collection(NameValuePair)|Nein|Informationen zu Dokumenteigenschaften, die eine Regelentsprechung ausgelöst haben.|
|OtherConditions|Collection(NameValuePair)|Nein|Eine Liste der Schlüssel-Wert-Paare zur Beschreibung beliebiger anderer Kriterien, die erfüllt wurden.|
|||||

### <a name="sensitiveinformation-complex-type"></a>Komplexer SensitiveInformation-Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Confidence|Edm.Int|Ja|Die aggregierte Konfidenz aller Musterübereinstimmungen für den Typ vertraulicher Informationen.|
|Anzahl|Edm.Int|Ja|Gesamtanzahl der erkannten vertraulichen Instanzen.|
|Speicherort|Edm.String|Nein||
|SensitiveType|Edm.Guid|Ja|Eine Guid, die den Typ der erkannten vertraulichen Daten bezeichnet.|
|SensitiveInformationDetections|Self.SensitiveInformationDetections|Nein|Ein Array von Objekten, das vertrauliche Informationsdaten und die folgenden Details enthält: übereinstimmender Wert und Kontext des übereinstimmenden Werts.|
|SensitiveInformationDetailedClassificationAttributes|Collection(SensitiveInformationDetailedConfidenceLevelResult)|Ja|Informationen über die Anzahl der erkannten Typen vertraulicher Informationen für jedes der drei Konfidenzniveaus (Hoch, Mittel und Niedrig) und ob sie der DLP-Regel entsprechen oder nicht|
|SensitiveInformationTypeName|Edm.String|Nein|Name des Typs vertraulicher Informationen.|
|UniqueCount|Edm.Int32|Ja|Anzahl der verschiedenen erkannten vertraulichen Instanzen.|
|||||

### <a name="sensitiveinformationdetailedclassificationattributes-complex-type"></a>Komplexer Typ „SensitiveInformationDetailedClassificationAttributes“

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Confidence|Edm.int32|Ja|Das Konfidenzniveau des erkannten Musters wurde erkannt.|
|Anzahl|Edm.Int32|Ja|Die Anzahl der erkannten vertraulichen Instanzen für ein bestimmtes Konfidenzniveau.|
|IsMatch|Edm.Boolean|Ja|Zeigt an, ob die angegebene Anzahl und das Konfidenzniveau des Typs vertraulicher Informationen zu einer Übereinstimmung mit einer DLP-Regel führt.|
|||||

### <a name="sensitiveinformationdetections-complex-type"></a>Komplexer SensitiveInformationDetections-Typ

Vertrauliche DLP-Daten sind nur in der Aktivitätsfeed-API für Benutzer verfügbar, denen die Berechtigung "Lesen vertraulicher DLP-Daten" erteilt wurde.

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|DetectedValues|Collection(Common.NameValuePair)|Ja|Ein Array vertraulicher Informationen, die erkannt wurden. Die Informationen enthalten Schlüssel-Wert-Paare mit Wert = übereinstimmenden Wert (z. B. Wert der Kreditkarte) und Kontext = ein Auszug aus der Inhaltsquelle, der den erkannten Wert enthält. |
|ResultsTruncated|Edm.Boolean|Ja|Zeigt an, ob die Protokolle aufgrund einer großen Anzahl von Ergebnissen abgeschnitten wurden. |
|||||

### <a name="exceptioninfo-complex-type"></a>Komplexer ExceptionInfo-Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Grund|Edm.String|Nein|Bei einem DLPRuleUndo-Ereignis gibt dies an, warum die Regel nicht mehr gilt, was einer der Gründe 3 sein kann: Außerkraftsetzung, Dokumentänderung oder Änderung der Sicherheitsrichtlinie.|
|FalsePositive|Edm.Boolean|Nein|Gibt an, ob der Benutzer dieses Ereignis als falsch positives Ergebnis festgelegt hat.|
|Begründung|Edm.String|Nein|Wenn sich der Benutzer entscheidet, die Richtlinie außer Kraft zu setzen, werden alle Begründungen des Benutzers hier erfasst.|
|Regeln|Collection(EDM.GUID)|Nein|Eine Auflistung von Guids für jede Regel, die als falsch positives Ergebnis oder Außerkraftsetzung eingestuft wurde oder für die eine Aktion rückgängig gemacht wurde.|
|||||

## <a name="security-and-compliance-center-schema"></a>Security & Compliance Center-Schema

|**Parameter**|**Typ**|**Erforderlich**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|StartTime|Edm.Date|Nein|Datum und Uhrzeit der Ausführung des Cmdlets.|
|ClientRequestId|Edm.String|Nein|Eine GUID, die zum Korrelieren dieses Cmdlets mit den Security & Compliance Center-UX-Vorgängen verwendet werden kann. Diese Informationen werden nur vom Microsoft-Support verwendet.|
|CmdletVersion|Edm.String|Nein|Die Buildversion des Cmdlets, als es ausgeführt wurde.|
|EffectiveOrganization|Edm.String|Nein|Die GUID für die vom Cmdlet betroffene Organisation. (Veraltet: Dieser Parameter wird in der Zukunft nicht mehr angezeigt.)|
|UserServicePlan|Edm.String|Nein|Der Exchange Online Protection-Serviceplan, der dem Benutzer, der das Cmdlet ausgeführt hat, zugewiesen wurde.|
|ClientApplication|Edm.String|Nein|Wenn das Cmdlet von einer Anwendung und nicht von einer PowerShell-Remoteinstanz ausgeführt wurde, enthält dieses Feld den Namen der Anwendung.|
|Parameter|Edm.String|Nein|Der Name und der Wert für Parameter, die mit dem Cmdlet verwendet wurden und keine personenbezogenen Informationen enthalten.|
|NonPiiParameters|Edm.String|Nein|Der Name und der Wert für Parameter, die mit dem Cmdlet verwendet wurden und personenbezogene Informationen enthalten. (Veraltet: Dieses Feld wird in der Zukunft nicht mehr angezeigt, und der Inhalt wird mit dem Feld "Parameter" zusammengeführt.)|
|||||

## <a name="security-and-compliance-alerts-schema"></a>Security &Compliance-Warnung-Schema

Warnsignale umfassen:

- Alle Warnungen, die basierend auf [Warnungsrichtlinien im Security & Compliance Center](/office365/securitycompliance/alert-policies#default-alert-policies) generierten wurden.
- Auf Office 365 bezogene Warnungen, die in [Office 365 Cloud App Security](/office365/securitycompliance/office-365-cas-overview) und [Microsoft Cloud App Security](/cloud-app-security/what-is-cloud-app-security) generiert wurden.

Die Benutzer-ID und der UserKey für diese Ereignisse sind immer SecurityComplianceAlerts. Es gibt drei Arten von Warnereignissen, die als Wert für die Operation-Eigenschaft des allgemeinen Schemas gespeichert sind:

- AlertTriggered: Eine neue Warnung wird aufgrund einer Richtlinienenübereinstimmung generiert.

- AlertEntityGenerated: Eine neue Entität wird zu einer Warnung hinzugefügt. Dieses Ereignis ist nur für Warnungen anwendbar, die basierend auf Warnungsrichtlinien im Security & Compliance Center generiert wurden. Jede generierte Warnung kann einem oder mehreren dieser Ereignisse zugeordnet werden. Beispielsweise ist eine Richtlinie so definiert, dass eine Warnung ausgelöst wird, wenn ein beliebiger Benutzer mehr als 100 Dateien in 5 Minuten löscht. Wenn zwei Benutzer in etwa der gleichen Zeit den Schwellenwert überschreiten, gibt es zwei AlertEntityGenerated-Ereignisse, aber nur ein AlertTriggered-Ereignis.

- AlertUpdated: Eine Aktualisierung der Metadaten eine Warnung wurde vorgenommen. Dieses Ereignis wird protokolliert, wenn der Status einer Warnung geändert wird (z. B. von "Aktiv" zu "Gelöst") und wenn jemand einen Kommentar zu der Warnung hinzufügt.

|**Parameter**|**Typ**|**Erforderlich**|**Description**|
|:-----|:-----|:-----|:-----|
|AlertId|Edm.Guid|Ja|Die GUID der Warnung.|
|AlertType|Self.String|Ja|Die Art der Warnung. Zu den Warnungstypen gehören: <ul><li>System</li><li>Benutzerdefiniert|
|Name|Edm.String|Ja|Der Name der Warnung.|
|PolicyId|Edm.Guid|Nein|Die GUID der Richtlinie, die die Warnung ausgelöst hat.|
|Status|Edm.String|Nein|Der Status der Warnung. Zu den Statuswerten gehören: <ul><li><p>Aktiv</li><li>Wird untersucht</li><li>Gelöst</li><li>Geschlossen|
|Severity|Edm.String|Nein|Der Schweregrad der Warnung. Zu den Schweregraden gehören: <ul><li>Niedrig</li><li>Mittel</li><li>Hoch</li></ul>|
|Kategorie|Edm.String|Nein|Die Kategorie der Warnung. Zu den Kategorien gehören: <ul><li>AccessGovernance</li><li>DataGovernance</li><li>DataLossPrevention</li><li>InsiderRiskManagement</li><li>MailFlow</li><li>ThreatManagement</li><li>Andere|
|Quelle|Edm.String|Nein|Die Quelle der Warnung. Zu den Quellen gehören: <ul><li>Office 365 Security & Compliance</li><li>Cloud-App-Sicherheit|
|Kommentare|Edm.String|Nein|Kommentare von Benutzer, die die Warnung angezeigt haben. Standardmäßig "Neue Warnung"|
|Daten|Edm.String|Nein|Der detaillierte Datenblob der Warnung oder Warnungsentität.|
|AlertEntityId|Edm.String|Nein|Die ID für die Warnungsentität. Dieser Parameter ist nur für AlertEntityGenerated-Ereignisse anwendbar.|
|EntityType|Edm.String|Nein|Typ der Warnung oder Warnungsentität. Die Entitätstypen umfassen: <ul><li>Benutzer</li><li>Empfänger</li><li>Absender</li><li>MalwareFamily</li></ul>Dieser Parameter ist nur für AlertEntityGenerated-Ereignisse anwendbar.|
|||||

## <a name="yammer-schema"></a>Yammer-Schema

Die unter [Durchsuchen des Überwachungsprotokolls im Security & Compliance Center](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#yammer-activities) aufgelisteten Yammer-Ereignisse verwenden dieses Schema.

|**Parameter**|**Typ**|**Erforderlich**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|ActorUserId|Edm.String|Nein|Die E-Mail-Adresse des Benutzers, der den Vorgang ausgeführt hat.|
|ActorYammerUserId|Edm.Int64|Nein|Die ID des Benutzers, der den Vorgang ausgeführt hat.|
|DataExportType|Edm.String|Nein|Gibt "Daten" zurück, wenn der Datenexport Nachrichten, Notizen, Dateien, Themen, Benutzer und Gruppen enthält; gibt "Benutzer" zurück, wenn der Datenexport nur Benutzer enthält.|
|FileId|Edm.Int64|Nein|Die ID der Datei innerhalb des Vorgangs. |
|FileName|Edm.String|Nein|Der Name der Datei innerhalb des Vorgangs. Ist leer, falls nicht relevant für den Vorgang.|
|GroupName|Edm.String|Nein|Der Name der Gruppe innerhalb des Vorgangs. Ist leer, falls nicht relevant für den Vorgang.|
|IsSoftDelete|Edm.Boolean|Nein|Gibt „true“ zurück, wenn die Datenaufbewahrungsrichtlinie des Netzwerks auf „Vorläufiges Löschen“ festgelegt ist; gibt „false“ zurück, wenn die Datenaufbewahrungsrichtlinie des Netzwerks auf „Endgültiges Löschen“ festgelegt ist.|
|MessageId|Edm.Int64|Nein|Die ID der Nachricht innerhalb des Vorgangs.|
|YammerNetworkId|Edm.Int64|Nein|Die Netzwerk-ID des Benutzers, der den Vorgang ausgeführt hat.|
|TargetUserId|Edm.String|Nein|Die E-Mail-Adresse des Zielbenutzers innerhalb des Vorgangs. Ist leer, falls nicht relevant für den Vorgang.|
|TargetYammerUserId|Edm.Int64|Nein|Die ID des Zielbenutzers innerhalb des Vorgangs.|
|VersionId|Edm.Int64|Nein|Die Versions-ID der Datei innerhalb des Vorgangs.|
|||||

## <a name="data-center-security-base-schema"></a>Rechenzentrum-Sicherheitsbasis-Schema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|DataCenterSecurityEventType|Self.[DataCenterSecurityEventType](#datacentersecurityeventtype)|Ja|Der Typ des Cmdlet-Ereignisses im Feld "Sperren".|
|||||

### <a name="enum-datacentersecurityeventtype---type-edmint32"></a>Enumeration: DataCenterSecurityEventType - Typ: Edm.Int32

#### <a name="datacentersecurityeventtype"></a>DataCenterSecurityEventType

|**Elementname**|**Beschreibung**|
|:-----|:-----|
|DataCenterSecurityCmdletAuditEvent|Dies ist der Enumerationswert für das Cmdlet-Überwachungstyp-Ereignis.|
|||

## <a name="data-center-security-cmdlet-schema"></a>Rechenzentrum-Sicherheits-Cmdlet-Schema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|StartTime|Edm.Date|Ja|Die Startzeit der Ausführung des Cmdlets.|
|EffectiveOrganization|Edm.String|Ja|Der Name des Mandanten, auf den die Erweiterung/das Cmdlet ausgelegt wurde.|
|ElevationTime|Edm.Date|Ja|Die Startzeit der Erweiterung.|
|ElevationApprover|Edm.String|Ja|Der Name eines Microsoft-Managers.|
|ElevationApprovedTime|Edm.Date|Nein|Der Zeitstempel, wann die Erweiterung genehmigt wurde.|
|ElevationRequestId|Edm.Guid|Ja|Ein eindeutiger Bezeichner für die Erweiterungsanforderung.|
|ElevationRole|Edm.String|Nein|Die Rolle, für die die Erweiterung angefordert wurde.|
|ElevationDuration|Edm.Int32|Ja|Die Dauer, in der die Erweiterung aktiv war.|
|GenericInfo|Edm.String|Nein|Kommentare und andere generische Informationen.|
|||||

## <a name="microsoft-teams-schema"></a>Microsoft Teams-Schema

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|AddOnGuid|Edm.Guid|Nein|Der eindeutige Bezeichner des Add-Ons, das das Ereignis generiert hat.|
|AddOnName|Edm.String|Nein|Der Name des Add-Ons, das das Ereignis generiert hat.|
|AddOnType|Self.[AddOnType](#addontype)|Nein|Der Typ des Add-Ons, das dieses Ereignis generiert hat.|
|ChannelGuid|Edm.Guid|Nein|Ein eindeutiger Bezeichner für den überwachten Kanal.|
|ChannelName|Edm.String|Nein|Der Name des überwachten Kanals.|
|ChannelType|Edm.String|Nein|Der Typ des zu überwachenden Kanals (Standard/privat).|
|ExtraProperties|Collection(Self.[KeyValuePair](#keyvaluepair-complex-type))|Nein|Eine Liste zusätzlicher Eigenschaften.|
|HostedContents|Sammlung (Self.[HostedContent](#hostedcontent-complex-type))|Nein|Eine Sammlung von Inhalten, die von Chat- oder Kanalnachrichten gehostet werden.|
|Members|Collection(Self.[MicrosoftTeamsMember](#microsoftteamsmember-complex-type))|Nein|Eine Liste der Benutzer innerhalb eines Teams.|
|MessageId|Edm.String|Nein|Ein Bezeichner für eine Chat- oder Kanalnachricht.|
|MessageURLs|Edm.String|Nein|Für jede URL vorhanden, die in Teams-Nachrichten gesendet wurde.|
|Nachrichten|Sammlung (Self.[Message](#message-complex-type))|Nein|Eine Sammlung von Chat- oder Kanalnachrichten.|
|MessageSizeInBytes|Edm.Int64|Nein|Die Größe einer Chat- oder Kanalnachricht in Bytes mit UTF-16-Codierung.|
|Name|Edm.String|Nein|Nur für Einstellungsereignisse vorhanden. Der Name der geänderten Einstellung.|
|NewValue|Edm.String|Nein|Nur für Einstellungsereignisse vorhanden. Neuer Wert der Einstellung.|
|OldValue|Edm.String|Nein|Nur für Einstellungsereignisse vorhanden. Alter Wert der Einstellung.|
|SubscriptionId|Edm.String|Nein|Ein eindeutiger Bezeichner eines Microsoft Graph-Änderungsbenachrichtigungsabonnements.|
|TabType|Edm.String|Nein|Nur für Registerkartenereignisse vorhanden. Der Registerkartentyp, der das Ereignis generiert hat.|
|TeamGuid|Edm.Guid|Nein|Die eindeutige ID des überwachten Teams.|
|TeamName|Edm.String|Nein|Der Name des überwachten Teams.|
||||

### <a name="microsoftteamsmember-complex-type"></a>Komplexer MicrosoftTeamsMember-Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|UPN|Edm.String|Nein|Der Benutzerprinzipalname des Benutzers.|
|Rolle|Self.[MemberRoleType](#memberroletype)|Nein|Die Rolle des Benutzers innerhalb des Teams.|
|DisplayName|Edm.String|Nein|Der Anzeigename des Benutzers.|
|||||

### <a name="enum-memberroletype---type-edmint32"></a>Enumeration: MemberRoleType - Typ: Edm.Int32

#### <a name="memberroletype"></a>MemberRoleType

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|0|Member|Ein Benutzer, der Mitglied des Teams ist.|
|1|Besitzer|Ein Benutzer, der Besitzer des Teams ist.|
|2|Gast|Ein Benutzer, der kein Mitglied des Teams ist.|
||||

### <a name="keyvaluepair-complex-type"></a>Komplexer Typ "KeyValuePair"

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Key|Edm.String|Nein|Der Schlüssel des Schlüssel-Wert-Paars.|
|Value|Edm.String|Nein|Der Wert des Schlüssel-Wert-Paars.|
|||||

### <a name="enum-addontype---type-edmint32"></a>Enumeration: AddOnType - Typ: Edm.Int32

#### <a name="addontype"></a>AddOnType

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|1|Bot|Ein Microsoft Teams-Bot.|
|2|Connector|Ein Microsoft Teams-Konnektor.|
|3|Tab|Eine Microsoft Teams-Registerkarte.|
||||

### <a name="hostedcontent-complex-type"></a>HostedContent komplexer Typ

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Id|Edm.String|Ja|Ein eindeutiger Bezeichner des von einer Nachricht gehosteten Inhalts.|
|SizeInBytes|Edm.Int64|Nein|Die Größe des von einer Nachricht gehosteten Inhalts in Bytes.|
|||||

### <a name="message-complex-type"></a>Komplexer Nachrichtentyp

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|AADGroupId|Edm.String|Nein|Ein eindeutiger Bezeichner der Gruppe in Azure Active Directory, zu der die Nachricht gehört.|
|Id|Edm.String|Ja|Ein eindeutiger Bezeichner für die Chat- oder Kanalnachricht.|
|ChannelGuid|Edm.String|Nein|Ein eindeutiger Bezeichner für den Kanal, zu dem die Nachricht gehört.|
|ChannelName|Edm.String|Nein|Der Name des Kanals, zu dem die Nachricht gehört.|
|ChannelType|Edm.String|Nein|Der Typ des Kanals, zu dem die Nachricht gehört.|
|ChatName|Edm.String|Nein|Der Name des Chats, zu dem die Nachricht gehört.|
|ChatThreadId|Edm.String|Nein|Ein eindeutiger Bezeichner für den Chat, zu dem die Nachricht gehört.|
|ParentMessageId|Edm.String|Nein|Ein eindeutiger Bezeichner für die übergeordnete Chat- oder Kanalnachricht.|
|SizeInBytes|Edm.Int64|Nein|Die Größe der Nachricht in Bytes mit UTF-16-Codierung.|
|TeamGuid|Edm.String|Nein|Ein eindeutiger Bezeichner für den Team, zu dem die Nachricht gehört.|
|TeamName|Edm.String|Nein|Der Name des Teams, zu dem die Nachricht gehört.|
|Version|Edm.String|Nein|Die Version der Chat- oder Kanalnachricht.|
|||||
 
## <a name="microsoft-defender-for-office-365-and-threat-investigation-and-response-schema"></a>Microsoft Defender für Office 365 und Threat Investigation and Response-Schema

[Microsoft Defender für Office 365](/office365/securitycompliance/office-365-atp)- und Threat Investigation and Response-Ereignisse stehen jetzt für Office 365-Kunden zur Verfügung, die einen Defender für Office 365 Plan 1, Defender für Office 365 Plan 2 oder ein E5-Abonnement haben. Jedes Ereignis im Defender für Office 365-Feed entspricht Folgendem, das als Bedrohung eingestuft wurde:

- Eine E-Mail-Nachricht mit Erkennung, die von einem Benutzer in der Organisation empfangen oder gesendet wurde, die für Nachrichten zum Übermittlungszeitpunkt und von [Automatische Bereinigung zur Nullstunde](https://support.office.com/article/Zero-hour-auto-purge-protection-against-spam-and-malware-96deb75f-64e8-4c10-b570-84c99c674e15) durchgeführt wurde. 

- Von einem Benutzer in der Organisation angeklickte URLs, die beim Klicken basierend auf dem Schutz [Sichere Links in Defender für Office 365](/office365/securitycompliance/atp-safe-links) als böswillig erkannt wurden.  

- Einer Datei in SharePoint Online, OneDrive for Business oder Microsoft Teams, die vom Schutz [Microsoft Defender für Office 365](/office365/securitycompliance/atp-for-spo-odb-and-teams) als böswillig eingestuft wurde.

- Einer Warnung, die ausgelöst wurde und eine [automatisierte Untersuchung](/office365/securitycompliance/automated-investigation-response-office) eingeleitet hat.

> [!NOTE]
> Funktionen von Microsoft Defender für Office 365 und Office 365 Threat Investigation and Response (vormals bekannt als „Office 365 Threat Intelligence“) sind nun Bestandteil von Defender für Office 365 Plan 2, mit zusätzlichen Funktionen zum Schutz vor Bedrohungen. Weitere Informationen hierzu finden Sie unter [Microsoft Defender für Office 365 – Pläne und Preise](https://products.office.com/exchange/advance-threat-protection) und in der [Defender für Office 365-Dienstbeschreibung](/office365/servicedescriptions/office-365-advanced-threat-protection-service-description).

### <a name="email-message-events"></a>E-Mail-Nachricht-Ereignisse

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|AttachmentData|Collection(Self.[AttachmentData](#attachmentdata))|Nein|Daten zu Anlagen der E-Mail-Nachricht, die das Ereignis ausgelöst hat.|
|DetectionType|Edm.String|Ja|Der Typ der Erkennung (z. B. **Inline** – erkannt zum Übermittlungszeitpunkt; **Verzögert** – erkannt nach Zustellung; **ZAP** – Nachrichten durch [Automatische Bereinigung zur Nullstunde](https://support.office.com/article/Zero-hour-auto-purge-protection-against-spam-and-malware-96deb75f-64e8-4c10-b570-84c99c674e15)) entfernt. In der Regel geht Ereignissen mit ZAP-Erkennungstyp eine Nachricht mit dem Erkennungstyp **Verzögert** voraus.|
|DetectionMethod|Edm.String|Ja|Die Methode oder Technologie, die von Defender für Office 365  für die Erkennung verwendet wurde.|
|InternetMessageId|Edm.String|Ja|Die Internetnachrichten-ID.|
|NetworkMessageId|Edm.String|Ja|Die Nachrichten-ID des Exchange Online-Netzwerks.|
|P1Sender|Edm.String|Ja|Der Rückpfad des Absenders der E-Mail-Nachricht.|
|P2Sender|Edm.String|Ja|Der Absenders der E-Mail-Nachricht.|
|Richtlinie|Self.[Policy](#policy-type-and-action-type)|Ja|Der für die E-Mail-Nachricht relevante Filterrichtlinientyp (z. B. **Antispam** oder **Antiphishing**) und der zugehörige Aktionstyp (z. B. **Nachricht mit hoher Spamwahrscheinlichkeit**, **Spam** oder **Phishing**).|
|Richtlinie|Self.[PolicyAction](#policy-action)|Ja|Die für die E-Mail-Nachricht relevante und in der Filterrichtlinie konfigurierte Aktion (z. B. **In Junk-E-Mail-Ordner verschieben** oder **Quarantäne**).|
|P2Sender|Edm.String|Ja|Der Absender im Feld **Von:** der E-Mail-Nachricht.|
|Empfänger|Collection(Edm.String)|Ja|Enthält eine Reihe von Empfängern einer E-Mail-Nachricht.|
|SenderIp|Edm.String|Ja|Die IP-Adresse, die die E-Mail über Office 365 übermittelt hat. Die IP-Adresse wird im Adressformat IPv4 oder IPv6 angezeigt.|
|Betreff|Edm.String|Ja|Die Betreffzeile der Nachricht.|
|Verdict|Edm.String|Ja|Die Bewertung der Nachricht.|
|MessageTime|Edm.Date|Ja|Zeitpunkt in UTC, zu dem die E-Mail empfangen oder gesendet wurde.|
|EventDeepLink|Edm.String|Ja|Deep-Link zum E-Mail-Ereignis im Explorer oder Echtzeit-Berichten im Office 365 Security & Compliance Center.|
|Sendeaktion |Edm.String|Ja|Die ursprüngliche Sendeaktion für die E-Mail-Nachricht.|
|Ursprünglicher Übermittlungsort |Edm.String|Ja|Der ursprüngliche Übermittlungsort der E-Mail-Nachricht.|
|Letzter Übermittlungsort |Edm.String|Ja|Der letzte Übermittlungsort der E-Mail-Nachricht zum Zeitpunkt des Ereignisses.|
|Directionality |Edm.String|Ja|Gibt an, ob eine E-Mail-Nachricht ein- oder ausgehend war, oder ob es sich um eine organisationsinterne Nachricht handelte.|
|ThreatsAndDetectionTech |Edm.String|Ja|Die Bedrohungen und die entsprechenden Erkennungstechnologien. In diesem Feld werden alle Bedrohungen einer E-Mail-Nachricht angezeigt, einschließlich des neuesten Zusatzes zur Spambewertung.  Beispiel: ["Phish: [Spoof DMARC]","Spam: [URL malicious reputation]"]. Die verschiedenen Erkennungstechnologien werden weiter unten beschrieben.|
|AdditionalActionsAndResults |Collection(Edm.String)|Nein|Die zusätzlichen Aktionen, die für die E-Mail ausgeführt wurden, z. B. ZAP oder manuelle Wartung. Umfasst auch die entsprechenden Ergebnisse.|
|Connectors |Edm.String|Nein|Die Namen und GUIDs der Connectors, die der E-Mail zugeordnet sind.|
|AuthDetails |Collection(Self.[AuthDetails](#authdetails))|Nein|Die Authentifizierungsprüfungen, die für die E-Mail durchgeführt werden. Umfasst auch die Werte für SPF, DKIM, DMARC und CompAuth.|
|SystemOverrides |Collection(Self.[SystemOverrides](#systemoverrides))|Nein|Außerkraftsetzungen, die für die E-Mail gelten. Dabei kann es sich um System- oder Benutzeraußerkraftsetzungen handelt.|
|Phishing-Konfidenzniveau |Edm.String|Nein|Gibt das Konfidenzniveau an, das der Phishing-Bewertung zugeordnet ist. Kann „Normal“ oder „Hoch“ sein.|  
|||||

> [!NOTE]
> Wir empfehlen, das neue Feld "ThreatsAndDetectionTech" zu verwenden, da hierin mehrere Bewertungen und die aktualisierten Erkennungstechnologien angezeigt werden. Dies entspricht auch den Werten, die in anderen Lösungen wie dem Sicherheitsrisiken-Explorer und der erweiterten Bedrohungssuche angezeigt würden. 

### <a name="detection-technologies"></a>Erkennungstechnologien

|**Name**|**Beschreibung**|
|:-----|:-----|
|Allgemeiner Filter |Phishing-Signale basierend auf Regeln.|
|Vorgetäuschte Marke | Der Dateityp der Anlage.|
|Spoofing externer Domäne |Der Absender versucht, eine andere Domäne zu spoofen.|
|Spoof DMARC |DMARC-Authentifizierungsfehler bei Nachrichten.|
|Vorgetäuschte Domäne | Vortäuschen von Domänen, die der Kunde besitzt oder definiert.|
|Dateidetonation |Dateianlagen, die während einer Detonationsanalyse als schädlich erkannt wurden.|
|Datei-Reputation |Aufgrund von schlechter Zuverlässigkeit als schädlich gekennzeichnete Dateianlagen.|
|Reputation der Dateidetonation |Aufgrund der Reputation früherer Detonation als schädlich gekennzeichnete Dateianlage.|
|Fingerabdruckübereinstimmung |Die Nachricht wurde aufgrund vorheriger Nachrichten als schädlich gekennzeichnet.|
|Mailbox Intelligence-basierte Identitätsvortäuschung |Identitätsvortäuschung basierend auf Mailbox Intelligence.|
|Domänenreputation |Analyse basierend auf der Domänenreputation.|
|Organisationsinternes Spoofing |  Der Absender versucht, die Empfängerdomäne zu spoofen. |
|Erweiterter Filter |  Phishing-Signale auf Grundlage von maschinellem Lernen.|
|Anti-Malware-Engine    | Erkennung von Schadsoftware-Engines. |
|Erkennung durch gemischte Analysen   | Mehrere Filter haben zur Bewertung dieser Nachricht beigetragen. |
|URL-Reputation als schädlich eingestuft   | Die Nachricht wurde aufgrund einer schädlichen URL als schlecht eingestuft. |
|URL-Detonation | Die Nachricht wurde aufgrund einer vorherigen Detonation einer schädlichen URL als schlecht eingestuft. |
|Reputation der URL-Detonation| Die Nachricht wurde aufgrund einer Detonation einer schädlichen URL als schlecht eingestuft. |
|Vorgetäuschte Benutzeridentität|    Vortäuschung von Benutzeridentitäten, die vom Administrator definiert oder deren Erkennung über Mailbox Intelligence erlernt wurde.|
|Kampagne   |Nachrichten, die als Teil einer Kampagne identifiziert wurden.|

### <a name="attachmentdata-complex-type"></a>Komplexer AttachmentData-Typ

#### <a name="attachmentdata"></a>AttachmentData

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|FileName|Edm.String|Ja|Der Dateiname der Anlage.|
|FileType|Edm.String|Ja|Der Dateityp der Anlage.|
|FileVerdict|Self.[FileVerdict](#fileverdict)|Ja|Die Bewertung der Schadsoftware der Datei.|
|MalwareFamily|Edm.String|Nein|Die Familie der Schadsoftware.|
|SHA256|Edm.String|Ja|Die Datei mit der Hash-Funktion SHA256.|
|||||

> [!NOTE]
> Innerhalb der Malwarefamilie können Sie den genauen Namen der MalwareFamily-Namen sehen (z. B. HTML/Phish.VS!MSR) oder schädliche Nutzlast als statische Zeichenfolge. Eine schädliche Nutzlast sollte auch dann als schädliche E-Mail behandelt werden, wenn kein bestimmter Name identifiziert wurde.

### <a name="systemoverrides-complex-type"></a>Komplexer SystemOverrides-Typ
 
#### <a name="systemoverrides"></a>SystemOverrides

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Details|Edm.String|Nein|Die Details zur spezifischen Außerkraftsetzung (z. B. ETR oder sicherer Absender), die angewendet wurde.|
|FinalOverride|Edm.String|Nein|Gibt die Außerkraftsetzung an, die sich bei mehreren Außerkraftsetzungen auf die Übermittlung ausgewirkt hat.|
|Result|Edm.String|Nein|Gibt an, ob die E-Mail basierend auf der Außerkraftsetzung auf „Zugelassen“ oder „Blockiert“ festgelegt wurde.|
|Quelle|Edm.String|Nein|Gibt an, ob die Außerkraftsetzung vom Benutzer oder vom Mandanten konfiguriert wurde.|
|||||

### <a name="authdetails-complex-type"></a>Komplexer AuthDetails-Typ
 
#### <a name="authdetails"></a>AuthDetails
 
|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Name|Edm.String|Nein|Der Name der spezifischen Authentifizierungsprüfung, z. B. DKIM oder DMARC.|
|Wert|Edm.String|Nein|Der Wert, der der spezifischen Authentifizierungsprüfung zugeordnet ist, z. B. „True“ oder „False“.|
|||||
 
### <a name="enum-fileverdict---type-edmint32"></a>Enumeration: FileVerdict - Typ: Edm.Int32

#### <a name="fileverdict"></a>FileVerdict

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|0|Gut|Keine Bedrohung erkannt.|
|1|Schlecht|Malware in der Anlage gefunden.|
|-1|Fehler|Scan-/Analysefehler.|
|-2|Timeout|Scan-/Analyse-Timeout.|
|-3|Ausstehend|Scan/Analyse nicht abgeschlossen.|
|||||

### <a name="enum-policy---type-edmint32"></a>Enum: Policy – Type: Edm.Int32

#### <a name="policy-type-and-action-type"></a>Richtlinientyp und Aktivitätstyp

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|1|Antispam, HSPM|Aktion für Nachricht mit hoher Spamwahrscheinlichkeit (HSPM) in der Antispamrichtlinie.|
|2|Antispam, SPM|Aktion für Spamnachricht (SPM) in der Antispamrichtlinie.|
|3|Antispam, Massensendung|Aktion für Massensendungen in der Antispamrichtlinie.|
|4|Antispam, PHSH|Aktion für Phishingnachricht (PHSH) in der Antispamrichtlinie.|
|5|Antiphishing, DIMP|Aktion für Domänenidentitätswechsel (DIMP) in der Antiphishingrichtlinie.|
|6|Antiphishing, UIMP|Aktion für Benutzeridentitätswechsel (UIMP) in der Antiphishingrichtlinie.|
|7|Antiphishing, SPOOF|Aktion für Spoofing in der Antiphishingrichtlinie.|
|8|Antiphishing, GIMP|Aktion für Mailbox Intelligence in der Antiphishingrichtlinie.|
|9|Antischadsoftware, AMP| Schadsoftware-Richtlinienaktion in der Antischadsoftware-Richtlinie.|
|10|Sichere Anlage, SAP| Richtlinienaktion in der Richtlinie für sichere Anlagen in Defender für Office 365.|
|11|Exchange-Transportregel; ETR| Richtlinienaktion in der Exchange-Transportregel.|
|12|Antischadsoftware, ZAPM| Schadsoftware-Richtlinienaktion in der auf ZAP (Automatische Bereinigung zur Nullstunde) angewendeten Antischadsoftware-Richtlinie.|
|13|Antiphishing, ZAPP| Phishing-Richtlinienaktion in der auf ZAP angewendeten Antiphishingrichtlinie.|
|14|Antiphishing, ZAPS| Spam-Richtlinienaktion in der auf ZAP angewendeten Antispamrichtlinie.|
|15|Antispam-Phishing-E-Mail mit hoher Vertrauenswürdigkeit (HPHISH)|Phishing-Richtlinienaktion mit hoher Vertraulichkeit in der Antispamrichtlinie.|
|17|Antispamrichtlinie für ausgehende Spam-E-Mails (OSPM)|Richtlinienaktion in der Filterrichtlinie für ausgehende Spam-E-Mails in Antispam.|
||||

### <a name="enum-policyaction---type-edmint32"></a>Enum: PolicyAction – Type: Edm.Int32

#### <a name="policy-action"></a>Richtlinienaktion

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|0|MoveToJMF|Die Richtlinienaktion besteht darin, das Element in den Junk-E-Mail-Ordner zu verschieben.|
|1|AddXHeader|Die Richtlinienaktion besteht darin, einen X-Header zur E-Mail-Nachricht hinzuzufügen.|
|2|ModifySubject|Die Richtlinienaktion besteht darin, dem Betreff in der E-Mail-Nachricht die in der Filterrichtlinie angegebenen Informationen hinzuzufügen.|
|3|Redirect|Die Richtlinienaktion besteht darin, die E-Mail-Nachricht an die in der Filterrichtlinie angegebene E-Mail-Adresse umzuleiten.|
|4|Delete|Die Richtlinienaktion besteht darin, die E-Mail-Nachricht zu löschen.|
|5|Quarantine|Die Richtlinienaktion besteht darin, die E-Mail-Nachricht in die Quarantäne zu verschieben.|
|6|NoAction| Die Richtlinie ist so konfiguriert, dass keine Aktionen für die E-Mail-Nachricht durchgeführt werden.|
|7|BccMessage|Die Richtlinienaktion besteht darin, die E-Mail-Nachricht per Bcc an die in der Filterrichtlinie angegebene E-Mail-Adresse zu senden.|
|8|ReplaceAttachment|Die Richtlinienaktion besteht darin, die Anlage in der E-Mail-Nachricht wie in der Filterrichtlinie angegeben zu ersetzen.|
||||

### <a name="url-time-of-click-events"></a>Ereignisse zum Zeitpunkt des Klickens auf eine URL

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|UserId|Edm.String|Ja|Bezeichner (z. B. E-Mail-Adresse) für den Benutzer, der auf die URL geklickt hat.|
|AppName|Edm.String|Ja|Office 365-Dienst, von dem aus auf die URL geklickt wurde (z. B. E-Mail).|
|URLClickAction|Self.[URLClickAction](#urlclickaction)|Ja|Klicken Sie auf die Aktion für die URL basierend auf den Richtlinien der Organisation für [Sichere Links in Defender für Office 365](/office365/securitycompliance/atp-safe-links).|
|SourceId|Edm.String|Ja|Bezeichner für den Office 365-Dienst, aus dem die URL angeklickt wurde (für E-Mail ist dies z. B. die Nachrichten-ID des Exchange Online-Netzwerks).|
|TimeOfClick|Edm.Date|Ja|Das Datum und die Uhrzeit in koordinierter Weltzeit (UTC), wann der Benutzer auf die URL geklickt hat.|
|URL|Edm.String|Ja|Die URL, auf die der Benutzer geklickt hat.|
|UserIp|Edm.String|Ja|Die IP-Adresse des Benutzer, der auf die URL geklickt hat. Die IP-Adresse wird im Adressformat IPv4 oder IPv6 angezeigt.|
|||||

### <a name="enum-urlclickaction---type-edmint32"></a>Enum: URLClickAction – Type: Edm.Int32

#### <a name="urlclickaction"></a>URLClickAction

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|2|Blockpage|Benutzer, für den das Navigieren zur URL durch [Sichere Links in Defender für Office 365](/office365/securitycompliance/atp-safe-links) blockiert wurde.|
|3|PendingDetonationPage|Benutzer, dem die Seite zur ausstehenden Denotation durch [Sichere Links in Defender für Office 365](/office365/securitycompliance/atp-safe-links) angezeigt wird.|
|4|BlockPageOverride|Benutzer, dem das Navigieren zur URL durch [Sichere Links in Defender für Office 365](/office365/securitycompliance/atp-safe-links) blockiert wurde. Der Benutzer hat jedoch die Sperre außer Kraft gesetzt, um zur URL zu navigieren.|
|5|PendingDetonationPageOverride|Benutzer, dem die Seite zur ausstehenden Detonation durch [Sichere Links in Defender für Office 365](/office365/securitycompliance/atp-safe-links) angezeigt wird. Der Benutzer hat dies jedoch außer Kraft gesetzt, um zur URL zu navigieren.|
|||||

### <a name="file-events"></a>Dateiereignisse

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|FileData|Self.[FileData](#filedata)|Ja|Daten zu der Datei, die das Ereignis ausgelöst hat.|
|SourceWorkload|Self.[SourceWorkload](#sourceworkload)|Ja|Arbeitslast oder Dienst, in der bzw. in dem die Datei gefunden wurde (z. B. SharePoint Online, OneDrive for Business oder Microsoft Teams).
|DetectionMethod|Edm.String|Ja|Die Methode oder Technologie, die von Microsoft Defender für Office 365 für die Erkennung verwendet wurde.|
|LastModifiedDate|Edm.Date|Ja|Der Zeitpunkt in UTC, zu dem die Datei erstellt oder zuletzt geändert wurde.|
|LastModifiedBy|Edm.String|Ja|Bezeichner (z. B. eine E-Mail-Adresse) für den Benutzer, der die Datei erstellt oder zuletzt geändert hat.|
|EventDeepLink|Edm.String|Ja|Deep-Link zum Dateiereignis im Explorer oder Echtzeit-Berichten im Security & Compliance Center.|
|||||

### <a name="filedata-complex-type"></a>Komplexer FileData-Typ

#### <a name="filedata"></a>FileData

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|DocumentId|Edm.String|Ja|Eindeutiger Bezeichner für die Datei in SharePoint, OneDrive oder Microsoft Teams.|
|FileName|Edm.String|Ja|Name der Datei, die das Ereignis ausgelöst hat.|
|FilePath|Edm.String|Ja|Pfad (Speicherort) zu der Datei in SharePoint, OneDrive oder Microsoft Teams|
|FileVerdict|Self.[FileVerdict](#fileverdict)|Ja|Die Bewertung der Schadsoftware der Datei.|
|MalwareFamily|Edm.String|Nein|Die Familie der Schadsoftware.|
|SHA256|Edm.String|Ja|Die Datei mit der Hash-Funktion SHA256.|
|FileSize|Edm.String|Ja|Größe der Datei in Byte.|
|||||

### <a name="enum-sourceworkload---type-edmint32"></a>Enum: SourceWorkload – Type: Edm.Int32

#### <a name="sourceworkload"></a>SourceWorkload

|**Wert**|**Elementname**|
|:-----|:-----|
|0|SharePoint Online|
|1|OneDrive for Business|
|2|Microsoft Teams|
|||||

## <a name="submission-schema"></a>Übermittlungsschema

[Übermittlungsereignisse](/microsoft-365/security/office-365-security/report-junk-email-messages-to-microsoft) sind für alle [Office 365-Kunden verfügbar, da sie im Lieferumfang von Security enthalten sind](/microsoft-365/security/office-365-security/overview). Dies schließt Organisationen ein, die Exchange Online Protection und Microsoft Defender für Office 365 verwenden. Jedes Ereignis im Übermittlungsfeed entspricht falsch-positiven oder falsch-negativen Ergebnissen, die übermittelt wurden als:

- **Administratorübermittlung**. Nachrichten, Dateien oder URLs, die zur Analyse an Microsoft übermittelt werden.
- **Vom Benutzer gemeldetes Element**. Nachrichten, die von Endbenutzern an den Administrator oder an Microsoft zur Überprüfung gemeldet wurden.

### <a name="submission-events"></a>Übermittlungsereignisse

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|AdminSubmissionRegistered|Edm.String|Nein|Die Administratorübermittlung ist registriert und ihre Verarbeitung steht aus.|
|AdminSubmissionDeliveryCheck|Edm.String|Nein|Das Administratorübermittlungssystem hat die E-Mail-Richtlinie überprüft.|
|AdminSubmissionSubmitting|Edm.String|Nein|Das Administratorübermittlungssystem übermittelt die E-Mail.|
|AdminSubmissionSubmitted|Edm.String|Nein|Das Administratorübermittlungssystem hat die E-Mail übermittelt.|
|AdminSubmissionTriage|Edm.String|Nein|Die Administratorübermittlung wird durch den Grader selektiert.|
|AdminSubmissionTimeout|Edm.String|Nein|Bei der Administratorübermittlung tritt ein Timeout ohne Ergebnis auf.|
|UserSubmission|Edm.String|Nein|Die Übermittlung wurde zuerst von einem Endbenutzer gemeldet.|
|UserSubmissionTriage|Edm.String|Nein|Die Benutzerübermittlung wird durch den Grader selektiert.|
|CustomSubmission|Edm.String|Nein|Die von einem Benutzer gemeldete Nachricht wurde an das benutzerdefinierte Postfach der Organisation gesendet, wie in den Einstellungen für vom Benutzer gemeldete Nachrichten festgelegt.|
|AttackSimUserSubmission|Edm.String|Nein|Die vom Benutzer gemeldete Nachricht war tatsächlich eine Phishingsimulations-Trainingsnachricht.|
|AdminSubmissionTablAllow|Edm.String|Nein|Zum Zeitpunkt der Übermittlung wurde eine Zulassung erstellt, um sofort Maßnahmen für ähnliche Nachrichten zu ergreifen, während sie erneut gescannt wird.|
|SubmissionNotification|Edm.String|Nein|Administratorfeedback wird an Endbenutzer gesendet.|
|||||

## <a name="automated-investigation-and-response-events-in-office-365"></a>Automatisierte Untersuchungs- und Reaktionsereignisse in Office 365

[Office 365 Automated Investigation and Response (AIR)](/office365/securitycompliance/automated-investigation-response-office)-Ereignisse (Automatisierte Untersuchung und Reaktion) stehen für Office 365-Kunden zur Verfügung, die ein Abonnement haben, in dem Microsoft Defender für Office 365 Plan 2 oder Office 365 E5 enthalten ist. Untersuchungen werden basierend einer Änderung des Untersuchungsstatus protokolliert. Wenn beispielsweise ein Administrator eine Aktion durchführt, mit der der Status einer Untersuchung von „Ausstehende Aktionen“ in „Abgeschlossen“ geändert wird, wird ein Ereignis protokolliert.

Zurzeit werden nur automatisierte Untersuchungen protokolliert. (Ereignisse für manuell gestartete Untersuchungen werden in Kürze verfügbar sein.) Die folgenden Statuswerte werden protokolliert:

- Untersuchung gestartet
- Keine Bedrohungen gefunden
- Vom System beendet
- Ausstehende Aktion
- Bedrohungen gefunden
- Bereinigt
- Fehlgeschlagen
- Durch Drosselung beendet
- Durch den Benutzer beendet
- Wird ausgeführt

### <a name="main-investigation-schema"></a>Hauptuntersuchungsschema

|Name    |Typ    |Beschreibung  |
|----|----|----|
|InvestigationId    |Edm.String    |Investigation ID/GUID |
|InvestigationName    |Edm.String    |Name der Untersuchung |
|InvestigationType    |Edm.String    |Typ der Untersuchung. Kann einen der folgenden Werte annehmen:<br/>- Vom Benutzer gemeldete Nachrichten<br/>- Mit ZAP behandelte Schadsoftware<br/>- Mit ZAP behandeltes Phishing<br/>- URL-Bewertungsänderung<p>(Manuelle Untersuchungen stehen derzeit nicht zur Verfügung, werden aber in Kürze verfügbar sein.) |
|LastUpdateTimeUtc    |Edm.Date    |UTC-Uhrzeit der letzten Aktualisierung einer Untersuchung |
|StartTimeUtc    |Edm.Date    |Startzeit einer Untersuchung |
|Status     |Edm.String     |Stande der Untersuchung, laufende, ausstehende Aktionen usw. |
|DeeplinkURL    |Edm.String    |Deep-Link-URL einer Untersuchung im Office 365 Security & Compliance Center |
|Aktionen |Auflistung (Edm.String)    |Auflistung der von einer Untersuchung empfohlenen Aktionen |
|Daten    |Edm.String    |Die Datenzeichenfolge, die weitere Details zu den Untersuchungsentitäten sowie Informationen zu Warnungen, die mit der Untersuchung zusammenhängen, enthält. Entitäten sind in einem separaten Knoten innerhalb des Daten-BLOBs verfügbar. |
||||

### <a name="actions"></a>Aktionen

|Feld    |Typ    |Beschreibung |
|----|----|----|
|ID     |Edm.String    |Action ID|
|ActionType    |Edm.String    |Der Typ der Aktion, z. b. E-Mail-Gegenmaßnahme |
|ActionStatus    |Edm.String    |Gültige Werte schließen ein: <br/>- Ausstehend<br/>- Wird ausgeführt<br/>- Warten auf Ressource<br/>- Abgeschlossen<br/>- Fehlgeschlagen |
|ApprovedBy    |Edm.String    |Null, wenn automatisch genehmigt; andernfalls der username/ID (in Kürze verfügbar) |
|TimestampUtc:    |Edm.DateTime    |Der Zeitstempel der Änderung des Aktivitätsstatus |
|ActionId    |Edm.String    |Eindeutiger Bezeichner der Aktion |
|InvestigationId    |Edm.String    |Eindeutiger Bezeichner einer Untersuchung |
|RelatedAlertIds    |Collection(Edm.String)    |Benachrichtigungen im Zusammenhang mit einer Untersuchung |
|StartTimeUtc    |Edm.DateTime    |Zeitstempel der Erstellung einer Aktion |
|EndTimeUtc    |Edm.DateTime    |Finaler Aktivitätsstatus-Zeitstempel einer Aktion |
|Ressourcen-Bezeichner     |Edm.String     |Besteht aus der Azure Active Directory-Mandanten-ID.|
|Entitäten    |Collection(Edm.String)    |Liste einer oder mehrerer durch eine Aktion betroffener Entitäten |
|Zugehörige Benachrichtigungs-IDs    |Edm.String    |Benachrichtigung im Zusammenhang mit einer Untersuchung |
||||

### <a name="entities"></a>Entitäten

#### <a name="mailmessage-email"></a>MailMessage (E-Mail)

|Feld    |Typ    |Beschreibung  |
|----|----|----|
|Typ    |Edm.String    |„mail-message“  |
|Dateien    |Auflistung (Self.File) |Details zu den Dateien, die Anlagen dieser Nachricht sind |
|Empfänger    |Edm.String    |Der Empfänger dieser Nachricht |
|URLs    |Auflistung (Self.URL) |Die URLs, die in dieser E-Mail enthalten sind  |
|Absender    |Edm.String    |Die E-Mail-Adresse des Absenders  |
|SenderIp    |Edm.String    |Die IP-Adresse des Absenders  |
|ReceivedDate    |Edm.DateTime    |Das Datum, an dem die Nachricht empfangen wurde  |
|NetworkMessageId    |Edm.Guid     |Die Netzwerk-Nachrichten-ID dieser E-Mail  |
|InternetMessageId    |Edm.String  |Die Internetnachrichten-ID dieser E-Mail |
|Betreff    |Edm.String    |Der Betreff dieser Nachricht  |
||||

#### <a name="ip"></a>IP

|Feld    |Typ    |Beschreibung  |
|----|----|----|
|Typ    |Edm.String    |„ip“ |
|Adresse    |Edm.String    |Die IP-Adresse als Zeichenfolge, wie z. b. `127.0.0.1`
||||

#### <a name="url"></a>URL

|Feld    |Typ    |Beschreibung  |
|----|----|----|
|Typ    |Edm.String    |„url“ |
|Url    |Edm.String    |Die vollständige URL, auf die eine Entität verweist  |
||||

#### <a name="mailbox-also-equivalent-to-the-user"></a>Postfach (entspricht dem Benutzer) 

|Feld    |Typ    |Beschreibung |
|----|----|----|
|Typ    |Edm.String    |„mailbox“  |
|MailboxPrimaryAddress    |Edm.String    |Die primäre Adresse des Postfachs  |
|DisplayName    |Edm.String    |Der Anzeigename des Postfachs |
|UPN    |Edm.String    |Der UPN des Postfachs  |
||||

#### <a name="file"></a>Datei

|Feld    |Typ    |Beschreibung  |
|----|----|----|
|Typ    |Edm.String    |„file“ |
|Name    |Edm.String    |Der Dateiname ohne Pfad |
FileHashes |Auflistung (Edm.String)    |Die Dateihashes, die der Datei zugeordnet sind |
||||

#### <a name="filehash"></a>FileHash

|Feld    |Typ    |Beschreibung |
|----|----|----|
|Typ    |Edm.String    |„filehash“ |
|Algorithmus    |Edm.String    |Der Hash-Algorithmustyp kann einen der folgenden Werte annehmen:<br/>- Unbekannt<br/>- MD5<br/>- SHA1<br/>- SHA256<br/>- SHA256AC
|Wert    |Edm.String    |Der Hashwert  |
||||

#### <a name="mailcluster"></a>MailCluster

|Feld    |Typ    |Beschreibung   |
|----|----|----|
|Typ    |Edm.String    |"MailCluster" <br/>Bestimmt den Typ der zu in Frage stehenden Entität |
|NetworkMessageIds    |Auflistung (Edm.String)    |Liste der E-Mail-IDs, die Teil des E-Mail-Clusters sind |
|CountByDeliveryStatus    |Auflistungen (Edm.String)    |Anzahl E-Mails nach DeliveryStatus-Zeichenfolgendarstellung |
|CountByThreatType    |Auflistungen (Edm.String) |Anzahl E-Mails nach ThreatType-Zeichenfolgendarstellung |
|Risiken    |Auflistungen (Edm.String)    |Die Bedrohungen durch E-Mails, die Teil des E-Mail-Clusters sind. Zu den Bedrohungen gehören Werte wie Phishing und Schadsoftware. |
|Query    |Edm.String    |Die Abfrage, die verwendet wurde, um die Nachrichten des E-Mail-Clusters zu identifizieren  |
|QueryTime    |Edm.DateTime    |Die Abfragezeit  |
|MailCount    |Edm.int    |Die Anzahl der E-Mails, die Teil des E-Mail-Clusters sind.  |
|Source    |Zeichenfolge    |Die Quelle des Mail-Clusters; der Wert der Cluster-Quelle. |
||||

## <a name="hygiene-events-schema"></a>Nachrichtenschutzereignis-Schema

Nachrichtenschutzereignisse beziehen sich auf den ausgehenden Spamschutz. Diese Ereignisse beziehen sich auf Benutzer, die nicht zum Senden von E-Mails berechtigt sind. Weitere Informationen finden Sie unter:

- [Ausgehender Spamschutz](/microsoft-365/security/office-365-security/outbound-spam-controls)

- [Entfernen von blockierten Benutzern aus dem Portal „Eingeschränkte Benutzer“ in Office 365](/microsoft-365/security/office-365-security/removing-user-from-restricted-users-portal-after-spam)

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Überwachung|Edm.String|Nein|Systeminformationen im Zusammenhang mit dem Nachrichtenschutzereignis.|
|Ereignis|Edm.String|Nein|Der Typ des Nachrichtenschutzereignisses. Die Werte für diesen Parameter sind **gelistet** oder **nicht gelistet**.|
|EventId|Edm.Int64|Nein|Die ID des Nachrichtenschutzereignistyps.|
|EventValue|Edm.String|Nein|Der betroffene Benutzer.|
|Grund|Edm.String|Nein|Details zu dem Nachrichtenschutzereignis.|
|||||

## <a name="power-bi-schema"></a>Power BI-Schema

Die unter [Durchsuchen des Überwachungsprotokolls im Office 365-Schutzcenter](/power-bi/service-admin-auditing#activities-audited-by-power-bi) aufgelisteten Power BI-Ereignisse verwenden dieses Schema.

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
| AppName               | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Nein  | Der Name der App, in der das Ereignis aufgetreten ist. |
| DashboardName         | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Nein  | Der Name des Dashboards, in dem das Ereignis aufgetreten ist. |
| DataClassification    | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Nein  | Die [Datenklassifizierung](/power-bi/service-data-classification), sofern vorhanden, für das Dashboard, in dem das Ereignis aufgetreten ist. |
| DatasetName           | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Nein  | Der Name des Datasets, in dem das Ereignis aufgetreten ist. |
| MembershipInformation | Collection([MembershipInformationType](#membershipinformationtype-complex-type))   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Nein  | Mitgliedschaftsinformationen zu der Gruppe. |
| OrgAppPermission      | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Nein  | Berechtigungsliste für eine Organisations-App (gesamte Organisation, bestimmte Benutzer oder bestimmte Gruppen). |
| ReportName            | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Nein  | Der Name des Berichts, in dem das Ereignis aufgetreten ist. |
| SharingInformation    | Collection([SharingInformationType](#sharinginformationtype-complex-type))   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"    |  Nein  | Informationen zu der Person, an die eine Einladung zur Freigabe gesendet wird. |
| SwitchState           | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Nein  | Informationen zum Status der verschiedener Mandantenebenenoptionen. |
| WorkSpaceName         | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Nein  | Der Name des Arbeitsbereichs, in dem das Ereignis aufgetreten ist. |
|||||

### <a name="membershipinformationtype-complex-type"></a>Komplexer Typ „MembershipInformationType“

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
| MemberEmail | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Nein  | Die E-Mail-Adresse der Gruppe. |
| Status      | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Nein  | Derzeit nicht ausgefüllt. |
|||||

### <a name="sharinginformationtype-complex-type"></a>Komplexer Typ „SharingInformationType“

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
| RecipientEmail    | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Nein  | Die E-Mail-Adresse des Empfängers einer Freigabeeinladung. |
| RecipientName    | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Nein  | Der Name des Empfängers einer Freigabeeinladung. |
| ResharePermission | Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Nein  | Die dem Empfänger erteilte Berechtigung. |
|||||

## <a name="dynamics-365-schema"></a>Dynamics 365-Schema

Bei den Überwachungseinträgen für Ereignisse im Zusammenhang mit modellgesteuerten Apps in Dynamics 365-Ereignissen wird sowohl ein Basis- als auch ein Entitätenvorgangsschema verwendet. Weitere Informationen finden Sie unter [Aktivieren und Verwenden der Aktivitätenprotokollierung](/power-platform/admin/enable-use-comprehensive-auditing#model-driven-apps-in-dynamics-365-schema).

### <a name="dynamics-365-base-schema"></a>Dynamics 365-Basisschema

| **Parameter**     | **Typ**            | **Erforderlich?** | **Beschreibung**|
|:------------------ | :------------------ | :--------------|:--------------|
|CrmOrganizationUniqueName|Edm.String|Ja|Der eindeutige Name der Organisation.|
|InstanceUrl|Edm.String|Ja|Die URL zur Instanz.|
|ItemUrl|Edm.String|Nein|Die URL zum Datensatz, der das Protokoll ausgibt.|
|ItemType|Edm.String|Nein|Der Name der Entität.|
|UserAgent|Edm.String|Nein|Der eindeutige Bezeichner der Benutzer-GUID in der Organisation.|
|Fields|Collection(Common.NameValuePair)|Nein|Ein JSON-Objekt mit den Schlüssel/Wert-Paaren der Eigenschaft, die erstellt oder aktualisiert wurden.|
|||||

### <a name="dynamics-365-entity-operation-schema"></a>Dynamics 365-Entitätenvorgangsschema

Entitätenereignisse aus modellgesteuerten Apps in Dynamics 365 verwenden dieses Schema, um auf dem Dynamics 365-Basisschema aufzubauen. Dieses Schema enthält Informationen über den Entitätenvorgang, der das überprüfte Ereignis ausgelöst hat.

| **Parameter**     | **Typ**            | **Erforderlich?** | **Beschreibung**|
|:------------------ | :------------------ | :--------------|:--------------|
|EntityId|Edm.Guid|Nein|Der eindeutige Bezeichner der Entität.|
|EntityName|Edm.String|Ja|Der Name der Entität in der Organisation. Beispiel für Entitäten sind `contact` oder `authentication`.|
|Message|Edm.String|Ja|Dieser Parameter enthält den Vorgang, der im Zusammenhang mit der Entität durchgeführt wurde. Wenn z. B. ein neuer Kontakt erstellt wurde, weist die Message-Eigenschaft den Wert `Create` auf, und der entsprechende Wert der EntityName-Eigenschaft lautet `contact`.|
|Abfrage|Edm.String|Nein|Die Parameter der Filterabfrage, die beim Ausführen des FetchXML-Vorgangs verwendet wurden.|
|PrimaryFieldValue|Edm.String|Nein|Gibt den Wert des Attributs an, das das Primärfeld der Entität darstellt.|
|||||

## <a name="workplace-analytics-schema"></a>Workplace Analytics-Schema

Die unter [Durchsuchen des Überwachungsprotokolls im Office 365 Security & Compliance Center](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#microsoft-workplace-analytics-activities) aufgelisteten WorkPlace Analytics-Ereignisse verwenden dieses Schema.

| **Parameter**     | **Typ**            | **Erforderlich?** | **Beschreibung**|
|:------------------ | :------------------ | :--------------|:--------------|
| WpaUserRole        | Edm.String | Nein     | Die Workplace Analytics-Rolle des Benutzers, der die Aktion ausgeführt hat.|
| ModifiedProperties | Sammlung (Common.ModifiedProperty) | Nein | Diese Eigenschaft enthält den Namen der Eigenschaft, die geändert wurde, den neuen Wert der geänderten Eigenschaft und den vorherigen Wert der geänderten Eigenschaft.|
| OperationDetails   | Collection (Common.NameValuePair)    | Nein | Eine Liste der erweiterten Eigenschaften für die geänderte Einstellung. Jede Eigenschaft besitzt einen **Namen** und einen **Wert**.|
||||

## <a name="quarantine-schema"></a>Quarantäne-Schema

Die unter [Durchsuchen des Überwachungsprotokolls im Office 365 Security & Compliance Center](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#quarantine-activities) aufgelisteten Quarantäne-Ereignisse verwenden dieses Schema. Weitere Informationen zur Quarantäne finden Sie unter [In Quarantäne stellen von E-Mail-Nachrichten in Office 365](/microsoft-365/security/office-365-security/quarantine-email-messages).

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|RequestType|Self.[RequestType](#enum-requesttype---type-edmint32)|Nein|Die Art der Quarantäneanforderung, die von einem Benutzer ausgeführt wurde.|
|RequestSource|Self.[RequestSource](#enum-requestsource---type-edmint32)|Nein|Die Quelle einer Quarantäneanforderung kann vom Security & Compliance Center (SCC), einem Cmdlet oder einem URLlink stammen.|
|NetworkMessageId|Edm.String|Nein|Die Netzwerknachrichten-ID einer in Quarantäne befindlichen E-Mail-Nachricht.|
|ReleaseTo|Edm.String|Nein|Der Empfänger der E-Mail-Nachricht.|
|||||

### <a name="enum-requesttype---type-edmint32"></a>Enum: RequestType - Type: Edm.Int32

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|0|Vorschau|Hierbei handelt es sich um eine Anforderung von einem Benutzer zur Vorschau einer E-Mail-Nachricht, die als schädlich eingestuft wurde.|
|1|Löschen|Hierbei handelt es sich um eine Anforderung von einem Benutzer zum Löschen einer E-Mail-Nachricht, die als schädlich eingestuft wurde.|
|2|Freigabe|Hierbei handelt es sich um eine Anforderung von einem Benutzer zum Freigeben einer E-Mail-Nachricht, die als schädlich eingestuft wurde.|
|3|Exportieren|Hierbei handelt es sich um eine Anforderung von einem Benutzer zum Exportieren einer E-Mail-Nachricht, die als schädlich eingestuft wurde.|
|4|ViewHeader|Hierbei handelt es sich um eine Anforderung von einem Benutzer zum Anzeigen der Kopfzeile einer E-Mail-Nachricht, die als schädlich eingestuft wurde.|
||||

### <a name="enum-requestsource---type-edmint32"></a>Enum: RequestSource - Type: Edm.Int32

|**Wert**|**Elementname**|**Beschreibung**|
|:-----|:-----|:-----|
|0|SCC|Das Security & Compliance Center (SCC) ist die Quelle, von der die Anforderung eines Benutzers stammen kann, eine potenziell gefährliche E-Mail-Nachricht in einer Vorschau anzuzeigen, sie zu löschen, freizugeben, zu exportieren oder ihre Kopfzeile anzuzeigen. |
|1|Cmdlet|Ein Cmdlet ist die Quelle, von der die Anforderung eines Benutzers stammen kann, eine potenziell gefährliche E-Mail-Nachricht in einer Vorschau anzuzeigen, sie zu löschen, freizugeben, zu exportieren oder ihre Kopfzeile anzuzeigen.|
|2|URLlink|Dies ist die Quelle, von der die Anforderung eines Benutzers stammen kann, eine potenziell gefährliche E-Mail-Nachricht in einer Vorschau anzuzeigen, sie zu löschen, freizugeben, zu exportieren oder ihre Kopfzeile anzuzeigen.|
||||

## <a name="microsoft-forms-schema"></a>Microsoft Forms-Schema

Die unter [Durchsuchen des Überwachungsprotokolls im Office 365 Security & Compliance Center](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#microsoft-forms-activities) aufgelisteten Microsoft Forms-Ereignisse verwenden dieses Schema.

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|FormsUserTypes|Collection(Self.[FormsUserTypes](#formsusertypes))|Ja|Die Rolle des Benutzers, der die Aktion ausgeführt hat.  Die Werte für diesen Parameter sind Administrator, Besitzer, Responder oder Mitautor.|
|SourceApp|Edm.String|Ja|Gibt an, ob die Aktion von der Forms-Website oder einer anderen App ausgeführt wird.|
|FormName|Edm.String|Nein|Name des aktuellen Formulars.|
|FormId |Edm.String|Nein|Die ID des Zielformulars.|
|FormTypes|Collection(Self.[FormTypes](#formtypes))|Nein|Gibt an, ob es sich um ein Formular, ein Quiz oder eine Umfrage handelt.|
|ActivityParameters|Edm.String|Nein|JSON-Zeichenfolge mit Aktivitätsparametern. Weitere Informationen finden Sie unter [Durchsuchen des Überwachungsprotokolls im Office 365 Security & Compliance Center](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#microsoft-forms-activities).|
||||

### <a name="enum-formsusertypes---type-edmint32"></a>Enumeration: FormsUserTypes – Typ: Edm.Int32

#### <a name="formsusertypes"></a>FormsUserTypes

|**Wert**|**Formular-Benutzertyp**|**Beschreibung**|
|:-----|:-----|:-----|
|0|Administrator|Ein Administrator, der Zugriff auf das Formular hat.|
|1|Besitzer|Ein Benutzer, der Besitzer des Formulars ist.|
|2|Responder|Ein Benutzer, der eine Antwort auf ein Formular gesendet hat.|
|3|Koautor|Ein Benutzer, der einen Link für die Zusammenarbeit verwendet hat, der vom Besitzer eines Formulars für die Anmeldung und die Bearbeitung eines Formulars bereitgestellt wurde.|
||||

### <a name="enum-formtypes---type-edmint32"></a>Enumeration: FormTypes – Typ: Edm.Int32

#### <a name="formtypes"></a>FormTypes

|**Wert**|**Formulartypen**|**Beschreibung**|
|:-----|:-----|:-----|
|0|Formular|Formulare, die mit der Option "Neues Formular" erstellt wurden.|
|1|Quiz|Quizze, die mit der Option „Neues Quiz“ erstellt wurden.  Bei einem Quiz handelt es sich um eine spezielle Art von Formular, das zusätzliche Funktionen für Punktwerte, automatische und manuelle Benotung, Kommentare usw. enthält.|
|2|Umfrage|Umfragen, die mit der Option "Neue Umfrage" erstellt wurden.  Bei einer Umfrage handelt es sich um eine spezielle Art von Formular, das zusätzliche Funktionen wie CMS-Integration und Unterstützung für Flussregeln enthält.|
||||

## <a name="mip-label-schema"></a>MIP-Bezeichnungsschema

Ereignisse im MIP-Bezeichnungsschema (Microsoft Information Protection) werden ausgelöst, wenn Microsoft 365 eine von Agents in der Transportpipeline verarbeitete E-Mail-Nachricht erkennt, auf die eine Vertraulichkeitsbezeichnung angewendet wurde. Die Vertraulichkeitsbezeichnung wurde kann manuell oder automatisch sowie innerhalb oder außerhalb der Transportpipeline angewendet worden sein. Vertraulichkeitsbezeichnungen können durch Richtlinien für die automatische Anwendung von Bezeichnungen automatisch auf E-Mail-Nachrichten angewendet werden.

Dieses Überwachungsschema dient zur Darstellung der Summe aller E-Mail-Aktivitäten mit Vertraulichkeitsbezeichnungen. Anders ausgedrückt: Für jede E-Mail-Nachricht mit einer Vertraulichkeitsbezeichnung, die an Benutzer oder von Benutzern in der Organisation gesendet wird, sollte es eine aufgezeichnete Überwachungsaktivität geben. Weitere Informationen zu Vertraulichkeitsbezeichnungen finden Sie unter

- [Weitere Informationen zu Vertraulichkeitsbezeichnungen](/microsoft-365/compliance/sensitivity-labels)

- [Automatisches Anwenden einer Vertraulichkeitsbezeichnung auf Inhalte](/microsoft-365/compliance/apply-sensitivity-label-automatically)

|**Parameter**|**Typ**|**Erforderlich?**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Absender|Edm.String|Nein|Die E-Mail-Adresse im Feld "Von" der E-Mail-Nachricht.|
|Empfänger|Collection(Edm.String)|Nein|Alle E-Mail-Adressen in den Feldern "An", "Cc" und "Bcc" der E-Mail-Nachricht.|
|ItemName|Edm.String|Nein|Die Zeichenfolge im Feld "Betreff" der E-Mail-Nachricht.|
|LabelId|Edm.Guid|Nein|Die GUID der auf die E-Mail-Nachricht angewendeten Vertraulichkeitsbezeichnung.|
|LabelName|Edm.String|Nein|Der Name der auf die E-Mail-Nachricht angewendeten Vertraulichkeitsbezeichnung.|
|LabelAction|Edm.String|Nein|Die durch die Vertraulichkeitsbezeichnung angegebenen Aktionen, die vor Eintreten der Nachricht in die E-Mail-Transportpipeline auf die E-Mail-Nachricht angewendet wurden.|
|LabelAppliedDateTime|Edm.Date|Nein|Das Datum, an dem die Vertraulichkeitsbezeichnung auf die E-Mail-Nachricht angewendet wurde.|
|ApplicationMode|Edm.String|Nein|Gibt an, wie die Vertraulichkeitsbezeichnung auf die E-Mail-Nachricht angewendet wurde. Der **Privileged**-Wert gibt an, dass die Bezeichnung manuell von einem Benutzer angewendet wurde. Der Wert **Standard** gibt an, dass die Bezeichnung durch einen clientseitigen oder dienstseitigen Bezeichnungsprozess automatisch angewendet wurde.|
|||||

## <a name="communication-compliance-exchange-schema"></a>Exchange-Schema der Kommunikationscompliance

Die im Office 365-Überwachungsprotokoll aufgeführten Kommunikationscompliance-Ereignisse verwenden dieses Schema. Dazu gehören Überwachungsdatensätze für den **SupervisoryReviewOLAudit**-Vorgang, der generiert wird, wenn der Inhalt der E-Mail-Nachricht anstößige Sprache enthält, die von Antispammodellen mit einer Übereinstimmungsgenauigkeit von \>= 99,5% erkannt wurde.

|**Parameter**  |**Typ**|**Erforderlich?** |**Beschreibung**|
|:---------------|:-------|:--------------|:--------------|
| ExchangeDetails |[ExchangeDetails](#exchangedetails)|Nein|Eigenschaften der E-Mail-Nachricht, die das SupervisoryReviewOLAudit-Ereignis ausgelöst hat.|
|||||

### <a name="enum-exchangedetails---type-exchangedetails"></a>Enum: ExchangeDetails – Type: ExchangeDetails

#### <a name="exchangedetails"></a>ExchangeDetails

| **Elementname**   | **Type**| **Beschreibung**|
|:----------------- | :-------|:---------------|
| NetworkMessageId  |Edm.Guid|Die Netzwerknachrichten-ID der E-Mail-Nachricht.|
| InternetMessageId |Edm.String|Die Internetnachrichten-ID der E-Mail-Nachricht.|
| AttachmentData|Collection([AttachmentDetails](#attachmentdetails))|Informationen zu Dateien, die an die E-Mail-Nachricht angefügt sind.|
| Empfänger|Collection(Edm.String)|Die E-Mail-Adressen in den Feldern "An", "Cc" und "Bcc" der E-Mail-Nachricht. |
| Betreff|Edm.String|Der Text im Feld "Betreff" der E-Mail-Nachricht.|
| MessageTime|Edm.Date|Das Datum und die Uhrzeit, zu der die E-Mail-Nachricht gesendet wurde.|
| Von| Edm.String|Die E-Mail-Adresse im Feld "Von" der E-Mail-Nachricht.|
| Directionality|Edm.String|Der Herkunftsstatus der E-Mail-Nachricht.|
||||

### <a name="enum-attachmentdetails---type-edmint32"></a>Enum: AttachmentDetails – Type: Edm.Int32

#### <a name="attachmentdetails"></a>AttachmentDetails

| **Elementname** | **Type**   | **Beschreibung**|
|:--------------- |:---------- | :--------------|
| FileName        | Edm.String | Der Name der an die E-Mail-Nachricht angefügten Datei.|
| FileType        | Edm.String | Die Dateierweiterung der an die E-Mail-Nachricht angefügten Datei.|
| SHA256          | Edm.String | Der SHA-256-Hash der an die E-Mail-Nachricht angefügten Datei.|
||||
