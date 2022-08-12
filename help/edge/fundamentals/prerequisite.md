---
title: Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK.
keywords: Erstanbieterdomäne;CNAME;Schema;Schema erstellen;Launch;AEP Web SDK-Erweiterung;Erweiterung;Konfigurations-ID;Konfigurationstool;Datenelement erstellen;Datenelement erstellen;XDM-Objekt;sendEvent;Ereignis senden;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 853c0a662592939c280c7e7ede8235d1b6155b2f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK

Um das Adobe Experience Platform Web SDK zu verwenden, müssen Sie zunächst:

- Lassen Sie Ihre Organisation diese Funktion bereitstellen. Wenn Sie Zugriff erhalten möchten, füllen Sie bitte Folgendes aus [Formular](https://adobe.ly/websdkaccess) und Adobe bietet Ihnen Zugriff auf Datenspeicher und Adobe Experience Platform (falls erforderlich). Bitte beachten Sie, dass Adobe Ihnen ohne Aufpreis den erforderlichen Zugriff zur begrenzten Nutzung mit dem SDK bietet.
- Es wird empfohlen, die Erstanbieterdomäne (CNAME) zu aktivieren. Wenn Sie bereits über einen CNAME für Adobe Analytics verfügen, sollten Sie diesen verwenden. Tests in der Entwicklung funktionieren ohne CNAME. Adobe empfiehlt jedoch, einen vor der Produktion zu verwenden. Obwohl eine CNAME-Implementierung keine Vorteile in Bezug auf die Cookie-Lebensdauer bietet, kann sie verhindern, dass bestimmte Anzeigensperren und seltener verwendete Browser SDK-Anforderungen blockieren. In diesen Fällen kann die Verwendung eines CNAME verhindern, dass die Datenerfassung für Benutzer, die diese Tools verwenden, unterbrochen wird.

>[!IMPORTANT]
>
>**Bitte beachten Sie, dass CNAME-Implementierungen von Erstanbietern ab dem 10.11.20 auf allen Safari-Browsern und mobilen iOS-Geräten eine Gültigkeit von 7 Tagen haben.**

- Wenn Ihre Website bereits die [Experience Cloud-ID-Dienst](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) auf Ihrer Website - entweder über die Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung innerhalb von Adobe Experience Platform Launch - und Sie möchten sie bei der Migration zum Adobe Experience Platform Web SDK weiterhin verwenden, müssen Sie die neueste Version der Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung verwenden. Siehe [ID-Migration](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) für weitere Informationen.

## Berechtigungen für das Adobe Experience Platform Web SDK verwalten

Um mit der Verwendung des Adobe Experience Platform Web SDK beginnen zu können, müssen Sie über die richtigen Berechtigungen verfügen. Weitere Informationen zum Einrichten Ihrer Konfiguration finden Sie in unserer Dokumentation unter [Verwaltung von Datenerfassungsberechtigungen](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
