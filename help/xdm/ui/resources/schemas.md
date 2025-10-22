---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Datenmodell;UI;Arbeitsbereich;Schema;Schemata;
solution: Experience Platform
title: Erstellen und Bearbeiten von Schemas in der Benutzeroberfläche
description: Erfahren Sie mehr über die Grundlagen zum Erstellen und Bearbeiten von Schemas in der Benutzeroberfläche von Experience Platform.
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: dc5ac5427e1eeef47434c3974235a1900d29b085
workflow-type: tm+mt
source-wordcount: '4652'
ht-degree: 3%

---

# Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche {#create-edit-schemas-in-ui}

Dieses Handbuch bietet einen Überblick darüber, wie Sie Experience-Datenmodell(XDM)-Schemas für Ihr Unternehmen in der Adobe Experience Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

>[!IMPORTANT]
>
>XDM-Schemata sind extrem anpassbar, sodass die Schritte, die zum Erstellen eines Schemas erforderlich sind, je nachdem, welche Art von Daten das Schema erfassen soll, variieren können. Daher behandelt dieses Dokument nur die grundlegenden Interaktionen, die Sie mit Schemata in der Benutzeroberfläche durchführen können, und schließt zugehörige Schritte wie das Anpassen von Klassen, Schemafeldern, Datentypen und Feldern aus.
>
>Eine vollständige Übersicht über den Prozess der Schemaerstellung finden Sie im Abschnitt [Tutorial zur Schemaerstellung](../../tutorials/create-schema-ui.md) , um ein vollständiges Beispielschema zu erstellen und sich mit den vielen Funktionen der [!DNL Schema Editor] vertraut zu machen.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Grundverständnis des XDM-Systems voraus. Unter [XDM-Übersicht](../../home.md) finden Sie eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und unter [Grundlagen der Schemakomposition](../../schema/composition.md) finden Sie einen Überblick über die Erstellung von Schemas.

## Erstellen eines neuen Schemas {#create}

Wählen Sie im Arbeitsbereich [!UICONTROL Schemas] oben rechts **[!UICONTROL Create schema]** aus. Das Dropdown-Menü „Schematyp auswählen“ wird mit Optionen für [!UICONTROL Standard] oder [!UICONTROL Relational] Schemata angezeigt.

![Der Arbeitsbereich „Schemata“ mit hervorgehobener [!UICONTROL Create Schema] und dem Dropdown-Menü „Schematyp auswählen“](../../images/ui/resources/schemas/create-schema.png).

## Relationales Schema erstellen {#create-relational-schema}

>[!AVAILABILITY]
>
>Data Mirror und relationale Schemata stehen Adobe Journey Optimizer-Lizenzinhabern **Orchestrierte Kampagnen** zur Verfügung. Sie sind auch als **eingeschränkte Version** für Customer Journey Analytics-Benutzer verfügbar, je nach Ihrer Lizenz und der Aktivierung von Funktionen. Wenden Sie sich an den Adobe-Support, um Zugang zu erhalten.

>[!NOTE]
>
>Relationale Schemata wurden in früheren Versionen der Adobe Experience Platform-Dokumentation zuvor als modellbasierte Schemata bezeichnet.

Wählen Sie **[!UICONTROL Relational]** aus, um strukturierte Schemata im relationalen Stil mit einer differenzierten Kontrolle über Datensätze zu definieren. Relationale Schemata unterstützen die Durchsetzung von Primärschlüsseln, die Versionierung auf Datensatzebene und Beziehungen auf Schemaebene über Primär- und Fremdschlüssel. Sie sind auch für die inkrementelle Aufnahme mithilfe der Änderungsdatenerfassung optimiert und unterstützen mehrere Datenmodelle, die in der Kampagnenorchestrierung, in der Data Distiller und in B2B-Implementierungen verwendet werden.

Weitere Informationen finden Sie in der Übersicht zu [Data Mirror](../../data-mirror/overview.md) oder [Relationales Schema](../../schema/relational.md) .

### Manuell erstellen {#create-manually}

>[!AVAILABILITY]
>
>Der DDL-Datei-Upload ist nur für Lizenzinhaber von Adobe Journey Optimizer Orchestered Campaign verfügbar. Ihre Benutzeroberfläche wird möglicherweise anders angezeigt.

Das Dialogfeld **[!UICONTROL Create a relational schema]** wird angezeigt. Sie können **[!UICONTROL Create manually]** oder [**[!UICONTROL Upload DDL file]**](#upload-ddl-file) auswählen, um die Schemastruktur zu definieren.

Wählen Sie im Dialogfeld **[!UICONTROL Create a relational schema]** die Option **[!UICONTROL Create manually]** und dann **[!UICONTROL Next]** aus.

![Das Dialogfeld „Relationales Schema erstellen“ mit der hervorgehobenen Option „Manuell erstellen“ und „Weiter“.](../../images/ui/resources/schemas/relational-dialog.png)

Die Seite **[!UICONTROL Relational schema details]** wird angezeigt. Geben Sie einen Anzeigenamen für das Schema und eine optionale Beschreibung ein und wählen Sie dann **[!UICONTROL Finish]** aus, um das Schema zu erstellen.

![Die Ansicht mit relationalen Schemadetails mit hervorgehobenen [!UICONTROL Schema display name], [!UICONTROL Description] und [!UICONTROL Finish].](../../images/ui/resources/schemas/relational-details.png)

Der Schema-Editor wird mit einer leeren Arbeitsfläche zum Definieren der Schemastruktur geöffnet. Sie können Felder wie gewohnt hinzufügen.

#### Feld für Versionskennung hinzufügen {#add-version-identifier}

Um die Versionsverfolgung zu aktivieren und die Datenerfassung bei Änderungen zu unterstützen, müssen Sie ein Feld für die Versionskennung in Ihrem Schema angeben. Wählen Sie im Schema-Editor das Pluszeichen (![A plus) aus.](/help/images/icons/plus.png)) neben dem Schemanamen, um ein neues Feld hinzuzufügen.

Geben Sie einen Feldnamen wie `updateSequence` ein und wählen Sie den Datentyp **[!UICONTROL DateTime]** oder **[!UICONTROL Number]** aus.

Aktivieren Sie in der rechten Leiste das Kontrollkästchen **[!UICONTROL Version Identifier]** und klicken Sie dann auf **[!UICONTROL Apply]** , um das Feld zu bestätigen.

![Der Schema-Editor mit einem DateTime-Feld namens `updateSequence` hinzugefügt und das Kontrollkästchen Versionskennung aktiviert.](../../images/ui/resources/schemas/add-version-identifier.png)

