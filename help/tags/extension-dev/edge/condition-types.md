---
title: Bedingungstypen für Edge-Erweiterungen
description: Erfahren Sie, wie Sie in Adobe Experience Platform ein Bibliotheksmodul des Typs „condition-type“ für eine Edge-Erweiterung definieren.
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 83%

---

# Bedingungstypen für Edge-Erweiterungen

>[!NOTE]
>
> Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

In einer Tag-Regel wird eine Bedingung ausgewertet, nachdem ein Ereignis aufgetreten ist. Alle Bedingungen müssen „true“ zurückgeben, damit die Regel weiter verarbeitet wird. Bedingungstypen werden von Erweiterungen bereitgestellt und bewerten, ob etwas wahr oder falsch ist, wobei ein boolescher Wert zurückgegeben wird.

Beispielsweise könnte eine Erweiterung einen Bedinungstyp „Viewport enthält“ bereitstellen, bei dem der Benutzer einen CSS-Selektor angeben kann. Wenn diese Bedingung auf der Website des Kunden ausgewertet wird, kann die Erweiterung nach Elementen suchen, die mit der CSS-Auswahl übereinstimmen, und die Information zurückgeben, ob sich eines davon im Ansichtsfenster des Benutzers befindet.

In diesem Dokument wird beschrieben, wie Sie Bedingungstypen für eine Kantenerweiterung in Adobe Experience Platform definieren.

>[!IMPORTANT]
>
>Wenn Sie eine Web-Erweiterung entwickeln, lesen Sie das Handbuch zu [Bedingungstypen für Web-Erweiterungen](../web/condition-types.md).
>
>In diesem Dokument wird auch davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Edge-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Bedingungstypen bestehen in der Regel aus Folgendem:

1. Eine Ansicht, die in der Experience Platform-Benutzeroberfläche und der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Bedingungseinstellungen zu ändern.
2. Ein Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und eine Bedingung auszuwerten.

Wenn Sie z. B. prüfen möchten, ob sich der Benutzer auf dem Host `example.com` befindet, könnte Ihr Modul wie folgt aussehen.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Wenn Sie möchten, dass der Host-Name vom Benutzer konfiguriert werden kann, um die Eingabe eines Host-Namens zuzulassen und ihn im settings-Objekt zu speichern, könnte das Objekt in etwa wie im folgenden Beispiel aussehen.

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
