---
keywords: Experience Platform;Startseite;beliebte Themen;Datenaufnahme;aufgenommene Daten;Streaming;Übersicht;Streaming-Aufnahme;Latenz;Streaming-Latenz
solution: Experience Platform
title: Überblick über den Import von Streamingdaten
description: Die Streaming-Aufnahme für Adobe Experience Platform bietet Benutzenden eine Methode, um Daten von Client- und Server-seitigen Geräten in Echtzeit an Experience Platform zu senden.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: f5ae9170b312d9f24c863a14b8cc2310fcaf1cb2
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 15%

---

# Streaming-Erfassung – Übersicht

Die Streaming-Aufnahme für Adobe Experience Platform bietet Benutzenden eine Methode, um Daten von Client- und Server-seitigen Geräten in Echtzeit an [!DNL Experience Platform] zu senden.

## Was können Sie mit Streaming-Erfassung tun?

Adobe Experience Platform ermöglicht es Ihnen, koordinierte, konsistente und relevante Erlebnisse zu erzielen, indem es für jede einzelne Kundin und jeden einzelnen Kunden einen [!DNL Real-Time Customer Profile] generiert. Die Streaming-Aufnahme spielt eine wichtige Rolle bei der Erstellung dieser Profile, da Sie [!DNL Profile] Daten mit möglichst geringer Latenz an die [!DNL Data Lake] senden können.

Das folgende Video soll Ihnen dabei helfen, die Streaming-Aufnahme zu verstehen, und umreißt die oben genannten Konzepte.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Streamen von Profildatensätzen und [!DNL ExperienceEvents]

Mit der Streaming-Aufnahme können Benutzer Profildatensätze streamen und in Sekunden in [!DNL ExperienceEvents] [!DNL Experience Platform], um die Echtzeit-Personalisierung zu fördern. Alle Daten, die an Streaming-Aufnahme-APIs gesendet werden, bleiben automatisch im [!DNL Data Lake] erhalten.

Weiterführende Informationen finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

### An Datensätze streamen

Sobald Sie sicher sind, dass Ihre Daten sauber sind, können Sie Ihre Datensätze für [!DNL Real-Time Customer Profile] und [!DNL Identity Service] aktivieren.

Weitere Informationen zum Aktivieren eines Datensatzes für [!DNL Profile] und [!DNL Identity Service] finden Sie im [Handbuch zum Konfigurieren eines Datensatzes](../../profile/tutorials/dataset-configuration.md).

## Wie hoch ist die erwartete Latenz für die Streaming-Aufnahme in Experience Platform?

>[!IMPORTANT]
>
>Leitplanken für die Streaming-Aufnahme sind an die gesamte Lizenznutzungsberechtigung gebunden, die Ihrer gesamten Organisation entspricht. Darüber hinaus ist die Datennutzung in Entwicklungs-Sandboxes auf 10 % Ihrer gesamten Profile beschränkt. Weitere Informationen zu Lizenznutzungsberechtigungen finden Sie im [Handbuch zu Best Practices für die Datenverwaltung](../../landing/license-usage-and-guardrails/data-management-best-practices.md). Informationen zum Festlegen von Beschränkungen für Ihren Streaming-Durchsatz finden Sie unter [Kapazitätsübersicht](../../landing/license-usage-and-guardrails/capacity.md).

| Ziel | Erwartete Latenz |
| --------- | ---------------- |
| Echtzeit-Kundenprofil | &lt; 15 Minuten beim 95. Perzentil |
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

Mit der Adobe Experience Platform-Erweiterung können Sie eine neue Streaming-Verbindung einrichten. Die [!DNL Experience Platform]-Erweiterung bietet Aktionen zum Senden von Beacons, die in [!DNL Experience Data Model] (XDM) für die Echtzeitaufnahme formatiert sind, an [!DNL Experience Platform]. Weiterführende Informationen finden Sie in der Dokumentation zur [Experience Platform-Erweiterung](../../tags/extensions/client/web-sdk/overview.md).
