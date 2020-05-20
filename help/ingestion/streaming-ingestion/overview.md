---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Streaming Ingestion - Überblick
topic: overview
translation-type: tm+mt
source-git-commit: a570a7a3d905c4618d80f56f01747cced1d124e8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 3%

---


# Übersicht über die Streaming-Erfassung

Die Streaming-Erfassung für Adobe Experience Platform bietet Benutzern eine Methode, Daten von client- und serverseitigen Geräten in Echtzeit an Experience Platform zu senden.

## Was können Sie mit Streaming-Erfassung tun?

Mit der Adobe Experience Platform können Sie koordinierte, konsistente und relevante Erlebnisse fördern, indem Sie für jeden Ihrer Kunden ein Echtzeit-Profil erstellen. Die Streaming-Erfassung spielt eine Schlüsselrolle beim Aufbau dieser Profil, da Sie so Profil-Daten mit so wenig Latenz wie möglich in den Data Lake liefern können.

### Streamen von Profil-Aufzeichnungen und ExperienceEvents

Mit der Streaming-Erfassung können Benutzer Profil-Datensätze und ExperienceEvents in Sekundenschnelle an Plattform streamen, um eine Personalisierung in Echtzeit zu ermöglichen. Alle an Streaming-APIs gesendeten Daten werden automatisch im Data Lake beibehalten.

Weitere Informationen finden Sie in der Anleitung [zum](../tutorials/create-streaming-connection.md) Erstellen einer Streaming-Verbindung.

### Stream zu Datasets

Sobald Sie sicher sind, dass Ihre Daten sauber sind, können Sie Ihre Datensätze für den Echtzeit-Kundendienst und Identitätsdienst aktivieren.

Weitere Informationen zum Aktivieren eines Datensatzes für den Profil- und Identitätsdienst finden Sie im Handbuch zum [Konfigurieren eines Datensatzes](../../profile/tutorials/dataset-configuration.md).

## Welche Latenz wird für die Streaming-Erfassung auf der Plattform erwartet?

| Ziel | Erwartete Latenz |
| --------- | ---------------- |
| Echtzeit-Kundenprofil | &lt; 1 Minute |
| Datensee | &lt; 60 Minuten |

## Adobe Experience Platform-Erweiterung

Mit der Adobe Experience Platform-Erweiterung können Sie eine neue Streaming-Verbindung erstellen. Die Experience Platform-Erweiterung bietet Aktionen zum Senden von Beacons, die im Experience Data Model (XDM) formatiert sind, zur Echtzeitaufnahme an die Experience Platform. Weitere Informationen finden Sie in der Dokumentation zur [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) .