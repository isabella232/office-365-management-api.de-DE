---
ms.TocTitle: Office 365 Management Activity API frequently asked questions
title: Office 365-Verwaltungsaktivitäts-API – Häufig gestellte Fragen
description: Häufig gestellte Fragen zur Verwendung der Office 365-Verwaltungsaktivitäts-API
ms.ContentId: ''
ms.topic: reference (API)
ms.date: 09/21/2018
ms.openlocfilehash: 8118f44b04beedf33e98edd5ebc63c85b8c0fbc5
ms.sourcegitcommit: a5a60b603acd9a17d7717420e377d5760e08c7da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2018
ms.locfileid: "27240624"
---
# <a name="office-365-management-activity-api-frequently-asked-questions"></a>Office 365-Verwaltungsaktivitäts-API – Häufig gestellte Fragen

#### <a name="what-events-are-audited-for-a-specific-office-365-service"></a>Welche Ereignisse werden für einen bestimmten Office 365-Dienst überwacht?

Die Dokumentation für das Office 365-Verwaltungsaktivitäts-API-Schema enthält eine umfassende Liste der Ereignisse. Einzelheiten hierzu finden Sie unter [Office 365-Verwaltungsaktivitäts-API – Schema](office-365-management-activity-api-schema.md).

#### <a name="how-do-i-onboard-to-the-management-activity-api"></a>Wie kann ich die Verwaltungsaktivitäts-API nutzen?

Informationen zu den ersten Schritten mit der Office 365-Verwaltungsaktivitäts-API finden Sie unter [Erste Schritte mit den Office 365-Verwaltungs-APIs](get-started-with-office-365-management-apis.md).
 
#### <a name="what-is-the-throttling-limit-for-the--management-activity-api"></a>Was ist der Einschränkungsgrenzwert für die Verwaltungsaktivitäts-API?

Der aktuelle Einschränkungsgrenzwert beträgt 60.000 Anforderungen/Minute pro Verleger-ID. 

#### <a name="we-want-to-programmatically-capture-all-events-in-all-workloads-what-is-the-most-reliable-way-to-do-this"></a>Wir möchten alle Ereignisse in allen Arbeitslasten programmgesteuert erfassen. Was ist die zuverlässigste Möglichkeit dafür?

