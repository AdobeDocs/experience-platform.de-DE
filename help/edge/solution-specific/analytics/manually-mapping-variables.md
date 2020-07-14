---
title: Manuelles Zuordnen von Variablen in Analytics
seo-title: Manuelles Zuordnen von Variablen in Analytics mit Web SDK
description: Manuelles Zuordnen von Variablen zu Analytics mithilfe von Verarbeitungsregeln
seo-description: Variablen manuell mit Verarbeitungsregeln mit Web SDK Analytics zuordnen
translation-type: tm+mt
source-git-commit: 71193ad346c3976f80b14ee0d6e5b12055a17473
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 15%

---


# Manuelles Zuordnen von Variablen in Analytics

Das Adobe Experience Platform (AEP) Web SDK kann bestimmte Variablen automatisch zuordnen, benutzerdefinierte Variablen müssen jedoch manuell zugeordnet werden.

Bei XDM-Daten, die nicht automatisch Analytics zugeordnet werden, können Sie [Kontextdaten](https://docs.adobe.com/content/help/de-DE/analytics/implementation/vars/page-vars/contextdata.html) verwenden, um Ihrem [Schema](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/schema/composition.html)zu entsprechen. Anschließend kann es mithilfe von [Verarbeitungsregeln](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) zum Füllen von Analytics-Variablen Analytics zugeordnet werden.

Außerdem können Sie einen Standardsatz von Listen und Aktionen verwenden, um Daten mit dem AEP Web SDK zu senden oder abzurufen. Siehe dazu [Produkte](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html).

## Kontextdaten

Zur Verwendung durch Analytics werden XDM-Daten mit Punktnotation reduziert und als `contextData`verfügbar gemacht. Die folgende Liste von Wertpaaren zeigt ein Beispiel `context data`:

```javascript
{
          "bh": "900",
          "bw": "1680",
          "c": "24",
          "c.a.d.key.[0]": "value1",
          "c.a.d.key.[1]": "value2",
          "c.a.d.object.key1": "value1",
          "c.a.d.object.key2.[0]": "value2",
          "c.a.x.environment.browserdetails.javascriptenabled": "true",
          "c.a.x.environment.type": "browser",
          "cust_hit_time_gmt": "1579781427",
          "g": "http://example.com/home",
          "gn": "home",
          "j": "1.8.5",
          "k": "Y",
          "s": "1680x1050",
          "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
          "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
          "v": "Y"
        }
```

## Verarbeitungsregeln

All data collected by the edge network can be accessed via [processing rules](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In Analytics können Sie mithilfe von Verarbeitungsregeln Kontextdaten in Analytics-Variablen einbinden.

In der folgenden Regel wird Analytics beispielsweise so eingestellt, dass **interne Suchbegriffe (eVar2)** mit den Daten gefüllt werden, die mit **a.x_atag.search.term(Kontextdaten)** verknüpft sind.

![](assets/examplerule.png)


## XDM-Schema

Experience Platform verwendet Schema, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende Definition von Daten wird es einfacher, Bedeutung beizubehalten und somit aus Daten Nutzen zu ziehen. Analytics-Kontextdaten funktionieren mit der vom Schema definierten Struktur.

Das folgende Beispiel zeigt, wie der [`event` Befehl](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) mit der `xdm` Option zum Senden und Abrufen von Daten mit dem AEP Web SDK verwendet werden kann. In diesem Beispiel stimmt der `event` Befehl mit dem [ExperienceEvent-Commerce-Details-Schema](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) überein, sodass productListItems `name` und `SKU` Werte verfolgt werden:


```
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

Weitere Informationen zum Verfolgen von Ereignissen mit dem AEP Web SDK finden Sie unter [Ereignis](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html)verfolgen.
