---
title: Manuelles Zuordnen von Adobe Analytics-Variablen im Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Variablen mithilfe von Verarbeitungsregeln im Experience Platform Web SDK manuell Adobe Analytics zuordnen.
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 9392a90b70699b79949095e178ea77dd34d313a3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 25%

---

# Manuelles Zuordnen von Variablen in Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] kann bestimmte Variablen automatisch zuordnen, benutzerdefinierte Variablen müssen jedoch manuell zugeordnet werden.

Für XDM-Daten, die nicht automatisch [!DNL Analytics] zugeordnet werden, können Sie [Kontextdaten](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=de) verwenden, um Ihr [Schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=de) zu entsprechen. Anschließend kann sie [!DNL Analytics] mithilfe von [Verarbeitungsregeln](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=de) zugeordnet werden, um [!DNL Analytics] -Variablen zu füllen.

Außerdem können Sie einen Standardsatz von Aktionen und Produktlisten verwenden, um Daten mit dem Adobe Experience Platform Web SDK zu senden oder abzurufen. Weitere Informationen finden Sie unter [Commerce- und Produktinformationen abrufen](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## Kontextdaten

Zur Verwendung durch [!DNL Analytics] werden XDM-Daten mit Punktnotation reduziert und als `contextData` verfügbar gemacht. Die folgende Liste von Wertpaaren zeigt ein Beispiel dafür, wie `context data` aussieht, wenn es reduziert wird:

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

Auf alle vom Edge Network erfassten Daten kann über [Verarbeitungsregeln](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) zugegriffen werden. In [!DNL Analytics] können Sie Verarbeitungsregeln verwenden, um Kontextdaten in [!DNL Analytics] -Variablen zu integrieren.

In der folgenden Regel wird Adobe Analytics beispielsweise so eingestellt, dass **Interne Suchbegriffe (eVar2)** mit den Daten gefüllt werden, die **a.x._atag.search.term(Kontextdaten)** zugeordnet sind.

![](assets/examplerule.png)


## XDM-Schema

Adobe Experience Platform verwendet Schemas, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, die Bedeutung beizubehalten und somit aus Daten Nutzen zu ziehen. [!DNL Analytics] -Kontextdaten funktionieren mit der vom Schema definierten Struktur.

Im folgenden Beispiel wird gezeigt, wie der Befehl [`event`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=de) mit der Option `xdm` verwendet werden kann, um Daten mit dem Adobe Experience Platform Web SDK zu senden und abzurufen. In diesem Beispiel stimmt der `event`-Befehl mit dem [ExperienceEvent Commerce Details Schema](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) überein, sodass die productListItems-Werte `name` und `SKU` verfolgt werden:


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

Weitere Informationen zum Verfolgen von Ereignissen mit Adobe Experience Platform [!DNL Web SDK] finden Sie unter [Verfolgen von Ereignissen](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html).
