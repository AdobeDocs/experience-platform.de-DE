---
title: getIdentity
description: Abrufen der Identität eines Besuchers ohne Senden von Ereignisdaten.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# `getIdentity`

Mit dem Befehl `getIdentity` können Sie eine Besucher-ID abrufen, ohne Ereignisdaten zu senden. Wenn Sie den `sendEvent` Befehl ausführen, ruft die Web-SDK automatisch die Besucheridentität ab, sofern noch keine vorhanden ist.

Wenn Sie separate Aufrufe benötigen, um eine Besucher-ID zu generieren und Daten zu senden, können Sie diesen Befehl verwenden.

## Abrufen von Identitäten mithilfe der Tag-Erweiterung „Web SDK&quot;

Die Web-Tag-Erweiterung von SDK bietet diesen Befehl nicht über die Benutzeroberfläche der Tag-Erweiterung an. Verwenden Sie den Editor für benutzerspezifischen Code unter Verwendung der JavaScript-Bibliothekssyntax.

## Abrufen von Identitäten mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den `getIdentity` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Die folgenden Optionen sind bei der Konfiguration dieses Befehls verfügbar:

* **`namespaces`**: Ein Array von Namespaces. Der Standardwert lautet `["ECID"]`. Andere unterstützte Werte sind: `["CORE"]`, `null`, `undefined`. Sie können [!DNL ECID] und [!DNL CORE ID] gleichzeitig anfordern. Beispiel: `"namespaces": ["ECID","CORE"]`.
* **`edgeConfigOverrides`**: Ein [Datenstromkonfigurations-Überschreibungsobjekt](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID","CORE"] //this command retrieves both ECID and CORE IDs.
});
```

## Antwortobjekt

Wenn Sie sich für [Handhabung von Antworten](command-responses.md) mit diesem Befehl entscheiden, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`identity.ECID`**: Eine Zeichenfolge, die die ECID des Besuchers enthält.
* **`identity.CORE`**: Eine Zeichenfolge, die die CORE-ID des Besuchers enthält.
* **`edge.regionID`**: Eine Ganzzahl, die die Region des Edge Networks darstellt, auf das der Browser beim Erfassen einer Identität gestoßen ist. Es ist dasselbe wie der Speicherorthinweis für den alten Audience Manager.
