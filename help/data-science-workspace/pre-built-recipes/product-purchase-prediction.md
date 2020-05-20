---
keywords: Experience Platform;product purchase recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Rezept zum Produktkauf
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 8%

---


# Rezept zum Produktkauf

## Übersicht

Mit dem Produktkaufprognostizierungsrezept können Sie die Wahrscheinlichkeit eines bestimmten Ereignisses des Kundenkaufs vorhersagen, z. B. eines Produktkaufs.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Das folgende Dokument beantwortet Fragen wie:
* Für wen ist dieses Rezept gebaut?
* Was macht dieses Rezept?

## Für wen ist dieses Rezept gebaut?

Ihre Marke möchte den vierteljährlichen Umsatz für Ihre Produktlinie durch effektive und zielgerichtete Promotions für Ihre Kunden steigern. Aber nicht alle Kunden sind gleich und Sie wollen Ihr Geld wert. Wen Zielgruppe du? Welche Ihrer Kunden reagieren am ehesten, ohne dass Sie Ihre Promotion in den Griff bekommen? Wie passen Sie Ihre Promotions für jeden Kunden an? Auf welche Kanal sollten Sie sich verlassen und wann sollten Sie Promotions versenden?

## Was macht dieses Rezept?

Das Rezept zur Prognose des Produktkaufs verwendet maschinelles Lernen, um das Kaufverhalten von Kunden vorherzusagen. Dies geschieht durch Anwendung eines benutzerdefinierten Random Forest-Classifications und eines zweistufigen Experience Data Model (XDM), um die Wahrscheinlichkeit eines Kaufs-Ereignisses vorherzusagen. Das Profil nutzt Eingabedaten mit Informationen zum Kundenverhalten und dem bisherigen Kaufverlauf sowie die Standardwerte vordefinierter Konfigurationsparameter, die von unseren Data Scientists festgelegt werden, um die Prädiktionsgenauigkeit zu verbessern.

## Data schema

Dieses Rezept verwendet [XDM-Schema](../../xdm/home.md) , um die Daten zu modellieren. Das für dieses Rezept verwendete Schema ist unten dargestellt:

| Feldname | Typ |
--- | ---
| userId | Zeichenfolge |
| genderRatio | Zahl |
| ageY | Zahl |
| ageM | Zahl |
| optinEmail | Boolesch |
| optinMobile | Boolesch |
| optinAddress | Boolesch |
| created | Ganzzahl |
| totalOrders | Zahl |
| totalItems | Zahl |
| orderDate1 | Zahl |
| shippingDate1 | Zahl |
| totalPrice1 | Zahl |
| tax1 | Zahl |
| orderDate2 | Zahl |
| shippingDate2 | Zahl |
| totalPrice2 | Zahl |


## Algorithmus

Zunächst wird der Schulungsdatensatz im Schema *ProductPrediction* geladen. Von hier aus wird das Modell mit einem [zufälligen Waldklassifizierer](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)trainiert. Random forest classifier ist eine Art zusammengesetzter Algorithmus, der sich auf einen Algorithmus bezieht, der mehrere Algorithmen kombiniert, um eine bessere Vorhersageleistung zu erzielen. Die Idee hinter dem Algorithmus ist, dass der Random Forest Classifier mehrere Entscheidungsbäume baut und diese zusammenführt, um eine genauere und stabilere Prognose zu erstellen.

Dieser Vorgang Beginn beim Erstellen einer Reihe von Entscheidungsbäumen, die nach dem Zufallsprinzip Untergruppen von Schulungsdaten auswählen. Danach werden die Ergebnisse der einzelnen Entscheidungsbaume gemittelt.