---
title: Data Distiller - Übersicht
description: Eine Zusammenfassung der Data Distiller-Nutzungsbeschränkungen für Query Service-Daten im Zusammenhang mit Ihrer Lizenzberechtigung.
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# Data Distiller - Übersicht

Data Distiller ist ein Package, das eine Untergruppe der Funktionen von Adobe Experience Platform enthält. Mit Data Distiller können Sie nach der Erfassung Datenvorbereitung (z. B. Reinigung, Formatierung und Bearbeitung) für Echtzeit-Kundenprofile oder Analytics-Anwendungsfälle durchführen, indem Sie in Query Service Batch-Abfragen ausführen. Ihre Verwendung von Data Distiller hängt von Ihrer aktuellen und fortlaufenden Lizenz für mindestens eine der folgenden Bedingungen ab: Adobe Real-time Customer Data Platform, Customer Journey Analytics und/oder Adobe Journey Optimizer.

## Lizenznutzung {#license-usage}

Siehe [Nutzungsdokument zur Distiller-Lizenz](./license-usage.md) , um wichtige Informationen zur Nutzung der Query Service-Lizenz Ihres Unternehmens anzuzeigen.

## Scoping-Parameter {#scoping-parameters}

Scoping-Parameter sind Nutzungsbeschränkungen, die sich auf das Scoping Ihres vorgeschlagenen Anwendungsfalls beziehen, wie durch Ihre Lizenzkapazität definiert. Ohne Add-ons lauten die Scoping-Parameter von Data Distiller wie folgt:

* **Berechnungsstunden**: Sie können PSQL oder die Query Service-API verwenden, um in einer beliebigen (geplanten oder anderweitig) Sandbox ausgeführte Batch-Abfragen zum Überprüfen und Schreiben von Daten auszuführen. Dabei werden die zugewiesenen Compute Hours pro Jahr verwendet, wie im Scoping-Prozess Ihres Lizenzvertrags festgelegt. Die Gesamtbetriebszeit wird für alle Sandboxes gesammelt.
* **Aufgenommene Daten**: Die in Adobe Experience Platform erfassten Daten, die mit Data Distiller abgefragt werden können, unterliegen den Einschränkungen, die in Ihrer damaligen aktuellen Lizenz für Adobe Real-time Customer Data Platform, Customer Journey Analytics und/oder Adobe Journey Optimizer beschrieben sind.
* **Data Lake Storage**: Der in Ihrer damaligen Lizenz für Adobe Real-time Customer Data Platform, Customer Journey Analytics und/oder Adobe Journey Optimizer bereitgestellte Daten-Lake-Speicher kann auch mit Data Distiller verwendet werden. Data Lake Storage ist eine gemeinsame Funktion.
* **Query Service-Benutzer**: Die Anzahl der Query Service-Benutzer, die in Ihrer aktuellen Lizenz für Adobe Real-time Customer Data Platform, Customer Journey Analytics und/oder Adobe Journey Optimizer aufgeführt sind, kann auch mit Data Distiller verwendet werden. Query Service-Benutzer sind eine freigegebene Funktion.

## Leitlinien

Siehe [Limits für Query Service](../guardrails.md) Dokument zu Standardbeschränkungen für Query Service-Daten in Bezug auf Ihre Lizenzberechtigung.

## Statische Beschränkungen

Eine statische Begrenzung ist die Nutzungsbegrenzung, die sich auf die funktionalen Grenzen der Adobe Experience Platform-Aktivierung bezieht. [Weitere Informationen zur Aktivierung von Adobe Experience Platform](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) finden Sie in den Hilfedokumenten der Adobe. Eine Zusammenfassung der statischen Limits für Data Distiller finden Sie unten. Weitere Informationen finden Sie im Dokument Query Service-Limits .

* **Batch-Abfragen**: Geplante Batch-Abfragen werden nach 24 Stunden beendet.
* **Query Service**: Sie können Query Service für folgende Zwecke verwenden:
   * Zum Ausführen von SQL-Abfragen für die Datenanalyse und die Vorbereitung der Datenerfassung nach der Erfassung (Bereinigen, Gestalten und Bearbeiten).
   * So führen Sie SQL-Abfragen aus, um Datenaggregationsmetriken zu erstellen, die direkt in ein BI-Tool einfließen.
   * So überprüfen Sie Daten schnell in Adobe Experience Platform.
* **Berichterstellungs-API-Aufruf**: Um sicherzustellen, dass Abfragen auf aggregierten Daten mithilfe der Reporting-API ausgeführt werden, verfügen sie über genügend Ressourcen, um effizient auszuführen. Dazu gehören Abfragen, die vorhandene Datenmodelle wie die von Real-time Customer Data Platform bereitgestellten erweitern. Die Reporting-API verfolgt die Ressourcenauslastung, indem jeder Abfrage Gleichzeitigkeitsfenster zugewiesen werden. Es sind maximal 4 Berichterstellungs-API-Aufrufe gleichzeitig verfügbar. Wenn Sie über ein BI-Tool auf die Berichterstellungs-API zugreifen und mehr Zeitfenster für gleichzeitige Nutzung benötigen, ist ein BI-Server erforderlich.


