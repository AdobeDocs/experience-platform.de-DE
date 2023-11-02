---
title: Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK.
keywords: Erstanbieterdomäne;CNAME;Schema;Schema erstellen;Launch;AEP Web SDK-Erweiterung;Erweiterung;Konfigurations-ID;Konfigurationstool;Datenelement erstellen;Datenelement erstellen;XDM-Objekt;sendEvent;Ereignis senden;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 4%

---

# Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK

Um das Adobe Experience Platform Web SDK zu verwenden, müssen Sie zunächst:

- Die richtigen Berechtigungen für Benutzer in Ihrer Organisation konfigurieren. Alle Experience Cloud-Kunden haben Zugriff auf die Datenerfassungs-Tools. Jeder Benutzer in Ihrer Organisation benötigt lediglich Berechtigungen für Schemas, Identitäten und Datastreams. Weitere Informationen zum Einrichten dieser Berechtigungen finden Sie in unserer Dokumentation unter [Verwaltung von Datenerfassungsberechtigungen](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=de).
- Es wird empfohlen, die Erstanbieterdomäne (CNAME) zu aktivieren. Wenn Sie bereits über einen CNAME für Adobe Analytics verfügen, sollten Sie diesen verwenden. Tests in der Entwicklung funktionieren ohne CNAME, aber Adobe empfiehlt, einen vor der Produktion zu haben. Obwohl eine CNAME-Implementierung keine Vorteile in Bezug auf die Cookie-Lebensdauer bietet, kann sie verhindern, dass bestimmte Anzeigensperren und seltener verwendete Browser SDK-Anforderungen blockieren. In diesen Fällen kann die Verwendung eines CNAME verhindern, dass die Datenerfassung für Benutzer, die diese Tools verwenden, unterbrochen wird.

>[!IMPORTANT]
>
>**Bitte beachten Sie, dass CNAME-Implementierungen von Erstanbietern ab dem 10.11.20 auf allen Safari-Browsern und mobilen iOS-Geräten eine Gültigkeit von 7 Tagen haben.**

- Wenn Ihre Website bereits die [Experience Cloud ID-Dienst](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=de) auf Ihrer Website - entweder über die Besucher-API oder die Experience Cloud ID-Dienst-Erweiterung innerhalb von Adobe Experience Platform Launch - und Sie möchten sie bei der Migration zum Adobe Experience Platform Web SDK weiterhin verwenden, müssen Sie die neueste Version der Besucher-API oder die Experience Cloud ID Service-Erweiterung verwenden. Siehe [ID-Migration](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#identity) für weitere Informationen.
