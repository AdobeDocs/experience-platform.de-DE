---
title: Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK.
keywords: Erstanbieterdomäne;CNAME;Schema;Schema erstellen;Start;aep-Web-SDK-Erweiterung;Erweiterung;Konfigurations-ID;Konfigurationstool;Datenelement;Datenelement erstellen;XDM-Objekt;sendEvent;Ereignis senden;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 4%

---


# Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK

Zur Verwendung des Platform Web SDK müssen Sie zunächst:

- Lassen Sie sich diese Funktion von Ihrem Unternehmen bereitstellen. (Der Zugriff auf das Platform Web SDK ist kostenlos. Wenn Sie Zugriff haben möchten, wenden Sie sich bitte an Ihren Customer Success Manager (CSM).
- Sie benötigen eine aktivierte Erstanbieter-Domäne (CNAME). Wenn Sie bereits einen CNAME für Adobe Analytics haben, sollten Sie diesen verwenden. Tests in der Entwicklung funktionieren ohne CNAME, Sie benötigen jedoch einen, bevor Sie zur Produktion gehen.

>[!IMPORTANT]
>
>**Bitte beachten Sie, dass CNAME-Implementierungen von Erstanbietern ab dem 10.11.20 auf allen Safari-Browsern und mobilen iOS-Geräten eine Laufzeit von 7 Tagen haben.**

- Berechtigung für Adobe Experience Platform. Wenn Sie Adobe Experience Platform nicht gekauft haben, bietet Ihnen die Adobe den erforderlichen Zugriff, um das SDK in begrenzter Weise ohne Aufpreis zu verwenden.
- Wenn Ihre Website bereits den [Experience Cloud-ID-Dienst](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) auf Ihrer Website verwendet - entweder über die Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung in Adobe Experience Platform Launch - und Sie ihn während der Migration zum Adobe Experience Platform Web SDK weiter verwenden möchten, müssen Sie die neueste Version der Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung verwenden. Weitere Informationen finden Sie unter [ID-Migration](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity).
