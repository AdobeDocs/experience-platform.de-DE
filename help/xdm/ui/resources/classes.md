---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Erlebnisdatenmodell; Datenmodell; ui; workspace; class; Klassen;
solution: Experience Platform
title: Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Klassen in der Experience Platform-Benutzeroberfläche erstellen und bearbeiten.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 8%

---

# Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Standard- oder benutzerdefinierte Klassenfilter"
>abstract="Die Liste der verfügbaren Klassen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen den Optionen „Standard“ und „Benutzerdefiniert“ zu wählen. Die Standardoption zeigt von Adobe erstellte Entitäten an und umfasst sowohl XDM-Kontaktprofil- als auch XDM-Erlebnisereignis-Klassen. Die Option „Benutzerdefiniert“ zeigt Entitäten an, die innerhalb Ihres Unternehmens erstellt wurden. Weitere Informationen zum Erstellen und Bearbeiten von Klassen finden Sie in der Dokumentation."

In Adobe Experience Platform definiert die Klasse eines Schemas die Verhaltensaspekte der Daten, die das Schema enthalten wird (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemata, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Adobe bietet mehrere standardmäßige (&quot;Core&quot;) Experience-Datenmodell (XDM)-Klassen, einschließlich XDM Individual Profile und XDM ExperienceEvent. Zusätzlich zu diesen Core-Klassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihr Unternehmen zu beschreiben.

Dieses Dokument bietet einen Überblick darüber, wie benutzerdefinierte Klassen in der Experience Platform-Benutzeroberfläche erstellt, bearbeitet und verwaltet werden.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schemakomposition](../../schema/composition.md) , um zu erfahren, wie Klassen zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, Sie sollten jedoch auch das Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche ](../../tutorials/create-schema-ui.md) befolgen, um sich mit den verschiedenen Funktionen des Schema-Editors vertraut zu machen.[

## Erste Schritte {#getting-started}

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Schemas]** aus, um den Arbeitsbereich [!UICONTROL Schemas] zu öffnen, und wählen Sie dann die Registerkarte **[!UICONTROL Klassen]** aus. Eine Liste der verfügbaren Klassen wird angezeigt.

## Filterklassen {#filter}

Die Liste der Klassen wird automatisch nach ihrer Erstellung gefiltert. Die Standardeinstellung zeigt die durch Adobe definierten Klassen an. Sie können die Liste auch filtern, um die von Ihrer Organisation erstellten anzuzeigen. Wählen Sie das Optionsfeld aus, um zwischen den Optionen [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert] zu wählen. Die Option [!UICONTROL Standard] zeigt von Adobe erstellte Entitäten und die Option [!UICONTROL Benutzerdefiniert] zeigt Entitäten an, die innerhalb Ihres Unternehmens erstellt wurden.

