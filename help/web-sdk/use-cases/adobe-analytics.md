---
title: Senden von Daten an Adobe Analytics mithilfe des Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Daten an Adobe Analytics senden.
keywords: Adobe Analytics;Analytics;zugeordnete Daten;zugeordnete Vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# Senden von Daten an Adobe Analytics mithilfe des Web SDK

Das Adobe Experience Platform Web SDK kann Daten über das Adobe Experience Platform Edge Network an Adobe Analytics senden. Wenn Daten im Edge Network eingehen, wird das XDM-Objekt in ein Format übersetzt, das Adobe Analytics versteht.

## XDM-Feldergruppe

Um die Erfassung der gängigsten Adobe Analytics-Metriken zu vereinfachen, stellt Adobe eine Feldergruppe bereit, die auf Adobe Analytics ausgerichtet ist und die Sie verwenden können. Weitere Informationen zu diesem Schema finden Sie unter [Feldergruppe Adobe Analytics ExperienceEvent Full Extension](/help/xdm/field-groups/event/analytics-full-extension.md).

## Variablenzuordnung

Das Edge-Netzwerk ordnet automatisch viele XDM-Variablen zu. Siehe [Analytics-Variablenzuordnung im Edge-Netzwerk](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=de) im Adobe Analytics-Implementierungshandbuch für eine umfassende Variablenliste mit automatisch zugeordneten Variablen.

Alle Variablen, die nicht automatisch zugeordnet werden, sind als [Kontextdatenvariablen](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=de). Sie können dann [Verarbeitungsregeln](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) um Kontextdatenvariablen Analytics-Variablen zuzuordnen. Wenn Sie beispielsweise über ein benutzerdefiniertes XDM-Schema verfügten, das wie folgt aussah:

```js
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Dies wären dann die Kontextdatenschlüssel, die Ihnen in der Oberfläche für Verarbeitungsregeln zur Verfügung stehen:

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

>[!NOTE]
>
>Mit der Edge Network-Sammlung werden alle Ereignisse an Analytics und alle anderen Dienste gesendet, die Sie für Ihren Datastream konfiguriert haben. Wenn Sie beispielsweise sowohl Analytics als auch Target als Dienste konfiguriert haben und separate Aufrufe für die Personalisierung und für Analytics tätigen, werden beide Ereignisse an Analytics und Target gesendet. Diese Ereignisse werden in Analytics-Berichten aufgezeichnet und können sich auf Metriken wie die Absprungrate auswirken.

## Seitenansichten und Linktracking-Aufrufe

AppMeasurement in Adobe Analytics verwendet separate Methodenaufrufe für Seitenansichten ([`t()` method](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html)) und Linktracking-Aufrufen ([`tl()` method](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html)). Stattdessen stellt das Web SDK nur die [`sendEvent`](../commands/sendevent/overview.md) -Befehl zum Senden von Seitenansichten und Linktracking. Die in ein Ereignis einbezogenen Daten bestimmen, ob es sich um eine [Seitenansicht](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html?lang=de) oder [Seitenereignis](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) in Adobe Analytics.

Standardmäßig werden alle Ereignisse in Adobe Analytics als Seitenansichten betrachtet. Wenn Sie ein Web SDK-Ereignis auf einen Adobe Analytics-Linktracking-Aufruf setzen möchten, legen Sie die folgenden XDM-Felder fest:

* **`web.webInteraction.URL`**: Die Link-URL.
* **`web.webInteraction.name`**: Der Dimensionsname Benutzerspezifischer Link, Downloadlink oder Exitlink, je nach Wert in `web.webInteraction.type`
* **`web.webInteraction.type`**: Bestimmt den Typ des angeklickten Links. Gültige Werte sind `other` (benutzerspezifische Links), `download` (Downloadlinks) und `exit` (Exitlinks).

Wenn Sie [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) im `configure` angegeben haben, werden diese XDM-Felder für Sie ausgefüllt.
