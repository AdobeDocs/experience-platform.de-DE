---
title: Freigabe von Mobilgeräte für das Internet und domänenübergreifende IDs
description: Erfahren Sie, wie Sie Besucher-IDs von mobilen auf Web-Eigenschaften und domänenübergreifend beibehalten können.
keywords: Identität; mobil; ID; Freigabe; Domäne; domänenübergreifend; SDK; Plattform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 3b65143e33804b251f888dbe2a69d238b3f4cda3
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---

# Freigabe von Mobilgeräte für das Internet und domänenübergreifende IDs

## Übersicht

Das Adobe Experience Platform Web SDK unterstützt Funktionen zur Freigabe von Besucher-IDs, mit denen Kunden personalisierte Erlebnisse präziser zwischen mobilen Apps und mobilen Webinhalten sowie domänenübergreifend bereitstellen können.

## Anwendungsfälle {#use-cases}

### Einheitliche Personalisierung zwischen mobilen Apps und mobilen Websites

Ein Bekleidungsunternehmen möchte das Kundenerlebnis auf der Grundlage seiner Interessen personalisieren und die Personalisierung in einer Mobile App, die auch WebViews lädt, präzise halten. Durch die Verwendung der Funktion zur Freigabe von mobilen IDs können sie sicherstellen, dass Kunden die präzisesten Angebote unterbreitet werden. Dabei wird dieselbe Besucherkennung in der App und der mobile Webinhalt verwendet, indem die Variable [!DNL ECID] zur mobilen Web-URL.

### Konsistente Personalisierung domänenübergreifend bereitstellen

Ein Einzelhändler mit mehreren Online-Stores möchte das Kundenerlebnis über seine Domänen hinweg personalisieren, basierend auf Kundeninteressen. Mithilfe der domänenübergreifenden ID-Freigabe-Funktion des Web SDK kann der Einzelhändler auf der Grundlage von Kundeninteressen präzise Angebote für alle ihre Domänen bereitstellen.

### Berichte zu Besucheraktivitäten verbessern

Ein Technologie-Händler möchte die Berichte zu Besucheraktivitäten verbessern und dabei Informationen darüber erhalten, wann seine Besucher von der Mobile App zur mobilen Website oder zu ihren anderen Domänen wechseln. Mithilfe der domänenübergreifenden ID-Freigabe-Funktion des Web SDK kann das Marketing-Team Besucher über ihre Webeigenschaften hinweg genau verfolgen und Aktivitätsberichte generieren.

## Voraussetzungen {#prerequisites}

Um die Freigabe mobiler und domänenübergreifender IDs zu verwenden, müssen Sie [!DNL Web SDK] Version 2.11.0 oder höher.

Bei mobilen Implementierungen von Edge Network wird diese Funktion im Abschnitt [Identität für Edge Network](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) -Erweiterung ab Version 1.1.0 (iOS und Android).

Diese Funktion ist auch mit [!DNL VisitorAPI.js] Version 1.7.0 oder höher.

## Freigabe mobiler oder Web-IDs {#mobile-to-web}

Verwenden Sie die `getUrlVariables` API von [Identität für Edge Network](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) Erweiterung, um die IDs als Abfrageparameter abzurufen und sie beim Öffnen an Ihre URL anzuhängen [!DNL webViews].

Es ist keine zusätzliche Konfiguration erforderlich, damit das Web SDK `ECID` -Werte in der Abfragezeichenfolge.

Der Abfragezeichenfolgenparameter umfasst:

* `MCID`: Die Experience Cloud-ID (`ECID`)
* `MCORGID`: Das Experience Cloud `orgID` muss mit dem `orgID` in der [!DNL Web SDK].
* `TS`: Ein Zeitstempelparameter, der nicht älter als fünf Minuten sein darf.


Die Freigabe von Mobile-to-Web-IDs verwendet die `adobe_mc` Parameter. Wenn die `adobe_mc` -Parameter vorhanden und gültig ist, wird die `ECID` aus der Abfragezeichenfolge wird bei der ersten Anfrage an das Edge-Netzwerk automatisch zur Identitätszuordnung hinzugefügt. Alle nachfolgenden Edge Network-Interaktionen verwenden diese `ECID`.

