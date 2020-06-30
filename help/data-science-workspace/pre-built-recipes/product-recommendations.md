---
keywords: Experience Platform;product recommendation recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Rezept für Produktempfehlungen
topic: overview
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 5%

---


# Rezept für Produktempfehlungen

Mit dem Rezept &quot;Produktempfehlungen&quot;können Sie personalisierte Produktempfehlungen bereitstellen, die auf die Bedürfnisse und Interessen Ihrer Kunden zugeschnitten sind. Mit einem präzisen Prognosemodell können Sie anhand der Einkaufshistorie eines Kunden feststellen, für welche Produkte Sie sich interessieren.

## Für wen ist dieses Rezept gebaut?

Heutzutage kann ein Einzelhändler eine Vielzahl von Angeboten anbieten, was seinen Kunden eine Vielzahl von Möglichkeiten bietet, die auch die Suche nach ihren Kunden behindern können. Aufgrund von Zeit- und Aufwandsbeschränkungen finden Kunden möglicherweise nicht das gewünschte Produkt, was zu Käufen mit einer hohen kognitiven Dissonanz oder gar keinem Kauf führt.

## Was macht dieses Rezept?

Das Rezept &quot;Produktempfehlungen&quot;verwendet maschinelles Lernen, um die Interaktionen eines Kunden mit Produkten in der Vergangenheit zu analysieren und eine personalisierte Liste von Produktempfehlungen schnell und mühelos zu generieren. Dadurch wird der Produktentdeckungsprozess optimiert und lange, unproduktive, irrelevante Suchvorgänge für Ihre Kunden werden vermieden. Das Rezept &quot;Produktempfehlungen&quot;kann daher die Einkaufserfahrung eines Kunden insgesamt verbessern, was zu einer höheren Interaktion und einer stärkeren Markentreue führt.

## Wie sehen die ersten Schritte aus?

Beginnen Sie mit dem Tutorial Adobe Experience Platform Lab (siehe Link unten). Dieses Lernprogramm zeigt Ihnen, wie Sie das Rezept &quot;Produktempfehlungen&quot;in einem Jupyter-Notebook erstellen, indem Sie dem Arbeitsablauf [für Rezept](../jupyterlab/create-a-recipe.md) folgen und das Rezept in implementieren [!DNL Experience Platform][!DNL Data Science Workspace].

* [Lab: Prognostizieren der Zukunft mit dem Arbeitsbereich für Datenwissenschaften](https://expleague.azureedge.net/labs/L777/index.html)
* [Lab-Ressourcen](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Data schema

Dieses Rezept verwendet benutzerdefinierte [XDM-Schema](../../xdm/schema/field-dictionary.md) , um die Eingabe- und Ausgabedaten zu modellieren:

### Schema für Eingabedaten

| Feldname | Typ |
--- | ---
| itemId | Zeichenfolge |
| interactionType | Zeichenfolge |
| timestamp | Zeichenfolge |
| userId | Zeichenfolge |

### Schema der Ausgabedaten

| Feldname | Typ |
--- | ---
| Empfehlungen | Zeichenfolge |
| userId | Ganzzahl |

## Algorithmus

Das Rezept &quot;Produktempfehlungen&quot;nutzt die kollaborative Filterung, um eine personalisierte Liste von Produktempfehlungen für Ihre Kunden zu generieren. Die kollaborative Filterung erfordert im Gegensatz zu einem inhaltsbasierten Ansatz keine Informationen über ein bestimmtes Produkt, sondern verwendet die historischen Präferenzen eines Kunden für eine Reihe von Produkten. Diese leistungsstarke Empfehlungstechnik basiert auf zwei einfachen Annahmen:
* Es gibt Kunden mit ähnlichen Interessen, und sie können gruppiert werden, indem sie ihr Einkaufs- und Browsing-Verhalten vergleichen.
* Ein Kunde ist eher an einer Empfehlung interessiert, die auf ähnlichen Kunden basiert, was sein Einkaufs- und Browsing-Verhalten betrifft.

Dieser Prozess ist in zwei Hauptschritte unterteilt. Definieren Sie zunächst eine Untergruppe ähnlicher Kunden. Identifizieren Sie dann innerhalb dieses Satzes ähnliche Funktionen unter diesen Kunden, um eine Empfehlung an den Kunden der Zielgruppe zurückzugeben.