![Die Registerkarte [!UICONTROL Klassen] im Arbeitsbereich [!UICONTROL Schemas] mit den Werten [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert], hervorgehoben.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Verwenden Sie die Suchfunktionen, um eine Klasse anhand ihres Namens zu filtern oder zu finden. Weitere Informationen finden Sie im Handbuch zum [Erkunden von XDM-Ressourcen](../explore.md) .

## Erstellen einer neuen Klasse {#create}

Es gibt zwei Methoden zum Erstellen einer Klasse in der Platform-Benutzeroberfläche. Wählen Sie auf jeder Registerkarte im Arbeitsbereich [!UICONTROL Schemas] die Option **[!UICONTROL Schema erstellen]** oder wählen Sie auf der Registerkarte [!UICONTROL Klassen] die Option **[!UICONTROL Klasse erstellen]** aus.

![Die Registerkarte [!UICONTROL Klassen] im Arbeitsbereich [!UICONTROL Schemas] mit dem Namen [!UICONTROL Schema erstellen] und [!UICONTROL Klasse erstellen] hervorgehoben](../../images/ui/resources/classes/create-class-methods.png)

Wenn Sie **[!UICONTROL Klasse erstellen]** auswählen, wird das Dialogfeld [!UICONTROL Klasse erstellen] angezeigt. Geben Sie einen [!UICONTROL Anzeigenamen] und eine [!UICONTROL Beschreibung] für Ihre Klasse ein und wählen Sie das gewünschte Verhalten Ihrer Klasse mit den Optionsfeldern aus. Klassen können vom Typ, von Datensatzreihen oder von Zeitreihen sein. Wählen Sie **[!UICONTROL Erstellen]** aus, um Ihre Auswahl zu bestätigen und zur Registerkarte [!UICONTROL Klassen] zurückzukehren.

![Das Dialogfeld [!UICONTROL Klasse erstellen] mit hervorgehobenem [!UICONTROL Erstellen]-Symbol.](../../images/ui/resources/classes/create-class-dialog.png)

Die von Ihnen erstellte Klasse ist verfügbar und wird in der Ansicht [!UICONTROL Klassen] aufgeführt.

![Die Registerkarte [!UICONTROL Klassen] im Arbeitsbereich [!UICONTROL Schemas] , wobei die kürzlich erstellte Klasse hervorgehoben ist.](../../images/ui/resources/classes/new-class-listing.png)

### Erstellen oder Bearbeiten einer Klasse {#create-or-edit}

Wenn Sie alternativ **[!UICONTROL Schema erstellen]** auswählen, wird der Workflow [!UICONTROL Schema erstellen] angezeigt. Wählen Sie im Abschnitt [!UICONTROL Schemadetails] die Option **[!UICONTROL Sonstige]**. Eine Liste der verfügbaren Klassen wird angezeigt. Von hier aus können Sie bereits vorhandene Klassen durchsuchen und filtern, auf denen Ihre neue Klasse basieren soll.

>[!NOTE]
>
>Nur benutzerdefinierte Klassen, die von Ihrem Unternehmen definiert wurden, können vollständig bearbeitet und angepasst werden. Für von Adobe definierte Kernklassen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schemas bearbeitet werden. Weitere Informationen finden Sie im Abschnitt [Bearbeiten von Anzeigenamen für Schemafelder](./schemas.md#display-names) .
>
>Sobald eine benutzerdefinierte Klasse gespeichert und bei der Datenerfassung verwendet wurde, können danach nur noch additive Änderungen daran vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) .

![Der Workflow [!UICONTROL Schema erstellen] , wobei [!UICONTROL Sonstige] im Abschnitt [!UICONTROL Schemadetails] hervorgehoben ist.](../../images/ui/resources/classes/other-schema-details.png)

Wählen Sie ein Optionsfeld aus, um die Klassen nach benutzerdefinierten oder Standardklassen zu filtern. Sie können die verfügbaren Ergebnisse auch nach Branche filtern oder mithilfe des Suchfelds nach einer bestimmten Klasse suchen.

![Der Workflow [!UICONTROL Schema erstellen] mit der Suchleiste, [!UICONTROL Benutzerdefiniert] und [!UICONTROL Branchen] hervorgehoben.](../../images/ui/resources/classes/filter-and-search.png)

Um Ihnen bei der Entscheidung über die entsprechende Klasse zu helfen, gibt es Infos (![Ein Infosymbol).](/help/images/icons/info.png)) und die Vorschau (![Ein Vorschausymbol.](/help/images/icons/preview.png)) für jede Klasse. Das Infosymbol öffnet ein Dialogfeld, das eine Beschreibung der Klasse und der Branche enthält, der sie zugeordnet ist. Über das Vorschausymbol wird ein Vorschaudialogfeld für die Klasse geöffnet, die ein Schema-Diagramm und dessen Eigenschaften enthält.

![Eine Vorschau der ausgewählten Klasse mit hervorgehobenen Schemadiagramm- und Klasseneigenschaften.](../../images/ui/resources/classes/class-preview.png)

Wählen Sie eine beliebige Zeile aus, um eine Klasse auszuwählen, und wählen Sie dann **[!UICONTROL Weiter]** aus, um Ihre Auswahl zu bestätigen.

![Der Workflow [!UICONTROL Schema erstellen] , bei dem eine Klasse aus der Tabelle der verfügbaren Klassen ausgewählt und [!UICONTROL Weiter] hervorgehoben ist.](../../images/ui/resources/classes/select-class.png)

Der Abschnitt [!UICONTROL Name und Überprüfung] des Workflows wird angezeigt. Geben Sie in diesem Abschnitt einen Namen und eine Beschreibung ein, um Ihr Schema zu identifizieren. &#x200B;Die (von der Klasse bereitgestellte) Basisstruktur des Schemas wird auf der Arbeitsfläche angezeigt, damit Sie Ihre ausgewählte Klasse und Schemastruktur überprüfen und überprüfen können.

Geben Sie im Textfeld [!UICONTROL Anzeigename des Schemas] einen kurzen, beschreibenden, eindeutigen und benutzerfreundlichen Namen für die Klasse ein. Geben Sie anschließend eine Beschreibung ein, um das Verhalten der vom Schema definierten Daten zu ermitteln. Wenn Sie Ihre Schemastruktur überprüft haben und mit Ihren Einstellungen zufrieden sind, wählen Sie **[!UICONTROL Beenden]** aus, um Ihr Schema zu erstellen.