Weitere Informationen zur Übergabe von Besucher-IDs von einer mobilen App an eine WebView finden Sie in der Dokumentation unter [Umgang mit WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Domänenübergreifende ID-Freigabe {#cross-domain-sharing}

Für die domänenübergreifende ID-Freigabe bietet das Web SDK Version 2.11.0 Unterstützung für die `appendIdentityToUrl` Befehl. Wenn dieser Befehl verwendet wird, generiert er die `adobe_mc` Abfragezeichenfolgen-Parameter.

Der Befehl akzeptiert ein Objekt mit einer Eigenschaft, `url`und gibt ein Objekt mit der Eigenschaft zurück `url`.

Dieser Befehl wartet nicht auf eine Aktualisierung der Zustimmung. Wenn keine Zustimmung erteilt wurde, wird die URL unverändert zurückgegeben.

Wenn eine `ECID` nicht angegeben wird, wird die `/acquire` Endpunkt wird aufgerufen, um eine `ECID`.

Im Folgenden finden Sie ein Beispiel dafür, wie ein Kunde die domänenübergreifende ID-Freigabe auf seiner Website implementieren kann.

Dieser Code fügt einen Ereignis-Listener für alle Klicks auf der Seite hinzu und wenn der Klick auf einen Link zu einer entsprechenden Domäne erfolgte (in diesem Fall `adobe.com` oder `behance.com`), fügt die Identität zur URL hinzu und leitet den Benutzer dorthin weiter.

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## Verwenden der Tag-Erweiterung {#tags-extension}

Ähnlich wie bei der Verwendung von [!DNL Web SDK], ist keine zusätzliche Konfiguration erforderlich in der [!DNL Tags] -Erweiterung verwenden, um Identitäten zu verwenden, die über die URL übergeben werden.

Um die Freigabe mobiler, Web- und domänenübergreifender IDs über die Tag-Erweiterung zu verwenden, müssen Sie Version 2.12.0 oder höher der Tag-Erweiterung verwenden.

Um Identitäten von der aktuellen Seite für andere Domänen freizugeben, gibt es eine neue Aktion im [!DNL Web SDK] [!DNL Tags] -Erweiterung. Diese Aktion ist für die Verwendung mit einer **[!UICONTROL Core - Click]** Ereignistyp und eine Wertvergleichsbedingung.

Führen Sie die beschriebenen Schritte aus [here](../../tags/ui/managing-resources/rules.md) , um eine Regel mit der folgenden Konfiguration zu erstellen:

* [!UICONTROL Ereigniskonfiguration]:
   * **[!UICONTROL Erweiterung: Core]**
   * **[!UICONTROL Ereignistyp: Klicken]**
   * Auswählen **[!UICONTROL Wenn der Benutzer auf > spezifische Elemente klickt]**
   * Geben Sie im Feld **[!UICONTROL Selektor]**: `a[href]`. Dieses Ereignis wird jedes Mal Trigger, wenn ein Anker-Tag auf der Seite mit einer `href` -Eigenschaft.

      ![UI-Bild, das die Ereigniskonfiguration mit den oben beschriebenen Einstellungen anzeigt](assets/id-sharing-event-configuration.png)

* [!UICONTROL Bedingungskonfiguration]
   * **[!UICONTROL Logiktyp]**: [!UICONTROL Normal]
   * **[!UICONTROL Erweiterung]**: [!UICONTROL Core]
   * **[!UICONTROL Bedingungstyp]**: [!UICONTROL Wertvergleich]
   * **[!UICONTROL Linke Opera]**: [!UICONTROL `%this.hostname%`]. Dies ist ein spezielles Datenelement, das mit [!UICONTROL Core - Click] -Ereignisse und wird zum Hostnamen des angeklickten Links aufgelöst.
   * **[!UICONTROL Operator]**: [!UICONTROL Stimmt überein mit Regex]
   * **[!UICONTROL Rechter Operand]**: Geben Sie einen regulären Ausdruck ein, der mit den Domänen übereinstimmt, für die Sie Identitäten freigeben möchten. So können Sie beispielsweise Links mit Hostnamen abgleichen, die auf `adobe.com` oder `behance.com`verwenden Sie diesen regulären Ausdruck: `behance.com$|adobe.com$`. Die verknüpfte Seite muss die [!DNL Web SDK] oder [!DNL Visitor ID] installiert, um die Identität zu akzeptieren.

      ![UI-Bild, das die Bedingungskonfiguration mit den oben beschriebenen Einstellungen anzeigt](assets/id-sharing-condition-configuration.png)

* [!UICONTROL Aktionskonfiguration]
   * **[!UICONTROL Erweiterung]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Aktionstyp]**: [!UICONTROL Umleiten mit Identität]
   * **[!UICONTROL Instanz]**: Wählen Sie Ihre Instanz aus. In den meisten Fällen ist nur eine Instanz konfiguriert. Wenn mehrere Instanzen vorhanden sind, wählen Sie die Instanz mit der Identität aus, die Sie freigeben möchten.

      ![UI-Bild, das die Aktionskonfiguration mit den oben beschriebenen Einstellungen anzeigt](assets/id-sharing-action-configuration.png)

Die **[!UICONTROL Umleiten mit Identität]** -Aktion verhindert, dass der Browser durch den Link navigiert. Anschließend wird die `appendIdentityToUrl` -Methode [!DNL Web SDK] -Instanz.

Schließlich wird der Benutzer zum [!DNL URL] mit dem `adobe_mc` Abfragezeichenfolgenparameter angehängt.
