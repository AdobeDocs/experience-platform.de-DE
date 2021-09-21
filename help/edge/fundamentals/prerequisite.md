---
title: Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK.
keywords: Erstanbieterdomäne;CNAME;Schema;Schema erstellen;Launch;AEP Web SDK-Erweiterung;Erweiterung;Konfigurations-ID;Konfigurationstool;Datenelement erstellen;Datenelement erstellen;XDM-Objekt;sendEvent;Ereignis senden;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 9d3965be1956de754f0d2a82178bf5dcd871e239
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 3%

---

# Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK

Um das Platform Web SDK zu verwenden, müssen Sie zunächst:

- Lassen Sie Ihre Organisation diese Funktion bereitstellen. (Der Zugriff auf das Platform Web SDK ist kostenlos. Wenn Sie Zugriff erhalten möchten, wenden Sie sich an Ihren Customer Success Manager (CSM).)
- Es wird empfohlen, die Erstanbieterdomäne (CNAME) zu aktivieren. Wenn Sie bereits über einen CNAME für Adobe Analytics verfügen, sollten Sie diesen verwenden. Tests in der Entwicklung funktionieren ohne CNAME. Adobe empfiehlt jedoch, einen vor der Produktion zu verwenden. Obwohl eine CNAME-Implementierung keine Vorteile in Bezug auf die Cookie-Lebensdauer bietet, kann sie verhindern, dass bestimmte Anzeigensperren und seltener verwendete Browser SDK-Anforderungen blockieren. In diesen Fällen kann die Verwendung eines CNAME verhindern, dass die Datenerfassung für Benutzer, die diese Tools verwenden, unterbrochen wird.

>[!IMPORTANT]
>
>**Bitte beachten Sie, dass CNAME-Implementierungen von Erstanbietern ab dem 10.11.20 auf allen Safari-Browsern und mobilen iOS-Geräten eine Gültigkeit von 7 Tagen haben.**

- Berechtigung für Adobe Experience Platform. Wenn Sie Adobe Experience Platform noch nicht erworben haben, bietet Adobe Ihnen den erforderlichen Zugriff, um das SDK in begrenztem Umfang und ohne Aufpreis verwenden zu können.
- Wenn Ihre Website bereits den [Experience Cloud-ID-Dienst](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) auf Ihrer Website verwendet - entweder über die Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung in Adobe Experience Platform Launch - und Sie ihn bei der Migration zum Adobe Experience Platform Web SDK weiterhin verwenden möchten, müssen Sie die neueste Version der Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung verwenden. Weitere Informationen finden Sie unter [ID-Migration](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) .

## Berechtigungen für das Adobe Experience Platform Web SDK verwalten

Die Verwendung von Adobe Experience Platform erfordert keine speziellen Berechtigungen, Sie müssen jedoch über die Berechtigung [permissions](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=de) verfügen, Ihre Schemas in Adobe Experience Platform zu erstellen. Die Mindestberechtigungen, die jemand benötigt, finden Sie in der Kategorie Datenmodellierung und Identitäten .

![](../images/AEP-permission-categories.png)

Weisen Sie den Benutzern in der Kategorie Datenmodellierung die Berechtigungen Schemaverwaltung und Schemaansicht zu.

![](../images/data-modeling-permissions.png)

Weisen Sie den Benutzern in der Kategorie Identity Management die Berechtigungen Identitäts-Namespaces verwalten und Identitäts-Namespaces anzeigen zu.

![](../images/identity-management-permissions.png)
