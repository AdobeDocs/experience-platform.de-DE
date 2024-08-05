---
keywords: Experience Platform; Modell für maschinelles Lernen; Data Science Workspace; beliebte Themen; Modell erstellen und veröffentlichen
solution: Experience Platform
title: Erstellen und Publish eines Modells für maschinelles Lernen
type: Tutorial
description: Im folgenden Handbuch werden die Schritte beschrieben, die zum Erstellen und Veröffentlichen eines Modells für maschinelles Lernen erforderlich sind.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 4%

---


# Erstellen und Veröffentlichen eines Modells für maschinelles Lernen

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Im folgenden Handbuch werden die Schritte beschrieben, die zum Erstellen und Veröffentlichen eines Modells für maschinelles Lernen erforderlich sind. Jeder Abschnitt enthält eine Beschreibung Ihrer Aktionen sowie einen Link zur Benutzeroberfläche und API-Dokumentation, um den beschriebenen Schritt durchzuführen.

## Erste Schritte

Bevor Sie mit diesem Tutorial beginnen, müssen Sie folgende Voraussetzungen erfüllen:

- Zugriff auf [!DNL Adobe Experience Platform]. Wenn Sie keinen Zugriff auf eine Organisation in [!DNL Experience Platform] haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

- Alle Data Science Workspace-Tutorials verwenden das Luma-Tendenzmodell. Um fortzufahren, müssen Sie die [Luma-Eigenschaftenmodellschemata und -datensätze](./create-luma-data.md) erstellt haben.

### Daten durchsuchen und Schemata verstehen

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Datensätze]** aus, um alle vorhandenen Datensätze aufzulisten und den Datensatz auszuwählen, den Sie untersuchen möchten. In diesem Fall sollten Sie den Datensatz **Luma Web data** auswählen.

![Luma-Webdatensatz auswählen](../images/models-recipes/model-walkthrough/luma-dataset.png)

Die Seite mit der Datensatzaktivität wird geöffnet und enthält Informationen zu Ihrem Datensatz. Sie können oben rechts die Option **[!UICONTROL Datensatz-Vorschau]** auswählen, um Beispieldatensätze zu untersuchen. Sie können auch das Schema für den ausgewählten Datensatz anzeigen.

![Vorschau der Luma-Webdaten anzeigen](../images/models-recipes/model-walkthrough/preview-dataset.png)

Wählen Sie in der rechten Leiste den Schema-Link aus. Es wird ein Popup angezeigt. Wenn Sie den Link unter **[!UICONTROL Schemaname]** auswählen, wird das Schema in einer neuen Registerkarte geöffnet.

![Vorschau des Luma-Webdatenschemas anzeigen](../images/models-recipes/model-walkthrough/preview-schema.png)

Sie können die Daten mithilfe des bereitgestellten Notebooks Exploratory Data Analysis (EDA) weiter untersuchen. Dieses Notebook kann verwendet werden, um Muster in den Luma-Daten zu verstehen, die Datensaniertheit zu überprüfen und die relevanten Daten für das prädiktive Tendenzmodell zusammenzufassen. Weitere Informationen zur Explorationsdatenanalyse finden Sie in der [EDA-Dokumentation](../jupyterlab/eda-notebook.md).

## Erstellen des Luma-Tendenzrezepts {#author-your-model}

Eine Hauptkomponente des Lebenszyklus von [!DNL Data Science Workspace] besteht aus der Erstellung von Rezepten und Modellen. Das Luma-Tendenzmodell wurde entwickelt, um eine Vorhersage darüber zu generieren, ob Kunden eine hohe Tendenz haben, ein Produkt von Luma zu kaufen.

Zum Erstellen des Luma-Tendenzmodells wird die Vorlage &quot;Rezept-Builder&quot;verwendet. Rezepte bilden die Grundlage für ein Modell, da sie Algorithmen für maschinelles Lernen und Logik zur Lösung spezifischer Probleme enthalten. Wichtiger noch: Rezepte ermöglichen es Ihnen, das maschinelle Lernen in Ihrer Organisation zu demokratisieren, sodass andere Benutzer für unterschiedliche Anwendungsfälle auf ein Modell zugreifen können, ohne Code schreiben zu müssen.

Befolgen Sie das Tutorial [Erstellen eines Modells mit JupyterLab Notebooks](../jupyterlab/create-a-model.md) , um das Rezept für das Luma-Tendenzmodell zu erstellen, das in nachfolgenden Tutorials verwendet wird.

## Importieren und verpacken Sie ein Rezept aus externen Quellen (*optional*)

Wenn Sie ein Rezept zur Verwendung in Data Science Workspace importieren und verpacken möchten, müssen Sie Ihre Quelldateien in einer Archivdatei verpacken. Befolgen Sie das Tutorial [Quelldateien in ein Rezept verpacken](./package-source-files-recipe.md) . In diesem Tutorial erfahren Sie, wie Sie Quelldateien in einem Rezept verpacken. Dies ist die Voraussetzung für den Import eines Rezepts in Data Science Workspace. Sobald das Tutorial abgeschlossen ist, erhalten Sie ein Docker-Bild in einer Azure Container Registry sowie die entsprechende Bild-URL, d. h. eine Archivdatei.

