---
title: End-to-End-Workflow der KI/ML-Datenpipeline-Anreicherung
description: Verwenden Sie Cloud-basierte Notebooks für maschinelle Lernumgebungen, um ein Modell für Schulung und Bewertung mit Tendenzwerten zu erstellen, das Abonnementkonversionen aus Adobe Experience Platform-Daten vorhersagt.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# End-to-End-Workflow zur Anreicherung von KI/ML-Daten

Verwenden Sie Data Distiller, um Ihre Pipelines für maschinelles Lernen mit hochwertigen Kundenerlebnisdaten anzureichern, die in Adobe Experience Platform erfasst und kuratiert wurden.

Dieses Dokument enthält eine Reihe von Cloud-basierten Notebooks für die maschinelle Lernumgebung, die einen durchgängigen Workflow demonstrieren. Der Workflow verwendet Ihre bevorzugten Tools für maschinelles Lernen, um benutzerdefinierte Datenmodelle zu erstellen, die Ihre Marketing-Anwendungsfälle mit Experience Platform-Daten unterstützen.

Dieser Workflow erfordert die Verwendung [!DNL Python] Notebooks in Ihren Umgebungen für maschinelles Lernen. Eine Anleitung für die ersten Schritte mit diesen [!DNL Python]-Notebooks finden Sie in den jeweiligen Readme-Dateien.

Bevor Sie mit diesem Handbuch fortfahren, führen Sie die Schritte aus, die unter [Übersicht über KI-/ML-Feature-Pipelines](./overview.md) beschrieben sind, um die Verwendung der in diesem Anwendungsfall für KI-/ML-Feature-Pipelines verwendeten Python-Beispielnotebooks zu aktivieren.

## Cloud-Notebooks für maschinelles Lernen {#cmle-notebooks}

Der End-to-End-Workflow kann basierend auf den Services, die zur Implementierung des Workflows verwendet werden, in drei große Phasen unterteilt werden.

- Die anfängliche Untersuchung und Vorbereitung von Experience Platform-Daten beruht auf Experience Platform-Services.
- Das Modell-Training und die Bewertung nutzt Tools in Ihrer Cloud-basierten ML-Umgebung. Zu den gängigen Optionen für ML-Plattformen gehören: Databricks ML, AWS Sagemaker, DataRobot usw.
- Die erneute Aufnahme von Scores in Experience Platform und die auf diesen Scores basierende Erstellung und Aktivierung von Code-basierten Zielgruppen würden wiederum auf Experience Platform-Services angewiesen sein.

Alle diese Phasen können jedoch in einem oder mehreren Notebooks aus Ihrer ML-Umgebung ausgeführt werden, ohne dass der Anwender den Kontext zwischen Experience Platform und seinen Cloud-basierten ML-Tools wechseln muss.

Die typischen Schritte dieses durchgängigen Arbeitsablaufs sind in eine Reihe modularer Notebooks unterteilt, die zusammengenommen die Schritte eines typischen maschinellen Lernprojekts mit Experience Platform-Daten darstellen. Dies erleichtert die Verwendung der Notebooks als Referenz für die Implementierung spezifischer Aktivitäten und die Auswahl und Anpassung von Code aus den entsprechenden Notebooks, um einen realen Anwendungsfall zu implementieren. In der Praxis kann ein Datenwissenschaftler ein einzelnes Notebook vorbereiten, das die End-to-End-Pipeline für sein ML-Projekt implementiert. Alternativ dazu kann ein Datenwissenschaftler den Beispielcode einfach anpassen, um Experience Platform-Daten abzufragen und in seiner ML-Umgebung verfügbar zu machen, bevor das Projekt weiterhin UI-basierte Funktionen in seiner ML-Plattform verwendet.

Die im verknüpften Repository enthaltenen Beispiel-Notebooks werden nachfolgend kurz beschrieben. Eine ausführliche Dokumentation zu jedem Notebook ist mit dem Code in den Notebooks selbst durchsetzt.

<!-- Below is the meat - the how to (but without links or details) -->

### Synthetische Daten generieren {#generate-synthetic-data}

Dieses Notebook enthält Code zum Generieren von Datensätzen mit synthetischen Profilen und Erlebnisereignissen in Ihrer Experience Platform, die zur Veranschaulichung des CMLE-Workflows verwendet werden.

### EDA und Feature mit Query Service {#eda-and-featurization-with-query-service}

Dieses Notebook enthält Beispiele für die explorative Analyse von Experience Platform-Datensätzen, die interaktive Abfragen über den Abfrage-Service von Experience Platform verwenden. Darauf folgen Beispiele für Featureabfragen zum Erstellen eines Trainings-Datensatzes für das Beispiel-Neigungs-Modell.

### Exportieren von Schulungsdaten {#export-training-data}

Dieses Notebook veranschaulicht den Export des Schulungsdatensatzes in den Cloud-Speicher, der von Ihren ML-Tools gelesen werden kann.

### Trainieren eines Tendenzmodells {#train-a-propensity-model}

Dieses Notebook veranschaulicht das Trainieren eines Tendenzmodells. Es setzt voraus, dass Databricks ML Ihre ML-Umgebung ist, wird jedoch generisch geschrieben (d. h. ohne starken Einsatz von Databricks-spezifischen Funktionen/APIs), sodass es an andere Plattformen angepasst werden kann.

### Bewerten des Tendenzmodells

Dieses Notebook veranschaulicht die Bewertung des trainierten Tendenzmodells, um einen Datensatz mit Tendenzwerten für jedes Experience Platform-Kundenprofil zu erstellen.

### Scores in AEP aufnehmen

Dieses kurze Notebook veranschaulicht die Aufnahme des Datensatzes mit Tendenz-Scores, um die Kundenprofile in AEP anzureichern.

### Erstellen und Aktivieren von Zielgruppen aus Code

Dieses Notebook zeigt, wie Benutzende aus den Bewertungen Zielgruppen erstellen und diese Zielgruppen über Experience Platform-Apps aus ihrem Notebook-Code aktivieren können.
