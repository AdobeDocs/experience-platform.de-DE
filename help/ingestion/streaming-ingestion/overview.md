---
keywords: Experience Platform;Home;beliebte Themen;Datenerfassung;erfassten Daten;Streaming;Übersicht;Streaming;Latenz;Streaming-Latenz; Streaming-Latenz;
solution: Experience Platform
title: Übersicht über die Streaming-Ingestion
topic: Übersicht
description: Die Streaming-Erfassung für Adobe Experience Platform bietet eine Möglichkeit, Daten von Client- und serverseitigen Geräten in Echtzeit an die Experience Platform zu senden.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 23%

---


# Streaming-Erfassung – Übersicht

Die Streaming-Erfassung für Adobe Experience Platform bietet Benutzern eine Möglichkeit, Daten von Client- und serverseitigen Geräten in Echtzeit an [!DNL Experience Platform] zu senden.

## Was können Sie mit Streaming-Erfassung tun?

Mit Adobe Experience Platform können Sie koordinierte, konsistente und relevante Erlebnisse fördern, indem Sie für jeden Ihrer Kunden ein [!DNL Real-time Customer Profile] generieren. Die Streaming-Erfassung spielt eine Schlüsselrolle beim Aufbau dieser Profil, indem Sie [!DNL Profile]-Daten mit so wenig Latenz wie möglich in das [!DNL Data Lake]-Element übertragen können.

Das folgende Video soll Ihnen helfen, das Streaming-Erlebnis zu verstehen, und beschreibt die oben genannten Konzepte.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Profildatensätze und streamen[!DNL ExperienceEvents]

Bei der Streaming-Erfassung können Profil-Datensätze und [!DNL ExperienceEvents] in Sekunden bis [!DNL Platform] streamen, um eine Personalisierung in Echtzeit zu ermöglichen. Alle Daten, die an Streaming-Erfassungsungs-APIs gesendet werden, werden automatisch in [!DNL Data Lake] beibehalten.

Weiterführende Informationen finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

### An Datensätze streamen

Sobald Sie sicher sind, dass Ihre Daten sauber sind, können Sie Ihre Datensätze für [!DNL Real-time Customer Profile] und [!DNL Identity Service] aktivieren.

Weitere Informationen zum Aktivieren eines Datasets für [!DNL Profile] und [!DNL Identity Service] finden Sie im Handbuch [Konfigurieren eines Datasets](../../profile/tutorials/dataset-configuration.md).

## Welche Latenz wird für die Streaming-Erfassung bei [!DNL Platform] erwartet?

| Ziel | Erwartete Latenz |
| --------- | ---------------- |
| Echtzeit-Kundenprofil | &lt; 1 Minute |
| Data Lake | &lt; 60 Minuten |

## Adobe Experience Platform-Erweiterung

Mit der Adobe Experience Platform-Erweiterung können Sie eine neue Streaming-Verbindung einrichten. Die Erweiterung [!DNL Experience Platform] stellt Aktionen zum Senden von Beacons bereit, die in [!DNL Experience Data Model] (XDM) formatiert sind, um sie in Echtzeit nach [!DNL Experience Platform] zu erfassen. Weiterführende Informationen finden Sie in der Dokumentation zur [Experience Platform-Erweiterung](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html).