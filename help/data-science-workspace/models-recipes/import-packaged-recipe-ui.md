---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics;recipes;ui;create engine
solution: Experience Platform
title: Gepacktes Rezept importieren (Benutzeroberfläche)
topic: tutorial
type: Tutorial
description: Dieses Tutorial bietet Einblicke in das Konfigurieren und Importieren eines gepackten Rezepts mit dem bereitgestellten Beispiel für Einzelhandelsumsätze. Nach Abschluss dieses Tutorials können Sie ein Modell in Adobe Experience Platform Data Science Workspace erstellen, trainieren und bewerten.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 41%

---


# Gepacktes Rezept importieren (Benutzeroberfläche)

Dieses Tutorial bietet Einblicke in das Konfigurieren und Importieren eines gepackten Rezepts mit dem bereitgestellten Beispiel für Einzelhandelsumsätze. By the end of this tutorial, you will be ready to create, train, and evaluate a Model in Adobe Experience Platform [!DNL Data Science Workspace].

## Voraussetzungen 

Dieses Lernprogramm erfordert ein gepacktes Rezept in Form einer Docker-Bild-URL. Weiterführende Informationen finden Sie im Tutorial zum [Verpacken von Quelldateien in einem Rezept](./package-source-files-recipe.md).

## Workflow in der Benutzeroberfläche

Importing a packaged recipe into [!DNL Data Science Workspace] requires specific recipe configurations, compiled into a single JavaScript Object Notation (JSON) file, this compilation of recipe configurations is referred to as the configuration file. Ein gepacktes Rezept mit einem bestimmten Satz von Konfigurationen wird als Rezeptinstanz bezeichnet. One recipe can be used to create many recipe instances in [!DNL Data Science Workspace].

