---
keywords: Experience Platform;Modell für maschinelles Lernen;Arbeitsbereich für Datenwissenschaften;beliebte Themen;Erstellen und Veröffentlichen eines Modells
solution: Experience Platform
title: Erstellen und Veröffentlichen eines maschinellen Lernmodells
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace bietet die Möglichkeit, Ihr Ziel mithilfe des vordefinierten Recommendations-Rezept zu erreichen. In diesem Lernprogramm erfahren Sie, wie Sie auf Ihre Einzelhandelsdaten zugreifen und diese verstehen, ein Modell für maschinelles Lernen erstellen und optimieren und Einblicke in Data Science Workspace generieren können.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 2%

---

# Erstellen und Veröffentlichen eines Modells für maschinelles Lernen

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

- Zugriff auf [!DNL Adobe Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich bitte an Ihren Systemadministrator, bevor Sie fortfahren.

- Aktivieren von Assets. Wenden Sie sich an Ihren Kundenbetreuer, um die folgenden Punkte für Sie bereitzustellen.
   - Recommendations Rezept
   - Recommendations Input DataSet
   - Recommendations Input Schema
   - Recommendations Output DataSet
   - Recommendations Output Schema
   - Golden Data Set postValues
   - Goldenes Datenset-Schema

- Laden Sie die drei erforderlichen [!DNL Jupyter Notebook]-Dateien aus dem Ordner [Adobe public [!DNL Git] repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs) herunter. Anhand dieser Dateien wird der [!DNL JupyterLab]-Arbeitsablauf in [!DNL Data Science Workspace] veranschaulicht.

Ein Verständnis der folgenden Schlüsselkonzepte, die in diesem Tutorial verwendet werden:
- [[!DNL Experience Data Model]](../../xdm/home.md): Der durch die Adobe zur Definition von Standard-Schemas wie  [!DNL Profile] und ExperienceEvent für Customer Experience Management angeführte Standardisierungsaufwand.
- Datensätze: Ein Datenspeicherung- und Verwaltungskonstrukt für tatsächliche Daten. Eine physische instanziierte Instanz eines [XDM-Schemas](../../xdm/schema/field-dictionary.md).
- Stapel: Datensätze bestehen aus Stapeln. Ein Stapel ist ein Datensatz, der über einen bestimmten Zeitraum erfasst und als eine Einheit verarbeitet wird.
- [!DNL JupyterLab]:  [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) ist eine Open-Source Web-basierte Schnittstelle für Project  [!DNL Jupyter] und ist eng in  [!DNL Experience Platform].

## Vorbereiten der Daten {#prepare-your-data}

Um ein Modell für maschinelles Lernen zu erstellen, das Ihren Kunden personalisierte Produktempfehlungen zukommen lässt, müssen frühere Käufe auf Ihrer Website analysiert werden. In diesem Abschnitt wird untersucht, wie diese Daten in [!DNL Platform] bis [!DNL Adobe Analytics] eingehen und wie diese Daten in ein Funktionsdatensatz umgewandelt werden, das von Ihrem maschinellen Lernmodell verwendet werden soll.

### Daten und Schemas

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Datensätze]**, um alle vorhandenen Datensätze Liste, und wählen Sie den Datensatz aus, den Sie untersuchen möchten. In diesem Fall der Datensatz [!DNL Analytics] **Goldener Datensatz postValues**.

![](../images/models-recipes/model-walkthrough/dataset-browse.png)

Die Seite zur Aktivität des Datensatzes wird geöffnet und enthält Informationen zu Ihrem Datensatz. Sie können **[!UICONTROL Vorschau DataSet]** oben rechts auswählen, um Beispieldatensätze zu prüfen. Sie können auch das Schema für den ausgewählten Datensatz Ansicht haben. Wählen Sie den Link Schema in der rechten Leiste aus. Es wird ein Popup angezeigt, in dem Sie den Link unter **[!UICONTROL Schema]** auswählen, um das Schema in einer neuen Registerkarte zu öffnen.

![](../images/models-recipes/model-walkthrough/dataset-activity.png)


![](../images/models-recipes/model-walkthrough/schema-view.png)

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

Navigieren Sie in der Experience Platform zu **[!UICONTROL Modelle]** aus der linken Navigationsspalte und wählen Sie **[!UICONTROL Rezepte]** in der oberen Navigation aus, um eine Liste der verfügbaren Rezepte für Ihr Unternehmen Ansicht.

![](../images/models-recipes/model-walkthrough/recipe-tab.png)

Suchen und öffnen Sie dann das bereitgestellte **[!UICONTROL Recommendations Rezept]**, indem Sie den Namen auswählen. Die Übersichtsseite &quot;Rezept&quot;wird angezeigt.

