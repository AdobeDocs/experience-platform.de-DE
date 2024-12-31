---
keywords: Experience Platform;Luma-Web-Daten;Data Science Workspace;beliebte Themen;Rezepte;Demodaten;Demo-Web-Daten;Luma-Daten
solution: Experience Platform
title: Erstellen der Luma-Web-Schemata und -Datensätze
type: Tutorial
description: In diesem Tutorial erhalten Sie die Voraussetzungen und Assets, die für das Demo-Tendenzmodell von Luma erforderlich sind.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Erstellen von Luma-Tendenzmodell-Schemata und -Datensätzen

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

In diesem Tutorial erhalten Sie die Voraussetzungen und Assets, die für alle anderen [!DNL Adobe Experience Platform]-[!DNL Data Science Workspace]-Tutorials erforderlich sind. Nach Abschluss des Vorgangs stehen Ihnen und Ihrem Unternehmen die folgenden Schemata und Datensätze zur Verfügung.

**Schemata:**

- Luma-Web-Datenschema
- Schema der Bewertungsergebnisse für Tendenzmodelle

**Datensätze:**

- Luma-Web-Datensatz
- Trainings-Datensatz für Tendenzmodelle
- Tendenzmodell-Bewertungsdatensatz
- Datensatz für Ergebnisse der Tendenzauswertung

## Herunterladen der Assets {#assets}

Das folgende Tutorial verwendet ein benutzerdefiniertes Luma-Kaufneigungsmodell. Bevor Sie fortfahren[ laden Sie den ZIP-Ordner der erforderlichen ](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) herunter. Dieser Ordner enthält:

- Das Notebook mit der Kaufneigung
- Ein Notebook, mit dem Daten in einen Trainings- und Scoring-Datensatz aufgenommen werden (einen Teil der Luma-Web-Daten)
- Eine JSON-Demodatei mit den Web-Daten von 730.000 Luma-Benutzern
- Ein optionales Python 3 EDA-Notebook (explorative Datenanalyse), das beim Verständnis der Web-Daten und -Modelle verwendet werden kann.

>[!NOTE]
>
> Sie können Ihr eigenes Schema und Ihre eigenen Daten für jedes der Tutorials verwenden. Das in den Assets bereitgestellte Demomodell funktioniert jedoch nur, wenn ihm die entsprechenden Konfigurationsdateien und die erforderlichen Dateien bereitgestellt werden. Dieses Demo-Tendenzmodell wurde für die Verwendung mit Luma-Web-Daten entwickelt.

### Erstellen des Luma-Web-Datenschemas und Aufnehmen der Daten

Um ein Modell zu erstellen, müssen Sie über einen Datensatz in Platform verfügen, mit dem Ihr Modell trainiert und bewertet wird. Das folgende Video-Tutorial aus dem [Data Science Workspace-Kurs](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw&amp;lang=de) führt Sie durch die Erstellung des Luma-Schemas und die Aufnahme der vom Kaufneigungsmodell verwendeten Daten.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Erstellen der Datensätze für Schulungs-, Scoring- und Scoring-Ergebnisse

Um das Rezept-Builder-Notebook auszuführen oder die API zum Trainieren und Bewerten eines Modells zu verwenden, müssen Sie den/die Datensatz/Datensätze und Schema(s) angeben, die für das Training/die Bewertung verwendet werden. Das folgende Video-Tutorial führt Sie durch die Einrichtung der Datensätze für Schulungs-, Scoring- und Scoring-Ergebnisse sowie des Schemas für Scoring-Ergebnisse, das im Kaufneigungsmodell Luma verwendet wird.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die erforderlichen Schemata und Datensätze für das Luma-Tendenzmodell erstellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und das Modell mithilfe des Tutorials [Rezept-Builder-Notebook](../jupyterlab/create-a-model.md) erstellen.

Darüber hinaus können Sie die Daten mit dem bereitgestellten Notebook zur explorativen Datenanalyse (EDA) untersuchen. Dieses Notebook kann verwendet werden, um Muster in den Luma-Daten zu verstehen, die Datenplausibilität zu überprüfen und die relevanten Daten für das prädiktive Tendenzmodell zusammenzufassen. Weitere Informationen zur explorativen Datenanalyse finden Sie in der [EDA-Dokumentation](../jupyterlab/eda-notebook.md).
