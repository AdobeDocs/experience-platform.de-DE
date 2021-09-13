---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: e9d5f24bec8cd2793ce30245b46c1d912bf17cc7
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 35%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: 25. August 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Ziele](#destinations)
- [Observability Insights](#observability)
- [Echtzeit-Kundenprofil](#profile)
- [Quellen](#sources)

## Ziele {#destinations}

Ziele sind vordefinierte Integrationen mit Zielplattformen, die die nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | Das zuvor in der Beta-Version enthaltene Ziel für Airship Attributes ist jetzt allgemein verfügbar. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | Das zuvor in der Beta-Phase befindliche Airship Tags-Ziel ist jetzt allgemein verfügbar. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | Das zuvor in der Betaphase enthaltene Ziel Braze ist jetzt allgemein verfügbar. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Mit dem Pinterest-Ziel &quot;Kundenliste&quot;können Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen erstellen, die bereits mit Ihren Inhalten in Pinterest interagiert haben. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Richten Sie Ihre bestehenden Follower und Kunden in Twitter ein und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen aktivieren. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX ist eine aggregierte Verizon Media-/Yahoo-Infrastruktur, die verschiedene Komponenten hostet, mit denen Verizon Media/Yahoo Daten mit externen Partnern auf sichere, automatisierte und skalierbare Weise austauschen kann. |

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Das Adobe Experience Platform Destination SDK ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für die Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. Die Konfigurationen werden in Experience Platform gespeichert und können über API für zusätzliche Aktualisierungen abgerufen werden. |
| [Verbesserungen der Benutzerfreundlichkeit für Ziele](../../destinations/ui/activation-overview.md) | Dank Verbesserungen der Benutzerfreundlichkeit an Zielen können Marketing-Experten Segmente nahtlos für vorhandene Ziele aktivieren. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Observability Insights {#observability}

Observability Insights ermöglicht es Ihnen, Platform-Aktivitäten mithilfe statistischer Metriken und Ereignisbenachrichtigungen zu überwachen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Warnhinweise | Sie können nun wichtige Warnhinweise zu Workflows abonnieren, die auf Platform ausgeführt werden. Nach dem Abonnieren bestimmter Warnungsregeln erhalten Sie Benachrichtigungen und E-Mails in der Benutzeroberfläche, wenn ein wichtiges Lebenszyklusereignis auftritt (z. B. bei erfolgreicher Datenerfassung) oder wenn Probleme auftreten, die Ihre Aufmerksamkeit erfordern (z. B. ein Fehler bei der Aufnahme oder ein länger als erwartet dauernder Segmentauftrag). Weitere Informationen finden Sie unter [Warnhinweise - Übersicht](../../observability/alerts/overview.md). |

Weitere Informationen zum Dienst finden Sie unter [Übersicht über Observability Insights](../../observability/home.md) .

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen und anderen Kanälen miteinander kombiniert. Mit Profil können Sie Kundendaten in einer einheitlichen Ansicht zusammenfassen, die eine umsetzbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Profile nach Zusammenführungsrichtlinie oder Identität durchsuchen | Beim Durchsuchen von Profilen in Experience Platform können Sie jetzt nach Zusammenführungsrichtlinien suchen, um anhand der ausgewählten Zusammenführungsrichtlinie eine Vorschau von 20 Beispielprofilen anzuzeigen. Sie können auch nach Identität suchen, um mithilfe eines Identitäts-Namespace und des zugehörigen Identitätswerts nach einem bestimmten Profil zu suchen. Weitere Informationen finden Sie im Handbuch [Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md). |

Um mehr über das Echtzeit-Kundenprofil zu erfahren, einschließlich Tutorials und Best Practices für die Arbeit mit Profildaten, lesen Sie zunächst die [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| ------- | ----------- |
| Quell-Connector für lokales Hochladen von Dateien | Die Kategorie der Dateierfassung wurde in ein lokales System umbenannt, sodass Sie lokale Dateien über den lokalen Dateiupload-Connector direkt in Platform übertragen können. Die über diesen Connector erfassten Daten können über das Monitoring-Dashboard überwacht werden. Weitere Informationen finden Sie unter [Übersicht über die lokale Datei-Upload-Quelle](../../sources/connectors/local-system/local-file-upload.md) . |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