![](../images/models-recipes/model-walkthrough/Recipe-view.png)

Wählen Sie dann in der rechten Leiste **[!UICONTROL Recommendations Input Schema]** aus, um das Schema mit dem Skript Ansicht. Die Schema-Felder &quot;[!UICONTROL itemId]&quot;und &quot;[!UICONTROL userId]&quot;entsprechen einem Produkt, das von diesem Kunden zu einem bestimmten Zeitpunkt gekauft wurde ([!UICONTROL interactionType]) ([!UICONTROL timestamp]). Führen Sie die gleichen Schritte aus, um die Felder für das **[!UICONTROL Recommendations Output Schema]** zu überprüfen.

![](../images/models-recipes/model-walkthrough/input-output.png)

Sie haben jetzt die Eingabe- und Ausgabedateien geprüft, die für das Produkt Recommendations Rezept erforderlich sind. Fahren Sie mit dem nächsten Abschnitt fort, um zu erfahren, wie Sie ein Recommendations-Produktmodell erstellen, ausbilden und bewerten.

## Schulung und Auswertung Ihres Modells {#train-and-evaluate-your-model}

Nachdem Ihre Daten vorbereitet wurden und das Rezept fertig ist, können Sie Ihr maschinelles Lernmodell erstellen, ausbilden und auswerten.

### Modell erstellen

Ein Modell ist eine Instanz eines Rezeptes, mit dem Sie mit Daten im Maßstab trainieren und bewerten können.

Navigieren Sie in der Experience Platform zu **[!UICONTROL Modelle]** aus der linken Navigationsspalte und wählen Sie **[!UICONTROL Rezepte]** in der oberen Navigationsleiste aus. Dadurch wird eine Liste der verfügbaren Rezepte für Ihr Unternehmen angezeigt.Wählen Sie das Rezept für die Produktempfehlung aus.

![](../images/models-recipes/model-walkthrough/recipe-tab.png)

Wählen Sie auf der Rezeptseite **[!UICONTROL Modell erstellen]**.

![Modell erstellen](../images/models-recipes/model-walkthrough/create-model-recipe.png)

Der Arbeitsablauf zum Erstellen eines Modells beginnt mit der Auswahl eines Rezepts. Wählen Sie das Rezept **[!UICONTROL Recommendations]** und klicken Sie dann auf **[!UICONTROL Weiter]** in der oberen rechten Ecke.

![](../images/models-recipes/model-walkthrough/create-model.png)

Geben Sie als Nächstes einen Modellnamen ein. Die verfügbaren Konfigurationen für das Modell werden mit den Einstellungen für das standardmäßige Schulungs- und Bewertungsverhalten des Modells aufgeführt. Überprüfen Sie die Konfigurationen und wählen Sie **[!UICONTROL Fertigstellen]**.

![](../images/models-recipes/model-walkthrough/configure-model.png)

Sie werden mit einem neu erstellten Schulungslauf auf Ihre Modellübersichtsseite umgeleitet. Beim Erstellen eines Modells wird standardmäßig ein Schulungslauf generiert.

![](../images/models-recipes/model-walkthrough/model-overview.png)

Sie können auf den Abschluss des Schulungslaufs warten oder im folgenden Abschnitt eine neue Schulungsausführung erstellen.

### Modell mithilfe benutzerdefinierter Hyperparameter trainieren

Wählen Sie auf der Seite **Modellübersicht** **[!UICONTROL Train]** oben rechts aus, um einen neuen Schulungslauf zu erstellen. Wählen Sie denselben Eingabedatensatz, den Sie beim Erstellen des Modells verwendet haben, und wählen Sie **[!UICONTROL Weiter]**.

![](../images/models-recipes/model-walkthrough/select-train.png)

Die Seite **[!UICONTROL Konfiguration]** wird angezeigt. Hier können Sie den Wert `num_recommendations` der Schulung konfigurieren, auch als Hyperparameter bezeichnet. Ein geschultes und optimiertes Modell verwendet die leistungsstärksten Hyperparameter, die auf den Ergebnissen der Schulungsausführung basieren.

Hyperparameter können nicht erlernt werden, daher müssen sie vor Schulungsdurchläufen zugewiesen werden. Durch Anpassen von Hyperparametern kann sich die Genauigkeit des geschulten Modells ändern. Da die Optimierung eines Modells ein iterativer Prozess ist, kann es erforderlich sein, dass mehrere Schulungen durchgeführt werden, bevor eine zufriedenstellende Bewertung erreicht wird.

>[!TIP]
>
>Setzen Sie `num_recommendations` auf 10.

![](../images/models-recipes/model-walkthrough/training-configuration.png)

Zusätzliche Datenpunkte werden im Modellbewertungsdiagramm angezeigt. Es kann bis zu mehreren Minuten dauern, bis dies nach Abschluss des Vorgangs angezeigt wird.

