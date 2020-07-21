---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors
topic: tutorials
translation-type: tm+mt
source-git-commit: 1445646be8fa3416a34408205eadca0a792290c6
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 58%

---


# Define a relationship between two schemas using the [!DNL Schema Editor]

Die Fähigkeit, Beziehungen zwischen Ihren Kunden und ihren Interaktionen mit Ihrer Marke über verschiedene Kanäle hinweg zu verstehen, ist ein wichtiger Bestandteil von Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data.

This document provides a tutorial for defining a one-to-one relationship between two schemas defined by your organization using the [!DNL Schema Editor] in the [!DNL Experience Platform] user interface. Anweisungen zum Definieren von Schemabeziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).

## Erste Schritte

Dieses Tutorial erfordert ein Arbeitsverständnis [!DNL XDM System] und die [!DNL Schema Editor] in der [!DNL Experience Platform] Benutzeroberfläche. Bevor Sie mit dieser Anleitung beginnen, lesen Sie folgende Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und seine Implementierung in Experience Platform.
* [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [Erstellen Sie ein Schema mit dem Schema-Editor](create-schema-ui.md): Ein Tutorial, das die Grundlagen der Arbeit mit dem [!DNL Schema Editor].

## Quell- und Zielschemas definieren

Es wird vorausgesetzt, dass Sie die beiden Schemas, die in der Beziehung definiert werden, bereits erstellt haben. For demonstration purposes, this tutorial creates a relationship between members of an organization&#39;s loyalty program (defined in a &quot;[!UICONTROL Loyalty Members]&quot; schema) and their favorite hotels (defined in a &quot;Hotels&quot; schema).

Schemabeziehungen werden durch ein **[!UICONTROL Quellschema]** mit einem Feld dargestellt, das auf ein anderes Feld innerhalb eines **[!UICONTROL Zielschemas]** verweist. In the steps that follow, &quot;[!UICONTROL Loyalty Members]&quot; will be the source schema, while &quot;Hotels&quot; will act as the destination schema.

Zu Referenzzwecken wird in den folgenden Abschnitten die Struktur der einzelnen Schemas beschrieben, die in dieser Anleitung verwendet werden, bevor eine Beziehung definiert wird.

### [!UICONTROL Schema „Mitglieder des Treueprogramms“]

The source schema &quot;[!UICONTROL Loyalty Members]&quot; is the schema that was constructed in the tutorial for [creating a schema in the UI](create-schema-ui.md). It includes a &quot;[!UICONTROL loyalty]&quot; object under its &quot;[!UICONTROL \_tenantId]&quot; namespace, which includes several loyalty-specific fields. One of these fields, &quot;[!UICONTROL loyaltyId]&quot;, serves as the primary identity for the schema under the &quot;[!UICONTROL Email]&quot; namespace. As seen under _Schema Properties_, this schema has been enabled for use in [!DNL Real-time Customer Profile](../../profile/home.md).

![](../images/tutorials/relationship/loyalty-members.png)

### Schema „Hotels“

The destination schema &quot;[!UICONTROL Hotels]&quot; contains fields that describe a hotel, include its address, brand, number of rooms, and star rating. The &quot;[!UICONTROL hotelId]&quot; field serves as the primary identity for the schema under the &quot;ECID&quot; namespace. Anders als &quot;[!UICONTROL Treueanwärter]&quot; wurde dieses Schema nicht aktiviert [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Beziehungs-Mixin erstellen

>[!NOTE]
>
>Dieser Schritt ist nur erforderlich, wenn Ihr Quellschema über kein dediziertes Zeichenfolgenfeld verfügt, das als Verweis auf ein anderes Schema verwendet werden kann. Wenn das Feld in Ihrem Quellschema bereits definiert ist, fahren Sie mit dem nächsten Schritt zum [Definieren eines Beziehungsfelds](#relationship-field) fort.

Um eine Beziehung zwischen zwei Schemas zu definieren, muss das Quellschema über ein dediziertes Feld verfügen, das als Verweis auf das Zielschema dient. Sie können dem Quellschema ein solches Feld hinzufügen, indem Sie ein neues Mixin erstellen.

Klicken Sie zunächst auf **[!UICONTROL Hinzufügen]** im Abschnitt _Mixins_.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Der Dialog [!UICONTROL _Mixin hinzufügen _]wird angezeigt. Klicken Sie hier auf**[!UICONTROL  Neues Mixin erstellen ]**. Geben Sie in den angezeigten Textfeldern einen Anzeigenamen und eine Beschreibung für das neue Mixin ein. Klicken Sie auf**[!UICONTROL  Mixin hinzufügen ]**, wenn Sie damit fertig sind.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

The canvas reappears with &quot;[!UICONTROL Favorite Hotel]&quot; appearing in the _Mixins_ section. Click the mixin name, then click **[!UICONTROL Add Field]** next to the root-level &quot;[!UICONTROL Loyalty Members]&quot; field.

![](../images/tutorials/relationship/loyalty-add-field.png)

A new field appears in the canvas under the &quot;[!UICONTROL \_tenantId]&quot; namespace. Under [!UICONTROL _Field Properties _], provide a field name and display name for the field, and set its type to &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Klicken Sie abschließend auf **[!UICONTROL Übernehmen]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

The updated &quot;[!UICONTROL favoriteHotel]&quot; field appears in the canvas. Klicken Sie auf **[!UICONTROL Speichern]**, um die Änderungen am Schema abzuschließen.

![](../images/tutorials/relationship/relationship-field-save.png)

## Beziehungsfeld für das Quellschema definieren {#relationship-field}

Sobald in Ihrem Quellschema ein dediziertes Referenzfeld definiert ist, können Sie es als Beziehungsfeld festlegen.

Klicken Sie in der Arbeitsfläche auf das Referenzfeld und scrollen Sie dann unter _[!UICONTROL Feldeigenschaften]_nach unten, bis das Kontrollkästchen**[!UICONTROL  Beziehung ]**erscheint. Aktivieren Sie das Kontrollkästchen, um die erforderlichen Parameter für die Konfiguration eines Beziehungsfelds anzuzeigen.

![](../images/tutorials/relationship/relationship-checkbox.png)

Click the dropdown for **[!UICONTROL Reference Schema]** and select the destination schema for the relationship (&quot;[!UICONTROL Hotels]&quot; in this example). Wenn das Zielschema für Vereinigungen aktiviert ist, wird das Feld **[!UICONTROL Referenz-Identitäts-Namespace]** automatisch auf den Namespace der primären Identität des Zielschemas festgelegt. Wenn für das Schema keine primäre Identität definiert ist, müssen Sie den zu verwendenden Namespace manuell aus dem Dropdown-Menü auswählen. Klicken Sie auf **[!UICONTROL Übernehmen]**, wenn Sie damit fertig sind.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Das Feld wird in der Arbeitsfläche als Beziehung angezeigt und gibt den Namen und den Referenz-Identitäts-Namespace des Zielschemas an. Klicken Sie auf **[!UICONTROL Speichern]**, um Ihre Änderungen zu speichern und den Workflow zu beenden.

![](../images/tutorials/relationship/relationship-save.png)

## Nächste Schritte

By following this tutorial, you have successfully created a one-to-one relationship between two schemas using the [!DNL Schema Editor]. Anweisungen zum Definieren von Beziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).