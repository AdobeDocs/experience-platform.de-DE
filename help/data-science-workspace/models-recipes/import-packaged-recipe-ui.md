---
keywords: Experience Platform;importiertes verpacktes Rezept;Data Science Workspace;beliebte Themen;Rezepte;ui;Create Engine
solution: Experience Platform
title: Ein gepacktes Rezept in die Benutzeroberfläche von Data Science Workspace importieren
topic: Tutorial
type: Übung
description: Dieses Tutorial bietet Einblicke in das Konfigurieren und Importieren eines gepackten Rezepts mit dem bereitgestellten Beispiel für Einzelhandelsumsätze. Nach Abschluss dieses Tutorials können Sie ein Modell in Adobe Experience Platform Data Science Workspace erstellen, trainieren und bewerten.
translation-type: tm+mt
source-git-commit: 13fa4af388c6f31768a6b7e1da05cb56c5635c9e
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 37%

---


# Importieren eines zusammengestellten Rezeptes in die Benutzeroberfläche von Data Science Workspace

Dieses Tutorial bietet Einblicke in das Konfigurieren und Importieren eines gepackten Rezepts mit dem bereitgestellten Beispiel für Einzelhandelsumsätze. Am Ende dieses Lernprogramms sind Sie bereit, ein Modell in Adobe Experience Platform zu erstellen, auszubilden und auszuwerten.[!DNL Data Science Workspace]

## Voraussetzungen

Dieses Lernprogramm erfordert ein gepacktes Rezept in Form einer Docker-Bild-URL. Weiterführende Informationen finden Sie im Tutorial zum [Verpacken von Quelldateien in einem Rezept](./package-source-files-recipe.md).

## Workflow in der Benutzeroberfläche

Für das Importieren eines gepackten Rezepts in [!DNL Data Science Workspace] sind spezifische Rezeptkonfigurationen erforderlich, die in einer einzigen JSON-Datei (JavaScript Object Notation) kompiliert werden. Diese Kompilierung von Skriptkonfigurationen wird als Konfigurationsdatei bezeichnet. Ein gepacktes Rezept mit einem bestimmten Satz von Konfigurationen wird als Rezeptinstanz bezeichnet. Ein Rezept kann verwendet werden, um viele Rezept-Instanzen in [!DNL Data Science Workspace] zu erstellen.

