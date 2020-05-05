---
keywords: Experience Platform;score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Modellbewertung (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Modellbewertung (UI)

Die Bewertung in Adobe Experience Platform Data Science Workspace kann durch die Einspeisung von Eingabedaten in ein vorhandenes geschultes Modell erreicht werden. Die Bewertungsergebnisse werden dann als neuer Stapel in einem angegebenen Ausgabedataset gespeichert und angezeigt.

In diesem Lernprogramm werden die Schritte erläutert, die erforderlich sind, um ein Modell in der Benutzeroberfläche von Data Science Workspace zu bewerten.

## Erste Schritte

Um dieses Lernprogramm abzuschließen, müssen Sie Zugriff auf die Erlebnisplattform haben. Wenn Sie keinen Zugriff auf eine IMS-Organisation in Experience Platform haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Dieses Lernprogramm erfordert ein geschultes Modell. Wenn Sie kein ausgebildetes Modell haben, folgen Sie dem [Zug und bewerten Sie ein Modell im UI](./train-evaluate-model-ui.md) -Lernprogramm, bevor Sie fortfahren.

## Erstellen eines neuen Bewertungslaufs

Eine Bewertungsausführung wird mithilfe optimierter Konfigurationen aus einem zuvor abgeschlossenen und ausgewerteten Schulungslauf erstellt. Der Satz der optimalen Konfigurationen für ein Modell wird in der Regel durch Überprüfen der Evaluierungsmetriken für Schulungsabbrüche bestimmt.

1. Finden Sie den optimalen Schulungsablauf, um seine Konfigurationen für die Bewertung zu verwenden. Öffnen Sie den gewünschten Schulungslauf, indem Sie auf dessen Namen klicken.

2. Klicken Sie auf der **[!UICONTROL Evaluation]** Registerkarte &quot;Schulungslauf&quot;auf die **[!UICONTROL Score]** Schaltfläche oben rechts im Bildschirm. Dadurch wird ein neuer Arbeitsablauf *zum Ausführen der* Auswertung initiiert.
   ![](../images/models-recipes/score/training_run_overview.png)

3. Wählen Sie den Dataset für die Eingabebewertung aus und klicken Sie auf **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_input.png)

4. Wählen Sie den Ergebnisbewertungsdatensatz aus. Hierbei handelt es sich um den dedizierten Ausgabedatensatz, in dem die Bewertungsergebnisse gespeichert werden. Bestätigen Sie Ihre Auswahl und klicken Sie auf **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_results.png)

5. Im letzten Schritt im Workflow werden Sie aufgefordert, Ihre Bewertungsausführung zu konfigurieren. Diese Konfigurationen werden vom Modell für die Bewertungsausführung verwendet.
Beachten Sie, dass Sie geerbte Parameter, die bei der Modellerstellung festgelegt wurden, nicht entfernen können. Sie können nicht geerbte Parameter bearbeiten oder wiederherstellen, indem Sie die Dublette auf den Wert klicken oder auf das Symbol zum Zurücksetzen klicken, während Sie den Mauszeiger über den Eintrag halten.
   ![](../images/models-recipes/score/configuration.png)
Überprüfen Sie die Bewertungskonfigurationen und bestätigen Sie sie und klicken Sie auf , **[!UICONTROL Finish]** um die Bewertungsausführung zu erstellen und auszuführen. Sie werden auf die Registerkarte *Scoring Runs* weitergeleitet, und der neue Scoring Run zeigt den Status an.
   ![](../images/models-recipes/score/scoring_runs_tab.png)
Bei einer Bewertungsausführung wird einer der vier folgenden Status angezeigt: Ausstehend, Abgeschlossen, Fehlgeschlagen oder Wird ausgeführt und werden automatisch aktualisiert. Fahren Sie mit dem nächsten Schritt fort, wenn der Status &quot;Abgeschlossen&quot;oder &quot;Fehlgeschlagen&quot;lautet.

## Ansichten-Bewertungsergebnisse

1. Suchen Sie nach dem für die Bewertungsausführung verwendeten Schulungslauf und klicken Sie auf den Namen, um die **[!UICONTROL Evaluation]** Seite Ansicht.

2. Klicken Sie oben auf der Bewertungsseite für die Schulungslaufausführung auf die **[!UICONTROL Scoring Runs]** Registerkarte, um eine Liste der vorhandenen Testläufe Ansicht. Klicken Sie auf die Punktliste, um die Ansicht in der rechten Spalte zu erhalten.
   ![](../images/models-recipes/score/view_details.png)

3. Wenn die ausgewählte Bewertungsausführung den Status &quot;Abgeschlossen&quot;oder &quot;Fehlgeschlagen&quot;hat, ist der in der rechten Spalte gefundene **[!UICONTROL View Activity Logs]** Link aktiv. Klicken Sie auf den Link zur Ansicht oder laden Sie die Ausführungsprotokolle herunter. Wenn eine Bewertungsausführung fehlgeschlagen ist, können die Ausführungsprotokolle nützliche Informationen zur Ermittlung des Fehlerursprungs liefern.
   ![](../images/models-recipes/score/activity_logs.png)

4. Klicken Sie auf **[!UICONTROL Preview Scoring Results Dataset]** den Link in der rechten Spalte. Sie können eine Vorschau des Ausgabedatasets aus der Bewertungsausführung sehen.
   ![](../images/models-recipes/score/preview_results.png)

5. Klicken Sie für den vollständigen Ergebnissatz auf den **[!UICONTROL Scoring Results Dataset]** Link in der rechten Spalte.

## Nächste Schritte

Dieses Lernprogramm begleitet Sie durch die Schritte zum Erfassen von Daten mithilfe eines geschulten Modells im Data Science Workspace. Befolgen Sie das Lernprogramm zum [Veröffentlichen eines Modells als Dienst in der Benutzeroberfläche](./publish-model-service-ui.md) , damit Benutzer in Ihrem Unternehmen Daten bewerten können, indem sie einfachen Zugriff auf einen maschinellen Lerndienst bieten.
