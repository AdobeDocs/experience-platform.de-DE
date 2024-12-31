---
keywords: Experience Platform;Modell für maschinelles Lernen;Data Science Workspace;beliebte Themen;Erstellen und Veröffentlichen eines Modells
solution: Experience Platform
title: Erstellen und Verwenden eines Publish-Modells für maschinelles Lernen
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

Im folgenden Handbuch werden die Schritte beschrieben, die zum Erstellen und Veröffentlichen eines Modells für maschinelles Lernen erforderlich sind. Jeder Abschnitt enthält eine Beschreibung Ihrer Vorgänge sowie einen Link zur Benutzeroberfläche und zur API-Dokumentation, in der Sie die beschriebenen Schritte ausführen können.

## Erste Schritte

Bevor Sie mit diesem Tutorial beginnen, müssen Sie folgende Voraussetzungen erfüllen:

- Zugriff auf [!DNL Adobe Experience Platform]. Wenn Sie in [!DNL Experience Platform] keinen Zugriff auf eine Organisation haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

- Alle Data Science Workspace-Tutorials verwenden das Luma-Tendenzmodell. Um diesem Schritt folgen zu können, müssen Sie die [Luma-Tendenzmodell-Schemata und Datensätze“ erstellt ](./create-luma-data.md).

### Daten untersuchen und Schemata verstehen

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Datensätze]** aus, um alle vorhandenen Datensätze aufzulisten und den Datensatz auszuwählen, den Sie untersuchen möchten. In diesem Fall sollten Sie den Datensatz **Luma Web Data** auswählen.

![Luma-Web-Datensatz auswählen](../images/models-recipes/model-walkthrough/luma-dataset.png)

Die Seite Datensatzaktivität wird geöffnet. Dort werden Informationen zu Ihrem Datensatz aufgelistet. Sie können oben rechts **[!UICONTROL Vorschau des Datensatzes]** auswählen, um Beispieldatensätze zu untersuchen. Sie können auch das Schema für den ausgewählten Datensatz anzeigen.

![Vorschau von Luma-Web-Daten](../images/models-recipes/model-walkthrough/preview-dataset.png)

Wählen Sie den Schema-Link in der rechten Leiste aus. Ein Pop-up wird angezeigt, in dem Sie den Link unter **[!UICONTROL Schemaname]** auswählen. Dadurch wird das Schema in einer neuen Registerkarte geöffnet.

![Vorschau des Luma-Web-Datenschemas](../images/models-recipes/model-walkthrough/preview-schema.png)

Sie können die Daten mit dem bereitgestellten Notebook zur explorativen Datenanalyse (EDA) weiter untersuchen. Dieses Notebook kann verwendet werden, um Muster in den Luma-Daten zu verstehen, die Datenplausibilität zu überprüfen und die relevanten Daten für das prädiktive Tendenzmodell zusammenzufassen. Weitere Informationen zur explorativen Datenanalyse finden Sie in der [EDA-Dokumentation](../jupyterlab/eda-notebook.md).

## Erstellen des Luma-Neigungsrezepts {#author-your-model}

Eine Hauptkomponente des [!DNL Data Science Workspace]-Lebenszyklus umfasst das Authoring von Rezepten und Modellen. Das Luma-Tendenzmodell ist so konzipiert, dass es eine Vorhersage darüber liefert, ob Kunden eine hohe Neigung haben, ein Produkt von Luma zu kaufen.

Um das Luma-Tendenzmodell zu erstellen, wird die Rezept-Builder-Vorlage verwendet. Rezepte sind die Grundlage für ein Modell, da sie Algorithmen für maschinelles Lernen und Logik enthalten, die zur Lösung spezifischer Probleme entwickelt wurden. Rezepte ermöglichen es Ihnen, das maschinelle Lernen in Ihrem Unternehmen zu demokratisieren, sodass andere Benutzer auf ein Modell für unterschiedliche Anwendungsfälle zugreifen können, ohne Code zu schreiben.

Befolgen Sie das Tutorial [Erstellen eines Modells mit JupyterLab-](../jupyterlab/create-a-model.md)&quot;, um das Rezept für das Luma-Tendenzmodell zu erstellen, das in nachfolgenden Tutorials verwendet wird.

## Rezept aus externen Quellen importieren und verpacken (*optional*)

Wenn Sie ein Rezept für die Verwendung in Data Science Workspace importieren und verpacken möchten, müssen Sie Ihre Quelldateien in eine Archivdatei packen. Tutorial [Packen von Quelldateien in ein ](./package-source-files-recipe.md)&quot;. In diesem Tutorial erfahren Sie, wie Sie Quelldateien in ein Rezept packen. Dies ist die Voraussetzung für den Import eines Rezepts in Data Science Workspace. Sobald das Tutorial abgeschlossen ist, erhalten Sie ein Docker-Image in einer Azure Container Registry zusammen mit der entsprechenden Bild-URL, d. h. eine Archivdatei.

