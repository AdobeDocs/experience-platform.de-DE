---
keywords: Experience Platform; Schulung und Auswertung; Data Science Workspace; beliebte Themen; Modell erstellen; Trainings-Lauf erstellen
solution: Experience Platform
title: Modell in der Benutzeroberfläche von Data Science Workspace trainieren und bewerten
topic-legacy: tutorial
type: Tutorial
description: In Adobe Experience Platform Data Science Workspace können Sie ein Modell für maschinelles Lernen einrichten, indem Sie ein vorhandenes Rezept einbinden, das für den Zweck des Modells geeignet ist. Anschließend wird das Modell trainiert und bewertet, um seine Effizienz und Wirksamkeit zu erhöhen; dazu werden die entsprechenden Hyperparameter fein abgestimmt. Rezepte sind wiederverwendbar; mit einem Rezept können also verschiedene Modelle erstellt und auf individuelle Zwecke zugeschnitten werden.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 64%

---

# Modell in der Benutzeroberfläche von Data Science Workspace trainieren und bewerten

In Adobe Experience Platform Data Science Workspace können Sie ein Modell für maschinelles Lernen einrichten, indem Sie ein vorhandenes Rezept einbinden, das für den Zweck des Modells geeignet ist. Anschließend wird das Modell trainiert und bewertet, um seine Effizienz und Wirksamkeit zu erhöhen; dazu werden die entsprechenden Hyperparameter fein abgestimmt. Rezepte sind wiederverwendbar; mit einem Rezept können also verschiedene Modelle erstellt und auf individuelle Zwecke zugeschnitten werden.

Dieses Tutorial leitet Sie durch die Schritte zum Erstellen, Trainieren und Bewerten eines Modells.

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform]Wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Das Tutorial setzt ein vorhandenes Rezept voraus. Wenn Sie kein Rezept haben, befolgen Sie die Anweisungen im Tutorial zum [Importieren eines gepackten Rezepts in der UI](./import-packaged-recipe-ui.md), bevor Sie fortfahren.

## Modell erstellen

Wählen Sie in Experience Platform die **[!UICONTROL Modelle]** im linken Navigationsbereich auf und wählen Sie dann die Registerkarte Durchsuchen aus, um Ihre vorhandenen Modelle anzuzeigen. Auswählen **[!UICONTROL Modell erstellen]** oben rechts auf der Seite, um einen Modellerstellungsprozess zu starten.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Durchsuchen Sie die Liste der vorhandenen Rezepte, wählen Sie das Rezept aus, das zum Erstellen des Modells verwendet werden soll, und wählen Sie **[!UICONTROL Nächste]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Wählen Sie einen entsprechenden Eingabedatensatz aus und wählen Sie **[!UICONTROL Nächste]**. Dadurch wird der standardmäßige Eingabedatensatz zum Trainieren des Modells festgelegt.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Geben Sie einen Namen für das Modell ein und überprüfen Sie die standardmäßigen Modellkonfigurationen. Bei der Rezepterstellung wurden Standardkonfigurationen angewendet; um die Konfigurationswerte zu prüfen und zu ändern, doppelklicken Sie auf die jeweiligen Werte.

Um einen neuen Konfigurationssatz bereitzustellen, wählen Sie **[!UICONTROL Neue Konfiguration hochladen]** und ziehen Sie eine JSON-Datei mit Modellkonfigurationen in das Browserfenster. Auswählen **[!UICONTROL Beenden]** , um das Modell zu erstellen.

