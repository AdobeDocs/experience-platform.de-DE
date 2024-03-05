---
title: Mobile-zu-Web und Domain-übergreifender ID-Austausch
description: Erfahren Sie, wie Sie Besucher-IDs von mobilen auf Web-Eigenschaften und domänenübergreifend beibehalten können.
keywords: Identität; mobil; ID; Freigabe; Domäne; domänenübergreifend; SDK; Plattform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 3%

---

# Mobile-zu-Web und Domain-übergreifender ID-Austausch

## Übersicht

Das Adobe Experience Platform Web SDK unterstützt Funktionen zur Freigabe von Besucher-IDs, mit denen Kunden personalisierte Erlebnisse präziser zwischen mobilen Apps und mobilen Webinhalten sowie domänenübergreifend bereitstellen können.

## Anwendungsfälle {#use-cases}

### Einheitliche Personalisierung zwischen mobilen Apps und mobilen Websites

Ein Bekleidungsunternehmen möchte das Kundenerlebnis auf der Grundlage seiner Interessen personalisieren und die Personalisierung in einer Mobile App, die auch WebViews lädt, präzise halten. Durch die Verwendung der Funktion zur Freigabe von mobilen IDs können sie sicherstellen, dass Kunden die präzisesten Angebote unterbreitet werden. Dabei wird dieselbe Besucherkennung in der App und der mobile Webinhalt verwendet, indem die Variable [!DNL ECID] zur mobilen Web-URL.

### Konsistente Personalisierung über Domänen hinweg

Ein Einzelhändler mit mehreren Online-Stores möchte das Kundenerlebnis über seine Domänen hinweg personalisieren, basierend auf Kundeninteressen. Mithilfe der domänenübergreifenden ID-Freigabe-Funktion des Web SDK kann der Einzelhändler auf der Grundlage von Kundeninteressen präzise Angebote für alle ihre Domänen bereitstellen.

### Berichte zu Besucheraktivitäten verbessern

Ein Technologie-Händler möchte die Berichte zu Besucheraktivitäten verbessern und dabei Informationen darüber erhalten, wann seine Besucher von der Mobile App zur mobilen Website oder zu ihren anderen Domänen wechseln. Mithilfe der domänenübergreifenden ID-Freigabe-Funktion des Web SDK kann das Marketing-Team Besucher über ihre Webeigenschaften hinweg genau verfolgen und Aktivitätsberichte generieren.

## Voraussetzungen {#prerequisites}

Um die Freigabe mobiler und domänenübergreifender IDs zu verwenden, müssen Sie [!DNL Web SDK] Version 2.11.0 oder höher.

Bei mobilen Implementierungen von Edge Network wird diese Funktion im Abschnitt [Identität für Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) -Erweiterung ab Version 1.1.0 (iOS und Android).

Diese Funktion ist auch mit [!DNL VisitorAPI.js] Version 1.7.0 oder höher.

## Freigabe mobiler oder Web-IDs {#mobile-to-web}

Verwenden Sie die `getUrlVariables` API von [Identität für Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) Erweiterung, um die IDs als Abfrageparameter abzurufen und sie beim Öffnen an Ihre URL anzuhängen [!DNL webViews].

Es ist keine zusätzliche Konfiguration erforderlich, damit das Web SDK `ECID` -Werte in der Abfragezeichenfolge.

Der Abfragezeichenfolgenparameter umfasst:

* `MCID`: Die Experience Cloud-ID (`ECID`)
* `MCORGID`: Die Experience Cloud `orgID` muss mit dem `orgID` in der [!DNL Web SDK].
* `TS`: Ein Zeitstempelparameter, der nicht älter als fünf Minuten sein darf.


Die Freigabe von Mobile-to-Web-IDs verwendet die `adobe_mc` -Parameter. Wenn die Variable `adobe_mc` -Parameter vorhanden und gültig ist, wird die `ECID` aus der Abfragezeichenfolge wird bei der ersten Anfrage an das Edge-Netzwerk automatisch zur Identitätszuordnung hinzugefügt. Alle nachfolgenden Edge Network-Interaktionen verwenden diese `ECID`.

Weitere Informationen zur Übergabe von Besucher-IDs von einer mobilen App an eine WebView finden Sie in der Dokumentation unter [Umgang mit WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Implementieren der domänenübergreifenden ID-Freigabe {#cross-domain-sharing}

Siehe [`appendIdentityToUrl`](../commands/appendidentitytourl.md) für Implementierungsanweisungen unter Verwendung der Web SDK-Tag-Erweiterung und der Web SDK-JavaScript-Bibliothek.
