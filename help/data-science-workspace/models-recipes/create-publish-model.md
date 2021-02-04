---
keywords: Experience Platform;Modell für maschinelles Lernen;Arbeitsbereich für Datenwissenschaften;beliebte Themen;Erstellen und Veröffentlichen eines Modells
solution: Experience Platform
title: Exemplarische Vorgehensweise zum Erstellen und Veröffentlichen eines maschinellen Lernmodells
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace bietet die Möglichkeit, Ihr Ziel mithilfe des vordefinierten Recommendations-Rezept zu erreichen. In diesem Lernprogramm erfahren Sie, wie Sie auf Ihre Einzelhandelsdaten zugreifen und diese verstehen, ein Modell für maschinelles Lernen erstellen und optimieren und Einblicke in Data Science Workspace generieren können.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 2%

---


# Exemplarische Vorgehensweise zum Erstellen und Veröffentlichen eines maschinellen Lernmodells

![](../images/models-recipes/model-walkthrough/objective.png)

Tun Sie so, als ob Sie eine Online-Einzelhandelswebsite besitzen. Wenn Ihre Kunden auf Ihrer Retail-Website einkaufen, möchten Sie ihnen personalisierte Produktempfehlungen präsentieren, um eine Reihe anderer Produkte Ihrer geschäftlichen Angebot verfügbar zu machen. Im Laufe der Existenz Ihrer Website haben Sie kontinuierlich Kundendaten gesammelt und möchten diese Daten irgendwie zur Erstellung personalisierter Produktempfehlungen verwenden.

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] stellt die Mittel bereit, um Ihr Ziel mit dem vorgefertigten  [Produkt Recommendations Rezept](../pre-built-recipes/product-recommendations.md) zu erreichen. In diesem Lernprogramm erfahren Sie, wie Sie auf Ihre für den Handel bestimmten Daten zugreifen und diese verstehen, ein Modell für maschinelles Lernen erstellen und optimieren und Einblicke in [!DNL Data Science Workspace] generieren können.

Dieses Lernprogramm spiegelt den Arbeitsablauf von [!DNL Data Science Workspace] wider und behandelt die folgenden Schritte zum Erstellen eines maschinellen Lernmodells:

