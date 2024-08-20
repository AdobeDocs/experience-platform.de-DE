---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Schema; Schemas;
solution: Experience Platform
title: Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche
description: Erfahren Sie mehr über die Grundlagen zum Erstellen und Bearbeiten von Schemas in der Experience Platform-Benutzeroberfläche.
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '3861'
ht-degree: 3%

---

# Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche {#create-edit-schemas-in-ui}

Dieses Handbuch bietet einen Überblick darüber, wie Sie Experience-Datenmodell (XDM)-Schemas für Ihr Unternehmen in der Adobe Experience Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

>[!IMPORTANT]
>
>XDM-Schemata sind extrem anpassbar, sodass die Schritte zum Erstellen eines Schemas variieren können, je nachdem, welche Art von Daten das Schema erfassen soll. Daher behandelt dieses Dokument nur die grundlegenden Interaktionen, die Sie mit Schemas in der Benutzeroberfläche durchführen können, und schließt verwandte Schritte wie das Anpassen von Klassen, Schemafeldergruppen, Datentypen und Feldern aus.
>
>Um einen umfassenden Überblick über den Erstellungsprozess von Schemas zu erhalten, folgen Sie dem Tutorial zur Erstellung von [Schemas](../../tutorials/create-schema-ui.md) , um ein vollständiges Beispielschema zu erstellen und sich mit den zahlreichen Funktionen von [!DNL Schema Editor] vertraut zu machen.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schemakomposition](../../schema/composition.md) , um einen Überblick darüber zu erhalten, wie Schemas erstellt werden.

## Erstellen eines neuen Schemas {#create}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie ein neues Schema in der Benutzeroberfläche manuell erstellen. Wenn Sie CSV-Daten in Platform erfassen, können Sie mithilfe von ML-Algorithmen (Machine Learning) ein Schema aus CSV-Beispieldaten generieren **.** Dieser Workflow entspricht Ihrem Datenformat und erstellt automatisch ein neues Schema, das auf der Struktur und dem Inhalt Ihrer CSV-Datei basiert. Weitere Informationen zu diesem Workflow finden Sie im Handbuch zur Erstellung von [ML-unterstützten Schemas](../ml-assisted-schema-creation.md) .

Wählen Sie im Arbeitsbereich [!UICONTROL Schemas] oben rechts die Option **[!UICONTROL Schema erstellen]** aus.

![Der Arbeitsbereich &quot;Schemas&quot;mit dem Eintrag [!UICONTROL Schema erstellen] ist hervorgehoben.](../../images/ui/resources/schemas/create-schema.png)

Das Dialogfeld [!UICONTROL Schema erstellen] wird angezeigt. In diesem Dialogfeld können Sie entweder manuell ein Schema durch Hinzufügen von Feldern und Feldergruppen erstellen oder eine CSV-Datei hochladen und mithilfe von ML-Algorithmen ein Schema generieren. Wählen Sie im Dialogfeld einen Workflow zur Schemaerstellung aus.

![Das Dialogfeld Schema erstellen mit den Workflow-Optionen und markieren hervorgehoben.](../../images/tutorials/create-schema/create-a-schema-dialog.png)

### Manuelle oder ML-gestützte Schemaerstellung {#manual-or-assisted}

Informationen dazu, wie Sie einen ML-Algorithmus verwenden können, um eine Schemastruktur basierend auf einer CSV-Datei zu empfehlen, finden Sie im Leitfaden zur Erstellung von Schemas mit maschinellem Lernen](../ml-assisted-schema-creation.md). [ Dieses UI-Handbuch konzentriert sich auf den Workflow für die manuelle Erstellung.

### Manuelle Schemaerstellung {#manual-creation}

Der Workflow [!UICONTROL Schema erstellen] wird angezeigt. Sie können eine Basisklasse für das Schema auswählen, indem Sie entweder **[!UICONTROL Individuelles Profil]**, **[!UICONTROL Erlebnisereignis]** oder **[!UICONTROL Sonstige]** und anschließend **[!UICONTROL Weiter]** auswählen, um Ihre Auswahl zu bestätigen. Weitere Informationen zu diesen Klassen finden Sie in der Dokumentation zu [[!UICONTROL XDM-individuellen Profilen]](../../classes/individual-profile.md) und [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md) .

![Der Workflow [!UICONTROL Schema erstellen] mit den drei Klassenoptionen und [!UICONTROL Weiter] hervorgehoben.](../../images/ui/resources/schemas/schema-class-options.png)

Nachdem Sie eine Klasse ausgewählt haben, wird der Abschnitt [!UICONTROL Name und Überprüfung] angezeigt. In diesem Abschnitt geben Sie einen Namen und eine Beschreibung ein, um Ihr Schema zu identifizieren. &#x200B;Die (von der Klasse bereitgestellte) Basisstruktur des Schemas wird auf der Arbeitsfläche angezeigt, damit Sie Ihre ausgewählte Klasse und Schemastruktur überprüfen und überprüfen können.

Geben Sie einen benutzerfreundlichen [!UICONTROL Anzeigenamen des Schemas] in das Textfeld ein. Geben Sie anschließend eine Beschreibung ein, die die Identifizierung Ihres Schemas erleichtert. Wenn Sie Ihre Schemastruktur überprüft haben und mit Ihren Einstellungen zufrieden sind, wählen Sie **[!UICONTROL Beenden]** aus, um Ihr Schema zu erstellen.

![Der Abschnitt [!UICONTROL Name und Überprüfung] des Workflows [!UICONTROL Schema erstellen] , in dem der [!UICONTROL Anzeigename des Schemas], die [!UICONTROL Beschreibung] und der Abschnitt [!UICONTROL Beenden] hervorgehoben sind.](../../images/ui/resources/schemas/name-and-review.png)

Die Registerkarte [!UICONTROL Schema] [!UICONTROL Durchsuchen] wird angezeigt. Ihr kürzlich erstelltes Schema ist jetzt in der Schema Library aufgeführt und kann im [!DNL Schema Editor] bearbeitet werden.

![Die Registerkarte &quot;Durchsuchen des Arbeitsbereichs &quot;Schemas&quot;mit dem kürzlich erstellten Schema.](../../images/ui/resources/schemas/example-schema.png)

## Vorhandenes Schema bearbeiten {#edit}

>[!NOTE]
>
>Sobald ein Schema gespeichert und in der Datenerfassung verwendet wurde, können nur noch additive Änderungen daran vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) .

