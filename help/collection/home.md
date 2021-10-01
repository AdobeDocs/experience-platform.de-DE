---
keywords: Experience Platform;Startseite;beliebte Themen;Datenerfassung;Start;Web-SDK
solution: Experience Platform
title: Datenerfassung – Übersicht
topic-legacy: overview
description: Erfahren Sie mehr über die verschiedenen Technologien zur Erfassung von Daten zu Kundenerlebnissen in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: f61a845b915df3d803085fbf528e014c8acd9dbd
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 100%

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
* [Ereignisweiterleitung](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Experience-Datenmodell (XDM)](../xdm/home.md)

![](./images/Collection.png)

## Einfachere Implementierungen, schnellere Client-seitige Performance

Adobe Experience Platform Web- und Mobile-SDKs reduzieren und komprimieren alle Adobe-Produktbibliotheken in einem Entwicklungs-Kit für Web- und Mobile-Plattformen. Durch Komprimieren dieser Bibliotheken wird die Datenerfassung beschleunigt und Vorgänge werden von Client-seitigen Geräten bis zum Adobe Experience Platform Edge Network zu einem einzigen Stream zusammengefasst.

## Schnelle Bereitstellung der Adobe-Technologie {#edge}

Platform Edge Network ist ein global verteiltes, schnelles und zuverlässiges Netzwerk von Servern, die Daten in einem enormen Umfang empfangen und verarbeiten können. Mit Tags können Sie [Datenströme](../edge/fundamentals/datastreams.md) für Produkte wie Adobe Target, Adobe Audience Manager und Adobe Analytics einrichten. Dadurch können Sie diese Produkte Server-seitig aktivieren, ohne den Client-seitigen Code zu ändern.

![](./images/deploy.png)

>[!NOTE]
>
>Eine allgemeine Einführung in Platform Edge Network finden Sie in der folgenden [interaktiven Produkttour](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Schnelles und sicheres Transformieren, Erweitern und Senden von Daten

Die [Ereignisweiterleitung in Adobe Experience Platform](../tags/ui/event-forwarding/overview.md) kann auf einen beliebigen Platform-Datenstrom zugreifen. Daten mit extrem niedriger Latenz können transformiert, angereichert und an Drittanbieter-Ziele gesendet werden, ohne dass dem Client-Gerät Drittanbieter-Code hinzugefügt werden muss. Dies ermöglicht eine schnellere und sicherere Datenerfassung und -verteilung.

![](./images/launch.png)
