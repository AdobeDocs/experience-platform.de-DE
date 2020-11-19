---
title: Manuelles Zuordnen von Variablen in Adobe Analytics
seo-title: Manuelles Zuordnen von Variablen in Adobe Analytics mit Web SDK
description: Manuelles Zuordnen von Variablen zu Adobe Analytics mithilfe von Verarbeitungsregeln
seo-description: Variablen manuell mit Verarbeitungsregeln mit Web SDK Adobe Analytics zuordnen
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 35%

---


# Manuelles Zuordnen von Variablen in Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] kann bestimmte Variablen automatisch zuordnen, benutzerdefinierte Variablen müssen jedoch manuell zugeordnet werden.

For XDM data that is not automatically mapped to [!DNL Analytics], you can use [context data](https://docs.adobe.com/content/help/de-DE/analytics/implementation/vars/page-vars/contextdata.html) to match your [schema](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/schema/composition.html). Anschließend kann sie mithilfe von [!DNL Analytics] Verarbeitungsregeln [](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) zugeordnet werden, um [!DNL Analytics] Variablen zu füllen.

Außerdem können Sie einen Standardsatz von Listen und Aktionen verwenden, um Daten mit dem Adobe Experience Platform Web SDK zu senden oder abzurufen. Weitere Information finden Sie unter [Produkte](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/implement/commerce.html).

## Kontextdaten

To be used by [!DNL Analytics], XDM data is flattened using dot notation and made available as `contextData`. Die folgende Liste von Wertpaaren zeigt ein Beispiel für `context data`:

```json
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

For example, in the following rule, Adobe Analytics is set to populate **Internal Search terms (eVar2)** with the data associated with **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## XDM-Schema

Adobe Experience Platform verwendet Schema, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende Definition von Daten wird es einfacher, Bedeutung beizubehalten und somit aus Daten Nutzen zu ziehen. [!DNL Analytics] Kontextdaten funktionieren mit der vom Schema definierten Struktur.

The following example shows how the [`event` command](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/fundamentals/tracking-events.html) can be used with the `xdm` option to send and retrieve data with Adobe Experience Platform Web SDK. In diesem Beispiel stimmt der `event`-Befehl mit dem [ExperienceEvent Commerce Details Schema](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) überein, sodass die productListItems-Werte `name` und `SKU` verfolgt werden:


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

Weitere Informationen zum Verfolgen von Ereignissen mit Adobe Experience Platform [!DNL Web SDK]finden Sie unter [Verfolgen von Ereignissen](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/fundamentals/tracking-events.html).
