---
keywords: Experience Platform; Rezept für den Produktkauf; Data Science Workspace; beliebte Themen; Rezepte; Rezept vor dem Erstellen
solution: Experience Platform
title: Rezept für Vorhersagen bei Produktkäufen
topic-legacy: overview
description: Mit dem Rezept "Vorhersage für Produktkäufe"können Sie die Wahrscheinlichkeit eines bestimmten Typs von Kundenkaufereignissen vorhersagen, z. B. einen Produktkauf.
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 13%

---

# Rezept für Produktakktionsvorhersage

Mit dem Rezept &quot;Vorhersage für Produktkäufe&quot;können Sie die Wahrscheinlichkeit eines bestimmten Typs von Kundenkaufereignissen vorhersagen, z. B. einen Produktkauf.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Das folgende Dokument beantwortet Fragen wie:
* Für wen ist dieses Rezept gedacht?
* Was macht dieses Rezept?

## Für wen ist dieses Rezept gedacht?

Ihre Marke möchte den vierteljährlichen Umsatz für Ihre Produktlinie durch effektive und zielgerichtete Promotions für Ihre Kunden steigern. Aber nicht alle Kunden sind gleich und Sie wollen den Wert Ihres Geldes. Wen zitierst du? Welche Ihrer Kunden reagieren am ehesten, ohne dass Ihre Promotion störend ist? Wie passen Sie Ihre Promotions für jeden Kunden an? Auf welche Kanäle sollten Sie sich verlassen und wann sollten Sie Promotions senden?

## Was macht dieses Rezept?

Das Rezept &quot;Vorhersage für Produktkäufe&quot;nutzt maschinelles Lernen, um das Kaufverhalten von Kunden vorherzusagen. Dies geschieht durch Anwendung eines benutzerdefinierten Random Forest-Classifications und eines zweistufigen Experience-Datenmodells (XDM) zur Vorhersage der Wahrscheinlichkeit eines Kaufereignisses. Das Modell nutzt Eingabedaten, die Kundenprofilinformationen sowie frühere Kaufverlauf und Standardwerte aus von unseren Data Scientists bestimmten vordefinierten Konfigurationsparametern enthalten, um die Vorhersagegenauigkeit zu verbessern.

## Datenschema

Dieses Rezept verwendet [XDM-Schemata](../../xdm/home.md) , um die Daten zu modellieren. Das für dieses Rezept verwendete Schema ist unten dargestellt:

| Feldname | Typ |
| --- | --- |
| userId | Zeichenfolge |
| genderRatio | Zahl |
| ageY | Zahl |
| ageM | Zahl |
| optinEmail | Boolesch |
| optinMobile | Boolesch |
| optinAddress | Boolesch |
| Erstellt | Ganzzahl |
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

Zunächst der Trainings-Datensatz im *ProductPrediction* -Schema geladen wird. Von hier aus wird das Modell mit einem [Random Forest-Classification](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Random forest classifier ist ein Typ von Ensembles Algorithmus, der auf einen Algorithmus verweist, der mehrere Algorithmen kombiniert, um eine verbesserte Vorhersageleistung zu erhalten. Die Idee hinter dem Algorithmus ist, dass der Random Forest Classifier mehrere Entscheidungsbäume baut und zusammenführt, um eine präzisere und stabilere Vorhersage zu erhalten.

Dieser Prozess beginnt mit der Erstellung einer Reihe von Entscheidungsbäumen, die nach dem Zufallsprinzip Untergruppen von Trainings-Daten auswählen. Danach werden die Ergebnisse jedes Entscheidungsbaums im Durchschnitt ermittelt.