Der Workflow zum Importieren eines gepackten Rezepts umfasst folgende Schritte:
- [Rezept konfigurieren](#configure)
- [Docker-basiertes Rezept importieren – Python](#python)
- [Docker-basiertes Rezept importieren – R](#r)
- [Docker-basiertes Rezept importieren - PySpark](#pyspark)
- [Docker-basiertes Rezept importieren - Scala](#scala)

### Rezept konfigurieren {#configure}

Jede Rezept-Instanz in [!DNL Data Science Workspace] wird mit einer Reihe von Konfigurationen begleitet, die die Rezept-Instanz an einen bestimmten Anwendungsfall anpassen. Konfigurationsdateien definieren das standardmäßige Trainings- und Scoring-Verhalten eines mit dieser Rezeptinstanz erstellten Modells.

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

Für die Zwecke dieses Lernprogramms können Sie die Standardkonfigurationsdateien für das Rezept Einzelhandel im [!DNL Data Science Workspace] Referenzhandbuch hinterlassen.

### Dockerbasiertes Rezept importieren - [!DNL Python] {#python}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform]-Benutzeroberfläche. Wählen Sie als Nächstes **Rezept importieren** und dann **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite **Konfigurieren** für den Arbeitsablauf **Importieren von Rezept** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann **[!UICONTROL Weiter]** in der oberen rechten Ecke aus.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md) wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit Python-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle auswählen** befinden, fügen Sie die Docker-URL entsprechend dem gepackten Rezept ein, das mit [!DNL Python]-Quelldateien im Feld **[!UICONTROL Quell-URL]** erstellt wurde. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Wählen Sie **[!UICONTROL Python]** in der Dropdown-Liste **Runtime** und **[!UICONTROL Klassifizierung]** in der Dropdownliste **Typ**. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** oben rechts, um mit **Schema verwalten** fortzufahren.

>[!NOTE]
>
> Typ unterstützt **[!UICONTROL Klassifizierung]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter **Schema verwalten** aus. Sie wurden mithilfe des Bootstrap-Skripts im Lernprogramm [Einzelhandelsverkäufe erstellen und den Datensatz](../models-recipes/create-retails-sales-dataset.md) erstellen erstellt.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Wählen Sie im Abschnitt **Funktionsverwaltung** im Schema-Viewer die Pachtnummer aus, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Weiter]**, um Ihr neues konfiguriertes Rezept zu überprüfen.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **[!UICONTROL Fertigstellen]**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für den Einzelhandel erstellt wird.

### Docker-basiertes Rezept importieren – R {#r}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform]-Benutzeroberfläche. Wählen Sie als Nächstes **Rezept importieren** und dann **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite **Konfigurieren** für den Arbeitsablauf **Importieren von Rezept** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann **[!UICONTROL Weiter]** in der oberen rechten Ecke aus.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md) wurde nach der Erstellung des Rezepts für Einzelhandelsumsätze mit R-Quelldateien eine Docker-URL bereitgestellt.

Sobald Sie sich auf der Seite **Quelle auswählen** befinden, fügen Sie die Docker-URL entsprechend dem gepackten Rezept, das mit R-Quelldateien erstellt wurde, in das Feld **[!UICONTROL Quell-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Wählen Sie **[!UICONTROL R]** in der Dropdownliste **Runtime** und **[!UICONTROL Klassifizierung]** in der Dropdownliste **Typ** aus. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** oben rechts, um mit **Schema verwalten** fortzufahren.

>[!NOTE]
>
> ** Typesupports unterstützt  **** Klassifizierung und  **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Wählen Sie anschließend die Schema für die Eingabe und Ausgabe im Einzelhandel unter **Schema verwalten** aus. Sie wurden mithilfe des Bootstrap-Skripts im Lernprogramm [Einzelhandelsverkäufe erstellen und den Datensatz](../models-recipes/create-retails-sales-dataset.md) erstellen erstellt.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Wählen Sie im Abschnitt *Funktionsverwaltung* im Schema-Viewer die Pachtnummer aus, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Weiter]**, um Ihr neues konfiguriertes Rezept zu überprüfen.

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **Fertigstellen**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für den Einzelhandel erstellt wird.

### Docker-basiertes Rezept importieren - PySpark {#pyspark}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform]-Benutzeroberfläche. Wählen Sie als Nächstes **Rezept importieren** und dann **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite **Konfigurieren** für den Arbeitsablauf **Importieren von Rezept** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann **[!UICONTROL Weiter]** in der oberen rechten Ecke aus, um fortzufahren.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in ein Rezept](./package-source-files-recipe.md) packen wurde eine Docker-URL am Ende des Builds des Retail Sales-Rezepts mit PySpark-Quelldateien bereitgestellt.

Sobald Sie sich auf der Seite **Quelle auswählen** befinden, fügen Sie die Docker-URL entsprechend dem gepackten Rezept, das mit PySpark-Quelldateien erstellt wurde, in das Feld **[!UICONTROL Quell-URL]** ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem **Browser** des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Wählen Sie **[!UICONTROL PySpark]** in der Dropdownliste **Runtime** aus. Nach Auswahl der PySpark-Laufzeit wird das standardmäßige Artefakt automatisch auf **[!UICONTROL Docker]** aufgefüllt. Wählen Sie anschließend **[!UICONTROL Klassifizierung]** in der Dropdownliste **Typ**. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** oben rechts, um mit **Schema verwalten** fortzufahren.

>[!NOTE]
>
> ** Typesupports unterstützt  **** Klassifizierung und  **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Wählen Sie anschließend mithilfe der Auswahl **Schema verwalten** die Schema für Einzelhandelsverkäufe aus. Die Schema wurden mit dem bereitgestellten Bootstrap-Skript im Lernprogramm [Einzelhandelsverkäufe erstellen und Schema](../models-recipes/create-retails-sales-dataset.md) erstellen erstellt.

![Schemas verwalten](../images/models-recipes/import-package-ui/manage-schemas.png)

Wählen Sie im Abschnitt **Funktionsverwaltung** im Schema-Viewer die Pachtnummer aus, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie in diesem Tutorial **[!UICONTROL weeklySales]** als **[!UICONTROL Zielfunktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Weiter]**, um Ihr neues konfiguriertes Rezept zu überprüfen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **[!UICONTROL Fertigstellen]**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für den Einzelhandel erstellt wird.

### Dockerbasiertes Rezept importieren - Skala {#scala}

Beginn durch Navigieren und Auswählen von **[!UICONTROL Workflows]** oben links in der [!DNL Platform]-Benutzeroberfläche. Wählen Sie als Nächstes **Rezept importieren** und dann **[!UICONTROL Starten]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Die Seite **Konfigurieren** für den Arbeitsablauf **Importieren von Rezept** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für das Rezept ein und wählen Sie dann **[!UICONTROL Weiter]** in der oberen rechten Ecke aus, um fortzufahren.

![Arbeitsablauf konfigurieren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Im Tutorial [Quelldateien in ein Rezept](./package-source-files-recipe.md) packen wurde eine Docker-URL am Ende des Builds des Retail Sales-Rezepts mit Scala-Quelldateien ([!DNL Spark]) bereitgestellt.

Sobald Sie sich auf der Seite **Quelle auswählen** befinden, fügen Sie die Docker-URL entsprechend dem gepackten Rezept, das mit Scala-Quelldateien erstellt wurde, in das Feld Quelle-URL ein. Importieren Sie anschließend die bereitgestellte Konfigurationsdatei per Drag-and-Drop oder mit dem Browser des Dateisystems. Die bereitgestellte Konfigurationsdatei finden Sie unter `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Wählen Sie **[!UICONTROL Spark]** in der Dropdownliste **Runtime** aus. Nach Auswahl der Laufzeitumgebung [!DNL Spark] wird das standardmäßige Artefakt automatisch auf **[!UICONTROL Docker]** aufgefüllt. Wählen Sie dann **[!UICONTROL Regression]** aus der Dropdownliste **Typ**. Nachdem alles ausgefüllt wurde, wählen Sie **[!UICONTROL Weiter]** oben rechts, um mit **Schema verwalten** fortzufahren.

>[!NOTE]
>
> Typ unterstützt **[!UICONTROL Klassifizierung]** und **[!UICONTROL Regression]**. Wenn Ihr Modell nicht unter einen dieser Typen fällt, wählen Sie **[!UICONTROL Benutzerdefiniert]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Wählen Sie anschließend mithilfe der Auswahl **Schema verwalten** die Schema für Einzelhandelsverkäufe aus. Die Schema wurden mit dem bereitgestellten Bootstrap-Skript im Lernprogramm [Einzelhandelsverkäufe erstellen und Schema](../models-recipes/create-retails-sales-dataset.md) erstellen erstellt.

![Schemas verwalten](../images/models-recipes/import-package-ui/manage-schemas.png)

Wählen Sie im Abschnitt **Funktionsverwaltung** im Schema-Viewer die Pachtnummer aus, um das Schema für die Eingabe des Einzelhandelsverkaufs zu erweitern. Wählen Sie die Ein- und Ausgabefunktionen aus, indem Sie die gewünschte Funktion markieren und entweder die Option **[!UICONTROL Eingabefunktion]** oder **[!UICONTROL Zielfunktion]** im rechten Fenster **[!UICONTROL Feldeigenschaften]** auswählen. Legen Sie für diese Übung &quot;[!UICONTROL weeklySales]&quot;als **[!UICONTROL Zielgruppe-Funktion]** und alles andere als **[!UICONTROL Eingabefunktion]** fest. Wählen Sie **[!UICONTROL Weiter]**, um Ihr neues konfiguriertes Rezept zu überprüfen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Prüfen Sie das Rezept und fügen Sie je nach Bedarf Konfigurationen hinzu bzw. ändern oder entfernen Sie sie. Wählen Sie **[!UICONTROL Fertigstellen]**, um das Rezept zu erstellen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Fahren Sie mit den [nächsten Schritten](#next-steps) fort, um herauszufinden, wie ein Modell in [!DNL Data Science Workspace] mit dem neu erstellten Rezept für den Einzelhandel erstellt wird.

## Nächste Schritte {#next-steps}

Dieses Lernprogramm bietet einen Einblick in die Konfiguration und den Import eines Skripts nach [!DNL Data Science Workspace]. Jetzt können Sie mit dem neu erstellten Rezept ein Modell erstellen, trainieren und bewerten.

- [Modell in der Benutzeroberfläche trainieren und bewerten](./train-evaluate-model-ui.md)
- [Modell mithilfe der API trainieren und bewerten](./train-evaluate-model-api.md)