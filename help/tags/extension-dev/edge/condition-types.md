---
title: Bedingungstypen für Edge-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ Bedingung für eine Kantenerweiterung in Adobe Experience Platform definieren.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 44%

---

# Bedingungstypen für Edge-Erweiterungen

>[!NOTE]
>
> Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

In einer Tag-Regel wird eine Bedingung ausgewertet, nachdem ein Ereignis aufgetreten ist. Alle Bedingungen müssen „true“ zurückgeben, damit die Regel weiter verarbeitet wird. Bedingungstypen werden von Erweiterungen bereitgestellt und bewerten, ob etwas wahr oder falsch ist, wobei ein boolescher Wert zurückgegeben wird.

Beispielsweise könnte eine Erweiterung einen Bedingungstyp &quot;Viewport enthält&quot;bereitstellen, in dem der Benutzer einen CSS-Selektor angeben könnte. Wenn diese Bedingung auf der Website des Kunden ausgewertet wird, kann die Erweiterung nach Elementen suchen, die mit der CSS-Auswahl übereinstimmen, und die Information zurückgeben, ob sich eines davon im Ansichtsfenster des Benutzers befindet.

In diesem Dokument wird beschrieben, wie Sie Bedingungstypen für eine Kantenerweiterung in Adobe Experience Platform definieren.

>[!IMPORTANT]
>
>Wenn Sie eine Web-Erweiterung entwickeln, lesen Sie das Handbuch zu [Bedingungstypen für Web-Erweiterungen](../web/condition-types.md).
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Edge-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Bedingungstypen bestehen in der Regel aus Folgendem:

1. Eine Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für die Bedingung zu ändern.
2. Ein Bibliotheksmodul wird in der Tag-Laufzeitbibliothek ausgegeben, um die Einstellungen zu interpretieren und eine Bedingung zu bewerten.

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
