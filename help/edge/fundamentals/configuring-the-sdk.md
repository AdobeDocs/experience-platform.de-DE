---
title: Adobe Experience Platform Web SDK konfigurieren
description: Erfahren Sie, wie Sie das Adobe Experience Platform Web SDK konfigurieren.
seo-description: Erfahren Sie, wie Sie das Experience Platform Web SDK konfigurieren
keywords: configure;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;Umgebung;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;webSDK-Einstellungen;prehidingStyle;opacity;cookieDestinationEnabled;urlDestination Enabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
translation-type: tm+mt
source-git-commit: 2895975b9c103e6afba7db221223b4ef2116caf3
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 39%

---

# Plattform-Web-SDK konfigurieren

Die Konfiguration für das SDK erfolgt mit dem `configure`-Befehl.

>[!IMPORTANT]
>
>`configure` ist  ** immer der erste Befehl namens.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Es gibt viele Optionen, die während der Konfiguration festgelegt werden können. Alle Optionen sind nachstehend nach Kategorie gruppiert aufgeführt.

## Allgemeine Optionen

### `edgeConfigId`

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
| Synchrone Überprüfung | Prüft die für das Schema erfassten Daten und gibt in der Antwort unter der folgenden Beschriftung einen Fehler zurück: `collect:error OR success` |
| Konsolen-Logging | Aktiviert die Anzeige von Debugging-Meldungen in der JavaScript-Konsole des Browsers |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

Füllen Sie dieses Feld mit Ihrer Erstanbieterdomäne. Weitere Informationen finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

Die Domäne ähnelt `data.{customerdomain.com}` für eine Website unter www.{customerdomain.com}.

### `orgId`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

{style=&quot;table-layout:auto&quot;}

Ihre zugeordnete Organisations-ID [!DNL Experience Cloud]. Beim Konfigurieren mehrerer Instanzen innerhalb einer Seite müssen Sie für jede Instanz eine andere `orgId` konfigurieren.

## Datenerfassung

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Gibt an, ob mit Linkklicks verbundene Daten automatisch erfasst werden. Weitere Informationen finden Sie unter [Automatische Linkverfolgung](../data-collection/track-links.md#automaticLinkTracking).

### `onBeforeEventSend`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Funktion | Nein | () => nicht definiert |

{style=&quot;table-layout:auto&quot;}

Konfigurieren Sie einen Rückruf, der für jedes Ereignis kurz vor dem Senden aufgerufen wird. Ein Objekt mit dem Feld `xdm` wird an den Rückruf gesendet. Um zu ändern, was gesendet wird, ändern Sie das `xdm`-Objekt. Innerhalb des Rückrufs werden die Daten für das `xdm`-Objekt bereits im Ereignis-Befehl und die automatisch erfassten Informationen übergeben. Weitere Informationen zum Timing dieses Rückrufs und ein Beispiel finden Sie unter [Globale Änderung von Ereignissen](tracking-events.md#modifying-events-globally).

## Datenschutzoptionen

### `defaultConsent` {#default-consent}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Objekt | Nein | `"in"` |

{style=&quot;table-layout:auto&quot;}

Legt die Standardzustimmung des Nutzers fest. Verwenden Sie diese Einstellung, wenn für den Benutzer keine Voreinstellung für die Zustimmung bereits gespeichert wurde. Die anderen gültigen Werte sind `"pending"` und `"out"`. Dieser Standardwert bleibt nicht auf dem Profil des Benutzers erhalten. Das Profil des Benutzers wird nur aktualisiert, wenn `setConsent` aufgerufen wird.
* `"in"`: Wenn diese Einstellung festgelegt ist oder kein Wert angegeben wird, wird die Arbeit ohne Benutzereinwilligung fortgesetzt.
* `"pending"`: Wenn diese Einstellung festgelegt ist, wird die Arbeit in die Warteschlange gestellt, bis der Benutzer die Voreinstellungen für die Zustimmung bereitstellt.
* `"out"`: Wenn diese Einstellung festgelegt ist, wird die Arbeit verworfen, bis der Benutzer seine Zustimmung erteilt.
Nachdem die Voreinstellungen des Nutzers bereitgestellt wurden, wird die Arbeit basierend auf den Voreinstellungen des Nutzers entweder fortgesetzt oder abgebrochen. Weitere Informationen finden Sie unter [Unterstützen von Zustimmung](../consent/supporting-consent.md).

## Personalisierungsoptionen

### `prehidingStyle`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Nein | Keine |

{style=&quot;table-layout:auto&quot;}

Wird verwendet, um eine CSS-Stildefinition zu erstellen, die Inhaltsbereiche Ihrer Web-Seite ausblendet, während personalisierter Inhalt vom Server geladen wird. Wenn diese Option nicht bereitgestellt wird, versucht das SDK nicht, Inhaltsbereiche auszublenden, während personalisierte Inhalte geladen werden, was möglicherweise zu einem Flackern führt.

Beispiel: Wenn ein Element auf Ihrer Webseite die ID `container` aufweist, deren Standardinhalt Sie ausblenden möchten, während personalisierter Inhalt vom Server geladen wird, verwenden Sie den folgenden Prähiding-Stil:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Optionen für Zielgruppen

### `cookieDestinationsEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Aktiviert die Cookie-Ziele [!DNL Audience Manager], wodurch Cookies basierend auf der Segmentqualifizierung gesetzt werden können.

### `urlDestinationsEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Aktiviert URL-Ziele [!DNL Audience Manager], was das Auslösen von URLs auf Grundlage der Segmentqualifikation ermöglicht.

## Identitätsoptionen

### `idMigrationEnabled` {#id-migration-enabled}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Wenn &quot;true&quot;, liest und setzt das SDK alte AMCV-Cookies. Diese Option unterstützt den Übergang zur Verwendung des Adobe Experience Platform Web SDK, während einige Teile der Site möglicherweise weiterhin Besucher.js verwenden. Wenn die Besucher-API auf der Seite definiert ist, die SDK Abfragen Besucher-API für die ECID. Mit dieser Option können Sie Seiten mit zwei Tags mit dem Adobe Experience Platform Web SDK versehen und immer noch die gleiche ECID haben.

### `thirdPartyCookiesEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style=&quot;table-layout:auto&quot;}

Aktiviert die Einstellung von Adobe-Drittanbieter-Cookies. Das SDK kann die Besucher-ID in einem Drittanbieterkontext beibehalten, um die Verwendung derselben Besucher-ID für mehrere Sites zu ermöglichen. Verwenden Sie diese Option, wenn Sie mehrere Sites haben oder Daten mit Partnern teilen möchten. Manchmal ist diese Option aus Datenschutzgründen nicht erwünscht.
