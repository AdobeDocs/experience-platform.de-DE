---
keywords: Experience Platform;Vorschau Schema Data;Data Science Workspace;beliebte Themen
solution: Experience Platform
title: Vorschau auf Schemas und Datensätze
topic: tutorial
type: Tutorial
description: Im folgenden Dokument wird die Vorschau von Schemas und Datensätzen auf Adobe Experience Platform beschrieben.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 67%

---


# Vorschau auf Schemas und Datensätze

Nach erfolgreichem Abschluss des Bootstrap-Skripts aus dem Tutorial zum [Erstellen des Einzelhandelsschemas und -datensatzes](./create-retails-sales-dataset.md). Output-Schema und -Datensätze können unter [!DNL Experience Platform] angezeigt werden. Gehen Sie zur Anzeige der Schemas und Datensätze wie folgt vor:

1. Klicken Sie in der linken Navigationsspalte auf den Link **[!UICONTROL Schemas]** und suchen Sie das vom Bootstrap-Skript erstellte Eingabeschema. Der Name des Schemas entspricht dem, der im vorherigen Schritt unter `config.yaml` definiert wurde. Zeigen Sie die Schemadetails und deren Komposition an, indem Sie darauf klicken.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Klicken Sie in der linken Navigationsspalte auf den Link **[!UICONTROL Datensätze]** und öffnen Sie den Eingabedatensatz, der durch Klicken auf den Namen der Auflistung erstellt wurde. Der Name des Datensatzes entspricht dem, der im vorherigen Schritt unter `config.yaml` definiert wurde.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Klicken Sie oben rechts in der Vorschau auf **[!UICONTROL Datensatz-Vorschau]**, um eine Untergruppe des Datensatzes anzuzeigen.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Nächste Schritte

Sie haben nun mit dem bereitgestellten Bootstrap-Skript erfolgreich Musterdaten zum Einzelhandelsverkauf in [!DNL Experience Platform] erfasst.

So arbeiten Sie weiter mit den aufgenommenen Daten:
- [Daten mit Jupyter-Notebooks analysieren](../jupyterlab/analyze-your-data.md)
   - Verwenden Sie Jupyter-Notebooks in [!DNL Data Science Workspace], um auf Ihre Daten zuzugreifen, sie zu untersuchen, darzustellen und sie zu verstehen.
- [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md)
   - Folgen Sie diesem Lernprogramm, um zu erfahren, wie Sie Ihr eigenes Modell in [!DNL Data Science Workspace] durch Verpacken von Quelldateien in einer wichtigen Recipe-Datei bringen.