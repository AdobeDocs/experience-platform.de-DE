---
title: Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK.
keywords: Erstanbieterdomäne;CNAME;Schema;Schema erstellen;Launch;AEP Web SDK-Erweiterung;Erweiterung;Konfigurations-ID;Konfigurationstool;Datenelement erstellen;Datenelement erstellen;XDM-Objekt;sendEvent;Ereignis senden;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: a9b63d2ad2c1adbd647c0c3a43331cddffa8a04e
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 2%

---

# Voraussetzungen für die Verwendung des Adobe Experience Platform Web SDK

Um das Adobe Experience Platform Web SDK zu verwenden, müssen Sie zunächst:

- Lassen Sie Ihre Organisation diese Funktion bereitstellen. Wenn Sie Zugriff erhalten möchten, füllen Sie bitte Folgendes aus [Formular](https://adobe.ly/websdkaccess) und Adobe bieten Ihnen Zugriff auf Datenströme und Adobe Experience Platform (falls erforderlich). Bitte beachten Sie, dass Adobe Ihnen ohne Aufpreis den erforderlichen Zugriff zur begrenzten Nutzung mit dem SDK bietet.
- Es wird empfohlen, die Erstanbieterdomäne (CNAME) zu aktivieren. Wenn Sie bereits über einen CNAME für Adobe Analytics verfügen, sollten Sie diesen verwenden. Tests in der Entwicklung funktionieren ohne CNAME. Adobe empfiehlt jedoch, einen vor der Produktion zu verwenden. Obwohl eine CNAME-Implementierung keine Vorteile in Bezug auf die Cookie-Lebensdauer bietet, kann sie verhindern, dass bestimmte Anzeigensperren und seltener verwendete Browser SDK-Anforderungen blockieren. In diesen Fällen kann die Verwendung eines CNAME verhindern, dass die Datenerfassung für Benutzer, die diese Tools verwenden, unterbrochen wird.

>[!IMPORTANT]
>
>**Bitte beachten Sie, dass CNAME-Implementierungen von Erstanbietern ab dem 10.11.20 auf allen Safari-Browsern und mobilen iOS-Geräten eine Gültigkeit von 7 Tagen haben.**

- Wenn Ihre Website bereits die [Experience Cloud-ID-Dienst](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) auf Ihrer Website - entweder über die Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung innerhalb von Adobe Experience Platform Launch - und Sie möchten sie bei der Migration zum Adobe Experience Platform Web SDK weiterhin verwenden, müssen Sie die neueste Version der Besucher-API oder die Experience Cloud-ID-Dienst-Erweiterung verwenden. Siehe [ID-Migration](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) für weitere Informationen.

## Berechtigungen für das Adobe Experience Platform Web SDK verwalten

Um Adobe Experience Platform verwenden zu können, benötigen Sie die [Berechtigungen](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=de) , um Ihre Schemas zu erstellen und Identitäten zu verwalten. Die erforderlichen Mindestberechtigungen finden Sie in der Kategorie Datenmodellierung und Identitäten .

![](../images/AEP-permission-categories.png)

Weisen Sie den Benutzern in der Kategorie Datenmodellierung die Berechtigungen Schemaverwaltung und Schemaansicht zu.

![](../images/data-modeling-permissions.png)

Weisen Sie den Benutzern in der Kategorie Identity Management die Berechtigungen Identitäts-Namespaces verwalten und Identitäts-Namespaces anzeigen zu.

![](../images/identity-management-permissions.png)
