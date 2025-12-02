---
title: Umgebung
description: Die Build-Umgebung, die die Tag-Eigenschaft derzeit verwendet.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 6%

---

# `environment`

Das `_satellite.environment`-Objekt gibt an, welche Build-Umgebung die Tag-Eigenschaft derzeit verwendet.

```js
readonly _satellite.environment: Environment
```

## Verfügbare Felder

Beim Aufrufen dieses Objekts sind die folgenden Felder verfügbar.

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| Name | Typ | Beschreibung |
|---|---|---|
| **`id`** | `string` | Die eindeutige Kennung für die Umgebung. Sie können die Umgebungs-ID finden, indem Sie in der Tag-Benutzeroberfläche unter **[!UICONTROL Install]** auf das Symbol [[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md) klicken. |
| **`stage`** | `development \| staging \| production` | Der Umgebungstyp. |
