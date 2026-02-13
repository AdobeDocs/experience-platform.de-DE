---
keywords: Experience Platform;Startseite;beliebte Themen;Datenaufnahme;aufgenommene Daten;Streaming;Übersicht;Streaming-Aufnahme;Latenz;Streaming-Latenz
solution: Experience Platform
title: Überblick über den Import von Streamingdaten
description: Erfahren Sie mehr über die Streaming-Aufnahme in Adobe Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 568208c9b2cb774bbbeed74ae2d456c87e99bca9
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 15%

---

# Streaming-Aufnahme – Übersicht

Die Streaming-Aufnahme für Adobe Experience Platform bietet Benutzenden eine Methode, um Daten von Client- und Server-seitigen Geräten in Echtzeit an Experience Platform zu senden.

## Was können Sie mit Streaming-Aufnahme tun?

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse, indem für jeden einzelnen Ihrer Kunden ein Echtzeit-Kundenprofil erstellt wird. Die Streaming-Aufnahme spielt eine wichtige Rolle beim Erstellen dieser Profile, da Sie Profildaten mit möglichst geringer Latenz in den Data Lake senden können.

Das folgende Video soll Ihnen dabei helfen, die Streaming-Aufnahme zu verstehen, und umreißt die oben genannten Konzepte.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Streamen von Profildatensätzen und [!DNL ExperienceEvents]

Mit der Streaming-Aufnahme können Benutzende Profildatensätze streamen und in Sekundenschnelle an Experience Platform [!DNL ExperienceEvents], um die Echtzeit-Personalisierung zu fördern. Alle Daten, die an Streaming-Aufnahme-APIs gesendet werden, werden automatisch im Data Lake beibehalten.

Weiterführende Informationen finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

### An Datensätze streamen

Sobald Sie sicher sind, dass Ihre Daten sauber sind, können Sie Ihre Datensätze für das Echtzeit-Kundenprofil und [!DNL Identity Service] aktivieren.

Weitere Informationen zum Aktivieren eines Datensatzes für Profil und [!DNL Identity Service] finden Sie im [Handbuch zum Konfigurieren eines Datensatzes](/help/profile/tutorials/dataset-configuration.md).

## Wie hoch ist die erwartete Latenz für die Streaming-Aufnahme in Experience Platform?

>[!IMPORTANT]
>
>Leitplanken für die Streaming-Aufnahme sind an die gesamte Lizenznutzungsberechtigung gebunden, die Ihrer gesamten Organisation entspricht. Darüber hinaus ist die Datennutzung in Entwicklungs-Sandboxes auf 10 % Ihrer gesamten Profile beschränkt. Weitere Informationen zu Lizenznutzungsberechtigungen finden Sie im [Handbuch zu Best Practices für die Datenverwaltung](/help/landing/license-usage-and-guardrails/data-management-best-practices.md). Informationen zum Festlegen von Beschränkungen für Ihren Streaming-Durchsatz finden Sie unter [Kapazitätsübersicht](../../landing/license-usage-and-guardrails/capacity.md).

| Ziel | Erwartete Latenz |
| --------- | ---------------- |
| Echtzeit-Kundenprofil | <ul><li>&lt; 15 Minuten beim 95. Perzentil für die B2C-Datenaufnahme.</li><li>&lt; 30 Minuten beim 95. Perzentil für die B2B-Datenaufnahme.</li></ul> |
| Data Lake | &lt; 60 Minuten |

## Anleitung pro Sekunde (RPS) für die Streaming-Aufnahme

In der folgenden Tabelle finden Sie Anleitungen zu den Beschränkungen der Anfrage pro Sekunde für die Streaming-Aufnahme.

| RPS-Grenzwert | Anmerkungen |
| --- | --- |
| 1.000 Anfragen pro Sekunde | Diese können bei Verwendung `/collection/batch` Endpunkts mehrere Nachrichten enthalten. |
| Einzelne Nachrichten pro Sekunde 10000 | Die Nachrichten können bei Verwendung des `/collection/`-Endpunkts in weniger Anfragen gruppiert werden. |

>[!IMPORTANT]
>
>Das erzwungene Limit beträgt **60 Anfragen pro Minute** wenn synchrone Validierung verwendet wird, da dies zu Debugging-Zwecken vorgesehen ist.

## Adobe Experience Platform-Erweiterung

Mit der Adobe Experience Platform-Erweiterung können Sie eine neue Streaming-Verbindung einrichten. Die [!DNL Experience Platform]-Erweiterung bietet Aktionen zum Senden von Beacons, die in [!DNL Experience Data Model] (XDM) für die Echtzeitaufnahme formatiert sind, an [!DNL Experience Platform]. Weiterführende Informationen finden Sie in der Dokumentation zur [Experience Platform-Erweiterung](/help/tags/extensions/client/web-sdk/overview.md).
