---
title: Senden von Daten an Adobe Analytics
seo-title: Senden von Daten an Adobe Analytics mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Daten mit dem Experience Platform Web SDK an Adobe Analytics gesendet werden
seo-description: Erfahren Sie, wie Daten mit dem Experience Platform Web SDK an Adobe Analytics gesendet werden
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Senden von Daten an Adobe Analytics

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Das Adobe Experience Platform Web SDK kann Daten an Adobe Analytics senden. Dies funktioniert durch die Übersetzung `xdm` in ein Format, das Adobe Analytics verwenden kann.

## Einrichten

Adobe Analytics nimmt die gesendeten Daten automatisch auf, wenn eine Report Suite in der Benutzeroberfläche für die Kundenkonfiguration zugeordnet ist. Hier können Sie einen oder mehrere Berichte einer bestimmten Konfiguration zuordnen. Nachdem eine Report Suite zugeordnet wurde, beginnen die Daten automatisch mit dem Datenfluss.

## Automatisch zugeordnete Daten

Das Adobe Experience Platform Edge Network ordnet automatisch viele XDM-Variablen zu. Die vollständige Liste der automatisch zugeordneten Variablen ist [hier](../analytics/automatically-mapped-vars.md)aufgeführt.

## Manuell zugeordnete Daten

Alle vom Edge-Netzwerk erfassten Daten können über Verarbeitungsregeln abgerufen werden. Die Daten werden mithilfe der Punktnotation reduziert und stehen als contextData zur Verfügung.

Wenn du ein Schema hättest, das so aussah.

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    v1,
    v2,
    v3
  ],
  arrayofobjects:[
    {
      obj1key:objval1
    },
    {
      obj2key:objval2
    }
  ]
}
```

Dies wären dann die Kontextdatenschlüssel, die Ihnen zur Verfügung stehen.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array[0] //v1
a.x.array[1] //v2
a.x.array[3] //v3
a.x.arrayofobjects[1].obj1key //objval1
a.x.arrayofobjects[2].obj2key //objval2
```

Hier ein Beispiel für eine Verarbeitungsregel, die diese Daten verwenden würde.

![Benutzeroberfläche für Verarbeitungsregeln](../../../assets/edge_analytics_processing_rules.png)
