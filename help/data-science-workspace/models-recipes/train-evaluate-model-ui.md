---
keywords: Experience Platform;Trainieren und Auswerten;Datenwissenschafts-Workspace;beliebte Themen;Erstellen eines Modells;Erstellen eines Trainings-Durchgangs
solution: Experience Platform
title: Trainieren und Bewerten eines Modells in der Data Science Workspace-Benutzeroberfläche
type: Tutorial
description: In Adobe Experience Platform Data Science Workspace können Sie ein Modell für maschinelles Lernen einrichten, indem Sie ein vorhandenes Rezept einbinden, das für den Zweck des Modells geeignet ist. Anschließend wird das Modell trainiert und ausgewertet, um seine Effizienz und Wirksamkeit zu erhöhen; dazu werden die entsprechenden Hyperparameter fein abgestimmt. Rezepte sind wiederverwendbar; mit einem Rezept können also verschiedene Modelle erstellt und auf individuelle Zwecke zugeschnitten werden.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 53%

---

# Trainieren und Bewerten eines Modells in der Data Science Workspace-Benutzeroberfläche

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

In Adobe Experience Platform Data Science Workspace können Sie ein Modell für maschinelles Lernen einrichten, indem Sie ein vorhandenes Rezept einbinden, das für den Zweck des Modells geeignet ist. Anschließend wird das Modell trainiert und ausgewertet, um seine Effizienz und Wirksamkeit zu erhöhen; dazu werden die entsprechenden Hyperparameter fein abgestimmt. Rezepte sind wiederverwendbar; mit einem Rezept können also verschiedene Modelle erstellt und auf individuelle Zwecke zugeschnitten werden.

Dieses Tutorial leitet Sie durch die Schritte zum Erstellen, Trainieren und Auswerten eines Modells.

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie in [!DNL Experience Platform] keinen Zugriff auf eine Organisation haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Das Tutorial setzt ein vorhandenes Rezept voraus. Wenn Sie kein Rezept haben, befolgen Sie die Anweisungen im Tutorial zum [Importieren eines gepackten Rezepts in der UI](./import-packaged-recipe-ui.md), bevor Sie fortfahren.

## Modell erstellen

Wählen Sie in Experience Platform die Registerkarte **[!UICONTROL Modelle]** im linken Navigationsbereich und anschließend die Registerkarte Durchsuchen aus, um Ihre vorhandenen Modelle anzuzeigen. Wählen Sie **[!UICONTROL Modell erstellen]** oben rechts auf der Seite aus, um mit der Modellerstellung zu beginnen.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Durchsuchen Sie die Liste der vorhandenen Rezepte, suchen Sie das Rezept, das zum Erstellen des Modells verwendet werden soll, und wählen Sie &quot;**[!UICONTROL &quot;]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Wählen Sie einen entsprechenden Eingabedatensatz aus und klicken Sie auf **[!UICONTROL Weiter]**. Dadurch wird der standardmäßige Eingabetraining-Datensatz für das Modell festgelegt.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Geben Sie einen Namen für das Modell ein und überprüfen Sie die standardmäßigen Modellkonfigurationen. Die Standardkonfigurationen wurden bei der Rezepterstellung angewendet. Überprüfen und ändern Sie die Konfigurationswerte durch Doppelklicken auf die Werte.

Um einen neuen Satz von Konfigurationen bereitzustellen, wählen Sie **[!UICONTROL Neue Konfiguration hochladen]** und ziehen Sie eine JSON-Datei mit Modellkonfigurationen in das Browser-Fenster. Wählen Sie **[!UICONTROL Beenden]**, um das Modell zu erstellen.

