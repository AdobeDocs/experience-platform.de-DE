---
keywords: Experience Platform;Entwicklerhandbuch;Datenwissenschafts-Arbeitsbereich;beliebte Themen;maschinelles Lernen in Echtzeit;
solution: Experience Platform
title: Übersicht zu maschinellem Lernen in Echtzeit
description: Maschinelles Lernen in Echtzeit kann die Relevanz der Inhalte Ihrer digitalen Erlebnisse für Ihre Endbenutzenden erheblich steigern. Dies wird durch die Nutzung von Echtzeit-Erkenntnissen und kontinuierlichem Lernen im Experience Platform Edge Network ermöglicht.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 93%

---

# Übersicht zu maschinellem Lernen in Echtzeit (Alpha)

>[!IMPORTANT]
>
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzenden zur Verfügung. Diese Funktion befindet sich in der Alpha-Phase und wird noch getestet. Dieses Dokument kann sich ändern.

Maschinelles Lernen in Echtzeit kann die Relevanz der Inhalte Ihrer digitalen Erlebnisse für Ihre Endbenutzenden erheblich steigern. Dies wird durch die Nutzung von Ableitungen in Echtzeit und kontinuierlichem Lernen im [!DNL Experience Platform Edge Network] ermöglicht.

Eine Kombination aus nahtloser Berechnung im Hub und [!DNL Edge] reduziert die Latenz erheblich, die traditionell mit der Bereitstellung hyperpersonalisierter Erlebnisse verbunden ist, die sowohl relevant als auch responsiv sind. Daher bietet maschinelles Lernen in Echtzeit Ableitungen mit unglaublich geringer Latenz für synchrone Entscheidungsfindungen. Beispiele sind das Rendern von personalisiertem Web-Seiteninhalt oder das Erscheinen eines Angebots oder Rabatts, um die Abwanderung zu reduzieren und Konversionen in einem Webstore zu erhöhen.

## Architektur des maschinellen Lernens in Echtzeit {#architecture}

Die folgenden Diagramme bieten einen Überblick über die Architektur des maschinellen Lernens in Echtzeit. Derzeit liegt die Alpha-Version in vereinfachter Form vor.

![Alpha-Architektur](../images/rtml/alpha-arch.png)

![Vereinfachte Übersicht](../images/rtml/end-to-end-arch.png)

## Workflow für maschinelles Lernen in Echtzeit

Im folgenden Workflow werden die typischen Schritte und Ergebnisse bei der Erstellung und Verwendung eines Modells für maschinelles Lernen in Echtzeit beschrieben.

### Datenaufnahme und -vorbereitung

Daten werden aufgenommen und mit dem [!DNL Experience Data Model] (XDM) in Adobe Experience Platform transformiert. Diese Daten werden für das Modell-Training verwendet. Weitere Informationen zu XDM finden Sie in [XDM – Übersicht](../../xdm/home.md).

### Authoring

Erstellen Sie ein Modell für maschinelles Lernen in Echtzeit, indem Sie es von Grund auf neu erstellen oder als vortrainiertes serialisiertes ONNX-Modell in Adobe Experience Platform-Jupyter-Notebooks einbinden.

### Bereitstellung

Stellen Sie Ihr Modell im [!DNL Edge Network] , um einen Dienst für maschinelles Lernen in Echtzeit im [!UICONTROL Service Gallery] mithilfe des API-Endpunkts Prognose .

### Folgerung   

Verwenden Sie den Prognose-REST-API-Endpunkt, um Insights in maschinelles Lernen in Echtzeit zu generieren.

### Versand

Marketing-Fachleute können dann Segmente und Regeln definieren, die in Echtzeit gewonnene maschinelle Lernergebnisse mithilfe von Adobe Target Erlebnissen zuordnen. Auf diese Weise kann Besuchenden der Website Ihrer Marke in Echtzeit auf derselben oder der nächsten Seite ein hyperpersonalisiertes Erlebnis angezeigt werden.

## Aktuelle Funktionalität

Das maschinelle Lernen in Echtzeit befindet sich derzeit in der Alpha-Phase. Die unten beschriebene Funktionalität kann sich ändern, wenn weitere Funktionen und Knoten verfügbar sind.

>[!NOTE]
>
> Alpha-Einschränkungen:
> - Derzeit werden nur ONNX-basierte Modelle unterstützt.
> - In Knoten verwendete Funktionen können nicht serialisiert werden, beispielsweise eine Lambda-Funktion, die in einem Pandas-Knoten verwendet wird.
> - Nach der manuellen Bereitstellung von [!DNL Edge] folgt ein 20 Sekunden langer Ruhezustand.
> - Für tiefes Lernen müssen Ihre Daten so gesendet werden, dass beim Aufruf von `df.values` ein Array zurückgegeben wird, das von Ihrem DL-Modell akzeptiert wird. Dies liegt daran, dass der ONNX-Modell-Bewertungsknoten `df.values` nutzt und die Ausgabe zur Bewertung gegenüber dem Modell sendet.


### Funktionen:

| | Alpha (Mai) |
| --- | --- |
| **Funktionen** | - Verwendung der RTML-Notebook-Vorlage zum Erstellen, Testen und Bereitstellen eines benutzerdefinierten maschinellen Lernmodells <br> - Unterstützung für den Import vortrainierter Modelle für maschinelles Lernen <br> - SDK für maschinelles Lernen in Echtzeit <br> - Startersatz von Erstellungsknoten <br> - Wird im Adobe Experience Platform Hub bereitgestellt. |
| **Verfügbarkeit** | Nordamerika |
| **Erstellungsknoten** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **Bewertung von Laufzeiten** | ONNX |

## Nächste Schritte

Beginnen Sie mit den [Ersten Schritten](./getting-started.md). Dieses Handbuch führt Sie durch die Einrichtung aller erforderlichen Voraussetzungen für die Erstellung eines Modells für maschinelles Lernen in Echtzeit.
