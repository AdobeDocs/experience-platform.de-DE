---
keywords: Experience Platform;Retail-Vertriebsrezept;Data Science Workspace;beliebte Themen;Rezepte;Prä-Build-Rezept
solution: Experience Platform
title: Rezept für Einzelhandel
topic-legacy: overview
description: Mit dem Retail Sales-Rezept können Sie eine Prognose der Verkaufszahlen für alle Läden für einen bestimmten Zeitraum erstellen. Mit einem präzisen Prognosemodell könnte der Einzelhändler das Verhältnis zwischen Nachfrage und Preispolitik ermitteln und optimierte Preisentscheidungen treffen, um Verkäufe und Umsätze zu optimieren.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 20%

---

# Rezept für Einzelhandel

Mit dem Retail Sales-Rezept können Sie eine Prognose der Verkaufszahlen für alle Läden für einen bestimmten Zeitraum erstellen. Mit einem präzisen Prognosemodell könnte der Einzelhändler das Verhältnis zwischen Nachfrage und Preispolitik ermitteln und optimierte Preisentscheidungen treffen, um Verkäufe und Umsätze zu optimieren.

Das folgende Dokument beantwortet Fragen wie:
* Für wen ist dieses Rezept gedacht?
* Was macht dieses Rezept?
* Wie sehen die ersten Schritte aus?

## Für wen ist dieses Rezept gedacht?

Einem Einzelhändler hat Probleme damit, auf dem aktuellen Markt wettbewerbsfähig zu bleiben. Ihre Marke möchte den Jahresumsatz für Ihre Handelsmarke steigern, aber es gibt viele Entscheidungen, um Ihre Betriebskosten zu minimieren. Zu viel Angebot erhöht die Lagerkosten, während zu wenig Angebot das Risiko erhöht, Kunden an andere Marken zu verlieren. Müssen Sie in den kommenden Monaten mehr Angebot bestellen? Wie entscheiden Sie sich für optimale Preise für Ihre Produkte, um die wöchentlichen Verkaufsziele zu erreichen?

## Was macht dieses Rezept?

Das Rezept für die Verkaufsvorausschätzung verwendet maschinelles Lernen, um Verkaufstrends vorherzusagen. Das Rezept nutzt dazu den Reichtum an historischen Einzelhandelsdaten und angepasste Steigerungsregressoren oder maschinellen Lernalgorithmen, um den Umsatz eine Woche im Voraus vorherzusagen. Das Modell nutzt den bisherigen Kaufverlauf und verwendet Standardwerte für vordefinierte Konfigurationsparameter, die von unseren Data Scientists festgelegt werden, um die Vorhersagegenauigkeit zu verbessern.

## Wie sehen die ersten Schritte aus?

Beginnen Sie mit diesem [Tutorial](../jupyterlab/create-a-recipe.md).

In diesem Lernprogramm wird beschrieben, wie Sie in einem Jupyter-Notebook das Rezept für den Einzelhandel erstellen und mit dem Notebook-Workflow das Rezept in Adobe Experience Platform erstellen.

## Datenschema

Dieses Rezept verwendet [XDM-Schema](../../xdm/schema/field-dictionary.md), um die Daten zu modellieren. Das für dieses Rezept verwendete Schema ist unten dargestellt:

| Feldname | Typ |
| --- | --- |
| date | Zeichenfolge |
| store | Ganzzahl |
| storeType | Zeichenfolge |
| weeklySales | Nummer |
| storeSize | Ganzzahl |
| Temperatur | Nummer |
| regionalFuelPrice | Nummer |
| markdown | Nummer |
| cpi | Nummer |
| Arbeitslosigkeit | Nummer |
| isHoliday | Boolesch |


## Algorithmus

Zunächst wird der Schulungsdatensatz im Schema *DSWRetailSales* geladen. Von hier aus wird das Modell mit einem [Farbverlauf verstärkenden Regressoralgorithmus](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html) trainiert. Die Verlaufsverstärkung basiert auf der Vorstellung, dass schwache Lernende (die wenigstens etwas besser sind als eine zufällige Chance) eine Reihe von Lernenden bilden können, die sich darauf konzentrieren, die Schwächen des vorherigen Lernenden zu verbessern. Zusammen können sie dazu verwendet werden, ein leistungsfähiges Vorhersagemodell zu schaffen.

Das Verfahren umfasst drei Elemente: eine Verlustfunktion, ein schwacher Lerner und ein additives Modell.

Die Verlustfunktion bezieht sich auf einen Maßstab, wie gut ein Vorhersagemodell im Hinblick auf die Vorhersage des erwarteten Ergebnisses ist - in diesem Rezept wird die Regression der kleinsten Quadrate verwendet.

Bei der Verlaufsverstärkung wird eine Entscheidungsstruktur als schwacher Lernender verwendet. In der Regel werden Bäume mit einer begrenzten Anzahl von Ebenen, Knoten und Teilen verwendet, um sicherzustellen, dass der Lernende schwach bleibt.

Schließlich wird ein Zusatzstoffmodell verwendet. Nach der Berechnung des Verlustes mit der Verlustfunktion wird der Baum, der den Verlust reduziert, gewählt und gewichtet, um die Modellierung der schwierigeren Beobachtungen zu verbessern. Die Ausgabe des gewichteten Baumes wird dann der bestehenden Baumsequenz hinzugefügt, um die endgültige Produktion des Modells zu verbessern - Menge der zukünftigen Verkäufe .
