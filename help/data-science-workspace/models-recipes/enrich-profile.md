---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics;machine learning insights
solution: Experience Platform
title: Echtzeit-Kundenprofil mit Einblicken aus maschinellem Lernen anreichern
topic: tutorial
type: Tutorial
description: Dieses Dokument bietet eine schrittweise Anleitung zur Erweiterung des Echtzeit-Profils durch maschinelles Lernen, zur Unterteilung der Schritte in die folgenden Abschnitte, zum Erstellen eines Output-Schemas/Datensatzes, zum Konfigurieren eines Output-Schemas/Datensatzes und zum Erstellen von Segmenten mithilfe des Segmentaufbaus.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 70%

---


# Mehr [!DNL Real-time Customer Profile] über maschinelles Lernen

[!DNL Adobe Experience Platform][!DNL Data Science Workspace] bietet die Tools und Ressourcen, um Modelle für maschinelles Lernen zu erstellen, zu bewerten und zu nutzen und so Datenprognosen und Einblicke zu generieren. When machine learning insights are ingested into a [!DNL Profile]-enabled dataset, that same data is also ingested as [!DNL Profile] records which can then be segmented into subsets of related elements by using [!DNL Experience Platform Segmentation Service].

This document provides a step-by-step tutorial to enrich [!DNL Real-time Customer Profile] with machine learning insights, steps are broken into the following sections:

