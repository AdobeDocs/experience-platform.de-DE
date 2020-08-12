---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors
topic: tutorials
translation-type: tm+mt
source-git-commit: d847329f675c7ac34a4feabb9e57a9e97f7e3ed1
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 44%

---


# Define a relationship between two schemas using the [!DNL Schema Editor]

Die Möglichkeit, Beziehungen zwischen Ihren Kunden und deren Interaktionen mit Ihrer Marke kanalübergreifend zu analysieren, ist ein wichtiger Bestandteil von Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data.

While schema relationships can be inferred through the use of the union schema and [!DNL Real-time Customer Profile], this only applies to schemas that share the same class. To establish a relationship between two schemas belonging to different classes, a dedicated **relationship field** must be added to a source schema, which references the identity of a destination schema.

This document provides a tutorial for defining a relationship between two schemas using the Schema Editor in the [!DNL Experience Platform] user interface. Anweisungen zum Definieren von Schemabeziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).

## Erste Schritte

This tutorial requires a working understanding of [!DNL XDM System] and the Schema Editor in the [!DNL Experience Platform] UI. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM System in Experience Platform](../home.md): An overview of XDM and its implementation in [!DNL Experience Platform].
* [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [Create a schema using the Schema Editor](create-schema-ui.md): A tutorial covering the basics of working with the [!DNL Schema Editor].

## Quell- und Zielschemas definieren

Wir gehen davon aus, dass Sie die beiden Schemas, die in der Beziehung definiert werden sollen, bereits erstellt haben. For demonstration purposes, this tutorial creates a relationship between members of an organization&#39;s loyalty program (defined in a &quot;[!UICONTROL Loyalty Members]&quot; schema) and their favorite hotels (defined in a &quot;[!DNL Hotels]&quot; schema).

>[!IMPORTANT]
>
>In order to establish a relationship, both schemas must have defined primary identities and be enabled for [!DNL Real-time Customer Profile]. See the section on [enabling a schema for use in Profile](./create-schema-ui.md#profile) in the schema creation tutorial if you require guidance on how to configure your schemas accordingly.

Schema relationships are represented by a dedicated field within a **source schema** that refers to another field within a **destination schema**. In the steps that follow, &quot;[!UICONTROL Loyalty Members]&quot; will be the source schema, while &quot;[!DNL Hotels]&quot; will act as the destination schema.

Zu Referenzzwecken wird in den folgenden Abschnitten die Struktur der einzelnen Schemas beschrieben, die in dieser Anleitung verwendet werden, bevor eine Beziehung definiert wird.

### [!UICONTROL Schema „Mitglieder des Treueprogramms“]

Das Quellcode-Schema &quot;[!UICONTROL Treuemitglieder]&quot;basiert auf der XDM- [!DNL Individual Profile] Klasse und ist das Schema, das im Lernprogramm zum [Erstellen eines Schemas in der Benutzeroberfläche](create-schema-ui.md)erstellt wurde. It includes a &quot;[!UICONTROL loyalty]&quot; object under its &quot;\_tenantId&quot; namespace, which includes several loyalty-specific fields. One of these fields, &quot;loyaltyId&quot;, serves as the primary identity for the schema under the &quot;[!UICONTROL Email]&quot; namespace. As seen under _[!UICONTROL Schema Properties]_, this schema has been enabled for use in[!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### Schema „Hotels“

Das Ziel-Schema &quot;[!UICONTROL Hotels]&quot; basiert auf einer benutzerspezifischen &quot;[!UICONTROL Hotels]&quot; Klasse und enthält Felder, die ein Hotel beschreiben. The &quot;[!DNL hotelId]&quot; field serves as the primary identity for the schema under a custom &quot;[!DNL hotelId]&quot; namespace. Wie &quot;[!UICONTROL Treueanwärter]&quot; wurde auch dieses Schema für [!DNL Real-time Customer Profile]Sie aktiviert.

![](../images/tutorials/relationship/hotels.png)

## Beziehungs-Mixin erstellen

>[!NOTE]
>
> Dieser Schritt ist nur erforderlich, wenn Ihr Quellschema über kein dediziertes Zeichenfolgenfeld verfügt, das als Verweis auf ein anderes Schema verwendet werden kann. Wenn das Feld in Ihrem Quellschema bereits definiert ist, fahren Sie mit dem nächsten Schritt zum [Definieren eines Beziehungsfelds](#relationship-field) fort.

Um eine Beziehung zwischen zwei Schemas zu definieren, muss das Quellschema über ein dediziertes Feld verfügen, das als Verweis auf das Zielschema dient. Sie können dem Quellschema ein solches Feld hinzufügen, indem Sie ein neues Mixin erstellen.

Klicken Sie zunächst auf **[!UICONTROL Hinzufügen]** im Abschnitt _[!UICONTROL Mixins]_.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Der Dialog _[!UICONTROL Mixin hinzufügen]_wird angezeigt. Klicken Sie hier auf**[!UICONTROL  Neues Mixin erstellen ]**. Geben Sie in den angezeigten Textfeldern einen Anzeigenamen und eine Beschreibung für das neue Mixin ein. Klicken Sie auf**[!UICONTROL  Mixin hinzufügen ]**, wenn Sie damit fertig sind.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

The canvas reappears with &quot;[!UICONTROL Loyalty Relationship]&quot; appearing in the _[!UICONTROL Mixins]_section. Click the mixin name, then click**[!UICONTROL  Add Field ]**next to the root-level &quot;[!UICONTROL Loyalty Members]&quot; field.

![](../images/tutorials/relationship/loyalty-add-field.png)

Auf der Arbeitsfläche wird unter dem Namespace „\_tenantId“ ein neues Feld angezeigt. Under _[!UICONTROL Field Properties]_, provide a field name and display name for the field, and set its type to &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Klicken Sie abschließend auf **[!UICONTROL Übernehmen]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

The updated &quot;[!UICONTROL favoriteHotel]&quot; field appears in the canvas. Klicken Sie auf **[!UICONTROL Speichern]**, um die Änderungen am Schema abzuschließen.

![](../images/tutorials/relationship/relationship-field-save.png)

## Beziehungsfeld für das Quellschema definieren {#relationship-field}

Sobald in Ihrem Quellschema ein dediziertes Referenzfeld definiert ist, können Sie es als Beziehungsfeld festlegen.

Select the reference field in the canvas, then scroll down under _[!UICONTROL Field Properties]_until the**[!UICONTROL  Relationship ]**checkbox appears. Aktivieren Sie das Kontrollkästchen, um die erforderlichen Parameter für die Konfiguration eines Beziehungsfelds anzuzeigen.

![](../images/tutorials/relationship/relationship-checkbox.png)

Select the dropdown for **[!UICONTROL Reference Schema]** and select the destination schema for the relationship (&quot;[!UICONTROL Hotels]&quot; in this example). If the destination schema is enabled for Profile, the **[!UICONTROL Reference Identity Namespace]** field is automatically set to the namespace of the destination schema&#39;s primary identity. Wenn für das Schema keine primäre Identität definiert ist, müssen Sie den zu verwendenden Namespace manuell aus dem Dropdown-Menü auswählen. Klicken Sie auf **[!UICONTROL Übernehmen]**, wenn Sie damit fertig sind.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Das Feld wird in der Arbeitsfläche als Beziehung angezeigt und gibt den Namen und den Referenz-Identitäts-Namespace des Zielschemas an. Klicken Sie auf **[!UICONTROL Speichern]**, um Ihre Änderungen zu speichern und den Workflow zu beenden.

![](../images/tutorials/relationship/relationship-save.png)

## Nächste Schritte

By following this tutorial, you have successfully created a one-to-one relationship between two schemas using the [!DNL Schema Editor]. Anweisungen zum Definieren von Beziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).