---
keywords: Experience Platform; Rezept für Einzelhandelsumsätze; Data Science Workspace; beliebte Themen; Rezepte; Rezept vorab erstellen
solution: Experience Platform
title: Rezept für Einzelhandelsumsätze
description: Mit dem Rezept "Einzelhandelsumsätze"können Sie eine Prognose für die Umsätze aller für einen bestimmten Zeitraum ausgelieferten Geschäfte erstellen. Mit einem präzisen Prognosemodell könnte der Einzelhändler das Verhältnis zwischen Nachfrage und Preispolitik ermitteln und optimierte Preisentscheidungen treffen, um Verkäufe und Umsätze zu optimieren.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 21%

---

# Einzelhandelsrezept

Mit dem Rezept &quot;Einzelhandelsumsätze&quot;können Sie eine Prognose für die Umsätze aller für einen bestimmten Zeitraum ausgelieferten Geschäfte erstellen. Mit einem präzisen Prognosemodell könnte der Einzelhändler das Verhältnis zwischen Nachfrage und Preispolitik ermitteln und optimierte Preisentscheidungen treffen, um Verkäufe und Umsätze zu optimieren.

Das folgende Dokument beantwortet Fragen wie:
* Für wen ist dieses Rezept gedacht?
* Was macht dieses Rezept?
* Wie sehen die ersten Schritte aus?

## Für wen ist dieses Rezept gedacht?

Einem Einzelhändler hat Probleme damit, auf dem aktuellen Markt wettbewerbsfähig zu bleiben. Ihre Marke will den Jahresumsatz für Ihre Einzelhandelsmarke steigern, aber es gibt viele Entscheidungen, um Ihre Betriebskosten zu minimieren. Zu viel Angebot erhöht die Lagerkosten, während zu wenig Angebot das Risiko erhöht, Kunden an andere Marken zu verlieren. Müssen Sie in den kommenden Monaten mehr Angebot bestellen? Wie entscheiden Sie sich für optimale Preise für Ihre Produkte, um die wöchentlichen Verkaufsziele zu erreichen?

## Was macht dieses Rezept?

Das Rezept &quot;Retail Sales Forecasting&quot;verwendet maschinelles Lernen, um Verkaufstrends vorherzusagen. Das Rezept nutzt dazu die Fülle historischer Einzelhandelsdaten und angepasste Regressoren zur Gänze-Verbesserung oder maschinellen Lernalgorithmen, um den Umsatz eine Woche im Voraus vorherzusagen. Das Modell nutzt den bisherigen Kaufverlauf und Standardeinstellungen für vordefinierte Konfigurationsparameter, die von unseren Data Scientists festgelegt werden, um die Vorhersagegenauigkeit zu verbessern.

## Wie sehen die ersten Schritte aus?

Beginnen Sie mit diesem [Tutorial](../jupyterlab/create-a-model.md).

In diesem Tutorial erfahren Sie, wie Sie das Rezept &quot;Einzelhandelsumsätze&quot;in einem Jupyter-Notebook erstellen und den Workflow Notebook an Rezept verwenden, um das Rezept in Adobe Experience Platform zu erstellen.

## Datenschema

Dieses Rezept verwendet [XDM-Schemata](../../xdm/schema/field-dictionary.md) , um die Daten zu modellieren. Das für dieses Rezept verwendete Schema ist unten dargestellt:

| Feldname | Typ |
| --- | --- |
| date | Zeichenfolge |
| store | Ganzzahl |
| storeType | Zeichenfolge |
| weeklySales | Zahl |
| storeSize | Ganzzahl |
| Temperatur | Zahl |
| regionalFuelPrice | Zahl |
| Markdown | Zahl |
| cpi | Zahl |
| Arbeitslosigkeit | Zahl |
| isHoliday | Boolesch |


## Algorithmus

Zunächst der Trainings-Datensatz im *DSWRetailSales* -Schema geladen wird. Von hier aus wird das Modell mit einem [Gradientenverstärkungs-Regressor-Algorithmus](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). Die Verlaufsverstärkung basiert auf der Vorstellung, dass schwache Lernende (die mindestens etwas besser sind als eine zufällige Chance) eine Abfolge von Lernenden bilden können, die sich auf die Verbesserung der Schwächen früherer Lernender konzentrieren. Gemeinsam können sie genutzt werden, um ein leistungsfähiges Vorhersagemodell zu schaffen.

Der Prozess umfasst drei Elemente: eine Verlustfunktion, einen schwachen Lerner und ein additives Modell.

Die Verlustfunktion bezieht sich auf einen Messwert, wie gut ein Prognosemodell in Bezug auf die Fähigkeit, das erwartete Ergebnis vorherzusagen, funktioniert. In diesem Rezept wird die Regression der kleinsten Quadrate verwendet.

Bei der Gradientenverstärkung wird ein Entscheidungsbaum als schwacher Lerner verwendet. In der Regel werden Bäume mit einer begrenzten Anzahl von Ebenen, Knoten und Aufspaltungen verwendet, um sicherzustellen, dass der Lernende schwach bleibt.

Schließlich wird ein Zusatzmodell verwendet. Nach der Berechnung des Verlusts mit der Verlustfunktion wird der Baum, der den Verlust reduziert, ausgewählt und gewichtet, um die Modellierung der schwierigeren Beobachtungen zu verbessern. Die Ausgabe der gewichteten Baumstruktur wird dann der bestehenden Baumsequenz hinzugefügt, um die endgültige Ausgabe des Modells zu verbessern - Menge der zukünftigen Verkäufe .
