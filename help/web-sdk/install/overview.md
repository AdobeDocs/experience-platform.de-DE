---
title: Web SDK-Installationsübersicht
description: Erfahren Sie, wie Sie den Experience Platform Web SDK installieren.
keywords: Web SDK-Installation;Installieren von Web SDK;Internet Explorer;Promise;npm-Paket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Web SDK-Installationsübersicht

Es gibt drei unterstützte Möglichkeiten, Adobe Experience Platform Web SDK zu verwenden:

1. **[Web SDK-Tag-Erweiterung](extension.md)**: Adobe empfiehlt die Verwendung dieser Methode. Installieren Sie einen Tag-Loader auf Ihrer Site und konfigurieren Sie dann Ihre Implementierung über die Datenerfassungs-Benutzeroberfläche von Adobe Experience Platform.
1. **[Web SDK JavaScript-Bibliothek](library.md)**: Verweisen Sie auf eine CDN-gehostete Bibliotheksdatei oder hosten Sie die Bibliotheksdatei mithilfe Ihrer eigenen Infrastruktur. Aufrufe an die -Bibliothek im Code auf Ihrer Site.
1. **[NPM](npm.md)**: Installieren Sie Web SDK mithilfe des NPM-Package Managers auf Ihrer Site.

## Voraussetzungen

Bevor Sie Web SDK verwenden oder installieren, müssen Sie die folgenden Anforderungen erfüllen:

* Die -Architektur in Adobe Experience Platform muss zuerst konfiguriert werden. Zu diesen Einstellungen gehören alle erforderlichen Schemata, Identitäten und Datenströme.
* Sie müssen über die entsprechenden Berechtigungen verfügen, um auf die entsprechenden Tools zugreifen zu können. Wenn Ihr Unternehmen beispielsweise beschließt, die Tag-Erweiterung zu verwenden, müssen Sie über die richtigen Berechtigungen für den Zugriff auf die Datenerfassungs-Benutzeroberfläche verfügen. Weitere [ finden Sie unter ](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=de) von Datenerfassungsberechtigungen .
* Es wird empfohlen, eine Erstanbieterdomäne (CNAME) zu verwenden. Wenn Sie bereits über einen CNAME für Adobe Analytics verfügen, können Sie diesen verwenden. Testen in der Entwicklungsumgebung funktioniert ohne einen CNAME, aber Adobe empfiehlt, einen zu haben, bevor er in der Produktionsumgebung veröffentlicht wird. Weitere Informationen finden [ unter ](../identity/first-party-device-ids.md)-IDs von Erstanbietern .