Der Workflow zum Importieren eines gepackten Rezepts umfasst folgende Schritte:
- [Rezept konfigurieren](#configure)
- [Docker-basiertes Rezept importieren – Python](#python)
- [Docker-basiertes Rezept importieren – R](#r)
- [Docker-basiertes Rezept importieren - PySpark](#pyspark)
- [Docker-basiertes Rezept importieren - Scala](#scala)

### Rezept konfigurieren {#configure}

Every recipe instance in [!DNL Data Science Workspace] is accompanied with a set of configurations that tailor the recipe instance to suit a particular use case. Konfigurationsdateien definieren das standardmäßige Trainings- und Scoring-Verhalten eines mit dieser Rezeptinstanz erstellten Modells.

>[!NOTE]
>
>Konfigurationsdateien sind rezept- und fallspezifisch.

Im Folgenden finden Sie eine Beispielkonfigurationsdatei mit standardmäßigem Trainings- und Scoring-Verhalten für das Rezept „Einzelhandelsumsätze“.

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
| `learning_rate` | Zahl | Skalar für graduelle Multiplikation. |
| `n_estimators` | Zahl | Zahl der Bäume im Wald für Random Forest Classifier. |
| `max_depth` | Zahl | Maximale Tiefe eines Baums in Random Forest Classifier. |
| `ACP_DSW_INPUT_FEATURES` | Zeichenfolge | Liste mit kommagetrennten Eingabeschemaattributen. |
| `ACP_DSW_TARGET_FEATURES` | Zeichenfolge | Liste mit kommagetrennten Ausgabeschemaattributen. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolesch | Legt fest, ob Eingabe- und Ausgabefunktionen geändert werden können. |
| `tenantId` | Zeichenfolge | Diese Kennung stellt sicher, dass die von Ihnen erstellten Ressourcen den richtigen Namespace erhalten und in Ihrer IMS-Organisation enthalten sind. [Gehen Sie wie folgt vor](../../xdm/api/getting-started.md#know-your-tenant_id), um Ihre Mandantenkennung zu suchen. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Zeichenfolge | Das zum Trainieren eines Modells verwendete Eingabeschema. Lassen Sie es beim Importieren in der Benutzeroberfläche leer; ersetzen Sie es beim Importieren mit der API durch die Trainings-SchemaID. |
| `evaluation.labelColumn` | Zeichenfolge | Spaltenbezeichnung für Bewertungsvisualisierungen. |
| `evaluation.metrics` | Zeichenfolge | Kommagetrennte Liste mit Bewertungsmetriken, die zur Bewertung eines Modells verwendet werden. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Zeichenfolge | Das zum Scoring eines Modells verwendete Ausgabeschema. Lassen Sie es beim Importieren in der Benutzeroberfläche leer; ersetzen Sie es beim Importieren mit der API durch die Scoring-SchemaID. |

For the purpose of this tutorial, you can leave the default configuration files for Retail Sales recipe in the [!DNL Data Science Workspace] Reference the way they are.

### Import Docker based recipe - [!DNL Python] {#python}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] Benutzeroberfläche. Wählen Sie als Nächstes **Rezept** importieren und klicken Sie auf **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; **Konfigurieren** &quot;für den Arbeitsablauf für **Skriptdateien** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **[!UICONTROL Weiter]** .

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md) wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit Python-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle **** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit [!DNL Python] Quelldateien erstellten gepackten Rezept in das Feld **[!UICONTROL Quell-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Wählen Sie **[!UICONTROL Python]** in der Dropdown-Liste **Laufzeit** und **[!UICONTROL Klassifizierung]** in der Dropdown-Liste **Typ** . Klicken Sie nach dem Ausfüllen auf **[!UICONTROL Weiter]** oben rechts, um mit &quot;Schema **verwalten&quot;fortzufahren**.

>[!NOTE]
>
> Typ unterstützt **[!UICONTROL Klassifizierung]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Next, select the Retail Sales input and output schemas under the section **Manage Schemas**, they were created using the provided bootstrap script in the [create the retail sales schema and dataset](../models-recipes/create-retails-sales-dataset.md) tutorial.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under the **Feature Management** section, click on your tenant identification in the schema viewer to expand the Retail Sales input schema. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Klicken Sie auf **[!UICONTROL Weiter]**, um Ihr neu konfiguriertes Rezept zu überprüfen.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Klicken Sie auf **[!UICONTROL Beenden]**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Proceed to the [next steps](#next-steps) to find out how to create a Model in [!DNL Data Science Workspace] using the newly created Retail Sales recipe.

### Docker-basiertes Rezept importieren – R {#r}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] Benutzeroberfläche. Wählen Sie als Nächstes **Rezept** importieren und klicken Sie auf **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; **Konfigurieren** &quot;für den Arbeitsablauf für **Skriptdateien** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **[!UICONTROL Weiter]** .

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md) wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit R-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle **** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit R-Quelldateien erstellten gepackten Rezept in das Feld **[!UICONTROL Quell-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Wählen Sie **[!UICONTROL R]** in der Dropdownliste **Laufzeit** und **[!UICONTROL Classification]** in der Dropdownliste **Typ** . Klicken Sie nach dem Ausfüllen auf **[!UICONTROL Weiter]** oben rechts, um mit &quot;Schema **verwalten&quot;fortzufahren**.

>[!NOTE]
>
> *Typ* unterstützt **[!UICONTROL Classification]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Next, select the Retail Sales input and output schemas under the section **Manage Schemas**, they were created using the provided bootstrap script in the [create the retail sales schema and dataset](../models-recipes/create-retails-sales-dataset.md) tutorial.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under the *Feature Management* section, click on your tenant identification in the schema viewer to expand the Retail Sales input schema. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Click **[!UICONTROL Next]** to review your new Configured recipe.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Klicken Sie auf **Beenden**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Proceed to the [next steps](#next-steps) to find out how to create a Model in [!DNL Data Science Workspace] using the newly created Retail Sales recipe.

### Import Docker based recipe - PySpark {#pyspark}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] Benutzeroberfläche. Wählen Sie als Nächstes **Rezept** importieren und klicken Sie auf **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; **Konfigurieren** &quot;für den Arbeitsablauf für **Skriptdateien** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **[!UICONTROL Weiter]** , um fortzufahren.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In the [Package source files into a Recipe](./package-source-files-recipe.md) tutorial, a Docker URL was provided at the end of building the Retail Sales recipe using PySpark source files.

Sobald Sie sich auf der Seite &quot;Quelle **** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit PySpark-Quelldateien erstellten gepackten Rezept in das Feld **[!UICONTROL Quell-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Wählen Sie **[!UICONTROL PySpark]** in der Dropdown-Liste **Laufzeit** . Sobald die PySpark-Laufzeit ausgewählt ist, wird das standardmäßige Artefakt automatisch in **[!UICONTROL Docker]** eingetragen. Wählen Sie anschließend **[!UICONTROL Klassifizierung]** in der Dropdown-Liste **Typ** . Klicken Sie nach dem Ausfüllen auf **[!UICONTROL Weiter]** oben rechts, um mit &quot;Schema **verwalten&quot;fortzufahren**.

>[!NOTE]
>
> *Typ* unterstützt **[!UICONTROL Classification]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Next, select the Retail Sales input and output schemas under the section **Manage Schemas**, they were created using the provided bootstrap script in the [create the retail sales schema and dataset](../models-recipes/create-retails-sales-dataset.md) tutorial.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under the **Feature Management** section, click on your tenant identification in the schema viewer to expand the Retail Sales input schema. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Klicken Sie auf **[!UICONTROL Weiter]**, um Ihr neu konfiguriertes Rezept zu überprüfen.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Klicken Sie auf **[!UICONTROL Beenden]**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Proceed to the [next steps](#next-steps) to find out how to create a Model in [!DNL Data Science Workspace] using the newly created Retail Sales recipe.

### Import Docker based recipe - Scala {#scala}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] Benutzeroberfläche. Wählen Sie als Nächstes **Rezept** importieren und klicken Sie auf **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; **Konfigurieren** &quot;für den Arbeitsablauf für **Skriptdateien** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **[!UICONTROL Weiter]** , um fortzufahren.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In the [Package source files into a Recipe](./package-source-files-recipe.md) tutorial, a Docker URL was provided at the end of building the Retail Sales recipe using Scala ([!DNL Spark]) source files.

Sobald Sie sich auf der Seite &quot;Quelle **** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit Scala-Quelldateien erstellten gepackten Rezept in das Feld &quot;Quell-URL&quot;ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem Browser des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Wählen Sie **[!UICONTROL Spark]** in der Dropdown-Liste **Laufzeit** . Nach Auswahl der [!DNL Spark] Laufzeitumgebung wird das standardmäßige Artefakt automatisch mit **[!UICONTROL Docker]** gefüllt. Wählen Sie dann **[!UICONTROL Regression]** aus der Dropdownliste **Typ** . Klicken Sie nach dem Ausfüllen auf **[!UICONTROL Weiter]** oben rechts, um mit &quot;Schema **verwalten&quot;fortzufahren**.

>[!NOTE]
>
> Typ unterstützt **[!UICONTROL Klassifizierung]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Next, select the Retail Sales input and output schemas under the section **Manage Schemas**, they were created using the provided bootstrap script in the [create the retail sales schema and dataset](../models-recipes/create-retails-sales-dataset.md) tutorial.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under the **Feature Management** section, click on your tenant identification in the schema viewer to expand the Retail Sales input schema. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. For the purpose of this tutorial, set &quot;[!UICONTROL weeklySales]&quot; as the  **[!UICONTROL Target Feature]** and everything else as **[!UICONTROL Input Feature]**. Klicken Sie auf **[!UICONTROL Weiter]**, um Ihr neu konfiguriertes Rezept zu überprüfen.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Klicken Sie auf **[!UICONTROL Beenden]**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Proceed to the [next steps](#next-steps) to find out how to create a Model in [!DNL Data Science Workspace] using the newly created Retail Sales recipe.

## Nächste Schritte {#next-steps}

This tutorial provided insight on configuring and importing a recipe into [!DNL Data Science Workspace]. Jetzt können Sie mit dem neu erstellten Rezept ein Modell erstellen, trainieren und bewerten.

- [Modell in der Benutzeroberfläche trainieren und bewerten](./train-evaluate-model-ui.md)
- [Modell mithilfe der API trainieren und bewerten](./train-evaluate-model-api.md)