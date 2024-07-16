---
title: getIdentity
description: Erhalten Sie die Identität eines Besuchers, ohne Ereignisdaten zu senden.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

Mit dem Befehl `getIdentity` können Sie eine Besucher-ID abrufen, ohne Ereignisdaten zu senden. Wenn Sie den Befehl `sendEvent` ausführen, ruft das Web SDK automatisch die Identität des Besuchers ab, falls noch keine vorhanden ist.

Wenn Sie separate Aufrufe benötigen, um eine Besucher-ID zu generieren und Daten zu senden, können Sie diesen Befehl verwenden.

## Abrufen von Identitäten mithilfe der Web SDK-Tag-Erweiterung

Die Web SDK-Tag-Erweiterung bietet diesen Befehl nicht über die Benutzeroberfläche der Tag-Erweiterung an. Verwenden Sie den benutzerdefinierten Code-Editor mit der JavaScript-Bibliothekssyntax.

## Abrufen von Identitäten mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den Befehl `getIdentity` aus, wenn Sie Ihre konfigurierte Instanz des Web SDK aufrufen. Die folgenden Optionen sind beim Konfigurieren dieses Befehls verfügbar:

* **`namespaces`**: Ein Array von Namespaces. Der Standardwert lautet `["ECID"]`. Gültige Werte sind `["ECID"]`, `null` oder `undefined`.
* **`edgeConfigOverrides`**: Eine [Datastream-Konfiguration überschreibt das Objekt](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Antwortobjekt

Wenn Sie mit diesem Befehl die [Handhabung von Antworten](command-responses.md) festlegen, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`identity.ECID`**: Eine Zeichenfolge, die die ECID des Besuchers enthält.
* **`edge.regionID`**: Eine Ganzzahl, die den Besucherbereich darstellt, auf den der Browser beim Erwerb einer Edge Network trifft. Dies entspricht dem alten Audience Manager-Standorthinweis.
