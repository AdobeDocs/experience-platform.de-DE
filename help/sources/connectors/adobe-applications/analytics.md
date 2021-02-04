---
keywords: Experience Platform;Home;beliebte Themen;Analytics Data Connector;Analytics;Analytics
solution: Experience Platform
title: Der Data Connector von Analytics
topic: overview
description: Dieses Dokument bietet Ihnen einen Überblick über Analytics und beschreibt die Anwendungsfälle für Analytics-Daten.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 42%

---


# Der Data Connector von Analytics

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics Data Connector (ADC) erfassen. ADC streamt Daten, die von [!DNL Analytics] erfasst wurden, in Echtzeit nach [!DNL Platform] und konvertiert SCDS-formatierte [!DNL Analytics]-Daten in [!DNL Experience Data Model]-(XDM-)Felder, um sie von [!DNL Platform] zu verwenden.

Dieses Dokument bietet eine Übersicht über [!DNL Analytics] und beschreibt die Anwendungsfälle für [!DNL Analytics]-Daten.

## Adobe Analytics und Analytics-Daten

[!DNL Analytics] ist eine leistungsstarke Engine, mit der Sie mehr über Ihre Kunden erfahren und herausfinden können, wie sie mit Ihren Web-Eigenschaften interagieren, wo Ihre Ausgaben für digitales Marketing effektiv sind und welche Verbesserungsmöglichkeiten es gibt. [!DNL Analytics] verwaltet Billionen von Web-Transaktionen pro Jahr und ADC ermöglicht es Ihnen, diese umfangreichen Verhaltensdaten einfach zu erfassen und die  [!DNL Real-time Customer Profile] in wenigen Minuten zu bereichern.

![](./images/analytics-data-experience-platform.png)

Auf hoher Ebene sammelt [!DNL Analytics] Daten von verschiedenen digitalen Kanälen und mehreren Rechenzentren weltweit. Nachdem die Daten erfasst wurden, werden VISTA-Regeln (für Besucheridentifikation, Segmentierung und Umwandlungsarchitektur) sowie Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. Nachdem Rohdaten diese leichte Verarbeitung durchlaufen haben, werden sie von [!DNL Real-time Customer Profile] als konsumbereit betrachtet. In einem Prozess, der parallel zu den oben genannten Daten erfolgt, werden dieselben verarbeiteten Daten in Mikrostapeln gepackt und in Platform-Datasets für den Verbrauch durch [!DNL Data Science Workspace], [!DNL Query Service] und andere Anwendungen zur Datensuche aufgenommen.

Weitere Informationen zu Verarbeitungsregeln finden Sie unter [Übersicht über Verarbeitungsregeln](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules.html).

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die allgemeine Strukturen und Definitionen für eine Anwendung bereitstellt, die für die Kommunikation mit Diensten unter [!DNL Experience Platform] verwendet wird.

Durch Einhaltung von XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weiterführende Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics XDM zugeordnet?

Wenn eine Quellverbindung zum Übertragen von [!DNL Analytics]-Daten in [!DNL Experience Platform] mithilfe der [!DNL Platform]-Benutzeroberfläche eingerichtet wird, werden Datenfelder innerhalb von Minuten automatisch zugeordnet und in [!DNL Real-time Customer Profile] aufgenommen. Anweisungen zum Erstellen einer Quellverbindung mit [!DNL Analytics] mithilfe der [!DNL Platform]-Benutzeroberfläche finden Sie im Lehrgang [Analytics Data Connector](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaillierte Informationen zur Feldzuordnung zwischen [!DNL Analytics] und [!DNL Experience Platform] finden Sie im Handbuch [Adobe Analytics-Feldzuordnung](./mapping/analytics.md).

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