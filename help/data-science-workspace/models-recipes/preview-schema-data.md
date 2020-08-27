---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: Vorschau auf Schemas und Datensätze
topic: Tutorial
description: Im folgenden Dokument wird die Vorschau von Schemas und Datensätzen auf Adobe Experience Platform beschrieben.
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 70%

---


# Vorschau auf Schemas und Datensätze

Nach erfolgreichem Abschluss des Bootstrap-Skripts aus dem Tutorial zum [Erstellen des Einzelhandelsschemas und -datensatzes](./create-retails-sales-dataset.md). Output schemas and datasets can be viewed on [!DNL Experience Platform]. Gehen Sie zur Anzeige der Schemas und Datensätze wie folgt vor:

1. Klicken Sie in der linken Navigationsspalte auf den Link **[!UICONTROL Schemas]** und suchen Sie das vom Bootstrap-Skript erstellte Eingabeschema. Der Name des Schemas entspricht dem, der im vorherigen Schritt unter `config.yaml` definiert wurde. Zeigen Sie die Schemadetails und deren Komposition an, indem Sie darauf klicken.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Klicken Sie in der linken Navigationsspalte auf den Link **[!UICONTROL Datensätze]** und öffnen Sie den Eingabedatensatz, der durch Klicken auf den Namen der Auflistung erstellt wurde. Der Name des Datensatzes entspricht dem, der im vorherigen Schritt unter `config.yaml` definiert wurde.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Klicken Sie oben rechts in der Vorschau auf **[!UICONTROL Datensatz-Vorschau]**, um eine Untergruppe des Datensatzes anzuzeigen.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Nächste Schritte

You have now successfully ingested Retail Sales sample data into [!DNL Experience Platform] using the provided bootstrap script.

So arbeiten Sie weiter mit den aufgenommenen Daten:
- [Daten mit Jupyter-Notebooks analysieren](../jupyterlab/analyze-your-data.md)
   - Use Jupyter notebooks in [!DNL Data Science Workspace] to access, explore, visualize, and understand your data.
- [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md)
   - Follow this tutorial to learn how to bring your own Model into [!DNL Data Science Workspace] by packaging source files in an importable Recipe file.