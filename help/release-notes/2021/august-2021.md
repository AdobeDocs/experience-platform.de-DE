---
title: Adobe Experience Platform – Versionshinweise August 2021
description: Versionshinweise August 2021 für Adobe Experience Platform.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 98%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 25. August 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Ziele](#destinations)
- [Observability Insights](#observability)
- [Echtzeit-Kundenprofil](#profile)
- [Quellen](#sources)

## Ziele {#destinations}

Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | Das zuvor in der Betaphase befindliche Ziel „Airship Attributes“ ist jetzt allgemein verfügbar. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | Das zuvor in der Betaphase befindliche Ziel „Airship Tags“ ist jetzt allgemein verfügbar. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | Das zuvor in der Betaphase befindliche Ziel „Braze“ ist jetzt allgemein verfügbar. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Mit dem Pinterest-Ziel „Kundenliste“ können Sie aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten auf Pinterest interagiert haben, Zielgruppen erstellen. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Sprechen Sie Ihre bestehenden Follower und Kunden auf Twitter an und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen aktivieren. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX ist eine aggregierte Infrastruktur von Verizon Media/Yahoo, die verschiedene Komponenten hostet, mit denen Verizon Media/Yahoo Daten mit externen Partnern auf sichere, automatisierte und skalierbare Weise austauschen kann. |

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Das Adobe Experience Platform Destination SDK ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden. |
| [Verbesserungen der Benutzerfreundlichkeit für Ziele](../../destinations/ui/activation-overview.md) | Dank Verbesserungen der Benutzerfreundlichkeit für Ziele können Marketing-Experten Segmente nahtlos für vorhandene Ziele aktivieren. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Observability Insights {#observability}

Mit Observability Insights können Sie Platform-Aktivitäten mithilfe von statistischen Metriken und Ereignisbenachrichtigungen überwachen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Warnhinweise | Sie können jetzt wichtige Warnhinweise zu Arbeitsabläufen abonnieren, die auf Platform ausgeführt werden. Nach dem Abonnieren bestimmter Warnhinweisregeln erhalten Sie in der Benutzeroberfläche Benachrichtigungen und E-Mails, wenn ein wichtiges Lebenszyklusereignis auftritt (z. B. bei erfolgreicher Datenerfassung) oder wenn Probleme auftreten, die Ihre Aufmerksamkeit erfordern (z. B. ein Fehler bei der Aufnahme oder ein länger als erwartet dauernder Segmentauftrag). Weiterführende Informationen finden Sie in der [Übersicht zu Warnhinweisen](../../observability/alerts/overview.md). |

Weitere Informationen zu dem Service finden Sie in der [Übersicht zu Observability Insights](../../observability/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Durchsuchen von Profilen nach Zusammenführungsrichtlinie oder Identität | Beim Durchsuchen von Profilen in Experience Platform können Sie jetzt nach Zusammenführungsrichtlinien suchen, um anhand der ausgewählten Zusammenführungsrichtlinie eine Vorschau von 20 Beispielprofilen anzuzeigen. Sie können auch nach Identität suchen, um mithilfe eines Identitäts-Namespace und des zugehörigen Identitätswerts nach einem bestimmten Profil zu suchen. Weitere Informationen finden Sie unter [Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md). |

Weitere Informationen zum Echtzeit-Kundenprofil, einschließlich Tutorials und Best Practices für die Arbeit mit Profildaten, finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| ------- | ----------- |
| Quell-Connector für den Upload lokaler Dateien | Die Kategorie der Dateiaufnahme wurde in ein lokales System umbenannt, sodass Sie lokale Dateien über den Connector zum Upload lokaler Dateien direkt in Platform übertragen können. Die über diesen Connector erfassten Daten können über das Monitoring-Dashboard überwacht werden. Weitere Informationen finden Sie in der [Übersicht über die Quelle für den Upload lokaler Dateien](../../sources/connectors/local-system/local-file-upload.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
