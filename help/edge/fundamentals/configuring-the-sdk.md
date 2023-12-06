---
title: Konfigurieren des Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie das Adobe Experience Platform Web SDK konfigurieren.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 24%

---


# Web SDK konfigurieren

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

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

{style="table-layout:auto"}

Ihre zugewiesene Konfigurations-ID, die das SDK mit den entsprechenden Konten und Konfigurationen verknüpft. Beim Konfigurieren mehrerer Instanzen innerhalb einer einzelnen Seite müssen Sie für jede Instanz eine andere `edgeConfigId` konfigurieren.

### `context` {#context}

| **Typ** | Erforderlich | **Standardwert** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array von Zeichenfolgen | Nein | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

Gibt an, welche Kontextkategorien automatisch erfasst werden sollen, wie unter [Automatische Informationen](../data-collection/automatic-information.md). Wenn diese Konfiguration nicht angegeben ist, werden standardmäßig alle Kategorien verwendet.

>[!IMPORTANT]
>
>Alle Kontexteigenschaften, außer für `highEntropyUserAgentHints`, sind standardmäßig aktiviert. Wenn Sie die Kontexteigenschaften in Ihrer Web SDK-Konfiguration manuell angegeben haben, müssen Sie alle Kontexteigenschaften aktivieren, um die erforderlichen Informationen weiterhin erfassen zu können.

Aktivieren [Clienthinweise mit hoher Entropie](user-agent-client-hints.md#enabling-high-entropy-client-hints) in Ihrer Web SDK-Bereitstellung müssen Sie die zusätzlichen `highEntropyUserAgentHints` -Kontextoption neben Ihrer vorhandenen Konfiguration.

Um beispielsweise Hinweise zu hochgradigen Entropy-Clients aus Web-Eigenschaften abzurufen, würde Ihre Konfiguration wie folgt aussehen:

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `false` |

{style="table-layout:auto"}

Gibt an, ob das Debugging aktiviert ist. Durch das Festlegen dieser Konfiguration auf `true` werden die folgenden Funktionen aktiviert:

| **Funktion** | **Funktion** |
| ---------------------- | ------------------ |
| Konsolen-Logging | Aktiviert die Anzeige von Debugging-Meldungen in der JavaScript-Konsole des Browsers |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

Füllen Sie dieses Feld mit Ihrer Erstanbieterdomäne aus. Weitere Informationen finden Sie unter [Dokumentation](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de).

Die Domäne ähnelt dem `data.{customerdomain.com}` für eine Website unter www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Pfad nach der edgeDomain, die zur Kommunikation und Interaktion mit Adobe-Diensten verwendet wird.  Häufig würde sich dies nur ändern, wenn nicht die standardmäßige Produktionsumgebung verwendet wird.

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Nein | ee |

{style="table-layout:auto"}

### `orgId`

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

{style="table-layout:auto"}

Ihr zugewiesener [!DNL Experience Cloud] Organisations-ID. Beim Konfigurieren mehrerer Instanzen innerhalb einer Seite müssen Sie für jede Instanz eine andere `orgId` konfigurieren.

## Datenerfassung

### `clickCollectionEnabled` {#clickCollectionEnabled}

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style="table-layout:auto"}