Diese Archivdatei kann verwendet werden, um ein Rezept in Data Science Workspace zu erstellen, indem der Import-Workflow für Rezepte mithilfe des [UI-Workflows](./import-packaged-recipe-ui.md) oder des [API-Workflows](./import-packaged-recipe-api.md).

## Modell trainieren und bewerten {#train-and-evaluate-your-model}

Nachdem Ihre Daten vorbereitet und ein Rezept fertig ist, können Sie Ihr Modell für maschinelles Lernen weiter erstellen, trainieren und auswerten. Wenn Sie den Rezept-Builder verwenden, sollten Sie Ihr Modell bereits trainiert, bewertet und bewertet haben, bevor Sie es in ein Rezept verpacken.

Mit der Data Science Workspace-Benutzeroberfläche und der API können Sie Ihr Rezept als Modell veröffentlichen. Darüber hinaus können Sie bestimmte Aspekte Ihres Modells weiter präzisieren, z. B. das Hinzufügen, Entfernen und Ändern von Hyperparametern.

### Modell erstellen

Weitere Informationen zum Erstellen eines Modells mithilfe der Benutzeroberfläche finden Sie im Abschnitt Trainieren und Bewerten eines Modells im Data Science Workspace [UI-Tutorial](./train-evaluate-model-ui.md) oder [API-Tutorial](./train-evaluate-model-api.md). In diesem Tutorial erhalten Sie ein Beispiel für das Erstellen, Trainieren und Aktualisieren von Hyperparametern zur Feinabstimmung des Modells.

>[!NOTE]
>
> Hyperparameter können nicht erlernt werden, daher müssen sie vor Trainings-Läufen zugewiesen werden. Durch die Anpassung von Hyperparametern kann sich die Genauigkeit des trainierten Modells ändern. Da die Optimierung eines Modells ein iterativer Prozess ist, können mehrere Trainings-Läufe erforderlich sein, bevor eine zufriedenstellende Bewertung erreicht wird.

## Bewerten eines Modells {#score-a-model}

Der nächste Schritt beim Erstellen und Veröffentlichen eines Modells besteht darin, Ihr Modell zu operationalisieren, um Einblicke aus dem Data Lake und dem Echtzeit-Kundenprofil zu bewerten und zu nutzen.

Die Bewertung in Data Science Workspace kann durch Einspeisung von Eingabedaten in ein bestehendes trainiertes Modell erzielt werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.

Um zu erfahren, wie Sie Ihr Modell bewerten, besuchen Sie das Tutorial [UI-](./score-model-ui.md) oder [API](./score-model-api.md).

## Publish hat ein Modell als Service bewertet

Mit Data Science Workspace können Sie Ihr trainiertes Modell als Service veröffentlichen. So können Benutzer in Ihrem Unternehmen Daten bewerten, ohne eigene Modelle erstellen zu müssen.

Informationen zum Veröffentlichen eines Modells als Service finden Sie im [UI-Tutorial](./publish-model-service-ui.md) oder [API-Tutorial](./publish-model-service-api.md).

### Planen automatisierter Schulungen für einen Service

Nachdem Sie ein Modell als Service veröffentlicht haben, können Sie geplante Scoring- und Trainings-Läufe für Ihren Service für maschinelles Lernen einrichten. Die Automatisierung des Trainings- und Bewertungsprozesses kann dazu beitragen, die Effizienz eines Service im Laufe der Zeit zu erhalten und zu verbessern, indem Muster in Ihren Daten beibehalten werden. Besuchen Sie das Tutorial [Planen eines Modells in der Data Science Workspace](./schedule-models-ui.md)-Benutzeroberfläche.

>[!NOTE]
>
> Sie können ein Modell nur für automatisiertes Training und Scoring über die Benutzeroberfläche planen.

## Nächste Schritte {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] bietet die Tools und Ressourcen zum Erstellen, Auswerten und Verwenden von Modellen für maschinelles Lernen, um Datenvorhersagen und Erkenntnisse zu generieren. Wenn Einblicke aus maschinellem Lernen in einen [!DNL Profile]-aktivierten Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile] aufgenommen, die dann mithilfe von [!DNL Adobe Experience Platform Segmentation Service] segmentiert werden können.

Bei der Aufnahme von Profil- und Zeitreihendaten entscheidet das Echtzeit-Kundenprofil mithilfe des fortlaufenden Prozesses namens Streaming-Segmentierung automatisch, ob diese Daten in Segmente eingeschlossen oder von ihnen ausgeschlossen werden, bevor sie mit vorhandenen Daten zusammengeführt und die Vereinigungsansicht aktualisiert werden. So können Sie Berechnungen sofort durchführen und Entscheidungen treffen, um Ihren Kunden bei der Interaktion mit Ihrer Marke optimierte, individuelle Erlebnisse zu bieten.

Besuchen Sie das Tutorial [Anreicherung von Echtzeit-Kundenprofilen mit Einblicken aus maschinellem Lernen](./enrich-profile.md), um mehr darüber zu erfahren, wie Sie Einblicke aus maschinellem Lernen nutzen können.
