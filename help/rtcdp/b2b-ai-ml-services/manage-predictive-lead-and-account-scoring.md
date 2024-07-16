---
title: Prädiktive Lead- und Kontobewertung in Real-Time CDP B2B verwalten
type: Documentation
description: Dieses Dokument enthält Informationen zur Verwaltung der prädiktiven Lead- und Kontoauswertungsfunktion in der Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 4%

---

# Prädiktive Lead- und Kontobewertung in Adobe Real-time Customer Data Platform, B2B Edition verwalten

>[!NOTE]
>
>Nur Benutzer mit der Berechtigung B2B AI verwalten können Bewertungsziele erstellen, ändern und löschen.

Dieses Tutorial führt Sie durch die Schritte zum Verwalten der Bewertungsziele des prädiktiven Lead- und Kontoauswertungsdienstes. Score-Ziele können entweder für Personenprofile oder Kontoprofile festgelegt werden.

## Neues Ergebnis erstellen

Um eine neue Punktzahl zu erstellen, wählen Sie in der Seitenleiste die Option **[!UICONTROL Dienste]** und danach **[!UICONTROL Punktzahl erstellen]** aus.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

Der Bildschirm **[!UICONTROL Grundlegende Informationen]** wird angezeigt und fordert Sie auf, einen Profiltyp auszuwählen, einen Namen und eine optionale Beschreibung einzugeben. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

Der Bildschirm **[!UICONTROL Ziel definieren]** wird angezeigt. Wählen Sie den Dropdown-Pfeil und dann einen Zieltyp aus dem angezeigten Dropdown-Fenster aus.

