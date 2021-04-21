---
keywords: Experience Platform;Entwicklerhandbuch;Data Science Workspace;beliebte Themen;Echtzeit-maschinelles Lernen
solution: Experience Platform
title: Übersicht über maschinelles Lernen in Echtzeit
topic-legacy: Overview
description: Echtzeit-maschinelles Lernen kann die Relevanz Ihrer digitalen Erlebnisinhalte für Ihre Endbenutzer dramatisch erhöhen. Dies wird durch die Nutzung von Echtzeit-Inferencing und kontinuierlichem Lernen im Experience Edge ermöglicht.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 5%

---

# Übersicht über maschinelles Lernen in Echtzeit (Alpha)

>[!IMPORTANT]
>
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzern zur Verfügung. Diese Funktion ist alphanumerisch und wird noch getestet. Dieses Dokument kann sich ändern.

Echtzeit-maschinelles Lernen kann die Relevanz Ihrer digitalen Erlebnisinhalte für Ihre Endbenutzer dramatisch erhöhen. Dies wird durch die Nutzung von Echtzeit-Inferencing und kontinuierlichem Lernen auf dem [!DNL Experience Edge] ermöglicht.

Eine Kombination aus nahtloser Berechnung auf dem Hub und dem [!DNL Edge] verringert die Latenz, die traditionell an der Bereitstellung hyperpersonalisierter Erlebnisse beteiligt ist, die sowohl relevant als auch reaktionsfähig sind, drastisch. Das maschinelle Lernen in Echtzeit bietet somit eine unglaublich niedrige Latenz für synchrone Entscheidungen. Beispiele sind das Rendern personalisierter Webseiteninhalte oder das Aufdecken eines Angebots oder Rabatt, um die Umrechnung in einem Webstore zu reduzieren und zu erhöhen.

## Architektur für maschinelles Lernen in Echtzeit {#architecture}

Die folgenden Diagramme geben einen Überblick über die Architektur des maschinellen Lernens in Echtzeit. Derzeit hat alpha eine vereinfachtere Version.

![Alpha-Bogen](../images/rtml/alpha-arch.png)

![Vereinfachte Übersicht](../images/rtml/end-to-end-arch.png)

## Arbeitsablauf für maschinelles Lernen in Echtzeit

Im folgenden Arbeitsablauf werden die typischen Schritte und Ergebnisse beim Erstellen und Verwenden eines Echtzeit-maschinellen Lernmodells erläutert.

### Datenerfassung und -vorbereitung

Daten werden mit dem [!DNL Experience Data Model] (XDM) unter Adobe Experience Platform erfasst und transformiert. Diese Daten werden für Modellschulungen verwendet. Weitere Informationen zu XDM finden Sie in [XDM – Übersicht](../../xdm/home.md).

### Authoring

Erstellen Sie ein Echtzeit-Modell für maschinelles Lernen, indem Sie es von Grund auf bearbeiten oder als vorab geschultes serialisiertes ONNX-Modell in Adobe Experience Platform Jupyter-Notebooks einführen.

### Implemenierung

Stellen Sie Ihr Modell auf [!DNL Experience Edge] bereit, um einen Service für maschinelles Lernen in Echtzeit in der [!UICONTROL Dienstgalerie] zu erstellen, indem Sie den Endpunkt der Prognose-API verwenden.

### Folgerung   

Verwenden Sie den REST API-Endpunkt &quot;Prognose&quot;, um Einblicke in das maschinelle Lernen in Echtzeit zu generieren.

### Bereitstellung

Marketingexperten können dann Segmente und Regeln definieren, die Echtzeit-maschinelle Lernergebnisse Erlebnissen mit Adobe Target zuordnen. Dadurch können Besucher der Website Ihrer Marke in Echtzeit mit einem hyper-personalisierten Erlebnis versehen werden.

## Aktuelle Funktion

Das maschinelle Lernen in Echtzeit befindet sich derzeit in der Alpha-Phase. Die unten beschriebene Funktionalität kann sich ändern, da weitere Funktionen und Knoten verfügbar sind.

>[!NOTE]
>
> Alpha-Beschränkungen:
> - Derzeit werden nur ONNX-basierte Modelle unterstützt.
> - Funktionen, die in Knoten verwendet werden, können nicht serialisiert werden. Beispielsweise eine Lambda-Funktion, die in einem Pandas-Knoten verwendet wird.
> - Nach der manuellen Bereitstellung von [!DNL Edge] wird ein 20-Sekunden-Schlaf ausgeführt.
> - Für tiefes Lernen müssen Ihre Daten so gesendet werden, dass `df.values` beim Namen ein Array zurückgibt, das von Ihrem DL-Modell akzeptiert werden kann. Dies liegt daran, dass der ONNX-Modellauswertungsknoten `df.values` verwendet und die Ausgabe an das Modell sendet.



### Funktionen:

|  | Alpha (Mai) |
| --- | --- |
| **Funktionen** | - Verwenden der RTML-Notebook-Vorlage, Erstellen, Testen und Bereitstellen eines benutzerdefinierten maschinellen Lernmodells. <br> - Unterstützung für den Import vorab ausgebildeter Modelle für maschinelles Lernen. <br> - SDK für maschinelles Lernen in Echtzeit. <br> - Startersatz von Authoring-Knoten. <br> - Auf Adobe Experience Platform Hub bereitgestellt. |
| **Verfügbarkeit** | Nordamerika |
| **Authoring-Knoten** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **Laufzeit bewerten** | ONNX |

## Nächste Schritte

Beginnen Sie mit den [Ersten Schritten](./getting-started.md). Dieser Leitfaden führt Sie durch die Einrichtung aller erforderlichen Voraussetzungen für die Erstellung eines maschinellen Lernmodells in Echtzeit.
