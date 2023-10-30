---
title: End-to-End-Workflow für die Anreicherung von AI-/ML-Data Pipeline
description: Verwenden Sie Cloud-basierte Notebook-Umgebungen für maschinelles Lernen, um eine Schulung zu erstellen und ein Tendenzmodell zu bewerten, das Abonnementkonversionen aus Adobe Experience Platform-Daten vorhersagt.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# End-to-End-Workflow für die Anreicherung der AI-/ML-Datenpipeline

Verwenden Sie Data Distiller, um Ihre Pipelines für maschinelles Lernen mit hochwertigen Kundenerlebnisdaten anzureichern, die in Adobe Experience Platform erfasst und kuratiert wurden.

Dieses Dokument bietet eine Reihe Cloud-basierter Notebook-Umgebungen für maschinelles Lernen, die einen durchgängigen Workflow demonstrieren. Der Workflow verwendet Ihre bevorzugten Tools für das maschinelle Lernen, um benutzerdefinierte Datenmodelle zu erstellen, die Ihre Marketing-Anwendungsfälle mit Experience Platform-Daten unterstützen.

Dieser Workflow erfordert die Verwendung von [!DNL Python] Notebooks in Ihren Umgebungen für maschinelles Lernen. Anweisungen für die ersten Schritte mit diesen [!DNL Python] Notebooks sind in ihren jeweiligen Readme-Dateien enthalten.

Bevor Sie mit diesem Handbuch fortfahren, führen Sie die Schritte aus, die im Abschnitt [Übersicht über KI/ML-Feature-Pipelines](./overview.md) , um die Verwendung der in dieser AI/ML-Feature-Pipeline verwendeten Python-Beispiel-Notebooks zu aktivieren.

## Notebooks mit der Cloud-Umgebung für maschinelles Lernen {#cmle-notebooks}

Der durchgängige Workflow kann auf der Basis der zur Workflow-Implementierung verwendeten Dienste in drei große Phasen unterteilt werden.

- Die erste Erforschung und Vorbereitung von Platform-Daten beruht auf Platform-Diensten.
- Modellschulung und -bewertung nutzt Tools in Ihrer Cloud-basierten ML-Umgebung. Zu den gebräuchlichen Optionen für ML-Plattformen zählen: Databricks ML, AWS Sagemaker, DataRobot usw.
- Wenn Sie Ergebnisse zurück in Platform erfassen und auf diesen Werten basierende code-basierte Zielgruppenerstellung und -aktivierung auf Grundlage dieser Bewertungen erneut auf Platform-Dienste zurücksetzen.

Alle diese Phasen können jedoch in einem oder mehreren Notebooks Ihrer ML-Umgebung ausgeführt werden, ohne dass der Benutzer zwischen Platform und seinen Cloud-basierten ML-Tools wechseln muss.

Die typischen Schritte dieses durchgängigen Workflows wurden in eine Reihe modularer Notebooks unterteilt, die zusammen die Schritte zeigen, die bei einem typischen maschinellen Lernprojekt mit Platform-Daten erforderlich sind. Dies erleichtert die Verwendung der Notebooks als Referenz für die Implementierung spezifischer Aktivitäten sowie die Auswahl und Anpassung von Code aus den entsprechenden Notebooks, um einen realen Anwendungsfall zu implementieren. In der Praxis kann ein Datenwissenschaftler ein einzelnes Notebook vorbereiten, das die End-to-End-Pipeline für sein ML-Projekt implementiert. Alternativ kann ein Datenwissenschaftler den Beispielcode einfach anpassen, um Platform-Daten abzufragen und sie in seiner ML-Umgebung verfügbar zu machen, bevor er das Projekt fortsetzt, um UI-basierte Funktionen in seiner ML-Plattform zu verwenden.

Die im verknüpften Repository enthaltenen Beispiel-Notebooks werden unten kurz beschrieben. Die detaillierte Dokumentation für jedes Notebook ist mit dem Code in den Notebooks selbst verknüpft.

<!-- Below is the meat - the how to (but without links or details) -->

### Generieren synthetischer Daten {#generate-synthetic-data}

Dieses Notebook bietet Code zum Generieren von Datensätzen synthetischer Profile und Erlebnisereignisse in Ihrer Plattform, die zur Veranschaulichung des CMLE-Workflows verwendet werden.

### EDA und Funktionen mit Query Service {#eda-and-featurization-with-query-service}

Dieses Notebook enthält Beispiele für die explorative Analyse von Platform-Datensätzen mithilfe interaktiver Abfragen über Platform Query Service. Diesen werden Beispiele für Funktionsabfragen folgen, um einen Trainings-Datensatz für das Beispiel-Tendenzmodell zu erstellen.

### Exportieren von Trainings-Daten {#export-training-data}

Dieses Notebook veranschaulicht den Export des Trainings-Datensatzes in Cloud-Speicher, der von Ihren ML-Tools gelesen werden kann.

### Tendenzmodell trainieren {#train-a-propensity-model}

Dieses Notebook zeigt das Training eines Tendenzmodells. Dabei wird von Databricks ML als Ihre ML-Umgebung ausgegangen, aber allgemein geschrieben (d. h. ohne starken Einsatz von Databricks-spezifischen Funktionen/APIs), sodass sie an andere Plattformen angepasst werden kann.

### Tendenzmodell bewerten

Dieses Notebook veranschaulicht die Auswertung des trainierten Tendenzmodells, um einen Datensatz mit Tendenzwerten für jedes Platform-Kundenprofil zu erstellen.

### Aufnehmen von Bewertungen in AEP

Dieses kurze Notebook veranschaulicht die Erfassung des Datensatzes mit Tendenzwerten zur Anreicherung der Kundenprofile in AEP.

### Erstellen und Aktivieren von Zielgruppen aus Code

Dieses Notebook veranschaulicht, wie Benutzer Zielgruppen aus den Bewertungen erstellen und diese Zielgruppen über Platform-Apps aus ihrem Notebook-Code aktivieren können.
