---
title: Edge Network Server-API – Übersicht
description: Erfahren Sie, was die Edge Network Server-API ist und wie Sie sie verwenden können.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 9%

---


# Edge Network Server-API – Übersicht {#overview}

Das Adobe Experience Platform Edge Network bietet eine optimierte Möglichkeit für Kunden, mit beliebigen Adobe Experience Cloud- oder Adobe Experience Platform Edge-Diensten zu interagieren.

Die [!DNL Edge Network Server API] kann für verschiedene Anwendungsfälle der Datenerfassung, Personalisierung, Werbung und Marketing verwendet werden. Die [!DNL Server API] kann auf Servern verwendet werden, [!DNL IoT] Geräte, Set-Top-Boxen und verschiedene andere Geräte.

Seit [!DNL Server API] ist nicht darauf angewiesen, dass Bibliotheken geladen werden, sondern bietet eine blitzschnelle Möglichkeit, mit dem Adobe Experience Platform Edge Network und den unterstützten Lösungen zu interagieren.

Die Vorteile der [!DNL Server API] -Architektur umfasst:

* Verringerte Seitenladezeit
* Verbesserte Latenz
* Erstanbieter-Datenerfassung
* Optimierte, serverseitige Kommunikation zwischen Diensten

Die [!DNL Server API] unterstützt die interaktive und Batch-Datenerfassung über zwei dedizierte Endpunkte:

1. Der interaktive Endpunkt unterstützt die Kommunikation mit Adobe Experience Platform- und Adobe Experience Cloud-Diensten, die erweiterte Segmentierung, Personalisierung und andere Marketing-Anwendungsfälle unterstützen.
2. Der Batch-Endpunkt ermöglicht das Senden von Anfragen im Batch-Modus, wenn Daten integriert werden müssen, ohne dass eine Antwort von den Anwendungen empfangen wird, die aufgerufen werden.

Die [!DNL Server API] unterstützt den folgenden Anforderungstyp:

* Authentifizierte Anfragen über [Adobe Developer](https://developer.adobe.com/), wobei `server.adobedc.net` -Endpunkt.
* Nicht authentifizierte Anforderungen über die `edge.adobedc.net` -Endpunkt.

Dies ermöglicht Anwendungsfälle, die eine sichere, authentifizierte Erfassung sensibler Daten gemäß den Datenschutzrichtlinien Ihres Unternehmens ermöglichen. Zusätzlich zur Authentifizierung unterstützt die Server-API das Markieren von Datenspeichern, um nur authentifizierte Kommunikation über die API zu akzeptieren.

Im folgenden Video erhalten Sie einen optimierten Überblick über die Server-API.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
