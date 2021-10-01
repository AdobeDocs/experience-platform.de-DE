---
keywords: Experience Platform; Vorschau von Schemadaten; Data Science Workspace; beliebte Themen
solution: Experience Platform
title: Vorschau des Schemas und Datensatzes für Einzelhandelsumsätze
topic-legacy: tutorial
type: Tutorial
description: Im folgenden Dokument wird die Vorschau von Schemas und Datensätzen in Adobe Experience Platform beschrieben.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 22%

---

# Vorschau des Einzelhandelsschemas und -datensatzes

Nach erfolgreichem Abschluss des Bootstrap-Skripts aus dem Tutorial [Einzelhandelsschema und -datensatz](./create-retails-sales-dataset.md). Ausgabeschemas und -datensätze können auf [!DNL Experience Platform] angezeigt werden. Gehen Sie zur Anzeige der Schemas und Datensätze wie folgt vor:

Wählen Sie im linken Navigationsbereich die Registerkarte **[!UICONTROL Schemas]** aus und suchen Sie nach dem vom Bootstrap-Skript erstellten Eingabeschema. Der Name des Schemas entspricht dem, der im vorherigen Schritt unter `config.yaml` definiert wurde. Zeigen Sie die Schemadetails und deren Komposition an, indem Sie darauf klicken.

![](../images/models-recipes/access-data/schema.PNG)

Wählen Sie im linken Navigationsbereich die Registerkarte **[!UICONTROL Datensätze]** aus und öffnen Sie den Eingabedatensatz, der durch Auswahl des Datensatznamens erstellt wurde. Der Name des Datensatzes entspricht dem, der im vorherigen Schritt unter `config.yaml` definiert wurde.

![](../images/models-recipes/access-data/dataset.PNG)

Wählen Sie **[!UICONTROL Datensatz-Vorschau]** oben rechts aus, um eine Teilmenge des Datensatzes in der Vorschau anzuzeigen.

![](../images/models-recipes/access-data/preview.PNG)

## Nächste Schritte

Sie haben jetzt mit dem bereitgestellten Bootstrap-Skript erfolgreich Beispieldaten für Einzelhandelsumsätze in [!DNL Experience Platform] erfasst.

So arbeiten Sie weiter mit den aufgenommenen Daten:
- [Daten mit Jupyter Notebooks analysieren](../jupyterlab/analyze-your-data.md)
   - Verwenden Sie Jupyter Notebooks in [!DNL Data Science Workspace], um auf Ihre Daten zuzugreifen, sie zu untersuchen, zu visualisieren und zu verstehen.
- [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md)
   - In diesem Tutorial erfahren Sie, wie Sie Ihr eigenes Modell in [!DNL Data Science Workspace] bringen, indem Sie Quelldateien in einer wichtigen Rezeptdatei verpacken.
