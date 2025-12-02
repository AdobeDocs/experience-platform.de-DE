---
title: Mobile-zu-Web und Domain-übergreifender ID-Austausch
description: Erfahren Sie, wie Sie Besucher-IDs von Mobile zu Web-Eigenschaften und domänenübergreifend beibehalten
keywords: Identität;Mobil;ID;Freigabe;Domain;domänenübergreifend;SDK;Plattform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 3%

---

# Mobile-zu-Web und Domain-übergreifender ID-Austausch

## Überblick

Adobe Experience Platform Web SDK unterstützt die Freigabe von Besucher-IDs, mit denen Kunden personalisierte Erlebnisse präziser zwischen Mobile Apps und mobilen Web-Inhalten sowie domänenübergreifend bereitstellen können.

## Anwendungsfälle {#use-cases}

### Konsistente Personalisierung zwischen mobilen Apps und mobilen Websites

Ein Bekleidungsunternehmen möchte die Erlebnisse seiner Kunden auf der Grundlage seiner Interessen personalisieren und die Personalisierung in einer mobilen Anwendung, die auch WebViews lädt, präzise halten. Durch die Verwendung der ID-Freigabe von Mobilgeräten an das Web können sie sicherstellen, dass Kundinnen und Kunden die genauesten Angebote unterbreitet werden, indem sie dieselbe Besucherkennung in der App und denselben mobilen Webinhalt verwenden, indem sie die [!DNL ECID] an die mobile Web-URL übergeben.

### Konsistente Personalisierung über Domains hinweg

Ein retailer mit mehreren Online-Shops möchte das Kundenerlebnis je nach Kundeninteressen domänenübergreifend personalisieren. Mit der Domain-übergreifenden ID-Freigabe von Web SDK kann retailer für alle Domains präzise, auf den Kundeninteressen basierende Angebote bereitstellen.

### Verbessern der Berichterstellung für Besucheraktivitäten

Eine Technologie, mit der retailer die Berichte zu Besucheraktivitäten verbessern möchte, indem Informationen darüber bereitgestellt werden, wann Besucher von der Mobile App zu ihrer mobilen Website oder zu anderen Domains wechseln. Mithilfe der Domain-übergreifenden ID-Freigabe von Web SDK kann das Marketing-Team Besuchende über ihre Web-Eigenschaften hinweg genau verfolgen und Aktivitätsberichte erstellen.

## Voraussetzungen {#prerequisites}

Um die Freigabe von Mobile-zu-Web- und Domain-übergreifenden IDs zu verwenden, müssen Sie [!DNL Web SDK] Version 2.11.0 oder höher verwenden.

Bei Edge Network Mobile-Implementierungen wird diese Funktion in der Erweiterung [Identität für Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) ab Version 1.1.0 (iOS und Android) unterstützt.

Diese Funktion ist auch mit [!DNL VisitorAPI.js] Version 1.7.0 oder höher kompatibel.

## Mobile-zu-Web-ID-Freigabe {#mobile-to-web}

Verwenden Sie die `getUrlVariables`-API aus der [Identität für Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables)-Erweiterung, um die Kennungen als Abfrageparameter abzurufen und sie beim Öffnen von [!DNL webViews] an Ihre URL anzuhängen.

Es ist keine zusätzliche Konfiguration erforderlich, damit Web SDK `ECID` Werte in der Abfragezeichenfolge akzeptiert.

Der Abfragezeichenfolgenparameter enthält:

* `MCID`: Die Experience Cloud-ID (`ECID`)
* `MCORGID`: Die Experience Cloud-`orgID`, die mit den in der `orgID` konfigurierten [!DNL Web SDK] übereinstimmen muss.
* `TS`: Ein Zeitstempelparameter, der nicht älter als fünf Minuten sein darf.


Die Freigabe der Mobile-zu-Web-IDs verwendet den `adobe_mc`. Wenn der `adobe_mc` vorhanden und gültig ist, wird der `ECID` aus der Abfragezeichenfolge bei der ersten Anfrage an die Edge Network automatisch zur Identitätszuordnung hinzugefügt. Alle nachfolgenden Edge Network-Interaktionen verwenden diese `ECID`.

Weitere Informationen zum Übergeben von Besucher-IDs von einer Mobile App an eine WebView finden Sie in der Dokumentation unter [ von WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Domain-übergreifende ID-Freigabe implementieren {#cross-domain-sharing}

Siehe die folgenden Links, je nachdem, wie Sie die Web-SDK konfiguriert haben:

* **JavaScript-Bibliothek**: [`appendIdentityToUrl`](../../js/commands/appendidentitytourl.md) Befehl
* **Tag-Erweiterung**: [Mit Identität umleiten](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) Aktion
