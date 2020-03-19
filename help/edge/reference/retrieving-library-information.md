---
title: Abrufen von Bibliotheksinformationen
seo-title: Abrufen von Bibliotheksinformationen mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Informationen über die auf der Website geladene Bibliothek abrufen können
seo-description: Erfahren Sie, wie Sie Informationen zur Bibliothek abrufen, die vom Adobe Experience Cloud SDK automatisch auf die Website geladen wird
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Abrufen von Bibliotheksinformationen

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Es ist oft hilfreich, auf einige Details hinter der Bibliothek zuzugreifen, die Sie auf Ihrer Website geladen haben. Führen Sie dazu den `getLibraryInfo` Befehl wie folgt aus:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Derzeit enthält das bereitgestellte `libraryInfo` Objekt die folgenden Eigenschaften:

* `version` Dies ist die Version der geladenen Bibliothek. Wenn die Version der Bibliothek, die geladen wird, beispielsweise 1.0.0 wäre, wäre der Wert `1.0.0`der Wert.