>[!NOTE]
>
>Konfigurationen sind für das beabsichtigte Rezept eindeutig und spezifisch. Das heißt, dass Konfigurationen für das Rezept „Einzelhandelsumsätze“ für das Rezept „Produktempfehlungen“ nicht funktionieren. Eine Liste der Rezeptkonfigurationen für „Einzelhandelsumsätze“ finden Sie im Abschnitt [Referenz](#reference).

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Trainings-Lauf erstellen

Wählen Sie in Experience Platform die **[!UICONTROL Modelle]** im linken Navigationsbereich auf und wählen Sie dann die Registerkarte Durchsuchen aus, um Ihre vorhandenen Modelle anzuzeigen. Suchen und wählen Sie den Hyperlink aus, der an den Namen des Modells angehängt ist, das Sie trainieren möchten.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alle vorhandenen Trainings-Läufe werden mit ihrem aktuellen Trainings-Status aufgeführt. Für Modelle, die mit dem [!DNL Data Science Workspace] -Benutzeroberfläche wird automatisch ein Trainings-Lauf mit den Standardkonfigurationen und dem Eingabedatensatz für das Training generiert und ausgeführt.

Erstellen Sie einen neuen Trainings-Lauf durch Auswahl von **[!UICONTROL Zug]** oben rechts auf der Modellübersichtsseite.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Wählen Sie den Eingabedatensatz für das Training aus und wählen Sie dann **[!UICONTROL Nächste]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Bei der Modellerstellung angegebene Standardkonfigurationen werden angezeigt; ändern Sie sie nach Bedarf, indem Sie auf die Werte doppelklicken. Auswählen **[!UICONTROL Beenden]** , um den Trainings-Lauf zu erstellen und auszuführen.

>[!NOTE]
>
>Konfigurationen sind für das beabsichtigte Rezept eindeutig und spezifisch. Das heißt, dass Konfigurationen für das Rezept „Einzelhandelsumsätze“ für das Rezept „Produktempfehlungen“ nicht funktionieren. Eine Liste der Rezeptkonfigurationen für „Einzelhandelsumsätze“ finden Sie im Abschnitt [Referenz](#reference).

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Modell bewerten

Wählen Sie in Experience Platform die **[!UICONTROL Modelle]** im linken Navigationsbereich auf und wählen Sie dann die Registerkarte Durchsuchen aus, um Ihre vorhandenen Modelle anzuzeigen. Suchen und wählen Sie den Hyperlink aus, der an den Namen des Modells angehängt ist, das Sie auswerten möchten.

![Auswahlmodell](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alle vorhandenen Trainings-Läufe werden mit ihrem aktuellen Trainings-Status aufgeführt. Bei mehreren abgeschlossenen Trainings-Läufen können Bewertungsmetriken über verschiedene Trainings-Läufe im Modellbewertungsdiagramm hinweg verglichen werden. Wählen Sie mithilfe der Dropdown-Liste über dem Diagramm eine Auswertungsmetrik aus.

Die Metrik „Mean Absolute Percent Error (MAPE)“ drückt die Genauigkeit als Fehlerprozentwert aus. So lässt sich das am besten geeignete Experiment ermitteln. Dabei gilt: Je niedriger der MAPE-Wert, desto besser.

![Übersicht über die Trainings-Läufe](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

Die Metrik „Präzision“ beschreibt den Prozentwert relevanter Instanzen im Vergleich zu den insgesamt *abgerufenen* Instanzen. Präzision kann als Wahrscheinlichkeit verstanden werden, mit der ein zufällig ausgewähltes Ergebnis richtig ist.

![Ausführen mehrerer Ausführungen](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Wenn Sie einen bestimmten Trainings-Lauf auswählen, erhalten Sie die Details zu diesem Lauf, indem Sie die Auswertungsseite öffnen. Das können Sie bereits vor Abschluss des Laufs tun. Auf der Auswertungsseite können Sie weitere Auswertungsmetriken, Konfigurationsparameter und Visualisierungen sehen, die spezifisch für den Trainings-Lauf sind.

![Vorschau-Logs](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

Außerdem können Sie Aktivitätsprotokolle herunterladen, um die Details zum Lauf anzuzeigen. Protokolle sind besonders bei fehlgeschlagenen Läufen nützlich: Mit ihrer Hilfe können Sie herausfinden, was falsch gelaufen ist.

![Aktivitätsprotokolle](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Hyperparameter können nicht trainiert werden und ein Modell muss durch Testen verschiedener Kombinationen von Hyperparametern optimiert werden. Wiederholen Sie dieses Trainings- und Bewertungsverfahren, bis Sie zu einem optimierten Modell gelangt sind.

## Nächste Schritte

Dieses Tutorial hat Sie durch das Erstellen, Trainieren und Bewerten eines Modells in [!DNL Data Science Workspace]. Sobald Sie ein optimiertes Modell erreicht haben, können Sie das trainierte Modell nutzen, um Einblicke zu generieren; folgen Sie dazu dem Tutorial [Modell in der UI bewerten](./score-model-ui.md).

## Referenz {#reference}

### Konfigurationen für das Rezept „Einzelhandelsumsätze“

Hyperparameter bestimmen über das Trainings-Verhalten des Modells. Eine Änderung von Hyperparametern wirkt sich auf die Genauigkeit und Präzision des Modells aus:

| Hyperparameter | Beschreibung | Empfohlener Bereich |
| --- | --- | --- |
| learning_rate | Die Lernrate verkleinert den Beitrag der einzelnen Baumstrukturen um learning_rate. Dabei gibt es einen Kompromiss zwischen learning_rate und n_estimators. | 0,1 |
| n_estimators | Die Zahl der auszuführenden Boosting-Phasen. Gradient Boosting ist relativ stabil, was Überanpassung angeht, sodass eine große Zahl in der Regel bessere Ergebnisse liefert. | 100 |
| max_depth | Maximale Tiefe der einzelnen Regressionsschätzer. Die maximale Tiefe begrenzt die Zahl der Knoten in der Baumstruktur. Passen Sie den Parameter für optimale Leistung an; der optimale Wert hängt von der Interaktion der Eingabevariablen ab. | 3 |

Zusätzliche Parameter bestimmen die technischen Eigenschaften des Modells:

| Parameterschlüssel | Typ | Beschreibung |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Zeichenfolge | Liste mit kommagetrennten Eingabeschemaattributen. |
| `ACP_DSW_TARGET_FEATURES` | Zeichenfolge | Liste mit kommagetrennten Ausgabeschemaattributen. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolesch | Legt fest, ob Eingabe- und Ausgabefunktionen geändert werden können. |
| `tenantId` | Zeichenfolge | Diese Kennung stellt sicher, dass die von Ihnen erstellten Ressourcen den richtigen Namespace erhalten und in Ihrer IMS-Organisation enthalten sind. [Gehen Sie wie folgt vor](../../xdm/api/getting-started.md#know-your-tenant_id), um Ihre Mandantenkennung zu suchen. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Zeichenfolge | Das zum Trainieren eines Modells verwendete Eingabeschema. |
| `evaluation.labelColumn` | Zeichenfolge | Spaltenbezeichnung für Bewertungsvisualisierungen. |
| `evaluation.metrics` | Zeichenfolge | Kommagetrennte Liste mit Bewertungsmetriken, die zur Bewertung eines Modells verwendet werden. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Zeichenfolge | Das zum Scoring eines Modells verwendete Ausgabeschema. |
