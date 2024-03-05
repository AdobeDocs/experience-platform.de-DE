---
title: Übersicht über die Installation des Web SDK
description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
keywords: Web SDK-Installation;Web SDK installieren;Internet Explorer;Zusage;npm-Paket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Übersicht über die Installation des Web SDK

Es werden drei Möglichkeiten zur Verwendung des Adobe Experience Platform Web SDK unterstützt:

1. **[Web SDK-Tag-Erweiterung](extension.md)**: Adobe empfiehlt die Verwendung dieser Methode. Installieren Sie einen Tag-Lader auf Ihrer Site und konfigurieren Sie dann Ihre Implementierung über die Adobe Experience Platform-Benutzeroberfläche zur Datenerfassung.
1. **[JavaScript-Bibliothek des Web SDK](library.md)**: Verweisen Sie auf eine von CDN gehostete Bibliotheksdatei oder hosten Sie die Bibliotheksdatei mithilfe Ihrer eigenen Infrastruktur. Rufen Sie die Bibliothek im Code auf Ihrer Site auf.
1. **[NPM](npm.md)**: Installieren Sie das Web SDK mit dem NPM Package Manager auf Ihrer Site.

## Voraussetzungen

Bevor Sie das Web SDK verwenden oder installieren, müssen Sie die folgenden Anforderungen erfüllen:

* Die Architektur in Adobe Experience Platform muss zuerst konfiguriert werden. Zu diesen Einstellungen gehören alle erforderlichen Schemas, Identitäten und Datastreams.
* Sie müssen über die richtigen Berechtigungen für den Zugriff auf die entsprechenden Tools verfügen. Wenn Ihr Unternehmen z. B. die Tag-Erweiterung verwendet, müssen Sie über die richtigen Berechtigungen für den Zugriff auf die Datenerfassungs-Benutzeroberfläche verfügen. Siehe [Verwaltung von Datenerfassungsberechtigungen](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=de) für weitere Informationen.
* Es wird empfohlen, eine Erstanbieterdomäne (CNAME) zu verwenden. Wenn Sie bereits über einen CNAME für Adobe Analytics verfügen, können Sie diesen verwenden. Tests in der Entwicklung funktionieren ohne CNAME, Adobe empfiehlt jedoch, einen vor der Veröffentlichung in der Produktion zu verwenden. Siehe [Erstanbieter-Geräte-IDs](../identity/first-party-device-ids.md) für weitere Informationen.
