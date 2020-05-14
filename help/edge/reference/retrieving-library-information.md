---
title: Abrufen von Bibliotheksinformationen
seo-title: Abrufen von Bibliotheksinformationen mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Informationen über die auf der Website geladene Bibliothek abrufen können
seo-description: Erfahren Sie, wie Sie Informationen zur Bibliothek abrufen, die in die Website geladen wird, die vom Adobe Experience Cloud SDK automatisch erfasst werden
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 100%

---


# Abrufen von Bibliotheksinformationen

Es ist oft hilfreich, auf einige Details hinter der Bibliothek zuzugreifen, die Sie in Ihre Website geladen haben. Führen Sie dazu den `getLibraryInfo`-Befehl wie folgt aus:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Derzeit enthält das bereitgestellte `libraryInfo`-Objekt die folgenden Eigenschaften:

* `version` Dies ist die Version der geladenen Bibliothek. Wenn die Version der Bibliothek, die geladen wird, beispielsweise 1.0.0 wäre, wäre der Wert `1.0.0`.