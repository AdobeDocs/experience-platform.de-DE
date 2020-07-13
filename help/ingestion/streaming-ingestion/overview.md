---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming-Erfassung für Adobe Experience Platform – Übersicht
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 93%

---


# Übersicht über Streaming-Erfassung

Streaming-Erfassung für Adobe Experience Platform bietet Benutzern eine Methode, um Daten von Client- und Server-seitigen Geräten in Echtzeit an Experience Platform zu senden.

## Was können Sie mit Streaming-Erfassung tun?

Mit Adobe Experience Platform können Sie für koordinierte, konsistente und relevante Erlebnisse sorgen, indem Sie für jeden Ihrer Kunden ein Echtzeit-Profil anlegen. Streaming-Erfassung spielt eine Schlüsselrolle beim Erstellen dieser Profile, da Sie so Profildaten mit minimaler Latenz im Data Lake bereitstellen können.

Das folgende Video soll Ihnen helfen, das Streaming-Erlebnis zu verstehen, und beschreibt die oben genannten Konzepte.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Profildatensätze und ExperienceEvents streamen

Mit Streaming-Erfassung können Benutzer Profildatensätze und ExperienceEvents in Sekundenschnelle an Platform streamen und auf diese Weise Personalisierung in Echtzeit ermöglichen. Alle an Streaming Ingestion-APIs gesendeten Daten werden automatisch im Data Lake persistiert.

Weiterführende Informationen finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

### An Datensätze streamen

Sobald Sie sicher sind, dass Ihre Daten sauber sind, können Sie Ihre Datensätze für das Echtzeit-Kundenprofil und Identity Service aktivieren.

Weiterführende Informationen zum Aktivieren eines Datensatzes für den Profile- und Identity Service finden Sie im [Handbuch zum Konfigurieren eines Datensatzes](../../profile/tutorials/dataset-configuration.md).

## Welche Latenz wird bei der Streaming-Erfassung auf Platform erwartet?

| Ziel | Erwartete Latenz |
| --------- | ---------------- |
| Echtzeit-Kundenprofil | &lt; 1 Minute |
| Data Lake | &lt; 60 Minuten |

## Adobe Experience Platform-Erweiterung

Mit der Adobe Experience Platform-Erweiterung können Sie eine neue Streaming-Verbindung einrichten. Die Experience Platform-Erweiterung bietet Aktionen zum Senden von Beacons, die in Experience-Datenmodell (XDM) formatiert sind, für die Echtzeit-Erfassung in Experience Platform. Weiterführende Informationen finden Sie in der Dokumentation zur [Experience Platform-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html).