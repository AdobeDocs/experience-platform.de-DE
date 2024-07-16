---
keywords: Experience Platform; Modell bewerten; Data Science Workspace; beliebte Themen; ui; Scoring-Lauf; Scoring-Ergebnisse
solution: Experience Platform
title: Modell in der Benutzeroberfläche von Data Science Workspace bewerten
type: Tutorial
description: Scoring in Adobe Experience Platform Data Science Workspace kann durch Einspeisung von Eingabedaten in ein vorhandenes trainiertes Modell erreicht werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 31%

---

# Modell in der Benutzeroberfläche von Data Science Workspace bewerten

Scoring in Adobe Experience Platform [!DNL Data Science Workspace] kann erzielt werden, indem Eingabedaten in ein vorhandenes trainiertes Modell eingespeist werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.

In diesem Tutorial werden die Schritte erläutert, die zum Bewerten eines Modells in der Benutzeroberfläche von [!DNL Data Science Workspace] erforderlich sind.

## Erste Schritte

Um dieses Tutorial abzuschließen, müssen Sie Zugriff auf [!DNL Experience Platform] haben. Wenn Sie keinen Zugriff auf eine Organisation in [!DNL Experience Platform] haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Diese Anleitung setzt ein trainiertes Modell voraus. Wenn Sie noch kein trainiertes Modell haben, folgen Sie der Anleitung zum [Trainieren und Auswerten eines Modells in der Benutzeroberfläche](./train-evaluate-model-ui.md), bevor Sie fortfahren.

## Neuen Scoring-Lauf erstellen

Ein Scoring-Lauf wird mithilfe optimierter Konfigurationen aus einem zuvor abgeschlossenen und ausgewerteten Trainings-Lauf erstellt. Der Satz optimaler Konfigurationen für ein Modell wird in der Regel durch Überprüfen der Auswertungsmetriken für Trainings-Läufe bestimmt.

Finden Sie den optimalen Training-Lauf, um dessen Konfigurationen für das Scoring zu nutzen. Öffnen Sie dann den gewünschten Trainings-Lauf, indem Sie den Hyperlink auswählen, der an den Namen angehängt ist.

![Trainings-Lauf auswählen](../images/models-recipes/score/select-run.png)

Wählen Sie auf der Registerkarte für den Trainings-Lauf **[!UICONTROL Auswertung]** die Option **[!UICONTROL Score]** oben rechts im Bildschirm. Ein neuer Scoring-Workflow wird gestartet.

![](../images/models-recipes/score/training_run_overview.png)

Wählen Sie den Eingabe-Scoring-Datensatz und dann **[!UICONTROL Weiter]** aus.

![](../images/models-recipes/score/scoring_input.png)

Wählen Sie den Ergebnis-Scoring-Datensatz aus. Hierbei handelt es sich um den dedizierten Ausgabedatensatz, in dem die Scoring-Ergebnisse gespeichert werden. Bestätigen Sie Ihre Auswahl und wählen Sie **[!UICONTROL Weiter]** aus.

![](../images/models-recipes/score/scoring_results.png)

Im letzten Schritt des Workflows werden Sie aufgefordert, Ihren Scoring-Lauf zu konfigurieren. Diese Konfigurationen werden vom Modell für den Scoring-Lauf verwendet.
Beachten Sie, dass Sie geerbte Parameter, die während der Modellerstellung festgelegt wurden, nicht entfernen können. Sie können nicht vererbte Parameter bearbeiten oder wiederherstellen, indem Sie auf den Wert doppelklicken oder das Symbol zum Zurücksetzen auswählen, während Sie den Mauszeiger über den Eintrag bewegen.

![configuration](../images/models-recipes/score/configuration.png)

Überprüfen und bestätigen Sie die Scoring-Konfigurationen und wählen Sie **[!UICONTROL Beenden]** aus, um den Scoring-Lauf zu erstellen und auszuführen. Sie werden zur Registerkarte **[!UICONTROL Scoring-Läufe]** geleitet und der neue Scoring-Lauf mit dem Status **[!UICONTROL Ausstehend]** wird angezeigt.

Registerkarte ![Scoring-Läufe ](../images/models-recipes/score/scoring_runs_tab.png)

Ein Scoring-Lauf kann mit einem der folgenden Status angezeigt werden:
- Ausstehend
- Abgeschlossen
- Fehlgeschlagen
- Läuft

Status werden automatisch aktualisiert. Fahren Sie mit dem nächsten Schritt fort, wenn der Status **[!UICONTROL Complete]** oder **[!UICONTROL Failed]** lautet.

## Scoring-Ergebnisse anzeigen

Um Scoring-Ergebnisse anzuzeigen, wählen Sie zunächst einen Trainings-Lauf aus.

![Trainings-Lauf auswählen](../images/models-recipes/score/select-run.png)

Sie werden zur Seite mit den Trainings-Läufen **[!UICONTROL Auswertung]** weitergeleitet. Wählen Sie oben auf der Auswertungsseite für Trainings-Läufe die Registerkarte **[!UICONTROL Scoring-Läufe]** aus, um eine Liste der vorhandenen Scoring-Läufe anzuzeigen.

![Auswertungsseite](../images/models-recipes/score/view_scoring_runs.png)

Wählen Sie als Nächstes einen Scoring-Lauf aus, um die Ausführungsdetails anzuzeigen.

![run details](../images/models-recipes/score/view_details.png)

Wenn der ausgewählte Scoring-Lauf den Status &quot;Abgeschlossen&quot;oder &quot;Fehlgeschlagen&quot;aufweist, wird der Link **[!UICONTROL Aktivitätsprotokolle anzeigen]** verfügbar gemacht. Wenn ein Scoring-Lauf fehlschlägt, können die Ausführungsprotokolle nützliche Informationen zur Bestimmung des Fehlerurteils bereitstellen. Um die Ausführungsprotokolle herunterzuladen, wählen Sie **[!UICONTROL Aktivitätsprotokolle anzeigen]** aus.

![Protokoll anzeigen auswählen](../images/models-recipes/score/view_logs.png)

Das Popup **[!UICONTROL Aktivitätsprotokolle anzeigen]** wird angezeigt. Wählen Sie eine URL aus, um die zugehörigen Protokolle automatisch herunterzuladen.

![](../images/models-recipes/score/activity_logs.png)

Sie können auch Ihre Scoring-Ergebnisse anzeigen, indem Sie **[!UICONTROL Vorschau des Datensatz mit Scoring-Ergebnissen anzeigen]** auswählen.

![Vorschauergebnisse auswählen](../images/models-recipes/score/view_results.png)

Eine Vorschau des Ausgabedatasets wird bereitgestellt.

![Ergebnisse in der Vorschau anzeigen](../images/models-recipes/score/preview_results.png)

Wählen Sie für den vollständigen Satz der Scoring-Ergebnisse den Link **[!UICONTROL Datensatz mit Scoring-Ergebnissen]** in der rechten Spalte aus.

## Nächste Schritte

In diesem Tutorial haben Sie die Schritte zum Erfassen von Daten mithilfe eines trainierten Modells in [!DNL Data Science Workspace] durchlaufen. Befolgen Sie die Anleitung zum [Veröffentlichen eines Modells als Service in der Benutzeroberfläche](./publish-model-service-ui.md), damit Benutzer in Ihrer Organisation Daten bewerten können, indem sie einfachen Zugriff auf einen maschinellen Lerndienst erhalten.