>[!IMPORTANT]
>
>Ein relationales Schema muss ein Feld zur Versionskennung enthalten, um Aktualisierungen auf Datensatzebene zu unterstützen und die Datenerfassung zu ändern.

Um Beziehungen zu definieren, wählen Sie im Schema-Editor die Option **[!UICONTROL Add Relationship]** aus, um Primär-/Fremdschlüsselbeziehungen auf Schemaebene zu erstellen. Weitere Informationen finden Sie im Tutorial [Hinzufügen &#x200B;](../../tutorials/relationship-ui.md#relationship-field) Beziehungen auf Schemaebene“.

Fahren Sie anschließend mit [Definieren von Primärschlüsseln](../fields/identity.md#define-a-identity-field) und [Hinzufügen zusätzlicher Felder](#add-field-groups) fort. Anleitungen zum Aktivieren der Änderungsdatenerfassung in Experience Platform-Quellen finden Sie [Handbuch zur Aufnahme der Änderungsdatenerfassung](../../../sources/tutorials/api/change-data-capture.md).

>[!NOTE]
>
>Nach dem Speichern zeigt das [!UICONTROL Type] Feld in der [!UICONTROL &#x200B; Schema properties] Seitenleiste an, dass es sich um ein [!UICONTROL Relational] handelt. Dies wird auch in der Detailseitenleiste in der Schema-Bestandsansicht angezeigt.
>&#x200B;>![Die Arbeitsfläche des Schema-Editors, auf der eine leere relationale Schemastruktur mit hervorgehobenem relationalen Typ angezeigt wird.](../../images/ui/resources/schemas/relational-empty-canvas.png)

### Hochladen einer DDL-Datei {#upload-ddl-file}

>[!AVAILABILITY]
>
>Der DDL-Datei-Upload ist nur für Lizenzinhaber von Adobe Journey Optimizer Orchestered Campaign verfügbar.

Verwenden Sie diesen Workflow, um das Schema durch Hochladen einer DDL-Datei zu definieren. Wählen Sie im Dialogfeld **[!UICONTROL Create a relational schema]** die Option **[!UICONTROL Upload DDL file]** aus und ziehen Sie dann entweder eine lokale DDL-Datei aus Ihrem System oder wählen Sie **[!UICONTROL Choose files]** aus. Experience Platform validiert das Schema und zeigt ein grünes Häkchen an, wenn der Datei-Upload erfolgreich war. Wählen Sie **[!UICONTROL Next]** aus, um den Upload zu bestätigen.

![Das Dialogfeld „Relationales Schema erstellen“ mit [!UICONTROL Upload DDL file] ausgewählten und hervorgehobenen [!UICONTROL Next].](../../images/ui/resources/schemas/upload-ddl-file.png)

Das Dialogfeld [!UICONTROL Select entities and fields to import] wird angezeigt, in dem Sie eine Vorschau des Schemas anzeigen können. Überprüfen Sie die Schemastruktur und verwenden Sie die Optionsfelder und Kontrollkästchen, um sicherzustellen, dass für jede Entität ein Primärschlüssel und eine Versionskennung angegeben sind.

>[!IMPORTANT]
>
>Die Tabellenstruktur muss einen **Primärschlüssel** und eine **Versionskennung** enthalten, z. B. ein `updateSequence` Feld vom Typ Datum/Uhrzeit oder Zahl.
>
>Für die Aufnahme von Änderungsdaten ist auch eine spezielle Spalte mit dem Namen `_change_request_type` vom Typ Zeichenfolge erforderlich, um die inkrementelle Verarbeitung zu ermöglichen. Dieses Feld gibt den Typ der Datenänderung an (z. B. `u` (upsert) oder `d` (delete)).

Während der Aufnahme sind Kontrollspalten wie `_change_request_type` zwar erforderlich, werden aber nicht im Schema gespeichert und erscheinen auch nicht in der endgültigen Schemastruktur. Wenn alles korrekt aussieht, wählen Sie **[!UICONTROL Done]** aus, um das Schema zu erstellen.

>[!NOTE]
>
>Die maximal unterstützte Dateigröße für einen DDL-Upload beträgt 10 MB.

![Die Ansicht zur Überprüfung des relationalen Schemas mit importierten Feldern wird angezeigt und [!UICONTROL Finish] hervorgehoben.](../../images/ui/resources/schemas/entities-and-files-to-inport.png)


Das Schema wird im Schema-Editor geöffnet, wo Sie die Struktur vor dem Speichern anpassen können.

Fahren Sie als Nächstes mit [Hinzufügen zusätzlicher Felder](#add-field-groups) und [Hinzufügen zusätzlicher Beziehungen auf &#x200B;](../../tutorials/relationship-ui.md#relationship-field) fort.

Anleitungen zum Aktivieren der Änderungsdatenerfassung in Experience Platform-Quellen finden Sie [Handbuch zur Aufnahme der Änderungsdatenerfassung](../../../sources/tutorials/api/change-data-capture.md).

## Erstellung eines Standardschemas {#standard-based-creation}

Wenn Sie im Dropdown-Menü „Schematyp auswählen“ die Option „Standardschematyp“ auswählen, wird das Dialogfeld &quot;[!UICONTROL Create a schema]&quot; angezeigt. In diesem Dialogfeld können Sie entweder manuell ein Schema erstellen, indem Sie Felder und Feldergruppen hinzufügen, oder Sie können eine CSV-Datei hochladen und ML-Algorithmen verwenden, um ein Schema zu generieren. Wählen Sie im Dialogfeld einen Workflow zur Schemaerstellung aus.

![Das Dialogfeld „Schema erstellen“ mit den Workflow-Optionen und hervorgehobener Auswahl.](../../images/ui/resources/schemas/create-a-schema-dialog.png)

### [!BADGE Beta]{type=Informative} Manuelle oder ML-unterstützte Schemaerstellung {#manual-or-assisted}

Informationen dazu, wie Sie einen ML-Algorithmus verwenden können, um eine Schemastruktur basierend auf einer CSV-Datei zu empfehlen, finden Sie [&#x200B; Handbuch zur Erstellung von Schemata durch maschinelles Lernen](../ml-assisted-schema-creation.md). Dieses Handbuch für die Benutzeroberfläche konzentriert sich auf den Workflow zur manuellen Erstellung.

### Manuelle Schemaerstellung {#manual-creation}

Der [!UICONTROL Create schema] Workflow wird angezeigt. Sie können eine Basisklasse für das Schema auswählen, indem Sie entweder **[!UICONTROL Individual Profile]**, **[!UICONTROL Experience Event]** oder **[!UICONTROL Other]** und dann zur Bestätigung **[!UICONTROL Next]** auswählen. Weitere Informationen zu diesen Klassen finden Sie in der Dokumentation zu [[!UICONTROL XDM individual profile]](../../classes/individual-profile.md) und [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md) .

![Der [!UICONTROL Create schema] Workflow mit den drei Klassenoptionen und [!UICONTROL Next] hervorgehoben.](../../images/ui/resources/schemas/schema-class-options.png)

Bei Auswahl von **[!UICONTROL Other]** wird eine Liste der verfügbaren Klassen angezeigt. Hier können Sie bereits vorhandene Klassen durchsuchen und filtern.

![Der [!UICONTROL Create schema] Workflow mit hervorgehobener [!UICONTROL Other] im [!UICONTROL Schema details] Abschnitt.](../../images/ui/resources/schemas/other-schema-details.png)

Wählen Sie ein Optionsfeld aus, um die Klassen danach zu filtern, ob es sich um benutzerdefinierte oder Standardklassen handelt. Sie können die verfügbaren Ergebnisse auch nach ihrer Branche filtern oder mithilfe des Suchfelds nach einer bestimmten Klasse suchen.

![Der [!UICONTROL Create schema]-Workflow mit Suchleiste, [!UICONTROL Custom] und [!UICONTROL Industries] hervorgehobenen Optionen.](../../images/ui/resources/schemas/filter-and-search.png)

Um Ihnen bei der Entscheidung über die entsprechende Klasse zu helfen, gibt es Informations- und Vorschausymbole für jede Klasse. Das Infosymbol (![Ein Infosymbol.](/help/images/icons/info.png)) Öffnet ein Dialogfeld, das eine Beschreibung der Klasse und der Branche enthält, mit der sie verknüpft ist.

![Das Infosymbol und die QuickInfo der ausgewählten Klasse sind hervorgehoben.](../../images/ui/resources/schemas/class-info.png)

Das Vorschausymbol (![Vorschausymbol).](/help/images/icons/preview.png)) Öffnet ein Vorschaudialogfeld für die Klasse, die ein Schemadiagramm und dessen Eigenschaften enthält.

![Eine Vorschau der ausgewählten Klasse mit dem Schemadiagramm und den Klasseneigenschaften.](../../images/ui/resources/schemas/class-preview.png)

Wählen Sie eine Zeile aus, um eine Klasse auszuwählen, und klicken Sie dann auf **[!UICONTROL Next]** , um Ihre Auswahl zu bestätigen.

![Der [!UICONTROL Create schema]-Workflow mit einer Klasse, die aus der Tabelle der verfügbaren Klassen ausgewählt und [!UICONTROL Next] hervorgehoben wurde.](../../images/ui/resources/schemas/select-class.png)

Nachdem Sie eine Klasse ausgewählt haben, wird der Abschnitt [!UICONTROL Name and review] angezeigt. In diesem Abschnitt geben Sie einen Namen und eine Beschreibung ein, um Ihr Schema zu identifizieren. &#x200B;Die Basisstruktur des Schemas (bereitgestellt von der -Klasse) wird auf der Arbeitsfläche angezeigt, damit Sie Ihre ausgewählte Klassen- und Schemastruktur überprüfen und überprüfen können.

Geben Sie eine benutzerfreundliche [!UICONTROL Schema display name] in das Textfeld ein. Geben Sie als Nächstes eine geeignete Beschreibung ein, um Ihr Schema zu identifizieren. Wenn Sie Ihre Schemastruktur überprüft haben und mit Ihren Einstellungen zufrieden sind, wählen Sie **[!UICONTROL Finish]** aus, um Ihr Schema zu erstellen.

![Der [!UICONTROL Name and review] Abschnitt des [!UICONTROL Create schema]-Workflows mit Hervorhebung von [!UICONTROL Schema display name], [!UICONTROL Description] und [!UICONTROL Finish].](../../images/ui/resources/schemas/name-and-review.png)

Der Schema-Editor wird angezeigt, wobei die Schemastruktur auf der Arbeitsfläche angezeigt wird. Falls gewünscht, können Sie jetzt [Felder zur Klasse hinzufügen](../../ui/resources/classes.md#add-fields).

![Der Schema-Editor mit der Schemastruktur, die auf der Arbeitsfläche angezeigt wird.](../../images/ui/resources/schemas/edit.png)

## Bearbeiten eines vorhandenen Schemas {#edit}

>[!NOTE]
>
>Nachdem ein Schema gespeichert und bei der Datenaufnahme verwendet wurde, können nur additive Änderungen daran vorgenommen werden. Weitere Informationen finden [&#x200B; unter „Regeln &#x200B;](../../schema/composition.md#evolution) Schemaentwicklung“.

Um ein vorhandenes Schema zu bearbeiten, wählen Sie die Registerkarte **[!UICONTROL Browse]** und dann den Namen des Schemas aus, das Sie bearbeiten möchten. Sie können auch die Suchleiste verwenden, um die Liste der verfügbaren Optionen einzugrenzen.

![Der Arbeitsbereich „Schema“ mit einem hervorgehobenen Schema.](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Sie können die Such- und Filterfunktionen des Arbeitsbereichs verwenden, um das Schema leichter zu finden. Weitere Informationen finden Sie im Handbuch [Erkunden von XDM](../explore.md)Ressourcen“.

Nachdem Sie ein Schema ausgewählt haben, wird das [!DNL Schema Editor] mit der Schemastruktur auf der Arbeitsfläche angezeigt. Sie können jetzt [Feldergruppen hinzufügen](#add-field-groups) zum Schema (oder [einzelne Felder hinzufügen](#add-individual-fields) aus diesen Gruppen), [Anzeigenamen von Feldern bearbeiten](#display-names) oder [vorhandene benutzerdefinierte Feldergruppen bearbeiten](./field-groups.md#edit) wenn das Schema eine verwendet.

## Mehr Aktionen {#more}

Im Schema-Editor können Sie auch Schnellaktionen durchführen, um die JSON-Struktur des Schemas zu kopieren oder das Schema zu löschen, wenn es nicht für das Echtzeit-Kundenprofil aktiviert wurde oder über verknüpfte Datensätze verfügt. Wählen Sie oben in der Ansicht [!UICONTROL More] aus, um eine Dropdown-Liste mit Schnellaktionen anzuzeigen.

Mit der Funktion JSON-Struktur kopieren können Sie sehen, wie eine Beispiel-Payload aussehen würde, während Sie noch das Schema und Ihre Daten-Pipelines erstellen. Dies ist besonders hilfreich in Situationen, in denen es komplexe Objektzuordnungsstrukturen im Schema gibt, z. B. eine Identitätszuordnung.

![Der Schema-Editor mit der hervorgehobenen Schaltfläche „Mehr“ und den angezeigten Dropdown-Optionen.](../../images/tutorials/create-schema/more-actions.png)

## Umschalten zwischen Anzeigenamen {#display-name-toggle}

Der Einfachheit halber bietet der Schema-Editor einen Umschalter zum Wechseln zwischen den ursprünglichen Feldnamen und den für Menschen besser lesbaren Anzeigenamen. Diese Flexibilität ermöglicht eine verbesserte Erkennung und Bearbeitung von Feldern Ihrer Schemata. Der Umschalter befindet sich oben rechts in der Ansicht des Schema-Editors.

>[!NOTE]
>
>Die Änderung von Feldnamen in Anzeigenamen ist rein kosmetischer Natur und ändert keine nachgelagerten Ressourcen.

![Der Schema-Editor mit hervorgehobener [!UICONTROL Show display names for fields].](../../images/ui/resources/schemas/display-name-toggle.png)

Die Anzeigenamen für Standardfeldgruppen werden vom System generiert, können jedoch angepasst werden, wie im Abschnitt [Anzeigenamen](#display-names) beschrieben. Anzeigenamen werden in mehreren Benutzeroberflächenansichten angezeigt, einschließlich Zuordnungs- und Datensatzvorschauen. Die Standardeinstellung ist deaktiviert und zeigt Feldnamen anhand ihrer ursprünglichen Werte an.

## Hinzufügen von Feldergruppen zu einem Schema {#add-field-groups}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie einem Schema vorhandene Feldergruppen hinzufügen. Wenn Sie eine neue benutzerdefinierte Feldergruppe erstellen möchten, lesen Sie stattdessen das Handbuch unter [Erstellen und Bearbeiten von Feldergruppen](./field-groups.md#create) .

Nachdem Sie ein Schema in der [!DNL Schema Editor] geöffnet haben, können Sie dem Schema mithilfe von Feldergruppen Felder hinzufügen. Wählen Sie zunächst **[!UICONTROL Add]** neben **[!UICONTROL Field groups]** in der linken Leiste aus.

![Der Schema-Editor mit der hervorgehobenen [!UICONTROL Add] aus dem [!UICONTROL Field groups] Abschnitt.](../../images/ui/resources/schemas/add-field-group-button.png)

Es wird ein Dialogfeld mit einer Liste von Feldergruppen angezeigt, die Sie für das Schema auswählen können. Da Feldergruppen nur mit einer Klasse kompatibel sind, werden nur die Feldergruppen aufgelistet, die mit der ausgewählten Klasse des Schemas verknüpft sind. Standardmäßig werden die aufgelisteten Feldergruppen nach ihrer Verwendungspopularität in Ihrer Organisation sortiert.

![Das hervorgehobene Dialogfeld &quot;[!UICONTROL Add field groups]&quot; mit hervorgehobener Spalte &quot;[!UICONTROL Popularity]&quot;.](../../images/ui/resources/schemas/field-group-popularity.png)

Wenn Sie den allgemeinen Aktivitäts- oder Geschäftsbereich der Felder kennen, die Sie hinzufügen möchten, wählen Sie in der linken Leiste mindestens eine der branchenvertikalen Kategorien aus, um die angezeigte Liste der Feldergruppen zu filtern.

![Das hervorgehobene Dialogfeld &quot;[!UICONTROL Add field groups]&quot; mit [!UICONTROL Industry] und hervorgehobener Spalte &quot;[!UICONTROL Industry]&quot;.](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Weitere Informationen zu Best Practices für die branchenspezifische Datenmodellierung in XDM finden Sie in der Dokumentation zu [branchenspezifischen Datenmodellen](../../schema/industries/overview.md).

Sie können auch die Suchleiste verwenden, um Ihre gewünschte Feldergruppe zu finden. Feldergruppen, deren Name mit der Abfrage übereinstimmt, werden oben in der Liste angezeigt. Unter **[!UICONTROL Standard Fields]** werden Feldergruppen angezeigt, die Felder enthalten, die die gewünschten Datenattribute beschreiben.

![Das [!UICONTROL Add field groups] mit hervorgehobener Suchfunktion &quot;[!UICONTROL Standard fields]&quot;.](../../images/ui/resources/schemas/field-group-search.png)

Aktivieren Sie das Kontrollkästchen neben dem Namen der Feldergruppe, die Sie dem Schema hinzufügen möchten. Sie können mehrere Feldergruppen aus der Liste auswählen, wobei jede ausgewählte Feldergruppe in der rechten Leiste angezeigt wird.

![Das Dialogfeld &quot;[!UICONTROL Add field groups]&quot; mit hervorgehobener Kontrollkästchenauswahl-Funktion.](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Für jede aufgelistete Feldergruppe können Sie den Mauszeiger über das Informationssymbol (![Informationssymbol](/help/images/icons/info.png)) bewegen oder den Fokus darauf legen, um eine kurze Beschreibung der Art von Daten anzuzeigen, die die Feldergruppe erfasst. Sie können auch auf das Vorschausymbol (![Vorschausymbol](/help/images/icons/preview.png)) klicken, um die Struktur der Felder anzuzeigen, die die Feldergruppe bereitstellt, bevor Sie sie zum Schema hinzufügen.

Nachdem Sie Ihre Feldergruppen ausgewählt haben, wählen Sie **[!UICONTROL Add field groups]** aus, um sie zum Schema hinzuzufügen.

![Das Dialogfeld &quot;[!UICONTROL Add field groups]&quot; mit ausgewählten Feldergruppen [!UICONTROL Add field groups] hervorgehoben.](../../images/ui/resources/schemas/add-field-group-finish.png)

Der [!DNL Schema Editor] wird erneut mit den von den Feldergruppen bereitgestellten Feldern angezeigt, die auf der Arbeitsfläche dargestellt werden.

![Die [!DNL Schema Editor] mit einem angezeigten Beispielschema.](../../images/ui/resources/schemas/field-groups-added.png)

>[!NOTE]
>
>Innerhalb des Schema-Editors werden Standardklassen (Adobe-generiert) und Feldergruppen mit dem Schlosssymbol (![&#x200B; Schlosssymbol) gekennzeichnet.](/help/images/icons/lock-closed.png). Das Vorhängeschloss wird in der linken Leiste neben dem Namen der Klasse oder Feldergruppe sowie neben einem beliebigen Feld im Schemadiagramm angezeigt, das Teil einer systemgenerierten Ressource ist.
>
>![Der Schema-Editor mit hervorgehobenem Vorhängeschloss-Symbol](../../images/ui/explore/schema-editor-padlock-icon.png)

Nachdem Sie eine Feldergruppe zu einem Schema hinzugefügt haben, können Sie optional [vorhandene Felder entfernen](#remove-fields) oder [neue benutzerdefinierte Felder hinzufügen](#add-fields) zu diesen Gruppen hinzufügen, je nach Ihren Anforderungen.

### Entfernen hinzugefügter Felder aus Feldergruppen {#remove-fields}

Nachdem Sie eine Feldergruppe zu einem Schema hinzugefügt haben, können Sie Felder entweder global aus der Feldergruppe entfernen oder lokal aus dem aktuellen Schema ausblenden. Um unbeabsichtigte Schemaänderungen zu vermeiden, ist es wichtig, den Unterschied zwischen diesen Aktionen zu verstehen.

>[!IMPORTANT]
>
>Durch Auswahl von **[!UICONTROL Remove]** wird das Feld aus der Feldergruppe selbst gelöscht, was sich auf *alle* Schemata auswirkt, die diese Feldergruppe verwenden.
>&#x200B;>Verwenden Sie diese Option nur, wenn Sie **Feld aus jedem Schema entfernen möchten, das die Feldergruppe**.

Um ein Feld aus der Feldergruppe zu löschen, wählen Sie es auf der Arbeitsfläche aus und wählen Sie in der rechten Leiste **[!UICONTROL Remove]** aus. Dieses Beispiel zeigt das `taxId` Feld aus der **[!UICONTROL Demographic Details]**.

![Der [!DNL Schema Editor] mit hervorgehobener [!UICONTROL Remove]. Diese Aktion entfernt ein einzelnes Feld.](../../images/ui/resources/schemas/remove-single-field.png)

Um mehrere Felder aus einem Schema auszublenden, ohne sie aus der Feldergruppe selbst zu entfernen, verwenden Sie die Option **[!UICONTROL Manage related fields]** . Wählen Sie auf der Arbeitsfläche ein beliebiges Feld aus der Gruppe und dann in der rechten Leiste **[!UICONTROL Manage related fields]** aus.

![Der [!DNL Schema Editor] mit hervorgehobenem [!UICONTROL Manage related fields].](../../images/ui/resources/schemas/manage-related-fields.png)

Es wird ein Dialogfeld mit der Struktur der Feldergruppe angezeigt. Aktivieren oder deaktivieren Sie mithilfe der Kontrollkästchen die Felder, die Sie einbeziehen möchten.

![Das Dialogfeld &quot;[!UICONTROL Manage related fields]&quot; mit ausgewählten Feldern und hervorgehobenen [!UICONTROL Confirm].](../../images/ui/resources/schemas/select-fields.png)

Wählen Sie **[!UICONTROL Confirm]** aus, um die Arbeitsfläche zu aktualisieren und Ihre ausgewählten Felder widerzuspiegeln.


![Felder hinzugefügt](../../images/ui/resources/schemas/fields-added.png)

### Feldverhalten beim Entfernen oder Verwerfen von Feldern {#field-removal-deprecation-behavior}

Die nachstehende Tabelle zeigt den Umfang der einzelnen Aktionen.

| Aktion | Gilt nur für das aktuelle Schema | Ändert die Feldergruppe | Wirkt sich auf andere Schemata aus | Beschreibung |
|--------------------------|--------------------------------|----------------------|-----------------------|-------------|
| **Feld entfernen** | Nein | Ja | Ja | Löscht das Feld aus der Feldergruppe. Dadurch wird sie aus allen Schemata entfernt, die diese Gruppe verwenden. |
| **Verwalten verwandter Felder** | Ja | Nein | Nein | Blendet nur Felder aus dem aktuellen Schema aus. Die Feldergruppe bleibt unverändert. |
| **Feld verwerfen** | Nein | Ja | Ja | Markiert das Feld in der Feldergruppe als veraltet. Sie ist nicht mehr zur Verwendung in einem Schema verfügbar. |

>[!NOTE]
>
>Dieses Verhalten ist sowohl bei datensatzbasierten als auch bei ereignisbasierten Schemata konsistent.

### Hinzufügen benutzerdefinierter Felder zu Feldergruppen {#add-fields}

Nachdem Sie eine Feldergruppe zu einem Schema hinzugefügt haben, können Sie zusätzliche Felder für diese Gruppe definieren. Alle Felder, die einer Feldergruppe in einem Schema hinzugefügt wurden, werden jedoch auch in allen anderen Schemata angezeigt, die dieselbe Feldergruppe verwenden.

Wenn ein benutzerdefiniertes Feld zu einer Standardfeldgruppe hinzugefügt wird, wird diese Feldgruppe außerdem in eine benutzerdefinierte Feldgruppe konvertiert, und die ursprüngliche Standardfeldgruppe ist nicht mehr verfügbar.

Wenn Sie ein benutzerdefiniertes Feld zu einer Standardfeldgruppe hinzufügen möchten, finden Sie im [&#x200B; Abschnitt unten &#x200B;](#custom-fields-for-standard-groups) spezifische Anweisungen. Wenn Sie Felder zu einer benutzerdefinierten Feldergruppe hinzufügen, lesen Sie den Abschnitt [Bearbeiten benutzerdefinierter Feldergruppen](./field-groups.md) im Handbuch zur Benutzeroberfläche für Feldergruppen.

Wenn Sie keine vorhandenen Feldergruppen ändern möchten, können Sie stattdessen [neue benutzerdefinierte Feldergruppe erstellen](./field-groups.md#create) um zusätzliche Felder zu definieren.

## Hinzufügen einzelner Felder zu einem Schema {#add-individual-fields}

Mit dem Schema-Editor können Sie einzelne Felder direkt zu einem Schema hinzufügen, wenn Sie nicht eine ganze Feldergruppe für einen bestimmten Anwendungsfall hinzufügen möchten. Sie können stattdessen [einzelne Felder aus Standardfeldgruppen hinzufügen](#add-standard-fields) oder [eigene benutzerdefinierte Felder hinzufügen](#add-custom-fields).

>[!IMPORTANT]
>
>Obwohl Sie mit dem Schema-Editor einzelne Felder direkt zu einem Schema hinzufügen können, ändert dies nichts an der Tatsache, dass alle Felder in einem XDM-Schema von der Klasse oder einer Feldergruppe bereitgestellt werden müssen, die mit dieser Klasse kompatibel ist. Wie in den folgenden Abschnitten erläutert, werden alle einzelnen Felder als wichtiger Schritt weiterhin einer Klasse oder Feldergruppe zugeordnet, wenn sie einem Schema hinzugefügt werden.

### Standardfelder hinzufügen {#add-standard-fields}

Sie können Felder aus Standardfeldgruppen direkt zu einem Schema hinzufügen, ohne die entsprechende Feldgruppe zuvor kennen zu müssen. Um ein Standardfeld zu einem Schema hinzuzufügen, klicken Sie auf das Pluszeichen (**+**) neben dem Namen des Schemas auf der Arbeitsfläche. Ein **[!UICONTROL Untitled Field]** Platzhalter wird in der Schemastruktur angezeigt, und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Feld-Platzhalter](../../images/ui/resources/schemas/root-custom-field.png)

Geben Sie unter **[!UICONTROL Field name]** den Namen des Felds ein, das Sie hinzufügen möchten. Das System sucht automatisch nach Standardfeldern, die mit der Abfrage übereinstimmen, und listet sie unter **[!UICONTROL Recommended Standard Fields]** auf, einschließlich der Feldergruppen, zu denen sie gehören.

![Empfohlene Standardfelder](../../images/ui/resources/schemas/standard-field-search.png)

Während einige Standardfelder denselben Namen haben, kann ihre Struktur je nach der Feldergruppe, aus der sie stammen, variieren. Wenn ein Standardfeld in einem übergeordneten Objekt in der Feldergruppenstruktur verschachtelt ist, wird das übergeordnete Feld ebenfalls in das Schema aufgenommen, wenn das untergeordnete Feld hinzugefügt wird.

Wählen Sie das Vorschausymbol (![Vorschausymbol](/help/images/icons/preview.png)) neben einem Standardfeld aus, um die Struktur seiner Feldergruppe anzuzeigen und besser zu verstehen, wie sie verschachtelt werden könnte. Um das Standardfeld zum Schema hinzuzufügen, wählen Sie das Pluszeichen (![Pluszeichen](/help/images/icons/add-circle.png)) aus.

![Standardfeld hinzufügen](../../images/ui/resources/schemas/add-standard-field.png)

Die Arbeitsfläche wird aktualisiert und zeigt das zum Schema hinzugefügte Standardfeld an, einschließlich aller übergeordneten Felder, unter denen es in der Feldergruppenstruktur verschachtelt ist. Der Name der Feldergruppe wird auch unter **[!UICONTROL Field groups]** in der linken Leiste aufgeführt. Wenn Sie mehr Felder aus derselben Feldergruppe hinzufügen möchten, wählen Sie **[!UICONTROL Manage related fields]** in der rechten Leiste aus.

![Standardfeld hinzugefügt](../../images/ui/resources/schemas/standard-field-added.png)

### Benutzerdefinierte Felder hinzufügen        {#add-custom-fields}

Ähnlich wie beim Workflow für Standardfelder können Sie auch Ihre eigenen benutzerdefinierten Felder direkt zu einem Schema hinzufügen.

Um Felder zur Stammebene eines Schemas hinzuzufügen, klicken Sie auf das Pluszeichen (**+**) neben dem Namen des Schemas auf der Arbeitsfläche. Ein **[!UICONTROL Untitled Field]** Platzhalter wird in der Schemastruktur angezeigt, und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Benutzerdefiniertes Stammfeld](../../images/ui/resources/schemas/root-custom-field.png)

Beginnen Sie mit der Eingabe des Namens des Felds, das Sie hinzufügen möchten, und das System beginnt automatisch mit der Suche nach übereinstimmenden Standardfeldern. Um stattdessen ein neues benutzerdefiniertes Feld zu erstellen, wählen Sie die obere Option aus, an die **([!UICONTROL New Field]) angehängt ist**.

![Neues Feld](../../images/ui/resources/schemas/custom-field-search.png)

Nachdem Sie einen Anzeigenamen und Datentyp für das Feld angegeben haben, besteht der nächste Schritt darin, das Feld einer übergeordneten XDM-Ressource zuzuweisen. Wenn Ihr Schema eine benutzerdefinierte Klasse verwendet, können Sie stattdessen [das Feld zur zugewiesenen Klasse hinzufügen](#add-to-class) oder eine [Feldergruppe](#add-to-field-group) auswählen. Wenn Ihr Schema jedoch eine Standardklasse verwendet, können Sie das benutzerdefinierte Feld nur einer Feldergruppe zuweisen.

#### Zuweisen des Felds zu einer benutzerdefinierten Feldergruppe {#add-to-field-group}

>[!NOTE]
>
>In diesem Abschnitt wird nur beschrieben, wie Sie das Feld einer benutzerdefinierten Feldergruppe zuweisen. Wenn Sie stattdessen eine Standardfeldgruppe um das neue benutzerdefinierte Feld erweitern möchten, finden Sie weitere Informationen im Abschnitt zum [Hinzufügen benutzerdefinierter Felder zu Standardfeldgruppen](#custom-fields-for-standard-groups).

Wählen Sie unter **[!UICONTROL Assign to]** die Option **[!UICONTROL Field Group]**. Wenn Ihr Schema eine Standardklasse verwendet, ist dies die einzige verfügbare Option und ist standardmäßig ausgewählt.

Als Nächstes müssen Sie eine Feldergruppe auswählen, mit der das neue Feld verknüpft werden soll. Beginnen Sie, den Namen der Feldergruppe in die bereitgestellte Texteingabe einzugeben. Wenn Sie über benutzerdefinierte Feldergruppen verfügen, die mit der Eingabe übereinstimmen, werden diese in der Dropdown-Liste angezeigt. Alternativ können Sie einen eindeutigen Namen eingeben, um stattdessen eine neue Feldergruppe zu erstellen.

![Feldergruppe auswählen](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>Wenn Sie eine vorhandene benutzerdefinierte Feldergruppe auswählen, erben alle anderen Schemata, die diese Feldergruppe verwenden, das neu hinzugefügte Feld ebenfalls, nachdem Sie Ihre Änderungen gespeichert haben. Wählen Sie daher nur dann eine vorhandene Feldergruppe aus, wenn Sie diese Art der Verbreitung wünschen. Andernfalls sollten Sie stattdessen eine neue benutzerdefinierte Feldergruppe erstellen.

Wählen Sie nach Auswahl der Feldergruppe aus der Liste die Option **[!UICONTROL Apply]** aus.

![Feld anwenden](../../images/ui/resources/schemas/apply-field.png)

Das neue Feld wird der Arbeitsfläche hinzugefügt und erhält einen Namespace unter Ihrer [Mandanten-ID](../../api/getting-started.md#know-your-tenant_id), um Konflikte mit standardmäßigen XDM-Feldern zu vermeiden. Die Feldergruppe, mit der Sie das neue Feld verknüpft haben, wird auch unter **[!UICONTROL Field groups]** in der linken Leiste angezeigt.

![Mandanten-ID](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>Die übrigen Felder, die von der ausgewählten benutzerdefinierten Feldergruppe bereitgestellt werden, werden standardmäßig aus dem Schema entfernt. Wenn Sie einige dieser Felder zum Schema hinzufügen möchten, wählen Sie ein Feld aus der Gruppe aus und klicken Sie dann in der rechten Leiste auf **[!UICONTROL Manage related fields]** .

#### Zuweisen des Felds zu einer benutzerdefinierten Klasse {#add-to-class}

Wählen Sie unter **[!UICONTROL Assign to]** die Option **[!UICONTROL Class]**. Das Eingabefeld unten wird durch den Namen der benutzerdefinierten Klasse des aktuellen Schemas ersetzt, was angibt, dass das neue Feld dieser Klasse zugewiesen wird.

![Die [!UICONTROL Class] Option, die für die neue Feldzuweisung ausgewählt wird.](../../images/ui/resources/schemas/assign-field-to-class.png)

Fahren Sie mit der Konfiguration des Felds wie gewünscht fort und wählen Sie **[!UICONTROL Apply]** aus, wenn Sie fertig sind.

![[!UICONTROL Apply] wird für das neue Feld ausgewählt.](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

Das neue Feld wird der Arbeitsfläche hinzugefügt und erhält einen Namespace unter Ihrer [Mandanten-ID](../../api/getting-started.md#know-your-tenant_id), um Konflikte mit standardmäßigen XDM-Feldern zu vermeiden. Wenn Sie den Klassennamen in der linken Leiste auswählen, wird das neue Feld als Teil der Klassenstruktur angezeigt.

![Das neue Feld, das auf die Struktur der benutzerdefinierten Klasse angewendet wird, dargestellt auf der Arbeitsfläche.](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### Hinzufügen benutzerdefinierter Felder zur Struktur von Standardfeldgruppen {#custom-fields-for-standard-groups}

Wenn das Schema, an dem Sie arbeiten, ein Feld vom Typ „Objekt“ hat, das von einer Standardfeldgruppe bereitgestellt wird, können Sie diesem Standardobjekt Ihre eigenen benutzerdefinierten Felder hinzufügen.

>[!WARNING]
>
>Alle Felder, die einer Feldergruppe in einem Schema hinzugefügt wurden, werden auch in allen anderen Schemata angezeigt, die dieselbe Feldergruppe verwenden. Wenn ein benutzerdefiniertes Feld zu einer Standardfeldgruppe hinzugefügt wird, wird diese Feldgruppe außerdem in eine benutzerdefinierte Feldgruppe konvertiert, und die ursprüngliche Standardfeldgruppe ist nicht mehr verfügbar.
>
>Wenn Sie an der Beta-Version für diese Funktion teilgenommen haben, erhalten Sie ein Dialogfeld, in dem Sie über die Standardfeldgruppen informiert werden, die Sie zuvor angepasst haben. Wenn Sie **[!UICONTROL Acknowledge]** auswählen, werden die aufgelisteten Ressourcen in benutzerdefinierte Feldergruppen konvertiert.
>
>![Bestätigungsdialogfeld zum Konvertieren von Standardfeldgruppen](../../images/ui/resources/schemas/beta-extension-confirmation.png)

Wählen Sie zunächst das Pluszeichen (**+**) neben dem Stamm des -Objekts aus, das von der Standardfeldgruppe bereitgestellt wird.

![Feld zum Standardobjekt hinzufügen](../../images/ui/resources/schemas/add-field-to-standard-object.png)

Es wird eine Warnmeldung angezeigt, in der Sie aufgefordert werden zu bestätigen, ob Sie die Standardfeldgruppe konvertieren möchten. Wählen Sie **[!UICONTROL Continue creating field group]** aus, um fortzufahren.

![Konvertierung der Feldergruppe bestätigen](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

Die Arbeitsfläche wird erneut mit einem unbenannten Platzhalter für das neue Feld angezeigt. Beachten Sie, dass an den Namen der Standardfeldgruppe „([!UICONTROL Extended])“ angehängt wurde, um anzugeben, dass sie von der Originalversion geändert wurde. Verwenden Sie von hier aus die Steuerelemente in der rechten Leiste, um die Eigenschaften des Felds zu definieren.

![Feld zum Standardobjekt hinzugefügt](../../images/ui/resources/schemas/standard-field-group-converted.png)

Nachdem Sie Ihre Änderungen angewendet haben, wird das neue Feld unter dem Namespace Ihrer Mandanten-ID im Standardobjekt angezeigt. Dieser verschachtelte Namespace verhindert Konflikte mit Feldnamen innerhalb der Feldergruppe selbst, um Unterbrechungen von Änderungen in anderen Schemas zu vermeiden, die dieselbe Feldergruppe verwenden.

![Feld zum Standardobjekt hinzugefügt](../../images/ui/resources/schemas/added-to-standard-object.png)

## Aktivieren eines Schemas für das Echtzeit-Kundenprofil {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="Aktivieren eines Schemas für das Echtzeit-Kundenprofil"
>abstract="Wenn ein Schema für das Echtzeit-Kundenprofil aktiviert ist, werden alle Datensätze, die aus diesem Schema erstellt werden, für das Echtzeit-Kundenprofil verwendet. Dieses führt Daten aus unterschiedlichen Quellen zusammen und erstellt eine vollständige Ansicht jedes Kunden. Nachdem ein Schema verwendet wurde, um Daten in das Echtzeit-Kundenprofil aufzunehmen, kann es nicht mehr deaktiviert werden. Weitere Informationen finden Sie in der Dokumentation."

[Echtzeit-Kundenprofil](../../../profile/home.md) führt Daten aus unterschiedlichen Quellen zusammen, um eine vollständige Ansicht jedes einzelnen Kunden zu erstellen. Wenn Sie möchten, dass die von einem Schema erfassten Daten in diesen Prozess einbezogen werden, müssen Sie das Schema für die Verwendung in [!DNL Profile] aktivieren.

>[!IMPORTANT]
>
>Um ein Schema für die [!DNL Profile] zu aktivieren, muss ein primäres Identitätsfeld definiert sein. Weitere Informationen finden Sie im Handbuch [Definieren &#x200B;](../fields/identity.md) Identitätsfeldern“.

Um das Schema zu aktivieren, wählen Sie zunächst den Namen des Schemas in der linken Leiste und dann den Umschalter **[!UICONTROL Profile]** in der rechten Leiste aus.

![](../../images/ui/resources/schemas/profile-toggle.png)

Es wird ein Pop-up mit einer Warnung angezeigt, dass ein Schema nach dem Aktivieren und Speichern nicht mehr deaktiviert werden kann. Wählen Sie **[!UICONTROL Enable]** aus, um fortzufahren.

![](../../images/ui/resources/schemas/profile-confirm.png)

Die Arbeitsfläche wird erneut angezeigt, wobei der Umschalter [!UICONTROL Profile] aktiviert ist.

>[!IMPORTANT]
>
>Da das Schema noch nicht gespeichert wurde, ist dies der Punkt, an dem es nicht mehr zurückgegeben wird, wenn Sie es sich anders überlegen, das Schema dem Echtzeit-Kundenprofil zuzulassen: Nachdem Sie ein aktiviertes Schema gespeichert haben, kann es nicht mehr deaktiviert werden. Wählen Sie erneut den Umschalter **[!UICONTROL Profile]** aus, um das Schema zu deaktivieren.

Um den Vorgang abzuschließen, wählen Sie **[!UICONTROL Save]** aus, um das Schema zu speichern.

![](../../images/ui/resources/schemas/profile-enabled.png)

Das Schema ist jetzt für die Verwendung im Echtzeit-Kundenprofil aktiviert. Wenn Experience Platform Daten basierend auf diesem Schema in Datensätze aufnimmt, werden diese Daten in Ihre zusammengefassten Profildaten integriert.

## Anzeigenamen für Schemafelder bearbeiten {#display-names}

Nachdem Sie eine Klasse zugewiesen und einem Schema Feldergruppen hinzugefügt haben, können Sie die Anzeigenamen der Felder des Schemas bearbeiten, unabhängig davon, ob diese Felder von standardmäßigen oder benutzerdefinierten XDM-Ressourcen bereitgestellt wurden.

>[!NOTE]
>
>Beachten Sie, dass die Anzeigenamen von Feldern, die zu Standardklassen oder Feldergruppen gehören, nur im Kontext eines bestimmten Schemas bearbeitet werden können. Mit anderen Worten: Die Änderung des Anzeigenamens eines Standardfelds in einem Schema wirkt sich nicht auf andere Schemata aus, die dieselbe verknüpfte Klasse oder Feldergruppe verwenden.
>
>Sobald Sie Änderungen an den Anzeigenamen für die Felder eines Schemas vornehmen, werden diese Änderungen sofort in allen vorhandenen Datensätzen widergespiegelt, die auf diesem Schema basieren.

Ändern Sie die Feldnamen in die Anzeigenamen, indem Sie die **[!UICONTROL Show display names for fields]** umschalten. Um den Anzeigenamen eines Schemafelds zu bearbeiten, wählen Sie das Feld auf der Arbeitsfläche aus. Geben Sie in der rechten Leiste den neuen Namen unter **[!UICONTROL Display name]** an.

![](../../images/ui/resources/schemas/display-name.png)

Wählen Sie **[!UICONTROL Apply]** in der rechten Leiste aus. Die Arbeitsfläche wird aktualisiert, um den neuen Anzeigenamen des Felds anzuzeigen. Wählen Sie **[!UICONTROL Save]** aus, um die Änderungen auf das Schema anzuwenden.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Ändern der Klasse eines Schemas {#change-class}

Sie können die Klasse eines Schemas während des anfänglichen Kompositionsprozesses jederzeit ändern, bevor das Schema gespeichert wurde.

>[!WARNING]
>
>Die Neuzuweisung der Klasse für ein Schema sollte mit äußerster Vorsicht erfolgen. Feldergruppen sind nur mit bestimmten Klassen kompatibel. Daher werden die Arbeitsfläche und alle von Ihnen hinzugefügten Felder beim Ändern der Klasse zurückgesetzt.

Um eine Klasse neu zuzuweisen, wählen Sie **[!UICONTROL Assign]** auf der linken Seite der Arbeitsfläche aus.

![](../../images/ui/resources/schemas/assign-class-button.png)

Es wird ein Dialogfeld mit einer Liste aller verfügbaren Klassen angezeigt, einschließlich der von Ihrem Unternehmen definierten Klassen (der Eigentümer ist &quot;[!UICONTROL Customer]„) sowie der von Adobe definierten Standardklassen.

Wählen Sie eine Klasse aus der Liste aus, um ihre Beschreibung auf der rechten Seite des Dialogfelds anzuzeigen. Sie können auch **[!UICONTROL Preview class structure]** auswählen, um die mit der Klasse verknüpften Felder und Metadaten anzuzeigen. Wählen Sie **[!UICONTROL Assign class]** aus, um fortzufahren.

![](../../images/ui/resources/schemas/assign-class.png)

Ein neues Dialogfeld wird geöffnet, in dem Sie bestätigen müssen, dass Sie eine neue Klasse zuweisen möchten. Wählen Sie zur Bestätigung **[!UICONTROL Assign]** aus.

![](../../images/ui/resources/schemas/assign-confirm.png)

Nach Bestätigung der Klassenänderung wird die Arbeitsfläche zurückgesetzt und der gesamte Kompositionsfortschritt geht verloren.

## Nächste Schritte {#next-steps}

In diesem Dokument wurden die Grundlagen zum Erstellen und Bearbeiten von Schemata in der Experience Platform-Benutzeroberfläche behandelt. Es wird dringend empfohlen, das [Tutorial zur Schemaerstellung](../../tutorials/create-schema-ui.md) durchzugehen, um einen umfassenden Workflow zum Erstellen eines vollständigen Schemas in der Benutzeroberfläche zu erhalten, einschließlich der Erstellung benutzerdefinierter Feldergruppen und Datentypen für individuelle Anwendungsfälle.

Weiterführende Informationen zu den Funktionen von [!UICONTROL Schemas] Workspace finden Sie in der Übersicht zu [[!UICONTROL Schemas] Workspace &#x200B;](../overview.md).

Informationen zum Verwalten von Schemas in der [!DNL Schema Registry]-API finden Sie im [Handbuch zu Schemas-Endpunkten](../../api/schemas.md).
