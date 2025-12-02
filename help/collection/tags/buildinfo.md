---
title: buildInfo
description: Erhalten Sie Informationen über den auf Ihrer Site implementierten Tag-Build.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# `buildInfo`

Das `_satellite.buildInfo`-Objekt enthält Informationen zum Build der implementierten Tag-Eigenschaft. Dieses Objekt ist besonders beim Debuggen häufiger Builds nützlich, um sicherzustellen, dass Sie die neueste Version verwenden.

```ts
readonly _satellite.buildInfo: BuildInfo
```

## Verfügbare Felder

Beim Aufrufen dieses Objekts sind die folgenden Felder verfügbar.

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| Name | Typ | Beschreibung |
| --- | --- | --- |
| **`minified`** | `boolean` | Gibt an, ob die Bibliothek minimiert ist. Produktions-Builds werden normalerweise minimiert (`true`), Entwicklungs- und Staging-Builds dagegen normalerweise nicht (`false`). |
| **`buildDate`** | `string (ISO-8601 datetime)` | Datum und Uhrzeit der Erstellung und Veröffentlichung Ihrer JavaScript-Datei. |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [Turbine](https://github.com/adobe/reactor-turbine) ist die Engine von Adobe, die Tag-Regeln verarbeitet und Logik an Tag-Erweiterungen delegiert. Dieses Feld enthält das Datum und die Uhrzeit des Turbine-Builds, der zum Veröffentlichen der Tag-Eigenschaft verwendet wird. |
| **`turbineVersion`** | `string` | Die Turbine -Version, mit der Ihre Tag-Eigenschaft erstellt und veröffentlicht wird. |

Ähnliche Informationen finden Sie auch in `_satellite._container.buildInfo`. Weitere Informationen finden Sie unter [`_container`](container.md) .
