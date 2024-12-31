---
keywords: Experience Platform; Bewerten eines Modells; Data Science Workspace; beliebte Themen; Benutzeroberfläche; Bewertungsdurchgang; Bewertungsergebnisse
solution: Experience Platform
title: Bewerten eines Modells in der Data Science Workspace-Benutzeroberfläche
type: Tutorial
description: Scoring in Adobe Experience Platform Data Science Workspace kann durch Einspeisung von Eingabedaten in ein vorhandenes trainiertes Modell erreicht werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 30%

---

# Bewerten eines Modells in der Data Science Workspace-Benutzeroberfläche

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Die Bewertung in Adobe Experience Platform [!DNL Data Science Workspace] kann durch Einspeisung von Eingabedaten in ein bestehendes trainiertes Modell erzielt werden. Scoring-Ergebnisse werden dann als neuer Batch in einem angegebenen Ausgabedatensatz gespeichert und angezeigt.

In diesem Tutorial werden die Schritte veranschaulicht, die zum Bewerten eines Modells in der [!DNL Data Science Workspace]-Benutzeroberfläche erforderlich sind.

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie in [!DNL Experience Platform] keinen Zugriff auf eine Organisation haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Diese Anleitung setzt ein trainiertes Modell voraus. Wenn Sie noch kein trainiertes Modell haben, folgen Sie der Anleitung zum [Trainieren und Auswerten eines Modells in der Benutzeroberfläche](./train-evaluate-model-ui.md), bevor Sie fortfahren.

## Neuen Scoring-Lauf erstellen

Ein Scoring-Lauf wird mithilfe optimierter Konfigurationen aus einem zuvor abgeschlossenen und ausgewerteten Trainings-Lauf erstellt. Der Satz optimaler Konfigurationen für ein Modell wird in der Regel durch Überprüfen der Auswertungsmetriken für Trainings-Läufe bestimmt.

Finden Sie den optimalen Training-Lauf, um dessen Konfigurationen für das Scoring zu nutzen. Öffnen Sie dann den gewünschten Trainings-Lauf, indem Sie den Hyperlink auswählen, der mit dem Namen verbunden ist.

![Trainings-Durchgang auswählen](../images/models-recipes/score/select-run.png)

Wählen Sie auf **[!UICONTROL Registerkarte]** Test **[!UICONTROL oben rechts]** Bildschirm die Option Score aus. Ein neuer Scoring-Workflow beginnt.

![](../images/models-recipes/score/training_run_overview.png)

Wählen Sie den Eingabe-Bewertungsdatensatz aus und klicken Sie auf **[!UICONTROL Weiter]**.

![](../images/models-recipes/score/scoring_input.png)

Wählen Sie den Ergebnis-Scoring-Datensatz aus. Hierbei handelt es sich um den dedizierten Ausgabedatensatz, in dem die Scoring-Ergebnisse gespeichert werden. Bestätigen Sie Ihre Auswahl und klicken Sie auf **[!UICONTROL Weiter]**.

![](../images/models-recipes/score/scoring_results.png)

Im letzten Schritt des Workflows werden Sie aufgefordert, Ihren Scoring-Lauf zu konfigurieren. Diese Konfigurationen werden vom Modell für den Scoring-Durchgang verwendet.
Beachten Sie, dass Sie keine übernommenen Parameter entfernen können, die bei der Modellerstellung festgelegt wurden. Sie können nicht vererbte Parameter bearbeiten oder zurücksetzen, indem Sie auf den Wert doppelklicken oder das Symbol „Zurücksetzen“ auswählen, während Sie den Mauszeiger über den Eintrag bewegen.

![Konfiguration](../images/models-recipes/score/configuration.png)

Prüfen und bestätigen Sie die Scoring-Konfigurationen und wählen Sie **[!UICONTROL Beenden]**, um den Scoring-Durchgang zu erstellen und auszuführen. Sie werden zur Registerkarte **[!UICONTROL Scoring-Durchgänge]** weitergeleitet und der neue Scoring-Durchgang mit dem Status **[!UICONTROL Ausstehend]** wird angezeigt.

![Registerkarte „Scoring-Durchgänge“](../images/models-recipes/score/scoring_runs_tab.png)

Ein Scoring-Durchgang kann mit einem der folgenden Status angezeigt werden:
- Ausstehend
- Abgeschlossen
- Fehlgeschlagen
- Läuft

Status werden automatisch aktualisiert. Fahren Sie mit dem nächsten Schritt fort, wenn der Status **[!UICONTROL Abgeschlossen]** oder **[!UICONTROL Fehlgeschlagen]** ist.

## Scoring-Ergebnisse anzeigen

Um die Bewertungsergebnisse anzuzeigen, wählen Sie zunächst einen Trainings-Lauf aus.

![Trainings-Durchgang auswählen](../images/models-recipes/score/select-run.png)

Sie werden zur Seite mit den Trainings-Läufen **[!UICONTROL Test]** weitergeleitet. Wählen Sie oben auf der Bewertungsseite für den Trainings-Durchgang die Registerkarte **[!UICONTROL Scoring-Durchgänge]** aus, um eine Liste der vorhandenen Scoring-Durchgänge anzuzeigen.

![Auswertungsseite](../images/models-recipes/score/view_scoring_runs.png)

Wählen Sie als Nächstes einen Scoring-Durchgang aus, um die Details des Durchgangs anzuzeigen.

![Ausführungsdetails](../images/models-recipes/score/view_details.png)

Wenn der ausgewählte Scoring-Durchgang den Status „Abgeschlossen“ oder „Fehlgeschlagen“ hat **[!UICONTROL wird der Link &quot;]** anzeigen“ zur Verfügung gestellt. Schlägt ein Scoring-Durchgang fehl, können die Ausführungsprotokolle nützliche Informationen zur Ermittlung der Fehlerursache liefern. Um die Ausführungsprotokolle herunterzuladen, wählen Sie **[!UICONTROL Aktivitätsprotokolle anzeigen]**.

![Protokolle anzeigen auswählen](../images/models-recipes/score/view_logs.png)

Das **[!UICONTROL Anzeigen von Aktivitätsprotokollen]** wird angezeigt. URL auswählen, um die zugehörigen Protokolle automatisch herunterzuladen.

![](../images/models-recipes/score/activity_logs.png)

Sie haben auch die Möglichkeit, Ihre Scoring-Ergebnisse anzuzeigen, indem Sie **[!UICONTROL Scoring-Ergebnisdatensatz in der Vorschau]**.

![Vorschauergebnisse auswählen](../images/models-recipes/score/view_results.png)

Eine Vorschau des Ausgabedatensatzes wird bereitgestellt.

![Vorschau der Ergebnisse](../images/models-recipes/score/preview_results.png)

Wählen Sie für den vollständigen Satz der Bewertungsergebnisse den **[!UICONTROL Datensatz für Bewertungsergebnisse]** in der rechten Spalte aus.

## Nächste Schritte

Dieses Tutorial führte Sie durch die Schritte zum Bewerten von Daten mithilfe eines trainierten Modells in [!DNL Data Science Workspace]. Befolgen Sie die Anleitung zum [Veröffentlichen eines Modells als Service in der Benutzeroberfläche](./publish-model-service-ui.md), damit Benutzer in Ihrer Organisation Daten bewerten können, indem sie einfachen Zugriff auf einen maschinellen Lerndienst erhalten.
