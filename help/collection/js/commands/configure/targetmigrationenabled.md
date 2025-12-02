---
title: targetMigrationEnabled
description: Der Web-SDK darf Adobe Target-Cookies lesen und schreiben.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: dade74bf4a5cfd7b60eaf216583deb67b93a61db
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# `targetMigrationEnabled`

Die `targetMigrationEnabled`-Eigenschaft ist ein boolescher Wert, der es dem Web-SDK ermöglicht, die [`mbox` und `mboxEdgeCluster` Cookies zu lesen und zu schreiben](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) die von den Adobe Target 1.x- und 2.x-Bibliotheken verwendet werden. Mit dieser Option können Sie das Besucherprofil zwischen Seiten beibehalten, die frühere Adobe Target-Implementierungen verwendet haben, und Seiten, die Web SDK verwenden.

Legen Sie beim Ausführen des `targetMigrationEnabled`-Befehls den booleschen Wert `configure` fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `false` gesetzt. Legen Sie diesen Wert auf `true` fest, wenn einige Seiten weiterhin die Adobe Target 1.x- oder 2.x-Bibliotheken verwenden.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## Aktivieren der Target-Migration mithilfe der Tag-Erweiterung „Web SDK&quot;

Diese Einstellung kann in der Tag-Erweiterung „Web SDK&quot; mithilfe der Konfigurationseinstellungen von [Personalization konfiguriert ](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk).