1. [Daten vorbereiten](#prepare-your-data)
2. [Modell erstellen](#author-your-model)
3. [Trainieren und Auswerten Ihres Modells](#train-and-evaluate-your-model)
4. [Modell operationalisieren](#operationalize-your-model)

## Erste Schritte

Bevor Sie mit diesem Tutorial beginnen, müssen Sie folgende Voraussetzungen erfüllen:

* Zugriff auf [!DNL Adobe Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich bitte an Ihren Systemadministrator, bevor Sie fortfahren.

* Aktivieren von Assets. Wenden Sie sich an Ihren Kundenbetreuer, um die folgenden Punkte für Sie bereitzustellen.
   * Recommendations Rezept
   * Recommendations Input DataSet
   * Recommendations Input Schema
   * Recommendations Output DataSet
   * Recommendations Output Schema
   * Golden Data Set postValues
   * Goldenes Datenset-Schema

* Laden Sie die drei erforderlichen [!DNL Jupyter Notebook]-Dateien aus dem Ordner [Adobe public [!DNL Git] repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs) herunter. Anhand dieser Dateien wird der [!DNL JupyterLab]-Arbeitsablauf in [!DNL Data Science Workspace] veranschaulicht.

* Ein Verständnis der folgenden Schlüsselkonzepte, die in diesem Tutorial verwendet werden:
   * [[!DNL Experience Data Model]](../../xdm/home.md): Der durch die Adobe zur Definition von Standard-Schemas wie  [!DNL Profile] und ExperienceEvent für Customer Experience Management angeführte Standardisierungsaufwand.
   * Datensätze: Ein Datenspeicherung- und Verwaltungskonstrukt für tatsächliche Daten. Eine physische instanziierte Instanz eines [XDM-Schemas](../../xdm/schema/field-dictionary.md).
   * Stapel: Datensätze bestehen aus Stapeln. Ein Stapel ist ein Datensatz, der über einen bestimmten Zeitraum erfasst und als eine Einheit verarbeitet wird.
   * [!DNL JupyterLab]:  [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) ist eine Open-Source Web-basierte Schnittstelle für Project  [!DNL Jupyter] und ist eng in  [!DNL Experience Platform].

## Vorbereiten der Daten {#prepare-your-data}

Um ein Modell für maschinelles Lernen zu erstellen, das Ihren Kunden personalisierte Produktempfehlungen vermittelt, müssen frühere Käufe auf Ihrer Website analysiert werden. In diesem Abschnitt wird untersucht, wie diese Daten in [!DNL Platform] bis [!DNL Adobe Analytics] eingehen und wie diese Daten in ein Funktionsdatensatz umgewandelt werden, das von Ihrem maschinellen Lernmodell verwendet werden soll.

### Daten und Schemas

1. Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com/) an und klicken Sie auf **[!UICONTROL Datensätze]**, um alle vorhandenen Datensätze Liste, und wählen Sie den Datensatz aus, den Sie untersuchen möchten. In diesem Fall der Datensatz [!DNL Analytics] **Goldener Datensatz postValues**.
   ![](../images/models-recipes/model-walkthrough/datasets_110.png)
2. Wählen Sie **[!UICONTROL Vorschau DataSet]** oben rechts, um Beispieldatensätze zu prüfen, und klicken Sie dann auf **[!UICONTROL Schließen]**.
   ![](../images/models-recipes/model-walkthrough/golden_data_set_110.png)
3. Wählen Sie den Link unter Schema in der rechten Leiste aus, um das Schema für den Datensatz Ansicht, und gehen Sie dann zurück zur Seite mit den Datensatzdetails.&quot;
   ![](../images/models-recipes/model-walkthrough/golden_schema_110.png)

Die anderen Datensätze wurden zur Vorschau mit Stapeln vorausgefüllt. Sie können diese Datensätze durch Wiederholen der oben genannten Schritte Ansicht werden.

| Datensatzname | Schema | Beschreibung |
| ----- | ----- | ----- |
| Golden Data Set postValues | Goldenes Datenset-Schema | [!DNL Analytics] Quelldaten von Ihrer Website |
| Recommendations Input DataSet | Recommendations Input Schema | Die [!DNL Analytics]-Daten werden mithilfe einer Feature-Pipeline in ein Schulungsdatensatz umgewandelt. Diese Daten werden zur Schulung des Product Recommendations Machine Learning Model verwendet. `itemid` und einem von diesem Kunden gekauften Produkt  `userid` entsprechen. |
| Recommendations Output DataSet | Recommendations Output Schema | Der Datensatz, für den die Bewertungsergebnisse gespeichert werden, enthält die Liste der empfohlenen Produkte für jeden Kunden. |

## Erstellen Sie Ihr Modell {#author-your-model}

Die zweite Komponente des [!DNL Data Science Workspace]-Lebenszyklus umfasst das Authoring von Rezepten und Modellen. Das Produkt Recommendations Rezept wurde entwickelt, um Produktempfehlungen im Maßstab zu generieren, indem alte Kaufdaten und maschinelles Lernen verwendet werden.

Rezepte bilden die Grundlage für ein Modell, da sie maschinelle Lernalgorithmen und Logik zur Lösung spezifischer Probleme enthalten. Wichtiger noch: Rezepte ermöglichen es Ihnen, das maschinelle Lernen in Ihrer gesamten Organisation zu demokratisieren, sodass andere Benutzer auf ein Modell für unterschiedliche Anwendungsfälle zugreifen können, ohne Code schreiben zu müssen.

### Recommendations-Rezept

1. Navigieren Sie in [!DNL Adobe Experience Platform] zu **[!UICONTROL Modelle]** aus der linken Navigationsspalte und klicken Sie dann oben auf **[!UICONTROL Rezepte]**, um eine Liste der verfügbaren Rezepte für Ihr Unternehmen Ansicht.
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. Suchen und öffnen Sie das bereitgestellte **[!UICONTROL Recommendations Rezept]**, indem Sie auf seinen Namen klicken.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. Klicken Sie in der rechten Leiste auf **[!UICONTROL Recommendations Input Schema]**, um das Schema mit dem Skript Ansicht. Die Schema-Felder &quot;[!UICONTROL itemId]&quot;und &quot;[!UICONTROL userId]&quot;entsprechen einem Produkt, das von diesem Kunden zu einem bestimmten Zeitpunkt gekauft wurde ([!UICONTROL interactionType]) ([!UICONTROL timestamp]). Führen Sie die gleichen Schritte aus, um die Felder für das **[!UICONTROL Recommendations Output Schema]** zu überprüfen.
   ![](../images/models-recipes/model-walkthrough/preview_schemas.png)

Sie haben jetzt die Eingabe- und Ausgabedateien geprüft, die für das Produkt Recommendations Rezept erforderlich sind. Sie können nun mit dem nächsten Abschnitt fortfahren, um zu erfahren, wie Sie ein Recommendations-Produktmodell erstellen, ausbilden und bewerten.

## Schulung und Auswertung Ihres Modells {#train-and-evaluate-your-model}

Nachdem Ihre Daten vorbereitet und das Rezept einsatzbereit ist, können Sie Ihr Modell für maschinelles Lernen erstellen, ausbilden und auswerten.

### Modell erstellen

Ein Modell ist eine Instanz eines Rezeptes, mit dem Sie mit Daten im Maßstab trainieren und bewerten können.

1. Navigieren Sie in [!DNL Adobe Experience Platform] zu **[!UICONTROL Modelle]** aus der linken Navigationsspalte und klicken Sie dann auf **[!UICONTROL Rezepte]** oben auf der Seite, um eine Liste aller für Ihr Unternehmen verfügbaren Rezepte anzuzeigen.
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. Suchen und öffnen Sie das bereitgestellte **[!UICONTROL Recommendations Rezept]**, indem Sie auf seinen Namen klicken und die Übersichtsseite des Rezepts eingeben. Klicken Sie auf **[!UICONTROL Erstellen Sie ein Modell]** entweder von der Mitte aus (wenn keine vorhandenen Modelle vorhanden sind) oder oben rechts auf der Seite &quot;Rezeptübersicht&quot;.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. Eine Liste der verfügbaren Eingabedaten für Schulungen wird angezeigt, wählen Sie **[!UICONTROL Recommendations Input DataSet]** und klicken Sie auf **[!UICONTROL Next]**.
   ![](../images/models-recipes/model-walkthrough/select_dataset.png)
4. Geben Sie einen Namen für das Modell ein, z. B. &quot;Recommendations-Produktmodell&quot;. Die verfügbaren Konfigurationen für das Modell werden aufgelistet und enthalten Einstellungen für das Standardschulungs- und Bewertungsverhalten des Modells. Es sind keine Änderungen erforderlich, da diese Konfigurationen für Ihr Unternehmen spezifisch sind. Überprüfen Sie die Konfigurationen und klicken Sie auf **[!UICONTROL Fertigstellen]**.
   ![](../images/models-recipes/model-walkthrough/configure_model.png)
5. Das Modell wurde jetzt erstellt und die Seite *Übersicht* des Modells wird in einem neu erstellten Schulungslauf angezeigt. Beim Erstellen eines Modells wird standardmäßig ein Schulungslauf generiert.
   ![](../images/models-recipes/model-walkthrough/model_post_creation.png)

Sie können auf den Abschluss des Schulungslaufs warten oder im folgenden Abschnitt eine neue Schulungsausführung erstellen.

### Modell mithilfe benutzerdefinierter Hyperparameter trainieren

1. Klicken Sie auf der Seite **Modellübersicht** auf **[!UICONTROL Zug]** rechts oben, um einen neuen Schulungslauf zu erstellen. Wählen Sie den gleichen Eingabedataset aus, den Sie beim Erstellen des Modells verwendet haben, und klicken Sie auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/model-walkthrough/training_select_dataset.png)
2. Die Seite **Konfiguration** wird angezeigt. Hier können Sie den Wert &quot;[!UICONTROL num_recommendations]&quot;des Schulungslaufs konfigurieren, auch als Hyperparameter bezeichnet. Ein geschultes und optimiertes Modell verwendet die leistungsstärksten Hyperparameter, die auf den Ergebnissen der Schulungsausführung basieren.

   Hyperparameter können nicht erlernt werden, daher müssen sie vor Schulungsdurchläufen zugewiesen werden. Die Anpassung von Hyperparametern kann die Genauigkeit des eingeübten Modells ändern. Da die Optimierung eines Modells ein iterativer Prozess ist, kann es erforderlich sein, dass mehrere Schulungen durchgeführt werden, bevor eine zufriedenstellende Bewertung erreicht wird.

   >[!TIP]
   >
   >Setzen Sie **[!UICONTROL num_recommendations]** auf 10.

   ![](../images/models-recipes/model-walkthrough/configure_hyperparameter.png)
3. Ein zusätzlicher Datenpunkt wird auf dem Modellbewertungsdiagramm angezeigt, sobald der neue Schulungslauf abgeschlossen ist. Dies kann bis zu mehreren Minuten dauern.
   ![](../images/models-recipes/model-walkthrough/post_training_run.png)

### Modell bewerten

Bei jedem Abschluss eines Schulungslaufs können Sie die resultierenden Bewertungsmetriken zur Ansicht der Leistung des Modells festlegen.

1. Überprüfen Sie die Bewertungsmetriken (Präzision und Rückruf) für jede abgeschlossene Schulung, indem Sie auf den Schulungslauf klicken.
2. Informationen zu den einzelnen Bewertungsmetriken Je höher diese Metriken sind, desto besser hat das Modell funktioniert.
   ![](../images/models-recipes/model-walkthrough/evaluation_metrics.png)
3. Sie können den Datensatz, das Schema und die Konfigurationsparameter anzeigen, die für jeden Schulungslauf auf der rechten Leiste verwendet werden.
4. Navigieren Sie zurück zur Modellseite und identifizieren Sie die Schulungen mit der höchsten Leistung, indem Sie deren Bewertungsmetriken beobachten.

## Operationalisieren Sie Ihr Modell {#operationalize-your-model}

Der letzte Schritt im Data Science-Arbeitsablauf besteht darin, Ihr Modell zu operieren, um Erkenntnisse aus Ihrem Datenspeicher zu bewerten und zu nutzen.

### Bewertung und Erstellung von Einblicken

1. Klicken Sie auf der Seite mit den Produktempfehlungen Modell *Übersicht* auf den Namen des Schulungslaufs mit den höchsten Rückruf- und Genauigkeitswerten.
2. Klicken Sie oben rechts auf der Seite mit den Details zum Schulungslauf auf **[!UICONTROL Ergebnis]**.
3. Wählen Sie den Datensatz **[!UICONTROL Recommendations Input DataSet]** als Scoring-Eingabedatensatz aus, der mit dem Datensatz übereinstimmt, den Sie beim Erstellen des Modells und Ausführen der zugehörigen Schulungen verwendet haben. Klicken Sie dann auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/model-walkthrough/scoring_input.png)
4. Wählen Sie als Bewertungsausgabedataset den Eintrag **[!UICONTROL Recommendations Output DataSet]** aus. Die Bewertungsergebnisse werden in diesem Datensatz als Stapel gespeichert.
   ![](../images/models-recipes/model-walkthrough/scoring_output.png)
5. Überprüfen Sie die Bewertungskonfigurationen. Diese Parameter enthalten die zuvor ausgewählten Eingabe- und Ausgabedaten zusammen mit den entsprechenden Schemas. Klicken Sie auf **[!UICONTROL Fertig stellen]**, um den Bewertungsvorgang zu starten. Die Ausführung kann mehrere Minuten dauern.
   ![](../images/models-recipes/model-walkthrough/scoring_configure.png)


### Ansicht erzielte Einblicke

Nach erfolgreichem Abschluss der Bewertungsausführung können Sie die Ergebnisse Vorschau und Ansicht der gewonnenen Erkenntnisse vornehmen.

1. Klicken Sie auf der Seite mit den Bewertungsergebnissen auf die abgeschlossene Bewertungsausführung und klicken Sie dann auf der rechten Leiste auf **[!UICONTROL Vorschau Scoring Results Dataset]**.
   ![](../images/models-recipes/model-walkthrough/score_complete.png)
2. In der Tabelle &quot;Vorschau&quot;enthält jede Zeile Produktempfehlungen für einen bestimmten Kunden mit der Bezeichnung [!UICONTROL recommendations] bzw. [!UICONTROL userId]. Da der Parameter [!UICONTROL num_recommendations] Hyperparameter in den Screenshots auf 10 gesetzt wurde, kann jede Empfehlungszeile bis zu 10 Produktidentitäten enthalten, die durch ein Nummernzeichen (#) getrennt sind.
   ![](../images/models-recipes/model-walkthrough/preview_score_results.png)

## Nächste Schritte {#next-steps}

Gut gemacht, Sie haben erfolgreich Produktempfehlungen generiert!

In diesem Lernprogramm wurde der Arbeitsablauf von [!DNL Data Science Workspace] vorgestellt, in dem gezeigt wird, wie unverarbeitete Rohdaten durch maschinelles Lernen in nützliche Informationen umgewandelt werden können. Um mehr über die Verwendung von [!DNL Data Science Workspace] zu erfahren, fahren Sie mit der nächsten Anleitung zu [Erstellen des Schemas und Datensatzes für den Einzelhandel](./create-retails-sales-dataset.md) fort.