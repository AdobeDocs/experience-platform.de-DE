---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Der Data Connector von Analytics
topic: overview
translation-type: tm+mt
source-git-commit: a93b3a1980ca0f1d3a32257a923eb7ffc8896fd5
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 42%

---


# Der Data Connector von Analytics

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics Data Connector (ADC) erfassen. ADC speichert Daten, die von [!DNL Analytics] zu [!DNL Platform] in Echtzeit gesammelt werden, und konvertiert SCDS-formatierte [!DNL Analytics] Daten in [!DNL Experience Data Model] (XDM-)Felder, um sie für den Gebrauch durch [!DNL Platform]die Benutzer zu verwenden.

This document provides an overview of [!DNL Analytics] and describes the use-cases for [!DNL Analytics] data.

## Adobe Analytics und Analytics-Daten

[!DNL Analytics] ist eine leistungsstarke Engine, mit der Sie mehr über Ihre Kunden erfahren und herausfinden können, wie sie mit Ihren Web-Eigenschaften interagieren, wo Ihre Ausgaben für digitales Marketing effektiv sind und welche Verbesserungsmöglichkeiten es gibt. [!DNL Analytics] verwaltet Billionen von Web-Transaktionen pro Jahr und ADC ermöglicht es Ihnen, diese umfassenden Verhaltensdaten einfach zu nutzen und die [!DNL Real-time Customer Profile] in wenigen Minuten zu bereichern.

![](./images/analytics-data-experience-platform.png)

At a high level, [!DNL Analytics] collects data from various digital channels and multiple data centers around the world. Nachdem die Daten erfasst wurden, werden VISTA-Regeln (für Besucheridentifikation, Segmentierung und Umwandlungsarchitektur) sowie Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. After raw data has gone through this lightweight processing, it is then considered ready for consumption by [!DNL Real-time Customer Profile]. In a process parallel to the aforementioned, the same processed data is micro-batched and ingested into Platform datasets for consumption by [!DNL Data Science Workspace], [!DNL Query Service], and other data-discovery applications.

Weitere Informationen zu Verarbeitungsregeln finden Sie unter Übersicht über die [Verarbeitungsregeln](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules.html) .

## Experience-Datenmodell (XDM)

XDM is a publicly documented specification that provides common structures and definitions for an application to use to communicate with services on [!DNL Experience Platform].

Durch Einhaltung von XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weiterführende Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics XDM zugeordnet?

When a source connection is established for bringing [!DNL Analytics] data into [!DNL Experience Platform] using the [!DNL Platform] user interface, data fields are automatically mapped and ingested into [!DNL Real-time Customer Profile] within minutes. For instructions on creating a source connection with [!DNL Analytics] using the [!DNL Platform] UI, see the [Analytics data connector tutorial](../../tutorials/ui/create/adobe-applications/analytics.md).

For detailed information on the field mapping that occurs between [!DNL Analytics] and [!DNL Experience Platform], please visit the [Adobe Analytics field mapping](./mapping/analytics.md) guide.

## Wie hoch ist die erwartete Latenz für Analytics-Daten in Platform?

| Analytics-Daten | Erwartete Latenz |
| -------------- | ---------------- |
| Neue Daten zu [!DNL Real-time Customer Profile] (A4T **nicht** aktiviert) | &lt; 2 Minuten |
| Neue Daten zu [!DNL Real-time Customer Profile] (A4T **ist** aktiviert) | &lt; 15 Minuten |
| Neue Daten an Data Lake | &lt; 45 Minuten |
| Aufstockungsdaten (13 Monate Daten oder 10 Milliarden Ereignisse, je nachdem, welcher Wert niedriger ist) | &lt; 4 Wochen |

>[!NOTE]
>
> Die Latenz variiert je nach Kundenkonfiguration, Datenvolumen und Verbraucheranwendungen. Wenn die Analytics-Implementierung beispielsweise mit `A4T` konfiguriert ist, erhöht sich die Latenz zur Pipeline um 5 bis 10 Minuten.

## Primär-IDs in Analytics-Daten

Jeder Treffer aus dem Analytics-Data Connector enthält einen primären Bezeichner, der davon abhängt, ob eine ECID oder eine AAID vorhanden ist. Wenn eine ECID vorhanden ist, wird die ECID als primärer Identifikator bezeichnet. Wenn eine AAID vorhanden ist, wird die AAID als Primär bezeichnet.