---
keywords: Experience Platform; Rezept für Produktempfehlungen; Data Science Workspace; beliebte Themen; Rezepte; Rezept vorerstellen
solution: Experience Platform
title: Rezept für Produktempfehlungen
description: Mit dem Rezept „Produktempfehlungen“ können Sie personalisierte Produktempfehlungen bereitstellen, die auf die Bedürfnisse und Interessen Ihrer Kunden zugeschnitten sind. Mit einem präzisen Prognosemodell können Sie anhand der Einkaufshistorie von Kunden feststellen, für welche Produkte sie sich interessieren.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 90%

---

# Rezept für Produktempfehlungen

Mit dem Rezept „Produktempfehlungen“ können Sie personalisierte Produktempfehlungen bereitstellen, die auf die Bedürfnisse und Interessen Ihrer Kunden zugeschnitten sind. Mit einem präzisen Prognosemodell können Sie anhand der Einkaufshistorie von Kunden feststellen, für welche Produkte sie sich interessieren.

## Für wen ist dieses Rezept gedacht?

Heutzutage können Einzelhändler eine Vielzahl von Produkten und Kunden somit eine große Auswahl anbieten, was jedoch auch die Suche erschweren kann. Aufgrund des begrenzten Zeit- und Arbeitsaufwands finden Kunden das gewünschte Produkt möglicherweise gar nicht, was zu Käufen mit hoher kognitiver Dissonanz oder überhaupt keinen Käufen führen kann.

## Was macht dieses Rezept?

Das Rezept „Produktempfehlungen“ verwendet maschinelles Lernen, um frühere Interaktionen eines Kunden mit Produkten zu analysieren sowie schnell und einfach eine personalisierte Liste mit Produktempfehlungen zu generieren. So wird die Produktsuche optimiert und lassen sich lange, unproduktive, irrelevante Suchen für Ihre Kunden vermeiden. Das Rezept „Produktempfehlungen“ kann daher das Einkaufserlebnis von Kunden insgesamt verbessern, was zu mehr Interaktion und einer höheren Markentreue führt.

## Wie sehen die ersten Schritte aus?

Beginnen Sie mit dem Tutorial zum Adobe Experience Platform Lab (siehe Lab-Link unten). In diesem Tutorial erfahren Sie, wie Sie das Produkt-Recommendations-Rezept in einem Jupyter-Notebook erstellen, indem Sie Folgendes befolgen: [Notebook an Rezept](../jupyterlab/create-a-model.md) und Implementierung des Rezepts in [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Lab: Prognostizieren der Zukunft mit Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Lab-Ressourcen](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Datenschema

Dieses Rezept nutzt benutzerdefinierte [XDM-Schemas](../../xdm/schema/field-dictionary.md) zum Modellieren der Eingabe- und Ausgabedaten:

### Schema für Eingabedaten

| Feldname | Typ |
| --- | --- |
| itemId | Zeichenfolge |
| interactionType | Zeichenfolge |
| timestamp | Zeichenfolge |
| userId | Zeichenfolge |

### Schema für Ausgabedaten

| Feldname | Typ |
| --- | --- |
| recommendations | Zeichenfolge |
| userId | Ganzzahl |

## Algorithmus

Das Rezept „Produktempfehlungen“ nutzt kollaborative Filterung, um eine personalisierte Liste mit Produktempfehlungen für Ihre Kunden zu generieren. Kollaborative Filterung erfordert im Gegensatz zu einem inhaltsbasierten Ansatz keine Informationen über ein bestimmtes Produkt, sondern nutzt vielmehr die historischen Präferenzen eines Kunden für eine Reihe von Produkten. Dieses leistungsstarke Empfehlungsverfahren basiert auf zwei einfachen Annahmen:
* Es gibt Kunden mit ähnlichen Interessen; diese lassen sich gruppieren, indem man ihr Einkaufs- und Browsing-Verhalten miteinander vergleicht.
* Kunden sind eher an Empfehlungen interessiert, an denen auch Kunden mit einem ähnlichen Einkaufs- und Browsing-Verhalten Interesse haben.

Dieses Verfahren ist in zwei Hauptschritte unterteilt. Zunächst definieren Sie eine Untergruppe ähnlicher Kunden. Dann identifizieren Sie innerhalb dieser Gruppe ähnliche Merkmale bei den Kunden, um eine Empfehlung für den Zielkunden zurückzugeben.
