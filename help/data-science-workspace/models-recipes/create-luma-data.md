---
keywords: Experience Platform; Luma-Web-Daten; Data Science Workspace; beliebte Themen; Rezepte; Demodaten; Demowebdaten; Luma-Daten
solution: Experience Platform
title: Erstellen von Luma-Webschemata und -Datensätzen
type: Tutorial
description: In diesem Tutorial erhalten Sie die Voraussetzungen und Assets, die für das Luma-Demo-Tendenzmodell erforderlich sind.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---

# Erstellen von Luma-Propensity-Modellschemas und -Datensätzen

In diesem Tutorial erhalten Sie die Voraussetzungen und Assets, die für alle anderen [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] Tutorials. Nach Abschluss des Vorgangs stehen Ihnen und Ihrer IMS-Organisation die folgenden Schemas und Datensätze zur Verfügung.

**Schemata:**

- Luma-Webdatenschema
- Schema für Tendenzmodelle mit Scoring-Ergebnissen

**Datensätze:**

- Luma-Webdatensatz
- Trainings-Datensatz für Tendenzmodelle
- Scoring-Datensatz für Tendenzmodelle
- Datensatz mit Tendenzmodellauswertungsergebnissen

## Herunterladen der Assets {#assets}

Das folgende Tutorial verwendet ein benutzerdefiniertes Luma-Kaufneigungsmodell. Vor dem Verfahren [Herunterladen der erforderlichen Assets](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) ZIP-Ordner. Dieser Ordner enthält:

- Das Modell-Notebook mit Kaufneigung
- Ein Notebook, mit dem Daten in einen Trainings- und Scoring-Datensatz (eine Untergruppe der Luma-Webdaten) aufgenommen werden
- Eine JSON-Demodatei mit den Webdaten von 730.000 Luma-Benutzern
- Ein optionales Python 3 EDA-Notebook (Exploratory data analysis), das zum Verständnis der Webdaten und -modelle verwendet werden kann.

>[!NOTE]
>
> Sie können Ihr eigenes Schema und Ihre Daten für jedes der Tutorials verwenden. Das in den Assets bereitgestellte Demo-Modell funktioniert jedoch nur, wenn es über die richtige Konfigurationsdatei und Anforderungsdatei verfügt. Dieses Demo-Tendenzmodell wurde für die Verwendung mit Luma-Webdaten entwickelt.

### Erstellen des Luma-Webdatenschemas und Erfassen der Daten

Um ein Modell zu erstellen, müssen Sie über einen Datensatz in Platform verfügen, der zum Trainieren und Bewertung Ihres Modells verwendet wird. Das folgende Video-Tutorial aus dem [Data Science Workspace-Kurs](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) führt Sie durch die Erstellung des Luma-Schemas und die Erfassung der vom Kaufpropensionsmodell verwendeten Daten.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Erstellen der Datensätze zu Trainings-, Scoring- und Scoring-Ergebnissen

Um das Rezept Builder-Notebook auszuführen oder die API zum Trainieren und Bewerten eines Modells zu verwenden, müssen Sie die Datensätze und Schemas angeben, die für Schulungen/Auswertungen verwendet werden. Das folgende Video-Tutorial führt Sie durch die Einrichtung der Datasets für Trainings-, Scoring- und Scoring-Ergebnisse sowie des Schemas für Scoring-Ergebnisse, das im Luma-Kaufneigungsmodell verwendet wird.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die erforderlichen Schemas und Datensätze für das Luma-Tendenzmodell erstellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und das Modell mithilfe der [Rezept-Builder-Notebook](../jupyterlab/create-a-model.md) Tutorial.

Darüber hinaus können Sie die Daten mithilfe des bereitgestellten Notebooks Exploratory Data Analysis (EDA) untersuchen. Dieses Notebook kann verwendet werden, um Muster in den Luma-Daten zu verstehen, die Datensaniertheit zu überprüfen und die relevanten Daten für das prädiktive Tendenzmodell zusammenzufassen. Weitere Informationen zur Explorationsdatenanalyse finden Sie unter [EDA-Dokumentation](../jupyterlab/eda-notebook.md).
