---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 3d6402a35e1813b94af866d7aaea975d4f103906
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 44%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: 25. August 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Observability Insights](#observability)
- [Echtzeit-Kundenprofil](#profile)
- [Quellen](#sources)

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
