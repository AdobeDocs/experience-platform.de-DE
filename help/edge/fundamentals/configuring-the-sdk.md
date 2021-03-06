---
title: Konfigurieren des Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie das Adobe Experience Platform Web SDK konfigurieren.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: configure;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;environment;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk settings;prehidingStyle;opacity;cookieDestinationsEnabled;urlDestinations Enabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: 4d0f1b3e064bd7b24e17ff0fafb50d930b128968
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 39%

---

# Konfigurieren des Platform Web SDK

Die Konfiguration für das SDK erfolgt mit dem `configure`-Befehl.

>[!IMPORTANT]
>
>`configure` is *always* der erste Befehl mit dem Namen .

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Es gibt viele Optionen, die während der Konfiguration festgelegt werden können. Alle Optionen sind nachstehend nach Kategorie gruppiert aufgeführt.

## Allgemeine Optionen

### `edgeConfigId`

>[!NOTE]
>
>**Edge-Konfigurationen wurden in Datastreams umbenannt. Eine Datastream-ID entspricht einer Konfigurations-ID.**

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

{style=&quot;table-layout:auto&quot;}

Ihre zugewiesene Konfigurations-ID, die das SDK mit den entsprechenden Konten und Konfigurationen verknüpft. Beim Konfigurieren mehrerer Instanzen innerhalb einer einzelnen Seite müssen Sie für jede Instanz eine andere `edgeConfigId` konfigurieren.

### `context`

| **Typ** | **Erforderlich** | **Standardwert** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array von Zeichenfolgen | Nein | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

Gibt an, welche Kontextkategorien automatisch erfasst werden sollen, wie unter [Automatische Informationen](../data-collection/automatic-information.md) beschrieben. Wenn diese Konfiguration nicht angegeben ist, werden standardmäßig alle Kategorien verwendet.

### `debugEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `false` |

{style=&quot;table-layout:auto&quot;}

Gibt an, ob das Debugging aktiviert ist. Durch das Festlegen dieser Konfiguration auf `true` werden die folgenden Funktionen aktiviert:

| **Funktion** | **Funktion** |
| ---------------------- | ------------------ |
| Konsolen-Logging | Aktiviert die Anzeige von Debugging-Meldungen in der JavaScript-Konsole des Browsers |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

Füllen Sie dieses Feld mit Ihrer Erstanbieterdomäne aus. Weitere Informationen finden Sie im [Dokumentation](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=de).

Die Domäne ähnelt dem `data.{customerdomain.com}` für eine Website unter www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Pfad nach der edgeDomain, die zur Kommunikation und Interaktion mit Adobe-Diensten verwendet wird.  Häufig würde sich dies nur ändern, wenn nicht die standardmäßige Produktionsumgebung verwendet wird.

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Nein | ee |

{style=&quot;table-layout:auto&quot;}

### `orgId`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

{style=&quot;table-layout:auto&quot;}

Ihr zugewiesener [!DNL Experience Cloud] Organisations-ID. Beim Konfigurieren mehrerer Instanzen innerhalb einer Seite müssen Sie für jede Instanz eine andere `orgId` konfigurieren.

