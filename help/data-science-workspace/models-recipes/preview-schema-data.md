---
keywords: Experience Platform;Vorschau von Schemadaten;Data Science Workspace;beliebte Themen
solution: Experience Platform
title: Vorschau des Einzelhandels-Schemas und -Datensatzes
type: Tutorial
description: Im folgenden Dokument wird die Vorschau von Schemata und Datensätzen auf Adobe Experience Platform beschrieben.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 20%

---

# Vorschau des Einzelhandelsverkaufsschemas und -datensatzes

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Nach erfolgreichem Abschluss des Bootstrap-Skripts aus dem Tutorial [Einzelhandelsverkaufsschema und -datensatz](./create-retails-sales-dataset.md). Ausgabeschemata und Datensätze können auf [!DNL Experience Platform] angezeigt werden. Gehen Sie zur Anzeige der Schemata und Datensätze wie folgt vor:

Wählen Sie im linken Navigationsbereich die Registerkarte **[!UICONTROL Schemas]** aus und suchen Sie das vom Bootstrap-Skript erstellte Eingabeschema. Der Name des Schemas entspricht dem, der im vorherigen Schritt unter `config.yaml` definiert wurde. Zeigen Sie die Schemadetails und deren Komposition an, indem Sie darauf klicken.

![](../images/models-recipes/access-data/schema.PNG)

Wählen Sie in der linken Navigationsleiste die Registerkarte **[!UICONTROL Datasets]** aus und öffnen Sie den erstellten Eingabedatensatz, indem Sie den Namen des Datensatzes auswählen. Der Name des Datensatzes entspricht dem, was im vorherigen Schritt in `config.yaml` definiert wurde.

![](../images/models-recipes/access-data/dataset.PNG)

Wählen Sie oben rechts **[!UICONTROL Preview Dataset]** aus, um eine Teilmenge des Datensatzes in der Vorschau anzuzeigen.

![](../images/models-recipes/access-data/preview.PNG)

## Nächste Schritte

Sie haben jetzt mit dem bereitgestellten Bootstrap-Skript erfolgreich Beispieldaten zu Einzelhandelsumsätzen in [!DNL Experience Platform] aufgenommen.

So arbeiten Sie weiter mit den aufgenommenen Daten:

- [Daten mit Jupyter Notebooks analysieren](../jupyterlab/analyze-your-data.md)
   - Verwenden Sie Jupyter-Notebooks in [!DNL Data Science Workspace], um auf Ihre Daten zuzugreifen, sie zu erkunden, zu visualisieren und zu verstehen.
- [Packen von Quelldateien in ein Rezept](./package-source-files-recipe.md)
   - In diesem Tutorial erfahren Sie, wie Sie Ihr eigenes Modell in [!DNL Data Science Workspace] importieren, indem Sie Quelldateien in eine importierbare Rezeptdatei packen.
