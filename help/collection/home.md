---
keywords: Experience Platform;Home;beliebte Themen;Datenerfassung;Start;Web-SDK
solution: Experience Platform
title: Übersicht über die Datenerfassung
topic-legacy: overview
description: Erfahren Sie mehr über die verschiedenen Technologien zur Datenerfassung über Kundenerlebnisse in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 6%

---

# Übersicht über die Datenerfassung

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Kundenerlebnisdaten aus clientseitigen Quellen erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie in Sekundenschnelle an Adoben- oder Nicht-Adobe-Ziele weitergegeben, transformiert und verteilt werden können.

Die Datenerfassung wird für die folgenden clientseitigen Quellen unterstützt:

* Webbasierte Anwendungen
* Native Mobilanwendungen
* OTT-Anwendungen (Over-the-top)

Die von der Experience Platform bereitgestellten Datenerfassungstechnologien konzentrieren sich auf die Entdeckung und Zugänglichkeit von erfassten Datensätzen. Diese Technologien umfassen Folgendes:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Adobe Experience Platform Launch](https://adobe.com/go/launch_help_en)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Experience-Datenmodell (XDM)](../xdm/home.md)

![](./images/Collection.png)

## Einfachere Implementierungen, schnellere clientseitige Performance

Adobe Experience Platform Web- und Mobile-SDKs reduzieren und komprimieren alle Produktbibliotheken in einem Entwicklungskit für Web- und Mobilplattformen. Durch Komprimieren dieser Bibliotheken wird die Datenerfassung beschleunigt und Vorgänge werden von clientseitigen Geräten bis zum Adobe Experience Platform Edge Network zu einem einzigen Stream zusammengefasst.

## Umschalten zwischen den Schaltvorgängen zur Bereitstellung der Adobe

Platform Edge Network ist ein global verteiltes, schnelles und zuverlässiges Netzwerk von Servern, die Daten in einem enormen Umfang empfangen und verarbeiten können. Mit Platform launch können Sie [Edge-Konfigurationen](../edge/fundamentals/edge-configuration.md) für Produkte wie Adobe Target, Adobe Audience Manager und Adobe Analytics einrichten, mit denen Sie diese Produkte serverseitig aktivieren können, ohne den clientseitigen Code zu ändern.

![](./images/deploy.png)

## Schnelles und sicheres Transformieren, Erweitern und Senden von Daten

[Adobe Experience Platform Launch Server ](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html) Sidecan tippen Sie auf einen beliebigen Plattform-Datenstrom. Mit extrem niedriger Latenz können Sie Daten mit extrem niedriger Latenz an andere Zielorte ohne Adobe transformieren, anreichern und senden, ohne dem Client-Gerät Drittanbieter-Code hinzuzufügen, der eine schnellere und sicherere Datenerfassung und -verteilung ermöglicht.

![](./images/launch.png)
