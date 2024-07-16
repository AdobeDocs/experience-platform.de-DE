---
title: getLibraryInfo
description: Rufen Sie Informationen zur aktuellen Web SDK-Bibliotheksversion ab.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

Der Befehl `getLibraryInfo` enthält Informationen zur aktuell verwendeten Version der Web SDK-Bibliothek. Mit diesem Befehl können Sie verfolgen, welche Versionen des Web SDK Sie für verschiedene Webeigenschaften bereitstellen.

## Bibliotheksinformationen mit der Web SDK-Tag-Erweiterung

Die Tag-Erweiterung bietet keine Schnittstelle zum Senden dieses Befehls. Verwenden Sie den Editor für benutzerdefinierten Code entsprechend der JavaScript-Bibliothekssyntax.

Wenn Sie diesen Befehl mit der Tag-Erweiterung ausführen, sind sowohl die Tag-Erweiterungsversion als auch die Bibliotheksversion mit einem `+` -Symbol verkettet. Die Web SDK-Bibliotheksversion wird zuerst aufgelistet, gefolgt von der Tag-Erweiterungsversion.

## Bibliotheksinformationen mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den Befehl `getLibraryInfo` aus, wenn Sie Ihre konfigurierte Instanz des Web SDK aufrufen. Dieser Befehl wird normalerweise mit einem JavaScript-Versprechen gepaart, mit dem Sie die Objekte abrufen können, die er füllt.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Antwortobjekt

Wenn Sie mit diesem Befehl die [Handhabung von Antworten](command-responses.md) festlegen, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`libraryInfo.commands`**: Ein Array von Befehlen, die diese Version des Web SDK unterstützt.
* **`libraryInfo.configs`**: Ein Array von Konfigurationseinstellungen, die von dieser Version des Web SDK unterstützt werden.
* **`libraryInfo.version`**: Die Version der Web SDK-Bibliothek.
