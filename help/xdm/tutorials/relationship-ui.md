---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors
description: Dieses Dokument bietet eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors in der Benutzeroberfläche "Experience Platform".
topic: tutorial
type: Tutorials
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 33%

---


# Define a relationship between two schemas using the [!DNL Schema Editor]

Die Möglichkeit, Beziehungen zwischen Ihren Kunden und deren Interaktionen mit Ihrer Marke kanalübergreifend zu analysieren, ist ein wichtiger Bestandteil von Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data.

Während Schema-Beziehungen durch die Verwendung des Vereinigung-Schemas abgeleitet werden können, gilt [!DNL Real-time Customer Profile]dies nur für Schema, die dieselbe Klasse gemeinsam haben. Zur Herstellung einer Beziehung zwischen zwei Schemas, die zu verschiedenen Klassen gehören, muss einem Quell-Schema ein dediziertes **Beziehungsfeld** hinzugefügt werden, das auf die Identität eines Ziel-Schemas verweist.

Dieses Dokument bietet eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors in der [!DNL Experience Platform] Benutzeroberfläche. Anweisungen zum Definieren von Schemabeziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).

## Erste Schritte

This tutorial requires a working understanding of [!DNL XDM System] and the Schema Editor in the [!DNL Experience Platform] UI. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und seine Implementierung in [!DNL Experience Platform].
* [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [Erstellen Sie ein Schema mit dem [!DNL Schema Editor]](create-schema-ui.md)folgenden: Ein Tutorial, das die Grundlagen der Arbeit mit dem [!DNL Schema Editor].

## Quell- und Zielschemas definieren

Wir gehen davon aus, dass Sie die beiden Schemas, die in der Beziehung definiert werden sollen, bereits erstellt haben. For demonstration purposes, this tutorial creates a relationship between members of an organization&#39;s loyalty program (defined in a &quot;[!DNL Loyalty Members]&quot; schema) and their favorite hotel (defined in a &quot;[!DNL Hotels]&quot; schema).

>[!IMPORTANT]
>
>Um eine Beziehung herzustellen, müssen beide Schema über definierte primäre Identitäten verfügen und für [!DNL Real-time Customer Profile]die sie aktiviert werden. Informationen zum Konfigurieren Ihrer Schema finden Sie im Abschnitt zum [Aktivieren eines Schemas für die Verwendung in Profil](./create-schema-ui.md#profile) im Lernprogramm zur Erstellung von Schemas.

Schema-Beziehungen werden durch ein dediziertes Feld innerhalb eines **Quell-Schemas** dargestellt, das auf ein anderes Feld innerhalb eines **Ziel-Schemas** verweist. In the steps that follow, &quot;[!DNL Loyalty Members]&quot; will be the source schema, while &quot;[!DNL Hotels]&quot; will act as the destination schema.

Zu Referenzzwecken wird in den folgenden Abschnitten die Struktur der einzelnen Schemas beschrieben, die in dieser Anleitung verwendet werden, bevor eine Beziehung definiert wird.

### [!DNL Loyalty Members] schema

Das Quellcode-Schema &quot;[!DNL Loyalty Members]&quot;basiert auf der [!DNL XDM Individual Profile] Klasse und ist das Schema, das im Lernprogramm zum [Erstellen eines Schemas in der Benutzeroberfläche](create-schema-ui.md)erstellt wurde. It includes a `loyalty` object under its `_tenantId` namespace, which includes several loyalty-specific fields. One of these fields, `loyaltyId`, serves as the primary identity for the schema under the [!UICONTROL Email] namespace. As seen under **[!UICONTROL Schema Properties]**, this schema has been enabled for use in [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Das Ziel-Schema &quot;[!DNL Hotels]&quot;basiert auf einer benutzerspezifischen &quot;[!DNL Hotels]&quot;-Klasse und enthält Hotelfelder. The `hotelId` field serves as the primary identity for the schema under a custom `hotelId` namespace. Wie das [!DNL Loyalty Members] Schema wurde auch dieses Schema aktiviert [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Beziehungs-Mixin erstellen

>[!NOTE]
>
>Dieser Schritt ist nur erforderlich, wenn Ihr Quell-Schema über kein dediziertes Zeichenfolgenfeld verfügt, das als Verweis auf das Ziel-Schema verwendet werden kann. Wenn das Feld in Ihrem Quellschema bereits definiert ist, fahren Sie mit dem nächsten Schritt zum [Definieren eines Beziehungsfelds](#relationship-field) fort.

Um eine Beziehung zwischen zwei Schemas zu definieren, muss das Quellschema über ein dediziertes Feld verfügen, das als Verweis auf das Zielschema dient. Sie können dem Quellschema ein solches Feld hinzufügen, indem Sie ein neues Mixin erstellen.

Start by selecting **[!UICONTROL Add]** in the **[!UICONTROL Mixins]** section.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Das Dialogfeld [!UICONTROL Mixin hinzufügen] wird angezeigt. From here, select **[!UICONTROL Create new mixin]**. Geben Sie in den angezeigten Textfeldern einen Anzeigenamen und eine Beschreibung für das neue Mixin ein. Select **[!UICONTROL Add mixin]** when finished.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

The canvas reappears with &quot;[!DNL Favorite Hotel]&quot; appearing in the **[!UICONTROL Mixins]** section. Wählen Sie den Namen der Mischung aus und wählen Sie dann **[!UICONTROL Hinzufügen Feld]** neben dem `Loyalty Members` Feld der Stammebene aus.

![](../images/tutorials/relationship/loyalty-add-field.png)

A new field appears in the canvas under the `_tenantId` namespace. Under **[!UICONTROL Field properties]**, provide a field name and display name for the field, and set its type to &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

When finished, select **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

The updated `favoriteHotel` field appears in the canvas. Select **[!UICONTROL Save]** to finalize your changes to the schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Beziehungsfeld für das Quellschema definieren {#relationship-field}

Sobald in Ihrem Quellschema ein dediziertes Referenzfeld definiert ist, können Sie es als Beziehungsfeld festlegen.

Select the `favoriteHotel` field in the canvas, then scroll down under **[!UICONTROL Field properties]** until the **[!UICONTROL Relationship]** checkbox appears. Aktivieren Sie das Kontrollkästchen, um die erforderlichen Parameter für die Konfiguration eines Beziehungsfelds anzuzeigen.

![](../images/tutorials/relationship/relationship-checkbox.png)

Select the dropdown for **[!UICONTROL Reference schema]** and select the destination schema for the relationship (&quot;[!DNL Hotels]&quot; in this example). If the destination schema is enabled for [!DNL Profile], the **[!UICONTROL Reference identity namespace]** field is automatically set to the namespace of the destination schema&#39;s primary identity. Wenn für das Schema keine primäre Identität definiert ist, müssen Sie den zu verwendenden Namespace manuell aus dem Dropdown-Menü auswählen. Select **[!UICONTROL Apply]** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

The `favoriteHotel` field is now highlighted as a relationship in the canvas, displaying the name and reference identity namespace of the destination schema. Select **[!UICONTROL Save]** to save your changes and complete the workflow.

![](../images/tutorials/relationship/relationship-save.png)

## Nächste Schritte

By following this tutorial, you have successfully created a one-to-one relationship between two schemas using the [!DNL Schema Editor]. Anweisungen zum Definieren von Beziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).