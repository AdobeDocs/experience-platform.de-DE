---
keywords: Experience Platform;Produktkaufrezept;Data Science Workspace;beliebte Themen;Rezepte;Rezept vorab erstellen
solution: Experience Platform
title: Rezept für Produktkaufprognosen
description: Mit dem Rezept für die Prognose von Produktkäufen können Sie die Wahrscheinlichkeit eines bestimmten Kundenkaufereignisses vorhersagen, z. B. eines Produktkaufs.
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 11%

---

# Rezept für Produktkaufprognosen

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Mit dem Rezept für die Prognose von Produktkäufen können Sie die Wahrscheinlichkeit eines bestimmten Kundenkaufereignisses vorhersagen, z. B. eines Produktkaufs.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Das folgende Dokument beantwortet Fragen wie:
* Für wen ist dieses Rezept gedacht?
* Was macht dieses Rezept?

## Für wen ist dieses Rezept gedacht?

Ihre Marke möchte den vierteljährlichen Umsatz für Ihre Produktlinie durch effektive und zielgerichtete Werbeaktionen für Ihre Kunden steigern. Allerdings sind nicht alle Kunden gleich und Sie wollen Ihr Geld wert. Auf wen zielen Sie ab? Welche Ihrer Kunden werden am ehesten reagieren, ohne dass Ihre Promotion aufdringlich erscheint? Wie passen Sie Ihre Werbeaktionen für jeden Kunden an? Auf welche Kanäle sollten Sie sich verlassen und wann sollten Sie Werbeaktionen versenden?

## Was macht dieses Rezept?

Das Rezept für die Prognose von Produktkäufen nutzt maschinelles Lernen, um das Kaufverhalten von Kunden vorherzusagen. Dies erfolgt durch die Anwendung einer benutzerdefinierten Klassifizierung der zufälligen Gesamtstruktur und eines zweistufigen Experience-Datenmodells (XDM), um die Wahrscheinlichkeit eines Kaufereignisses vorherzusagen. Das Modell verwendet Eingabedaten, die Kundenprofilinformationen und frühere Kaufhistorien enthalten, und verwendet standardmäßig vorab festgelegte Konfigurationsparameter, die von unseren Datenwissenschaftlern festgelegt werden, um die Prognosegenauigkeit zu verbessern.

## Datenschema

Dieses Rezept verwendet [XDM-Schemata](../../xdm/home.md) um die Daten zu modellieren. Das für dieses Rezept verwendete Schema wird unten angezeigt:

| Feldname | Typ |
| --- | --- |
| userId | Zeichenfolge |
| Geschlechterverhältnis | Zahl |
| AlterJ | Zahl |
| AlterM | Zahl |
| optionEmail | Boolesch |
| optinMobile | Boolesch |
| optinAddress | Boolesch |
| Erstellt | Ganzzahl |
| totalOrders | Zahl |
| totalItems | Zahl |
| orderDate1 | Zahl |
| shippingDate1 | Zahl |
| totalPrice1 | Zahl |
| Steuer1 | Zahl |
| orderDate2 | Zahl |
| shippingDate2 | Zahl |
| totalPrice2 | Zahl |


## Algorithmus

Zunächst wird der Trainings-Datensatz im *ProductPrediction*-Schema geladen. Von hier aus wird das Modell mit einem [Random Forest Classifier“ ](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Random Forest Classifier ist eine Art von verkettetem Algorithmus, der sich auf einen Algorithmus bezieht, der mehrere Algorithmen kombiniert, um eine verbesserte Vorhersageleistung zu erhalten. Die Idee hinter dem Algorithmus ist, dass die zufällige Waldklassifizierung mehrere Entscheidungsbäume erstellt und sie zusammenführt, um eine genauere und stabilere Vorhersage zu erstellen.

Dieser Prozess beginnt mit der Erstellung eines Satzes von Entscheidungsbäumen, die zufällig Untergruppen von Trainingsdaten auswählen. Danach werden die Ergebnisse jedes Entscheidungsbaums gemittelt.
