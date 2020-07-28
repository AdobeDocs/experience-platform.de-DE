---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Der Data Connector von Analytics
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 97%

---


# Der Data Connector von Analytics

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics Data Connector (ADC) erfassen. ADC streamt Daten, die von Adobe Analytics gesammelt wurden, in Echtzeit an Platform, wobei SCDS-formatierte Analytics-Daten in XDM-Felder (Experience-Datenmodell) umgewandelt werden, um sie für Platform zu nutzen.

Dieses Dokument bietet Ihnen einen Überblick über Adobe Analytics und beschreibt die Anwendungsfälle für Analytics-Daten.

## Adobe Analytics und Analytics-Daten

Adobe Analytics ist eine leistungsstarke Engine, mit der Sie mehr über Ihre Kunden erfahren und herausfinden können, wie sie mit Ihren Web-Eigenschaften interagieren, wo Ihre Ausgaben für digitales Marketing effektiv sind und welche Verbesserungsmöglichkeiten es gibt. Adobe Analytics verarbeitet jährlich mehrere Billionen von Web-Transaktionen. Mit ADC können Sie diese umfangreichen Verhaltensdaten ganz einfach nutzen und das Echtzeit-Kundenprofil in Minutenschnelle anreichern.

![](./images/analytics-data-experience-platform.png)

Adobe Analytics sammelt Daten aus verschiedenen digitalen Kanälen und Rechenzentren auf der ganzen Welt. Nachdem die Daten erfasst wurden, werden VISTA-Regeln (für Besucheridentifikation, Segmentierung und Umwandlungsarchitektur) sowie Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. Nachdem Rohdaten diese kleine Verarbeitung durchlaufen haben, werden sie vom Echtzeit-Kundenprofil als konsumbereit betrachtet. In einem Verfahren, das zu dem oben genannten parallel ist, werden dieselben verarbeiteten Daten in Mikro-Batches gepackt und in Platform-Datensätzen erfasst, die von Data Science Workspace, Query Service und anderen Anwendungen zur Datenerkennung verwendet werden können.

Weitere Informationen zu Verarbeitungsregeln finden Sie unter Übersicht über die [Verarbeitungsregeln](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules.html) .

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die einheitliche Strukturen und Definitionen für eine Anwendung bereitstellt, damit diese mit Diensten in Adobe Experience Platform kommunizieren kann.

Durch Einhaltung von XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weiterführende Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics XDM zugeordnet?

Wenn über die Platform-Benutzeroberfläche eine Quellverbindung zum Übertragen von Analytics-Daten in Experience Platform hergestellt wird, werden Datenfelder automatisch zugeordnet und innerhalb von Minuten in das Echtzeit-Kundenprofil aufgenommen. Anweisungen zum Erstellen einer Quellverbindung mit Adobe Analytics unter Einsatz der Platform-Benutzeroberfläche finden Sie in der Anleitung zum [Data Connector von Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaillierte Informationen zum Feld-Mapping zwischen Analytics und Experience Platform finden Sie im Handbuch zum [Mapping von Adobe Analytics-Feldern](./mapping/analytics.md).

## Wie hoch ist die erwartete Latenz für Analytics-Daten in Platform?

| Analytics-Daten | Erwartete Latenz |
| -------------- | ---------------- |
| Neue Daten an Echtzeit-Kundenprofil (A4T **nicht** aktiviert) | &lt; 2 Minuten |
| Neue Daten an Echtzeit-Kundenprofil (A4T **ist** aktiviert) | &lt; 15 Minuten |
| Neue Daten an Data Lake | &lt; 45 Minuten |
| Aufstockungsdaten (13 Monate Daten oder 10 Milliarden Ereignisse, je nachdem, welcher Wert niedriger ist) | &lt; 4 Wochen |

>[!NOTE]
>
> Die Latenz variiert je nach Kundenkonfiguration, Datenvolumen und Verbraucheranwendungen. Wenn die Analytics-Implementierung beispielsweise mit `A4T` konfiguriert ist, erhöht sich die Latenz zur Pipeline um 5 bis 10 Minuten.