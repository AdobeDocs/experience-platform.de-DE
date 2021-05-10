---
keywords: Experience Platform;Home;beliebte Themen;Analytics-Quell-Connector;Analyse;Analytics
solution: Experience Platform
title: Adobe Analytics Source Connector for Report Suite Data
topic-legacy: overview
description: Dieses Dokument bietet Ihnen einen Überblick über Analytics und beschreibt die Anwendungsfälle für Analytics-Daten.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
translation-type: tm+mt
source-git-commit: af5ad975bbfd6a67fe66c90e33da1365d49c8899
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 27%

---

# Adobe Analytics-Quellanschluss für Report Suite-Daten

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics-Quellanschluss erfassen. Der [!DNL Analytics]-Quellanschluss streamt Daten, die von [!DNL Analytics] erfasst werden, in Echtzeit an Plattform, wobei SCDS-formatierte [!DNL Analytics]-Daten in [!DNL Experience Data Model]-(XDM-)Felder umgewandelt werden, die für den Verbrauch nach Plattform bestimmt sind.

Dieses Dokument bietet eine Übersicht über [!DNL Analytics] und beschreibt die Anwendungsfälle für [!DNL Analytics]-Daten.

## Adobe Analytics und Analytics-Daten

[!DNL Analytics] ist eine leistungsstarke Engine, die Ihnen hilft, mehr über Ihre Kunden zu erfahren, wie sie mit Ihren Webeigenschaften interagieren, herauszufinden, wo Ihre Ausgaben für digitales Marketing effektiv sind, und Verbesserungsbereiche zu identifizieren. [!DNL Analytics] verwaltet Billionen von Web-Transaktionen pro Jahr und der  [!DNL Analytics] Quell-Connector ermöglicht es Ihnen, diese umfangreichen Verhaltensdaten einfach zu erfassen und  [!DNL Real-time Customer Profile] in wenigen Minuten zu bereichern.

![](./images/analytics-data-experience-platform.png)

Auf hoher Ebene sammelt [!DNL Analytics] Daten von verschiedenen digitalen Kanälen und mehreren Rechenzentren weltweit. Nachdem die Daten erfasst wurden, werden VISTA-Regeln (Besucher Identification, Segmentation and Transformation Architecture) und Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. Nachdem Rohdaten diese leichte Verarbeitung durchlaufen haben, werden sie von [!DNL Real-time Customer Profile] als konsumbereit betrachtet. In einem Prozess, der parallel zu den oben genannten Daten erfolgt, werden dieselben verarbeiteten Daten in Mikrostapeln gepackt und in Platform-Datasets für den Verbrauch durch [!DNL Data Science Workspace], [!DNL Query Service] und andere Anwendungen zur Datensuche aufgenommen.

Weitere Informationen zu Verarbeitungsregeln finden Sie unter [Übersicht über Verarbeitungsregeln](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/processing-rules/processing-rules.html).

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die einheitliche Strukturen und Definitionen für eine Anwendung bereitstellt, damit diese mit Diensten in Experience Platform kommunizieren kann.

Durch Einhaltung von XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weiterführende Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics XDM zugeordnet?

Wenn eine Quellverbindung hergestellt wird, um [!DNL Analytics]-Daten mithilfe der Plattform-Benutzeroberfläche in die Experience Platform zu bringen, werden Datenfelder automatisch zugeordnet und innerhalb von Minuten in [!DNL Real-time Customer Profile] eingefügt. Anweisungen zum Erstellen einer Quellverbindung mit [!DNL Analytics] mithilfe der Plattform-Benutzeroberfläche finden Sie im Lernprogramm [Analytics-Quellanschluss](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaillierte Informationen zur Feldzuordnung zwischen [!DNL Analytics] und Experience Platform finden Sie im Handbuch [Adobe Analytics field mapping](./mapping/analytics.md).

## Wie hoch ist die erwartete Latenz für Analytics-Daten in Platform?

| Analytics-Daten | Erwartete Latenz |
| -------------- | ---------------- |
| Neue Daten zu [!DNL Real-time Customer Profile] (A4T **nicht** aktiviert) | &lt; 2 Minuten |
| Neue Daten zu [!DNL Real-time Customer Profile] (A4T **ist** aktiviert) | &lt; 15 Minuten |
| Neue Daten an Data Lake | &lt; 90 Minuten |
| Aufstockungsdaten (13 Monate Daten oder 10 Milliarden Ereignisse, je nachdem, welcher Wert niedriger ist) | &lt; 4 Wochen |

>[!NOTE]
>
> Die Latenz variiert je nach Kundenkonfiguration, Datenvolumen und Verbraucheranwendungen. Wenn beispielsweise die Implementierung von [!DNL Analytics] mit `A4T` konfiguriert ist, erhöht sich die Latenz für Pipeline auf 5-10 Minuten.

## Primär-IDs in [!DNL Analytics]-Daten

Jeder Treffer aus dem [!DNL Analytics]-Quellanschluss enthält einen primären Bezeichner, der davon abhängt, ob eine ECID oder eine AAID vorhanden ist. Wenn eine ECID vorhanden ist, wird die ECID als primärer Identifikator bezeichnet. Wenn eine AAID vorhanden ist, wird die AAID als Primär bezeichnet.
