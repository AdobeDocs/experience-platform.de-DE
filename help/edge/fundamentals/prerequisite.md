---
title: Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK
seo-title: Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK
description: Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK
seo-description: Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: 94b3faf3157f4e1f4e46b6055914a04883dc44fa
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 4%

---


# Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK

Um dieses SDK zu verwenden, müssen Sie zuerst:

- Stellen Sie Ihre Organisation für diese Funktion bereit. (Wenn Sie die wartende Liste fortsetzen möchten, wenden Sie sich bitte an Ihren Kundenbetreuer (Customer Success Manager, CSM)).
- Sie benötigen eine aktivierte Erstanbieter-Domäne (CNAME). Wenn Sie bereits einen CNAME für Adobe Analytics haben, sollten Sie diesen verwenden. Tests in der Entwicklung funktionieren ohne CNAME, Sie benötigen jedoch einen, bevor Sie zur Produktion gehen.

>[!IMPORTANT]
>
>**Bitte beachten Sie, dass CNAME-Implementierungen von Erstanbietern ab dem 10.11.20 auf allen Safari-Browsern und mobilen iOS-Geräten eine Laufzeit von 7 Tagen haben.**

- Berechtigung für Adobe Experience Platform. Wenn Sie Adobe Experience Platform nicht erworben haben, stellt Adobe Ihnen die Experience Platform Data Services Foundation zur begrenzten Verwendung mit dem SDK kostenlos zur Verfügung.
- Wenn Ihre Website bereits den [Experience Cloud-ID-Dienst](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) auf Ihrer Website verwendet - entweder über die Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung in Adobe Experience Platform Launch - und Sie ihn während der Migration zum Adobe Experience Platform Web SDK weiter verwenden möchten, müssen Sie die neueste Version der Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung verwenden. Weitere Informationen finden Sie unter [ID-Migration](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity).
