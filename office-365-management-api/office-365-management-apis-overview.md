---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Management APIs overview
title: Übersicht über die Office 365-Verwaltungs-APIs
description: Bietet eine einzelne Erweiterbarkeitsplattform für alle Verwaltungsaufgaben von Office 365-Kunden und -Partnern, einschließlich Dienstkommunikation, Sicherheit, Compliance, Berichterstattung und Überwachung.
ms.ContentId: 4fca85f9-efa6-3b4b-b10d-a07cb31f803f
ms.topic: reference (API)
ms.date: 09/28/2016
ms.localizationpriority: high
ms.openlocfilehash: 52924d518dd74f822a61977d96c5edbb7fc1e888
ms.sourcegitcommit: 13b50617b1a73f5890414087d8eabe6b2240cfb4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2021
ms.locfileid: "58510111"
---
# <a name="office-365-management-apis-overview"></a>Übersicht über die Office 365-Verwaltungs-APIs

Die Office 365-Verwaltungs-APIs bieten eine einzelne Erweiterbarkeitsplattform für alle Verwaltungsaufgaben von Office 365-Kunden und -Partnern, einschließlich Dienstkommunikation, Sicherheit, Compliance, Berichterstattung und Überwachung. Alle Office 365-Verwaltungs-APIs sind in Entwurf und Implementierung mit der aktuellen Suite von Office 365 REST-APIs einheitlich, entsprechend den branchenüblicher Ansätze wie OAuth v2, OData v4 und JSON. Wie bei anderen Office 365-APIs werden Anwendungen in Azure Active Directory registriert, sodass Entwickler eine konsistente Möglichkeit zum Authentifizieren und Autorisieren ihrer Apps haben.

Wenn Sie Fragen zu den Office 365-Verwaltungs-APIs haben, posten Sie Ihre Frage auf [Stack Overflow](http://stackoverflow.com/tags/office365) mit dem Tag [Office 365].

## <a name="office-365-service-communications-api-preview"></a>Office 365-Dienstkommunikations-API (Vorschau)

Die Office 365-Dienstkommunikations-API wurde im Vorschaumodus veröffentlicht. Sie ersetzt die Office 365-Dienstkommunikations-API und bietet Informationen zum Dienststatus für Mandantenadministratoren und Partner. Im Gegensatz zur vorherigen Version bietet die neue Dienstkommunikations-API eine einheitliche Plattformumgebung, in der REST-APIs konsistent eingebunden sind, einschließlich URL-Benennung, Datenformat und Authentifizierung.

Neue Features werden nur zur neuen Version der API hinzugefügt, um die Übernahme durch Kunden, die bereits die ältere Version verwenden, zu fördern. Bei der allgemeinen Ankündigung der Office 365-Dienstkommunikations-API begann gleichzeitig die Außerbetriebnahme der älteren Version der Dienstkommunikations-API. 

Die Betriebsreferenz finden Sie unter [Office 365-Dienstkommunikations-API – Referenz (Vorschau)](office-365-service-communications-api-reference.md).


## <a name="office-365-management-activity-api"></a>Office 365-Verwaltungsaktivitäts-API

Die Office 365-Verwaltungsaktivitäts-API bietet Informationen über verschiedene Benutzer-, Verwaltungs-, System- und Richtlinienaktionen und -ereignisse aus Office 365 und Azure Active Directory-Aktivitätsprotokollen. Kunden und Partner können diese Informationen zum Erstellen neuer Betriebs-, Sicherheits- und Compliance-Überwachungslösungen für das Unternehmen nutzen oder bestehene Lösungen verbessern. 

Die Betriebsreferenz finden Sie unter [Office 365-Verwaltungsaktivitäts-API – Referenz](office-365-management-activity-api-reference.md).

## <a name="see-also"></a>Siehe auch

- [Erste Schritte mit den Office 365-Verwaltungs-APIs](get-started-with-office-365-management-apis.md)
- [Office 365-Verwaltungsaktivitäts-API –Schema](office-365-management-activity-api-schema.md)
- [Problembehandlung bei der Office 365-Verwaltungsaktivitäts-API](troubleshooting-the-office-365-management-activity-api.md)
- [Office 365-REST-APIs](/previous-versions/office/office-365-api/how-to/platform-development-overview)
