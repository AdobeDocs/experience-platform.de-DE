---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutorials zu Data Science Workspace
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 18%

---


# [!DNL Data Science Workspace] tutorials

Adobe Experience Platform [!DNL Data Science Workspace] uses machine learning and artificial intelligence to create insights from your data. Integrated into Adobe Experience Platform, [!DNL Data Science Workspace] helps you make predictions using your content and data assets across Adobe solutions. Datenwissenschaftler aller Qualifikationsstufen verfügen über ausgereifte, benutzerfreundliche Tools, die eine schnelle Entwicklung, Schulung und Abstimmung von Rezepten für maschinelles Lernen unterstützen – all die Vorteile der KI-Technologie, ohne die Komplexität.

Um mehr zu erfahren, lesen Sie zunächst [Data Science Workspace – Überblick](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

Die [!DNL Sensei Machine Learning] API bietet Datenwissenschaftlern einen Mechanismus zur Organisation und Verwaltung von Dienstleistungen für maschinelles Lernen, von der Algorithmusüberwachung über Experimente bis zur Dienstbereitstellung.

**Die folgenden API-Entwicklerhandbücher stehen zur Verfügung:**
- [Motoren](../data-science-workspace/api/engines.md) - Erfahren Sie, wie Sie Ihre [!DNL Docker] Registrierung nachschlagen, eine Engine erstellen, eine Feature-Pipeline-Engine erstellen, die Informationen für eine Engine abrufen, eine Engine aktualisieren und eine Engine löschen können.
- [MLInstances (Rezepte)](../data-science-workspace/api/mlinstances.md) - Erfahren Sie, wie Sie eine MLInstanz erstellen, die Informationen für eine MLInstanz abrufen, eine MLInstance aktualisieren und eine MLInstance löschen.
- [Experimente](../data-science-workspace/api/experiments.md) - Erfahren Sie, wie Sie ein Experiment erstellen, Informationen zu Experimenten oder Experimenten abrufen, ein Experiment aktualisieren und ein Experiment löschen können.
- [Modelle](../data-science-workspace/api/models.md) - Erfahren Sie, wie Sie Ihr eigenes Modell registrieren, die Informationen für ein Modell abrufen, ein Modell aktualisieren, ein Modell löschen, eine neue Transkodierung für ein Modell erstellen und die Details eines transkodierten Modells abrufen.
- [MLServices](../data-science-workspace/api/mlservices.md) - Erfahren Sie, wie Sie einen MLService erstellen, die Informationen für einen MLService abrufen, einen MLService aktualisieren und einen MLService löschen.
- [Einblicke](../data-science-workspace/api/insights.md) - Erfahren Sie, wie Sie Informationen zu einem Insight abrufen, einen neuen Model Insight hinzufügen und eine Liste von Standardmetriken für Algorithmen abrufen können.

Weitere Informationen und die erforderlichen Werte für die Ausführung von CRUD-Operationen mit der Sensei Machine Learning API finden Sie im Handbuch [Erste Schritte](../data-science-workspace/api/getting-started.md).

## How to use [!DNL JupyterLab] Notebooks

[!DNL JupyterLab] ist eine Web-basierte Benutzeroberfläche für [!DNL Project Jupyter] und ist eng in Adobe Experience Platform integriert. It provides an interactive development environment for data scientists to work with [!DNL Jupyter notebooks], code, and data. This document provides an overview of [!DNL JupyterLab] and its features as well as instructions to perform common actions.

**Dieses Handbuch hilft Ihnen:**
- Greifen Sie auf die [!DNL JupyterLab] Benutzeroberfläche zu und verstehen Sie sie.
- Machen Sie sich mit den Codezellen und den verfügbaren Kerneln in [!DNL JupyterLab]vertraut.
- Machen Sie sich mit der GPU- und Speicherserverkonfiguration in [!DNL Python]/R vertraut.
- Lesen und Abfrage von [!DNL Platform] Daten mit Notebooks.
- Machen Sie sich mit den Einschränkungen für Notebook-Daten vertraut.

Weitere Informationen finden Sie im [JupyterLab-Benutzerhandbuch](../data-science-workspace/jupyterlab/overview.md).

## Quelldateien für das Erstellen von [!DNL Docker] Rezepten packen

Mit einem [!DNL Docker] Bild können Sie eine Anwendung mit allen benötigten Teilen verpacken. Dazu gehören Bibliotheken und andere Abhängigkeiten in einem Paket. Das erstellte [!DNL Docker] Bild wird mit den Anmeldeinformationen, die Sie während des Arbeitsablaufs für die Skripterstellung erhalten haben, an den [!DNL Azure Container Registry] Empfänger gesendet.

**Dieses Lernprogramm hilft Ihnen:**
- Laden Sie die erforderlichen Voraussetzungen für die Rezepterstellung herunter.
- Verstehen Sie das [!DNL Docker] basierte Authoring von Modellen.
- Erstellen Sie ein [!DNL Docker] Bild für [!DNL Python], R, PySpark oder Scala ([!DNL Spark]).
- Abrufen der URL einer [!DNL Docker] Quelldatei.

Um mehr zu erfahren, folgen Sie den Quelldateien des [Pakets in einem Rezept-Lernprogramm](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Rezept importieren

>[!NOTE]
>
>
>Für dieses Lernprogramm ist eine URL für die [!DNL Docker] Quelldatei erforderlich. Rufen Sie die Quelldateien des [Pakets in einem Rezept-Lernprogramm](../data-science-workspace/models-recipes/package-source-files-recipe.md) auf, wenn Sie keine URL für die [!DNL Docker] Quelldatei haben.

Die Importrezeptschulungen bieten Einblicke in die Konfiguration und den Import eines gepackten Rezepts. By the end of this tutorial, you can create, train, and evaluate a Model in Adobe Experience Platform [!DNL Data Science Workspace].

**Dieses Lernprogramm hilft Ihnen:**
- Erstellen Sie einen Konfigurationssatz für ein Rezept.
- Importieren Sie ein [!DNL Docker] basiertes Rezept für [!DNL Python], R, PySpark oder Scala ([!DNL Spark]).

Weitere Informationen finden Sie im [UI-Tutorial](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) zum Importieren eines zusammengestellten Skripts oder im [API-Tutorial](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Schulung und Auswertung eines Modells

In Adobe Experience Platform [!DNL Data Science Workspace], a machine learning Model is created by incorporating an existing Recipe that is appropriate for the Model&#39;s intent. Anschließend wird das Modell trainiert und bewertet, um seine Effizienz und Wirksamkeit zu erhöhen; dazu werden die entsprechenden Hyperparameter fein abgestimmt. Rezepte sind wiederverwendbar; mit einem Rezept können also verschiedene Modelle erstellt und auf individuelle Zwecke zugeschnitten werden.

**Dieses Lernprogramm hilft Ihnen:**
- Erstellen Sie ein neues Modell.
- Erstellen Sie einen Schulungslauf für Ihr Modell.
- Testen Sie Ihre Modellschulungen.

Beginnen Sie zunächst mit einer Schulung und der Auswertung eines Modell- [API-Tutorials](../data-science-workspace/models-recipes/train-evaluate-model-api.md) oder des [UI-Tutorials](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Optimieren eines Modells mit dem Model Insight-Framework

The Model Insights Framework provides the data scientist with tools in Adobe Experience Platform [!DNL Data Science Workspace] to make quick and informed choices for optimal machine learning models based on experiments. Das Framework verbessert die Geschwindigkeit und Effektivität des Workflows für maschinelles Lernen und erhöht die Anwenderfreundlichkeit für Data Scientists. Dies geschieht durch Bereitstellung einer Standardvorlage für jeden maschinellen Lernalgorithmustyp, sodass sich Modelle verfeinern lassen. Das Endergebnis ermöglicht es Data Scientists und Citizen Data Scientists, bessere Entscheidungen zur Optimierung von Modellen ihrer Endkunden zu treffen.

**Dieses Lernprogramm hilft Ihnen:**
- Konfigurieren des Rezeptcodes.
- Definieren Sie benutzerspezifische Metriken.
- Verwenden Sie vordefinierte Evaluierungsmetriken und Visualisierungsdiagramme.

Beginnen Sie mit dem Tutorial zur [Optimierung eines Modells](../data-science-workspace/models-recipes/optimize-model.md).

## Modellbewertung

Scoring in Adobe Experience Platform [!DNL Data Science Workspace] can be achieved by feeding input data into an existing trained Model. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.

**Dieses Lernprogramm hilft Ihnen:**
- Neuen Scoring-Lauf erstellen.
- Ansicht der Bewertungsergebnisse.

To get started, follow the score a model [API tutorial](../data-science-workspace/models-recipes/score-model-api.md) or the [UI tutorial](../data-science-workspace/models-recipes/score-model-ui.md).

## Veröffentlichen eines Modells als Dienst

Adobe Experience Platform [!DNL Data Science Workspace] allows you to publish your Model as a service, enabling users within your IMS Organization to score data without the need for creating their own Models. Dies kann über die [!DNL Platform] Benutzeroberfläche oder die [!DNL Sensei Machine Learning] API erfolgen.

**Dieses Lernprogramm hilft Ihnen:**
- Veröffentlichen Sie ein Modell als Dienst.
- Ergebnisdaten mithilfe eines Dienstes über die [!DNL Platform] Servicegalerie .

Beginnen Sie zunächst mit dem [API-Tutorial](../data-science-workspace/models-recipes/publish-model-service-api.md) oder dem [Benutzeroberflächen-Tutorial](../data-science-workspace/models-recipes/publish-model-service-ui.md) zum Veröffentlichen eines Modells als Dienst.

## Planen von Schulungen und Bewertungen für ein Modell

Adobe Experience Platform [!DNL Data Science Workspace] allows you to set up scheduled scoring and training runs on a machine learning service. Die Automatisierung des Schulungs- und Bewertungsvorgangs kann dazu beitragen, die Effizienz eines Dienstes im Laufe der Zeit zu erhalten und zu verbessern, indem Sie die Muster in Ihren Daten beibehalten.

**Dieses Lernprogramm hilft Ihnen:**
- Geplantes Scoring konfigurieren
- Geplantes Training konfigurieren

Um zu beginnen, folgen Sie dem [Einplanen eines UI-Lehrgangs](../data-science-workspace/models-recipes/schedule-models-ui.md)für das Modell.

## Erstellen einer Feature-Pipeline

>[!NOTE]
>Derzeit sind Feature Pipelines nur über API verfügbar.

Mit der Adobe Experience Platform können Sie benutzerdefinierte Funktionenpipelines erstellen und erstellen, um die Funktionstechnik im Maßstab durchzuführen [!DNL Sensei Machine Learning Framework Runtime].

**Dieses Handbuch hilft Ihnen:**
- Implementieren Sie Feature Pipeline-Klassen.
- Erstellen Sie eine Feature Pipeline-Engine mit der API.

Weitere Informationen finden Sie im Tutorial zum [Erstellen einer Feature-Pipeline](../data-science-workspace/authoring/feature-pipeline.md).

## Erstellen einer [!DNL Real-Time Machine Learning] Anwendung (Alpha)

Eine Kombination aus nahtloser Berechnung auf dem Hub und dem [!DNL Edge] reduziert die Latenz, die traditionell bei der Erzielung übermäßig personalisierter Erlebnisse, die sowohl relevant als auch reaktionsfähig sind, eine entscheidende Rolle spielt. Daher [!DNL Real-time Machine Learning] bietet die Latenz für die synchrone Entscheidungsfindung unglaublich gering an. Beispiele sind das Rendering personalisierter Webseiteninhalte, das Aufdecken eines Angebots und Rabatte, um den Absturz zu reduzieren und gleichzeitig die Konversionen in einem Webstore zu erhöhen.

**Dieses Handbuch hilft Ihnen:**
- Verstehen Sie die [!DNL Real-time Machine Learning] Architektur.
- Verstehen Sie den [!DNL Real-time Machine Learning] Workflow.
- Machen Sie sich mit der aktuellen Funktionalität vertraut [!DNL Real-time Machine Learning].
- Sehen Sie sich die nächsten Schritte zum Erstellen Ihrer eigenen an [!DNL Real-time Machine Learning model].

Weitere Informationen finden Sie in der Übersicht über [maschinelles Lernen in Echtzeit](../data-science-workspace/real-time-machine-learning/home.md).