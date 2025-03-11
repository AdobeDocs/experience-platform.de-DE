---
title: getIdentity
description: Abrufen der Identität eines Besuchers ohne Senden von Ereignisdaten.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 5f8a9938eaccfd2eeabc75c56608f11819a81ffa
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---

# `getIdentity`

Wenn Sie den [`sendEvent`](sendevent/overview.md) Befehl ausführen, ruft die Web-SDK automatisch die Besucheridentität ab, sofern noch keine vorhanden ist.

Mit dem Befehl `getIdentity` können Sie eine Besucher-ID abrufen, ohne Ereignisdaten zu senden.

Wenn Sie separate Aufrufe benötigen, um eine Besucher-ID zu generieren und Daten zu senden, können Sie diesen Befehl verwenden.

Der `getIdentity` Befehl durchläuft den folgenden Fluss, um die `ECID` abzurufen.

1. Sie verwenden Web SDK, um entweder `getIdentity` oder [`appendIdentityToUrl`](appendidentitytourl.md) aufzurufen.
1. Web SDK wartet auf die Bereitstellung von Einverständnisinformationen.
1. Web SDK prüft, ob beim Aufruf der `ECID` Namespace angefordert wurde. Standardmäßig ist der `ECID`-Namespace immer enthalten.
1. Web SDK liest das `kndctr`-Cookie und gibt seinen Wert als `ECID` zurück, falls vorhanden. Dadurch wird nur der `ECID` Wert zurückgegeben, nicht aber die `regionId`.
1. Wenn das `kndctr` Identitäts-Cookie nicht gesetzt ist oder der `"CORE"`-Namespace angefordert wurde, sendet Web SDK eine Anfrage an die Edge Network.
1. Die Edge Network gibt sowohl die `ECID` als auch die `regionId` (und die `CORE ID`, falls angefordert) zurück.

## Abrufen von Identitäten mithilfe der Tag-Erweiterung „Web SDK&quot;

Die Web-Tag-Erweiterung von SDK bietet diesen Befehl nicht über die Benutzeroberfläche der Tag-Erweiterung an. Verwenden Sie den Editor für benutzerspezifischen Code unter Verwendung der JavaScript-Bibliothekssyntax.

## Abrufen von Identitäten mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den `getIdentity` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Die folgenden Optionen sind bei der Konfiguration dieses Befehls verfügbar:

* **`namespaces`**: Ein Array von Namespaces. Der Standardwert lautet `["ECID"]`. Weitere unterstützte Werte sind:
   * `["CORE"]`
   * `["ECID","CORE"]`
   * `null`
   * `undefined`

  Sie können [!DNL ECID] und [!DNL CORE ID] gleichzeitig anfordern. Beispiel: `"namespaces": ["ECID","CORE"]`.

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
* **`edge.regionID`**: Eine Ganzzahl, die die Edge Network-Region darstellt, die der Browser beim Erfassen einer Identität aufgerufen hat. Es ist identisch mit dem Legacy-Standorthinweis für Audience Manager.