Diese Archivdatei kann verwendet werden, um ein Rezept in Data Science Workspace zu erstellen, indem Sie dem Workflow zum Importieren von Rezepten mithilfe des Arbeitsablaufs für die Benutzeroberfläche [1} oder des [API-Workflows](./import-packaged-recipe-api.md) folgen.](./import-packaged-recipe-ui.md)

## Modell trainieren und bewerten {#train-and-evaluate-your-model}

Nachdem Ihre Daten vorbereitet wurden und ein Rezept bereit ist, können Sie Ihr maschinelles Lernmodell weiter erstellen, trainieren und bewerten. Bei Verwendung des Recipe Builder sollten Sie Ihr Modell bereits trainiert, bewertet und bewertet haben, bevor Sie es in ein Rezept verpacken.

Mit der Data Science Workspace-Benutzeroberfläche und -API können Sie Ihr Rezept als Modell veröffentlichen. Darüber hinaus können Sie bestimmte Aspekte Ihres Modells weiter anpassen, z. B. das Hinzufügen, Entfernen und Ändern von Hyperparametern.

### Modell erstellen

Weitere Informationen zum Erstellen eines Modells mithilfe der Benutzeroberfläche finden Sie im Tutorial zur Benutzeroberfläche von Data Science Workspace [UI ](./train-evaluate-model-ui.md) oder im Tutorial [API-Tutorial](./train-evaluate-model-api.md) im Zug und zur Bewertung eines Modells. Dieses Tutorial bietet ein Beispiel für das Erstellen, Trainieren und Aktualisieren von Hyperparametern zur Feinabstimmung Ihres Modells.

>[!NOTE]
>
> Hyperparameter können nicht erlernt werden. Daher müssen sie vor Trainings-Läufen zugewiesen werden. Die Anpassung von Hyperparametern kann die Genauigkeit Ihres trainierten Modells ändern. Da die Optimierung eines Modells ein iterativer Prozess ist, können mehrere Trainings-Läufe erforderlich sein, bevor eine zufriedenstellende Bewertung erreicht wird.

## Modell bewerten {#score-a-model}

Der nächste Schritt bei der Erstellung und Veröffentlichung eines Modells besteht darin, Ihr Modell zu operationalisieren, um Einblicke aus dem Data Lake und dem Echtzeit-Kundenprofil zu gewinnen und zu nutzen.

Scoring in Data Science Workspace kann durch die Einspeisung von Eingabedaten in ein vorhandenes trainiertes Modell erreicht werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.

Um zu erfahren, wie Sie Ihr Modell bewerten können, besuchen Sie das Tutorial [UI-Tutorial](./score-model-ui.md) oder das [API-Tutorial](./score-model-api.md).

## Publish ein Modell mit Bewertungen als Dienst

Mit Data Science Workspace können Sie Ihr trainiertes Modell als Dienst veröffentlichen. Dadurch können Benutzer in Ihrer Organisation Daten bewerten, ohne eigene Modelle erstellen zu müssen.

Um zu erfahren, wie Sie ein Modell als Dienst veröffentlichen, besuchen Sie das Tutorial [UI-Tutorial](./publish-model-service-ui.md) oder das [API-Tutorial](./publish-model-service-api.md).

### Planen automatisierter Schulungen für einen Dienst

Nachdem Sie ein Modell als Dienst veröffentlicht haben, können Sie geplante Scoring- und Trainings-Läufe für Ihren maschinellen Lerndienst einrichten. Die Automatisierung des Trainings- und Scoring-Prozesses kann dazu beitragen, die Effizienz eines Dienstes im Laufe der Zeit zu erhalten und zu verbessern, indem Sie mit den Mustern in Ihren Daten Schritt halten. Besuchen Sie das Tutorial [Planen eines Modells im Data Science Workspace UI](./schedule-models-ui.md) -Tutorial.

>[!NOTE]
>
> Sie können ein Modell nur für automatisierte Schulungen und Auswertungen über die Benutzeroberfläche planen.

## Nächste Schritte {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] bietet die Tools und Ressourcen zum Erstellen, Auswerten und Verwenden maschineller Lernmodelle, um Datenprognosen und Einblicke zu generieren. Wenn Einblicke aus maschinellem Lernen in einen [!DNL Profile]-aktivierten Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile]-Datensätze erfasst, die dann mit [!DNL Adobe Experience Platform Segmentation Service] segmentiert werden können.

Da Profil- und Zeitreihendaten erfasst werden, entscheidet das Echtzeit-Kundenprofil automatisch, diese Daten über einen kontinuierlichen Prozess, der Streaming-Segmentierung genannt wird, ein- oder auszuschließen, bevor sie mit vorhandenen Daten zusammengeführt und die Vereinigungsansicht aktualisiert wird. So können Sie sofort Berechnungen durchführen und Entscheidungen treffen, um Kunden bei der Interaktion mit Ihrer Marke erweiterte, individuelle Erlebnisse bereitzustellen.

In der Anleitung zum [Anreichern des Echtzeit-Kundenprofils mit Einblicken aus maschinellem Lernen](./enrich-profile.md) erfahren Sie mehr darüber, wie Sie Einblicke aus maschinellem Lernen nutzen können.
