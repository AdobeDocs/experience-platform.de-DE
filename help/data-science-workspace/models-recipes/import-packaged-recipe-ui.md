---
keywords: Experience Platform;Gepacktes Rezept importieren;Datenwissenschafts-Workspace;beliebte Themen;Rezepte;Benutzeroberfläche;Engine erstellen
solution: Experience Platform
title: Importieren eines gepackten Rezepts in die Data Science Workspace-Benutzeroberfläche
type: Tutorial
description: Dieses Tutorial bietet Einblicke in das Konfigurieren und Importieren eines gepackten Rezepts mit dem bereitgestellten Beispiel für Einzelhandelsumsätze. Nach Abschluss dieses Tutorials können Sie ein Modell in Adobe Experience Platform Data Science Workspace erstellen, trainieren und auswerten.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 32%

---

# Importieren eines gepackten Rezepts in die Data Science Workspace-Benutzeroberfläche

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Dieses Tutorial bietet Einblicke in das Konfigurieren und Importieren eines gepackten Rezepts mit dem bereitgestellten Beispiel für Einzelhandelsumsätze. Am Ende dieses Tutorials sind Sie bereit, ein Modell in Adobe Experience Platform [!DNL Data Science Workspace] zu erstellen, zu trainieren und auszuwerten.

## Voraussetzungen

Für dieses Tutorial ist ein gepacktes Rezept in Form einer Docker-Bild-URL erforderlich. Weiterführende Informationen finden Sie im Tutorial zum [Verpacken von Quelldateien in einem Rezept](./package-source-files-recipe.md).

## Workflow in der Benutzeroberfläche

Das Importieren eines gepackten Rezepts in [!DNL Data Science Workspace] erfordert spezifische Rezepturkonfigurationen, die in eine einzige JavaScript Object Notation (JSON)-Datei kompiliert werden. Diese Kompilierung von Rezepturkonfigurationen wird als Konfigurationsdatei bezeichnet. Ein gepacktes Rezept mit einem bestimmten Satz von Konfigurationen wird als Rezeptinstanz bezeichnet. Ein Rezept kann verwendet werden, um viele Rezeptinstanzen in [!DNL Data Science Workspace] zu erstellen.

