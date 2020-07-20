---
title: Manuelles Zuordnen von Variablen in Analytics
seo-title: Manuelles Zuordnen von Variablen in Analytics mit Web SDK
description: Manuelles Zuordnen von Variablen zu Analytics mithilfe von Verarbeitungsregeln
seo-description: Variablen manuell mit Verarbeitungsregeln mit Web SDK Analytics zuordnen
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 16%

---


# Manuelles Zuordnen von Variablen in Analytics

Die Adobe Experience Platform (AEP) [!DNL Web SDK] kann bestimmte Variablen automatisch zuordnen, benutzerdefinierte Variablen müssen jedoch manuell zugeordnet werden.

Bei XDM-Daten, denen nicht automatisch zugeordnet wird, können Sie [!DNL Analytics]mithilfe von [Kontextdaten](https://docs.adobe.com/content/help/de-DE/analytics/implementation/vars/page-vars/contextdata.html) eine Übereinstimmung mit Ihrem [Schema](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/schema/composition.html)herstellen. Anschließend kann sie mithilfe von [!DNL Analytics] Verarbeitungsregeln [](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) zugeordnet werden, um [!DNL Analytics] Variablen zu füllen.

Außerdem können Sie einen Standardsatz von Aktionen und Produkteinstellungen verwenden, um Daten mit AEP zu senden oder abzurufen [!DNL Web SDK]. Siehe dazu [Produkte](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html).

## Kontextdaten

Zur Verwendung [!DNL Analytics]werden XDM-Daten mit Punktnotation reduziert und als `contextData`verfügbar gemacht. Die folgende Liste von Wertpaaren zeigt ein Beispiel `context data`:

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

All data collected by the edge network can be accessed via [processing rules](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). Sie können [!DNL Analytics]außerdem Verarbeitungsregeln verwenden, um Kontextdaten in [!DNL Analytics] Variablen zu integrieren.

In der folgenden Regel wird Analytics beispielsweise so eingestellt, dass **interne Suchbegriffe (eVar2)** mit den Daten gefüllt werden, die mit **a.x_atag.search.term(Kontextdaten)** verknüpft sind.

![](assets/examplerule.png)


## XDM-Schema

[!DNL Experience Platform] verwendet Schema, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende Definition von Daten wird es einfacher, Bedeutung beizubehalten und somit aus Daten Nutzen zu ziehen. [!DNL Analytics] Kontextdaten funktionieren mit der vom Schema definierten Struktur.

Das folgende Beispiel zeigt, wie der [`event` Befehl](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) mit der `xdm` Option zum Senden und Abrufen von Daten mit dem AEP verwendet werden kann [!DNL Web SDK]. In diesem Beispiel stimmt der `event` Befehl mit dem [ExperienceEvent-Commerce-Details-Schema](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) überein, sodass productListItems `name` und `SKU` Werte verfolgt werden:


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

Weitere Informationen zur Verfolgung von Ereignissen mit AEP [!DNL Web SDK]finden Sie unter [Tracking-Ereignis](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
