---
keywords: Experience Platform;Modellbewertung;Arbeitsbereich für Datenwissenschaften;beliebte Themen;ui;Punktzahl;Ergebnisse bewerten
solution: Experience Platform
title: Bewerten eines Modells (Benutzeroberfläche)
topic: tutorial
type: Tutorial
description: 'Scoring in Adobe Experience Platform Data Science Workspace kann durch Einspeisung von Eingabedaten in ein vorhandenes trainiertes Modell erreicht werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt. '
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 87%

---


# Bewerten eines Modells (Benutzeroberfläche)

Die Punktzahl in Adobe Experience Platform [!DNL Data Science Workspace] lässt sich erreichen, indem Eingabedaten in ein vorhandenes geschultes Modell eingespeist werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.

In diesem Lernprogramm werden die Schritte erläutert, die erforderlich sind, um ein Modell in der [!DNL Data Science Workspace]-Benutzeroberfläche zu bewerten.

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich bitte an Ihren Systemadministrator, bevor Sie fortfahren.

Diese Anleitung setzt ein trainiertes Modell voraus. Wenn Sie noch kein trainiertes Modell haben, folgen Sie der Anleitung zum [Trainieren und Bewerten eines Modells in der Benutzeroberfläche](./train-evaluate-model-ui.md), bevor Sie fortfahren.

## Neuen Scoring-Lauf erstellen

Ein Scoring-Lauf wird mithilfe optimierter Konfigurationen aus einem zuvor abgeschlossenen und ausgewerteten Trainings-Lauf erstellt. Der Satz optimaler Konfigurationen für ein Modell wird in der Regel durch Überprüfen der Auswertungsmetriken für Trainings-Läufe bestimmt.

1. Finden Sie den optimalen Training-Lauf, um dessen Konfigurationen für das Scoring zu nutzen. Öffnen Sie den gewünschten Trainings-Lauf, indem Sie auf dessen Namen klicken.

2. Klicken Sie auf dem Tab **[!UICONTROL Auswertung]** des Trainings-Laufs auf die Schaltfläche **[!UICONTROL Score]** oben rechts im Bildschirm. Dadurch wird ein neuer **Scoring ausführen**-Workflow initiiert.
   ![](../images/models-recipes/score/training_run_overview.png)

3. Wählen Sie den Eingabe-Scoring-Datensatz aus und klicken Sie auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/score/scoring_input.png)

4. Wählen Sie den Ergebnis-Scoring-Datensatz aus. Hierbei handelt es sich um den dedizierten Ausgabedatensatz, in dem die Scoring-Ergebnisse gespeichert werden. Bestätigen Sie Ihre Auswahl und klicken Sie auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/score/scoring_results.png)

5. Im letzten Schritt des Workflows werden Sie aufgefordert, Ihren Scoring-Lauf zu konfigurieren. Diese Konfigurationen werden vom Modell für den Scoring-Lauf verwendet.
Beachten Sie, dass Sie geerbte Parameter, die bei der Modellerstellung festgelegt wurden, nicht entfernen können. Sie können nicht geerbte Parameter bearbeiten oder wiederherstellen, indem Sie auf den Wert doppelklicken oder auf das Symbol zum Zurücksetzen klicken, während Sie mit dem Mauszeiger über den Eintrag fahren.
   ![](../images/models-recipes/score/configuration.png)
Überprüfen und bestätigen Sie die Scoring-Konfigurationen und klicken Sie auf **[!UICONTROL Fertig stellen]**, um den Scoring-Lauf zu erstellen und auszuführen. Sie werden zum Tab **[!UICONTROL Scoring-Läufe]** weitergeleitet; für den neuen Scoring-Lauf wird ein Status angezeigt.
   ![](../images/models-recipes/score/scoring_runs_tab.png)
Für einen Scoring-Lauf wird einer der vier folgenden Status angezeigt: „Ausstehend“, „Abgeschlossen“, „Fehlgeschlagen“ oder „Wird ausgeführt“. Die Status werden automatisch aktualisiert. Fahren Sie mit dem nächsten Schritt fort, wenn der Status „Abgeschlossen“ oder „Fehlgeschlagen“ lautet.

## Scoring-Ergebnisse anzeigen

1. Suchen Sie nach dem Trainings-Lauf, der für den Scoring-Lauf verwendet wurde, und klicken Sie auf dessen Namen, um die **[!UICONTROL Auswertungsseite]** anzuzeigen.

2. Klicken Sie oben auf der Auswertungsseite des Trainings-Laufs auf den Tab **[!UICONTROL Scoring-Läufe]**, um eine Liste der vorhandenen Scoring-Läufe anzuzeigen. Klicken Sie auf die Scoring-Liste, um in der rechten Spalte die entsprechenden Details anzuzeigen.
   ![](../images/models-recipes/score/view_details.png)

3. Wenn der ausgewählte Scoring-Lauf den Status „Abgeschlossen“ oder „Fehlgeschlagen“ aufweist, ist der Link **[!UICONTROL Aktivitätsprotokolle anzeigen]** in der rechten Spalte aktiv. Klicken Sie auf den Link, um die Ausführungsprotokolle anzuzeigen und herunterzuladen. Wenn ein Scoring-Lauf fehlgeschlagen ist, können die Ausführungsprotokolle nützliche Daten zur Ermittlung der Fehlerquelle enthalten.
   ![](../images/models-recipes/score/activity_logs.png)

4. Klicken Sie in der rechten Spalte auf den Link **[!UICONTROL Vorschau von Datensatz mit Scoring-Ergebnissen anzeigen]**. Sie können eine Vorschau des Ausgabedatensatzes des Scoring-Laufs anzeigen.
   ![](../images/models-recipes/score/preview_results.png)

5. Klicken Sie für den vollständigen Satz der Scoring-Ergebnisse auf den Link **[!UICONTROL Datensatz mit Scoring-Ergebnissen]** in der rechten Spalte.

## Nächste Schritte

Dieses Lernprogramm begleitet Sie durch die Schritte, um Daten mit einem trainierten Modell in [!DNL Data Science Workspace] zu bewerten. Befolgen Sie die Anleitung zum [Publizieren eines Modells als Dienst in der Benutzeroberfläche](./publish-model-service-ui.md), damit Benutzer in Ihrer Organisation Daten bewerten können, indem sie einfachen Zugriff auf einen maschinellen Lerndienst erhalten.
