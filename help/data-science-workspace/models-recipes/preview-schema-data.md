---
keywords: Experience Platform;Vorschau Schema Data;Data Science Workspace;beliebte Themen
solution: Experience Platform
title: Vorschau des Schemas Einzelhandelsverkäufe und des Datasets
topic-legacy: tutorial
type: Tutorial
description: Im folgenden Dokument wird die Vorschau von Schemas und Datensätzen auf Adobe Experience Platform beschrieben.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 22%

---

# Vorschau des Schemas und des Datensatzes für den Einzelhandel

Nach erfolgreichem Abschluss des Bootstrap-Schemas aus dem Tutorial [Retail Sales und DataSet](./create-retails-sales-dataset.md). Output-Schema und -Datensätze können unter [!DNL Experience Platform] angezeigt werden. Gehen Sie zur Anzeige der Schemas und Datensätze wie folgt vor:

Wählen Sie die Registerkarte **[!UICONTROL Schema]** in der linken Navigation aus und suchen Sie das vom Bootstrap-Schema erstellte Eingabedatum. Der Name des Schemas entspricht dem, der im vorherigen Schritt unter `config.yaml` definiert wurde. Zeigen Sie die Schemadetails und deren Komposition an, indem Sie darauf klicken.

![](../images/models-recipes/access-data/schema.PNG)

Wählen Sie in der linken Navigation die Registerkarte **[!UICONTROL Datensätze]** und öffnen Sie das Eingabedataset, das durch Auswahl des Namens des Datensatzes erstellt wurde. Der Name des Datensatzes entspricht dem, was im vorherigen Schritt unter `config.yaml` definiert wurde.

![](../images/models-recipes/access-data/dataset.PNG)

Wählen Sie **[!UICONTROL Vorschau DataSet]** oben rechts aus, um eine Untergruppe des Datensatzes Vorschau.

![](../images/models-recipes/access-data/preview.PNG)

## Nächste Schritte

Sie haben nun mit dem bereitgestellten Bootstrap-Skript erfolgreich Musterdaten für Einzelhandelsverkäufe in [!DNL Experience Platform] erfasst.

So arbeiten Sie weiter mit den aufgenommenen Daten:
- [Analysieren Ihrer Daten mit Jupyter-Notebooks](../jupyterlab/analyze-your-data.md)
   - Verwenden Sie Jupyter-Notebooks in [!DNL Data Science Workspace], um auf Ihre Daten zuzugreifen, sie zu untersuchen, darzustellen und sie zu verstehen.
- [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md)
   - Folgen Sie diesem Lernprogramm, um zu erfahren, wie Sie Ihr eigenes Modell in [!DNL Data Science Workspace] durch Verpacken von Quelldateien in einer wichtigen Recipe-Datei bringen.
