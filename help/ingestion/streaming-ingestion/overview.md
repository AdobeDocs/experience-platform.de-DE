---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming-Erfassung für Adobe Experience Platform – Übersicht
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 32%

---


# Übersicht über Streaming-Erfassung

Streaming ingestion for Adobe Experience Platform provides users a method to send data from client and server-side devices to [!DNL Experience Platform] in real-time.

## Was können Sie mit Streaming-Erfassung tun?

Adobe Experience Platform enables you to drive coordinated, consistent, and relevant experiences by generating a [!DNL Real-time Customer Profile] for each of your individual customers. Streaming ingestion plays a key role in building these profiles by enabling you to deliver [!DNL Profile] data into the [!DNL Data Lake] with as little latency as possible.

Das folgende Video soll Ihnen helfen, das Streaming-Erlebnis zu verstehen, und beschreibt die oben genannten Konzepte.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Profildatensätze und streamen[!DNL ExperienceEvents]

With streaming ingestion, users can stream profile records and [!DNL ExperienceEvents] to [!DNL Platform] in seconds to help drive real-time personalization. All data sent to streaming ingestion APIs is automatically persisted in the [!DNL Data Lake].

Weiterführende Informationen finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

### An Datensätze streamen

Once you are confident that your data is clean, you can enable your datasets for [!DNL Real-time Customer Profile] and [!DNL Identity Service].

For more information on enabling a dataset for [!DNL Profile] and [!DNL Identity Service], please read the [configure a dataset guide](../../profile/tutorials/dataset-configuration.md).

## What is the expected latency for streaming ingestion on [!DNL Platform]?

| Ziel | Erwartete Latenz |
| --------- | ---------------- |
| Echtzeit-Kundenprofil | &lt; 1 Minute |
| Data Lake | &lt; 60 Minuten |

## Adobe Experience Platform-Erweiterung

Mit der Adobe Experience Platform-Erweiterung können Sie eine neue Streaming-Verbindung einrichten. Die [!DNL Experience Platform] Erweiterung bietet Aktionen zum Senden von Beacons, die in [!DNL Experience Data Model] (XDM) formatiert sind, zur Echtzeitaufnahme an [!DNL Experience Platform]. Weiterführende Informationen finden Sie in der Dokumentation zur [Experience Platform-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html).