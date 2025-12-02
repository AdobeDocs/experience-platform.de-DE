---
title: Gesellschaft
description: Erhalten Sie Informationen über die IMS-Organisation, der die implementierte Tag-Eigenschaft gehört.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

Das `_satellite.company`-Objekt zeigt Informationen über die IMS-Organisation an, der die Tag-Eigenschaft gehört.

```ts
readonly _satellite.company: Company
```

## Verfügbare Felder

Beim Aufrufen dieses Objekts sind die folgenden Felder verfügbar:

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| Name | Typ | Beschreibung |
| --- | --- | --- |
| **`orgId`** | `string` | Die IMS-Organisations-ID der Tag-Eigenschaft. |
| **`dynamicCdnEnabled`** | `boolean` | Legt fest, ob Ihre Tag-Eigenschaft die dynamische CDN-Switching-Funktion von Adobe verwendet. Wenn er auf `true` festgelegt ist, wechselt das CDN, von dem ein Besucher Ihr Tag anfordert, basierend auf seinem Speicherort automatisch. |
| **`cdnAllowList`** | `string[]` | Die zulässigen CDNs zum Laden Ihrer Tag-Eigenschaft aus . |

Ähnliche Informationen finden Sie auch in `_satellite._container.company`. Weitere Informationen finden Sie unter [`_container`](container.md) .
