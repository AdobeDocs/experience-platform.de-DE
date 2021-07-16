---
title: Bedingungstypen für Edge-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ Bedingung für eine Kantenerweiterung in Adobe Experience Platform definieren.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 58%

---

# Bedingungstypen für Edge-Erweiterungen

>[!NOTE]
>
> Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Ein Bibliotheksmodul vom Typ Bedingung wertet aus, ob etwas wahr oder falsch ist, und gibt einen booleschen Wert zurück.

>[!IMPORTANT]
>
>In diesem Dokument werden Bedingungstypen für Randerweiterungen behandelt. Wenn Sie eine Web-Erweiterung entwickeln, lesen Sie das Handbuch zu [Bedingungstypen für Web-Erweiterungen](../web/condition-types.md).
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Tag-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Wenn Sie beispielsweise prüfen möchten, ob sich der Benutzer auf dem Host `example.com` befindet, könnte Ihr Modul wie folgt aussehen.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Wenn Sie möchten, dass der Hostname vom Benutzer konfiguriert werden kann, um die Eingabe eines Hostnamens zuzulassen und ihn im settings-Objekt zu speichern, könnte das Objekt in etwa wie im folgenden Beispiel aussehen.

```js
{
  "hostname": "example.com"
}
```

Um mit dem benutzerdefinierten Hostnamen arbeiten zu können, muss das Modul wie folgt geändert werden:

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## Bedingungsergebnis

Das von einem Bedingungsmodul zurückgegebene Ergebnis kann eines der folgenden sein:

1. Ein boolescher Wert (`true` oder `false`).
1. Ein [Promise](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise), das nach Auflösung einen booleschen Wert zurückgibt.

## Kontext des Bibliotheksmoduls

Alle Bedingungsmodule haben Zugriff auf eine `context`-Variable, die beim Aufruf des Moduls bereitgestellt wird. Weitere Informationen finden Sie [hier](./context.md).
