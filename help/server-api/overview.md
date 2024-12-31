---
title: Edge Network Server-API – Übersicht
description: Erfahren Sie, was die Edge Network Server-API ist und wie Sie sie verwenden können.
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: 041a1782442df5f08bb52e4e450734a51c7781ea
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 9%

---

# Edge Network Server-API – Übersicht {#overview}

Das Adobe Experience Platform-Edge Network bietet eine optimierte Möglichkeit für Kunden, mit beliebigen Adobe Experience Cloud- oder Adobe Experience Platform Edge-Services zu interagieren.

Die [!DNL Edge Network Server API] kann für verschiedene Anwendungsfälle zur Datenerfassung, Personalisierung, Werbung und Marketing verwendet werden. Die [!DNL Server API] kann auf Servern, [!DNL IoT], Set-Top-Boxen und verschiedenen anderen Geräten verwendet werden.

Da der [!DNL Server API] nicht auf das Laden von Bibliotheken angewiesen ist, bietet er eine blitzschnelle Möglichkeit, mit dem Adobe Experience Platform-Edge Network und unterstützten Lösungen zu interagieren.

Zu den Vorteilen der [!DNL Server API]-Architektur gehören:

* Verkürzte Seitenladezeit
* Verbesserte Latenz
* Erstanbieter-Datenerfassung
* Optimierte, Server-seitige Kommunikation zwischen Services

Die [!DNL Server API] unterstützt die interaktive und Batch-Datenerfassung über zwei dedizierte Endpunkte:

1. Der interaktive Endpunkt unterstützt die Kommunikation mit Adobe Experience Platform- und Adobe Experience Cloud-Services, die erweiterte Segmentierungs-, Personalisierungs- und andere Marketing-Anwendungsfälle unterstützen.
2. Der Batch-Endpunkt ermöglicht das Senden von Anfragen im Batch, wenn Daten eingebunden werden müssen, ohne eine Antwort von den aufgerufenen Anwendungen zu erhalten.

Der [!DNL Server API] unterstützt die folgenden Anfragetypen:

* Authentifizierte Anfragen über [Adobe Developer](https://developer.adobe.com/) unter Verwendung des `server.adobedc.net`-Endpunkts.
* Nicht authentifizierte Anfragen über den `edge.adobedc.net`-Endpunkt.

Dies ermöglicht Anwendungsfälle, die eine sichere, authentifizierte Erfassung sensibler Daten gemäß den Datenschutzrichtlinien Ihres Unternehmens ermöglichen. Zusätzlich zur Authentifizierung unterstützt die Server-API das Markieren von Datenströmen, sodass nur authentifizierte Kommunikation über die API akzeptiert wird.

Sehen Sie sich das folgende Video an, um einen optimierten Überblick über die Server-API zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
