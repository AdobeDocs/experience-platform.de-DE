---
title: Senden von Daten an Adobe Analytics mithilfe der Web-SDK
description: Erfahren Sie, wie Sie mit Adobe Experience Platform Web SDK Daten an Adobe Analytics senden.
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Senden von Daten an Adobe Analytics mithilfe der Web-SDK

Der Experience Platform Web SDK kann Daten über das Experience Platform-Edge Network an Adobe Analytics senden. Adobe bietet mehrere Optionen, um Daten mithilfe der Web-SDK an Adobe Analytics zu senden:

* Fügen Sie die [**[!UICONTROL Adobe Analytics ExperienceEvent]**](../../xdm/field-groups/event/analytics-full-extension.md)Feldergruppe zu Ihrem Schema hinzu und verwenden Sie dann das [`XDM`-Objekt](../commands/sendevent/xdm.md).
* Verwenden Sie das [`data` -](../commands/sendevent/data.md), um Daten ohne XDM-Schema an Adobe Analytics zu senden.
* Verwenden Sie automatisch generierte [Kontextdatenvariablen](https://experienceleague.adobe.com/de/docs/analytics/implementation/vars/page-vars/contextdata) und [Verarbeitungsregeln](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about).

## Verwenden des `XDM` {#use-xdm-object}

Wenn Sie ein vordefiniertes Schema verwenden möchten, das speziell für Adobe Analytics gilt, können Sie die Schemafeldgruppe [Adobe Analytics ExperienceEvent](../../xdm/field-groups/event/analytics-full-extension.md) zu Ihrem Schema hinzufügen. Nach dem Hinzufügen können Sie dieses Schema mithilfe des `xdm`-Objekts in der Web-SDK ausfüllen, um Daten an eine Report Suite zu senden. Wenn Daten am Edge Network eintreffen, wird das XDM-Objekt in ein Format übersetzt, das Adobe Analytics versteht.

Es gibt zwei Möglichkeiten, Daten über Web SDK an Adobe Analytics zu senden:

* [Senden von Daten an Adobe Analytics mithilfe der Tag-Erweiterung „Web SDK&quot;](https://experienceleague.adobe.com/de/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [Senden von Daten an Adobe Analytics mithilfe der Web SDK JavaScript-Bibliothek](https://experienceleague.adobe.com/de/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

Siehe [XDM-Objektvariablenzuordnung zu Adobe Analytics](https://experienceleague.adobe.com/de/docs/analytics/implementation/aep-edge/xdm-var-mapping) im Adobe Analytics-Implementierungshandbuch für eine vollständige Referenz zu XDM-Feldern und deren Zuordnung zu Analytics-Variablen.

## Verwenden des `data` {#use-data-object}

Als Alternative zur Verwendung des XDM-Objekts können Sie stattdessen das Datenobjekt verwenden. Das Datenobjekt ist auf Implementierungen ausgerichtet, die derzeit AppMeasurement verwenden, was das Upgrade auf die Web-SDK viel einfacher macht.

Je nachdem, ob Sie AppMeasurement oder die Analytics-Tag-Erweiterung verwenden, finden Sie in den folgenden Handbüchern Details zur Migration zu Web SDK:

* [Migrieren von der Adobe Analytics-Tag-Erweiterung zur Web SDK-Tag-Erweiterung](https://experienceleague.adobe.com/de/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [Migration vom AppMeasurement zur Web-SDK](https://experienceleague.adobe.com/de/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

Eine vollständige Referenz der Datenobjektfelder und ihrer Zuordnung zu Analytics[Variablen finden Sie in der Dokumentation ](https://experienceleague.adobe.com/de/docs/analytics/implementation/aep-edge/data-var-mapping)Datenobjektvariablenzuordnung zu Adobe Analytics&quot; im Adobe Analytics-Implementierungshandbuch.

## Verwenden von Kontextdatenvariablen {#use-context-data-variables}

Alle Variablen, die nicht automatisch zugeordnet werden, sind als [Kontextdatenvariablen“ ](https://experienceleague.adobe.com/de/docs/analytics/implementation/vars/page-vars/contextdata). Anschließend können Sie [Verarbeitungsregeln](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) verwenden, um Kontextdatenvariablen Analytics-Variablen zuzuordnen. Angenommen, Sie haben ein benutzerdefiniertes XDM-Schema, das wie folgt aussieht:

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

Dann wären diese Felder die Kontextdatenschlüssel, die Ihnen in der Benutzeroberfläche für Verarbeitungsregeln zur Verfügung stehen:

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

+++Wie unterscheide ich Seitenansichtsaufrufe von Linktracking-Aufrufen in Web SDK?

Beim AppMeasurement in Adobe Analytics werden separate Methodenaufrufe für Seitenansichten ([`t()`) ](https://experienceleague.adobe.com/de/docs/analytics/implementation/vars/functions/t-method) Linktracking-Aufrufe ([`tl()`) ](https://experienceleague.adobe.com/de/docs/analytics/implementation/vars/functions/tl-method). Die Web-SDK stellt stattdessen nur den [`sendEvent`](../commands/sendevent/overview.md)-Befehl zum Senden sowohl von Seitenansichten als auch von Linktracking bereit. Die Daten, die Sie in ein Ereignis einbeziehen, bestimmen, ob es sich um eine [Seitenansicht](https://experienceleague.adobe.com/de/docs/analytics/components/metrics/page-views) oder ein [Seitenereignis](https://experienceleague.adobe.com/de/docs/analytics/components/metrics/page-events) in Adobe Analytics handelt.

Standardmäßig werden alle Ereignisse in Adobe Analytics als Seitenansichten betrachtet. Wenn Sie ein Web-SDK-Ereignis auf einen Adobe Analytics-Linktracking-Aufruf festlegen möchten, legen Sie die folgenden Felder fest:

* **XDM-Objekt**: `xdm.web.webInteraction.name`, `web.webInteraction.type` und `web.webInteraction.URL`
* **Datenobjekt**: `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType` und `data.__adobe.analytics.linkURL`
* **Kontextdaten**: Nicht unterstützt

Weitere Informationen finden Sie [&#128279;](https://experienceleague.adobe.com/de/docs/analytics/implementation/vars/functions/tl-method) der `tl()` Methode im Adobe Analytics-Implementierungshandbuch .

Wenn Sie [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) im `configure`-Befehl aktivieren, werden diese Felder für Sie ausgefüllt.

+++

+++Wie unterscheidet ein Datenstrom Daten von anderen Services mit Daten, die für Adobe Analytics vorgesehen sind?

Alle Ereignisse, die an einen Datenstrom gesendet werden, werden an alle konfigurierten Services übergeben. Wenn Sie beispielsweise separate Aufrufe für Personalisierung und Analyse ausführen, werden beide Ereignisse an Analytics und Target gesendet. Diese Ereignisse werden im Analytics-Reporting aufgezeichnet und können Metriken wie die Absprungrate beeinflussen.

Wenn Sie die Web-SDK verwenden, werden diese Aufrufe normalerweise im [`sendEvent`](../commands/sendevent/overview.md)-Befehl kombiniert.

+++
