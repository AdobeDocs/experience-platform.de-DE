---
keywords: Experience Platform; Startseite; beliebte Themen; Analytics Source Connector; Analytics; Analytics
solution: Experience Platform
title: Adobe Analytics Source Connector für Report Suite-Daten
topic-legacy: overview
description: Dieses Dokument bietet Ihnen einen Überblick über Analytics und beschreibt die Anwendungsfälle für Analytics-Daten.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 25%

---

# Adobe Analytics-Quell-Connector für Report Suite-Daten

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics-Quell-Connector erfassen. Der Quell-Connector [!DNL Analytics] streamt Daten, die von [!DNL Analytics] erfasst wurden, in Echtzeit an Platform und konvertiert SCDS-formatierte [!DNL Analytics]-Daten in [!DNL Experience Data Model] (XDM)-Felder, um sie für Platform zu verwenden.

Dieses Dokument bietet einen Überblick über [!DNL Analytics] und beschreibt die Anwendungsfälle für [!DNL Analytics]-Daten.

## Adobe Analytics und Analytics-Daten

[!DNL Analytics] ist eine leistungsstarke Engine, die Ihnen hilft, mehr über Ihre Kunden zu erfahren, wie sie mit Ihren Web-Eigenschaften interagieren, zu sehen, wo Ihre Ausgaben für digitales Marketing effektiv sind, und zu identifizieren, welche Verbesserungsmöglichkeiten es gibt. [!DNL Analytics] verarbeitet jährlich mehrere Billionen von Web-Transaktionen. Der  [!DNL Analytics] Quell-Connector ermöglicht es Ihnen, diese umfangreichen Verhaltensdaten einfach zu erfassen und  [!DNL Real-time Customer Profile] in Minutenschnelle anzureichern.

![](./images/analytics-data-experience-platform.png)

Auf hoher Ebene erfasst [!DNL Analytics] Daten aus verschiedenen digitalen Kanälen und Rechenzentren auf der ganzen Welt. Nachdem die Daten erfasst wurden, werden VISTA-Regeln (Visitor Identification, Segmentation and Transformation Architecture) und Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. Nachdem die Rohdaten diese einfache Verarbeitung durchlaufen haben, werden sie von [!DNL Real-time Customer Profile] als konsumbereit betrachtet. In einem Prozess, der parallel zu dem oben genannten erfolgt, werden dieselben verarbeiteten Daten in Mikro-Batches gepackt und in Platform-Datensätze aufgenommen, die von [!DNL Data Science Workspace], [!DNL Query Service] und anderen Anwendungen zur Datenerkennung verwendet werden können.

Weitere Informationen zu Verarbeitungsregeln finden Sie unter [Übersicht über Verarbeitungsregeln](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) .

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die einheitliche Strukturen und Definitionen für eine Anwendung bereitstellt, damit diese mit Diensten in Experience Platform kommunizieren kann.

Durch Einhaltung von XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weiterführende Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics XDM zugeordnet?

Wenn über die Platform-Benutzeroberfläche eine Quellverbindung zum Übertragen von [!DNL Analytics]-Daten in die Experience Platform hergestellt wird, werden Datenfelder automatisch zugeordnet und innerhalb von Minuten in [!DNL Real-time Customer Profile] aufgenommen. Anweisungen zum Erstellen einer Quellverbindung mit [!DNL Analytics] unter Verwendung der Platform-Benutzeroberfläche finden Sie im Tutorial [Analytics-Quell-Connector](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaillierte Informationen zur Feldzuordnung zwischen [!DNL Analytics] und der Experience Platform finden Sie im Handbuch [Adobe Analytics field mapping](./mapping/analytics.md) .

## Wie hoch ist die erwartete Latenz für Analytics-Daten in Platform?

| Analytics-Daten | Erwartete Latenz |
| -------------- | ---------------- |
| Neue Daten zu [!DNL Real-time Customer Profile] (A4T **nicht** aktiviert) | &lt; 2 Minuten |
| Neue Daten zu [!DNL Real-time Customer Profile] (A4T **is** aktiviert) | &lt; 15 Minuten |
| Neue Daten an Data Lake | &lt; 90 Minuten |
| Aufstockungsdaten (13 Monate Daten oder 10 Milliarden Ereignisse, je nachdem, welcher Wert niedriger ist) | &lt; 4 Wochen |

>[!NOTE]
>
> Die Latenz variiert je nach Kundenkonfiguration, Datenvolumen und Verbraucheranwendungen. Wenn beispielsweise die [!DNL Analytics]-Implementierung mit `A4T` konfiguriert ist, erhöht sich die Latenz zur Pipeline auf 5-10 Minuten.

## Primäre Kennungen in [!DNL Analytics] -Daten

Jeder Treffer aus dem Quell-Connector [!DNL Analytics] enthält eine primäre Kennung, die davon abhängt, ob eine ECID oder eine AAID vorhanden ist. Wenn eine ECID vorhanden ist, wird die ECID als primäre Kennung bezeichnet. Wenn eine AAID vorhanden ist, wird die AAID als primäre ID bezeichnet.