Der Workflow zum Importieren eines gepackten Rezepts umfasst folgende Schritte:
- [Konfigurieren eines Rezepts](#configure)
- [Docker-basiertes Rezept importieren - Python](#python)
- [Docker-basiertes Rezept importieren - R](#r)
- [Docker-basiertes Rezept importieren - PySpark](#pyspark)
- [Docker-basiertes Rezept importieren - Scala](#scala)

### Konfigurieren eines Rezepts {#configure}

Jeder Rezeptinstanz in [!DNL Data Science Workspace] wird eine Reihe von Konfigurationen hinzugefügt, die die Rezeptinstanz an einen bestimmten Anwendungsfall anpassen. Konfigurationsdateien definieren das standardmäßige Trainings- und Scoring-Verhalten eines mit dieser Rezeptinstanz erstellten Modells.

>[!NOTE]
>
>Konfigurationsdateien sind rezeptspezifisch und fallspezifisch.

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
| `tenantId` | Zeichenfolge | Diese ID stellt sicher, dass die von Ihnen erstellten Ressourcen über einen ordnungsgemäßen Namespace verfügen und in Ihrer Organisation enthalten sind. [Gehen Sie wie folgt vor](../../xdm/api/getting-started.md#know-your-tenant_id), um Ihre Mandantenkennung zu suchen. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Zeichenfolge | Das zum Trainieren eines Modells verwendete Eingabeschema. Lassen Sie es beim Importieren in der Benutzeroberfläche leer; ersetzen Sie es beim Importieren mit der API durch die Trainings-SchemaID. |
| `evaluation.labelColumn` | Zeichenfolge | Spaltenbezeichnung für Auswertungsvisualisierungen. |
| `evaluation.metrics` | Zeichenfolge | Kommagetrennte Liste mit Auswertungsmetriken, die zur Auswertung eines Modells verwendet werden. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Zeichenfolge | Das zum Scoring eines Modells verwendete Ausgabeschema. Lassen Sie es beim Importieren in der Benutzeroberfläche leer; ersetzen Sie es beim Importieren mit der API durch die Scoring-SchemaID. |

Für die Zwecke dieses Tutorials können Sie die Standardkonfigurationsdateien für das Rezept „Einzelhandel“ in der [!DNL Data Science Workspace]-Referenz unverändert lassen.

### Docker-basiertes Rezept importieren - [!DNL Python] {#python}

Navigieren Sie zunächst zu und wählen **[!UICONTROL Workflows]** oben links in der [!DNL Experience Platform]-Benutzeroberfläche aus. Wählen Sie als Nächstes **Rezept importieren** und wählen Sie **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die **Konfigurieren** für den Workflow **Rezept importieren** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke.

![Workflow konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md) wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit Python-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle auswählen** befinden, fügen Sie die Docker-URL, die dem gepackten Rezept entspricht, das mit [!DNL Python] Quelldateien erstellt wurde, in das Feld **[!UICONTROL Source-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Wählen Sie **[!UICONTROL Python]** in der **Laufzeit** Dropdown-Liste und **[!UICONTROL Klassifizierung]** in der **Typ** Dropdown-Liste aus. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke, um mit &quot;**verwalten“**.

>[!NOTE]
>
> Der Typ unterstützt **[!UICONTROL Klassifizierung]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Wählen Sie als Nächstes die Ein- und Ausgabeschemata für den Einzelhandel unter dem Abschnitt **Schemata verwalten** aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Tutorial [Erstellen des Schemas und Datensatzes für den Einzelhandel](../models-recipes/create-retails-sales-dataset.md) erstellt.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Wählen Sie im Abschnitt **Feature Management** im Schema-Viewer Ihre Mandanten-ID aus, um das Eingabeschema für Einzelhandelsumsätze zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Weiter]** aus, um Ihr neu konfiguriertes Rezept zu überprüfen.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **[!UICONTROL Beenden]**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie Sie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für Einzelhandelsumsätze erstellen.

### Docker-basiertes Rezept importieren - R {#r}

Navigieren Sie zunächst zu und wählen **[!UICONTROL Workflows]** oben links in der [!DNL Experience Platform]-Benutzeroberfläche aus. Wählen Sie als Nächstes **Rezept importieren** und wählen Sie **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die **Konfigurieren** für den Workflow **Rezept importieren** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke.

![Workflow konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md) wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit R-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle auswählen** befinden, fügen Sie die Docker-URL, die dem mit R-Quelldateien erstellten gepackten Rezept entspricht, in das Feld **[!UICONTROL Source-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Wählen Sie **[!UICONTROL R]** in der Dropdown **Liste** und **[!UICONTROL Klassifizierung]** in der Dropdown-Liste **Typ** aus. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke, um mit &quot;**verwalten“**.

>[!NOTE]
>
> *Type* unterstützt **[!UICONTROL Classification]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Wählen Sie als Nächstes die Ein- und Ausgabeschemata für den Einzelhandel unter dem Abschnitt **Schemata verwalten** aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Tutorial [Erstellen des Schemas und Datensatzes für den Einzelhandel](../models-recipes/create-retails-sales-dataset.md) erstellt.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Wählen Sie im Abschnitt *Feature Management* im Schema-Viewer Ihre Mandanten-ID aus, um das Eingabeschema für Einzelhandelsumsätze zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Weiter]** aus, um Ihr neues konfiguriertes Rezept zu überprüfen.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **Beenden**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie Sie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für Einzelhandelsumsätze erstellen.

### Docker-basiertes Rezept importieren - PySpark {#pyspark}

Navigieren Sie zunächst zu und wählen **[!UICONTROL Workflows]** oben links in der [!DNL Experience Platform]-Benutzeroberfläche aus. Wählen Sie als Nächstes **Rezept importieren** und wählen Sie **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die **Konfigurieren** für den Workflow **Rezept importieren** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke, um fortzufahren.

![Workflow konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Packen von Quelldateien in ein Rezept](./package-source-files-recipe.md) wurde am Ende der Erstellung des Rezepts für Einzelhandelsumsätze mit PySpark-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle auswählen** befinden, fügen Sie die Docker-URL, die dem gepackten Rezept entspricht, das mit PySpark-Quelldateien erstellt wurde, in das Feld **[!UICONTROL Source-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Wählen Sie **[!UICONTROL PySpark]** in der **Runtime** Dropdown-Liste aus. Sobald die PySpark-Laufzeit ausgewählt ist, wird das Standard-Artefakt automatisch mit &quot;**[!UICONTROL &quot;]**. Wählen Sie als Nächstes **[!UICONTROL Klassifizierung]** in der **Typ** Dropdown. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke, um mit &quot;**verwalten“**.

>[!NOTE]
>
> *Type* unterstützt **[!UICONTROL Classification]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Wählen Sie als Nächstes die Ein- und Ausgabeschemata für den Einzelhandel mit der Auswahl **Schemata verwalten** aus. Die Schemata wurden mithilfe des bereitgestellten Bootstrap-Skripts im Tutorial [Erstellen des Schemas und Datensatzes für den Einzelhandel](../models-recipes/create-retails-sales-dataset.md) erstellt.

![Schemata verwalten](../images/models-recipes/import-package-ui/manage-schemas.png)

Wählen Sie im Abschnitt **Feature Management** im Schema-Viewer Ihre Mandanten-ID aus, um das Eingabeschema für Einzelhandelsumsätze zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Weiter]** aus, um Ihr neu konfiguriertes Rezept zu überprüfen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **[!UICONTROL Beenden]**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie Sie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für Einzelhandelsumsätze erstellen.

### Docker-basiertes Rezept importieren - Scala {#scala}

Navigieren Sie zunächst zu und wählen **[!UICONTROL Workflows]** oben links in der [!DNL Experience Platform]-Benutzeroberfläche aus. Wählen Sie als Nächstes **Rezept importieren** und wählen Sie **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die **Konfigurieren** für den Workflow **Rezept importieren** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke, um fortzufahren.

![Workflow konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Packen von Quelldateien in ein Rezept](./package-source-files-recipe.md) wurde am Ende der Erstellung des Retail Sales-Rezepts mithilfe von Scala ([!DNL Spark])-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle auswählen** befinden, fügen Sie die Docker-URL, die dem gepackten Rezept entspricht, das mit Scala-Quelldateien erstellt wurde, in das Feld Source-URL ein. Importieren Sie als Nächstes die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder verwenden Sie den Dateisystem-Browser. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Wählen Sie **[!UICONTROL Spark]** in der **Runtime** Dropdown-Liste aus. Sobald die [!DNL Spark]-Laufzeit ausgewählt ist, wird das Standard-Artefakt automatisch mit &quot;**[!UICONTROL &quot;]**. Wählen Sie als Nächstes **[!UICONTROL Regression]** aus der **Typ** Dropdown. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** in der oberen rechten Ecke, um mit &quot;**verwalten“**.

>[!NOTE]
>
> Der Typ unterstützt **[!UICONTROL Klassifizierung]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Wählen Sie als Nächstes die Ein- und Ausgabeschemata für den Einzelhandel mit der Auswahl **Schemata verwalten** aus. Die Schemata wurden mithilfe des bereitgestellten Bootstrap-Skripts im Tutorial [Erstellen des Schemas und Datensatzes für den Einzelhandel](../models-recipes/create-retails-sales-dataset.md) erstellt.

![Schemata verwalten](../images/models-recipes/import-package-ui/manage-schemas.png)

Wählen Sie im Abschnitt **Feature Management** im Schema-Viewer Ihre Mandanten-ID aus, um das Eingabeschema für Einzelhandelsumsätze zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie für die Zwecke dieses Tutorials &quot;[!UICONTROL weeklySales]&quot; als **[!UICONTROL Target-Funktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Weiter]** aus, um Ihr neu konfiguriertes Rezept zu überprüfen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **[!UICONTROL Beenden]**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie Sie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für Einzelhandelsumsätze erstellen.

## Nächste Schritte {#next-steps}

In diesem Tutorial wurde insight über das Konfigurieren und Importieren eines Rezepts in [!DNL Data Science Workspace] informiert. Jetzt können Sie mit dem neu erstellten Rezept ein Modell erstellen, trainieren und auswerten.

- [Trainieren und Auswerten eines Modells in der Benutzeroberfläche](./train-evaluate-model-ui.md)
- [Trainieren und Auswerten eines Modells mithilfe der API](./train-evaluate-model-api.md)
