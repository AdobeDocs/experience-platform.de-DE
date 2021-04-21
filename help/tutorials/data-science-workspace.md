---
keywords: Experience Platform;Home;beliebte Themen;dsw;DSW
solution: Experience Platform
title: Tutorials zu Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace verwendet maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.
exl-id: 7cfd71b1-584f-4588-bbcd-bc42a08a0bc0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 19%

---

# [!DNL Data Science Workspace] Tutorials

Adobe Experience Platform [!DNL Data Science Workspace] verwendet maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. In Adobe Experience Platform integriert hilft [!DNL Data Science Workspace] Ihnen bei der Erstellung von Prognosen mit Ihren Inhalten und Daten-Assets in allen Adoben. Datenwissenschaftler aller Qualifikationsstufen verfügen über ausgereifte, benutzerfreundliche Tools, die eine schnelle Entwicklung, Schulung und Abstimmung von Rezepten für maschinelles Lernen unterstützen – all die Vorteile der KI-Technologie, ohne die Komplexität.

Um mehr zu erfahren, lesen Sie zunächst [Data Science Workspace – Überblick](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

Die [!DNL Sensei Machine Learning]-API bietet Datenwissenschaftlern einen Mechanismus zum Organisieren und Verwalten von maschinellen Lerndiensten, von der Algorithmusüberwachung über Experimente bis zur Dienstbereitstellung.

**Die folgenden API-Entwicklerhandbücher stehen zur Verfügung:**
- [Motoren](../data-science-workspace/api/engines.md)  - Erfahren Sie, wie Sie Ihre  [!DNL Docker] Registrierung nachschlagen, eine Engine erstellen, eine Feature-Pipeline-Engine erstellen, die Informationen für eine Engine abrufen, eine Engine aktualisieren und eine Engine löschen können.
- [MLInstances (recipes)](../data-science-workspace/api/mlinstances.md)  - Erfahren Sie, wie Sie eine MLInstance erstellen, die Informationen für eine MLInstanz abrufen, eine MLInstanz aktualisieren und eine MLInstance löschen.
- [Experimente](../data-science-workspace/api/experiments.md) : Erfahren Sie, wie Sie ein Experiment erstellen, Informationen zu Experimenten oder Experimenten abrufen, ein Experiment aktualisieren und ein Experiment löschen können.
- [Modelle](../data-science-workspace/api/models.md)  - Erfahren Sie, wie Sie Ihr eigenes Modell registrieren, die Informationen für ein Modell abrufen, ein Modell aktualisieren, ein Modell löschen, eine neue Transkodierung für ein Modell erstellen und die Details eines transkodierten Modells abrufen.
- [MLServices](../data-science-workspace/api/mlservices.md)  - Erfahren Sie, wie Sie einen MLService erstellen, die Informationen für einen MLService abrufen, einen MLService aktualisieren und einen MLService löschen.
- [Einblicke](../data-science-workspace/api/insights.md)  - Erfahren Sie, wie Sie Informationen zu einem Insight abrufen, einen neuen Model Insight hinzufügen und eine Liste von Standardmetriken für Algorithmen abrufen können.

Weitere Informationen und die erforderlichen Werte für die Ausführung von CRUD-Operationen mit der Sensei Machine Learning API finden Sie im Handbuch [Erste Schritte](../data-science-workspace/api/getting-started.md).

## Verwendung von [!DNL JupyterLab]-Notebooks

[!DNL JupyterLab] ist eine Web-basierte Benutzeroberfläche für [!DNL Project Jupyter] und ist eng in Adobe Experience Platform integriert. Es bietet eine interaktive Entwicklungs-Umgebung, mit der Datenwissenschaftler mit [!DNL Jupyter Notebooks], Code und Daten arbeiten können. In diesem Dokument erhalten Sie einen Überblick über [!DNL JupyterLab] und die zugehörigen Funktionen sowie Anweisungen zum Durchführen gemeinsamer Aktionen.

**Dieses Handbuch hilft Ihnen:**
- Greifen Sie auf die [!DNL JupyterLab]-Schnittstelle zu und verstehen Sie sie.
- Verstehen Sie die Codezellen und die verfügbaren Kernels innerhalb von [!DNL JupyterLab].
- Machen Sie sich mit der GPU- und Speicherserverkonfiguration in [!DNL Python]/R vertraut.

Weitere Informationen finden Sie im [JupyterLab-Benutzerhandbuch](../data-science-workspace/jupyterlab/overview.md).

## Datenzugriff in JupyterLab-Notebooks

Derzeit unterstützt JupyterLab in Data Science Workspace Notebooks für [!DNL Python], R, PySpark und Scala. Jeder unterstützte Kernel bietet native Funktionen, mit denen Sie Platform-Daten aus einem Datensatz in einem Notebook lesen können. Die Unterstützung für die Paginierung von Daten ist jedoch auf [!DNL Python]- und R-Notebooks beschränkt. Dieser Leitfaden konzentriert sich darauf, wie Sie mit JupyterLab-Notebooks auf Ihre Daten zugreifen können.

**Dieses Handbuch hilft Ihnen:**
- Plattformdaten mit Python-, R-, PySpark- oder Scala-Notebooks lesen, schreiben und schreiben.
- Machen Sie sich mit den Leseinschränkungen der einzelnen Notebooks vertraut.

Weitere Informationen finden Sie im Handbuch [JupyterLab für den Datenzugriffs-Entwickler für Notebooks](../data-science-workspace/jupyterlab/access-notebook-data.md)

## Quelldateien für [!DNL Docker] Rezept-Authoring verpacken

Mit einem [!DNL Docker]-Bild können Sie eine Anwendung mit allen erforderlichen Teilen verpacken. Dazu gehören Bibliotheken und andere Abhängigkeiten in einem Paket. Das erstellte [!DNL Docker]-Bild wird mit den Anmeldeinformationen, die Ihnen während des Rezepterstellungsarbeitsablaufs zur Verfügung gestellt wurden, an das [!DNL Azure Container Registry]-Bild gesendet.

**Dieses Lernprogramm hilft Ihnen:**
- Laden Sie die erforderlichen Voraussetzungen für die Rezepterstellung herunter.
- Verstehen Sie [!DNL Docker]-basiertes Modell-Authoring.
- Erstellen Sie ein [!DNL Docker]-Bild für [!DNL Python], R, PySpark oder Scala ([!DNL Spark]).
- Abrufen einer [!DNL Docker]-Quelldatei-URL.

Um mehr zu erfahren, folgen Sie den [Quelldateien des Pakets in einem Rezept-Lernprogramm](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Rezept importieren

>[!NOTE]
>
>Für dieses Lernprogramm ist eine [!DNL Docker]-Quelldatei-URL erforderlich. Gehen Sie zu den Quelldateien für das [Paket in ein Rezept-Lernprogramm](../data-science-workspace/models-recipes/package-source-files-recipe.md), wenn Sie keine [!DNL Docker]-Quelldatei-URL haben.

Die Importrezeptschulungen bieten Einblicke in die Konfiguration und den Import eines gepackten Rezepts. Am Ende dieses Lernprogramms können Sie ein Modell in Adobe Experience Platform [!DNL Data Science Workspace] erstellen, ausbilden und auswerten.

**Dieses Lernprogramm hilft Ihnen:**
- Erstellen Sie einen Konfigurationssatz für ein Rezept.
- Importieren Sie ein [!DNL Docker]-basiertes Rezept für [!DNL Python], R, PySpark oder Scala ([!DNL Spark]).

Weitere Informationen finden Sie im Abschnitt zum Importieren eines gepackten Skripts [UI-Tutorial](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) oder im [API-Tutorial](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Schulung und Auswertung eines Modells

In Adobe Experience Platform [!DNL Data Science Workspace] wird ein Modell für maschinelles Lernen erstellt, indem ein vorhandenes Rezept integriert wird, das für die Absicht des Modells geeignet ist. Anschließend wird das Modell trainiert und bewertet, um seine Effizienz und Wirksamkeit zu erhöhen; dazu werden die entsprechenden Hyperparameter fein abgestimmt. Rezepte sind wiederverwendbar; mit einem Rezept können also verschiedene Modelle erstellt und auf individuelle Zwecke zugeschnitten werden.

**Dieses Lernprogramm hilft Ihnen:**
- Erstellen Sie ein neues Modell.
- Erstellen Sie einen Schulungslauf für Ihr Modell.
- Testen Sie Ihre Modellschulungen.

Beginnen Sie zunächst mit der Schulung und der Auswertung eines Modells [API-Tutorials](../data-science-workspace/models-recipes/train-evaluate-model-api.md) oder des [UI-Tutorials](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Optimieren eines Modells mit dem Model Insight-Framework

Das Model Insights Framework bietet dem Datenwissenschaftler Werkzeuge in Adobe Experience Platform [!DNL Data Science Workspace], um schnell und fundierte Entscheidungen für optimale Modelle des maschinellen Lernens auf der Grundlage von Experimenten zu treffen. Das Framework verbessert die Geschwindigkeit und Effektivität des Workflows für maschinelles Lernen und erhöht die Anwenderfreundlichkeit für Data Scientists. Dies geschieht durch Bereitstellung einer Standardvorlage für jeden maschinellen Lernalgorithmustyp, sodass sich Modelle verfeinern lassen. Das Endergebnis ermöglicht es Data Scientists und Citizen Data Scientists, bessere Entscheidungen zur Optimierung von Modellen ihrer Endkunden zu treffen.

**Dieses Lernprogramm hilft Ihnen:**
- Konfigurieren des Rezeptcodes.
- Definieren Sie benutzerspezifische Metriken.
- Verwenden Sie vordefinierte Evaluierungsmetriken und Visualisierungsdiagramme.

Beginnen Sie mit dem Lernprogramm [Optimieren eines Modells](../data-science-workspace/models-recipes/optimize-model.md).

## Modellbewertung

Die Punktzahl in Adobe Experience Platform [!DNL Data Science Workspace] lässt sich erreichen, indem Eingabedaten in ein vorhandenes geschultes Modell eingespeist werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.

**Dieses Lernprogramm hilft Ihnen:**
- Neuen Scoring-Lauf erstellen.
- Ansicht der Bewertungsergebnisse.

Beginnen Sie mit dem Ergebnis eines Modells [API-Tutorials](../data-science-workspace/models-recipes/score-model-api.md) oder dem [UI-Tutorial](../data-science-workspace/models-recipes/score-model-ui.md).

## Veröffentlichen eines Modells als Dienst

Mit Adobe Experience Platform [!DNL Data Science Workspace] können Sie Ihr Modell als Dienst veröffentlichen, sodass Benutzer innerhalb Ihrer IMS-Organisation Daten bewerten können, ohne eigene Modelle erstellen zu müssen. Dies kann über die [!DNL Platform]-Benutzeroberfläche oder die [!DNL Sensei Machine Learning]-API erfolgen.

**Dieses Lernprogramm hilft Ihnen:**
- Veröffentlichen Sie ein Modell als Dienst.
- Daten mit einem Dienst über die [!DNL Platform] [!UICONTROL Dienstgalerie] bewerten.

Beginnen Sie zunächst mit dem [API-Tutorial](../data-science-workspace/models-recipes/publish-model-service-api.md) oder dem [Benutzeroberflächen-Tutorial](../data-science-workspace/models-recipes/publish-model-service-ui.md) zum Veröffentlichen eines Modells als Dienst.

## Planen von Schulungen und Bewertungen für ein Modell

Mit Adobe Experience Platform [!DNL Data Science Workspace] können Sie geplante Scoring- und Schulungsläufe auf einem maschinellen Lerndienst einrichten. Die Automatisierung des Schulungs- und Bewertungsvorgangs kann dazu beitragen, die Effizienz eines Dienstes im Laufe der Zeit zu erhalten und zu verbessern, indem Sie die Muster in Ihren Daten beibehalten.

**Dieses Lernprogramm hilft Ihnen:**
- Geplantes Scoring konfigurieren
- Geplantes Training konfigurieren

Um zu beginnen, folgen Sie den Anweisungen unter [Planen eines UI-Lehrgangs für das Modell](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Erstellen einer Feature-Pipeline

>[!NOTE]
>
>Derzeit sind Feature Pipelines nur über API verfügbar.

Mit Adobe Experience Platform können Sie benutzerdefinierte Funktionenpipelines erstellen und erstellen, um die Funktionstechnik im Maßstab bis zum [!DNL Sensei Machine Learning Framework Runtime] durchzuführen.

**Dieses Handbuch hilft Ihnen:**
- Implementieren Sie Feature Pipeline-Klassen.
- Erstellen Sie eine Feature Pipeline-Engine mit der API.

Weitere Informationen finden Sie im Lernprogramm für [Erstellen einer Feature-Pipeline](../data-science-workspace/authoring/feature-pipeline.md).

## Erstellen einer [!DNL Real-Time Machine Learning]-Anwendung (Alpha)

Eine Kombination aus nahtloser Berechnung auf dem Hub und dem [!DNL Edge] verringert die Latenz, die traditionell an der Bereitstellung hyperpersonalisierter Erlebnisse beteiligt ist, die sowohl relevant als auch reaktionsfähig sind, drastisch. [!DNL Real-time Machine Learning] bietet somit eine unglaublich niedrige Latenz für die synchrone Entscheidungsfindung. Beispiele sind das Rendering personalisierter Webseiteninhalte, das Aufdecken eines Angebots und Rabatte, um den Absturz zu reduzieren und gleichzeitig die Konversionen in einem Webstore zu erhöhen.

**Dieses Handbuch hilft Ihnen:**
- Verstehen Sie die [!DNL Real-time Machine Learning]-Architektur.
- Verstehen Sie den [!DNL Real-time Machine Learning]-Arbeitsablauf.
- Machen Sie sich mit der aktuellen Funktionalität von [!DNL Real-time Machine Learning] vertraut.
- Führen Sie die nächsten Schritte zum Erstellen Ihrer eigenen [!DNL Real-time Machine Learning model]-Variablen ein.

Weitere Informationen finden Sie unter [Übersicht über maschinelles Lernen in Echtzeit](../data-science-workspace/real-time-machine-learning/home.md).