## Datenerfassung

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Gibt an, ob mit Link-Klicks verknüpfte Daten automatisch erfasst werden. Siehe [Automatische Linktracking](../data-collection/track-links.md#automaticLinkTracking) für weitere Informationen. Links werden auch als Downloadlinks bezeichnet, wenn sie ein Download-Attribut enthalten oder wenn der Link mit einer Dateierweiterung endet. Downloadlink-Qualifikatoren können mit einem regulären Ausdruck konfiguriert werden. Der Standardwert lautet `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Funktion | Nein | () => nicht definiert |

{style=&quot;table-layout:auto&quot;}

Konfigurieren Sie einen Callback, der für jedes Ereignis kurz vor dem Senden aufgerufen wird. Ein Objekt mit dem Feld `xdm` wird an den Rückruf gesendet. Um die gesendeten Nachrichten zu ändern, ändern Sie die `xdm` -Objekt. Innerhalb des Rückrufs wird die `xdm` -Objekt enthält bereits die Daten, die im Ereignisbefehl übergeben werden, und die automatisch erfassten Informationen. Weitere Informationen zum Timing dieses Rückrufs und ein Beispiel finden Sie unter [Globale Änderung von Ereignissen](tracking-events.md#modifying-events-globally).

## Datenschutzoptionen

### `defaultConsent` {#default-consent}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Objekt | Nein | `"in"` |

{style=&quot;table-layout:auto&quot;}

Legt die Standardzustimmung des Nutzers fest. Verwenden Sie diese Einstellung, wenn für den Benutzer keine Zustimmungsvoreinstellung gespeichert wurde. Die anderen gültigen Werte sind `"pending"` und `"out"`. Dieser Standardwert wird nicht im Profil des Benutzers beibehalten. Das Benutzerprofil wird nur aktualisiert, wenn `setConsent` aufgerufen wird.
* `"in"`: Wenn diese Einstellung festgelegt ist oder kein Wert angegeben wird, wird die Arbeit ohne Voreinstellungen für die Benutzerzustimmung fortgesetzt.
* `"pending"`: Wenn diese Einstellung festgelegt ist, wird die Arbeit in die Warteschlange gestellt, bis der Benutzer Zustimmungsvoreinstellungen bereitstellt.
* `"out"`: Wenn diese Einstellung festgelegt ist, wird die Arbeit verworfen, bis der Benutzer Zustimmungsvoreinstellungen bereitstellt.
Nachdem die Voreinstellungen des Nutzers bereitgestellt wurden, wird die Arbeit basierend auf den Voreinstellungen des Nutzers entweder fortgesetzt oder abgebrochen. Weitere Informationen finden Sie unter [Unterstützen von Zustimmung](../consent/supporting-consent.md).

## Personalisierungsoptionen

### `prehidingStyle`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Nein | Keine |

{style=&quot;table-layout:auto&quot;}

Wird verwendet, um eine CSS-Stildefinition zu erstellen, die Inhaltsbereiche Ihrer Web-Seite ausblendet, während personalisierter Inhalt vom Server geladen wird. Wenn diese Option nicht bereitgestellt wird, versucht das SDK nicht, Inhaltsbereiche beim Laden personalisierter Inhalte auszublenden, was möglicherweise zu einem &quot;Flackern&quot;führt.

Wenn beispielsweise ein Element auf Ihrer Web-Seite die ID `container`, deren Standardinhalt Sie ausblenden möchten, während personalisierter Inhalt vom Server geladen wird, verwenden Sie den folgenden Stil für die Vorab-Ausblendung:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Optionen für Zielgruppen

### `cookieDestinationsEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Aktiviert [!DNL Audience Manager] Cookie-Ziele, die das Setzen von Cookies basierend auf der Segmentqualifizierung ermöglichen.

### `urlDestinationsEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Aktiviert [!DNL Audience Manager] URL-Ziele, die das Auslösen von URLs basierend auf der Segmentqualifizierung ermöglichen.

## Identitätsoptionen

### `idMigrationEnabled` {#id-migration-enabled}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Wenn &quot;true&quot;, liest und setzt das SDK alte AMCV-Cookies. Diese Option hilft beim Übergang zur Verwendung des Adobe Experience Platform Web SDK, während einige Teile der Site möglicherweise noch Visitor.js verwenden. Wenn die Besucher-API auf der Seite definiert ist, fragt das SDK die Besucher-API für die ECID ab. Mit dieser Option können Sie Seiten mit dem Adobe Experience Platform Web SDK doppelt taggen, die immer noch dieselbe ECID aufweisen.

### `thirdPartyCookiesEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Aktiviert die Einstellung von Adobe-Drittanbieter-Cookies. Das SDK kann die Besucher-ID in einem Drittanbieterkontext beibehalten, damit dieselbe Besucher-ID siteübergreifend verwendet werden kann. Verwenden Sie diese Option, wenn Sie mehrere Sites haben oder Daten mit Partnern teilen möchten. Manchmal ist diese Option jedoch aus Datenschutzgründen nicht wünschenswert.
