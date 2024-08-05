---
keywords: Experience Platform; Einzelhandelsumsätze Rezept; Daten Wissenschaft Arbeitsbereich; beliebte Themen; Rezepte; Vor Build Rezept
solution: Experience Platform
title: Retail Sales-Recipe
description: Mit dem Rezept "Einzelhandelsumsätze" können Sie die Prognose Verkäufe für alle Geschäfte vorhersagen, die für eine bestimmte Zeitraum gesetzt sind. Mit einem präzisen Prognosemodell könnte der Einzelhändler das Verhältnis zwischen Nachfrage und Preispolitik ermitteln und optimierte Preisentscheidungen treffen, um Verkäufe und Umsätze zu optimieren.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 20%

---

# Einzelhandelsrezept

>[!NOTE]
>
>Daten Science Arbeitsbereich ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit früheren Berechtigungen für Daten Science Arbeitsbereich.

Mit dem Rezept &quot;Einzelhandelsumsätze&quot; können Sie die Prognose Verkäufe für alle Geschäfte vorhersagen, die für eine bestimmte Zeitraum gesetzt sind. Mit einem präzisen Prognosemodell könnte der Einzelhändler das Verhältnis zwischen Nachfrage und Preispolitik ermitteln und optimierte Preisentscheidungen treffen, um Verkäufe und Umsätze zu optimieren.

Folgende Dokument beantworten Fragen wie:
* Für wen ist dieses Rezept gedacht?
* Was macht dieses Rezept?
* Wie sehen die ersten Schritte aus?

## Für wen ist dieses Rezept gedacht?

Einem Einzelhändler hat Probleme damit, auf dem aktuellen Markt wettbewerbsfähig zu bleiben. Ihr Werbetreibender zielt darauf ab, den Jahresumsatz für Ihre Einzelhandels Werbetreibender zu steigern, aber es gibt viele Entscheidungen, die Sie treffen müssen, um Ihre Betriebskosten zu minimieren. Ein zu hohes Angebot erhöht Warenbestand Kosten, während ein zu geringes Angebot das Risiko erhöht, Kunden an andere Marken zu verlieren. Benötigen Sie für die kommenden Monate mehr Vorrat bestellen? Wie entscheiden Sie sich für die optimale Preisgestaltung für Ihre Produkte, um die wöchentlichen Verkaufsziele zu erreichen?

## Was macht dieses Rezept?

Die Rezept zur Prognose von Einzelhandelsumsätzen nutzt maschinelles Lernen, um Verkaufstrends vorherzusagen. Das Rezept tut dies, indem es die Fülle historischer Einzelhandelsdaten und den benutzerdefinierten Regressor-Machine-Learning-Algorithmus nutzt, um den Umsatz eine Woche im Voraus vorherzusagen. Das Modell nutzt die Kaufhistorie der Vergangenheit und verwendet standardmäßig vordefinierte Konfigurationsparameter, die von unseren Daten Wissenschaftlern festgelegt wurden, um die Vorhersagegenauigkeit zu verbessern.

## Wie sehen die ersten Schritte aus?

Folgen Sie dieser [Anleitung](../jupyterlab/create-a-model.md).

In diesem Anleitung werden die Erstellung des Rezept &quot;Retail Sales&quot; in einem Jupyter Notebook und die Verwendung des Notebooks zum Rezept arbeitsablauf zum Erstellen der Rezept in Adobe Experience Platform beschrieben.

## Datenschema

Dieses Rezept verwendet [XDM Schemata, um die Daten zu modellieren](../../xdm/schema/field-dictionary.md) . Im Folgenden finden Sie die Schema, die für diese Rezept verwendet werden:

| Feldname | Typ |
| --- | --- |
| date | String |
| abspeichern | Ganzzahl |
| storeType | String |
| weeklySales | Zahl |
| storeSize | Ganzzahl |
| Temperatur | Zahl |
| regionalFuelPrice | Zahl |
| Abschlag | Zahl |
| cpi | Zahl |
| Arbeitslosigkeit | Zahl |
| isHoliday | Boolesch |


## Algorithmus

Zuerst wird die Training Datensatz in der *DSWRetailSales* Schema geladen. Von hier aus wird das Modell mit einem [Gradient Boosting Regressor-Algorithmus](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html) trainiert. Verlauf Boosting verwendet die Idee, dass schwache Lernende (eine, die zumindest geringfügig besser ist als der Zufall) eine Reihe von Lernenden bilden können, die sich darauf konzentrieren, die Schwächen des vorherigen Lernenden zu verbessern. Zusammen können sie verwendet werden, um ein leistungsfähiges Vorhersagemodell zu erstellen.

Der Prozess umfasst drei Elemente: eine Verlustfunktion, einen schwachen Lerner und ein additives Modell.

Die Verlustfunktion bezieht sich auf eine messen darüber, wie gut ein Vorhersagemodell in Bezug auf die Vorhersage des erwarteten Ergebnisses abschneidet - die Regression der kleinsten Quadrate wird in diesem Rezept verwendet.

Beim Gradient Boosting wird ein Entscheidungsbaum als schwacher Lerner verwendet. In der Regel werden Bäume mit einer begrenzten Anzahl von Layern, Knoten und Teilungen verwendet, um sicherzustellen, dass der Lernende schwach bleibt.

Schließlich wird ein additives Modell verwendet. Nach der Berechnung des Verlusts mit der Verlustfunktion wird der Baum, der den Verlust reduziert, ausgewählt und gewichtet, um die Modellierung der schwierigeren Beobachtungen zu verbessern. Die Ausgabe des gewichteten Baums wird dann der vorhandenen Sequenz von Bäumen hinzugefügt, um die endgültige Ausgabe des Modells zu verbessern - Anzahl zukünftiger Verkäufe .
