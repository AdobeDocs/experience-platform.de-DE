---
keywords: Experience Platform; verpacktes Rezept importieren; Data Science Workspace; beliebte Themen; Rezepte; ui; Engine erstellen
solution: Experience Platform
title: Importieren eines gepackten Rezepts in die Benutzeroberfläche von Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Dieses Tutorial bietet Einblicke in das Konfigurieren und Importieren eines gepackten Rezepts mit dem bereitgestellten Beispiel für Einzelhandelsumsätze. Nach Abschluss dieses Tutorials können Sie ein Modell in Adobe Experience Platform Data Science Workspace erstellen, trainieren und bewerten.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 37%

---

# Importieren eines gepackten Rezepts in die Benutzeroberfläche von Data Science Workspace

Dieses Tutorial bietet Einblicke in das Konfigurieren und Importieren eines gepackten Rezepts mit dem bereitgestellten Beispiel für Einzelhandelsumsätze. Am Ende dieses Tutorials können Sie ein Modell in Adobe Experience Platform [!DNL Data Science Workspace] erstellen, trainieren und bewerten.

## Voraussetzungen

Für dieses Tutorial ist ein gepacktes Rezept in Form einer Docker-Bild-URL erforderlich. Weiterführende Informationen finden Sie im Tutorial zum [Verpacken von Quelldateien in einem Rezept](./package-source-files-recipe.md).

## Workflow in der Benutzeroberfläche

Für das Importieren eines gepackten Rezepts in [!DNL Data Science Workspace] sind spezifische Rezeptkonfigurationen erforderlich, die in einer JSON-Datei (JavaScript Object Notation) kompiliert sind. Diese Kompilierung von Rezeptkonfigurationen wird als Konfigurationsdatei bezeichnet. Ein gepacktes Rezept mit einem bestimmten Satz von Konfigurationen wird als Rezeptinstanz bezeichnet. Ein Rezept kann verwendet werden, um viele Rezeptinstanzen in [!DNL Data Science Workspace] zu erstellen.

Der Workflow zum Importieren eines gepackten Rezepts umfasst folgende Schritte:
- [Rezept konfigurieren](#configure)
- [Docker-basiertes Rezept importieren – Python](#python)
- [Docker-basiertes Rezept importieren – R](#r)
- [Docker-basiertes Rezept importieren - PySpark](#pyspark)
- [Docker-basiertes Rezept importieren - Scala](#scala)

### Rezept konfigurieren {#configure}

Jede Rezeptinstanz in [!DNL Data Science Workspace] wird von einer Reihe von Konfigurationen begleitet, die die Rezeptinstanz an einen bestimmten Anwendungsfall anpassen. Konfigurationsdateien definieren das standardmäßige Trainings- und Scoring-Verhalten eines mit dieser Rezeptinstanz erstellten Modells.

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

Für diese Anleitung können Sie die Standardkonfigurationsdateien für das Rezept &quot;Einzelhandelsumsätze&quot;in der [!DNL Data Science Workspace]-Referenz so belassen, wie sie sind.

### Docker-basiertes Rezept importieren - [!DNL Python] {#python}

Beginnen Sie mit der Navigation und Auswahl von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] -Benutzeroberfläche. Wählen Sie als Nächstes **Rezept importieren** und dann **[!UICONTROL Launch]** aus.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite **Configure** für den Workflow **Import recipe** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke **[!UICONTROL Weiter]** aus.

![Workflow konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md) wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit Python-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle** auswählen befinden, fügen Sie die Docker-URL ein, die dem mit [!DNL Python]-Quelldateien erstellten gepackten Rezept entspricht, und zwar im Feld **[!UICONTROL Quell-URL]** . Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Wählen Sie **[!UICONTROL Python]** in der Dropdown-Liste **Runtime** und **[!UICONTROL Classification]** in der Dropdown-Liste **Typ** aus. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke aus, um mit **Schemas verwalten** fortzufahren.

>[!NOTE]
>
> Typ unterstützt **[!UICONTROL Klassifizierung]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]** aus.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Wählen Sie anschließend die Eingabe- und Ausgabeschemata für Einzelhandelsumsätze im Abschnitt **Schemas verwalten** aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Tutorial [Erstellen des Einzelhandelsschemas und -datensatzes](../models-recipes/create-retails-sales-dataset.md) erstellt.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Wählen Sie im Abschnitt **Funktionsverwaltung** im Schema-Viewer die Option zur Mandantenkennung aus, um das Eingabeschema für Einzelhandelsumsätze zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Next]** aus, um Ihr neues konfiguriertes Rezept zu überprüfen.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **[!UICONTROL Finish]** aus, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um zu erfahren, wie Sie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für Einzelhandelsumsätze erstellen.

### Docker-basiertes Rezept importieren – R {#r}

Beginnen Sie mit der Navigation und Auswahl von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] -Benutzeroberfläche. Wählen Sie als Nächstes **Rezept importieren** und dann **[!UICONTROL Launch]** aus.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite **Configure** für den Workflow **Import recipe** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke **[!UICONTROL Weiter]** aus.

![Workflow konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md) wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit R-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle** auswählen befinden, fügen Sie die Docker-URL ein, die dem mit R-Quelldateien erstellten gepackten Rezept entspricht, und zwar im Feld **[!UICONTROL Quell-URL]** . Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Wählen Sie **[!UICONTROL R]** in der Dropdown-Liste **Runtime** und **[!UICONTROL Classification]** in der Dropdown-Liste **Typ** aus. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke aus, um mit **Schemas verwalten** fortzufahren.

>[!NOTE]
>
> ** Typesupports  **** Classification und  **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]** aus.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Wählen Sie anschließend die Eingabe- und Ausgabeschemata für Einzelhandelsumsätze im Abschnitt **Schemas verwalten** aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Tutorial [Erstellen des Einzelhandelsschemas und -datensatzes](../models-recipes/create-retails-sales-dataset.md) erstellt.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Wählen Sie im Abschnitt *Funktionsverwaltung* im Schema-Viewer die Option zur Mandantenkennung aus, um das Eingabeschema für Einzelhandelsumsätze zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Next]** aus, um Ihr neues konfiguriertes Rezept zu überprüfen.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **Finish** aus, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um zu erfahren, wie Sie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für Einzelhandelsumsätze erstellen.