Sie können dies mithilfe der Office 365-Verwaltungsaktivitäts-API tun. Außerdem wird empfohlen, aufgrund von Problemen bei der Verwendung von Webhooks das **Pull-Modell** zu verwenden. Weitere Informationen finden Sie im Abschnitt „Verwenden von Webhooks“ in [Problembehandlung bei der Office 365-Verwaltungsaktivitäts-API](troubleshooting-the-office-365-management-activity-api.md#using-webhooks).

#### <a name="is-it-true-that-mailbox-auditing-in-exchange-online-can-only-be-enabled-by-using-powershell"></a>Trifft es zu, dass die Postfachüberwachung in Exchange Online nur mit PowerShell aktiviert werden kann?

Ja. Wir arbeiten jedoch daran, die Postfachüberwachung standardmäßig für alle Postfächer in einer Office 365-Organisation zu aktivieren. Weitere Informationen finden Sie unter „Exchange-Postfachüberwachung wird standardmäßig aktiviert“ im [Microsoft-Blog für Sicherheit, Datenschutz und Compliance](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Exchange-Mailbox-Auditing-will-be-enabled-by-default/ba-p/215171).

#### <a name="are-there-any-differences-in-the-records-that-are-fetched-by-the-management-activity-api-versus-the-records-that-are-returned-by-using-the-audit-log-search-tool-in-the-office-365-security--compliance-center"></a>Gibt es Unterschiede in den Datensätzen, die von der Verwaltungsaktivitäts-API abgerufen werden, und den Datensätzen, die mit dem Überwachungsprotokoll-Suchtool im Office 365 Security & Compliance Center zurückgegeben werden?

Von beiden Methoden werden identische Daten zurückgegeben. Es erfolgt keine Filterung. Der einzige Unterschied besteht darin, dass Sie mit der API Daten für die letzten 7 Tage gleichzeitig abrufen können. Wenn Sie das Überwachungsprotokoll im Security & Compliance Center durchsuchen (oder das entsprechende Cmdlet [Search-UnifiedAuditLog](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance-audit/search-unifiedauditlog) in Exchange Online verwenden), können Sie Daten für die letzten 90 Tage abrufen. 
 
#### <a name="arent-webhook-notifications-more-immediate-after-all-arent-they-event-driven"></a>Sind Webhook-Benachrichtigungen nicht unmittelbarer? Sind sie nicht ereignisgesteuert?

Nein. Webhook-Benachrichtigungen sind nicht in dem Sinn ereignisgesteuert, dass das Ereignis die Benachrichtigung auslöst. Das Inhalts-Blob muss weiterhin erstellt werden, und die Erstellung des Inhalts-Blobs löst die Benachrichtigungsübermittlung aus. In letzter Zeit waren die Wartezeiten für Benachrichtigungen bei Verwendung eines Webhooks länger als beim direkten Abfragen der API mit dem Vorgang */content*. Daher sollte die Verwaltungsaktivitäts-API nicht als Echtzeit-Sicherheitsalarmsystem betrachtet werden. Dafür hat Microsoft andere Produkte. Wenn es um die Sicherheit geht, können Ereignisbenachrichtigungen der Verwaltungsaktivitäts-API besser zum Ermitteln von Verwendungsmustern über längere Zeiträume verwendet werden.

#### <a name="when-pulling-the-data-from-the-management-activity-api-there-is-sometimes-a-delay-of-more-than-3-to-5-days-why-is-this"></a>Wenn die Daten von der Verwaltungsaktivitäts-API abgerufen werden, besteht manchmal eine Verzögerung von mehr als 3 bis 5 Tagen. Wie kommt das?

Manchmal gibt es einen temporären Ausfall oder andere Probleme in den Office 365-Diensten. In diesen Fällen werden einige Überwachungsdatensätze gelöscht, und der Dienst versucht, sie abzugleichen. Obwohl dies nur für ungefähr 5 bis 10 % der Datensätze geschieht, werden diese Datensätze in bestimmten Situationen möglicherweise verzögert. Wenn die Verzögerung mehr als 5 Tage beträgt, überprüfen Sie das Service Health Dashboard im Office 365 Admin Center. Bei Bedarf können Sie auch ein Ticket beim [Microsoft-Support](https://support.office.com/article/contact-support-for-business-products-admin-help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b#ID0EAADAAA=online) öffnen.

#### <a name="im-encountering-a-throttling-error-in-the-management-activity-api-what-should-i-do"></a>In der Verwaltungsaktivitäts-API tritt ein Einschränkungsfehler auf. Was soll ich machen?

Öffnen Sie ein Ticket beim [Microsoft-Support](https://support.office.com/article/contact-support-for-business-products-admin-help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b#ID0EAADAAA=online), fordern Sie einen neuen Einschränkungsgrenzwert an, und geben Sie dabei eine geschäftliche Begründung für die Erhöhung des Grenzwerts an. Die Anforderung wird ausgewertet, und wenn sie akzeptiert wird, wird der Einschränkungsgrenzwert erhöht.

#### <a name="what-happens-if-i-disable-auditing-for-my-office-365-organization-will-i-still-get-events-via-the-management-activty-api"></a>Was passiert, wenn ich für meine Office 365-Organisation die Überwachung deaktiviere? Erhalte ich weiterhin Ereignisse über die Verwaltungsaktivitäts-API?

Nein. Die Überwachung muss für Ihre Organisation sein, damit Datensätze über die Verwaltungsaktivitäts-API abgerufen werden können.

