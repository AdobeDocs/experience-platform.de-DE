---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Verpacktes Rezept importieren (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 0%

---


# Verpacktes Rezept importieren (UI)

Dieses Lernprogramm bietet einen Einblick in die Konfiguration und den Import eines gepackten Rezepts mithilfe des im Lieferumfang enthaltenen Verkaufsbeispiels. Am Ende dieses Lernprogramms sind Sie bereit, ein Modell in der Adobe Experience Platform zu erstellen, auszubilden und zu bewerten [!DNL Data Science Workspace].

## Voraussetzungen

Dieses Lernprogramm erfordert ein gepacktes Rezept in Form einer Docker-Bild-URL. Weitere Informationen finden Sie im Lernprogramm zum [Verpacken von Quelldateien in einem Rezept](./package-source-files-recipe.md) .

## Arbeitsablauf der Benutzeroberfläche

Für das Importieren eines gepackten Rezepts in eine [!DNL Data Science Workspace] Datei mit einer JavaScript Object Notation (JSON) sind spezifische Rezeptkonfigurationen erforderlich. Diese Kompilierung von Skriptkonfigurationen wird als **Konfigurationsdatei** bezeichnet. Ein gepacktes Rezept mit einem bestimmten Satz von Konfigurationen wird als **Rezept-Instanz** bezeichnet. Ein Rezept kann verwendet werden, um viele Rezept-Instanzen in zu erstellen [!DNL Data Science Workspace].

Der Arbeitsablauf zum Importieren eines Paketrezepts besteht aus den folgenden Schritten:
- [Konfigurieren eines Rezepts](#configure)
- [Dockerbasiertes Rezept importieren - Python](#python)
- [Dockerbasiertes Rezept importieren - R](#r)
- [Docker-basiertes Rezept importieren - PySpark](#pyspark)
- [Docker-basiertes Rezept importieren - Scala](#scala)

### Konfigurieren eines Rezepts {#configure}

Jede Rezept-Instanz in [!DNL Data Science Workspace] wird mit einer Reihe von Konfigurationen begleitet, die die Rezept-Instanz an einen bestimmten Anwendungsfall anpassen. Konfigurationsdateien definieren die standardmäßigen Schulungs- und Bewertungsmethoden eines mit dieser Skriptinstanz erstellten Modells.

>[!NOTE]
>
>Konfigurationsdateien sind Rezept- und Fallspezifisch.

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

Für diese Übung können Sie die Standardkonfigurationsdateien für das Rezept Einzelhandel in der [!DNL Data Science Workspace] Referenz so belassen, wie sie sind.

### Docker-basiertes Rezept importieren - [!DNL Python] {#python}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] Benutzeroberfläche. Wählen Sie als Nächstes *Rezept* importieren und klicken Sie auf **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; *Konfigurieren* &quot;für den Arbeitsablauf für *Skriptdateien* wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **[!UICONTROL Weiter]** .

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> In den Quelldateien [für das Verpacken in einem Rezept](./package-source-files-recipe.md) -Lernprogramm wurde am Ende der Erstellung des Retail Sales-Rezepts mit Python-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle ** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit [!DNL Python] Quelldateien erstellten gepackten Rezept in das Feld **[!UICONTROL Quell-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Wählen Sie **[!UICONTROL Python]** in der Dropdown-Liste *Laufzeit* und **[!UICONTROL Klassifizierung]** in der Dropdown-Liste *Typ* . Klicken Sie nach dem Ausfüllen auf **[!UICONTROL Weiter]** oben rechts, um mit &quot;Schema *verwalten&quot;fortzufahren*.

>[!NOTE]
> *Typ *unterstützt **[!UICONTROL Classification]**und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter &quot;Schema *verwalten*&quot;aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes für den Einzelhandel [erstellt](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicken Sie im Abschnitt *Funktionsverwaltung* auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **[!UICONTROL Feldeigenschaften&quot;entweder &quot;]** Eingabefunktion **[!UICONTROL &quot;oder &quot;]** Target-Funktion **[!UICONTROL &quot;auswählen]** . Legen Sie für diese Übung **[!UICONTROL weeklySales]** als **[!UICONTROL Target-Funktion]** und alles andere als **[!UICONTROL Input-Funktion]** fest. Klicken Sie auf **[!UICONTROL Weiter]** , um Ihr neues konfiguriertes Rezept zu überprüfen.

Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **[!UICONTROL Fertig stellen]** , um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell mit dem neu erstellten Vertriebsrezept [!DNL Data Science Workspace] für Einzelhändler erstellt wird.

### Dockerbasiertes Rezept importieren - R {#r}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] Benutzeroberfläche. Wählen Sie als Nächstes *Rezept* importieren und klicken Sie auf **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; *Konfigurieren* &quot;für den Arbeitsablauf für *Skriptdateien* wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **[!UICONTROL Weiter]** .

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> In den Quelldateien [für das Verpacken in einem Rezept](./package-source-files-recipe.md) -Lernprogramm wurde am Ende der Erstellung des Retail Sales-Rezepts mit R-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle ** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit R-Quelldateien erstellten gepackten Rezept in das Feld **[!UICONTROL Quell-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Wählen Sie **[!UICONTROL R]** in der Dropdownliste *Laufzeit* und **[!UICONTROL Classification]** in der Dropdownliste *Typ* . Klicken Sie nach dem Ausfüllen auf **[!UICONTROL Weiter]** oben rechts, um mit &quot;Schema *verwalten&quot;fortzufahren*.

>[!NOTE]
> *Typ *unterstützt **[!UICONTROL Classification]**und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter &quot;Schema *verwalten*&quot;aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes für den Einzelhandel [erstellt](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicken Sie im Abschnitt *Funktionsverwaltung* auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **[!UICONTROL Feldeigenschaften&quot;entweder &quot;]** Eingabefunktion **[!UICONTROL &quot;oder &quot;]** Target-Funktion **[!UICONTROL &quot;auswählen]** . Legen Sie für diese Übung **[!UICONTROL weeklySales]** als **[!UICONTROL Target-Funktion]** und alles andere als **[!UICONTROL Input-Funktion]** fest. Klicken Sie auf **[!UICONTROL Weiter]** , um Ihr neues konfiguriertes Rezept zu überprüfen.

Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **Fertig stellen** , um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell mit dem neu erstellten Vertriebsrezept [!DNL Data Science Workspace] für Einzelhändler erstellt wird.

### Docker-basiertes Rezept importieren - PySpark {#pyspark}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] Benutzeroberfläche. Wählen Sie als Nächstes *Rezept* importieren und klicken Sie auf **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; *Konfigurieren* &quot;für den Arbeitsablauf für *Skriptdateien* wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **[!UICONTROL Weiter]** , um fortzufahren.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> In der [Paketquellendatei in einem Rezept](./package-source-files-recipe.md) -Tutorial wurde am Ende der Erstellung des Retail Sales-Rezeptes mit PySpark-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle ** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit PySpark-Quelldateien erstellten gepackten Rezept in das Feld **[!UICONTROL Quell-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Wählen Sie **[!UICONTROL PySpark]** in der Dropdown-Liste *Laufzeit* . Sobald die PySpark-Laufzeit ausgewählt ist, wird das standardmäßige Artefakt automatisch in **[!UICONTROL Docker]** eingetragen. Wählen Sie anschließend **[!UICONTROL Klassifizierung]** in der Dropdown-Liste *Typ* . Klicken Sie nach dem Ausfüllen auf **[!UICONTROL Weiter]** oben rechts, um mit &quot;Schema *verwalten&quot;fortzufahren*.

>[!NOTE]
> *Typ *unterstützt **[!UICONTROL Classification]**und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter &quot;Schema *verwalten*&quot;aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes für den Einzelhandel [erstellt](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicken Sie im Abschnitt *Funktionsverwaltung* auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **[!UICONTROL Feldeigenschaften&quot;entweder &quot;]** Eingabefunktion **[!UICONTROL &quot;oder &quot;]** Target-Funktion **[!UICONTROL &quot;auswählen]** . Legen Sie für diese Übung **[!UICONTROL weeklySales]** als **[!UICONTROL Target-Funktion]** und alles andere als **[!UICONTROL Input-Funktion]** fest. Klicken Sie auf **[!UICONTROL Weiter]** , um Ihr neues konfiguriertes Rezept zu überprüfen.

Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **[!UICONTROL Fertig stellen]** , um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell mit dem neu erstellten Vertriebsrezept [!DNL Data Science Workspace] für Einzelhändler erstellt wird.

### Docker-basiertes Rezept importieren - Scala {#scala}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform] Benutzeroberfläche. Wählen Sie als Nächstes *Rezept* importieren und klicken Sie auf **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite &quot; *Konfigurieren* &quot;für den Arbeitsablauf für *Skriptdateien* wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann in der oberen rechten Ecke die Option **[!UICONTROL Weiter]** , um fortzufahren.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> In den Quelldateien [für das Verpacken in einem Rezept](./package-source-files-recipe.md) -Lernprogramm wurde am Ende der Erstellung des Retail Sales-Rezepts mit Scala-([!DNL Spark]) Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite &quot;Quelle ** auswählen&quot;befinden, fügen Sie die Docker-URL entsprechend dem mit Scala-Quelldateien erstellten gepackten Rezept in das Feld *Quell-URL* ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag &amp; Drop oder verwenden Sie den Dateisystem- **Browser**. Die angegebene Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Wählen Sie **[!UICONTROL Spark]** in der Dropdown-Liste *Laufzeit* . Nach Auswahl der [!DNL Spark] Laufzeitumgebung wird das standardmäßige Artefakt automatisch mit **[!UICONTROL Docker]** gefüllt. Wählen Sie dann **[!UICONTROL Regression]** aus der Dropdownliste *Typ* . Klicken Sie nach dem Ausfüllen auf **[!UICONTROL Weiter]** oben rechts, um mit &quot;Schema *verwalten&quot;fortzufahren*.

>[!NOTE]
> *Typ *unterstützt **[!UICONTROL Classification]**und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter &quot;Schema *verwalten*&quot;aus. Sie wurden mithilfe des bereitgestellten Bootstrap-Skripts im Lernprogramm zum Erstellen des Schemas und des Datensatzes für den Einzelhandel [erstellt](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicken Sie im Abschnitt *Funktionsverwaltung* auf Ihre Pachtnummer im Schema-Viewer, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und im rechten Fenster &quot; **[!UICONTROL Feldeigenschaften&quot;entweder &quot;]** Eingabefunktion **[!UICONTROL &quot;oder &quot;]** Target-Funktion **[!UICONTROL &quot;auswählen]** . Legen Sie für diese Übung **[!UICONTROL weeklySales]** als **[!UICONTROL Target-Funktion]** und alles andere als **[!UICONTROL Input-Funktion]** fest. Klicken Sie auf **[!UICONTROL Weiter]** , um Ihr neues konfiguriertes Rezept zu überprüfen.

Überprüfen Sie das Rezept, fügen Sie Konfigurationen hinzu, ändern oder entfernen Sie sie nach Bedarf. Klicken Sie auf **[!UICONTROL Fertig stellen]** , um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell mit dem neu erstellten Vertriebsrezept [!DNL Data Science Workspace] für Einzelhändler erstellt wird.

## Nächste Schritte {#next-steps}

Dieses Lernprogramm bietet einen Einblick in die Konfiguration und den Import eines Skripts [!DNL Data Science Workspace]. Sie können ein Modell jetzt mit dem neu erstellten Rezept erstellen, ausbilden und auswerten.

- [Erstellen und Auswerten eines Modells in der Benutzeroberfläche](./train-evaluate-model-ui.md)
- [Erstellen und Auswerten eines Modells mithilfe der API](./train-evaluate-model-api.md)