---
title: Adobe Experience Platform Web SDK konfigurieren
description: Erfahren Sie, wie Sie das Adobe Experience Platform Web SDK konfigurieren.
seo-description: Erfahren Sie, wie Sie das Experience Platform Web SDK konfigurieren
keywords: configure;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;Umgebung;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;webSDK-Einstellungen;prehidingStyle;opacity;cookieDestinationEnabled;urlDestination Enabled;idMigrationEnabled;thirdPartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: f78da58ba7a593d9c161030833d9b69e2ba57c9a
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 64%

---


# Plattform-Web-SDK konfigurieren

Die Konfiguration für das SDK erfolgt mit dem `configure`-Befehl.

>[!IMPORTANT]
>
>`configure` sollte *immer* als erster Befehl abgerufen werden.

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

Ihre zugewiesene Konfigurations-ID, die das SDK mit den entsprechenden Konten und Konfigurationen verknüpft.  Beim Konfigurieren mehrerer Instanzen innerhalb einer einzelnen Seite müssen Sie für jede Instanz eine andere `edgeConfigId` konfigurieren.

### `context`

| **Typ** | **Erforderlich** | **Standardwert** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array von Zeichenfolgen | Nein | `["web", "device", "environment", "placeContext"]` |

Gibt an, welche Kontextkategorien automatisch erfasst werden sollen, wie unter [Automatische Informationen](../data-collection/automatic-information.md) beschrieben.  Wenn diese Konfiguration nicht angegeben ist, werden standardmäßig alle Kategorien verwendet.

### `debugEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `false` |

Gibt an, ob Debugging aktiviert werden soll. Durch das Festlegen dieser Konfiguration auf `true` werden die folgenden Funktionen aktiviert:

| **Funktion** | **Funktion** |
| ---------------------- | ------------------ |
| Synchrone Überprüfung | Prüft die für das Schema erfassten Daten und gibt in der Antwort unter der folgenden Beschriftung einen Fehler zurück: `collect:error OR success` |
| Konsolen-Logging | Aktiviert die Anzeige von Debugging-Meldungen in der JavaScript-Konsole des Browsers |

### `edgeDomain` {#edge-domain}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ------------------ |
| Zeichenfolge | Nein | `beta.adobedc.net` |
| Zeichenfolge | Nein | `omtrdc.net` |

Die Domäne, die für die Interaktion mit Adobe-Diensten verwendet wird. Wird nur verwendet, wenn Sie über eine Erstanbieter-Domäne (CNAME) verfügen, die Anforderungen an die Adobe Edge-Infrastruktur weiterleitet.

### `orgId`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

Ihre zugeordnete Organisations-ID [!DNL Experience Cloud].  Beim Konfigurieren mehrerer Instanzen innerhalb einer Seite müssen Sie für jede Instanz eine andere `orgId` konfigurieren.

## Datenerfassung

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

Gibt an, ob mit Link-Klicks verbundene Daten automatisch erfasst werden sollen. Weitere Informationen finden Sie unter [Automatische Linkverfolgung](../data-collection/track-links.md#automaticLinkTracking).

### `onBeforeEventSend`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Funktion | Nein | () => nicht definiert |

Legen Sie dies fest, um einen Rückruf zu konfigurieren, der für jedes Ereignis kurz vor dem Senden aufgerufen wird.  Ein Objekt mit dem Feld `xdm` wird an den Rückruf gesendet.  Ändern Sie das `xdm`-Objekt, um die gesendeten Daten zu ändern.  Innerhalb des Rückrufs werden dem `xdm`-Objekt bereits die Daten im Ereignisbefehl und die automatisch erfassten Informationen übergeben. Weitere Informationen zum Timing dieses Rückrufs und ein Beispiel finden Sie unter [Globale Änderung von Ereignissen](tracking-events.md#modifying-events-globally).

## Datenschutzoptionen

### `defaultConsent` {#default-consent}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Objekt | Nein | `"in"` |

Legt die Standardzustimmung des Nutzers fest. Wird verwendet, wenn für den Nutzer noch keine Voreinstellung für die Zustimmung gespeichert wurde. Die anderen gültigen Werte sind `"pending"` und `"out"`. Dieser Standardwert bleibt nicht auf dem Profil des Benutzers erhalten. Nur wenn setConsent aufgerufen wird, wird das Profil des Benutzers aktualisiert.
* `"in"`: Wenn dieser Wert festgelegt ist oder kein Wert angegeben wird, wird die Arbeit ohne Benutzereinwilligung fortgesetzt.
* `"pending"`: Wenn dies festgelegt ist, wird die Arbeit in die Warteschlange gestellt, bis der Nutzer die Zustimmungseinstellungen eingibt.
* `"out"`: Wenn dies festgelegt ist, werden die Arbeiten verworfen, bis der Benutzer seine Zustimmung erteilt.
Nachdem die Voreinstellungen des Nutzers bereitgestellt wurden, wird die Arbeit basierend auf den Voreinstellungen des Nutzers entweder fortgesetzt oder abgebrochen. Weitere Informationen finden Sie unter [Unterstützen von Zustimmung](../consent/supporting-consent.md).

## Personalisierungsoptionen

### `prehidingStyle`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Nein | Keine |

Wird verwendet, um eine CSS-Stildefinition zu erstellen, die Inhaltsbereiche Ihrer Web-Seite ausblendet, während personalisierter Inhalt vom Server geladen wird. Wenn diese Option nicht bereitgestellt wird, versucht das SDK nicht, Inhaltsbereiche auszublenden, während personalisierte Inhalte geladen werden, was möglicherweise zu einem Flackern führt.

Wenn Sie z. B. ein Element auf Ihrer Web-Seite mit einer Kennung von `container` haben, dessen Standardinhalt Sie ausblenden möchten, während personalisierter Inhalt vom Server geladen wird, wäre ein Beispiel für einen Vorabausblendungsstil wie folgt:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Optionen für Zielgruppen

### `cookieDestinationsEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

Aktiviert die Cookie-Ziele [!DNL Audience Manager], wodurch Cookies basierend auf der Segmentqualifizierung gesetzt werden können.

### `urlDestinationsEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

Aktiviert URL-Ziele [!DNL Audience Manager], was das Auslösen von URLs auf Grundlage der Segmentqualifikation ermöglicht.

## Identitätsoptionen

### `idMigrationEnabled` {#id-migration-enabled}

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | wahr |

Wenn &quot;true&quot;, liest das SDK alte AMCV-Cookies und legt sie fest. Dies hilft beim Übergang zur Verwendung des Adobe Experience Platform Web SDK, während einige Teile der Site möglicherweise noch Besucher.js verwenden. Wenn die Besucher-API auf der Seite definiert ist, wird vom SDK außerdem die Besucher-API für die ECID Abfrage. Auf diese Weise können Sie zwei Tags mit dem Adobe Experience Platform Web SDK verwenden und immer noch dieselbe ECID haben.

### `thirdPartyCookiesEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | wahr |

Aktiviert die Einstellung von Adobe-Drittanbieter-Cookies. Das SDK kann die Besucher-ID in einem Drittanbieterkontext beibehalten, um die Verwendung derselben Besucher-ID für mehrere Sites zu ermöglichen. Dies ist nützlich, wenn Sie mehrere Sites haben oder Daten mit Partnern teilen möchten. Dies ist jedoch manchmal aus Datenschutzgründen nicht wünschenswert.