### Docker-basiertes Rezept importieren - PySpark {#pyspark}

Beginnen Sie mit der Navigation und Auswahl von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] -Benutzeroberfläche. Wählen Sie als Nächstes **Rezept importieren** und dann **[!UICONTROL Launch]** aus.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite **Configure** für den Workflow **Import recipe** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann **[!UICONTROL Weiter]** in der oberen rechten Ecke aus, um fortzufahren.

![Workflow konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept](./package-source-files-recipe.md) verpacken wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit PySpark-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle** auswählen befinden, fügen Sie die Docker-URL, die dem mit PySpark-Quelldateien erstellten gepackten Rezept entspricht, in das Feld **[!UICONTROL Quell-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Wählen Sie **[!UICONTROL PySpark]** in der Dropdown-Liste **Runtime** aus. Sobald die PySpark-Laufzeitumgebung ausgewählt ist, wird das standardmäßige Artefakt automatisch in **[!UICONTROL Docker]** eingefügt. Wählen Sie anschließend **[!UICONTROL Klassifizierung]** in der Dropdown-Liste **Typ** aus. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke aus, um mit **Schemas verwalten** fortzufahren.

>[!NOTE]
>
> ** Typesupports  **** Classification und  **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]** aus.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Wählen Sie anschließend mithilfe des Selektors **Schemas verwalten** die Eingabe- und Ausgabeschemata für Einzelhandelsumsätze aus. Die Schemas wurden mithilfe des im Tutorial [Erstellen des Schemas und Datensatzes](../models-recipes/create-retails-sales-dataset.md) bereitgestellten Bootstrap-Skripts erstellt.

![Schemas verwalten](../images/models-recipes/import-package-ui/manage-schemas.png)

Wählen Sie im Abschnitt **Funktionsverwaltung** im Schema-Viewer die Option zur Mandantenkennung aus, um das Eingabeschema für Einzelhandelsumsätze zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Next]** aus, um Ihr neues konfiguriertes Rezept zu überprüfen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **[!UICONTROL Finish]** aus, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um zu erfahren, wie Sie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für Einzelhandelsumsätze erstellen.

### Docker-basiertes Rezept importieren - Scala {#scala}

Beginnen Sie mit der Navigation und Auswahl von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] -Benutzeroberfläche. Wählen Sie als Nächstes **Rezept importieren** und dann **[!UICONTROL Launch]** aus.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite **Configure** für den Workflow **Import recipe** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann **[!UICONTROL Weiter]** in der oberen rechten Ecke aus, um fortzufahren.

![Workflow konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept](./package-source-files-recipe.md) verpacken wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit Scala-Quelldateien ([!DNL Spark]) eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle** auswählen befinden, fügen Sie die Docker-URL ein, die dem mit Scala-Quelldateien erstellten gepackten Rezept entspricht, und zwar im Feld Quell-URL . Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem Browser des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Wählen Sie **[!UICONTROL Spark]** in der Dropdown-Liste **Runtime** aus. Sobald die [!DNL Spark]-Laufzeitumgebung ausgewählt ist, wird das standardmäßige Artefakt automatisch in **[!UICONTROL Docker]** eingefügt. Wählen Sie als Nächstes **[!UICONTROL Regression]** aus der Dropdown-Liste **Typ** aus. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke aus, um mit **Schemas verwalten** fortzufahren.

>[!NOTE]
>
> Typ unterstützt **[!UICONTROL Klassifizierung]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]** aus.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Wählen Sie anschließend mithilfe des Selektors **Schemas verwalten** die Eingabe- und Ausgabeschemata für Einzelhandelsumsätze aus. Die Schemas wurden mithilfe des im Tutorial [Erstellen des Schemas und Datensatzes](../models-recipes/create-retails-sales-dataset.md) bereitgestellten Bootstrap-Skripts erstellt.

![Schemas verwalten](../images/models-recipes/import-package-ui/manage-schemas.png)

Wählen Sie im Abschnitt **Funktionsverwaltung** im Schema-Viewer die Option zur Mandantenkennung aus, um das Eingabeschema für Einzelhandelsumsätze zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie für diese Anleitung &quot;[!UICONTROL weeklySales]&quot;als **[!UICONTROL Target-Funktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Next]** aus, um Ihr neues konfiguriertes Rezept zu überprüfen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **[!UICONTROL Finish]** aus, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um zu erfahren, wie Sie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für Einzelhandelsumsätze erstellen.

## Nächste Schritte {#next-steps}

Dieses Tutorial bietet Einblicke in die Konfiguration und den Import eines Rezepts in [!DNL Data Science Workspace]. Jetzt können Sie mit dem neu erstellten Rezept ein Modell erstellen, trainieren und bewerten.

- [Modell in der Benutzeroberfläche trainieren und bewerten](./train-evaluate-model-ui.md)
- [Modell mithilfe der API trainieren und bewerten](./train-evaluate-model-api.md)
