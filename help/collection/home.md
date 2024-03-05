---
keywords: Experience Platform;Startseite;beliebte Themen;Datenerfassung;Start;Web-SDK
solution: Experience Platform
title: Datenerfassung – Übersicht
description: Erfahren Sie mehr über die verschiedenen Technologien zur Erfassung von Daten zu Kundenerlebnissen in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 100%

---

# Datenerfassung – Übersicht

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Kundenerlebnisdaten aus Client-seitigen Quellen erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie in Sekundenschnelle an Adobe oder andere Ziele weitergegeben, transformiert und verteilt werden können.

Die Datenerfassung wird für die folgenden Client-seitigen Quellen unterstützt:

* Web-basierte Programme
* Native Mobile Apps
* OTT-Programme (Over-the-top)

Die Datenerfassung konzentriert sich auf die Auffindbarkeit und Zugänglichkeit aufgenommener Datensätze und umfasst Folgendes:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html?lang=de)
* [Tags](../tags/home.md)
* [Datenströme](../datastreams/overview.md)
* [Ereignisweiterleitung](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../web-sdk/home.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)
* [Edge Network Server-API](../server-api/overview.md)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=de)
* [Experience Platform Assurance](../assurance/home.md)


Dieses Handbuch bietet eine allgemeine Einführung in die Datenerfassung und dazu, wie damit Daten über das Platform Edge Network an Adobe Experience Cloud-Produkte und nicht von Adobe stammende Anwendungen gesendet werden.

## Tags, Web SDK und Mobile SDK

Das Platform Web SDK und Platform Mobile SDK reduzieren und komprimieren alle Adobe-Produktbibliotheken in einem einzigen Entwicklungs-Kit für Web- bzw. Mobilplattformen. Diese können mit Raw-Code oder mithilfe von [Tags](../tags/home.md) über die Datenerfassungsoberfläche oder die Adobe Experience Platform-Benutzeroberfläche implementiert werden.

Durch Komprimieren dieser Bibliotheken wird die Datenerfassung beschleunigt und Vorgänge werden von Client-seitigen Geräten bis Platform Edge Network zu einem einzigen Stream zusammengefasst.

![Tags, Web SDK, Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge Network und Datenströme {#edge}

Platform Edge Network ist ein global verteiltes, schnelles und zuverlässiges Netzwerk von Servern, die Daten in einem enormen Umfang empfangen und verarbeiten können. Mit Tags können Sie [Datenströme](../datastreams/overview.md) für Produkte wie Adobe Target, Adobe Audience Manager und Adobe Analytics einrichten. Dadurch können Sie diese Produkte Server-seitig aktivieren, ohne den Client-seitigen Code zu ändern.

Darüber hinaus sind Datenströme in verschiedene Platform-Funktionen integriert, mit denen sichergestellt wird, dass sensible Daten, die Sie senden, im Hinblick auf Unternehmensrichtlinien und rechtliche Vorschriften angemessen verarbeitet werden. Weiterführende Informationen finden Sie im Abschnitt zum [Umgang mit sensiblen Daten](../datastreams/overview.md#sensitive) in der Dokumentation zu Datenströmen.

![Datenströme und Adobe-Lösungen](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Eine allgemeine Einführung in Platform Edge Network finden Sie in der folgenden [interaktiven Produkttour](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Ereignisweiterleitung

[Ereignisweiterleitung](../tags/ui/event-forwarding/overview.md) kann sich einen beliebigen Experience Platform-Datenstrom zunutze machen, sodass Sie Daten mit extrem geringer Latenz umwandeln, anreichern und an ein Ziel senden können, bei dem es sich nicht um ein Adobe-Programm handelt, ohne dass dem Client-Gerät Drittanbieter-Code hinzugefügt wird.

![Ereignisweiterleitung](./images/home/event-forwarding.png)

>[!NOTE]
>
>Die Ereignisweiterleitung ist eine gebührenpflichtige Funktion, die im Rahmen von Adobe Real-time Customer Data Platform Connections, Prime und Ultimate angeboten wird.

## Nächste Schritte

Dieses Dokument bietet einen allgemeinen Überblick darüber, wie die Datenerfassung dazu beiträgt, den Prozess des Versands Ihrer erfassten Kundenerlebnisdaten an Adobe-Produkte und Drittanbieterziele zu automatisieren.

![Datenerfassungs-Framework](./images/home/collection.png)

Weitere Informationen zum allgemeinen Workflow für das Senden von Ereignisdaten über Edge Network finden Sie im Abschnitt [End-to-End-Übersicht](./e2e.md).
