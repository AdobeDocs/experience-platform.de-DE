---
keywords: Experience Platform; home; beliebte Themen; Datenerfassung; erfasste Daten; Streaming; Übersicht; Streaming-Erfassung; Latenz; Streaming-Latenz; Streaming-Latenz;
solution: Experience Platform
title: Streaming-Erfassung - Überblick
description: Streaming-Erfassung für Adobe Experience Platform bietet Benutzern eine Methode, Daten von Client- und Server-seitigen Geräten in Echtzeit an Experience Platform zu senden.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 008537dffff4cc428de9070964446f4e7ebf039f
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 18%

---

# Streaming-Erfassung – Übersicht

Die Streaming-Erfassung für Adobe Experience Platform bietet Benutzern eine Methode zum Senden von Daten von Client- und Server-seitigen Geräten an [!DNL Experience Platform] in Echtzeit.

## Was können Sie mit Streaming-Erfassung tun?

Mit Adobe Experience Platform können Sie koordinierte, konsistente und relevante Erlebnisse durch Generieren einer [!DNL Real-Time Customer Profile] für jeden Ihrer Kunden. Die Streaming-Erfassung spielt bei der Erstellung dieser Profile eine wichtige Rolle, da Sie die Bereitstellung von [!DNL Profile] Daten in die [!DNL Data Lake] mit möglichst wenig Latenz.

Das folgende Video soll Ihnen dabei helfen, die Streaming-Erfassung zu verstehen, und beschreibt die oben genannten Konzepte.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Profildatensätze und streamen[!DNL ExperienceEvents]

Mit der Streaming-Erfassung können Benutzer Profildatensätze streamen und [!DNL ExperienceEvents] nach [!DNL Platform] in Sekunden, um die Echtzeit-Personalisierung zu fördern. Alle an Streaming-Aufnahme-APIs gesendeten Daten werden automatisch in der Variablen [!DNL Data Lake].

Weiterführende Informationen finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

### An Datensätze streamen

Sobald Sie sicher sind, dass Ihre Daten sauber sind, können Sie Ihre Datensätze für [!DNL Real-Time Customer Profile] und [!DNL Identity Service].

Weitere Informationen zum Aktivieren eines Datensatzes für [!DNL Profile] und [!DNL Identity Service], lesen Sie bitte die [Datensatz-Handbuch konfigurieren](../../profile/tutorials/dataset-configuration.md).

## Wie hoch ist die erwartete Latenz für die Streaming-Erfassung in [!DNL Platform]?

| Ziel | Erwartete Latenz |
| --------- | ---------------- |
| Echtzeit-Kundenprofil | &lt; 1 Minute |
| Data Lake | &lt; 60 Minuten |

## Anleitung für Anfragen pro Sekunden (RPS) bei der Streaming-Erfassung

In der folgenden Tabelle finden Sie Anleitungen zur Anforderung pro Sekunden für die Streaming-Erfassung.

| RPS-Limit | Anmerkungen |
| --- | --- |
| 1000 Anfragen pro Sekunde | Diese können bei Verwendung von `/collection/batch` -Endpunkt. |
| 10000 Einzelnachrichten pro Sekunde | Die Nachrichten können bei Verwendung der `/collection/batch` -Endpunkt. |

>[!IMPORTANT]
>
>Das erzwungene Limit wird **60 Anfragen pro Minute** bei der Verwendung der synchronen Validierung, da sie für Debugging-Zwecke vorgesehen ist.

## Adobe Experience Platform-Erweiterung

Mit der Adobe Experience Platform-Erweiterung können Sie eine neue Streaming-Verbindung einrichten. Die [!DNL Experience Platform] Erweiterung bietet Aktionen zum Senden von Beacons, die in [!DNL Experience Data Model] (XDM) für die Echtzeit-Erfassung in [!DNL Experience Platform]. Weiterführende Informationen finden Sie in der Dokumentation zur [Experience Platform-Erweiterung](../../tags/extensions/client/web-sdk/overview.md).