Um ein vorhandenes Schema zu bearbeiten, wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** aus und wählen Sie dann den Namen des Schemas aus, das Sie bearbeiten möchten. Sie können auch die Suchleiste verwenden, um die Liste der verfügbaren Optionen einzuschränken.

![Der Arbeitsbereich &quot;Schema&quot;mit einem hervorgehobenen Schema.](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Sie können die Such- und Filterfunktionen des Arbeitsbereichs verwenden, um das Schema leichter zu finden. Weitere Informationen finden Sie im Handbuch zum [Erkunden von XDM-Ressourcen](../explore.md) .

Nachdem Sie ein Schema ausgewählt haben, wird der [!DNL Schema Editor] mit der Struktur des Schemas auf der Arbeitsfläche angezeigt. Sie können jetzt [Feldergruppen](#add-field-groups) zum Schema hinzufügen (oder [einzelne Felder](#add-individual-fields) aus diesen Gruppen hinzufügen), [Anzeigenamen von Feldern bearbeiten](#display-names) oder [vorhandene benutzerdefinierte Feldergruppen bearbeiten](./field-groups.md#edit) , wenn das Schema beliebige verwendet.

## Mehr Aktionen {#more}

Im Schema Editor können Sie auch Schnellaktionen durchführen, um die JSON-Struktur des Schemas zu kopieren oder das Schema zu löschen, wenn es nicht für das Echtzeit-Kundenprofil aktiviert wurde oder über verknüpfte Datensätze verfügt. Wählen Sie oben in der Ansicht [!UICONTROL Mehr] aus, um eine Dropdown-Liste mit Schnellaktionen anzuzeigen.

Mit der Funktion JSON-Struktur kopieren können Sie sehen, wie eine Beispiel-Payload aussehen würde, während Sie das Schema und Ihre Daten-Pipelines noch erstellen. Dies ist besonders hilfreich in Situationen, in denen komplexe Objektzuordnungsstrukturen im Schema vorhanden sind, z. B. bei einer Identitätszuordnung.

![Der Schema-Editor mit der hervorgehobenen Schaltfläche Mehr und den angezeigten Dropdown-Optionen.](../../images/tutorials/create-schema/more-actions.png)

## Umschalter für Anzeigename {#display-name-toggle}

Der Schema Editor bietet einen Umschalter zum Ändern zwischen den ursprünglichen Feldnamen und den für Menschen lesbareren Anzeigenamen. Diese Flexibilität ermöglicht eine verbesserte Erkennung und Bearbeitung von Feldern Ihrer Schemata. Der Umschalter befindet sich oben rechts in der Ansicht Schema Editor .

>[!NOTE]
>
>Die Änderung von Feldnamen zu Anzeigenamen ist rein kosmetischer Natur und ändert keine nachgelagerten Ressourcen.

![Der Schema-Editor mit [!UICONTROL Anzeigenamen für Felder anzeigen] hervorgehoben.](../../images/ui/resources/schemas/display-name-toggle.png)

Die Anzeigenamen für Standardfeldgruppen werden vom System generiert, können jedoch angepasst werden, wie im Abschnitt [Anzeigenamen](#display-names) beschrieben. Anzeigenamen werden in mehreren Ansichten der Benutzeroberfläche angezeigt, einschließlich der Zuordnung und Datensatzvorschau. Die Standardeinstellung ist deaktiviert und zeigt die Feldnamen anhand ihrer ursprünglichen Werte an.

## Hinzufügen von Feldergruppen zu einem Schema {#add-field-groups}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie einem Schema vorhandene Feldergruppen hinzufügen. Wenn Sie eine neue benutzerdefinierte Feldergruppe erstellen möchten, lesen Sie stattdessen das Handbuch zum Erstellen und Bearbeiten von Feldergruppen](./field-groups.md#create) .[

Nachdem Sie ein Schema innerhalb von [!DNL Schema Editor] geöffnet haben, können Sie dem Schema mithilfe von Feldergruppen Felder hinzufügen. Wählen Sie zunächst in der linken Leiste **[!UICONTROL Hinzufügen]** neben **[!UICONTROL Feldergruppen]** aus.

![Der Schema-Editor mit dem Abschnitt [!UICONTROL Hinzufügen] aus dem Abschnitt [!UICONTROL Feldergruppen] wurde hervorgehoben.](../../images/ui/resources/schemas/add-field-group-button.png)

Es wird ein Dialogfeld mit einer Liste von Feldergruppen angezeigt, die Sie für das Schema auswählen können. Da Feldergruppen nur mit einer Klasse kompatibel sind, werden nur die Feldergruppen aufgelistet, die mit der ausgewählten Klasse des Schemas verknüpft sind. Standardmäßig werden die aufgelisteten Feldergruppen nach ihrer Nutzungspersönlichkeit in Ihrem Unternehmen sortiert.

![Das Dialogfeld [!UICONTROL Feldergruppen hinzufügen] wurde hervorgehoben und die Spalte [!UICONTROL Beliebtheit] wurde hervorgehoben.](../../images/ui/resources/schemas/field-group-popularity.png)

Wenn Sie die allgemeine Aktivität oder den Geschäftsbereich der Felder kennen, die Sie hinzufügen möchten, wählen Sie in der linken Leiste mindestens eine der vertikalen Branchen-Kategorien aus, um die angezeigte Liste der Feldergruppen zu filtern.

![Das Dialogfeld [!UICONTROL Feldergruppen hinzufügen] wurde mit den Filtern [!UICONTROL Branche] hervorgehoben und die Spalte [!UICONTROL Branche] hervorgehoben.](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Weitere Informationen zu Best Practices für branchenspezifische Datenmodellierung in XDM finden Sie in der Dokumentation zu [Datenmodellen der Branche](../../schema/industries/overview.md).

Sie können auch die Suchleiste verwenden, um Ihre gewünschte Feldergruppe zu finden. Feldergruppen, deren Name mit der Abfrage übereinstimmt, werden oben in der Liste angezeigt. Unter **[!UICONTROL Standardfelder]** werden Feldergruppen angezeigt, die Felder enthalten, die die gewünschten Datenattribute beschreiben.

![Das Dialogfeld [!UICONTROL Feldergruppen hinzufügen] mit der hervorgehobenen Suchfunktion [!UICONTROL Standardfelder].](../../images/ui/resources/schemas/field-group-search.png)

Aktivieren Sie das Kontrollkästchen neben dem Namen der Feldergruppe, die Sie zum Schema hinzufügen möchten. Sie können mehrere Feldergruppen aus der Liste auswählen, wobei jede ausgewählte Feldergruppe in der rechten Leiste angezeigt wird.

![Das Dialogfeld [!UICONTROL Feldergruppen hinzufügen] mit hervorgehobener Funktion zur Kontrollkästchen-Auswahl.](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Für jede aufgelistete Feldergruppe können Sie den Mauszeiger über das Informationssymbol (![Infosymbol](/help/images/icons/info.png)) bewegen oder sich auf dieses konzentrieren, um eine kurze Beschreibung der Art der Daten anzuzeigen, die von der Feldergruppe erfasst werden. Sie können auch das Vorschausymbol (![Vorschausymbol](/help/images/icons/preview.png)) auswählen, um die Struktur der Felder anzuzeigen, die die Feldergruppe bereitstellt, bevor Sie sie zum Schema hinzufügen.

Nachdem Sie Ihre Feldergruppen ausgewählt haben, wählen Sie **[!UICONTROL Feldergruppen hinzufügen]** aus, um sie dem Schema hinzuzufügen.

![Das Dialogfeld [!UICONTROL Feldergruppen hinzufügen] mit ausgewählten Feldergruppen und [!UICONTROL Feldergruppen hinzufügen] hervorgehoben.](../../images/ui/resources/schemas/add-field-group-finish.png)

Die [!DNL Schema Editor] wird mit den von der Feldergruppe bereitgestellten Feldern wieder angezeigt, die auf der Arbeitsfläche dargestellt werden.

![Der [!DNL Schema Editor] mit einem Beispielschema, das angezeigt wird.](../../images/ui/resources/schemas/field-groups-added.png)

>[!NOTE]
>
>Im Schema Editor werden Standardklassen (Adobe-generierte) und Feldgruppen mit dem Vorhängeschloss-Symbol (![Vorhängeschlosssymbol) angezeigt.](/help/images/icons/lock-closed.png). Das Vorhängeschloss wird in der linken Leiste neben dem Namen der Klasse oder Feldergruppe sowie neben jedem Feld im Schemadiagramm angezeigt, das Teil einer systemgenerierten Ressource ist.
>
>![Der Schema-Editor mit dem Vorhängeschloss-Symbol hervorgehoben](../../images/ui/explore/schema-editor-padlock-icon.png)

Nachdem Sie eine Feldergruppe zu einem Schema hinzugefügt haben, können Sie optional [vorhandene Felder entfernen](#remove-fields) oder [neue benutzerdefinierte Felder hinzufügen](#add-fields), um diese Gruppen hinzuzufügen, je nach Ihren Anforderungen.

### Felder, die zu Feldergruppen hinzugefügt wurden, entfernen {#remove-fields}

Nachdem Sie einem Schema eine Feldergruppe hinzugefügt haben, können Sie alle Felder entfernen, die Sie nicht benötigen.

>[!NOTE]
>
>Das Entfernen von Feldern aus einer Feldergruppe wirkt sich nur auf das bearbeitete Schema aus und hat keine Auswirkungen auf die Feldergruppe selbst. Wenn Sie Felder in einem Schema entfernen, sind diese Felder weiterhin in allen anderen Schemas verfügbar, die dieselbe Feldergruppe verwenden.

Im folgenden Beispiel wurde dem Schema die Standardfeldgruppe **[!UICONTROL Demografische Details]** hinzugefügt. Um ein einzelnes Feld wie `taxId` zu entfernen, wählen Sie das Feld auf der Arbeitsfläche aus und klicken Sie dann in der rechten Leiste auf **[!UICONTROL Entfernen]** .

![Die [!DNL Schema Editor] mit [!UICONTROL Remove] hervorgehoben. Dadurch wird ein einzelnes Feld entfernt.](../../images/ui/resources/schemas/remove-single-field.png)

Wenn Sie mehrere Felder entfernen möchten, können Sie die Feldergruppe als Ganzes verwalten. Wählen Sie auf der Arbeitsfläche ein Feld aus, das zur Gruppe gehört, und wählen Sie dann in der rechten Leiste **[!UICONTROL Zugehörige Felder verwalten]** aus.

![Die [!DNL Schema Editor] mit [!UICONTROL zugeordneten Feldern verwalten] hervorgehoben.](../../images/ui/resources/schemas/manage-related-fields.png)

Es wird ein Dialogfeld mit der Struktur der betreffenden Feldergruppe angezeigt. Hier können Sie die Kontrollkästchen verwenden, um die erforderlichen Felder auszuwählen oder die Auswahl aufzuheben. Wenn Sie zufrieden sind, wählen Sie **[!UICONTROL Bestätigen]** aus.

![Das Dialogfeld [!UICONTROL Zugehörige Felder verwalten] mit ausgewählten Feldern und [!UICONTROL Bestätigen] hervorgehoben.](../../images/ui/resources/schemas/select-fields.png)

Die Arbeitsfläche wird nur mit den in der Schemastruktur ausgewählten Feldern wieder angezeigt.

![Felder hinzugefügt](../../images/ui/resources/schemas/fields-added.png)

### Hinzufügen benutzerdefinierter Felder zu Feldergruppen {#add-fields}

Nachdem Sie einem Schema eine Feldergruppe hinzugefügt haben, können Sie zusätzliche Felder für diese Gruppe definieren. Alle Felder, die einer Feldergruppe in einem Schema hinzugefügt werden, werden jedoch auch in allen anderen Schemas angezeigt, die dieselbe Feldergruppe verwenden.

Wenn ein benutzerdefiniertes Feld zu einer Standardfeldgruppe hinzugefügt wird, wird diese Feldergruppe in eine benutzerdefinierte Feldergruppe konvertiert und die ursprüngliche Standardfeldgruppe ist nicht mehr verfügbar.

Wenn Sie ein benutzerdefiniertes Feld zu einer Standardfeldgruppe hinzufügen möchten, finden Sie bestimmte Anweisungen im Abschnitt [unter ](#custom-fields-for-standard-groups). Wenn Sie Felder zu einer benutzerdefinierten Feldergruppe hinzufügen, lesen Sie den Abschnitt über das Bearbeiten benutzerdefinierter Feldergruppen](./field-groups.md) im Handbuch zur Feldergruppen-Benutzeroberfläche.[

Wenn Sie keine vorhandenen Feldergruppen ändern möchten, können Sie [eine neue benutzerdefinierte Feldergruppe ](./field-groups.md#create) erstellen, um stattdessen zusätzliche Felder zu definieren.

## Hinzufügen einzelner Felder zu einem Schema {#add-individual-fields}

Mit dem Schema Editor können Sie einzelne Felder direkt zu einem Schema hinzufügen, wenn Sie vermeiden möchten, eine ganze Feldergruppe für einen bestimmten Anwendungsfall hinzuzufügen. Sie können stattdessen [einzelne Felder aus Standardfeldgruppen hinzufügen](#add-standard-fields) oder [eigene benutzerdefinierte Felder hinzufügen](#add-custom-fields).

>[!IMPORTANT]
>
>Auch wenn Sie im Schema Editor mit Funktionen einzelne Felder direkt zu einem Schema hinzufügen können, ändert dies nichts daran, dass alle Felder in einem XDM-Schema von seiner Klasse oder einer Feldergruppe bereitgestellt werden müssen, die mit dieser Klasse kompatibel ist. Wie in den folgenden Abschnitten erläutert, sind alle einzelnen Felder weiterhin einer Klasse oder Feldergruppe als wichtigen Schritt zugeordnet, wenn sie einem Schema hinzugefügt werden.

### Standardfelder hinzufügen {#add-standard-fields}

Sie können Felder aus Standardfeldgruppen direkt zu einem Schema hinzufügen, ohne zuvor die entsprechende Feldergruppe kennen zu müssen. Um einem Schema ein Standardfeld hinzuzufügen, wählen Sie auf der Arbeitsfläche das Pluszeichen (**+**) neben dem Namen des Schemas aus. Ein Platzhalter **[!UICONTROL Unbenanntes Feld]** wird in der Schemastruktur angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Feld-Platzhalter](../../images/ui/resources/schemas/root-custom-field.png)

Geben Sie unter **[!UICONTROL Feldname]** den Namen des Felds ein, das Sie hinzufügen möchten. Das System sucht automatisch nach Standardfeldern, die mit der Abfrage übereinstimmen, und listet sie unter **[!UICONTROL Empfohlene Standardfelder]** auf, einschließlich der Feldergruppen, zu denen sie gehören.

![Empfohlene Standardfelder](../../images/ui/resources/schemas/standard-field-search.png)

Einige Standardfelder weisen denselben Namen auf, ihre Struktur kann jedoch von der Feldergruppe abhängen, aus der sie stammen. Wenn ein Standardfeld innerhalb eines übergeordneten Objekts in der Feldergruppenstruktur verschachtelt ist, wird das übergeordnete Feld auch im Schema enthalten sein, wenn das untergeordnete Feld hinzugefügt wird.

Wählen Sie das Vorschausymbol (![Vorschau-Symbol](/help/images/icons/preview.png)) neben einem Standardfeld aus, um die Struktur seiner Feldergruppe anzuzeigen und besser zu verstehen, wie sie möglicherweise verschachtelt ist. Um das Standardfeld zum Schema hinzuzufügen, wählen Sie das Pluszeichen (![Plussymbol](/help/images/icons/add-circle.png)) aus.

![Standardfeld hinzufügen](../../images/ui/resources/schemas/add-standard-field.png)

Die Arbeitsfläche wird aktualisiert und zeigt das Standardfeld an, das dem Schema hinzugefügt wurde, einschließlich der übergeordneten Felder, unter denen es innerhalb der Feldergruppenstruktur verschachtelt ist. Der Name der Feldergruppe wird auch in der linken Leiste unter **[!UICONTROL Feldergruppen]** aufgeführt. Wenn Sie weitere Felder aus derselben Feldergruppe hinzufügen möchten, wählen Sie in der rechten Leiste **[!UICONTROL Zugehörige Felder verwalten]** aus.

![Standardfeld hinzugefügt](../../images/ui/resources/schemas/standard-field-added.png)

### Benutzerdefinierte Felder hinzufügen        {#add-custom-fields}

Ähnlich wie beim Workflow für Standardfelder können Sie auch eigene benutzerdefinierte Felder direkt zu einem Schema hinzufügen.

Um Felder zur Stammebene eines Schemas hinzuzufügen, wählen Sie auf der Arbeitsfläche das Pluszeichen (**+**) neben dem Namen des Schemas aus. Ein Platzhalter **[!UICONTROL Unbenanntes Feld]** wird in der Schemastruktur angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Benutzerdefiniertes Stammfeld](../../images/ui/resources/schemas/root-custom-field.png)

Beginnen Sie mit der Eingabe des Namens des Felds, das Sie hinzufügen möchten, und das System beginnt automatisch mit der Suche nach entsprechenden Standardfeldern. Um stattdessen ein neues benutzerdefiniertes Feld zu erstellen, wählen Sie die obere Option aus, die an **([!UICONTROL Neues Feld])** angehängt ist.

![Neues Feld](../../images/ui/resources/schemas/custom-field-search.png)

Nachdem Sie einen Anzeigenamen und einen Datentyp für das Feld bereitgestellt haben, besteht der nächste Schritt darin, das Feld einer übergeordneten XDM-Ressource zuzuweisen. Wenn Ihr Schema eine benutzerdefinierte Klasse verwendet, können Sie stattdessen das Feld [zur zugewiesenen Klasse](#add-to-class) oder einer [Feldergruppe](#add-to-field-group) hinzufügen. Wenn Ihr Schema jedoch eine Standardklasse verwendet, können Sie das benutzerdefinierte Feld nur einer Feldergruppe zuweisen.

#### Weisen Sie das Feld einer benutzerdefinierten Feldergruppe zu {#add-to-field-group}

>[!NOTE]
>
>In diesem Abschnitt wird nur beschrieben, wie Sie das Feld einer benutzerdefinierten Feldergruppe zuweisen. Wenn Sie stattdessen eine Standardfeldgruppe mit dem neuen benutzerdefinierten Feld erweitern möchten, finden Sie weitere Informationen im Abschnitt [Hinzufügen benutzerdefinierter Felder zu Standardfeldgruppen](#custom-fields-for-standard-groups).

Wählen Sie unter &quot;**[!UICONTROL Zuweisen zu]**&quot;die Option &quot;**[!UICONTROL Feldergruppe]**&quot;. Wenn Ihr Schema eine Standardklasse verwendet, ist dies die einzige verfügbare Option und standardmäßig ausgewählt.

Als Nächstes müssen Sie eine Feldergruppe auswählen, mit der das neue Feld verknüpft werden soll. Beginnen Sie mit der Eingabe des Namens der Feldergruppe in der bereitgestellten Texteingabe. Wenn bereits benutzerdefinierte Feldergruppen vorhanden sind, die mit der Eingabe übereinstimmen, werden diese in der Dropdown-Liste angezeigt. Alternativ können Sie einen eindeutigen Namen eingeben, um stattdessen eine neue Feldergruppe zu erstellen.

![Feldgruppe auswählen](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>Wenn Sie eine vorhandene benutzerdefinierte Feldergruppe auswählen, übernehmen alle anderen Schemas, die diese Feldergruppe verwenden, auch das neu hinzugefügte Feld, nachdem Sie Ihre Änderungen gespeichert haben. Wählen Sie daher nur dann eine existierende Feldergruppe aus, wenn Sie diese Art von Vermehrung wünschen. Andernfalls sollten Sie stattdessen eine neue benutzerdefinierte Feldergruppe erstellen.

Nachdem Sie die Feldergruppe aus der Liste ausgewählt haben, wählen Sie **[!UICONTROL Anwenden]**.

![Feld anwenden](../../images/ui/resources/schemas/apply-field.png)

Das neue Feld wird der Arbeitsfläche hinzugefügt und unter Ihrer [Mandanten-ID](../../api/getting-started.md#know-your-tenant_id) als Namespace angegeben, um Konflikte mit Standard-XDM-Feldern zu vermeiden. Die Feldergruppe, mit der Sie das neue Feld verknüpft haben, wird auch in der linken Leiste unter **[!UICONTROL Feldergruppen]** angezeigt.

![Mandanten-ID](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>Die übrigen von der ausgewählten benutzerdefinierten Feldergruppe bereitgestellten Felder werden standardmäßig aus dem Schema entfernt. Wenn Sie einige dieser Felder zum Schema hinzufügen möchten, wählen Sie ein Feld aus, das zur Gruppe gehört, und wählen Sie dann in der rechten Leiste **[!UICONTROL Zugehörige Felder verwalten]** aus.

#### Weisen Sie das Feld einer benutzerdefinierten Klasse zu {#add-to-class}

Wählen Sie unter &quot;**[!UICONTROL Zuweisen zu]**&quot;die Option &quot;**[!UICONTROL Klasse]**&quot;. Das nachstehende Eingabefeld wird durch den Namen der benutzerdefinierten Klasse des aktuellen Schemas ersetzt und gibt an, dass das neue Feld dieser Klasse zugewiesen wird.

![ Die für die neue Feldzuweisung ausgewählte Option [!UICONTROL Klasse].](../../images/ui/resources/schemas/assign-field-to-class.png)

Fahren Sie mit der Konfiguration des Felds fort und wählen Sie **[!UICONTROL Anwenden]** , wenn Sie fertig sind.

![[!UICONTROL Anwenden], das für das neue Feld ausgewählt wurde.](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

Das neue Feld wird der Arbeitsfläche hinzugefügt und unter Ihrer [Mandanten-ID](../../api/getting-started.md#know-your-tenant_id) als Namespace angegeben, um Konflikte mit Standard-XDM-Feldern zu vermeiden. Wenn Sie den Klassennamen in der linken Leiste auswählen, wird das neue Feld als Teil der Klassenstruktur angezeigt.

![Das neue Feld, das auf die Struktur der benutzerdefinierten Klasse angewendet wird und auf der Arbeitsfläche dargestellt wird.](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### Fügen Sie benutzerdefinierte Felder zur Struktur von Standardfeldgruppen hinzu {#custom-fields-for-standard-groups}

Wenn das Schema, mit dem Sie arbeiten, ein Objekt enthält, das von einer Standardfeldgruppe bereitgestellt wird, können Sie diesem Standardobjekt eigene benutzerdefinierte Felder hinzufügen.

>[!WARNING]
>
>Alle Felder, die einer Feldergruppe in einem Schema hinzugefügt werden, werden auch in allen anderen Schemas angezeigt, die dieselbe Feldergruppe verwenden. Wenn ein benutzerdefiniertes Feld zu einer Standardfeldgruppe hinzugefügt wird, wird diese Feldergruppe in eine benutzerdefinierte Feldergruppe konvertiert und die ursprüngliche Standardfeldgruppe ist nicht mehr verfügbar.
>
>Wenn Sie an der Beta-Version für diese Funktion teilgenommen haben, erhalten Sie einen Dialog, in dem Sie über die Standardfeldgruppen informiert werden, die Sie zuvor angepasst haben. Nachdem Sie **[!UICONTROL Bestätigen]** ausgewählt haben, werden die aufgelisteten Ressourcen in benutzerdefinierte Feldergruppen konvertiert.
>
>![Bestätigungsdialogfeld zum Konvertieren von Standardfeldgruppen](../../images/ui/resources/schemas/beta-extension-confirmation.png)

Wählen Sie zunächst das Pluszeichen (**+**) neben dem Stamm des von der Standardfeldgruppe bereitgestellten Objekts aus.

![Feld zum Standardobjekt hinzufügen](../../images/ui/resources/schemas/add-field-to-standard-object.png)

Es wird eine Warnmeldung angezeigt, in der Sie aufgefordert werden zu bestätigen, ob Sie die Standardfeldgruppe konvertieren möchten. Wählen Sie **[!UICONTROL Fahren Sie mit der Erstellung der Feldergruppe fort]**, um fortzufahren.

![Konvertierung der Feldergruppe bestätigen](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

Die Arbeitsfläche wird mit einem unbenannten Platzhalter für das neue Feld erneut angezeigt. Beachten Sie, dass der Name der Standardfeldgruppe mit &quot;([!UICONTROL Extended])&quot;angehängt wurde, um anzugeben, dass sie von der Originalversion geändert wurde. Verwenden Sie von hier aus die Steuerelemente in der rechten Leiste, um die Eigenschaften des Felds zu definieren.

![Feld zum Standardobjekt hinzugefügt](../../images/ui/resources/schemas/standard-field-group-converted.png)

Nachdem Sie Ihre Änderungen angewendet haben, wird das neue Feld unter Ihrem Mandanten-ID-Namespace innerhalb des Standardobjekts angezeigt. Dieser verschachtelte Namespace verhindert Konflikte mit Feldnamen innerhalb der Feldergruppe selbst, um Änderungen in anderen Schemas zu vermeiden, die dieselbe Feldergruppe verwenden.

![Feld zum Standardobjekt hinzugefügt](../../images/ui/resources/schemas/added-to-standard-object.png)

## Aktivieren eines Schemas für das Echtzeit-Kundenprofil {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="Aktivieren eines Schemas für das Echtzeit-Kundenprofil"
>abstract="Wenn ein Schema für das Echtzeit-Kundenprofil aktiviert ist, werden alle Datensätze, die aus diesem Schema erstellt werden, für das Echtzeit-Kundenprofil verwendet. Dieses führt Daten aus unterschiedlichen Quellen zusammen und erstellt eine vollständige Ansicht jedes Kunden. Nachdem ein Schema verwendet wurde, um Daten in das Echtzeit-Kundenprofil aufzunehmen, kann es nicht mehr deaktiviert werden. Weitere Informationen finden Sie in der Dokumentation."

[Echtzeit-Kundenprofil](../../../profile/home.md) führt Daten aus unterschiedlichen Quellen zusammen, um eine vollständige Ansicht jedes einzelnen Kunden zu erstellen. Wenn die von einem Schema erfassten Daten an diesem Prozess teilnehmen sollen, müssen Sie das Schema zur Verwendung in [!DNL Profile] aktivieren.

>[!IMPORTANT]
>
>Um ein Schema für [!DNL Profile] zu aktivieren, muss ein primäres Identitätsfeld definiert sein. Weitere Informationen finden Sie im Handbuch zum [Definieren von Identitätsfeldern](../fields/identity.md) .

Um das Schema zu aktivieren, wählen Sie zunächst den Namen des Schemas in der linken Leiste aus und wählen Sie dann in der rechten Leiste den Umschalter **[!UICONTROL Profil]** aus.

![](../../images/ui/resources/schemas/profile-toggle.png)

Es wird ein Popup angezeigt, in dem Sie darauf hingewiesen werden, dass ein Schema nach seiner Aktivierung und Speicherung nicht mehr deaktiviert werden kann. Wählen Sie **[!UICONTROL Aktivieren]** aus, um fortzufahren.

![](../../images/ui/resources/schemas/profile-confirm.png)

Die Arbeitsfläche wird mit aktiviertem Umschalter [!UICONTROL Profil] wieder angezeigt.

>[!IMPORTANT]
>
>Da das Schema noch nicht gespeichert wurde, ist dies der Punkt, an dem Sie Ihre Meinung ändern, das Schema im Echtzeit-Kundenprofil teilnehmen zu lassen: Nachdem Sie ein aktiviertes Schema gespeichert haben, kann es nicht mehr deaktiviert werden. Wählen Sie den Umschalter **[!UICONTROL Profil]** erneut aus, um das Schema zu deaktivieren.

Um den Prozess abzuschließen, wählen Sie **[!UICONTROL Speichern]** aus, um das Schema zu speichern.

![](../../images/ui/resources/schemas/profile-enabled.png)

Das Schema ist jetzt für die Verwendung im Echtzeit-Kundenprofil aktiviert. Wenn Platform Daten in Datensätze erfasst, die auf diesem Schema basieren, werden diese Daten in Ihre aggregierten Profildaten integriert.

## Anzeigenamen für Schemafelder bearbeiten {#display-names}

Nachdem Sie einem Schema eine Klasse zugewiesen und Feldergruppen hinzugefügt haben, können Sie die Anzeigenamen der Felder des Schemas bearbeiten, unabhängig davon, ob diese Felder von standardmäßigen oder benutzerdefinierten XDM-Ressourcen bereitgestellt wurden.

>[!NOTE]
>
>Beachten Sie, dass die Anzeigenamen von Feldern, die zu Standardklassen oder Feldgruppen gehören, nur im Kontext eines bestimmten Schemas bearbeitet werden können. Das heißt, dass die Änderung des Anzeigenamens eines Standardfelds in einem Schema keine Auswirkungen auf andere Schemas hat, die dieselbe zugeordnete Klasse oder Feldergruppe verwenden.
>
>Sobald Sie die Anzeigenamen für die Felder eines Schemas ändern, werden diese Änderungen sofort in allen vorhandenen Datensätzen übernommen, die auf diesem Schema basieren.

Um den Anzeigenamen eines Schemafelds zu bearbeiten, wählen Sie das Feld auf der Arbeitsfläche aus. Geben Sie in der rechten Leiste unter **[!UICONTROL Anzeigename]** den neuen Namen ein.

![](../../images/ui/resources/schemas/display-name.png)

Wählen Sie in der rechten Leiste **[!UICONTROL Anwenden]** und die Arbeitsfläche wird aktualisiert, um den neuen Anzeigenamen des Felds anzuzeigen. Wählen Sie **[!UICONTROL Speichern]** aus, um die Änderungen auf das Schema anzuwenden.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Klasse eines Schemas ändern {#change-class}

Sie können die Klasse eines Schemas während des anfänglichen Kompositionsprozesses jederzeit ändern, bevor das Schema gespeichert wurde.

>[!WARNING]
>
>Die Neuzuweisung der Klasse für ein Schema sollte mit äußerster Vorsicht erfolgen. Feldergruppen sind nur mit bestimmten Klassen kompatibel. Daher werden die Arbeitsfläche und alle von Ihnen hinzugefügten Felder beim Ändern der Klasse zurückgesetzt.

Um eine Klasse neu zuzuweisen, wählen Sie auf der linken Seite der Arbeitsfläche **[!UICONTROL Zuweisen]** aus.

![](../../images/ui/resources/schemas/assign-class-button.png)

Es wird ein Dialogfeld angezeigt, in dem eine Liste aller verfügbaren Klassen angezeigt wird, einschließlich aller von Ihrem Unternehmen definierten Klassen (der Inhaber ist &quot;[!UICONTROL Kunde]&quot;) sowie der von Adobe definierten Standardklassen.

Wählen Sie eine Klasse aus der Liste aus, um ihre Beschreibung auf der rechten Seite des Dialogfelds anzuzeigen. Sie können auch **[!UICONTROL Klassenstruktur in der Vorschau anzeigen]** auswählen, um die mit der Klasse verknüpften Felder und Metadaten anzuzeigen. Wählen Sie **[!UICONTROL Klasse zuweisen]** aus, um fortzufahren.

![](../../images/ui/resources/schemas/assign-class.png)

Es wird ein neues Dialogfeld geöffnet, in dem Sie aufgefordert werden zu bestätigen, dass Sie eine neue Klasse zuweisen möchten. Wählen Sie zur Bestätigung **[!UICONTROL Zuweisen]** aus.

![](../../images/ui/resources/schemas/assign-confirm.png)

Nach Bestätigung der Klassenänderung wird die Arbeitsfläche zurückgesetzt und der gesamte Kompositionsprozess geht verloren.

## Nächste Schritte {#next-steps}

In diesem Dokument wurden die Grundlagen zum Erstellen und Bearbeiten von Schemas in der Platform-Benutzeroberfläche beschrieben. Es wird dringend empfohlen, das Tutorial [zur Schemaerstellung](../../tutorials/create-schema-ui.md) für einen umfassenden Workflow zum Erstellen eines vollständigen Schemas in der Benutzeroberfläche zu lesen, einschließlich der Erstellung benutzerdefinierter Feldergruppen und Datentypen für eindeutige Anwendungsfälle.

Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie in der Übersicht über den Arbeitsbereich [[!UICONTROL Schemas] ](../overview.md) .

Informationen zum Verwalten von Schemas in der [!DNL Schema Registry]-API finden Sie im [Schemas-Endpunkthandbuch](../../api/schemas.md).
