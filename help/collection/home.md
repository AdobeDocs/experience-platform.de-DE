---
keywords: Experience Platform;Startseite;beliebte Themen;Datenerfassung;Start;Web-SDK
solution: Experience Platform
title: Datenerfassung – Übersicht
topic-legacy: overview
description: Erfahren Sie mehr über die verschiedenen Technologien zur Erfassung von Daten zu Kundenerlebnissen in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 0926f0a6dc005b1bf278e7a0fa0afe4296d8ad80
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 55%

---

# Datenerfassung – Übersicht

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Kundenerlebnisdaten aus Client-seitigen Quellen erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie in Sekundenschnelle an Adobe oder andere Ziele weitergegeben, transformiert und verteilt werden können.

Die Datenerfassung wird für die folgenden Client-seitigen Quellen unterstützt:

* Web-basierte Programme
* Native Mobile Apps
* OTT-Programme (Over-the-top)

Von Experience Platform bereitgestellte Datenerfassungstechnologien konzentrieren sich auf die Entdeckung und Zugänglichkeit von aufgenommenen Datensätzen. Diese Technologien umfassen Folgendes:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html?lang=de)
* [Tags](../tags/home.md)
* [Datenströme](../edge/fundamentals/datastreams.md)
* [Ereignisweiterleitung](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=de)
* [Experience-Datenmodell (XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

Dieses Handbuch bietet eine allgemeine Einführung in das Datenerfassungs-Framework und dessen Funktionsweise, Daten über das Platform Edge Network an Adobe Experience Cloud-Produkte und Anwendungen ohne Adobe zu senden.

## Tags, Web SDK und Mobile SDK

Das Platform Web SDK und Platform Mobile SDK reduzieren und komprimieren alle Adobe-Produktbibliotheken in einem einzigen Entwicklungs-Kit für Web- bzw. Mobilplattformen. Diese können mit Rohcode oder mithilfe von [tags](../tags/home.md) über die Datenerfassungs-Benutzeroberfläche.

Das Komprimieren dieser Bibliotheken beschleunigt die Datenerfassung und konsolidiert Vorgänge in einem einzigen Stream von Client-seitigen Geräten zum Platform Edge Network.

![Tags, Web SDK, Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge Network und Datenspeicher {#edge}

Platform Edge Network ist ein global verteiltes, schnelles und zuverlässiges Netzwerk von Servern, die Daten in einem enormen Umfang empfangen und verarbeiten können. Mit Tags können Sie [Datenströme](../edge/fundamentals/datastreams.md) für Produkte wie Adobe Target, Adobe Audience Manager und Adobe Analytics einrichten. Dadurch können Sie diese Produkte Server-seitig aktivieren, ohne den Client-seitigen Code zu ändern.

![Datenspeicher und Adobe-Lösungen](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Eine allgemeine Einführung in Platform Edge Network finden Sie in der folgenden [interaktiven Produkttour](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Ereignisweiterleitung

[Ereignisweiterleitung](../tags/ui/event-forwarding/overview.md) kann in einen beliebigen Experience Platform-Datastream tippen, sodass Sie Daten mit extrem geringer Latenz umwandeln, anreichern und an ein Ziel senden können, das keine Adobe ist, ohne dass dem Client-Gerät Drittanbietercode hinzugefügt wird.

![Ereignisweiterleitung](./images/home/event-forwarding.png)

## Nächste Schritte

Dieses Dokument bietet einen allgemeinen Überblick darüber, wie die Datenerfassungstechnologien von Platform dazu beitragen, den Prozess des Versands Ihrer erfassten Kundenerlebnisdaten an Adobe-Produkte und Drittanbieterziele zu automatisieren.

![Datenerfassungs-Framework](./images/home/collection.png)

Weitere Informationen zum allgemeinen Workflow für das Senden von Ereignisdaten über das Edge-Netzwerk finden Sie im Abschnitt [End-to-End-Übersicht für die Datenerfassung](./e2e.md).
