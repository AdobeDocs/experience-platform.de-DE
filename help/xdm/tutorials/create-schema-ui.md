---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Schemas mit dem Schema Editor
topic: tutorials
translation-type: tm+mt
source-git-commit: 661789fa15ea11b0e42060b1b90d74785c04fa1f
workflow-type: tm+mt
source-wordcount: '3376'
ht-degree: 57%

---


# Create a schema using the [!DNL Schema Editor]

The [!DNL Schema Registry] provides a user interface and RESTful API from which you can view and manage all resources in the Adobe Experience Platform [!DNL Schema Library]. The [!DNL Schema Library] contains resources made available to you by Adobe, Experience Platform partners, and vendors whose applications you use, as well as resources that you define and save to the [!DNL Schema Registry].

This tutorial covers the steps for creating a schema using the Schema Editor within [!DNL Experience Platform]. Wenn Sie lieber ein Schema mit der Schema Registry-API erstellen möchten, lesen Sie zunächst das [Entwicklerhandbuch für die Schema Registry](../api/getting-started.md), bevor Sie versuchen, [ein Schema mithilfe der API zu erstellen](create-schema-api.md).

Dieses Tutorial enthält außerdem Schritte zum [Definieren einer neuen Klasse](#create-new-class), die Sie dann zum Erstellen eines Schemas verwenden können.

## Erste Schritte

Dieses Tutorial erfordert ein Verständnis der verschiedenen Aspekte von Adobe Experience Platform, die mit der Verwendung des Schema Editors verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie die Dokumentation für die folgenden Konzepte:

* [!DNL Experience Data Model (XDM)](../home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
* [Grundlagen der Schema-Zusammensetzung](../schema/composition.md): Eine Übersicht über XDM-Schemas und ihre Bausteine, einschließlich Klassen, Mixins, Datentypen und Feldern.
* [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Für dieses Tutorial benötigen Sie Zugriff auf [!DNL Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding.

## Vorhandene Schemas im Arbeitsbereich „Schemas“ durchsuchen {#browse}

The Schemas workspace within [!DNL Experience Platform] provides a visualization of the [!DNL Schema Library], allowing you to view and manage all of the schemas available to you, as well as compose new ones. Der Arbeitsbereich umfasst auch den Schema Editor, die Arbeitsfläche, auf der Sie während dieses Tutorials ein Schema erstellen.

After logging into [!DNL Experience Platform], click **[!UICONTROL Schemas]** in the left-hand navigation and you will be taken to the Schemas workspace. You will see a list of schemas (a representation of the [!DNL Schema Library]) where you can view, manage, and customize all schemas available to you. Die Liste umfasst den Namen, den Typ, die Klasse und das Verhalten (Datensatz oder Zeitreihen), auf denen das Schema basiert, sowie das Datum und die Uhrzeit der letzten Änderung des Schemas.

Klicken Sie auf das Filtersymbol neben der Suchleiste, um Filterfunktionen für alle Ressourcen in der Registry zu verwenden, einschließlich Klassen, Mixins und Datentypen.

![Anzeigen der Schema Library](../images/tutorials/create-schema/schemas_filter.png)

## Erstellen und Benennen eines Schemas {#create}

Um mit dem Erstellen eines Schemas zu beginnen, klicken Sie rechts oben im Arbeitsbereich „Schemas“ auf **[!UICONTROL Schema erstellen]**.

![Schaltfläche „Schema erstellen“](../images/tutorials/create-schema/create_schema_button.png)

Der *Schema Editor* wird angezeigt. Dies ist die Arbeitsfläche, auf der Sie Ihr Schema zusammenstellen. Wenn Sie zum Editor gelangen, wird im Bereich *Struktur* der Arbeitsfläche automatisch ein „Unbenanntes Schema“ erstellt, das Sie bearbeiten können.

![Schema Editor](../images/tutorials/create-schema/schema_editor.png)

Auf der rechten Seite des Editors befinden sich die *Schema-Eigenschaften*, in denen Sie einen Namen für das Schema angeben können (mithilfe des Felds **[!UICONTROL Anzeigename]**). Sobald ein Name eingegeben wurde, wird die Arbeitsfläche aktualisiert und gibt den neuen Namen des Schemas wieder.

![Schema-Arbeitsfläche](../images/tutorials/create-schema/name_schema.png)

Bei der Entscheidung über einen Namen für Ihr Schema sind einige wichtige Aspekte zu beachten:

* Schemanamen sollten kurz und beschreibend sein, damit das Schema später leicht in der Bibliothek gefunden werden kann.
* Die Namen der Schemas müssen eindeutig sein, d. h. sie sollten so spezifisch sein, dass sie in Zukunft nicht wiederverwendet werden. Wenn Ihr Unternehmen z. B. über separate Loyalitätsprogramme für verschiedene Marken verfügt, wäre es ratsam, Ihr Schema mit „Loyalitätsmitglieder, Marke A“ zu benennen, damit Sie dieses leicht von anderen Loyalitätsschemas unterscheiden können, die Sie u. U. später definieren.
* Optional können Sie im Feld **[!UICONTROL Beschreibung]** weitere Informationen zum Schema angeben.

Dieses Tutorial stellt ein Schema zur Aufnahme von Daten über die Mitglieder eines Loyalitätsprogramms zusammen, daher heißt das Schema „Loyalitätsmitglieder“.

## Zuweisen einer Klasse {#class}

Auf der linken Seite des Editors befindet sich der Abschnitt *Komposition*. Dieser enthält derzeit zwei Unterabschnitte: *[!UICONTROL Schema]* und *[!UICONTROL Klasse]*.

Da das Schema nun einen Namen hat, können Sie jetzt die Klasse zuweisen, die vom Schema implementiert wird. Klicken Sie auf **[!UICONTROL Zuweisen]** neben *[!UICONTROL Klasse]*.

![](../images/tutorials/create-schema/assign_class_button.png)

Das Dialogfeld *[!UICONTROL Klasse zuweisen]* wird angezeigt. In diesem Fenster wird eine Liste aller verfügbaren Klassen angezeigt, einschließlich aller von Ihrem Unternehmen definierten Klassen (der Inhaber ist „Kunde“) sowie der von Adobe definierten Standardklassen.

Klicken Sie auf den Klassennamen, um die Beschreibung der Klasse anzuzeigen. Sie können auch die **[!UICONTROL Vorschau der Klassenstruktur]** auswählen, um die mit der Klasse verknüpften Felder und Metadaten anzuzeigen.

This tutorial uses the [!DNL XDM Individual Profile] class. Klicken Sie auf das Optionsfeld neben der Klasse, um sie auszuwählen, und klicken Sie dann auf **[!UICONTROL Klasse zuweisen]**.

![Dialogfeld „Klasse zuweisen“](../images/tutorials/create-schema/assign_class.png)

Die Arbeitsfläche wird wieder angezeigt. The *[!UICONTROL Class]* section now contains the class you selected ([!DNL XDM Individual Profile]) and the fields contributed by the [!DNL XDM Individual Profile] class are now visible within the *[!UICONTROL Structure]* section.

![Zugewiesene Klasse „XDM Individual Profile“](../images/tutorials/create-schema/class_assigned_structure.png)

Die Felder werden im Format „Feldname | Datentyp“ angezeigt. Die Schritte zum Definieren von Schemafeldern in der Benutzeroberfläche finden Sie weiter unten in diesem Tutorial.

>[!NOTE]
>
>Sie können [die Klasse eines Schemas](#change-class) jederzeit während des anfänglichen Kompositionsprozesses ändern, bevor das Schema gespeichert wird. Dies sollte jedoch mit größter Vorsicht geschehen. Mixins sind nur mit bestimmten Klassen kompatibel. Daher werden die Arbeitsfläche und alle von Ihnen hinzugefügten Felder durch Ändern der Klasse zurückgesetzt.

## Hinzufügen eines Mixins {#mixin}

Nachdem nun eine Klasse zugewiesen wurde, enthält der Abschnitt *Komposition* einen dritten Unterabschnitt: *[!UICONTROL Mixins]*.

Sie können nun beginnen, Ihrem Schema Felder hinzuzufügen, indem Sie Mixins hinzufügen. Ein Mixin ist eine Gruppe aus einem oder mehreren Feldern, die ein bestimmtes Konzept beschreiben. In diesem Tutorial werden Mixins verwendet, um die Mitglieder des Loyalitätsprogramms zu beschreiben und wichtige Informationen wie Name, Geburtstag, Telefonnummer, Adresse und mehr zu erfassen.

Um ein Mixin hinzuzufügen, klicken Sie auf **Hinzufügen** im Unterabschnitt *Mixins*.

![](../images/tutorials/create-schema/add_mixin_button.png)

Das Dialogfeld *[!UICONTROL Mixin hinzufügen]* wird angezeigt. Mixins are only intended for use with specific classes, therefore the list of mixins shows only those compatible with the class you selected (in this case, the [!DNL XDM Individual Profile] class).

Wenn Sie das Optionsfeld neben einem Mixin auswählen, haben Sie die Möglichkeit, eine **[!UICONTROL Vorschau der Mixin-Struktur]** anzuzeigen. Wählen Sie das Mixin „Persönliche Daten des Profils“ und klicken Sie dann auf **[!UICONTROL Mixin hinzufügen]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Die Arbeitsfläche des Schemas wird wieder angezeigt. The *[!UICONTROL Mixins]* section now lists the &quot;[!UICONTROL Profile Person Details]&quot; mixin and the *[!UICONTROL Structure]* section includes the fields contributed by the mixin.

![](../images/tutorials/create-schema/person_details_structure.png)

Dieses Mixin trägt mehrere Felder unter dem Namen der obersten Ebene „Person“ mit dem Datentyp „Person“ ein. Diese Gruppe von Feldern beschreibt Informationen zu einer Person, einschließlich Name, Geburtsdatum und Geschlecht.

>[!NOTE]
>
>Remember that fields may use scalar types (such as string, integer, array, or date) as their data type, as well as any &quot;data type&quot; (a group of fields representing a common concept) in the [!DNL Schema Registry].

Notice that the &quot;[!UICONTROL name]&quot; field has a data type of &quot;[!UICONTROL Person Name]&quot;, meaning it too describes a common concept and contains name-related sub-fields such as first name, last name, and full name.

Klicken Sie auf verschiedene Felder auf der Arbeitsfläche, um weitere Felder anzuzeigen, die sie zur Schema-Struktur beitragen.

## Hinzufügen eines weiteren Mixins {#mixin-2}

Sie können jetzt dieselben Schritte wiederholen, um ein weiteres Mixin hinzuzufügen. When you view the *[!UICONTROL Add Mixin]* dialog this time, notice that the &quot;[!UICONTROL Profile Person Details]&quot; mixin has been greyed out and the radio button next to it cannot be selected. Dadurch wird verhindert, dass Mixins, die bereits in Ihrem aktuellen Schema enthalten sind, versehentlich dupliziert werden.

Sie können nun das &quot;[!DNL Profile Personal Details" mixin] aus dem *[!UICONTROL Hinzufügen Mixin]* Dialog hinzufügen.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Nach dem Hinzufügen wird die Arbeitsfläche wieder angezeigt. The &quot;[!UICONTROL Profile Personal Details]&quot; is now listed under *[!UICONTROL Mixins]* in the *[!UICONTROL Composition]* section, and fields for home address, mobile phone, and more have been added under *[!UICONTROL Structure]*.

Similar to the &quot;[!UICONTROL name]&quot; field, the fields you just added represent multi-field concepts. For example, &quot;[!UICONTROL homeAddress]&quot; has a data type of &quot;[!UICONTROL Address]&quot; and &quot;[!UICONTROL mobilePhone]&quot; has a data type of &quot;[!UICONTROL Phone Number]&quot;. Sie können auf jedes dieser Felder klicken, um sie zu erweitern und die zusätzlichen Felder im Datentyp anzuzeigen.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definieren eines neuen Mixins {#define-mixin}

The &quot;[!UICONTROL Loyalty Members]&quot; schema is meant to capture data related to the members of a loyalty program, so it will require some specific loyalty-related fields. Es gibt keine standardmäßigen Mixins, die die erforderlichen Felder enthalten. Daher müssen Sie ein neues Mixin definieren.

Wenn Sie dieses Mal das Dialogfeld *[!UICONTROL Mixin hinzufügen]* öffnen, wählen Sie **[!UICONTROL Neues Mixin erstellen]**. Sie werden dann aufgefordert, einen **[!UICONTROL Anzeigenamen]** und eine **[!UICONTROL Beschreibung]** für Ihr Mixin anzugeben.

![](../images/tutorials/create-schema/mixin_create_new.png)

Wie bei Klassennamen sollte der Name des Mixins kurz und einfach sein und beschreiben, was das Mixin zum Schema beiträgt. Auch diese sind einzigartig, sodass Sie den Namen nicht wiederverwenden können und daher sicherstellen müssen, dass er spezifisch genug ist.

For this tutorial, name the new mixin &quot;[!UICONTROL Loyalty Details]&quot;.

Klicken Sie auf **[!UICONTROL Mixin hinzufügen]**, um zum Schema Editor zurückzukehren. &quot;[!UICONTROL Loyalty Details]&quot; should now appear under *[!UICONTROL Mixins]* on the left-side of the canvas, but there are no fields associated with it yet and therefore no new fields appear under *[!UICONTROL Structure]*.

## Hinzufügen von Feldern zum Mixin {#mixin-fields}

Now that you have created the &quot;[!UICONTROL Loyalty Details]&quot; mixin, it is time to define the fields that the mixin will contribute to the schema.

Klicken Sie zunächst auf den Namen des Mixins im Abschnitt *[!UICONTROL Mixins]*. Danach werden die *[!UICONTROL Mixin-Eigenschaften]* auf der rechten Seite des Editors angezeigt. Neben dem Namen des Schemas wird eine Schaltfläche **[!UICONTROL Feld hinzufügen]** unter *[!UICONTROL Struktur]* angezeigt.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Click **[!UICONTROL Add Field]** next to &quot;[!UICONTROL Loyalty Members]&quot; to create a new node in the structure. Dieser Knoten (in diesem Beispiel mit der Bezeichnung „_tenantId“) stellt die Mandanten-ID Ihrer IMS-Organisation dar, der ein Unterstrich vorangestellt ist. Das Vorhandensein der Mandanten-ID zeigt an, dass die Felder, die Sie hinzufügen, im Namensraum Ihres Unternehmens enthalten sind.

In other words, the fields you are adding are unique to your organization and are going to be saved in the [!DNL Schema Registry] in a specific area accessible only to your IMS Org. Fields you define must always be added to your namespace to prevent collisions with names from other standard classes, mixins, data types, and fields.

Inside that namespaced node is a &quot;[!UICONTROL New Field]&quot;. This is the beginning of the &quot;[!UICONTROL Loyalty Details]&quot; mixin.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Using *[!UICONTROL Field Properties]* on the right-hand side of the editor, start by creating a &quot;[!UICONTROL loyalty]&quot; field with type &quot;[!UICONTROL Object]&quot; that will be used to hold your loyalty-related fields. Klicken Sie abschließend auf **[!UICONTROL Übernehmen]**.

![](../images/tutorials/create-schema/loyalty_object.png)

The changes are applied and the newly created &quot;[!UICONTROL loyalty]&quot; object appears. Klicken Sie auf **[!UICONTROL Feld hinzufügen]** neben dem Objekt, um weitere loyalitätsbezogene Felder hinzuzufügen. Ein „Neues Feld“ wird angezeigt und der Abschnitt *[!UICONTROL Feldeigenschaften]* ist rechts auf der Arbeitsfläche sichtbar.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Für jedes Feld sind die folgenden Informationen erforderlich:

* **[!UICONTROL Feldname]:**Der Name des Felds, in Kamelschreibweise geschrieben. Beispiel: LoyalitätsStufe
* **[!UICONTROL Anzeigename]:**Der Name des Felds, in der Titelschrift geschrieben. Beispiel: Loyalitäts-Stufe
* **[!UICONTROL Typ]:**Der Datentyp des Felds. This includes basic scalar types and any data types defined in the[!DNL Schema Registry]. Beispiele: Zeichenfolge, Ganzzahl, Boolescher Wert, Person, Adresse, Telefonnummer usw.
* **[!UICONTROL Beschreibung]:**Es sollte eine optionale Beschreibung des Feldes eingefügt werden, die im Satzfall verfasst ist. (max. 200 Zeichen)

The first field for the Loyalty object will be a string called &quot;[!UICONTROL loyaltyId]&quot;. When setting the new field&#39;s type to &quot;[!UICONTROL String]&quot;, the *[!UICONTROL Field Properties]* window becomes populated with several options for applying constraints, including **[!UICONTROL Default Value]**, **[!UICONTROL Format]**, and **[!UICONTROL Maximum Length]**.

![](../images/tutorials/create-schema/string_constraints.png)

Je nach ausgewähltem Datentyp stehen verschiedene Einschränkungsoptionen zur Verfügung. Since &quot;[!UICONTROL loyaltyId]&quot; will be an email address, select &quot;[!UICONTROL email]&quot; from the **[!UICONTROL Format]** dropdown menu. Wählen Sie **[!UICONTROL Übernehmen]**, um Ihre Änderungen anzuwenden.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Hinzufügen von mehr Feldern zum Mixin {#mixin-fields-2}

Now that you have added the &quot;[!UICONTROL loyaltyId]&quot; field, you can add additional fields to capture loyalty-related information such as:

* Punkte (Ganzzahl)
* Mitglied seit (Datum)

Jedes Feld wird hinzugefügt, indem Sie auf dem Loyalitätsobjekt auf **[!UICONTROL Feld hinzufügen]** klicken und die erforderlichen Informationen eingeben.

Nach Abschluss des Vorgangs enthält das Loyalitätsobjekt die Felder: „Loyalitäts-ID“, „Punkte“ und „Mitglied seit“.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Hinzufügen des Felds „enum“ zum Mixin {#enum}

Beim Definieren von Feldern im Schema Editor gibt es einige zusätzliche Optionen, die Sie auf einfache Feldtypen anwenden können, um weitere Einschränkungen für die Daten, die das Feld enthalten kann, bereitzustellen.

An example of this would be a &quot;[!UICONTROL Loyalty Level]&quot; field, where the value can only be one of four possible options. To add this field to the schema, click **[!UICONTROL Add Field]** beside the &quot;[!UICONTROL loyalty]&quot; object and fill in the required fields under *[!UICONTROL Field Properties]*.

Wählen Sie „Zeichenfolge“ für **[!UICONTROL Typ]** und Sie sehen zusätzliche Kontrollkästchen für **[!UICONTROL Array]**, **[!UICONTROL Enum]** und **[!UICONTROL Identität]**.

Aktivieren Sie das Kontrollkästchen **[!UICONTROL Enum]**, um den nachstehenden Abschnitt *[!UICONTROL Enum-Werte]* zu öffnen. Hier können Sie für jede akzeptable Loyalitätsstufe den **[!UICONTROL Wert]** (in Binnenmajuskel-Schreibweise) und die **[!UICONTROL Bezeichnung]** (einen optionalen, leserfreundlichen Namen in der Titelschreibweise) eingeben.

When you have completed all field properties, click **[!UICONTROL Apply]** and the &quot;[!UICONTROL loyaltyLevel]&quot; field will be added to the &quot;loyalty&quot; object.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

Weitere Informationen zu verfügbaren zusätzlichen Einschränkungen:

* **[!UICONTROL Erforderlich]:**Gibt an, dass das Feld für die Datenerfassung erforderlich ist. Daten, die auf Grundlage dieses Schemas in einen Datensatz hochgeladen wurden und dieses Feld nicht enthalten, schlagen bei der Aufnahme fehl.
* **[!UICONTROL Array]:**Gibt an, dass das Feld ein Array von Werten mit jeweils dem angegebenen Datentyp enthält. Wenn Sie beispielsweise den Datentyp „Zeichenfolge“ auswählen und das Kontrollkästchen „Array“ aktivieren, enthält das Feld ein Zeichenfolgen-Array.
* **[!UICONTROL Enum]:**Gibt an, dass dieses Feld einen der Werte aus einer aufgezählten Liste möglicher Werte enthalten muss.
* **[!UICONTROL Identität]:**Gibt an, dass dieses Feld ein Identitätsfeld ist. Weitere Informationen zu Identitätsfeldern finden Sie[weiter unten in diesem Tutorial](#identity-field).

## Konvertieren eines Objekts mit mehreren Feldern in einen Datentyp {#datatype}

After adding several loyalty-specific fields, the &quot;[!UICONTROL loyalty]&quot; object now contains a common data structure that could be useful in other schemas.

Wenn Sie der Meinung sind, dass eine Struktur mit mehreren Feldern wiederverwendbar sein könnte, und Sie die Flexibilität haben möchten, dieselbe Datenstruktur an anderer Stelle zu verwenden, ermöglicht der Schema Editor die Konvertierung dieser Struktur in einen Datentyp.

Datentypen ermöglichen den konsistenten Einsatz von Strukturen mit mehreren Feldern und bieten mehr Flexibilität als ein Mixin, da sie überall in einem Schema verwendet werden können. Dies geschieht, indem der **[!UICONTROL Typ]** eines Felds in einem Mixin mit dem Datentyp festgelegt wird, der in der Registrierung definiert wurde.

To convert the &quot;[!UICONTROL loyalty]&quot; object to a data type, click on the &quot;loyalty&quot; field under *[!UICONTROL Structure]* and select **[!UICONTROL Convert to New Data Type]** on the right-hand-side of the editor under *[!UICONTROL Field Properties]*. A small green pop-up appears confirming &quot;[!UICONTROL Object Converted to Data Type]&quot;.

Now, when you look under *[!UICONTROL Structure]*, you can see that the &quot;[!UICONTROL loyalty]&quot; field has a data type of &quot;[!UICONTROL Loyalty]&quot; and the fields have small lock icons beside them indicating they are no longer individual fields, but rather part of a multi-field structure.

In a future schema, you could now assign a field the **[!UICONTROL Type]** of &quot;[!UICONTROL Loyalty]&quot; and it would automatically include Loyalty Level, Points, Member Since, and Loyalty ID fields.

![](../images/tutorials/create-schema/loyalty_data_type.png)

## Festlegen eines Schemafelds als Identitätsfeld {#identity-field}

Schemas are used for ingesting data into [!DNL Experience Platform], and that data is ultimately used to identify individuals and stitch together information coming from multiple sources. To help with this process, key fields can be marked as &quot;[!UICONTROL Identity]&quot; fields.

[!DNL Experience Platform] erleichtert die Identifizierung eines Identitätsfelds mithilfe eines **[!UICONTROL Identitäts]** -Kontrollkästchens im [!DNL Schema Editor].

So kann es beispielsweise Tausende von Mitgliedern des Loyalitätsprogramms geben, die derselben „Stufe“ angehören, allerdings hat jedes Mitglied des Loyalitätsprogramms eine eindeutige „loyaltyId“ (E-Mail-Adresse des jeweiligen Mitglieds). Die Tatsache, dass „loyaltyId“ eine eindeutige Kennung für jedes Mitglied ist, macht den Wert zu einem guten Kandidaten für ein Identitätsfeld, während „Stufe“ dies nicht ist.

In the *[!UICONTROL Structure]* section of the editor, click on the &quot;[!UICONTROL loyaltyId]&quot; field that you created and you will see the **[!UICONTROL Identity]** checkbox appear under *[!UICONTROL Field Properties]*. Markieren Sie das Kästchen. Sie haben die Option, dies als **[!UICONTROL primäre Identität]** festzulegen. Markieren Sie auch dieses Kästchen.

Als Nächstes müssen Sie einen **[!UICONTROL Identitätsnamensraum]** angeben. There are several pre-defined namespaces, but since the &quot;[!UICONTROL loyaltyId]&quot; is the member&#39;s email address, select &quot;Email&quot; from the dropdown list. You can now click **[!UICONTROL Apply]** to confirm the updates to the &quot;[!UICONTROL loyaltyId]&quot; field.

Now all data ingested into the &quot;[!UICONTROL loyaltyId]&quot; field will be used to help identify that individual and stitch together a single view of that customer.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Nachdem ein Schemafeld als primäre Identität festgelegt wurde, erhalten Sie eine Fehlermeldung, wenn Sie später versuchen, ein anderes Feld im Schema als primäres Feld festzulegen. Jedes Schema darf nur ein primäres Identitätsfeld enthalten.

To learn more about working with identities, please review the [!DNL Identity Service](../../identity-service/home.md) documentation.

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## Schema zur Verwendung in [!DNL Real-time Customer Profile] {#profile}

The Schema Editor provides the ability to enable a schema for use with [!DNL Real-time Customer Profile](../../profile/home.md). [!DNL Profile] bietet eine ganzheitliche Ansicht der einzelnen Kunden, indem ein robustes 360°-Profil mit Kundenattributen sowie ein zeitgestempeltes Benutzerkonto für jede Interaktion erstellt wird, die der Kunde über ein in das System integriertes System verfügt [!DNL Experience Platform].

In order for a schema to be enabled for use with [!DNL Real-time Customer Profile], it must have a primary identity defined. Sie erhalten die Fehlermeldung „Fehlende primäre Identität“, wenn Sie versuchen, ein Schema zu aktivieren, ohne vorher eine primäre Identität zu definieren.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

To enable the &quot;Loyalty Members&quot; schema for use in [!DNL Profile], begin by clicking on &quot;Loyalty Members&quot; in the *Structure* section of the editor.

Auf der rechten Seite des Editors werden unter *Schema-Eigenschaften* Informationen zum Schema angezeigt, einschließlich dessen Anzeigename, Beschreibung und Typ. Zusätzlich zu diesen Informationen gibt es eine Schaltfläche mit der Bezeichnung **[!UICONTROL Profil]**.

![](../images/tutorials/create-schema/unified_profile_toggle.png)

Click **[!UICONTROL Profile]** and a pop-up appears, asking you to confirm that you wish to enable the schema for [!DNL Profile].

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE]
>
>Once a schema has been enabled for [!DNL Real-time Customer Profile] and saved, it cannot be disabled.

## Nächste Schritte und zusätzliche Ressourcen

Now that you have finished composing a &quot;[!UICONTROL Loyalty Members]&quot; schema, you can see the complete schema in the *Structure* section of the editor. Click **[!UICONTROL Save]** and the schema will be saved to the [!DNL Schema Library], making it accessible by the [!DNL Schema Registry].

Your new schema is now able to be used to ingest data into [!DNL Platform]. Denken Sie daran, dass nach Verwendung des Schemas zur Datenaufnahme nur noch Ergänzungen vorgenommen werden können. Weitere Informationen zur Schemaversionierung finden Sie in den [Grundlagen der Schema-Komposition](../schema/composition.md).

The &quot;[!UICONTROL Loyalty Members]&quot; schema is also available to be viewed and managed using the [!DNL Schema Registry] API. Um mit der API zu arbeiten, lesen Sie zunächst das [Entwicklerhandbuch für die Schema Registry-API](../api/getting-started.md).

>[!WARNING]
>
>Die in den folgenden Videos dargestellte [!DNL Platform] Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der obigen Dokumentation.

Das folgende Video zeigt, wie Sie ein einfaches Schema in der [!DNL Platform] Benutzeroberfläche erstellen.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

Das folgende Video soll Ihnen die Arbeit mit Mixins und Klassen erleichtern.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Anhang

Die folgenden Informationen ergänzen das Tutorial zum Schema Editor.

### Neue Klasse erstellen {#create-new-class}

[!DNL Experience Platform] bietet die Flexibilität, ein Schema auf der Grundlage einer Klasse zu definieren, die spezifisch für Ihr Unternehmen ist.

Öffnen Sie das Dialogfeld *[!UICONTROL Klasse zuweisen]*, indem Sie im Schema Editor im Abschnitt **[!UICONTROL Klasse]** auf *[!UICONTROL Zuweisen]* klicken. Within the dialog, select **C[!UICONTROL reate New Class ]**.

You can then give your new class a **[!UICONTROL Display Name]** (a short, descriptive, unique, and user-friendly name for the class), a **[!UICONTROL Description]**, and a **[!UICONTROL Behavior]** (&quot;[!UICONTROL Record]&quot; or &quot;[!UICONTROL Time Series]&quot;) for the data the schema will define.

![Neue Klassendetails](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE]
>
>Denken Sie beim Erstellen eines Schemas, das eine von Ihrem Unternehmen definierte Klasse implementiert, daran, dass Mixins nur für kompatible Klassen verfügbar sind. Da die von Ihnen definierte Klasse neu ist, sind keine kompatiblen Mixins im Dialogfeld *Mixin hinzufügen* aufgeführt. Stattdessen müssen Sie **[!UICONTROL Neues Mixin erstellen]** auswählen und ein Mixin definieren, das mit dieser Klasse verwendet werden soll. Wenn Sie das nächste Mal ein Schema erstellen, das die neue Klasse implementiert, wird das von Ihnen definierte Mixin aufgelistet und ist zur Verwendung verfügbar.

### Klasse eines Schemas ändern {#change-class}

Sie können jederzeit während der anfänglichen Erstellung des Schemas vor dem Speichern des Schemas die Klasse ändern, auf der das Schema basiert.

>[!WARNING]
>
>Gehen Sie beim Ändern der Klasse vorsichtig vor. Mixins sind nur mit bestimmten Klassen kompatibel. Wenn Sie die Klasse ändern, wird die Arbeitsfläche daher zurückgesetzt und alle Felder, die Sie zu diesem Punkt hinzugefügt haben, werden entfernt.

Um die Klasse zu ändern, klicken Sie im Editor im Abschnitt **[!UICONTROL Komposition]** neben *[!UICONTROL Klasse]* auf *[!UICONTROL Zuweisen]*.

Wenn das Dialogfeld *[!UICONTROL Klasse zuweisen]* geöffnet wird, können Sie eine neue Klasse aus der verfügbaren Liste auswählen. Klicken Sie auf **[!UICONTROL Klasse zuweisen]**. Daraufhin wird ein neues Dialogfeld mit der Aufforderung angezeigt, zu bestätigen, dass Sie eine neue Klasse zuweisen möchten.

![Klasse ändern](../images/tutorials/create-schema/assign_new_class_warning.png)

Wenn Sie die Klassenänderung bestätigen, wird die Arbeitsfläche zurückgesetzt und der gesamte Kompositionsprozess geht verloren.