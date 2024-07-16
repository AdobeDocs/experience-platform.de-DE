---
keywords: Experience Platform; home; beliebte Themen; Datenerfassung; erfasste Daten; Streaming; Übersicht; Streaming-Erfassung; Latenz; Streaming-Latenz; Streaming-Latenz;
solution: Experience Platform
title: Überblick über den Import von Streamingdaten
description: Streaming-Erfassung für Adobe Experience Platform bietet Benutzern eine Methode, Daten von Client- und Server-seitigen Geräten in Echtzeit an Experience Platform zu senden.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: d6424e2a9afc046f4bff329797954fd43939a819
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 14%

---

# Streaming-Erfassung – Übersicht

Die Streaming-Erfassung für Adobe Experience Platform bietet Benutzern eine Methode, Daten von Client- und Server-seitigen Geräten in Echtzeit an [!DNL Experience Platform] zu senden.

## Was können Sie mit Streaming-Erfassung tun?

Mit Adobe Experience Platform können Sie koordinierte, konsistente und relevante Erlebnisse bereitstellen, indem Sie für jeden Ihrer Kunden eine [!DNL Real-Time Customer Profile] generieren. Die Streaming-Erfassung spielt eine Schlüsselrolle beim Erstellen dieser Profile, indem Sie [!DNL Profile] -Daten mit so wenig Latenz wie möglich an die [!DNL Data Lake] übermitteln können.

Das folgende Video soll Ihnen dabei helfen, die Streaming-Erfassung zu verstehen, und beschreibt die oben genannten Konzepte.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Profildatensätze streamen und [!DNL ExperienceEvents]

Mit der Streaming-Erfassung können Benutzer Profildatensätze und [!DNL ExperienceEvents] in [!DNL Platform] in Sekunden streamen, um die Echtzeit-Personalisierung zu fördern. Alle Daten, die an Streaming-Aufnahme-APIs gesendet werden, werden automatisch im [!DNL Data Lake] beibehalten.

Weiterführende Informationen finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

### An Datensätze streamen

Sobald Sie sicher sind, dass Ihre Daten sauber sind, können Sie Ihre Datensätze für [!DNL Real-Time Customer Profile] und [!DNL Identity Service] aktivieren.

Weitere Informationen zum Aktivieren eines Datensatzes für [!DNL Profile] und [!DNL Identity Service] finden Sie im [Handbuch zum Konfigurieren eines Datensatzes](../../profile/tutorials/dataset-configuration.md).

## Wie hoch ist die erwartete Latenz für die Streaming-Erfassung auf Experience Platform?

>[!IMPORTANT]
>
>Limits für die Streaming-Erfassung werden auf Organisationsebene und nicht auf Sandbox-Ebene berechnet. Das bedeutet, dass Ihre Datennutzung pro Sandbox an die gesamte Berechtigung zur Lizenznutzung gebunden ist, die Ihrer gesamten Organisation entspricht. Darüber hinaus ist die Datennutzung in Entwicklungs-Sandboxes auf 10 % Ihrer Gesamtprofile beschränkt. Weitere Informationen zur Lizenzverwendungsberechtigung finden Sie im Leitfaden [Best Practices für die Datenverwaltung](../../landing/license-usage-and-guardrails/data-management-best-practices.md).

| Ziel | Erwartete Latenz |
| --------- | ---------------- |
| Echtzeit-Kundenprofil | &lt; 15 Minuten beim 95. Perzentil |
| Data Lake | &lt; 60 Minuten |

## Anleitung für Anfragen pro Sekunden (RPS) bei der Streaming-Erfassung

In der folgenden Tabelle finden Sie Anleitungen zur Anforderung pro Sekunden für die Streaming-Erfassung.

| RPS-Limit | Anmerkungen |
| --- | --- |
| 1000 Anfragen pro Sekunde | Diese können bei Verwendung des Endpunkts `/collection/batch` mehrere Nachrichten enthalten. |
| 10000 Einzelnachrichten pro Sekunde | Bei Verwendung des Endpunkts `/collection/batch` können die Nachrichten in weniger tatsächliche Anforderungen gruppiert werden. |

>[!IMPORTANT]
>
>Die erzwungene Beschränkung wird bei der Verwendung der synchronen Validierung zu **60 Anforderungen pro Minute**, da sie für Debugging-Zwecke vorgesehen ist.

## Adobe Experience Platform-Erweiterung

Mit der Adobe Experience Platform-Erweiterung können Sie eine neue Streaming-Verbindung einrichten. Die Erweiterung [!DNL Experience Platform] bietet Aktionen zum Senden von in [!DNL Experience Data Model] formatierten Beacons (XDM) für die Echtzeit-Erfassung in [!DNL Experience Platform]. Weiterführende Informationen finden Sie in der Dokumentation zur [Experience Platform-Erweiterung](../../tags/extensions/client/web-sdk/overview.md).
