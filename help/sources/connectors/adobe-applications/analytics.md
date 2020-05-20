---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics Data Connector
topic: overview
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 3%

---


# Analytics Data Connector

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics Data Connector (ADC) erfassen. ADC streamt Daten, die von Adobe Analytics gesammelt wurden, in Echtzeit an Plattform, wobei SCDS-formatierte Analytics-Daten in XDM-Felder (Experience Data Model) umgewandelt werden, um sie für die Plattform zu verwenden.

Dieses Dokument bietet einen Überblick über Adobe Analytics und beschreibt die Anwendungsfälle für Analytics-Daten.

## Adobe Analytics- und Analytics-Daten

Adobe Analytics ist eine leistungsstarke Engine, mit der Sie mehr über Ihre Kunden erfahren, wie sie mit Ihren Webeigenschaften interagieren, feststellen können, wo Ihre Ausgaben für digitales Marketing effektiv sind, und Verbesserungsbereiche identifizieren können. Adobe Analytics verarbeitet jährlich mehrere Billionen Webtransaktionen. Mit ADC können Sie diese umfangreichen Verhaltensdaten mühelos nutzen und das Echtzeit-Profil Ihrer Kunden in wenigen Minuten erweitern.

![](./images/analytics-data-experience-platform.png)

Adobe Analytics sammelt Daten aus verschiedenen digitalen Kanälen und aus mehreren Rechenzentren auf der ganzen Welt. Nachdem die Daten erfasst wurden, werden VISTA-Regeln (Besucher Identification, Segmentation and Transformation Architecture) und Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. Nachdem die Rohdaten diese leichte Verarbeitung durchlaufen haben, werden sie vom Echtzeit-Kunden-Profil als konsumbereit betrachtet. In einem parallel zu den oben genannten Verfahren werden dieselben verarbeiteten Daten in Kleinststapeln gepackt und in Plattformdatensätze aufgenommen, die von Data Science Workspace, Abfrage Service und anderen Anwendungen zur Datenerkennung verwendet werden können.

Weitere Informationen zu Verarbeitungsregeln finden Sie unter Übersicht über die [Verarbeitungsregeln](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules.html) .

## Erlebnisdatenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die allgemeine Strukturen und Definitionen für eine Anwendung bereitstellt, die zur Kommunikation mit Diensten auf Adobe Experience Platform verwendet werden kann.

Durch die Einhaltung der XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weitere Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics zu XDM zugeordnet?

Wenn über die Plattform-Benutzeroberfläche eine Quellverbindung zum Übertragen von Analytics-Daten in die Experience Platform hergestellt wird, werden Datenfelder automatisch zugeordnet und innerhalb von Minuten in das Echtzeit-Kundenkonto eingeordnet. Anweisungen zum Erstellen einer Quellverbindung mit Adobe Analytics mithilfe der Plattform-Benutzeroberfläche finden Sie im Lernprogramm [Analytics-Datenschnittstellen](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaillierte Informationen zur Feldzuordnung zwischen Analytics und Experience Platform finden Sie im Handbuch zur Feldzuordnung für [Adobe Analytics](./mapping/analytics.md) .

## Welche Latenz wird für Analytics Data on Platform erwartet?

| Analytics-Daten | Erwartete Latenz |
| -------------- | ---------------- |
| Neue Daten für Echtzeit-Kundendaten (A4T **nicht** aktiviert) | &lt; 2 Minuten |
| Neue Daten für Echtzeit-Kundendaten (A4T **ist** aktiviert) | &lt; 15 Minuten |
| Neue Daten in Data Lake | &lt; 45 Minuten |
| Aufstockungsdaten (Daten 13 Monate oder 10 Milliarden Ereignis, je nachdem, welcher Wert niedriger ist) | &lt; 4 Wochen |

>[!NOTE] Die Latenz variiert je nach Kundenkonfiguration, Datenvolumen und Verbraucheranwendungen. Wenn beispielsweise die Analytics-Implementierung mit `A4T` der Latenz für Pipeline konfiguriert ist, wird sie auf 5-10 Minuten erhöht.