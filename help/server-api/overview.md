---
title: Edge Network Server-API
description: Erfahren Sie, was die Edge Network Server-API ist und wie Sie sie verwenden können.
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: Datenerfassung; Datenerfassung; Adobe Experience Platform Edge Network; Server-API;
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Übersicht über die Edge Network Server-API {#overview}

Das Adobe Experience Platform Edge Network bietet eine optimierte Möglichkeit für Kunden, mit beliebigen Adobe Experience Cloud- oder Adobe Experience Platform Edge-Diensten zu interagieren.

Die [!DNL Edge Network Server API] kann für eine Vielzahl von Anwendungsfällen zur Datenerfassung, Personalisierung, Werbung und Marketing verwendet werden. Die [!DNL Server API] kann auf Servern verwendet werden, [!DNL IoT] Geräte, Set-Top-Boxen und eine Vielzahl anderer Geräte.

Seit [!DNL Server API] ist nicht darauf angewiesen, dass Bibliotheken geladen werden, sondern bietet eine blitzschnelle Möglichkeit, mit dem Adobe Experience Platform Edge Network und den unterstützten Lösungen zu interagieren.

Die Vorteile der [!DNL Server API] -Architektur umfasst:

* Verringerte Seitenladezeit
* Verbesserte Latenz
* Erstanbieter-Datenerfassung
* Optimierte, serverseitige Kommunikation zwischen Diensten

Die [!DNL Server API] unterstützt die interaktive und Batch-Datenerfassung über zwei dedizierte Endpunkte:

1. Der interaktive Endpunkt unterstützt die Kommunikation mit Adobe Experience Platform- und Adobe Experience Cloud-Diensten, die erweiterte Segmentierung, Personalisierung und andere Marketing-Anwendungsfälle unterstützen.
2. Der Batch-Endpunkt ermöglicht das Senden von Anfragen im Batch-Modus, wenn Daten integriert werden müssen, ohne eine Antwort von den Anwendungen zu erhalten, die aufgerufen werden.

Die [!DNL Server API] unterstützt den folgenden Anforderungstyp:

* Authentifizierte Anfragen über [Adobe I/O](https://developer.adobe.com/), unter Verwendung der neuen `server.adobedc.net` -Endpunkt.
* Nicht authentifizierte Anforderungen über die `edge.adobedc.net` -Endpunkt.

Dies ermöglicht Anwendungsfälle, die eine sichere, authentifizierte Erfassung sensibler Daten gemäß den Datenschutzrichtlinien Ihres Unternehmens ermöglichen. Zusätzlich zur Authentifizierung unterstützt die Server-API das Markieren von Datenspeichern, um nur authentifizierte Kommunikation über die API zu akzeptieren.

Im folgenden Video erhalten Sie einen optimierten Überblick über die Server-API.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