>[!NOTE]
>
>Konfigurationen sind eindeutig und spezifisch für ihr beabsichtigtes Rezept. Dies bedeutet, dass Konfigurationen für das Rezept für Einzelhandelsumsätze für das Produkt &quot;Recommendations&quot; nicht funktionieren. Eine Liste der Rezeptkonfigurationen für „Einzelhandelsumsätze“ finden Sie im Abschnitt [Referenz](#reference).

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Trainings-Lauf erstellen

Wählen Sie in Experience Platform die Registerkarte **[!UICONTROL Modelle]** im linken Navigationsbereich und anschließend die Registerkarte Durchsuchen aus, um Ihre vorhandenen Modelle anzuzeigen. Suchen Sie den Hyperlink, der mit dem Namen des Modells verbunden ist, das Sie trainieren möchten, und wählen Sie ihn aus.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alle vorhandenen Trainings-Läufe werden mit ihrem aktuellen Trainings-Status aufgeführt. Für Modelle, die mit der [!DNL Data Science Workspace]-Benutzeroberfläche erstellt wurden, wird automatisch ein Trainings-Durchgang generiert und mit den Standardkonfigurationen und dem eingegebenen Trainings-Datensatz ausgeführt.

Erstellen Sie einen neuen Trainings-Lauf, indem **[!UICONTROL Trainieren]** oben rechts auf der Seite Modellübersicht auswählen.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Wählen Sie den Trainings-Eingabedatensatz für den Trainings-Lauf und klicken Sie dann auf **[!UICONTROL Weiter]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Bei der Modellerstellung angegebene Standardkonfigurationen werden angezeigt; ändern Sie sie nach Bedarf, indem Sie auf die Werte doppelklicken. Wählen **[!UICONTROL Beenden]**, um den Trainings-Lauf zu erstellen und auszuführen.

>[!NOTE]
>
>Konfigurationen sind eindeutig und spezifisch für ihr beabsichtigtes Rezept. Dies bedeutet, dass Konfigurationen für das Rezept für Einzelhandelsumsätze für das Produkt &quot;Recommendations&quot; nicht funktionieren. Eine Liste der Rezeptkonfigurationen für „Einzelhandelsumsätze“ finden Sie im Abschnitt [Referenz](#reference).

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Modell auswerten

Wählen Sie in Experience Platform die Registerkarte **[!UICONTROL Modelle]** im linken Navigationsbereich und anschließend die Registerkarte Durchsuchen aus, um Ihre vorhandenen Modelle anzuzeigen. Suchen Sie den Hyperlink, der mit dem Namen des Modells verbunden ist, das Sie auswerten möchten, und wählen Sie ihn aus.

![Modell auswählen](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alle vorhandenen Trainings-Läufe werden mit ihrem aktuellen Trainings-Status aufgeführt. Bei mehreren abgeschlossenen Trainings-Durchgängen können Bewertungsmetriken über verschiedene Trainings-Durchgänge hinweg im Modellevaluierungsdiagramm verglichen werden. Wählen Sie mithilfe der Dropdown-Liste über dem Diagramm eine Auswertungsmetrik aus.

Die Metrik „Mean Absolute Percent Error (MAPE)“ drückt die Genauigkeit als Fehlerprozentwert aus. So lässt sich das am besten geeignete Experiment ermitteln. Dabei gilt: Je niedriger der MAPE-Wert, desto besser.

![Überblick über Trainings-Läufe](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

Die Metrik „Präzision“ beschreibt den Prozentwert relevanter Instanzen im Vergleich zu den insgesamt *abgerufenen* Instanzen. Präzision kann als Wahrscheinlichkeit verstanden werden, mit der ein zufällig ausgewähltes Ergebnis richtig ist.

![Ausführen mehrerer Ausführungen](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Die Auswahl eines bestimmten Trainings-Durchgangs liefert die Details dieses Durchgangs, indem die Auswertungsseite geöffnet wird. Das können Sie bereits vor Abschluss des Laufs tun. Auf der Seite „Evaluierung“ können Sie andere Auswertungsmetriken, Konfigurationsparameter und Visualisierungen sehen, die für den Trainings-Lauf spezifisch sind.

![Vorschau der Protokolle](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

Außerdem können Sie Aktivitätsprotokolle herunterladen, um die Details zum Lauf anzuzeigen. Protokolle sind besonders bei fehlgeschlagenen Läufen nützlich: Mit ihrer Hilfe können Sie herausfinden, was falsch gelaufen ist.

![Aktivitätsprotokolle](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Hyperparameter können nicht trainiert werden und ein Modell muss durch Testen verschiedener Kombinationen von Hyperparametern optimiert werden. Wiederholen Sie dieses Trainings- und Auswertungsverfahren, bis Sie zu einem optimierten Modell gelangt sind.

## Nächste Schritte

Dieses Tutorial führte Sie durch die Erstellung, Schulung und Bewertung eines Modells in [!DNL Data Science Workspace]. Sobald Sie ein optimiertes Modell erreicht haben, können Sie das trainierte Modell nutzen, um Einblicke zu generieren; folgen Sie dazu dem Tutorial [Modell in der UI bewerten](./score-model-ui.md).

## Referenz {#reference}

### Konfigurationen für das Rezept „Einzelhandelsumsätze“

Hyperparameter bestimmen über das Trainings-Verhalten des Modells. Eine Änderung von Hyperparametern wirkt sich auf die Genauigkeit und Präzision des Modells aus:

| Hyperparameter | Beschreibung | Empfohlener Bereich |
| --- | --- | --- |
| learning_rate | Die Lernrate verkleinert den Beitrag der einzelnen Baumstrukturen um learning_rate. Dabei gibt es einen Kompromiss zwischen learning_rate und n_estimators. | 0,1 |
| n_estimators | Die Zahl der auszuführenden Boosting-Phasen. Gradient Boosting ist relativ stabil, was Überanpassung angeht, sodass eine große Zahl in der Regel bessere Ergebnisse liefert. | 100 |
| max_depth | Maximale Tiefe der einzelnen Regressionsschätzer. Die maximale Tiefe begrenzt die Zahl der Knoten in der Baumstruktur. Passen Sie den Parameter für optimale Performance an; der optimale Wert hängt von der Interaktion der Eingabevariablen ab. | 3 |

Zusätzliche Parameter bestimmen die technischen Eigenschaften des Modells:

| Parameterschlüssel | Typ | Beschreibung |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Zeichenfolge | Liste mit kommagetrennten Eingabeschemaattributen. |
| `ACP_DSW_TARGET_FEATURES` | Zeichenfolge | Liste mit kommagetrennten Ausgabeschemaattributen. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolesch | Legt fest, ob Eingabe- und Ausgabefunktionen geändert werden können. |
| `tenantId` | Zeichenfolge | Diese ID stellt sicher, dass die von Ihnen erstellten Ressourcen über einen ordnungsgemäßen Namespace verfügen und in Ihrer Organisation enthalten sind. [Gehen Sie wie folgt vor](../../xdm/api/getting-started.md#know-your-tenant_id), um Ihre Mandantenkennung zu suchen. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Zeichenfolge | Das zum Trainieren eines Modells verwendete Eingabeschema. |
| `evaluation.labelColumn` | Zeichenfolge | Spaltenbezeichnung für Auswertungsvisualisierungen. |
| `evaluation.metrics` | Zeichenfolge | Kommagetrennte Liste mit Auswertungsmetriken, die zur Auswertung eines Modells verwendet werden. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Zeichenfolge | Das zum Scoring eines Modells verwendete Ausgabeschema. |
