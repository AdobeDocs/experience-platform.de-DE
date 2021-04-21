---
keywords: Experience Platform;Modellbewertung;Arbeitsbereich für Datenwissenschaften;beliebte Themen;ui;Punktzahl;Ergebnisse bewerten
solution: Experience Platform
title: Modellbewertung in der Benutzeroberfläche des Arbeitsbereichs "Datenwissenschaften"
topic-legacy: tutorial
type: Tutorial
description: Scoring in Adobe Experience Platform Data Science Workspace kann durch Einspeisung von Eingabedaten in ein vorhandenes trainiertes Modell erreicht werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 32%

---

# Modellbewertung in der Benutzeroberfläche von Data Science Workspace

Die Punktzahl in Adobe Experience Platform [!DNL Data Science Workspace] lässt sich erreichen, indem Eingabedaten in ein vorhandenes geschultes Modell eingespeist werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.

In diesem Lernprogramm werden die Schritte erläutert, die erforderlich sind, um ein Modell in der [!DNL Data Science Workspace]-Benutzeroberfläche zu bewerten.

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich bitte an Ihren Systemadministrator, bevor Sie fortfahren.

Diese Anleitung setzt ein trainiertes Modell voraus. Wenn Sie noch kein trainiertes Modell haben, folgen Sie der Anleitung zum [Trainieren und Bewerten eines Modells in der Benutzeroberfläche](./train-evaluate-model-ui.md), bevor Sie fortfahren.

## Neuen Scoring-Lauf erstellen

Ein Scoring-Lauf wird mithilfe optimierter Konfigurationen aus einem zuvor abgeschlossenen und ausgewerteten Trainings-Lauf erstellt. Der Satz optimaler Konfigurationen für ein Modell wird in der Regel durch Überprüfen der Auswertungsmetriken für Trainings-Läufe bestimmt.

Finden Sie den optimalen Training-Lauf, um dessen Konfigurationen für das Scoring zu nutzen. Öffnen Sie dann die gewünschte Schulung, indem Sie den Hyperlink zum Namen auswählen.

![Auswählen des Schulungslaufs](../images/models-recipes/score/select-run.png)

Wählen Sie auf der Registerkarte **[!UICONTROL Evaluierung]** die Option **[!UICONTROL Ergebnis]** oben rechts im Bildschirm aus. Ein neuer Bewertungsarbeitsablauf beginnt.

![](../images/models-recipes/score/training_run_overview.png)

Wählen Sie den Eingabesortierungsdataset aus und wählen Sie **[!UICONTROL Weiter]**.

![](../images/models-recipes/score/scoring_input.png)

Wählen Sie den Ergebnis-Scoring-Datensatz aus. Hierbei handelt es sich um den dedizierten Ausgabedatensatz, in dem die Scoring-Ergebnisse gespeichert werden. Bestätigen Sie Ihre Auswahl und wählen Sie **[!UICONTROL Weiter]**.

![](../images/models-recipes/score/scoring_results.png)

Im letzten Schritt des Workflows werden Sie aufgefordert, Ihren Scoring-Lauf zu konfigurieren. Diese Konfigurationen werden vom Modell für die Bewertungsausführung verwendet.
Beachten Sie, dass Sie geerbte Parameter, die bei der Modellerstellung festgelegt wurden, nicht entfernen können. Sie können nicht geerbte Parameter bearbeiten oder wiederherstellen, indem Sie die Dublette auf den Wert klicken oder das Symbol zum Zurücksetzen auswählen, während Sie den Mauszeiger über den Eintrag halten.

![Konfiguration](../images/models-recipes/score/configuration.png)

Überprüfen Sie die Bewertungskonfigurationen und bestätigen Sie sie und wählen Sie **[!UICONTROL Fertigstellen]**, um die Bewertungsausführung zu erstellen und auszuführen. Sie werden zum Register **[!UICONTROL Scoring Runs]** weitergeleitet und die neue Scoring-Ausführung mit dem Status **[!UICONTROL Ausstehend]** wird angezeigt.

![Registerkarte &quot;Bewertungsläufe&quot;](../images/models-recipes/score/scoring_runs_tab.png)

Eine Bewertungsausführung kann mit einem der folgenden Status angezeigt werden:
- Ausstehend
- Abgeschlossen
- Fehlgeschlagen
- Wird ausgeführt

Status werden automatisch aktualisiert. Fahren Sie mit dem nächsten Schritt fort, wenn der Status **[!UICONTROL Complete]** oder **[!UICONTROL Fehlgeschlagen]** ist.

## Scoring-Ergebnisse anzeigen

Zur Ansicht der Bewertungsergebnisse wählen Sie einen Beginn aus.

![Auswählen des Schulungslaufs](../images/models-recipes/score/select-run.png)

Sie werden zu der Seite **[!UICONTROL Evaluierung]** umgeleitet. Wählen Sie oben auf der Seite zur Evaluierung der Schulungslaufausführung die Registerkarte **[!UICONTROL Bewertungsläufe]** aus, um eine Liste der vorhandenen Testläufe Ansicht.

![Bewertungsseite](../images/models-recipes/score/view_scoring_runs.png)

Wählen Sie anschließend einen Bewertungslauf aus, um die Ausführungsdetails Ansicht.

![Ausführungsdetails](../images/models-recipes/score/view_details.png)

Wenn der ausgewählte Bewertungslauf entweder den Status &quot;Complete&quot;oder &quot;Failure&quot;hat, wird der Link **[!UICONTROL Ansicht Aktivität Logs]** verfügbar gemacht. Wenn eine Bewertungsausführung fehlschlägt, können die Ausführungsprotokolle nützliche Informationen zur Bestimmung des Fehlerursprungs liefern. Um die Ausführungsprotokolle herunterzuladen, wählen Sie **[!UICONTROL Ansicht Aktivität Logs]**.

![Ansichten auswählen](../images/models-recipes/score/view_logs.png)

Das Popup **[!UICONTROL Ansicht Aktivität logs]** wird angezeigt. Wählen Sie eine URL aus, um die zugehörigen Protokolle automatisch herunterzuladen.

![](../images/models-recipes/score/activity_logs.png)

Sie haben auch die Möglichkeit, Ihre Bewertungsergebnisse Ansicht, indem Sie **[!UICONTROL Vorschau Scoring results dataset]** auswählen.

![Vorschauen auswählen](../images/models-recipes/score/view_results.png)

Eine Vorschau des Ausgabedatasets wird bereitgestellt.

![Vorschauen](../images/models-recipes/score/preview_results.png)

Wählen Sie für den vollständigen Satz der Bewertungsergebnisse den Link **[!UICONTROL Bewertungsergebnis-Datensatz]** in der rechten Spalte.

## Nächste Schritte

Dieses Lernprogramm begleitet Sie durch die Schritte, um Daten mit einem trainierten Modell in [!DNL Data Science Workspace] zu bewerten. Befolgen Sie die Anleitung zum [Publizieren eines Modells als Dienst in der Benutzeroberfläche](./publish-model-service-ui.md), damit Benutzer in Ihrer Organisation Daten bewerten können, indem sie einfachen Zugriff auf einen maschinellen Lerndienst erhalten.
