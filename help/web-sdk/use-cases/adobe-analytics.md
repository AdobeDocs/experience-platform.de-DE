---
title: Senden von Daten an Adobe Analytics mithilfe des Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Daten an Adobe Analytics senden.
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Senden von Daten an Adobe Analytics mithilfe des Web SDK

Das Experience Platform Web SDK kann Daten über das Experience Platform-Edge Network an Adobe Analytics senden. Adobe bietet mehrere Optionen zum Senden von Daten an Adobe Analytics mithilfe des Web SDK:

* Fügen Sie Ihrem Schema die Feldergruppe [**[!UICONTROL Adobe Analytics ExperienceEvent]**](../../xdm/field-groups/event/analytics-full-extension.md) hinzu und verwenden Sie dann das Objekt [`XDM` ](../commands/sendevent/xdm.md) .
* Verwenden Sie das [`data` -Objekt](../commands/sendevent/data.md) , um Daten ohne XDM-Schema an Adobe Analytics zu senden.
* Verwenden Sie automatisch generierte [Kontextdatenvariablen](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata) und [Verarbeitungsregeln](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about).

## Verwenden des Objekts `XDM` {#use-xdm-object}

Wenn Sie ein vordefiniertes Adobe Analytics-spezifisches Schema verwenden möchten, können Sie Ihrem Schema die Schemafeldergruppe [Adobe Analytics ExperienceEvent](../../xdm/field-groups/event/analytics-full-extension.md) hinzufügen. Nach dem Hinzufügen können Sie dieses Schema mit dem Objekt `xdm` im Web SDK füllen, um Daten an eine Report Suite zu senden. Wenn Daten in das Edge Network eingehen, wird das XDM-Objekt in ein Format übersetzt, das von Adobe Analytics verstanden wird.

Es gibt zwei Möglichkeiten, Daten über das Web SDK an Adobe Analytics zu senden:

* [Senden von Daten an Adobe Analytics mithilfe der Web SDK-Tag-Erweiterung](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [Senden von Daten an Adobe Analytics mithilfe der Web SDK JavaScript-Bibliothek](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

Eine vollständige Referenz zu XDM-Feldern und deren Zuordnung zu Analytics-Variablen finden Sie unter [Zuordnung von XDM-Objektvariablen zu Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping) im Adobe Analytics-Implementierungshandbuch.

## Verwenden des Objekts `data` {#use-data-object}

Als Alternative zur Verwendung des XDM-Objekts können Sie stattdessen das Datenobjekt verwenden. Das Datenobjekt ist auf Implementierungen ausgerichtet, die derzeit AppMeasurement verwenden, wodurch die Aktualisierung auf das Web SDK viel einfacher wird.

Je nachdem, ob Sie AppMeasurement oder die Analytics-Tag-Erweiterung verwenden, finden Sie in den folgenden Handbüchern Informationen zur Migration zum Web SDK:

* [Migration von der Adobe Analytics-Tag-Erweiterung zur Web SDK-Tag-Erweiterung](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [Migration von AppMeasurement zum Web SDK](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

Eine vollständige Referenz zu Datenobjektfeldern und deren Zuordnung zu Analytics-Variablen finden Sie in der Dokumentation zu [Datenobjektvariablenzuordnung zu Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) im Adobe Analytics-Implementierungshandbuch.

## Kontextdatenvariablen verwenden {#use-context-data-variables}

Variablen, die nicht automatisch zugeordnet werden, sind als [Kontextdatenvariablen](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata) verfügbar. Anschließend können Sie [Verarbeitungsregeln](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) verwenden, um Kontextdatenvariablen Analytics-Variablen zuzuordnen. Wenn Sie beispielsweise über ein benutzerdefiniertes XDM-Schema verfügten, das wie folgt aussah:

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

Dann wären diese Felder die Kontextdatenschlüssel, die Ihnen in der Oberfläche für Verarbeitungsregeln zur Verfügung stehen:

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## Häufig gestellte Fragen

+++ Wie unterscheidet ich Seitenansichtsaufrufe von Linktracking-Aufrufen im Web SDK?

AppMeasurement in Adobe Analytics verwendet separate Methodenaufrufe für Seitenansichten ([`t()` method](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/t-method)) und Linktracking-Aufrufe ([`tl()` method](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method)). Das Web SDK stellt stattdessen nur den Befehl [`sendEvent`](../commands/sendevent/overview.md) zum Senden von Seitenansichten und Linktracking bereit. Die Daten, die Sie in ein Ereignis aufnehmen, bestimmen, ob es sich um eine [Seitenansicht](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-views) oder ein [Seitenereignis](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-events) in Adobe Analytics handelt.

Standardmäßig werden alle Ereignisse in Adobe Analytics als Seitenansichten betrachtet. Wenn Sie ein Web SDK-Ereignis auf einen Adobe Analytics-Linktracking-Aufruf setzen möchten, legen Sie die folgenden Felder fest:

* **XDM-Objekt**: `xdm.web.webInteraction.name`, `web.webInteraction.type` und `web.webInteraction.URL`
* **Datenobjekt**: `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType` und `data.__adobe.analytics.linkURL`
* **Kontextdaten**: Nicht unterstützt

Weitere Informationen finden Sie unter der [`tl()` -Methode](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method) im Adobe Analytics-Implementierungshandbuch.

Wenn Sie im Befehl `configure` die Option [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) aktivieren, werden diese Felder für Sie ausgefüllt.

+++

+++ Wie unterscheidet ein Datastream Daten von anderen Diensten mit Daten, die für Adobe Analytics bestimmt sind?

Alle Ereignisse, die an einen Datastream gesendet werden, werden an alle konfigurierten Dienste übergeben. Wenn Sie beispielsweise separate Aufrufe für Personalisierung und Analytics tätigen, werden beide Ereignisse an Analytics und Target gesendet. Diese Ereignisse werden in Analytics-Berichten aufgezeichnet und können sich auf Metriken wie die Absprungrate auswirken.

Wenn Sie das Web SDK verwenden, werden diese Aufrufe normalerweise im Befehl [`sendEvent`](../commands/sendevent/overview.md) kombiniert.

+++
