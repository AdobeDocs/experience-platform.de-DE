---
keywords: Experience Platform; Vorschau von Schemadaten; Data Science Workspace; beliebte Themen
solution: Experience Platform
title: Vorschau des Schemas und Datensatzes für Einzelhandelsumsätze
type: Tutorial
description: Im folgenden Dokument wird die Vorschau von Schemas und Datensätzen in Adobe Experience Platform beschrieben.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 22%

---

# Vorschau des Einzelhandelsschemas und -datensatzes

Nach erfolgreichem Abschluss des Bootstrap-Skripts aus dem [Einzelhandelsschema und -datensatz](./create-retails-sales-dataset.md) Tutorial. Ausgabeschemas und -datensätze können angezeigt werden unter [!DNL Experience Platform]. Gehen Sie zur Anzeige der Schemas und Datensätze wie folgt vor:

Wählen Sie die **[!UICONTROL Schemas]** im linken Navigationsbereich und suchen Sie das vom Bootstrap-Skript erstellte Eingabeschema. Der Name des Schemas entspricht dem, der im vorherigen Schritt unter `config.yaml` definiert wurde. Zeigen Sie die Schemadetails und deren Komposition an, indem Sie darauf klicken.

![](../images/models-recipes/access-data/schema.PNG)

Wählen Sie die **[!UICONTROL Datensätze]** in der linken Navigation und öffnen Sie den Eingabedatensatz, der durch Auswahl des Datensatznamens erstellt wurde. Der Name des Datensatzes entspricht dem, der in `config.yaml` aus dem vorherigen Schritt.

![](../images/models-recipes/access-data/dataset.PNG)

Auswählen **[!UICONTROL Vorschau eines Datensatzes anzeigen]** oben rechts, um eine Teilmenge des Datensatzes in der Vorschau anzuzeigen.

![](../images/models-recipes/access-data/preview.PNG)

## Nächste Schritte

Sie haben jetzt erfolgreich Beispieldaten für Einzelhandelsumsätze in [!DNL Experience Platform] mithilfe des bereitgestellten Bootstrap-Skripts.

So arbeiten Sie weiter mit den aufgenommenen Daten:
- [Daten mit Jupyter Notebooks analysieren](../jupyterlab/analyze-your-data.md)
   - Verwenden von Jupyter-Notebooks in [!DNL Data Science Workspace] , um auf Ihre Daten zuzugreifen, sie zu untersuchen, zu visualisieren und zu verstehen.
- [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md)
   - In diesem Tutorial erfahren Sie, wie Sie Ihr eigenes Modell in [!DNL Data Science Workspace] durch Verpacken von Quelldateien in einer wichtigen Rezeptdatei.