![Der Abschnitt [!UICONTROL Name und Überprüfung] des Workflows [!UICONTROL Schema erstellen] , in dem der [!UICONTROL Anzeigename des Schemas], die [!UICONTROL Beschreibung] und der Abschnitt [!UICONTROL Beenden] hervorgehoben sind.](../../images/ui/resources/classes/name-and-review-class.png)

Der Schema-Editor wird angezeigt, wobei die Struktur des Schemas auf der Arbeitsfläche angezeigt wird. Jetzt können Sie [beginnen, der Klasse ](#add-fields) Felder hinzuzufügen.

![Der Schema-Editor mit der Struktur des Schemas wird auf der Arbeitsfläche angezeigt.](../../images/ui/resources/classes/edit.png)

## Felder zu einer Klasse hinzufügen {#add-fields}

Sobald Sie über ein Schema verfügen, das eine benutzerdefinierte Klasse verwendet, die im [!UICONTROL Schema Editor] geöffnet ist, können Sie damit beginnen, der Klasse Felder hinzuzufügen. Um ein neues Feld hinzuzufügen, wählen Sie das Symbol **Plus (+)** neben dem Namen des Schemas aus.

>[!IMPORTANT]
>
>Denken Sie beim Erstellen eines Schemas, das eine von Ihrem Unternehmen definierte Klasse implementiert, daran, dass Schemafeldgruppen nur für kompatible Klassen verfügbar sind. Da die von Ihnen definierte Klasse neu ist, sind keine kompatiblen Feldergruppen im Dialogfeld **[!UICONTROL Feldergruppe hinzufügen]** aufgeführt. Stattdessen müssen Sie [neue Feldergruppen erstellen](./field-groups.md#create), um sie mit dieser Klasse zu verwenden. Wenn Sie das nächste Mal ein Schema erstellen, das die neue Klasse implementiert, werden die von Ihnen definierten Feldergruppen aufgelistet und zur Verwendung verfügbar.

![Der Schema-Editor mit hervorgehobener Schaltfläche zum Hinzufügen.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Beachten Sie, dass alle Felder, die Sie zu einer Klasse hinzufügen, in allen Schemas verwendet werden, die diese Klasse verwenden. Daher sollten Sie sorgfältig überlegen, welche Felder in allen Anwendungsfällen des Schemas nützlich sein werden. Wenn Sie erwägen, ein Feld hinzuzufügen, das möglicherweise nur in einigen Schemas unter dieser Klasse verwendet wird, sollten Sie es diesen Schemas hinzufügen, indem Sie stattdessen [eine Feldergruppe](./field-groups.md#create) erstellen.

Auf der Arbeitsfläche wird ein Platzhalter **[!UICONTROL Unbenanntes Feld]** angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Wählen Sie unter &quot;**[!UICONTROL Zuweisen zu]**&quot;die Option &quot;**[!UICONTROL Klasse]**&quot;.

![Ein unbenanntes Feld auf der Arbeitsfläche des Schemaeditors mit der ausgewählten und hervorgehobenen Eigenschaft &quot;Assign to Class&quot;.](../../images/ui/resources/classes/assign-to-class.png)

Spezifische Schritte zum Konfigurieren und Hinzufügen des Felds zur Klasse finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) . Fügen Sie der Klasse weiterhin beliebig viele Felder hinzu. Wählen Sie abschließend **[!UICONTROL Speichern]** aus, um sowohl das Schema als auch die Klasse zu speichern.

![Das neu erstellte Schema auf der Arbeitsfläche des Schema-Editors mit der Markierung [!UICONTROL Speichern].](../../images/ui/resources/classes/save.png)

Wenn Sie zuvor Schemas erstellt haben, die diese Klasse verwenden, werden die neu hinzugefügten Felder automatisch in diesen Schemata angezeigt.

## Ändern der Klasse eines Schemas {#schema}

Sie können die Klasse des Schemas jederzeit während des anfänglichen Erstellungsprozesses ändern, bevor es gespeichert wurde. Dies sollte jedoch mit Vorsicht erfolgen, da Feldgruppen nur mit bestimmten Klassen kompatibel sind. Durch das Ändern der Klasse werden die Arbeitsfläche und alle von Ihnen hinzugefügten Felder zurückgesetzt.
Weitere Informationen finden Sie im Handbuch zum [Erstellen und Bearbeiten von Schemas](./schemas.md#change-class) .

## Nächste Schritte {#next-steps}

In diesem Dokument wurde beschrieben, wie Klassen mithilfe der Platform-Benutzeroberfläche erstellt und bearbeitet werden. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie in der Übersicht über den Arbeitsbereich [[!UICONTROL Schemas] ](../overview.md) .

Informationen zum Verwalten von Klassen mithilfe der Schema Registry-API finden Sie im [Klassen-Endpunkthandbuch](../../api/classes.md).
