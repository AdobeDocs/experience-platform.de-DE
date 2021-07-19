---
keywords: Experience Platform; Startseite; beliebte Themen; Datenerfassung; erfasste Daten; Streaming; Übersicht; Streaming-Erfassung; Latenz; Streaming-Latenz; Streaming-Latenz;
solution: Experience Platform
title: Streaming-Erfassung - Übersicht
topic-legacy: overview
description: Die Streaming-Erfassung für Adobe Experience Platform bietet Benutzern eine Methode, Daten von Client- und Server-seitigen Geräten in Echtzeit an die Experience Platform zu senden.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 23%

---

# Streaming-Erfassung – Übersicht

Die Streaming-Erfassung für Adobe Experience Platform bietet Benutzern eine Methode, Daten von Client- und Server-seitigen Geräten in Echtzeit an [!DNL Experience Platform] zu senden.

## Was können Sie mit Streaming-Erfassung tun?

Mit Adobe Experience Platform können Sie koordinierte, konsistente und relevante Erlebnisse durch Generieren eines [!DNL Real-time Customer Profile]-Werts für jeden Ihrer Kunden bereitstellen. Die Streaming-Erfassung spielt eine Schlüsselrolle beim Erstellen dieser Profile, indem Sie [!DNL Profile]-Daten mit so wenig Latenz wie möglich an [!DNL Data Lake] übermitteln können.

Das folgende Video soll Ihnen dabei helfen, die Streaming-Erfassung zu verstehen, und beschreibt die oben genannten Konzepte.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Profildatensätze und streamen[!DNL ExperienceEvents]

Mit der Streaming-Erfassung können Benutzer Profildatensätze und [!DNL ExperienceEvents] in Sekunden bis [!DNL Platform] streamen, um die Echtzeit-Personalisierung zu fördern. Alle an Streaming-Aufnahme-APIs gesendeten Daten werden automatisch im [!DNL Data Lake] beibehalten.

Weiterführende Informationen finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

### An Datensätze streamen

Sobald Sie sicher sind, dass Ihre Daten sauber sind, können Sie Ihre Datensätze für [!DNL Real-time Customer Profile] und [!DNL Identity Service] aktivieren.

Weitere Informationen zum Aktivieren eines Datensatzes für [!DNL Profile] und [!DNL Identity Service] finden Sie im [Konfigurieren eines Datensatzhandbuchs](../../profile/tutorials/dataset-configuration.md).

## Wie hoch ist die erwartete Latenz für die Streaming-Erfassung auf [!DNL Platform]?

| Ziel | Erwartete Latenz |
| --------- | ---------------- |
| Echtzeit-Kundenprofil | &lt; 1 Minute |
| Data Lake | &lt; 60 Minuten |

## Adobe Experience Platform-Erweiterung

Mit der Adobe Experience Platform-Erweiterung können Sie eine neue Streaming-Verbindung einrichten. Die [!DNL Experience Platform]-Erweiterung bietet Aktionen zum Senden von Beacons, die in [!DNL Experience Data Model] (XDM) formatiert sind, für die Echtzeit-Erfassung zu [!DNL Experience Platform]. Weiterführende Informationen finden Sie in der Dokumentation zur [Experience Platform-Erweiterung](../../tags/extensions/web/sdk/overview.md).
