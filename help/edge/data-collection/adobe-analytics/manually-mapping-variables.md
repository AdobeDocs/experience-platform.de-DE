---
title: Manuelles Zuordnen von Adobe Analytics-Variablen im Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mithilfe der Verarbeitungsregeln im Experience Platform Web SDK Variablen manuell Adobe Analytics zuordnen.
seo-description: Manuelles Zuordnen von Variablen zu Adobe Analytics mithilfe von Verarbeitungsregeln mit Web SDK
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;contextData;Processing rules;rules;xdm;Schema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 33%

---


# Manuelles Zuordnen von Variablen in Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] kann bestimmte Variablen automatisch zuordnen, benutzerdefinierte Variablen müssen jedoch manuell zugeordnet werden.

Für XDM-Daten, die nicht automatisch [!DNL Analytics] zugeordnet werden, können Sie [Kontextdaten](https://docs.adobe.com/content/help/de-DE/analytics/implementation/vars/page-vars/contextdata.html) verwenden, um mit Ihrem [Schema](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/schema/composition.html) abzugleichen. Anschließend kann sie mithilfe von [Verarbeitungsregeln](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) [!DNL Analytics]-Variablen zugeordnet werden.[!DNL Analytics]

Außerdem können Sie einen Standardsatz von Listen und Aktionen verwenden, um Daten mit dem Adobe Experience Platform Web SDK zu senden oder abzurufen. Weitere Information finden Sie unter [Produkte](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/implement/commerce.html).

## Kontextdaten

Um von [!DNL Analytics] verwendet zu werden, werden XDM-Daten mit Punktnotation reduziert und als `contextData` verfügbar gemacht. Die folgende Liste von Wertpaaren zeigt ein Beispiel für `context data`:

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

Auf alle vom Edge Network erfassten Daten kann über [Verarbeitungsregeln](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) zugegriffen werden. In [!DNL Analytics] können Sie Verarbeitungsregeln verwenden, um Kontextdaten in [!DNL Analytics]-Variablen zu integrieren.

In der folgenden Regel wird Adobe Analytics beispielsweise so eingestellt, dass **Interne Suchbegriffe (eVar2)** mit den Daten gefüllt werden, die **a.x._atag.search.term(Kontextdaten)** zugeordnet sind.

![](assets/examplerule.png)


## XDM-Schema

Adobe Experience Platform verwendet Schema, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende Definition von Daten wird es einfacher, Bedeutung beizubehalten und somit aus Daten Nutzen zu ziehen. [!DNL Analytics] Kontextdaten funktionieren mit der vom Schema definierten Struktur.

Das folgende Beispiel zeigt, wie der Befehl [`event` mit der Option `xdm` verwendet werden kann, um Daten mit dem Adobe Experience Platform Web SDK zu senden und abzurufen. ](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/fundamentals/tracking-events.html) In diesem Beispiel stimmt der `event`-Befehl mit dem [ExperienceEvent Commerce Details Schema](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) überein, sodass die productListItems-Werte `name` und `SKU` verfolgt werden:


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

Weitere Informationen zur Verfolgung von Ereignissen mit Adobe Experience Platform [!DNL Web SDK] finden Sie unter [Tracking-Ereignis](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
