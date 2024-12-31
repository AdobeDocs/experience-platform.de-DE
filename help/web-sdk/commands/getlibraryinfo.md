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

Der Befehl `getLibraryInfo` liefert Informationen zur aktuell verwendeten Version der Web SDK-Bibliothek. Sie können diesen Befehl verwenden, um zu verfolgen, welche Versionen der Web-SDK Sie für verschiedene Web-Eigenschaften bereitstellen.

## Bibliotheksinformationen mithilfe der Tag-Erweiterung „Web SDK&quot;

Die Tag-Erweiterung stellt keine Schnittstelle zum Senden dieses Befehls bereit. Verwenden Sie den Editor für benutzerspezifischen Code entsprechend der JavaScript-Bibliothekssyntax.

Wenn Sie diesen Befehl mit der Tag-Erweiterung ausführen, sind sowohl die Tag-Erweiterungsversion als auch die Bibliotheksversion enthalten, verkettet mit einem `+`. Die Web SDK-Bibliotheksversion wird zuerst aufgeführt, gefolgt von der Tag-Erweiterungsversion.

## Bibliotheksinformationen mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den `getLibraryInfo` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Dieser Befehl ist in der Regel mit einem JavaScript-Versprechen gepaart, mit dem Sie die -Objekte abrufen können, die er ausfüllt.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Antwortobjekt

Wenn Sie sich für [Handhabung von Antworten](command-responses.md) mit diesem Befehl entscheiden, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`libraryInfo.commands`**: Ein Array von Befehlen, die von dieser Version des Web-SDK unterstützt werden.
* **`libraryInfo.configs`**: Ein Array von Konfigurationseinstellungen, die diese Version von Web SDK unterstützt.
* **`libraryInfo.version`**: Die Version der Web SDK-Bibliothek.
