---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Verpacktes Rezept importieren (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: a7db31793d33d4571a867f5632243c59b5cb7975

---


# Verpacktes Rezept importieren (UI)

Dieses Lernprogramm bietet einen Einblick in die Konfiguration und den Import eines gepackten Rezepts mithilfe des im Lieferumfang enthaltenen Verkaufsbeispiels. Am Ende dieses Lernprogramms sind Sie bereit, ein Modell in Adobe Experience Platform Data Science Workspace zu erstellen, auszubilden und zu bewerten.

## Voraussetzungen

Dieses Lernprogramm erfordert ein gepacktes Rezept in Form einer Docker-Bild-URL. Weitere Informationen finden Sie im Lernprogramm zum [Verpacken von Quelldateien in einem Rezept](./package-source-files-recipe.md) .

## Arbeitsablauf der Benutzeroberfläche

Für das Importieren eines gepackten Rezepts in Data Science Workspace sind spezifische Rezeptkonfigurationen erforderlich, die in einer einzigen JSON-Datei (JavaScript Object Notation) kompiliert sind. Diese Zusammenstellung von Rezeptkonfigurationen wird als **Konfigurationsdatei** bezeichnet. Ein gepacktes Rezept mit einem bestimmten Satz von Konfigurationen wird als **Rezept-Instanz** bezeichnet. Ein Rezept kann verwendet werden, um viele Rezeptinstanzen im Data Science Workspace zu erstellen.

Der Arbeitsablauf zum Importieren eines Paketrezepts besteht aus den folgenden Schritten:
- [Konfigurieren eines Rezepts](#configure)
- [Dockerbasiertes Rezept importieren - Python](#python)
- [Dockerbasiertes Rezept importieren - R](#r)
- [Docker-basiertes Rezept importieren - PySpark](#pyspark)
- [Docker-basiertes Rezept importieren - Scala](#scala)

Veraltete Workflows:
- [Binärbasiertes Rezept importieren - PySpark](#pyspark-deprecated)
- [Binärbasiertes Rezept importieren - Scala Spark](#scala-deprecated)

### Konfigurieren eines Rezepts {#configure}

Jede Skriptinstanz in Data Science Workspace wird mit einer Reihe von Konfigurationen begleitet, die die Rezepturinstanz an einen bestimmten Anwendungsfall anpassen. Konfigurationsdateien definieren die standardmäßigen Schulungs- und Bewertungsmethoden eines mit dieser Skriptinstanz erstellten Modells.

>[!NOTE] Konfigurationsdateien sind Rezept- und Fallspezifisch.

Im Folgenden finden Sie eine Beispielkonfigurationsdatei mit standardmäßigen Trainings- und Bewertungsverhaltensweisen für das Rezept Einzelhandel.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| Parameterschlüssel | Typ | Beschreibung |
| ----- | ----- | ----- |
| `learning_rate` | Zahl | Skalar für Verlaufsmultiplikation. |
| `n_estimators` | Zahl | Anzahl der Bäume im Wald für Random Forest Classifier. |
| `max_depth` | Zahl | Maximale Tiefe eines Baums in der Random Forest Classifier. |
| `ACP_DSW_INPUT_FEATURES` | Zeichenfolge | Liste von kommagetrennten Eingabe-Schema-Attributen. |
| `ACP_DSW_TARGET_FEATURES` | Zeichenfolge | Liste von kommagetrennten Schema-Attributen. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolesch | Bestimmt, ob Eingabe- und Ausgabefunktionen geändert werden können |
| `tenantId` | Zeichenfolge | Diese ID stellt sicher, dass die von Ihnen erstellten Ressourcen korrekt benannt und in Ihrer IMS-Organisation enthalten sind. [Gehen Sie wie folgt vor](../../xdm/api/getting-started.md#know-your-tenant_id) , um Ihre Mandanten-ID zu finden. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Zeichenfolge | Das für die Modellschulung verwendete Input-Schema. Lassen Sie diese Angabe beim Importieren in die Benutzeroberfläche leer. Ersetzen Sie sie beim Importieren mit der API durch die Schulung SchemaID. |
| `evaluation.labelColumn` | Zeichenfolge | Spaltenbeschriftung für Evaluierungsvisualisierungen. |
| `evaluation.metrics` | Zeichenfolge | Kommagetrennte Liste von Bewertungsmetriken, die für die Bewertung eines Modells verwendet werden. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Zeichenfolge | Das für das Scoring eines Schemas verwendete Ausgabemodell. Lassen Sie diese Angabe beim Importieren in die Benutzeroberfläche leer. Ersetzen Sie sie beim Importieren mit der API durch eine Bewertungsschema-ID. |

Für diese Übung können Sie die Standardkonfigurationsdateien für das Rezept Einzelhandel im Data Science Workspace-Referenzhandbuch wie gewünscht beibehalten.

### Dockerbasiertes Rezept importieren - Python {#python}

Beginn durch Navigieren und Auswählen von **Workflows** oben links in der Plattform-Benutzeroberfläche. Wählen Sie als Nächstes *Rezept* importieren und klicken Sie auf **Starten**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; *Konfigurieren* &quot;für den Arbeitsablauf für *Skriptdateien* wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **Weiter** .

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> In den Quelldateien [für das Verpacken in einem Rezept](./package-source-files-recipe.md) -Lernprogramm wurde am Ende der Erstellung des Retail Sales-Rezepts mit Python-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle ** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit Python-Quelldateien erstellten gepackten Rezept in das Feld **Quell-URL** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Wählen Sie **Python** in der Dropdown-Liste *Laufzeit* und **Klassifizierung** in der Dropdown-Liste *Typ* . Klicken Sie nach dem Ausfüllen auf **Weiter** oben rechts, um mit &quot;Schema *verwalten&quot;fortzufahren*.

>[!NOTE]
> *Typ *unterstützt **Classification**und **Regression**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **Benutzerdefiniert**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter &quot;Schema *verwalten*&quot;aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes für den Einzelhandel [erstellt](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicken Sie im Abschnitt *Funktionsverwaltung* auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **Feldeigenschaften&quot;entweder &quot;** Eingabefunktion **&quot;oder &quot;** Zielgruppe-Funktion **&quot;auswählen** . Legen Sie für diese Übung **weeklySales** als **Zielgruppe-Funktion** und alles andere als **Input-Funktion** fest. Klicken Sie auf **Weiter** , um Ihr neues konfiguriertes Rezept zu überprüfen.

Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **Fertig stellen** , um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in Data Science Workspace mit dem neu erstellten Rezept Einzelhandelsverkäufe erstellt wird.

### Dockerbasiertes Rezept importieren - R {#r}

Beginn durch Navigieren und Auswählen von **Workflows** oben links in der Plattform-Benutzeroberfläche. Wählen Sie als Nächstes *Rezept* importieren und klicken Sie auf **Starten**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; *Konfigurieren* &quot;für den Arbeitsablauf für *Skriptdateien* wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **Weiter** .

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> In den Quelldateien [für das Verpacken in einem Rezept](./package-source-files-recipe.md) -Lernprogramm wurde am Ende der Erstellung des Retail Sales-Rezepts mit R-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle ** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit R-Quelldateien erstellten gepackten Rezept in das Feld **Quell-URL** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Wählen Sie **R** in der Dropdownliste *Laufzeit* und **Classification** in der Dropdownliste *Typ* . Klicken Sie nach dem Ausfüllen auf **Weiter** oben rechts, um mit &quot;Schema *verwalten&quot;fortzufahren*.

>[!NOTE]
> *Typ *unterstützt **Classification**und **Regression**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **Benutzerdefiniert**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter &quot;Schema *verwalten*&quot;aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes für den Einzelhandel [erstellt](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicken Sie im Abschnitt *Funktionsverwaltung* auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **Feldeigenschaften&quot;entweder &quot;** Eingabefunktion **&quot;oder &quot;** Zielgruppe-Funktion **&quot;auswählen** . Legen Sie für diese Übung **weeklySales** als **Zielgruppe-Funktion** und alles andere als **Input-Funktion** fest. Klicken Sie auf **Weiter** , um Ihr neues konfiguriertes Rezept zu überprüfen.

Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **Fertig stellen** , um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in Data Science Workspace mit dem neu erstellten Rezept Einzelhandelsverkäufe erstellt wird.

### Docker-basiertes Rezept importieren - PySpark {#pyspark}

Beginn durch Navigieren und Auswählen von **Workflows** oben links in der Plattform-Benutzeroberfläche. Wählen Sie als Nächstes *Rezept* importieren und klicken Sie auf **Starten**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; *Konfigurieren* &quot;für den Arbeitsablauf für *Skriptdateien* wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **Weiter** , um fortzufahren.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> In der [Paketquellendatei in einem Rezept](./package-source-files-recipe.md) -Tutorial wurde am Ende der Erstellung des Retail Sales-Rezeptes mit PySpark-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle ** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit PySpark-Quelldateien erstellten gepackten Rezept in das Feld **Quell-URL** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Wählen Sie **PySpark** in der Dropdown-Liste *Laufzeit* . Sobald die PySpark-Laufzeit ausgewählt ist, wird das standardmäßige Artefakt automatisch in **Docker** eingetragen. Wählen Sie anschließend **Klassifizierung** in der Dropdown-Liste *Typ* . Klicken Sie nach dem Ausfüllen auf **Weiter** oben rechts, um mit &quot;Schema *verwalten&quot;fortzufahren*.

>[!NOTE]
> *Typ *unterstützt **Classification**und **Regression**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **Benutzerdefiniert**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter &quot;Schema *verwalten*&quot;aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes für den Einzelhandel [erstellt](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicken Sie im Abschnitt *Funktionsverwaltung* auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **Feldeigenschaften&quot;entweder &quot;** Eingabefunktion **&quot;oder &quot;** Zielgruppe-Funktion **&quot;auswählen** . Legen Sie für diese Übung **weeklySales** als **Zielgruppe-Funktion** und alles andere als **Input-Funktion** fest. Klicken Sie auf **Weiter** , um Ihr neues konfiguriertes Rezept zu überprüfen.

Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **Fertig stellen** , um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in Data Science Workspace mit dem neu erstellten Rezept Einzelhandelsverkäufe erstellt wird.

### Docker-basiertes Rezept importieren - Scala {#scala}

Beginn durch Navigieren und Auswählen von **Workflows** oben links in der Plattform-Benutzeroberfläche. Wählen Sie als Nächstes *Rezept* importieren und klicken Sie auf **Starten**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; *Konfigurieren* &quot;für den Arbeitsablauf für *Skriptdateien* wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **Weiter** , um fortzufahren.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> In der [Paketquellendatei in einem Rezept](./package-source-files-recipe.md) -Tutorial wurde am Ende der Erstellung des Retail Sales-Rezeptes mit Scala-Quelldateien (Spark) eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle ** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit Scala-Quelldateien erstellten gepackten Rezept in das Feld *Quell-URL* ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Wählen Sie **Spark** in der Dropdown-Liste *Laufzeit* . Nach Auswahl der Spark-Laufzeit wird das standardmäßige Artefakt automatisch mit **Docker** gefüllt. Wählen Sie dann **Regression** aus der Dropdownliste *Typ* . Klicken Sie nach dem Ausfüllen auf **Weiter** oben rechts, um mit &quot;Schema *verwalten&quot;fortzufahren*.

>[!NOTE]
> *Typ *unterstützt **Classification**und **Regression**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **Benutzerdefiniert**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter &quot;Schema *verwalten*&quot;aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes für den Einzelhandel [erstellt](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicken Sie im Abschnitt *Funktionsverwaltung* auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **Feldeigenschaften&quot;entweder &quot;** Eingabefunktion **&quot;oder &quot;** Zielgruppe-Funktion **&quot;auswählen** . Legen Sie für diese Übung **weeklySales** als **Zielgruppe-Funktion** und alles andere als **Input-Funktion** fest. Klicken Sie auf **Weiter** , um Ihr neues konfiguriertes Rezept zu überprüfen.

Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **Fertig stellen** , um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in Data Science Workspace mit dem neu erstellten Rezept Einzelhandelsverkäufe erstellt wird.

## Nächste Schritte

Dieses Lernprogramm bietet einen Einblick in die Konfiguration und den Import eines Skripts in Data Science Workspace. Sie können ein Modell jetzt mit dem neu erstellten Rezept erstellen, ausbilden und auswerten.

- [Erstellen und Auswerten eines Modells in der Benutzeroberfläche](./train-evaluate-model-ui.md)
- [Erstellen und Auswerten eines Modells mithilfe der API](./train-evaluate-model-api.md)

## Veraltete Workflows

>[!CAUTION]
>Das Importieren binärer Rezepte wird in PySpark 3 (Spark 2.4) und Scala (Spark 2.4) nicht mehr unterstützt.

### Binärbasiertes Rezept importieren - PySpark {#pyspark-deprecated}

In den Quelldateien [Package in ein Rezept](./package-source-files-recipe.md) -Lernprogramm wurde eine **EGG** -Binärdatei mithilfe der Quelldateien Retail Sales PySpark erstellt.

1. Suchen Sie in [Adobe Experience Platform](https://platform.adobe.com/)das linke Navigationsfenster und klicken Sie auf **Workflows**. Starten Sie auf der Workflows-Oberfläche einen neuen **Import-Vorgang für die Quelldatei****** .
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Geben Sie einen entsprechenden Namen für das Rezept Einzelhandelsverkäufe ein. Beispiel: &quot;Retail Sales recipe PySpark&quot;. Fügen Sie optional eine Beschreibung des Rezepts und eine Dokumentations-URL ein. Klicken Sie auf **Weiter** , wenn Sie fertig sind.
   ![](../images/models-recipes/import-package-ui/recipe_info.png)
3. Importieren Sie das PySpark Retail Sales-Rezept, das in den Quelldateien des [Pakets erstellt wurde, in ein Rezept](./package-source-files-recipe.md) -Tutorial, indem Sie per Drag &amp; Drop oder mithilfe des Dateisystem- **Browsers**. Das verpackte Rezept sollte sich in `experience-platform-dsw-reference/recipes/pyspark/dist`.
Importieren Sie die bereitgestellte Konfigurationsdatei auch per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/pyspark/pipeline.json`. Klicken Sie auf **Weiter** , wenn beide Dateien bereitgestellt wurden.
   ![](../images/models-recipes/import-package-ui/recipe_source.png)
4. An dieser Stelle können Fehler auftreten. Dies ist ein normales Verhalten und ist zu erwarten. Wählen Sie die Schemas für die Eingabe und Ausgabe im Einzelhandel unter **Verwalten von Schemas** aus. Sie wurden mithilfe des Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes [](../models-recipes/create-retails-sales-dataset.md) für den Einzelhandel erstellt.
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Klicken Sie im Abschnitt **Funktionsverwaltung** auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **Feldeigenschaften&quot;entweder &quot;** Eingabefunktion **&quot;oder &quot;** Zielgruppe-Funktion **&quot;auswählen** . Legen Sie für diese Übung **weeklySales** als **Zielgruppe-Funktion** und alles andere als **Input-Funktion** fest. Klicken Sie auf **Weiter** , um Ihr neues konfiguriertes Rezept zu überprüfen.
5. Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **Fertig stellen** , um das Rezept zu erstellen.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in Data Science Workspace mit dem neu erstellten Rezept Einzelhandelsverkäufe erstellt wird.


### Binärbasiertes Rezept importieren - Scala Spark {#scala-deprecated}

In den Quelldateien [Package in ein Rezept](./package-source-files-recipe.md) -Lernprogramm wurde eine **JAR** -Binärdatei mithilfe der Quelldateien Retail Sales Scala Spark erstellt.

1. Suchen Sie in [Adobe Experience Platform](https://platform.adobe.com/)das linke Navigationsfenster und klicken Sie auf **Workflows**. Starten Sie auf der Workflows-Oberfläche einen neuen **Import-Vorgang für die Quelldatei****** .
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Geben Sie einen entsprechenden Namen für das Rezept Einzelhandelsverkäufe ein. Beispiel: &quot;Retail Sales recipe Scala Spark&quot;. Fügen Sie optional eine Beschreibung des Rezepts und eine Dokumentations-URL ein. Klicken Sie auf **Weiter** , wenn Sie fertig sind.
   ![](../images/models-recipes/import-package-ui/recipe_info_scala.png)
3. Importieren Sie das Scala Spark Retail Sales-Rezept, das in den Quelldateien des [Pakets erstellt wurde, in ein Rezept](./package-source-files-recipe.md) -Tutorial, indem Sie per Drag &amp; Drop oder mithilfe des Dateisystem- **Browsers**. Das gepackte Rezept **mit Abhängigkeiten** befindet sich in `experience-platform-dsw-reference/recipes/scala/target`. Importieren Sie die bereitgestellte Konfigurationsdatei auch per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/scala/src/main/resources/pipelineservice.json`. Klicken Sie auf **Weiter** , wenn beide Dateien bereitgestellt wurden.
   ![](../images/models-recipes/import-package-ui/recipe_source_scala.png)
4. An dieser Stelle können Fehler auftreten. Dies ist ein normales Verhalten und ist zu erwarten. Wählen Sie die Schemas für die Eingabe und Ausgabe im Einzelhandel unter **Verwalten von Schemas** aus. Sie wurden mithilfe des Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes [](../models-recipes/create-retails-sales-dataset.md) für den Einzelhandel erstellt.
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Klicken Sie im Abschnitt **Funktionsverwaltung** auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **Feldeigenschaften&quot;entweder &quot;** Eingabefunktion **&quot;oder &quot;** Zielgruppe-Funktion **&quot;auswählen** . Legen Sie für diese Übung **weeklySales** als **Zielgruppe-Funktion** und alles andere als **Input-Funktion** fest. Klicken Sie auf **Weiter** , um Ihr neues konfiguriertes Rezept zu überprüfen.
5. Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **Fertig stellen** , um das Rezept zu erstellen.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in Data Science Workspace mit dem neu erstellten Rezept Einzelhandelsverkäufe erstellt wird.