---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: Erstellen und Auswerten eines Modells (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 2%

---


# Erstellen und Auswerten eines Modells (UI)

In Adobe Experience Platform Data Science Workspace wird ein Modell für maschinelles Lernen erstellt, indem ein vorhandenes Rezept integriert wird, das für die Absicht des Modells geeignet ist. Anschließend wird das Modell trainiert und bewertet, um seine Betriebseffizienz und Wirksamkeit zu optimieren, indem die zugehörigen Hyperparameter präzisiert werden. Rezepte sind wiederverwendbar, d. h., mehrere Modelle können mit einem Rezept erstellt und auf spezifische Zwecke zugeschnitten werden.

Dieses Lernprogramm führt Sie durch die Schritte zum Erstellen, Ausbilden und Auswerten eines Modells.

## Erste Schritte

Um dieses Lernprogramm abzuschließen, müssen Sie Zugriff auf die Erlebnisplattform haben. Wenn Sie keinen Zugriff auf eine IMS-Organisation in Experience Platform haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Dieses Lernprogramm erfordert ein vorhandenes Rezept. Wenn Sie kein Rezept haben, befolgen Sie die Anweisungen zum [Importieren eines gepackten Rezepts im UI](./import-packaged-recipe-ui.md) -Lernprogramm, bevor Sie fortfahren.

## Modell erstellen

1. Klicken Sie in Adobe Experience Platform auf den Link **[!UICONTROL Modelle]** in der linken Navigationsspalte, um alle vorhandenen Modelle Liste. Klicken Sie oben rechts auf der Seite auf Modell **[!UICONTROL erstellen]** , um mit der Modellerstellung zu beginnen.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Durchsuchen Sie die Liste der vorhandenen Rezepte, wählen Sie das Rezept aus, das zum Erstellen des Modells verwendet werden soll, und klicken Sie auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

3. Wählen Sie einen entsprechenden Eingabedatensatz aus und klicken Sie auf **[!UICONTROL Weiter]**. Dadurch wird der Standard-Datensatz für die Eingabeschulung für das Modell festgelegt.
   ![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

4. Geben Sie einen Namen für das Modell ein und überprüfen Sie die Standardmodellkonfigurationen. Während der Erstellung von Rezepten wurden Standardkonfigurationen angewendet, um die Konfigurationswerte zu überprüfen und zu ändern, indem die Dublette auf die Werte klickt. Um einen neuen Konfigurationssatz bereitzustellen, klicken Sie auf Neue Konfiguration **[!UICONTROL hochladen]** und ziehen Sie eine JSON-Datei mit Modellkonfigurationen in das Browserfenster. Klicken Sie auf **[!UICONTROL Fertig stellen]** , um das Modell zu erstellen.
   >[!NOTE]Konfigurationen sind eindeutig und spezifisch für das gewünschte Rezept. Das bedeutet, dass Konfigurationen für das Einzelhandelsrezept für das Produktempfehlungsrezept nicht funktionieren. Eine Liste der Retail-Rezeptkonfigurationen finden Sie im [Referenzabschnitt](#reference) .

   ![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Erstellen eines Schulungslaufs

1. Klicken Sie in Adobe Experience Platform auf den Link **[!UICONTROL Modelle]** in der linken Navigationsspalte, um alle vorhandenen Modelle Liste. Klicken Sie auf den Namen des zu trainierenden Modells.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Alle vorhandenen Schulungen mit ihrem aktuellen Schulungsstatus werden aufgelistet. Bei Modellen, die mit der Benutzeroberfläche von Data Science Workspace erstellt wurden, wird automatisch ein Schulungslauf mit den Standardkonfigurationen und dem Eingabeteilschulungsdatensatz generiert und ausgeführt.
   ![](../images/models-recipes/train-evaluate-ui/model_overview.png)

3. Erstellen Sie eine neue Schulung, indem Sie auf **[!UICONTROL Zug]** oben rechts auf der Modellübersichtsseite klicken.
   ![](../images/models-recipes/train-evaluate-ui/training_input.png)

4. Wählen Sie den für die Schulung erforderlichen Eingabedatensatz aus und klicken Sie auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

5. Während der Modellerstellung bereitgestellte Standardkonfigurationen werden angezeigt, ändern und ändern Sie sie entsprechend, indem Sie die Dublette auf die Werte klicken. Klicken Sie auf **[!UICONTROL Fertig stellen]** , um den Schulungsvorgang zu erstellen und auszuführen.
   >[!NOTE]Konfigurationen sind eindeutig und spezifisch für das gewünschte Rezept. Das bedeutet, dass Konfigurationen für das Einzelhandelsrezept für das Produktempfehlungsrezept nicht funktionieren. Eine Liste der Retail-Rezeptkonfigurationen finden Sie im [Referenzabschnitt](#reference) .

   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

## Modell bewerten

1. Klicken Sie in Adobe Experience Platform auf den Link **[!UICONTROL Modelle]** in der linken Navigationsspalte, um alle vorhandenen Modelle Liste. Klicken Sie auf den Namen des auszuwertenden Modells.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Alle vorhandenen Schulungen mit ihrem aktuellen Schulungsstatus werden aufgelistet. Bei mehreren abgeschlossenen Schulungsläufen können Bewertungsmetriken über verschiedene Schulungsläufe im Modellbewertungsdiagramm verglichen werden. Wählen Sie eine Bewertungsmetrik aus der Dropdown-Liste oberhalb des Diagramms.

   Die Metrik &quot;Mean Absolute Percent Error (MAPE)&quot;gibt die Genauigkeit als Prozentsatz des Fehlers an. Damit wird das leistungsstärkste Experiment identifiziert. Je niedriger der MAPE, desto besser.

   ![](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

   Die Metrik &quot;Präzision&quot;beschreibt den Prozentsatz der relevanten Instanzen im Vergleich zur insgesamt *abgerufenen* Instanzen. Präzision kann als Wahrscheinlichkeit gesehen werden, dass ein zufällig ausgewähltes Ergebnis korrekt ist.
   ![](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

   Klicken Sie auf einen bestimmten Schulungslauf, um die Details zu dieser Ausführung Ansicht. Dies kann bereits vor Abschluss der Ausführung erfolgen. Auf der Seite &quot;Ausführungsdetails&quot;können Sie weitere Evaluierungsmetriken, Konfigurationsparameter und Visualisierungen sehen, die spezifisch für den Schulungsablauf sind. Sie können auch Aktivitäten-Protokolle herunterladen, um die Details der Ausführung anzuzeigen. Protokolle sind besonders nützlich für fehlgeschlagene Ausführung, um zu sehen, was schiefgelaufen ist.
   ![](../images/models-recipes/train-evaluate-ui/activity_logs.png)

3. Hyperparameter können nicht trainiert werden und ein Modell muss durch Testen verschiedener Kombinationen von Hyperparametern optimiert werden. Wiederholen Sie diesen Modellschulungs- und -bewertungsprozess, bis Sie zu einem optimierten Modell gelangt sind.

## Nächste Schritte

Dieses Lernprogramm führte Sie durch die Erstellung, Schulung und Auswertung eines Modells im Data Science Workspace. Sobald Sie ein optimiertes Modell erreicht haben, können Sie das geschulte Modell verwenden, um Einblicke zu generieren, indem Sie der [Bewertung eines Modells im UI](./score-model-ui.md) -Lernprogramm folgen.

## Referenz {#reference}

### Konfiguration von Rezept für Einzelhandel

Hyperparameter bestimmen das Schulungsverhalten des Modells. Die Änderung der Hyperparameter wirkt sich auf die Genauigkeit und Präzision des Modells aus:

| Hyperparameter | Beschreibung | Empfohlener Bereich |
--- | --- | ---
| learning_rate | Die Lernrate schrumpft den Beitrag der einzelnen Bäume nach learning_rate. Es gibt einen Kompromiss zwischen learning_rate und n_estimators. | 0.1 | [2 - 10] /Anzahl der Schätzungen |
| n_estimators | Die Anzahl der auszuführenden Verstärkungsphasen. Die Verlaufsverstärkung ist relativ stabil bis zur Überpassung, sodass eine große Anzahl in der Regel bessere Leistung erzielt. | 100 | 100 - 1000 |
| max_depth | Maximale Tiefe der einzelnen Regressionsschätzungen. Die maximale Tiefe begrenzt die Anzahl der Knoten im Baum. Passen Sie diesen Parameter für eine optimale Leistung an. der beste Wert hängt von der Interaktion der Eingabevariablen ab. | 3 | 4 - 10 |

Zusätzliche Parameter bestimmen die technischen Eigenschaften des Modells:

| Parameterschlüssel | Typ | Beschreibung |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Zeichenfolge | Liste von kommagetrennten Eingabe-Schema-Attributen. |
| `ACP_DSW_TARGET_FEATURES` | Zeichenfolge | Liste von kommagetrennten Schema-Attributen. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolesch | Bestimmt, ob Eingabe- und Ausgabefunktionen geändert werden können |
| `tenantId` | Zeichenfolge | Diese ID stellt sicher, dass die von Ihnen erstellten Ressourcen korrekt benannt und in Ihrer IMS-Organisation enthalten sind. [Gehen Sie wie folgt vor](../../xdm/api/getting-started.md#know-your-tenant_id) , um Ihre Mandanten-ID zu finden. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Zeichenfolge | Das für die Modellschulung verwendete Input-Schema. |
| `evaluation.labelColumn` | Zeichenfolge | Spaltenbeschriftung für Evaluierungsvisualisierungen. |
| `evaluation.metrics` | Zeichenfolge | Kommagetrennte Liste von Bewertungsmetriken, die für die Bewertung eines Modells verwendet werden. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Zeichenfolge | Das für das Scoring eines Schemas verwendete Ausgabemodell. |