Gibt an, ob mit Link-Klicks verknüpfte Daten automatisch erfasst werden. Siehe [Automatische Linktracking](../data-collection/track-links.md#automaticLinkTracking) für weitere Informationen. Links werden auch als Downloadlinks bezeichnet, wenn sie ein Download-Attribut enthalten oder wenn der Link mit einer Dateierweiterung endet. Downloadlink-Qualifikatoren können mit einem regulären Ausdruck konfiguriert werden. Der Standardwert ist `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Funktion | Nein | () => nicht definiert |

{style="table-layout:auto"}

Konfigurieren Sie einen Callback, der für jedes Ereignis kurz vor dem Senden aufgerufen wird. Ein Objekt mit dem Feld `xdm` an den Callback gesendet. Um die gesendeten Nachrichten zu ändern, ändern Sie die `xdm` -Objekt. Innerhalb des Rückrufs wird die `xdm` -Objekt enthält bereits die Daten, die im Ereignisbefehl übergeben werden, und die automatisch erfassten Informationen. Weitere Informationen zum Timing dieses Rückrufs und ein Beispiel finden Sie unter [Globale Änderung von Ereignissen](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Funktion | Nein | () => nicht definiert |

{style="table-layout:auto"}

Konfigurieren Sie einen Callback, der für jedes Linkklick-Tracking-Ereignis kurz vor dem Senden aufgerufen wird. Der Rückruf sendet ein Objekt mit der `xdm`, `clickedElement`, und `data` -Felder.

Beim Filtern der Linktracking mithilfe der DOM-Elementstruktur können Sie die `clickElement` Befehl. `clickedElement` ist der DOM-Elementknoten, auf den geklickt wurde und der die Struktur der übergeordneten Knoten enthielt.

Um zu ändern, welche Daten gesendet werden, ändern Sie die `xdm` und/oder `data` Objekte. Innerhalb des Rückrufs wird die `xdm` -Objekt enthält bereits die Daten, die im Ereignisbefehl übergeben werden, und die automatisch erfassten Informationen.

* Ein anderer Wert als `false` ermöglicht die Verarbeitung des Ereignisses und des zu sendenden Rückrufs.
* Wenn der Rückruf die `false` -Wert, wird die Ereignisverarbeitung angehalten, es wird kein Fehler ausgegeben und das Ereignis wird nicht gesendet. Dieser Mechanismus ermöglicht die Filterung bestimmter Ereignisse, indem die Ereignisdaten untersucht und `false` , wenn das Ereignis nicht gesendet werden soll.
* Wenn der Rückruf eine Ausnahme auslöst, wird die Verarbeitung für das Ereignis angehalten und das Ereignis wird nicht gesendet.


## Datenschutzoptionen

### `defaultConsent` {#default-consent}

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Objekt | Nein | `"in"` |

{style="table-layout:auto"}

Legt die Standardzustimmung des Nutzers fest. Verwenden Sie diese Einstellung, wenn für den Benutzer keine Zustimmungsvoreinstellung gespeichert wurde. Die anderen gültigen Werte sind `"pending"` und `"out"`. Dieser Standardwert wird nicht im Profil des Benutzers beibehalten. Das Benutzerprofil wird nur aktualisiert, wenn `setConsent` aufgerufen wird.
* `"in"`: Wenn diese Einstellung festgelegt ist oder kein Wert angegeben wird, wird die Arbeit ohne Voreinstellungen für die Benutzerzustimmung fortgesetzt.
* `"pending"`: Wenn diese Einstellung festgelegt ist, wird die Arbeit in die Warteschlange gestellt, bis der Benutzer Zustimmungsvoreinstellungen bereitstellt.
* `"out"`: Wenn diese Einstellung festgelegt ist, wird die Arbeit verworfen, bis der Benutzer Zustimmungsvoreinstellungen bereitstellt.
Nachdem die Voreinstellungen des Nutzers bereitgestellt wurden, wird die Arbeit basierend auf den Voreinstellungen des Nutzers entweder fortgesetzt oder abgebrochen. Weitere Informationen finden Sie unter [Unterstützen von Zustimmung](../consent/supporting-consent.md).

## Personalisierungsoptionen {#personalization}

### `prehidingStyle` {#prehidingStyle}

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Nein | Keine |

{style="table-layout:auto"}

Wird verwendet, um eine CSS-Stildefinition zu erstellen, die Inhaltsbereiche Ihrer Web-Seite ausblendet, während personalisierter Inhalt vom Server geladen wird. Wenn diese Option nicht bereitgestellt wird, versucht das SDK nicht, Inhaltsbereiche beim Laden personalisierter Inhalte auszublenden, was möglicherweise zu einem &quot;Flackern&quot;führt.

Wenn beispielsweise ein Element auf Ihrer Web-Seite die ID `container`, deren Standardinhalt Sie ausblenden möchten, während personalisierter Inhalt vom Server geladen wird, verwenden Sie den folgenden Stil für die Vorab-Ausblendung:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

Diese Option sollte bei der Migration einzelner Seiten von [!DNL at.js] zum Web SDK.

Verwenden Sie diese Option, um das Web SDK zum Lesen und Schreiben der Legacy zu aktivieren. `mbox` und `mboxEdgeCluster` von [!DNL at.js]. Auf diese Weise können Sie das Besucherprofil beibehalten, während Sie von einer Seite, die das Web SDK verwendet, zu einer Seite wechseln, die die Variable [!DNL at.js] Bibliothek und umgekehrt.

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `false` |

## Optionen für Zielgruppen

### `cookieDestinationsEnabled`

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style="table-layout:auto"}

Aktiviert [!DNL Audience Manager] Cookie-Ziele, die das Setzen von Cookies basierend auf der Segmentqualifizierung ermöglichen.

### `urlDestinationsEnabled`

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style="table-layout:auto"}

Aktiviert [!DNL Audience Manager] URL-Ziele, die das Auslösen von URLs basierend auf der Segmentqualifizierung ermöglichen.

## Identitätsoptionen

### `idMigrationEnabled` {#id-migration-enabled}

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style="table-layout:auto"}

Wenn &quot;true&quot;, liest und setzt das SDK alte AMCV-Cookies. Diese Option hilft beim Übergang zur Verwendung des Adobe Experience Platform Web SDK, während einige Teile der Site möglicherweise noch Visitor.js verwenden.

Wenn die Besucher-API auf der Seite definiert ist, fragt das SDK die Besucher-API für die ECID ab. Mit dieser Option können Sie Seiten mit dem Adobe Experience Platform Web SDK doppelt taggen, die immer noch dieselbe ECID aufweisen.

### `thirdPartyCookiesEnabled`

| Typ | Erforderlich | Standardwert |
| -------- | ------------ | ----------------- |
| Boolesch | Nein | `true` |

{style="table-layout:auto"}

Aktiviert die Einstellung von Adobe-Drittanbieter-Cookies. Das SDK kann die Besucher-ID in einem Drittanbieterkontext beibehalten, damit dieselbe Besucher-ID siteübergreifend verwendet werden kann. Verwenden Sie diese Option, wenn Sie mehrere Sites haben oder Daten mit Partnern teilen möchten. Manchmal ist diese Option jedoch aus Datenschutzgründen nicht erwünscht.
