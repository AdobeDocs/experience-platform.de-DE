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

Das Adobe Experience Platform-Edge Network bietet eine optimierte Möglichkeit für Kunden, mit beliebigen Adobe Experience Cloud- oder Adobe Experience Platform Edge-Diensten zu interagieren.

Der [!DNL Edge Network Server API] kann für verschiedene Datenerfassungs-, Personalisierungs-, Werbe- und Marketing-Anwendungsfälle verwendet werden. Der [!DNL Server API] kann auf Servern, [!DNL IoT] Geräten, Set-Top-Feldern und verschiedenen anderen Geräten verwendet werden.

Da das [!DNL Server API] nicht darauf angewiesen ist, Bibliotheken zu laden, bietet es eine blitzschnelle Möglichkeit, mit dem Adobe Experience Platform-Edge Network und den unterstützten Lösungen zu interagieren.

Die Vorteile der [!DNL Server API] -Architektur sind:

* Verringerte Seitenladezeit
* Verbesserte Latenz
* Erstanbieter-Datenerfassung
* Optimierte, serverseitige Kommunikation zwischen Diensten

Der [!DNL Server API] unterstützt die interaktive und Batch-Datenerfassung über zwei dedizierte Endpunkte:

1. Der interaktive Endpunkt unterstützt die Kommunikation mit Adobe Experience Platform- und Adobe Experience Cloud-Diensten, die erweiterte Segmentierung, Personalisierung und andere Marketing-Anwendungsfälle unterstützen.
2. Der Batch-Endpunkt ermöglicht das Senden von Anfragen im Batch-Modus, wenn Daten integriert werden müssen, ohne dass eine Antwort von den Anwendungen empfangen wird, die aufgerufen werden.

Der [!DNL Server API] unterstützt den folgenden Anforderungstyp:

* Authentifizierte Anfragen über [Adobe Developer](https://developer.adobe.com/), wobei der `server.adobedc.net` -Endpunkt verwendet wird.
* Nicht authentifizierte Anforderungen über den `edge.adobedc.net` -Endpunkt.

Dies ermöglicht Anwendungsfälle, die eine sichere, authentifizierte Erfassung sensibler Daten gemäß den Datenschutzrichtlinien Ihres Unternehmens ermöglichen. Zusätzlich zur Authentifizierung unterstützt die Server-API das Markieren von Datenspeichern, um nur authentifizierte Kommunikation über die API zu akzeptieren.

Im folgenden Video erhalten Sie einen optimierten Überblick über die Server-API.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