1. [Ausgabeschema und -datensatz erstellen](#create-an-output-schema-and-dataset)
2. [Ausgabeschema und -datensatz konfigurieren](#configure-an-output-schema-and-dataset)
3. [Segmente mit dem Segment Builder erstellen](#create-segments-using-the-segment-builder)

## Erste Schritte

This tutorial requires a working understanding of the various aspects of [!DNL Adobe Experience Platform] involved in ingesting [!DNL Profile] data and creating segments. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Real-time Customer Profile]](../../rtcdp/overview.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Identity Service]](../../identity-service/home.md): Ermöglicht [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in Plattform erfasst werden.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.

Neben den oben genannten Dokumenten sollten Sie auch folgende Leitfäden zu Schemas und dem Schema-Editor lesen:

* [Grundlagen der Zusammensetzung](../../xdm/schema/composition.md)des Schemas: Beschreibt XDM-Schema, Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in [!DNL Experience Platform]verwendet werden sollen.
* [Anleitung für den Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Enthält ausführliche Anweisungen zum Erstellen von Schemas mit dem Schema-Editor in [!DNL Experience Platform].

## Ausgabeschema und Datensatz erstellen {#create-an-output-schema-and-dataset}

The first step towards enriching [!DNL Real-time Customer Profile] with scoring insights is knowing what real-world object (such as a person) your data defines. Wenn Sie Ihre Daten verstehen, können Sie eine Struktur beschreiben und entwerfen, die für Ihre Daten sinnvoll ist (ähnlich wie beim Entwerfen einer relationalen Datenbank).

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Dieser Abschnitt enthält grundlegende Anweisungen zum Erstellen eines Schemas mit dem Schema-Builder. Eine ausführlichere Anleitung finden Sie im Tutorial zum [Erstellen eines Schemas mit dem Schema-Editor](../../xdm/tutorials/create-schema-ui.md).

1. Klicken Sie in Adobe Experience Platform auf die Registerkarte **[!UICONTROL Schema]**, um auf den Schema-Browser zuzugreifen. Klicken Sie auf **[!UICONTROL Schema erstellen]**, um den **Schema-Editor** zu öffnen, wo Sie interaktiv Schemas erstellen und einrichten können.
   ![](../images/models-recipes/enrich-rtcdp/schema_browser.png)

2. Klicken Sie im Fenster **Komposition** auf **[!UICONTROL Zuweisen]**, um die verfügbaren Klassen zu durchsuchen.
   * Um eine vorhandene Klasse zuzuweisen, markieren Sie die gewünschte Klasse und klicken Sie dann auf **[!UICONTROL Klasse zuweisen]**.
      ![](../images/models-recipes/enrich-rtcdp/existing_class.png)

   * Um eine benutzerdefinierte Klasse zu erstellen, klicken Sie in der Mitte des Browser-Fensters auf **[!UICONTROL Neue Klasse erstellen]**. Geben Sie einen Klassennamen und eine Beschreibung an und wählen Sie das Verhalten der Klasse aus. Klicken Sie auf **[!UICONTROL Klasse zuweisen]**, sobald Sie damit fertig sind.
      ![](../images/models-recipes/enrich-rtcdp/create_new_class.png)

   An diesem Punkt sollte die Struktur Ihres Schemas einige Klassenfelder enthalten; jetzt können Sie Mixins zuweisen. Ein Mixin ist eine Gruppe aus einem oder mehreren Feldern, die ein bestimmtes Konzept beschreiben.

3. Klicken Sie im Fenster **Komposition** im Unterabschnitt **Mixins** auf **[!UICONTROL Hinzufügen]**.
   * Um ein vorhandenes Mixin zuzuweisen, markieren Sie das gewünschte Mixin und klicken Sie auf **[!UICONTROL Mixin hinzufügen]**. Anders als bei Klassen können einem einzelnen Schema mehrere Mixins zugewiesen werden, sofern dies nützlich ist.
      ![](../images/models-recipes/enrich-rtcdp/existing_mixin.png)

   * Um ein neues Mixin zu erstellen, klicken Sie in der Mitte des Browser-Fensters auf **[!UICONTROL Neues Mixin erstellen]**. Geben Sie einen Namen und eine Beschreibung für das Mixin ein und klicken Sie auf **[!UICONTROL Mixin zuweisen]**, sobald Sie damit fertig sind.
      ![](../images/models-recipes/enrich-rtcdp/create_new_mixin.png)

   * Um Mixin-Felder hinzuzufügen, klicken Sie im Fenster *Komposition* auf den Namen des Mixins. Sie erhalten dann die Möglichkeit, Mixin-Felder hinzuzufügen, indem Sie im Fenster *Struktur* auf **[!UICONTROL Feld hinzufügen]** klicken. Stellen Sie sicher, dass Sie die entsprechenden Mixin-Eigenschaften angeben.
      ![](../images/models-recipes/enrich-rtcdp/mixin_properties.png)

4. Nachdem Sie das Schema erstellt haben, klicken Sie im Fenster *Struktur* auf das Feld auf oberster Ebene des Schemas, um im rechten Eigenschaftenfenster die Eigenschaften des Schemas anzuzeigen. Geben Sie einen Namen und eine Beschreibung ein und klicken Sie auf **[!UICONTROL Speichern]**, um das Schema zu erstellen.
   ![](../images/models-recipes/enrich-rtcdp/save_schema.png)

5. Erzeugen Sie mit Ihrem neu erstellten Schema einen Ausgabedatensatz, indem Sie in der linken Navigationsspalte auf **[!UICONTROL Datensätze]** und dann auf **[!UICONTROL Datensatz erstellen]** klicken. Wählen Sie im nächsten Bildschirm **[!UICONTROL Datensatz aus Schema erstellen]**.
   ![](../images/models-recipes/enrich-rtcdp/dataset_overview.png)

6. Wählen Sie mit dem Schema-Browser das neu erstellte Schema aus und klicken Sie dann auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/enrich-rtcdp/choose_schema.png)

7. Geben Sie einen Namen und eine optionale Beschreibung ein und klicken Sie dann auf **[!UICONTROL Fertig stellen]**, um den Datensatz zu erstellen.
   ![](../images/models-recipes/enrich-rtcdp/configure_dataset.png)

Nachdem Sie einen Ausgabeschemadatensatz erstellt haben, fahren Sie mit dem nächsten Abschnitt fort, um den Datensatz für die Profilanreicherung zu konfigurieren und zu aktivieren.

## Ausgabeschema und -datensatz konfigurieren {#configure-an-output-schema-and-dataset}

Before you can enable a dataset for [!DNL Profile], you need to configure the dataset&#39;s schema to having a primary identity field and then enable the schema for [!DNL Profile]. Wenn Sie ein neues Schema erstellen und aktivieren möchten, konsultieren Sie die Anleitung zum [Erstellen eines Schemas mit dem Schema-Editor](../../xdm/tutorials/create-schema-ui.md). Befolgen Sie andernfalls die unten stehenden Anweisungen, um ein vorhandenes Schema und einen vorhandenen Datensatz zu aktivieren.

1. On Adobe Experience Platform, use the schema browser to find the output schema you wish to enable [!DNL Profile] on and click its name to view its composition.
   ![](../images/models-recipes/enrich-rtcdp/schemas.png)

2. Erweitern Sie die Schemastruktur und suchen Sie nach einem geeigneten Feld, das als primäre Kennung dienen soll. Klicken Sie auf das gewünschte Feld, um dessen Eigenschaften anzuzeigen.
   ![](../images/models-recipes/enrich-rtcdp/schema_structure.png)

3. Legen Sie das Feld als primäre Identität fest, indem Sie die Eigenschaft **[!UICONTROL Identität]** des Felds sowie die Eigenschaft **[!UICONTROL Primäre Identität]** aktivieren und dann einen entsprechenden **[!UICONTROL Identity-Namespace]** auswählen. Klicken Sie auf **[!UICONTROL Übernehmen]**, nachdem Sie Ihre Änderungen vorgenommen haben.
   ![](../images/models-recipes/enrich-rtcdp/set_identity.png)

4. Klicken Sie auf das Objekt auf der obersten Ebene Ihrer Schemastruktur, um die Schemaeigenschaften anzuzeigen und das Schema für das Profil zu aktivieren, indem Sie den **[!UICONTROL Profil]**-Umschalter aktivieren. Klicken Sie auf **[!UICONTROL Speichern]**, um die Änderungen abzuschließen. Datensätze, die mit diesem Schema erstellt wurden, können jetzt für das Profil aktiviert werden.
   ![](../images/models-recipes/enrich-rtcdp/enable_schema.png)

5. Use the dataset browser to find the dataset you wish to enable [!DNL Profile] on and click its name to access its details.
   ![](../images/models-recipes/enrich-rtcdp/datasets.png)

6. Enable the dataset for [!DNL Profile] by toggling the **[!UICONTROL Profile]** switch found in the right information column.
   ![](../images/models-recipes/enrich-rtcdp/enable_dataset.png)

When data is ingested into a [!DNL Profile]-enabled dataset, that same data is also ingested as [!DNL Profile] records. Nach der Vorbereitung Ihres Schemas und Datensatzes generieren Sie einige Daten im Datensatz, indem Sie mit einem geeigneten Modell Scoring-Läufe durchführen. Fahren Sie mit dieser Anleitung fort, um mithilfe von Segment Builder Insight-Segmente zu erstellen.

## Segmente mit dem Segment Builder erstellen {#create-segments-using-the-segment-builder}

Now that you have generated and ingested insights into your [!DNL Profile]-enabled dataset, you can manage that data by identifying subsets of related elements using the Segment Builder. Gehen Sie wie folgt vor, um eigene Segmente zu erstellen.

1. Klicken Sie in Adobe Experience Platform auf die Registerkarte **[!UICONTROL Segmente]** und anschließend auf **[!UICONTROL Segment erstellen]**, um auf den Segment Builder zuzugreifen.
   ![](../images/models-recipes/enrich-rtcdp/segments_overview.png)

2. Im Segment Builder bietet die linke Leiste Zugriff auf die wichtigsten Bausteine von Segmenten: Attribute, Ereignisse und vorhandene Segmente. Jeder Baustein wird auf einer eigenen Registerkarte angezeigt. Select the class to which your [!DNL Profile]-enabled schema extends then browse and find the building blocks for your segment.
   ![](../images/models-recipes/enrich-rtcdp/segment_builder.png)

3. Ziehen Sie Bausteine per Drag-and-Drop auf die Arbeitsfläche des Rule Builder und ergänzen Sie sie durch Angabe vergleichender Anweisungen.
   ![](../images/models-recipes/enrich-rtcdp/drag_fill.gif)

4. Bei der Erstellung Ihres Segments können Sie geschätzte Segmentergebnisse unter Beachtung des Bereichs *Segmenteigenschaften* als Vorschau anzeigen.
   ![](../images/models-recipes/enrich-rtcdp/preview_segment.gif)

5. Wählen Sie eine geeignete **[!UICONTROL Zusammenführungsrichtlinie]**, geben Sie einen Namen und eine optionale Beschreibung ein und klicken Sie dann auf **[!UICONTROL Speichern]**, um Ihr neues Segment abzuschließen.
   ![](../images/models-recipes/enrich-rtcdp/save_segment.png)


## Nächste Schritte {#next-steps}

This document walked you through the steps required to enable a schema and dataset for [!DNL Profile], and briefly demonstrated the workflow for creating insight segments using the Segment Builder. Weiterführende Informationen zu Segmenten und Segment Builder finden Sie unter [Segmentation Service – Übersicht](../../segmentation/home.md).