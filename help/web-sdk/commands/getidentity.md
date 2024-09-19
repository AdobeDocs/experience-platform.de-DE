---
title: getIdentity
description: Erhalten Sie die Identität eines Besuchers, ohne Ereignisdaten zu senden.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# `getIdentity`

Mit dem Befehl `getIdentity` können Sie eine Besucher-ID abrufen, ohne Ereignisdaten zu senden. Wenn Sie den Befehl `sendEvent` ausführen, ruft das Web SDK automatisch die Identität des Besuchers ab, falls noch keine vorhanden ist.

Wenn Sie separate Aufrufe benötigen, um eine Besucher-ID zu generieren und Daten zu senden, können Sie diesen Befehl verwenden.

## Abrufen von Identitäten mithilfe der Web SDK-Tag-Erweiterung

Die Web SDK-Tag-Erweiterung bietet diesen Befehl nicht über die Benutzeroberfläche der Tag-Erweiterung an. Verwenden Sie den benutzerdefinierten Code-Editor mit der JavaScript-Bibliothekssyntax.

## Abrufen von Identitäten mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den Befehl `getIdentity` aus, wenn Sie Ihre konfigurierte Instanz des Web SDK aufrufen. Die folgenden Optionen sind beim Konfigurieren dieses Befehls verfügbar:

* **`namespaces`**: Ein Array von Namespaces. Der Standardwert lautet `["ECID"]`. Weitere unterstützte Werte sind: `["CORE"]`, `null`, `undefined`. Sie können [!DNL ECID] und [!DNL CORE ID] gleichzeitig anfordern. Beispiel: `"namespaces": ["ECID","CORE"]`.
* **`edgeConfigOverrides`**: Eine [Datastream-Konfiguration überschreibt das Objekt](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID","CORE"] //this command retrieves both ECID and CORE IDs.
});
```

## Antwortobjekt

Wenn Sie mit diesem Befehl die [Handhabung von Antworten](command-responses.md) festlegen, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`identity.ECID`**: Eine Zeichenfolge, die die ECID des Besuchers enthält.
* **`identity.CORE`**: Eine Zeichenfolge, die die CORE-ID des Besuchers enthält.
* **`edge.regionID`**: Eine Ganzzahl, die den Besucherbereich darstellt, auf den der Browser beim Erwerb einer Edge Network trifft. Dies entspricht dem alten Audience Manager-Standorthinweis.
