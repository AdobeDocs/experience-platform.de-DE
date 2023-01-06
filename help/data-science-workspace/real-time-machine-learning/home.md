---
keywords: Experience Platform; Entwicklerhandbuch; Data Science Workspace; beliebte Themen; Echtzeit-maschinelles Lernen
solution: Experience Platform
title: Übersicht über maschinelles Lernen in Echtzeit
description: Das maschinelle Lernen in Echtzeit kann die Relevanz Ihrer digitalen Erlebnisinhalte für Ihre Endbenutzer erheblich steigern. Dies wird durch die Nutzung von Echtzeit-Unterscheidungen und kontinuierlichem Lernen am Experience Edge ermöglicht.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 5%

---

# Übersicht über maschinelles Lernen in Echtzeit (Alpha)

>[!IMPORTANT]
>
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzern zur Verfügung. Diese Funktion befindet sich in der Alpha-Phase und wird noch getestet. Dieses Dokument kann sich ändern.

Das maschinelle Lernen in Echtzeit kann die Relevanz Ihrer digitalen Erlebnisinhalte für Ihre Endbenutzer erheblich steigern. Dies wird durch die Nutzung von Echtzeit-Erkenntnissen und kontinuierlichem Lernen über die [!DNL Experience Edge].

Eine Kombination aus nahtloser Berechnung auf dem Hub und der [!DNL Edge] reduziert die Latenz, die traditionell an der Bereitstellung personalisierter Erlebnisse beteiligt ist, die sowohl relevant als auch responsiv sind, erheblich. Daher bietet maschinelles Lernen in Echtzeit Rückschlüsse mit unglaublich geringer Latenz für die synchrone Entscheidungsfindung. Beispiele sind das Rendern von personalisiertem Webseiteninhalt oder das Erscheinen eines Angebots oder Rabatts, um die Abwanderung zu reduzieren und Konversionen in einem Webstore zu erhöhen.

## Architektur des maschinellen Lernens in Echtzeit {#architecture}

Die folgenden Diagramme bieten einen Überblick über die Architektur des maschinellen Lernens in Echtzeit. Derzeit hat Alpha eine vereinfachtere Version.

![Alpha-Bogen](../images/rtml/alpha-arch.png)

![Vereinfachte Übersicht](../images/rtml/end-to-end-arch.png)

## Arbeitsablauf für maschinelles Lernen in Echtzeit

Im folgenden Workflow werden die typischen Schritte und Ergebnisse bei der Erstellung und Verwendung eines Modells für maschinelles Lernen in Echtzeit beschrieben.

### Datenaufnahme und -vorbereitung

Daten werden erfasst und mit der [!DNL Experience Data Model] (XDM) in Adobe Experience Platform. Diese Daten werden für die Modellschulung verwendet. Weitere Informationen zu XDM finden Sie in [XDM – Übersicht](../../xdm/home.md).

### Authoring

Erstellen Sie ein Modell für maschinelles Lernen in Echtzeit, indem Sie es von Grund auf neu erstellen oder als vortrainiertes serialisiertes ONNX-Modell in Adobe Experience Platform Jupyter Notebooks einbinden.

### Implemenierung

Bereitstellen des Modells für [!DNL Experience Edge] , um einen Dienst für maschinelles Lernen in Echtzeit im [!UICONTROL Service Gallery] mithilfe des API-Endpunkts Prognose .

### Folgerung   

Verwenden Sie den REST-API-Endpunkt Prognose , um Einblicke in maschinelles Lernen in Echtzeit zu generieren.

### Versand

Marketingexperten können dann Segmente und Regeln definieren, die maschinelle Lernergebnisse in Echtzeit Erlebnissen mit Adobe Target zuordnen. Auf diese Weise können Besuchern der Website Ihrer Marke in Echtzeit dasselbe oder auf der nächsten Seite personalisierte Erlebnis angezeigt werden.

## Aktuelle Funktionen

Das maschinelle Lernen in Echtzeit befindet sich derzeit in der Alpha-Phase. Die unten beschriebene Funktion kann sich ändern, wenn weitere Funktionen und Knoten verfügbar sind.

>[!NOTE]
>
> Alpha-Einschränkungen:
> - Derzeit werden nur ONNX-basierte Modelle unterstützt.
> - In Knoten verwendete Funktionen können nicht serialisiert werden. Beispielsweise eine Lambda-Funktion, die in einem Pandas-Knoten verwendet wird.
> - Nach 20 Sekunden schlafen [!DNL Edge] Die Bereitstellung erfolgt manuell.
> - Für tiefes Lernen müssen Ihre Daten so gesendet werden, dass `df.values` heißt, es wird ein Array zurückgegeben, das von Ihrem DL-Modell akzeptiert wird. Dies liegt daran, dass der ONNX-Modell-Scoring-Knoten `df.values` und sendet die Ausgabe an das Modell.



### Funktionen:

|  | Alpha (Mai) |
| --- | --- |
| **Funktionen** | - Verwenden Sie die RTML-Notebook-Vorlage, um ein benutzerdefiniertes maschinelles Lernmodell zu erstellen, zu testen und bereitzustellen. <br> - Unterstützung für den Import vortrainierter Modelle für maschinelles Lernen. <br> - Echtzeit-SDK für maschinelles Lernen. <br> - Startersatz von Authoring-Knoten. <br> - Wird auf Adobe Experience Platform Hub bereitgestellt. |
| **Verfügbarkeit** | Nordamerika |
| **Authoring-Knoten** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Aufspaltung <br> - ModelUpload <br> - OneHotEncoder |
| **Scoring-Laufzeiten** | ONNX |

## Nächste Schritte

Beginnen Sie mit den [Ersten Schritten](./getting-started.md). Dieser Leitfaden führt Sie durch die Einrichtung aller erforderlichen Voraussetzungen für die Erstellung eines Modells für maschinelles Lernen in Echtzeit.
