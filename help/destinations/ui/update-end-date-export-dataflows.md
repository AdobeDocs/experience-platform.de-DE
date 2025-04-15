---
title: Aktualisieren des Enddatums von Datenflüssen zum Datensatzexport (Aktion erforderlich bis zum 1. Mai 2025)
type: Tutorial
hide: true
hidefromtoc: true
description: Erfahren Sie, wie Sie das Enddatum für Datensatzexport-Datenflüsse mit dem aktuellen Enddatum 1. Mai 2025 aktualisieren.
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Aktualisieren des Enddatums von Datenflüssen zum Datensatzexport (Aktion erforderlich bis zum 1. Mai 2025)

>[!IMPORTANT]
>
>Die Aktionselemente auf dieser Seite gelten, wenn Ihr Unternehmen Datensatz-Exportdatenflüsse vor der Experience Platform-Version vom September 2024 eingerichtet hat.

## Was geschieht?

In [ Experience Platform-Version vom September 2024 ](/help/release-notes/latest/latest.md#destinations) die Option zum Festlegen eines `endTime` für den Export von Datensatzdatenflüssen eingeführt. Adobe hat außerdem das standardmäßige Enddatum 1. Mai 2025 für alle Datensatzexport-Datenflüsse eingeführt, die (*der Version vom September 2024) erstellt*. Diese Datenflüsse zeigen derzeit eine Meldung ähnlich der unten gezeigten an.

![Benutzeroberflächenbenachrichtigung über die Notwendigkeit, das Enddatum des Datensatzexport-Datenflusses zu aktualisieren.](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**Aktionselement**: Für jeden dieser Datenflüsse müssen Sie das Enddatum manuell aktualisieren, bevor es abläuft. Andernfalls werden Ihre Exporte angehalten. Verwenden Sie die Experience Platform-Benutzeroberfläche, um zu ermitteln, welche Datenflüsse am 1. Mai 2025 beendet werden sollen.

## Warum werde ich benachrichtigt?

Für Ihre Organisation wurden aktive Datenflüsse für den Datensatzexport mit dem Enddatum 1. Mai 2025 ermittelt.

## Verwenden der Benutzeroberfläche zum Aktualisieren des Enddatums

Verwenden Sie die Experience Platform-Benutzeroberfläche, um Datenflüsse mit dem Enddatum 1. Mai 2025 zu identifizieren und sie auf ein zukünftiges Datum zu aktualisieren.

### Ermitteln der Datenflüsse, die aktualisiert werden müssen

Navigieren Sie zu **Ziele > Durchsuchen** und suchen Sie in der Spalte **Datentyp** nach **Datensätze**, wie unten dargestellt. Wählen Sie die gewünschten Datenflüsse aus, um sie zu überprüfen.

![Datenflüsse für den Datensatzexport, die auf der Registerkarte Durchsuchen hervorgehoben sind.](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### Enddatum der Datenflüsse aktualisieren

So aktualisieren Sie das Enddatum von Datenflüssen:

1. Wählen Sie in den Datenflüssen, die Sie im vorherigen Schritt zur Überprüfung ausgewählt haben, **Datensätze exportieren**.
   ![Das Steuerelement zum Exportieren von Datensätzen ist auf der Registerkarte „Durchsuchen“ hervorgehoben.](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. Fahren Sie im Workflow mit dem Schritt **Planung** fort und wählen Sie **Zeitplan bearbeiten**.
   ![Steuerung „Zeitplan bearbeiten“ im Schritt „Planung“ hervorgehoben.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. Wählen Sie ein gewünschtes Enddatum nach dem 1. Mai 2025 aus und klicken Sie auf **Speichern**.
   ![Im Planungsschritt hervorgehobenes Steuerelement „Enddatum auswählen“](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. Fahren Sie mit dem Ende des Workflows fort und speichern Sie die Aktualisierungen.

Ausführliche Informationen zum Planungsschritt finden Sie im Tutorial [Exportieren von Datensätzen in der Benutzeroberfläche](/help/destinations/api/export-datasets.md#scheduling).

## Verwenden der API zum Aktualisieren des Enddatums

### Ermitteln der Datenflüsse, die aktualisiert werden müssen

### Enddatum der Datenflüsse aktualisieren
