---
keywords: Experience Platform;home;popular topics; delete dataflows
description: Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. This tutorial provides steps for deleting dataflows from the Sources workspace.
solution: Experience Platform
title: Delete dataflows
topic: overview
translation-type: tm+mt
source-git-commit: ccbf9de6b64ecc4595ea455374f81bb5520d7b83
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 16%

---


# Delete dataflows

Source connectors in Adobe Experience Platform provide the ability to ingest externally sourced data on a scheduled basis. This tutorial provides steps for deleting dataflows from the *[!UICONTROL Sources]* workspace.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Experience-Datenmodell (XDM)-System](../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema Editor tutorial](../../../xdm/tutorials/create-schema-ui.md): Learn how to create custom schemas using the Schema Editor UI.
- [Echtzeit-Kundenprofil](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Delete dataflows using the UI

Log in to [Adobe Experience Platform](https://platform.adobe.com) and then select **[!UICONTROL Sources]** from the left navigation bar to access the *[!UICONTROL Sources]* workspace. The *[!UICONTROL Catalog]* screen displays a variety of sources for which you can create accounts and dataflows with. Each source shows the number of existing accounts and dataflows associated to them.

Select **[!UICONTROL Dataflows]** to access the *[!UICONTROL Dataflows]* page.

![dataset-flow-activity](../../images/tutorials/delete/dataflows.png)

A list of existing dataflows appears. On this page is a list of sortable information for existing dataflows such as source, username, run status, and last run date. Select the **funnel icon** on the top left to sort.

![dataflows-Liste](../../images/tutorials/delete/dataflows-list.png)

Das Sortierungsbedienfeld wird auf der linken Seite des Bildschirms mit einer Liste der verfügbaren Quellen angezeigt.
Mit der Sortierfunktion können Sie mehrere Quellen auswählen.

Select the source you wish to access and locate the dataflow you intend to delete from the list of dataflows in the main interface. In the example, the source selected is **Azure Blob Storage** and the dataflow name is **Customer profiles dataflow**. When selecting multiple sources from the sorting panel, your most recently created dataflows appear first because the list is sorted by created date.

Select the dataflow you intend to delete.

![dataflows-sort](../../images/tutorials/delete/dataflows-sort.png)

The *[!UICONTROL Properties]* panel appears on the right side of the screen, containing information regarding the selected dataflow as well as an option to *[!UICONTROL Edit schedule]*.

To delete the dataflow, select **[!UICONTROL Delete]**.

![dataflows-sort](../../images/tutorials/delete/dataflows-properties.png)

A final confirmation dialog box appears, select **[!UICONTROL Delete]** to complete the process.

![Löschen Sie](../../images/tutorials/delete/delete.png)

After a few moments, a green confirmation box appears on the bottom of the screen to confirm a successful deletion.

![confirmed](../../images/tutorials/delete/confirmed.png)

## Nächste Schritte

By following this tutorial, you have successfully accessed existing accounts and dataflows from the *[!UICONTROL Sources]* workspace. Incoming data can now be used by downstream [!DNL Platform] services such as [!DNL Real-time Customer Profile] and [!DNL Data Science Workspace]. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../profile/home.md)
- [Data Science Workspace overview](../../../data-science-workspace/home.md)