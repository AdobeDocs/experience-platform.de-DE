---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Rezept für Einzelhandel
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 5%

---


# Rezept für Einzelhandel

Mit dem Retail Sales-Rezept können Sie eine Prognose der Verkaufszahlen für alle Läden für einen bestimmten Zeitraum erstellen. Mit einem präzisen Prognosemodell wäre der Einzelhändler in der Lage, das Verhältnis zwischen der Nachfrage- und der Preispolitik zu ermitteln und optimierte Preisentscheidungen zu treffen, um Verkäufe und Umsatz zu maximieren.

Das folgende Dokument beantwortet Fragen wie:
* Für wen ist dieses Rezept gebaut?
* Was macht dieses Rezept?
* Wie sehen die ersten Schritte aus?

## Für wen ist dieses Rezept gebaut?

Ein Einzelhändler steht vor vielen Herausforderungen, um auf dem aktuellen Markt wettbewerbsfähig zu bleiben. Ihre Marke möchte den Jahresumsatz für Ihre Handelsmarke steigern, aber es gibt viele Entscheidungen, um Ihre Betriebskosten zu minimieren. Zu viel Angebot erhöht die Lagerkosten, während zu wenig Angebot das Risiko erhöht, Kunden an andere Marken zu verlieren. Müssen Sie in den kommenden Monaten mehr Angebot bestellen? Wie entscheiden Sie sich für optimale Preise für Ihre Produkte, um die wöchentlichen Verkaufsziele zu erreichen?

## Was macht dieses Rezept?

Das Rezept für die Verkaufsvorausschätzung verwendet maschinelles Lernen, um Verkaufstrends vorherzusagen. Das Rezept nutzt dazu den Reichtum an historischen Einzelhandelsdaten und angepasste Steigerungsregressoren oder maschinellen Lernalgorithmen, um den Umsatz eine Woche im Voraus vorherzusagen. Das Modell nutzt den bisherigen Kaufverlauf und verwendet Standardwerte für vordefinierte Konfigurationsparameter, die von unseren Data Scientists festgelegt werden, um die Vorhersagegenauigkeit zu verbessern.

## Wie sehen die ersten Schritte aus?

Beginnen Sie mit diesem [Tutorial](../jupyterlab/create-a-recipe.md).

In diesem Lernprogramm wird beschrieben, wie Sie das Rezept für den Vertrieb im Einzelhandel in einem Jupyter-Notebook erstellen und mithilfe des Notebooks Arbeitsabläufe für die Skripterstellung in der Adobe Experience Platform erstellen.

## Data schema

Dieses Rezept verwendet [XDM-Schema](../../xdm/schema/field-dictionary.md) , um die Daten zu modellieren. Das für dieses Rezept verwendete Schema ist unten dargestellt:

| Feldname | Typ |
--- | ---
| date | Zeichenfolge |
| store | Ganzzahl |
| storeType | Zeichenfolge |
| weeklySales | Zahl |
| storeSize | Ganzzahl |
| Temperatur | Zahl |
| regionalFuelPrice | Zahl |
| markdown | Zahl |
| cpi | Zahl |
| Arbeitslosigkeit | Zahl |
| isHoliday | Boolesch |


## Algorithmus

Zunächst wird der Schulungsdatensatz im *DSWRetailSales* -Schema geladen. Von hier aus wird das Modell mit einem [Steigerungs-Regressoralgorithmus](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html)trainiert. Die Verlaufsverstärkung basiert auf der Vorstellung, dass schwache Lernende (die wenigstens etwas besser sind als eine zufällige Chance) eine Reihe von Lernenden bilden können, die sich darauf konzentrieren, die Schwächen des vorherigen Lernenden zu verbessern. Zusammen können sie dazu verwendet werden, ein leistungsfähiges Vorhersagemodell zu schaffen.

Das Verfahren umfasst drei Elemente: eine Verlustfunktion, ein schwacher Lerner und ein additives Modell.

Die Verlustfunktion bezieht sich auf einen Maßstab, wie gut ein Vorhersagemodell im Hinblick auf die Vorhersage des erwarteten Ergebnisses ist - in diesem Rezept wird die Regression der kleinsten Quadrate verwendet.

Bei der Verlaufsverstärkung wird eine Entscheidungsstruktur als schwacher Lernender verwendet. In der Regel werden Bäume mit einer begrenzten Anzahl von Ebenen, Knoten und Teilen verwendet, um sicherzustellen, dass der Lernende schwach bleibt.

Schließlich wird ein Zusatzstoffmodell verwendet. Nach der Berechnung des Verlustes mit der Verlustfunktion wird der Baum, der den Verlust reduziert, gewählt und gewichtet, um die Modellierung der schwierigeren Beobachtungen zu verbessern. Die Ausgabe des gewichteten Baumes wird dann der bestehenden Baumsequenz hinzugefügt, um die endgültige Produktion des Modells zu verbessern - Menge der zukünftigen Verkäufe .