---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übungen zum Arbeitsbereich für Datenwissenschaften
topic: tutorial
translation-type: tm+mt
source-git-commit: 4d7d61660e6691d77701db1c089b84eee7f60974
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---


# Übungen zum Arbeitsbereich für Datenwissenschaften

Adobe Experience Platform Data Science Workspace verwendet maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in die Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen mithilfe Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen. Datenwissenschaftler aller Qualifikationsstufen verfügen über ausgereifte, benutzerfreundliche Werkzeuge, die eine schnelle Entwicklung, Ausbildung und Abstimmung von maschinellen Lernrezepten unterstützen - all die Vorteile der AI-Technologie, ohne die Komplexität.

Um mehr zu erfahren, lesen Sie zunächst die Übersicht über den [Data Science Workspace](../data-science-workspace/home.md).

## Sensei Machine Learning API

Die Sensei Machine Learning API bietet Datenwissenschaftlern einen Mechanismus zur Organisation und Verwaltung von Dienstleistungen des maschinellen Lernens, von Algorithmus-Onboarding über Experimentierungen bis hin zur Service-Bereitstellung.

**Die folgenden API-Entwicklerhandbücher stehen zur Verfügung:**
- [Motoren](../data-science-workspace/api/engines.md) - Erfahren Sie, wie Sie Ihre Docker-Registrierung nachschlagen, eine Engine erstellen, eine Feature-Pipeline-Engine erstellen, die Informationen für eine Engine abrufen, eine Engine aktualisieren und eine Engine löschen können.
- [MLInstances (Rezepte)](../data-science-workspace/api/mlinstances.md) - Erfahren Sie, wie Sie eine MLInstanz erstellen, die Informationen für eine MLInstanz abrufen, eine MLInstance aktualisieren und eine MLInstance löschen.
- [Experimente](../data-science-workspace/api/experiments.md) - Erfahren Sie, wie Sie ein Experiment erstellen, Informationen zu Experimenten oder Experimenten abrufen, ein Experiment aktualisieren und ein Experiment löschen können.
- [Modelle](../data-science-workspace/api/models.md) - Erfahren Sie, wie Sie Ihr eigenes Modell registrieren, die Informationen für ein Modell abrufen, ein Modell aktualisieren, ein Modell löschen, eine neue Transkodierung für ein Modell erstellen und die Details eines transkodierten Modells abrufen.
- [MLServices](../data-science-workspace/api/mlservices.md) - Erfahren Sie, wie Sie einen MLService erstellen, die Informationen für einen MLService abrufen, einen MLService aktualisieren und einen MLService löschen.
- [Einblicke](../data-science-workspace/api/insights.md) - Erfahren Sie, wie Sie Informationen zu einem Insight abrufen, einen neuen Model Insight hinzufügen und eine Liste von Standardmetriken für Algorithmen abrufen können.

Weitere Informationen und die erforderlichen Werte für die Ausführung von CRUD-Operationen mit der Sensei Machine Learning API finden Sie im Handbuch [Erste Schritte](../data-science-workspace/api/getting-started.md).

## Verwendung von JupyterLab-Notebooks

[!DNL JupyterLab] ist eine webbasierte Benutzeroberfläche für [!DNL Project Jupyter] und ist eng in die Adobe Experience Platform integriert. Es bietet eine interaktive Entwicklungs-Umgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, -Codes und -Daten arbeiten können. In diesem Dokument erhalten Sie einen Überblick über [!DNL JupyterLab] die Funktionen und Anweisungen zum Durchführen gemeinsamer Aktionen.

**Dieses Handbuch hilft Ihnen:**
- Greifen Sie auf die [!DNL JupyterLab] Benutzeroberfläche zu und verstehen Sie sie.
- Machen Sie sich mit den Codezellen und den verfügbaren Kerneln in [!DNL JupyterLab]vertraut.
- Machen Sie sich mit der GPU- und Speicherserverkonfiguration in Python/R vertraut.
- Lesen und Abfrage von [!DNL Platform] Daten mit Notebooks.
- Machen Sie sich mit den Einschränkungen für Notebook-Daten vertraut.

Weitere Informationen finden Sie im [JupyterLab-Benutzerhandbuch](../data-science-workspace/jupyterlab/overview.md).

## Quelldateien für das Erstellen von Dockerrezepten verpacken

