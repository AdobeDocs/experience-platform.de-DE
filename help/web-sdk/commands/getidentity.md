---
title: getIdentity
description: Erhalten Sie die Identität eines Besuchers, ohne Ereignisdaten zu senden.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

Die `getIdentity` -Befehl können Sie eine Besucher-ID abrufen, ohne Ereignisdaten zu senden. Wenn Sie die `sendEvent` angegeben ist, ruft das Web SDK automatisch die Identität des Besuchers ab, falls noch keine vorhanden ist.

Wenn Sie separate Aufrufe benötigen, um eine Besucher-ID zu generieren und Daten zu senden, können Sie diesen Befehl verwenden.

## Abrufen von Identitäten mithilfe der Web SDK-Tag-Erweiterung

Die Web SDK-Tag-Erweiterung bietet diesen Befehl nicht über die Benutzeroberfläche der Tag-Erweiterung an. Verwenden Sie den benutzerdefinierten Code-Editor mit der JavaScript-Bibliothekssyntax.

## Abrufen von Identitäten mithilfe der Web SDK-JavaScript-Bibliothek

Führen Sie die `getIdentity` beim Aufruf Ihrer konfigurierten Instanz des Web SDK. Die folgenden Optionen sind beim Konfigurieren dieses Befehls verfügbar:

* **`namespaces`**: Ein Array von Namespaces. Der Standardwert lautet `["ECID"]`. Gültige Werte sind `["ECID"]`, `null`oder `undefined`.
* **`edgeConfigOverrides`**: ein [Überschreiben des Datenspeicherkonfigurationsobjekts](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Antwortobjekt

Wenn Sie sich für [Antworten verarbeiten](command-responses.md) Mit diesem Befehl sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`identity.ECID`**: Eine Zeichenfolge, die die ECID des Besuchers enthält.
* **`edge.regionID`**: Eine Ganzzahl, die den Edge Network-Bereich darstellt, den der Browser beim Erwerb einer Identität aufruft. Dies entspricht dem alten Audience Manager-Standorthinweis.
