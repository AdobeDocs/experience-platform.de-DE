---
title: edgeBasePath
description: Der Basispfad des Endpunkts, der für die Interaktion mit Adobe-Services verwendet wird.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

Die `edgeBasePath`-Eigenschaft ändert den Zielpfad, wenn Sie mit Adobe-Services interagieren. Adobe fordert Sie möglicherweise auf, diese Variable zu ändern, wenn Sie an Alpha- oder Beta-Programmen für die Datenerfassung teilnehmen. Die meisten Organisationen müssen diese Eigenschaft nicht festlegen oder ändern.

Legen Sie beim Ausführen des `edgeBasePath`-Befehls das `configure` Textfeld fest. Wenn Sie diese Eigenschaft auslassen, wird standardmäßig der Wert `ee` verwendet. Adobe empfiehlt, diese Eigenschaft in den meisten Konfigurationen wegzulassen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## Edge-Basispfad mit der Tag-Erweiterung „Web SDK&quot;

Die Web SDK-Tag-Erweiterung, die diesem Feld entspricht, befindet sich bei [ Konfiguration der Tag](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md)Erweiterung unter Erweiterte Konfigurationseinstellungen .
