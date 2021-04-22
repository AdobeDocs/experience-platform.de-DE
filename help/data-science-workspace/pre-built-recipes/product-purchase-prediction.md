---
keywords: Experience Platform;Produktkaufrezept;Data Science Workspace;beliebte Themen;Rezepte;Prä-Build-Rezept
solution: Experience Platform
title: Rezept für Produktkäufe
topic-legacy: overview
description: Mit dem Produktkaufprognostizierungsrezept können Sie die Wahrscheinlichkeit eines bestimmten Ereignisses des Kundenkaufs vorhersagen, z. B. eines Produktkaufs.
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 13%

---

# Rezept für Produktkaufprognosen

Mit dem Produktkaufprognostizierungsrezept können Sie die Wahrscheinlichkeit eines bestimmten Ereignisses des Kundenkaufs vorhersagen, z. B. eines Produktkaufs.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Das folgende Dokument beantwortet Fragen wie:
* Für wen ist dieses Rezept gedacht?
* Was macht dieses Rezept?

## Für wen ist dieses Rezept gedacht?

Ihre Marke möchte den vierteljährlichen Umsatz für Ihre Produktlinie durch effektive und zielgerichtete Promotions für Ihre Kunden steigern. Aber nicht alle Kunden sind gleich und Sie wollen Ihr Geld wert. Wen Zielgruppe du? Welche Ihrer Kunden reagieren am ehesten, ohne dass Sie Ihre Promotion in den Griff bekommen? Wie passen Sie Ihre Promotions für jeden Kunden an? Auf welche Kanal sollten Sie sich verlassen und wann sollten Sie Promotions versenden?

## Was macht dieses Rezept?

Das Rezept zur Prognose des Produktkaufs verwendet maschinelles Lernen, um das Kaufverhalten von Kunden vorherzusagen. Dies geschieht durch Anwendung eines benutzerdefinierten Random Forest-Classifications und eines zweistufigen Experience Data Model (XDM), um die Wahrscheinlichkeit eines Kaufs-Ereignisses vorherzusagen. Das Profil nutzt Eingabedaten mit Informationen zum Kundenverhalten und dem bisherigen Kaufverlauf sowie die Standardwerte vordefinierter Konfigurationsparameter, die von unseren Data Scientists festgelegt werden, um die Prädiktionsgenauigkeit zu verbessern.

## Datenschema

Dieses Rezept verwendet [XDM-Schema](../../xdm/home.md), um die Daten zu modellieren. Das für dieses Rezept verwendete Schema ist unten dargestellt:

| Feldname | Typ |
| --- | --- |
| userId | Zeichenfolge |
| genderRatio | Nummer |
| ageY | Nummer |
| ageM | Nummer |
| optinEmail | Boolesch |
| optinMobile | Boolesch |
| optinAddress | Boolesch |
| Erstellt | Ganzzahl |
| totalOrders | Nummer |
| totalItems | Nummer |
| orderDate1 | Nummer |
| shippingDate1 | Nummer |
| totalPrice1 | Nummer |
| tax1 | Nummer |
| orderDate2 | Nummer |
| shippingDate2 | Nummer |
| totalPrice2 | Nummer |


## Algorithmus

Zunächst wird der Schulungsdatensatz im Schema *ProductPrediction* geladen. Von hier aus wird das Modell mit einem [random forest classifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html) trainiert. Random forest classifier ist eine Art zusammengesetzter Algorithmus, der sich auf einen Algorithmus bezieht, der mehrere Algorithmen kombiniert, um eine bessere Vorhersageleistung zu erzielen. Die Idee hinter dem Algorithmus ist, dass der Random Forest Classifier mehrere Entscheidungsbäume baut und diese zusammenführt, um eine genauere und stabilere Prognose zu erstellen.

Dieser Vorgang Beginn beim Erstellen einer Reihe von Entscheidungsbäumen, die nach dem Zufallsprinzip Untergruppen von Schulungsdaten auswählen. Danach werden die Ergebnisse der einzelnen Entscheidungsbaume gemittelt.
