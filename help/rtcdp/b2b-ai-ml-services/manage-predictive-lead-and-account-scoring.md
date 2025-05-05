---
title: Verwalten von prädiktivem Lead- und Konto-Scoring in Real-Time CDP B2B
type: Documentation
description: Dieses Dokument enthält Informationen zum Verwalten der Funktion zum prädiktiven Lead- und Konto-Scoring in Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 4%

---

# Verwalten von prädiktivem Lead- und Konto-Scoring in Adobe Real-time Customer Data Platform, B2B edition

>[!NOTE]
>
>Nur Benutzer mit der Berechtigung B2B-KI verwalten können Score-Ziele erstellen, ändern und löschen.

Dieses Tutorial führt Sie durch die Schritte zum Verwalten der Score-Ziele des Predictive Lead and Account Scoring-Service. Score-Ziele können entweder für das Personenprofil oder das Kontoprofil festgelegt werden.

## Neuen Score erstellen

Um einen neuen Score zu erstellen, wählen Sie in der Seitenleiste **[!UICONTROL Dienste]** aus und klicken Sie auf **[!UICONTROL Score erstellen]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

Der Bildschirm **[!UICONTROL Grundlegende Informationen]** wird angezeigt, in dem Sie aufgefordert werden, einen Profiltyp auszuwählen, einen Namen und eine optionale Beschreibung einzugeben. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

Der **[!UICONTROL „Ziel definieren]** wird angezeigt. Wählen Sie den Dropdown-Pfeil und dann im angezeigten Dropdown-Fenster einen Zieltyp aus.