![](../images/models-recipes/model-walkthrough/training-graphs.png)

### Modell bewerten

Bei jedem Abschluss eines Schulungslaufs können Sie die resultierenden Bewertungsmetriken zur Ansicht der Leistung des Modells festlegen.

Um die Bewertungsmetriken (Präzision und Rückruf) für jeden abgeschlossenen Schulungslauf zu überprüfen, wählen Sie den Schulungslauf aus.

![](../images/models-recipes/model-walkthrough/select-training-run.png)

Sie können die Informationen zu den einzelnen Bewertungsmetriken untersuchen. Je höher diese Metriken sind, desto besser hat das Modell abgeschnitten.

![](../images/models-recipes/model-walkthrough/metrics.png)

Sie können den Datensatz, das Schema und die Konfigurationsparameter anzeigen, die für jeden Schulungslauf auf der rechten Leiste verwendet werden. Navigieren Sie zurück zur Modellseite und identifizieren Sie die Schulungen mit der höchsten Leistung, indem Sie deren Bewertungsmetriken beobachten.

## Operationalisieren Sie Ihr Modell {#operationalize-your-model}

Der letzte Schritt im Data Science-Arbeitsablauf besteht darin, Ihr Modell zu operieren, um Erkenntnisse aus Ihrem Datenspeicher zu bewerten und zu nutzen.

### Bewertung und Erstellung von Einblicken

Wählen Sie auf der Übersichtsseite des Produktempfehlungsmodells den Namen des Schulungslaufs mit den höchsten Rückruf- und Präzisionswerten aus, der die beste Leistung erzielt.

![die beste Ausführung](../images/models-recipes/model-walkthrough/select-training-run.png)

Wählen Sie dann oben rechts auf der Seite mit den Details zum Schulungslauf **[!UICONTROL Ergebnis]**.

![Wert auswählen](../images/models-recipes/model-walkthrough/select-score.png)

Wählen Sie anschließend den **[!UICONTROL Recommendations Input DataSet]** als Scoring-Eingabedataset aus, der mit dem Datensatz übereinstimmt, den Sie beim Erstellen des Modells und Ausführen der zugehörigen Schulungen verwendet haben. Wählen Sie dann **[!UICONTROL Weiter]**.

![](../images/models-recipes/model-walkthrough/score-input.png)

Sobald Sie über Ihren Eingabedatensatz verfügen, wählen Sie den Eintrag **[!UICONTROL Recommendations Output DataSet]** als Scoring-Ausgabedataset aus. Die Bewertungsergebnisse werden in diesem Datensatz als Stapel gespeichert.

![](../images/models-recipes/model-walkthrough/score-output.png)

Überprüfen Sie abschließend die Bewertungskonfigurationen. Diese Parameter enthalten die zuvor ausgewählten Eingabe- und Ausgabedatasets zusammen mit den entsprechenden Schemas. Wählen Sie **[!UICONTROL Fertig stellen]**, um den Bewertungsvorgang zu starten. Die Ausführung kann mehrere Minuten dauern.

![](../images/models-recipes/model-walkthrough/score-finish.png)

### Ansicht erzielte Einblicke

Nach erfolgreichem Abschluss der Bewertungsausführung können Sie die Ergebnisse Vorschau und Ansicht der gewonnenen Erkenntnisse vornehmen.

Wählen Sie auf der Seite mit den Scoring-Vorgängen die abgeschlossene Scoring-Ausführung und dann **[!UICONTROL Vorschau Scoring Results Dataset]** auf der rechten Leiste aus.

![](../images/models-recipes/model-walkthrough/preview-scores.png)

In der Tabelle &quot;Vorschau&quot;enthält jede Zeile Produktempfehlungen für einen bestimmten Kunden mit der Bezeichnung [!UICONTROL recommendations] bzw. [!UICONTROL userId]. Da der Hyperparameter [!UICONTROL num_recommendations] in den Screenshots der Beispiele auf 10 gesetzt wurde, kann jede Empfehlungszeile bis zu 10 Produktidentitäten mit einem Nummernzeichen (#) enthalten.

![](../images/models-recipes/model-walkthrough/preview_score_results.png)

## Nächste Schritte {#next-steps}

In diesem Lernprogramm wurde der Arbeitsablauf von [!DNL Data Science Workspace] vorgestellt, in dem gezeigt wird, wie unverarbeitete Rohdaten durch maschinelles Lernen in nützliche Informationen umgewandelt werden können. Um mehr über die Verwendung von [!DNL Data Science Workspace] zu erfahren, fahren Sie mit der nächsten Anleitung zu [Erstellen des Schemas und Datensatzes für den Einzelhandel](./create-retails-sales-dataset.md) fort.
