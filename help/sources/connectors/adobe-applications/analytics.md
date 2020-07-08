---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics Data Connector
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 3%

---


# Analytics Data Connector

Mit der Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics Data Connector (ADC) erfassen. ADC speichert von Adobe Analytics erfasste Daten in Echtzeit zur Platform und konvertiert SCDS-formatierte Analytics-Daten in Experience Data Model-(XDM-)Felder, um sie nach Platform zu nutzen.

Dieses Dokument bietet einen Überblick über Adobe Analytics und beschreibt die Anwendungsfälle für Analytics-Daten.

## Adobe Analytics- und Analytics-Daten

Adobe Analytics ist eine leistungsstarke Engine, mit der Sie mehr über Ihre Kunden erfahren, wie sie mit Ihren Webeigenschaften interagieren, feststellen können, wo Ihre Ausgaben für digitales Marketing effektiv sind, und Verbesserungsbereiche identifizieren können. Adobe Analytics verarbeitet jährlich mehrere Billionen Webtransaktionen. ADC ermöglicht Ihnen, diese umfangreichen Verhaltensdaten einfach zu nutzen und das Echtzeit-Profil Ihrer Kunden innerhalb weniger Minuten zu erweitern.

![](./images/analytics-data-experience-platform.png)

Auf hoher Ebene sammelt Adobe Analytics Daten von verschiedenen digitalen Kanälen und von mehreren Rechenzentren auf der ganzen Welt. Nachdem die Daten erfasst wurden, werden VISTA-Regeln (Besucher Identification, Segmentation and Transformation Architecture) und Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. Nachdem die Rohdaten diese leichte Verarbeitung durchlaufen haben, werden sie vom Echtzeit-Kunden-Profil als konsumbereit betrachtet. Parallel dazu werden dieselben verarbeiteten Daten in Kleinststapeln gespeichert und in Datasets zur Platform aufgenommen, die von Data Science Workspace, Abfrage Service und anderen Anwendungen zur Datenerkennung verwendet werden.

Weitere Informationen zu Verarbeitungsregeln finden Sie unter Übersicht über die [Verarbeitungsregeln](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules.html) .

## Erlebnisdatenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die allgemeine Strukturen und Definitionen für eine Anwendung bereitstellt, die zur Kommunikation mit Diensten auf der Adobe Experience Platform verwendet wird.

Durch die Einhaltung der XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weitere Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics zu XDM zugeordnet?

Wenn eine Quellverbindung hergestellt wird, um Analytics-Daten mithilfe der Benutzeroberfläche &quot;Platform&quot;in die Experience Platform zu bringen, werden Datenfelder automatisch zugeordnet und innerhalb von Minuten in das Echtzeit-Customer-Profil eingefügt. Anweisungen zum Erstellen einer Quellverbindung mit Adobe Analytics mithilfe der Benutzeroberfläche der Platform finden Sie im Lernprogramm [Analytics Data Connector](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaillierte Informationen zur Feldzuordnung zwischen Analytics und Experience Platform finden Sie im Handbuch [Adobe Analytics Feldzuordnung](./mapping/analytics.md) .

## Welche Latenz wird für Analytics Data on Platform erwartet?

| Analytics-Daten | Erwartete Latenz |
| -------------- | ---------------- |
| Neue Daten für Echtzeit-Kundendaten (A4T **nicht** aktiviert) | &lt; 2 Minuten |
| Neue Daten für Echtzeit-Kundendaten (A4T **ist** aktiviert) | &lt; 15 Minuten |
| Neue Daten in Data Lake | &lt; 45 Minuten |
| Aufstockungsdaten (Daten 13 Monate oder 10 Milliarden Ereignis, je nachdem, welcher Wert niedriger ist) | &lt; 4 Wochen |

>[!NOTE]
>
>Die Latenz variiert je nach Kundenkonfiguration, Datenvolumen und Verbraucheranwendungen. Wenn beispielsweise die Analytics-Implementierung mit `A4T` der Latenz zu Pipeline konfiguriert ist, wird sie auf 5-10 Minuten erhöht.