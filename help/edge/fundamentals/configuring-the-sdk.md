---
title: Konfigurieren des SDK
seo-title: Konfigurieren des Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie das Experience Platform Web SDK konfigurieren
seo-description: Erfahren Sie, wie Sie das Experience Platform Web SDK konfigurieren
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 86%

---


# Konfigurieren des SDK

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

Gibt an, welche Kontextkategorien automatisch erfasst werden sollen, wie unter [Automatische Informationen](../reference/automatic-information.md) beschrieben.  Wenn diese Konfiguration nicht angegeben ist, werden standardmäßig alle Kategorien verwendet.

### `debugEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `false` |

Gibt an, ob Debugging aktiviert werden soll. Durch das Festlegen dieser Konfiguration auf `true` werden die folgenden Funktionen aktiviert:

| **Funktion** | **Funktion** |
| ---------------------- | ------------------ |
| Synchrone Überprüfung | Prüft die für das Schema erfassten Daten und gibt in der Antwort unter der folgenden Beschriftung einen Fehler zurück: `collect:error OR success` |
| Konsolen-Logging | Aktiviert die Anzeige von Debugging-Meldungen in der JavaScript-Konsole des Browsers |

### `edgeDomain`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ------------------ |
| Zeichenfolge | Nein | `beta.adobedc.net` |

Die Domäne, die für die Interaktion mit Adobe-Diensten verwendet wird. Wird nur verwendet, wenn Sie über eine Erstanbieter-Domäne (CNAME) verfügen, die Anforderungen an die Adobe Edge-Infrastruktur weiterleitet.

### `orgId`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

Your assigned [!DNL Experience Cloud] organization ID.  Beim Konfigurieren mehrerer Instanzen innerhalb einer Seite müssen Sie für jede Instanz eine andere `orgId` konfigurieren.

## Datenerfassung

### `clickCollectionEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

Gibt an, ob mit Link-Klicks verbundene Daten automatisch erfasst werden sollen. Für Klicks, die als Link-Klicks gelten, werden die folgenden [Web-Interaktionsdaten](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) erfasst:

| **Eigenschaft** | **Beschreibung** |
| ------------ | ----------------------------------- |
| Link-Name | Durch den Link-Kontext bestimmter Name |
| Link-URL | Normalisierte URL |
| Link-Typ | Auf Herunterladen, Beenden oder Sonstiges festlegen |

### `onBeforeEventSend`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Funktion | Nein | () => nicht definiert |

Legen Sie dies fest, um einen Rückruf zu konfigurieren, der für jedes Ereignis kurz vor dem Senden aufgerufen wird.  Ein Objekt mit dem Feld `xdm` wird an den Rückruf gesendet.  Modify the `xdm` object to change what is sent.  Innerhalb des Rückrufs werden dem `xdm`-Objekt bereits die Daten im Ereignisbefehl und die automatisch erfassten Informationen übergeben.  Weitere Informationen zum Timing dieses Rückrufs und ein Beispiel finden Sie unter [Globale Änderung von Ereignissen](tracking-events.md#modifying-events-globally).

## Datenschutzoptionen

### `defaultConsent`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Objekt | Nein | `{"general": "in"}` |

Legt die Standardzustimmung des Nutzers fest. Wird verwendet, wenn für den Nutzer noch keine Voreinstellung für die Zustimmung gespeichert wurde. Der andere gültige Wert ist `{"general": "pending"}`. Wenn dies festgelegt ist, wird die Arbeit in die Warteschlange gestellt, bis der Nutzer die Zustimmungseinstellungen eingibt. Nachdem die Voreinstellungen des Nutzers bereitgestellt wurden, wird die Arbeit basierend auf den Voreinstellungen des Nutzers entweder fortgesetzt oder abgebrochen. Weitere Informationen finden Sie unter [Unterstützen von Zustimmung](supporting-consent.md).

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

Enables [!DNL Audience Manager] [!UICONTROL cookie destinations], which allows the setting of cookies based on segment qualification.

### `urlDestinationsEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

Enables [!DNL Audience Manager] [!UICONTROL URL destinations], which allows the firing of URLs based on segment qualification.

## Identitätsoptionen

### `idSyncContainerId`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zahl | Nein | Keine |

Die Container-ID, die angibt, welche ID-Synchronisierungen ausgelöst werden. Dies ist eine nicht negative Ganzzahl, die Sie von Ihrem Berater erhalten können.

### `idSyncEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

Aktiviert die ID-Synchronisierungsfunktion, mit der URLs ausgelöst werden können, um die individuelle Adobe-Nutzerkennung mit der individuellen Nutzerkennung einer Drittanbieter-Datenquelle zu synchronisieren.

### `thirdPartyCookiesEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | wahr |

Aktiviert die Einstellung von Adobe-Drittanbieter-Cookies. Das SDK kann die Besucher-ID in einem Drittanbieterkontext beibehalten, um die Verwendung derselben Besucher-ID für mehrere Sites zu ermöglichen. Dies ist nützlich, wenn Sie mehrere Sites haben oder Daten mit Partnern teilen möchten. Dies ist jedoch manchmal aus Datenschutzgründen nicht wünschenswert.
