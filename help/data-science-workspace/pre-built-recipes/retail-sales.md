---
keywords: Experience Platform;Einzelhandelsverkaufsrezept;Data Science Workspace;beliebte Themen;Rezepte;Rezept vorab erstellen
solution: Experience Platform
title: Rezept für Einzelhandelsumsätze
description: Mit dem Rezept für Einzelhandelsumsätze können Sie eine Absatzprognose für alle Läden vorhersagen, die für einen bestimmten Zeitraum vorinstalliert wurden. Mit einem präzisen Prognosemodell könnte der Einzelhändler das Verhältnis zwischen Nachfrage und Preispolitik ermitteln und optimierte Preisentscheidungen treffen, um Verkäufe und Umsätze zu optimieren.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 20%

---

# Einzelhandelsrezept

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Mit dem Rezept für Einzelhandelsumsätze können Sie eine Absatzprognose für alle Läden vorhersagen, die für einen bestimmten Zeitraum vorinstalliert wurden. Mit einem präzisen Prognosemodell könnte der Einzelhändler das Verhältnis zwischen Nachfrage und Preispolitik ermitteln und optimierte Preisentscheidungen treffen, um Verkäufe und Umsätze zu optimieren.

Das folgende Dokument beantwortet Fragen wie:
* Für wen ist dieses Rezept gedacht?
* Was macht dieses Rezept?
* Wie sehen die ersten Schritte aus?

## Für wen ist dieses Rezept gedacht?

Einem Einzelhändler hat Probleme damit, auf dem aktuellen Markt wettbewerbsfähig zu bleiben. Ihre Marke strebt danach, den Jahresumsatz für Ihre Einzelhandelsmarke zu steigern, aber es gibt viele Entscheidungen, um Ihre Betriebskosten zu minimieren. Ein zu hohes Angebot erhöht die Lagerkosten, während ein zu geringes Angebot das Risiko erhöht, Kunden an andere Marken zu verlieren. Benötigen Sie für die kommenden Monate mehr Nachschub? Wie entscheiden Sie sich für eine optimale Preisgestaltung für Ihre Produkte, um die wöchentlichen Verkaufsziele beizubehalten?

## Was macht dieses Rezept?

Das Rezept für die Prognose von Einzelhandelsumsätzen verwendet maschinelles Lernen, um Verkaufstrends vorherzusagen. Das Rezept nutzt dazu die Fülle historischer Einzelhandelsdaten und den benutzerdefinierten, den Regressor verstärkenden Machine-Learning-Algorithmus, um den Umsatz eine Woche im Voraus vorherzusagen. Das Modell nutzt den Verlauf früherer Käufe und verwendet standardmäßig vorab festgelegte Konfigurationsparameter, die von unseren Datenwissenschaftlern festgelegt werden, um die Prognosegenauigkeit zu verbessern.

## Wie sehen die ersten Schritte aus?

Beginnen Sie mit diesem [Tutorial](../jupyterlab/create-a-model.md).

In diesem Tutorial wird beschrieben, wie Sie das Rezept für Einzelhandelsumsätze in einem Jupyter-Notebook erstellen und den Workflow Notebook-Rezepte verwenden, um das Rezept in Adobe Experience Platform zu erstellen.

## Datenschema

Dieses Rezept verwendet [XDM-Schemata](../../xdm/schema/field-dictionary.md) um die Daten zu modellieren. Das für dieses Rezept verwendete Schema wird unten angezeigt:

| Feldname | Typ |
| --- | --- |
| date | String |
| store | Ganzzahl |
| storeType | String |
| wöchentlicher Umsatz | Zahl |
| storeSize | Ganzzahl |
| Temperatur | Zahl |
| regionalFuelPrice | Zahl |
| Markdown | Zahl |
| CPI | Zahl |
| Arbeitslosigkeit | Zahl |
| isHoliday | Boolesch |


## Algorithmus

Zunächst wird der Trainings-Datensatz im *DSWRetailSales*-Schema geladen. Von hier aus wird das Modell mit einem „Gradienten-[ Regressor-Algorithmus“ trainiert](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). Beim Gradientenboosting wird die Idee verwendet, dass schwache Lernende (eine Lernende, die zumindest etwas besser ist als eine Zufallsfolge) eine Folge von Lernenden bilden können, die sich darauf konzentrieren, die Schwächen des vorherigen Lernenden zu verbessern. Zusammen können sie verwendet werden, um ein leistungsfähiges prädiktives Modell zu erstellen.

Der Prozess umfasst drei Elemente: eine Verlustfunktion, einen schwachen Lernenden und ein additives Modell.

Die Verlustfunktion bezieht sich auf ein Maß dafür, wie gut ein Prognosemodell in Bezug auf die Vorhersage des erwarteten Ergebnisses funktioniert - in diesem Rezept wird die Regression der kleinsten Quadrate verwendet.

Beim Steigern des Verlaufs wird ein Entscheidungsbaum als schwacher Teilnehmer verwendet. Normalerweise werden Bäume mit einer eingeschränkten Anzahl von Ebenen, Knoten und Teilungen verwendet, um sicherzustellen, dass die Teilnehmer schwach bleiben.

Schließlich wird ein additives Modell verwendet. Nach der Berechnung des Verlusts mit der Verlustfunktion wird der Baum, der den Verlust reduziert, ausgewählt und gewichtet, um die Modellierung der schwierigeren Beobachtungen zu verbessern. Die Ausgabe des gewichteten Baums wird dann zur vorhandenen Baumreihe hinzugefügt, um die endgültige Ausgabe des Modells zu verbessern - Menge der zukünftigen Verkäufe .