Mit einem Docker-Bild können Sie eine Anwendung mit allen benötigten Teilen verpacken. Dazu gehören Bibliotheken und andere Abhängigkeiten in einem Paket. Das erstellte Docker-Bild wird mit den Anmeldeinformationen, die Sie während des Rezepterstellungsarbeitsablaufs erhalten haben, in die Azurblaue Container-Registrierung verschoben.

**Dieses Lernprogramm hilft Ihnen:**
- Laden Sie die erforderlichen Voraussetzungen für die Rezepterstellung herunter.
- Verstehen Sie das Docker-basierte Modell-Authoring.
- Erstellen Sie ein Docker-Bild für Python, R, PySpark oder Scala (Spark).
- Abrufen der URL der Docker-Quelldatei.

Um mehr zu erfahren, folgen Sie den Quelldateien des [Pakets in einem Rezept-Lernprogramm](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Rezept importieren

>[!NOTE]
>Für dieses Lernprogramm ist eine Docker-URL für die Quelldatei erforderlich. Besuchen Sie die Quelldateien des [Pakets in einem Rezept-Lernprogramm](../data-science-workspace/models-recipes/package-source-files-recipe.md) , wenn Sie keine Docker-Quelldatei-URL haben.

Die Importrezeptschulungen bieten Einblicke in die Konfiguration und den Import eines gepackten Rezepts. Am Ende dieses Lernprogramms können Sie ein Modell in Adobe Experience Platform Data Science Workspace erstellen, ausbilden und auswerten.

**Dieses Lernprogramm hilft Ihnen:**
- Erstellen Sie einen Konfigurationssatz für ein Rezept.
- Importieren Sie ein Docker-basiertes Rezept für Python, R, PySpark oder Scala (Spark).

Weitere Informationen finden Sie im [UI-Tutorial](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) zum Importieren eines zusammengestellten Skripts oder im [API-Tutorial](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Zugreifen und Auswerten eines Modells

In Adobe Experience Platform Data Science Workspace wird ein Modell für maschinelles Lernen erstellt, indem ein vorhandenes Rezept integriert wird, das für die Absicht des Modells geeignet ist. Anschließend wird das Modell trainiert und bewertet, um seine Betriebseffizienz und Wirksamkeit zu optimieren, indem die zugehörigen Hyperparameter präzisiert werden. Rezepte sind wiederverwendbar, d. h., mehrere Modelle können mit einem Rezept erstellt und auf spezifische Zwecke zugeschnitten werden.

**Dieses Lernprogramm hilft Ihnen:**
- Erstellen Sie ein neues Modell.
- Erstellen Sie einen Schulungslauf für Ihr Modell.
- Testen Sie Ihre Modellschulungen.

Beginnen Sie zunächst mit einer Schulung und der Auswertung eines Modell- [API-Tutorials](../data-science-workspace/models-recipes/train-evaluate-model-api.md) oder des [UI-Tutorials](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Optimieren eines Modells mit dem Model Insight-Framework

Das Model Insights Framework bietet dem Datenwissenschaftler Werkzeuge in Adobe Experience Platform Data Science Workspace, um auf der Grundlage von Experimenten schnell und fundierte Entscheidungen für optimale maschinelle Lernmodelle zu treffen. Der Rahmen wird die Geschwindigkeit und Effektivität des Arbeitsablaufs für maschinelles Lernen verbessern und die Benutzerfreundlichkeit von Datenwissenschaftlern verbessern. Dies geschieht durch Bereitstellung einer Standardvorlage für jeden maschinellen Lernalgorithmustyp, um die Modellverfeinerung zu unterstützen. Das Endergebnis ermöglicht es Datenwissenschaftlern und Bürgerdatenwissenschaftlern, bessere Modelloptimierungsentscheidungen für ihre Endkunden zu treffen.

**Dieses Lernprogramm hilft Ihnen:**
- Konfigurieren des Rezeptcodes.
- Definieren Sie benutzerspezifische Metriken.
- Verwenden Sie vordefinierte Evaluierungsmetriken und Visualisierungsdiagramme.

Beginnen Sie mit dem Tutorial zur [Optimierung eines Modells](../data-science-workspace/models-recipes/optimize-model.md).

## Modellbewertung

Die Auswertung im Data Science Workspace der Adobe Experience Platform kann durch die Einspeisung von Eingabedaten in ein vorhandenes geschultes Modell erreicht werden. Die Bewertungsergebnisse werden dann als neuer Stapel in einem angegebenen Ausgabedataset gespeichert und angezeigt.

**Dieses Lernprogramm hilft Ihnen:**
- Erstellen Sie einen neuen Bewertungslauf.
- Ansicht der Bewertungsergebnisse.

Beginnen Sie zunächst mit dem Ergebnis eines Modell- [API-Tutorials](../data-science-workspace/models-recipes/score-model-api.md) oder des [UI-Tutorials](../data-science-workspace/models-recipes/score-model-ui.md).

## Veröffentlichen eines Modells als Dienst

Adobe Experience Platform Data Science Workspace ermöglicht es Ihnen, Ihr Modell als Dienst zu veröffentlichen, sodass Benutzer innerhalb Ihrer IMS-Organisation Daten bewerten können, ohne eigene Modelle erstellen zu müssen. Dies kann über die [!DNL Platform] Benutzeroberfläche oder die Sensei Machine Learning API erfolgen.

**Dieses Lernprogramm hilft Ihnen:**
- Veröffentlichen Sie ein Modell als Dienst.
- Ergebnisdaten mithilfe eines Dienstes über die [!DNL Platform] Servicegalerie.

Beginnen Sie zunächst mit der Veröffentlichung eines Modells als Service- [API-Lernprogramm](../data-science-workspace/models-recipes/publish-model-service-api.md) oder dem [UI-Lernprogramm](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## Planen von Schulungen und Bewertungen für ein Modell

Mit Adobe Experience Platform Data Science Workspace können Sie planmäßige Scoring- und Schulungsabläufe auf einem maschinellen Lerndienst einrichten. Die Automatisierung des Schulungs- und Bewertungsvorgangs kann dazu beitragen, die Effizienz eines Dienstes im Laufe der Zeit zu erhalten und zu verbessern, indem Sie die Muster in Ihren Daten beibehalten.

**Dieses Lernprogramm hilft Ihnen:**
- Geplante Bewertung konfigurieren
- Planmäßige Schulungen konfigurieren

Um zu beginnen, folgen Sie dem [Einplanen eines UI-Lehrgangs](../data-science-workspace/models-recipes/schedule-models-ui.md)für das Modell.

## Erstellen einer Feature-Pipeline

>[!NOTE]
>Derzeit sind Feature Pipelines nur über API verfügbar.

Mit der Adobe Experience Platform können Sie benutzerdefinierte Funktionenpipelines erstellen und erstellen, um mithilfe der Sensei Machine Learning Framework Runtime umfangreiche Funktionen zu entwickeln.

**Dieses Handbuch hilft Ihnen:**
- Implementieren Sie Feature Pipeline-Klassen.
- Erstellen Sie eine Feature Pipeline-Engine mit der API.

Weitere Informationen finden Sie im Tutorial zum [Erstellen einer Feature-Pipeline](../data-science-workspace/authoring/feature-pipeline.md).

## Erstellen einer Echtzeit-Anwendung für maschinelles Lernen (Alpha)

Eine Kombination aus nahtloser Berechnung auf dem Hub und dem Edge verringert die Latenz, die traditionell bei der Bereitstellung übermäßig personalisierter Erlebnisse, die sowohl relevant als auch reaktionsfähig sind, eine entscheidende Rolle spielt. Das maschinelle Lernen in Echtzeit bietet somit eine unglaublich niedrige Latenz für synchrone Entscheidungen. Beispiele sind das Rendering personalisierter Webseiteninhalte, das Aufdecken eines Angebots und Rabatte, um den Absturz zu reduzieren und gleichzeitig die Konversionen in einem Webstore zu erhöhen.

**Dieses Handbuch hilft Ihnen:**
- Verstehen Sie die Architektur des maschinellen Lernens in Echtzeit.
- Machen Sie sich mit dem Arbeitsablauf für maschinelles Lernen in Echtzeit vertraut.
- Machen Sie sich mit den aktuellen Funktionen für maschinelles Lernen in Echtzeit vertraut.
- Sehen Sie sich die nächsten Schritte an, um ein eigenes Echtzeit-Modell für maschinelles Lernen zu erstellen.

Weitere Informationen finden Sie in der Übersicht über [maschinelles Lernen in Echtzeit](../data-science-workspace/real-time-machine-learning/home.md).