![plas-select-a-goal](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

Das **[!UICONTROL Zieldetails]** wird geöffnet. Wählen Sie den Dropdown-Pfeil und dann aus dem angezeigten Dropdown-Fenster den Namen des Zielfelds aus.

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

Die **[!UICONTROL Zielbedingungen]** wird angezeigt. Wählen Sie den Dropdown-Pfeil und dann im angezeigten Dropdown-Fenster Bedingung aus.

![plas-goal-specific-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

Das Feld **[!UICONTROL Zielwert]** wird angezeigt. Konfigurieren Sie anschließend Ihre [!UICONTROL Zieldetails]. Wählen Sie das Bedienfeld [!UICONTROL Feldwert eingeben] und geben Sie Ihren Zielwert ein.

>[!NOTE]
>
>Es können mehrere Zielwerte hinzugefügt werden.

![plas-goal-specific-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Um zusätzliche Felder hinzuzufügen, wählen Sie **[!UICONTROL Feld hinzufügen]** aus.

![plas-goal-specific-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Um den Prognosezeitrahmen zu konfigurieren, klicken Sie auf den Dropdown-Pfeil und wählen Sie dann Ihren gewünschten Zeitrahmen aus.

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

Die ausgewählte Zusammenführungsrichtlinie bestimmt, wie die Feldwerte eines Personenprofils ausgewählt werden. Wählen Sie mithilfe des Dropdown-Pfeils Ihre gewünschte Zusammenführungsrichtlinie aus und klicken Sie dann auf **[!UICONTROL Beenden]**.

Das **[!UICONTROL Scoring-Einrichtung ist abgeschlossen]** erscheint und bestätigt, dass der neue Score erstellt wurde. Klicken Sie **[!UICONTROL OK]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Es kann bis zu 24 Stunden dauern, bis jeder Scoring-Prozess abgeschlossen ist.

Sie kehren zur Registerkarte **[!UICONTROL Services]** zurück, auf der Sie den neuen Score in der Liste der Score-Werte sehen können.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Wählen Sie die Punktzahl aus, um Details und zusätzliche Informationen zum letzten Durchgang anzuzeigen.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Weitere Informationen zu den Fehler-Codes, die unter den Details des letzten Durchgangs angezeigt werden, finden Sie im Abschnitt zu [Leads-KI-Pipeline-Fehler](#leads-ai-pipeline-error-codes) in diesem Dokument.

## Punktzahl bearbeiten

Um einen Score zu bearbeiten, wählen Sie einen Score auf der Registerkarte **[!UICONTROL Services]** und wählen Sie **[!UICONTROL Bearbeiten]** im Bedienfeld „Zusätzliche Details“ auf der rechten Seite des Bildschirms aus.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

Das **[!UICONTROL Instanz bearbeiten]** wird angezeigt, in dem Sie die Beschreibung für den Score bearbeiten können. Nehmen Sie die gewünschten Änderungen vor und klicken Sie auf **[!UICONTROL Speichern]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>Die Score-Konfiguration kann nicht geändert werden, da dies das Trainings- und Scoring-Modell des Triggers verändert. Dies entspricht dem Löschen des Punktwerts und dem Erstellen eines neuen Punktwerts. Um die Konfiguration des Punktwerts zu bearbeiten, müssen Sie diesen Punktwert klonen oder einen neuen Punktwert erstellen.

Sie kehren zur Registerkarte **[!UICONTROL Services]** zurück. Wählen Sie die Punktzahl aus, um die aktualisierten Beschreibungsdetails im Bedienfeld Zusätzliche Details auf der rechten Seite des Bildschirms anzuzeigen.

## Punktzahl klonen

Um einen Score zu klonen, wählen Sie einen Score auf der Registerkarte **[!UICONTROL Services]** und wählen Sie **[!UICONTROL Klonen]** im Bedienfeld „Zusätzliche Details“ auf der rechten Seite des Bildschirms.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

Der Bildschirm **[!UICONTROL Grundlegende Informationen]** wird angezeigt. Der Profiltyp, der Name und die Beschreibung werden aus der ursprünglichen Bewertung geklont. Ändern Sie diese Details und wählen Sie **[!UICONTROL Weiter]** aus.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

Der **[!UICONTROL „Ziel definieren]** wird angezeigt. Füllen Sie den Abschnitt Ziele wie bei der Erstellung eines neuen Punktwerts aus und klicken Sie auf **[!UICONTROL Beenden]**.

Sie kehren zur Registerkarte **[!UICONTROL Services]** zurück, auf der Sie den neu geklonten Score in der Liste sehen können.

>[!NOTE]
>
>Der **[!UICONTROL Definieren des Ziels]** wird nicht aus der ursprünglichen Bewertung geklont.

## Punktzahl löschen

Um einen Score zu löschen, wählen Sie einen Score auf der Registerkarte **[!UICONTROL Services]** und wählen Sie **[!UICONTROL Löschen]** im Bedienfeld „Zusätzliche Details“ auf der rechten Seite des Bildschirms aus.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

Das **[!UICONTROL Dokumentation löschen]** Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>Durch das Löschen der Score-Definition werden auch alle prognostizierten Score-Werte für das Personen- oder Kontoprofil gelöscht, jedoch nicht die für die Score-Definition erstellte Feldergruppe. Die Feldergruppe bleibt im Datenmodell „verwaist“.

Sie kehren zur Registerkarte **[!UICONTROL Services]** zurück, auf der Sie den Score in der Liste nicht mehr sehen können.

## Leads-KI-Pipeline-Fehler-Codes

| Fehler-Code | Fehlermeldung |
| --- | --- |
| 401 | FEHLER 401. Leads-KI-Pipeline gestoppt: Nicht genügend gültige Konten für Kontobewertung. Anzahl Konten: {}. |
| 402 | FEHLER 402. Leads-KI-Pipeline gestoppt: nicht genügend gültige Kontakte für Kontaktbewertung. Anzahl der Kontakte: {}. |
| 403 | FEHLER 403. Leads-KI-Pipeline gestoppt: Nicht genügend Aktivitätsvolumen für Modelltraining. Anzahl der Ereignisse: {}. |
| 404 | FEHLER 404. Leads-KI-Pipeline gestoppt: Nicht genügend Konversionen für Modellschulung. Anzahl der Konversionen: {}. |
| 405 | FEHLER 405. Leads-KI-Pipeline gestoppt: Aktivität zu dünn für gültiges Modell-Training. Nur {} Prozent der Konten sind aktiv. |
| 406 | FEHLER 406. Leads-KI-Pipeline gestoppt: Aktivität zu dünn für gültiges Modell-Training. Nur {} Prozent der Kontakte haben Aktivität. |
| 407 | FEHLER 407. Leads-KI-Pipeline gestoppt: Die Aktivitätstypen für die Bewertungsdaten stimmen nicht mit den Schulungsdaten überein. |
| 408 | FEHLER 408. Leads-KI-Pipeline gestoppt: fehlende Rate ist zu hoch für Aktivitätsfunktionen. Fehlende Quote: {}. |
| 409 | FEHLER 409. Leads-KI-Pipeline gestoppt: Test-AUC ist zu niedrig. Test-AUC: {}. |
| 410 | FEHLER 410. Leads-KI-Pipeline gestoppt: Test-AUC ist nach der Parameteroptimierung zu niedrig. Test-AUC: {}. |
| 411 | FEHLER 411. Leads-KI-Pipeline gestoppt: Bei Trainingsdaten fehlen Konversionen, um ein zuverlässiges Modell zu erstellen. Konversionen: {}. |
| 412 | FEHLER 412. Leads-KI-Pipeline gestoppt: Für die Testdaten findet keine Konversion zur Berechnung des AUC-ROC statt. |

| Warn-/Informationscode | Nachricht |
| --- | --- |
| 100 | INFO 100. Leads-KI-Qualitätsprüfung: Die Anzahl der Konten ist: {}. |
| 101 | INFO 101. Leads-KI-Qualitätsprüfung: Die Anzahl der Kontakte ist: {}. |
| 102 | INFO 102. Leads-KI-Qualitätsprüfung: Die Anzahl der Opportunities ist: {}. |
| 103 | INFO 103. Leads-KI-Qualitätsprüfung: Die Testauc ist niedrig. Parameteroptimierung starten. Testen der AUC: {}. |
| 200 | WARNUNG 200. Leads AI-Qualitätsprüfung: Die fehlende Rate firmografischer Funktionen ist: {}. |
| 201 | WARNUNG 201. Leads-KI-Qualitätsprüfung: Die fehlende Aktivitätsrate ist: {}. |

## Nächste Schritte

In diesem Tutorial können Sie jetzt erfolgreich Scores erstellen und verwalten. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Prädiktives Lead- und Konto-Scoring](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Überwachen von prädiktiven Lead- und Konto-Scoring-Aufträgen](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