![plas-select-a-target](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

Das Dialogfeld **[!UICONTROL Zielspezifikationen]** wird geöffnet. Wählen Sie den Dropdown-Pfeil aus und wählen Sie dann im angezeigten Dropdown-Fenster den Zielfeldnamen aus.

![plas-select-a-target-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

Die Auswahl **[!UICONTROL Zielbedingungen]** wird angezeigt. Wählen Sie den Dropdown-Pfeil und dann die Bedingung aus dem angezeigten Dropdown-Fenster aus.

![plas-target-specifics-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

Das Feld **[!UICONTROL Zielwert]** wird angezeigt. Konfigurieren Sie als Nächstes Ihre [!UICONTROL Zielspezifikationen]. Wählen Sie das Bedienfeld [!UICONTROL Feldwert eingeben] aus und geben Sie Ihren Zielwert ein.

>[!NOTE]
>
>Es können mehrere Zielwerte hinzugefügt werden.

![plas-target-specifics-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Um weitere Felder hinzuzufügen, wählen Sie **[!UICONTROL Feld hinzufügen]** aus.

![plas-target-specifics-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Um den Prognosezeitrahmen zu konfigurieren, wählen Sie den Dropdown-Pfeil aus und wählen Sie dann den gewünschten Zeitrahmen aus.

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

Die ausgewählte Zusammenführungsrichtlinie bestimmt, wie die Feldwerte eines Personenprofils ausgewählt werden. Wählen Sie mithilfe des Dropdown-Pfeils Ihre gewünschte Zusammenführungsrichtlinie aus und wählen Sie dann **[!UICONTROL Beenden]** aus.

Das Dialogfeld **[!UICONTROL Scoring setup is complete]** wird angezeigt, in dem bestätigt wird, dass die neue Punktzahl erstellt wurde. Wählen Sie **[!UICONTROL OK]** aus.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Es kann bis zu 24 Stunden dauern, bis jeder Scoring-Prozess abgeschlossen ist.

Sie werden zur Registerkarte **[!UICONTROL Dienste]** zurückgeleitet, wo Sie die neue Punktzahl sehen können, die in der Liste der Bewertungen erstellt wurde.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Wählen Sie die Punktzahl aus, um Details und zusätzliche Informationen zu den letzten Ausführungsdetails anzuzeigen.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Ausführlichere Informationen zu den Fehlercodes, die unter den letzten Ausführungsdetails angezeigt werden, finden Sie im Abschnitt [Lead AI Pipeline-Fehlercodes](#leads-ai-pipeline-error-codes) in diesem Dokument.

## Ergebnis bearbeiten

Um eine Punktzahl zu bearbeiten, wählen Sie auf der Registerkarte **[!UICONTROL Dienste]** eine Punktzahl aus und klicken Sie auf der rechten Seite des Bildschirms im Bereich mit den zusätzlichen Details auf **[!UICONTROL Bearbeiten]** .

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

Das Dialogfeld **[!UICONTROL Instanz bearbeiten]** wird angezeigt, in dem Sie die Beschreibung für das Ergebnis bearbeiten können. Nehmen Sie Ihre Änderungen vor und wählen Sie **[!UICONTROL Speichern]** aus.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>Die Punktkonfiguration kann nicht geändert werden, da dies die Umschulung und Neubewertung von Triggern zur Folge hat. Dies entspricht dem Löschen der Punktzahl und dem Erstellen einer neuen Punktzahl. Um die Konfiguration der Punktzahl zu bearbeiten, müssen Sie diese Punktzahl klonen oder eine neue Punktzahl erstellen.

Sie werden zur Registerkarte **[!UICONTROL Dienste]** zurückgeleitet. Wählen Sie die Punktzahl aus, um die aktualisierten Beschreibungsdetails im Bedienfeld mit zusätzlichen Details auf der rechten Seite des Bildschirms anzuzeigen.

## Klonen einer Punktzahl

Um eine Punktzahl zu klonen, wählen Sie auf der Registerkarte **[!UICONTROL Dienste]** eine Punktzahl aus und wählen Sie im Bereich &quot;Zusätzliche Details&quot;auf der rechten Seite des Bildschirms die Option **[!UICONTROL Klonen]** aus.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

Der Bildschirm **[!UICONTROL Grundlegende Informationen]** wird angezeigt. Der Profiltyp, der Name und die Beschreibung werden aus dem ursprünglichen Ergebnis geklont. Ändern Sie diese Details und wählen Sie **[!UICONTROL Weiter]** aus.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

Der Bildschirm **[!UICONTROL Ziel definieren]** wird angezeigt. Füllen Sie den Zielabschnitt wie bei der Erstellung eines neuen Punkts aus und wählen Sie **[!UICONTROL Beenden]** aus.

Sie werden zur Registerkarte **[!UICONTROL Dienste]** zurückgeleitet, wo Sie das neu geklonte Ergebnis in der Liste sehen können.

>[!NOTE]
>
>Der Abschnitt **[!UICONTROL Definieren Sie Ihr Ziel]** wird nicht aus dem ursprünglichen Ergebnis geklont.

## Löschen eines Punkts

Um eine Punktzahl zu löschen, wählen Sie auf der Registerkarte **[!UICONTROL Dienste]** eine Punktzahl aus und klicken Sie auf der rechten Seite des Bildschirms im Bereich mit den zusätzlichen Details auf **[!UICONTROL Löschen]** .

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

Das Bestätigungsdialogfeld **[!UICONTROL Dokumentation löschen]** wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus.

![plas-delete-score-validation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>Wenn Sie die Punktzahl-Definition löschen, werden auch alle prognostizierten Werte für das Personenprofil oder Kontoprofil gelöscht, nicht jedoch die für die Punktzahl-Definition erstellte Feldergruppe. Die Feldergruppe bleibt im Datenmodell &quot;verwaist&quot;.

Sie werden zur Registerkarte **[!UICONTROL Dienste]** zurückgeleitet, auf der die Punktzahl nicht mehr in der Liste angezeigt wird.

## Führt AI-Pipeline-Fehlercodes aus

| Fehler-Code | Fehlermeldung |
| --- | --- |
| 401 | FEHLER 401. Leads AI-Pipeline gestoppt: Nicht genügend gültige Konten für die Kontobewertung. Anzahl Konten: {} |
| 402 | FEHLER 402. Leads AI-Pipeline angehalten: Nicht genügend gültige Kontakte für die Kontaktscoring. Anzahl der Kontakte: {}. |
| 403 | FEHLER 403. Leads AI-Pipeline angehalten: nicht genügend Aktivitätsvolumen für Modellschulungen. Anzahl der Ereignisse: {}. |
| 404 | FEHLER 404. Leads AI-Pipeline angehalten: Nicht genügend Konversionen für Modellschulungen. Zählung der Konversionen: {}. |
| 405 | FEHLER 405. Leads AI-Pipeline angehalten: Aktivität zu sparsam für eine gültige Modellschulung. Nur {} Prozent der Konten weisen Aktivitäten auf. |
| 406 | FEHLER 406. Leads AI-Pipeline angehalten: Aktivität zu sparsam für eine gültige Modellschulung. Nur {} Prozent der Kontakte haben Aktivität. |
| 407 | FEHLER 407. Leads AI-Pipeline angehalten: Die Aktivitätstypen für Scoring-Daten stimmen nicht mit den Trainings-Daten überein. |
| 408 | FEHLER 408. Die Leads-AI-Pipeline wurde angehalten: Die fehlende Rate ist zu hoch für Aktivitätsfunktionen. Fehlende Rate: {}. |
| 409 | FEHLER 409. Leads AI-Pipeline gestoppt: Testauc ist zu niedrig. Prüfung: {}. |
| 410 | FEHLER 410. Leads AI-Pipeline gestoppt: Test-auc ist nach der Parameteroptimierung zu niedrig. Prüfung: {}. |
| 411 | FEHLER 411. Leads AI-Pipeline angehalten: Trainings-Daten verfügen nicht über genügend Konversionen, um ein zuverlässiges Modell zu erstellen. Konversionen: {}. |
| 412 | FEHLER 412. Leads AI-Pipeline angehalten: Testdaten haben keine Konversion zur Berechnung von AUC-ROC. |

| Warn-/Info-Code | Nachricht |
| --- | --- |
| 100 | INFO 100. Führt AI-Qualitätsprüfung durch: Die Anzahl der Konten lautet: {}. |
| 101 | INFO 101. Führt eine KI-Qualitätsprüfung durch: Die Anzahl der Kontakte lautet: {}. |
| 102 | INFO 102. Führt eine KI-Qualitätsprüfung durch: Die Anzahl der Möglichkeiten lautet: {}. |
| 103 | INFO 103. Führt eine KI-Qualitätsprüfung durch: Testauc ist gering. Parameteroptimierung starten. Testauc: {}. |
| 200 | WARNUNG 200. Führt AI-Qualitätsprüfung durch: Die fehlende Rate von firmografischen Funktionen lautet: {}. |
| 201 | WARNUNG 201. Führt eine KI-Qualitätsprüfung durch: Die fehlende Rate von Aktivitätsfunktionen lautet: {}. |

## Nächste Schritte

In diesem Tutorial können Sie jetzt erfolgreich Bewertungen erstellen und verwalten. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Prädiktives Lead- und Konto-Scoring](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Überwachen von prädiktiven Lead- und Kontobewertungsaufträgen](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
