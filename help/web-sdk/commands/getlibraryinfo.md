---
title: getLibraryInfo
description: Rufen Sie Informationen zur aktuellen Web SDK-Bibliotheksversion ab.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

Die `getLibraryInfo` liefert Informationen zur aktuell verwendeten Version der Web SDK-Bibliothek. Mit diesem Befehl können Sie verfolgen, welche Versionen des Web SDK Sie für verschiedene Webeigenschaften bereitstellen.

## Bibliotheksinformationen mit der Web SDK-Tag-Erweiterung

Die Tag-Erweiterung bietet keine Schnittstelle zum Senden dieses Befehls. Verwenden Sie den Editor für benutzerdefinierten Code entsprechend der JavaScript-Bibliothekssyntax.

Wenn Sie diesen Befehl mit der Tag-Erweiterung ausführen, sind sowohl die Tag-Erweiterungsversion als auch die Bibliotheksversion enthalten, verkettet mit einer `+` Symbol. Die Web SDK-Bibliotheksversion wird zuerst aufgelistet, gefolgt von der Tag-Erweiterungsversion.

## Bibliotheksinformationen mit der JavaScript-Bibliothek des Web SDK

Führen Sie die `getLibraryInfo` beim Aufruf Ihrer konfigurierten Instanz des Web SDK. Dieser Befehl wird in der Regel mit einem JavaScript-Versprechen gepaart, mit dem Sie die Objekte abrufen können, die er füllt.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Antwortobjekt

Wenn Sie sich für [Antworten verarbeiten](command-responses.md) Mit diesem Befehl sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`libraryInfo.commands`**: Ein Array von Befehlen, die diese Version des Web SDK unterstützt.
* **`libraryInfo.configs`**: Ein Array von Konfigurationseinstellungen, die von dieser Version des Web SDK unterstützt werden.
* **`libraryInfo.version`**: Die Version der Web SDK-Bibliothek.
