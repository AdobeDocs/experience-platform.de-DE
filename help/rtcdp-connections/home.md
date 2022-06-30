---
keywords: Experience Platform;Startseite;beliebte Themen;Datenerfassung;Start;Web-SDK
solution: Experience Platform
title: Übersicht über Real-time Customer Data Platform-Verbindungen
topic-legacy: overview
description: Erfahren Sie mehr über die verschiedenen Technologien zur Erfassung von Daten zu Kundenerlebnissen in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 62%

---

# Übersicht über Real-time Customer Data Platform-Verbindungen

Real-time Customer Data Platform (RTCDP) Connections bietet eine Reihe von Technologien, mit denen Sie Kundenerlebnisdaten aus Client-seitigen Quellen erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie in Sekundenschnelle an Adobe- oder Nicht-Adobe-Ziele angereichert, transformiert und verteilt werden können.

RTCDP-Verbindungen werden für die folgenden clientseitigen Quellen unterstützt:

* Web-basierte Programme
* Native Mobile Apps
* OTT-Programme (Over-the-top)

RTCDP-Verbindungen konzentrieren sich auf die Erkennung und Zugänglichkeit erfasster Datensätze und umfassen Folgendes:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html?lang=de)
* [Tags](../tags/home.md)
* [Datenströme](../edge/datastreams/overview.md)
* [Ereignisweiterleitung](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=de)
* [Experience-Datenmodell (XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

Dieses Handbuch bietet eine allgemeine Einführung in RTCDP-Verbindungen und wie Daten über das Platform Edge Network an Adobe Experience Cloud-Produkte und Nicht-Adobe-Anwendungen gesendet werden können.

## Tags, Web SDK und Mobile SDK

Das Platform Web SDK und Platform Mobile SDK reduzieren und komprimieren alle Adobe-Produktbibliotheken in einem einzigen Entwicklungs-Kit für Web- bzw. Mobilplattformen. Diese können mit Rohcode oder mithilfe von [Tags](../tags/home.md) über die Datenerfassungsbenutzeroberfläche implementiert werden.

Durch Komprimieren dieser Bibliotheken wird die Datenerfassung beschleunigt und Vorgänge werden von Client-seitigen Geräten bis Platform Edge Network zu einem einzigen Stream zusammengefasst.

![Tags, Web SDK, Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge Network und Datenströme {#edge}

Platform Edge Network ist ein global verteiltes, schnelles und zuverlässiges Netzwerk von Servern, die Daten in einem enormen Umfang empfangen und verarbeiten können. Mit Tags können Sie [Datenströme](../edge/datastreams/overview.md) für Produkte wie Adobe Target, Adobe Audience Manager und Adobe Analytics einrichten. Dadurch können Sie diese Produkte Server-seitig aktivieren, ohne den Client-seitigen Code zu ändern.

![Datenströme und Adobe-Lösungen](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Eine allgemeine Einführung in Platform Edge Network finden Sie in der folgenden [interaktiven Produkttour](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Ereignisweiterleitung

[Ereignisweiterleitung](../tags/ui/event-forwarding/overview.md) kann sich einen beliebigen Experience Platform-Datenstrom zunutze machen, sodass Sie Daten mit extrem geringer Latenz umwandeln, anreichern und an ein Ziel senden können, bei dem es sich nicht um ein Adobe-Programm handelt, ohne dass dem Client-Gerät Drittanbieter-Code hinzugefügt wird.

![Ereignisweiterleitung](./images/home/event-forwarding.png)

>[!NOTE]
>
>Die Ereignisweiterleitung ist eine gebührenpflichtige Funktion, die nur im Rahmen von Real-time Customer Data Platform-Verbindungen angeboten wird.

## Nächste Schritte

In diesem Dokument erhalten Sie einen allgemeinen Überblick darüber, wie RTCDP-Verbindungen den Versand Ihrer erfassten Kundenerlebnisdaten an Adobe-Produkte und Drittanbieterziele automatisieren.

![Datenerfassungs-Framework](./images/home/collection.png)

Weitere Informationen zum allgemeinen Workflow für das Senden von Ereignisdaten über das Edge-Netzwerk finden Sie im Abschnitt [End-to-End-Übersicht](./e2e.md).
