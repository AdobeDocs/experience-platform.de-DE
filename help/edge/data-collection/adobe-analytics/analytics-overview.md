---
title: Verwenden von Adobe Analytics mit dem Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Daten an Adobe Analytics senden.
keywords: Adobe Analytics;Analytics;zugeordnete Daten;zugeordnete Vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 836fa7814a6966903639e871bfaea0563847f363
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 34%

---

# Verwenden von Adobe Analytics mit dem Platform Web SDK

Die Adobe Experience Platform [!DNL Web SDK] kann Daten an Adobe Analytics senden. Dies funktioniert durch die Übersetzung von `xdm` in ein Format, das Adobe Analytics verwenden kann.

## Einrichten

Adobe Analytics nimmt die gesendeten Daten automatisch auf, wenn in der Benutzeroberfläche für die Kundenkonfiguration eine Report Suite zugeordnet ist. Hier können Sie einen oder mehrere Berichte einer bestimmten Konfiguration zuordnen. Nachdem eine Report Suite zugeordnet wurde, beginnt automatisch der Datenfluss.

## XDM-Feldergruppe

Um die Erfassung der gängigsten Adobe Analytics-Metriken zu vereinfachen, stellen wir eine Analytics-Feldergruppe bereit, die Sie verwenden können. Weitere Informationen zu diesem Schema finden Sie in der Dokumentation für das [Feldergruppe Adobe Analytics ExperienceEvent Full Extension](../../../xdm/field-groups/event/analytics-full-extension.md)

## Automatisch zugeordnete Daten

Die Adobe Experience Platform [!DNL Edge Network] ordnet viele XDM-Variablen automatisch zu. Die vollständige Liste dieser Variablen wird angezeigt [here](automatically-mapped-vars.md).

## Manuell zugeordnete Daten

Alle Daten, die nicht automatisch von der [!DNL Edge Network] kann über Verarbeitungsregeln aufgerufen werden. Die Daten werden mithilfe der Punktnotation reduziert und stehen als Kontextdaten zur Verfügung.

Angenommen, Sie haben ein Schema, das so aussieht:

```javascript
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

Dann wären dies die Kontextdatenschlüssel, die Ihnen zur Verfügung stehen.

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

Hier ein Beispiel für eine Verarbeitungsregel, die diese Daten verwenden würde.

![Benutzeroberfläche für Verarbeitungsregeln](./assets/edge_analytics_processing_rules.png)

>[!NOTE]
>
>Mit der Experience Edge-Sammlung werden alle Ereignisse an Analytics sowie an alle anderen Dienste gesendet, die Sie für Ihren Datastream konfiguriert haben. Wenn Sie beispielsweise sowohl Analytics als auch Target als Dienste konfiguriert haben und separate Aufrufe für die Personalisierung und für Analytics tätigen, werden beide Ereignisse an Analytics und Target gesendet. Diese Ereignisse werden in Analytics-Berichten aufgezeichnet und können sich auf Metriken wie die Absprungrate auswirken.
