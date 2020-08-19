---
title: Manuelles Zuordnen von Variablen in Analytics
seo-title: Manuelles Zuordnen von Variablen in Analytics zu Web SDK
description: Manuelles Zuordnen von Variablen zu Analytics mithilfe von Verarbeitungsregeln
seo-description: Variablen manuell Analytics zuordnen mithilfe von Verarbeitungsregeln mit Web SDK
translation-type: tm+mt
source-git-commit: 075d71353877045e12985b3914aaeeb478ed46d6
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 47%

---


# Manuelles Zuordnen von Variablen in Analytics

Das Adobe Experience Platform (AEP) [!DNL Web SDK] kann bestimmte Variablen automatisch zuordnen, benutzerdefinierte Variablen müssen jedoch manuell zugeordnet werden.

For XDM data that is not automatically mapped to [!DNL Analytics], you can use [context data](https://docs.adobe.com/content/help/de-DE/analytics/implementation/vars/page-vars/contextdata.html) to match your [schema](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/schema/composition.html). Anschließend kann sie mithilfe von [!DNL Analytics] Verarbeitungsregeln [](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) zugeordnet werden, um [!DNL Analytics] Variablen zu füllen.

Also, you can use a default set of actions and product lists to send or retrieve data with the AEP [!DNL Web SDK]. Weitere Information finden Sie unter [Produkte](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/implement/commerce.html).

## Kontextdaten

To be used by [!DNL Analytics], XDM data is flattened using dot notation and made available as `contextData`. Die folgende Liste von Wertpaaren zeigt ein Beispiel für `context data`:

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

Auf alle vom Edge Network erfassten Daten kann über [Verarbeitungsregeln](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) zugegriffen werden. In [!DNL Analytics], you can use processing rules to incorporate context data into [!DNL Analytics] variables.

In der folgenden Regel wird Analytics beispielsweise so eingestellt, dass **interne Suchbegriffe (eVar2)** mit den Daten gefüllt werden, die mit **a.x_atag.search.term(Kontextdaten)** verknüpft sind.

![](assets/examplerule.png)


## XDM-Schema

[!DNL Experience Platform]Schemas dienen in zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende Definition von Daten wird es einfacher, Bedeutung beizubehalten und somit aus Daten Nutzen zu ziehen. [!DNL Analytics] Kontextdaten funktionieren mit der vom Schema definierten Struktur.

The following example shows how the [`event` command](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/fundamentals/tracking-events.html) can be used with the `xdm` option to send and retrieve data with the AEP [!DNL Web SDK]. In diesem Beispiel stimmt der `event`-Befehl mit dem [ExperienceEvent Commerce Details Schema](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) überein, sodass die productListItems-Werte `name` und `SKU` verfolgt werden:


```javascript
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

For more information on tracking events with the AEP [!DNL Web SDK], see [Tracking events](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/fundamentals/tracking-events.html).
