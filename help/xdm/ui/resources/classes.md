---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Erlebnisdatenmodell; Datenmodell; ui; workspace; class; Klassen;
solution: Experience Platform
title: Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Klassen in der Experience Platform-Benutzeroberfläche erstellen und bearbeiten.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c04e5a49f2a4e90345ca20ecd0547d02b5004fcf
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

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Siehe Abschnitt [XDM-Übersicht](../../home.md) für eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und [Grundlagen der Schemakomposition](../../schema/composition.md) , um zu erfahren, wie Klassen zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, es wird jedoch empfohlen, auch das Tutorial zu [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) sich mit den verschiedenen Funktionen des Schema-Editors vertraut zu machen.

## Erste Schritte {#getting-started}

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Schemas]** im linken Navigationsbereich, um die [!UICONTROL Schemas] Arbeitsbereich und wählen Sie dann die **[!UICONTROL Klassen]** Registerkarte. Eine Liste der verfügbaren Klassen wird angezeigt.

## Filterklassen {#filter}

Die Liste der Klassen wird automatisch nach ihrer Erstellung gefiltert. Die Standardeinstellung zeigt die durch Adobe definierten Klassen an. Sie können die Liste auch filtern, um die von Ihrer Organisation erstellten anzuzeigen. Wählen Sie das Optionsfeld aus, um zwischen dem [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert] Optionen. Die [!UICONTROL Standard] -Option zeigt die von Adobe erstellten Entitäten an und [!UICONTROL Benutzerdefiniert] -Option zeigt Entitäten an, die innerhalb Ihres Unternehmens erstellt wurden.

![Die [!UICONTROL Klassen] des [!UICONTROL Schemas] Arbeitsbereich mit [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert] hervorgehoben.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Verwenden Sie die Suchfunktionen, um eine Klasse anhand ihres Namens zu filtern oder zu finden. Siehe Handbuch unter [Erkunden von XDM-Ressourcen](../explore.md) für weitere Informationen.

## Erstellen einer neuen Klasse {#create}

Es gibt zwei Methoden zum Erstellen einer Klasse in der Platform-Benutzeroberfläche. Auf jeder Registerkarte im [!UICONTROL Schemas] Arbeitsbereich auswählen **[!UICONTROL Schema erstellen]** oder von der [!UICONTROL Klassen] tab select **[!UICONTROL Klasse erstellen]**.

![Die [!UICONTROL Klassen] des [!UICONTROL Schemas] Arbeitsbereich mit [!UICONTROL Schema erstellen] und [!UICONTROL Klasse erstellen] hervorgehoben](../../images/ui/resources/classes/create-class-methods.png)

Wenn Sie **[!UICONTROL Klasse erstellen]**, die [!UICONTROL Klasse erstellen] angezeigt. Geben Sie einen [!UICONTROL Anzeigename] und [!UICONTROL Beschreibung] für Ihre Klasse und wählen Sie das gewünschte Verhalten Ihrer Klasse mit den Optionsfeldern aus. Klassen können vom Typ, von Datensatzreihen oder von Zeitreihen sein. Auswählen **[!UICONTROL Erstellen]** um Ihre Auswahl zu bestätigen und zur [!UICONTROL Klassen] Registerkarte.

![Die [!UICONTROL Klasse erstellen] Dialogfeld mit [!UICONTROL Erstellen] hervorgehoben.](../../images/ui/resources/classes/create-class-dialog.png)

Die von Ihnen erstellte Klasse ist verfügbar und wird im [!UICONTROL Klassen] anzeigen.

![Die [!UICONTROL Klassen] des [!UICONTROL Schemas] Arbeitsbereich, in dem die kürzlich erstellte Klasse hervorgehoben ist.](../../images/ui/resources/classes/new-class-listing.png)

### Erstellen oder Bearbeiten einer Klasse {#create-or-edit}

Wenn Sie **[!UICONTROL Schema erstellen]**, die [!UICONTROL Schema erstellen] Workflow angezeigt. Im [!UICONTROL Schemadetails] Bereich, wählen Sie **[!UICONTROL Sonstiges]**. Eine Liste der verfügbaren Klassen wird angezeigt. Von hier aus können Sie bereits vorhandene Klassen durchsuchen und filtern, auf denen Ihre neue Klasse basieren soll.

>[!NOTE]
>
>Nur benutzerdefinierte Klassen, die von Ihrem Unternehmen definiert wurden, können vollständig bearbeitet und angepasst werden. Für von Adobe definierte Kernklassen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schemas bearbeitet werden. Siehe Abschnitt zu [Bearbeiten von Anzeigenamen für Schemafelder](./schemas.md#display-names) für Details.
>
>Sobald eine benutzerdefinierte Klasse gespeichert und bei der Datenerfassung verwendet wurde, können danach nur noch additive Änderungen daran vorgenommen werden. Siehe [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) für weitere Informationen.

![Die [!UICONTROL Schema erstellen] Workflow mit [!UICONTROL Sonstiges] hervorgehoben in [!UICONTROL Schemadetails] Abschnitt.](../../images/ui/resources/classes/other-schema-details.png)

Wählen Sie ein Optionsfeld aus, um die Klassen nach benutzerdefinierten oder Standardklassen zu filtern. Sie können die verfügbaren Ergebnisse auch nach Branche filtern oder mithilfe des Suchfelds nach einer bestimmten Klasse suchen.

![Die [!UICONTROL Schema erstellen] Workflow mit der Suchleiste, [!UICONTROL Benutzerdefiniert], und [!UICONTROL Branchen] hervorgehoben.](../../images/ui/resources/classes/filter-and-search.png)

Um Ihnen bei der Entscheidung über die entsprechende Klasse zu helfen, gibt es Informationen (![Ein Infosymbol.](../../images/ui/resources/classes/info.png)) und Vorschau (![Ein Vorschausymbol.](../../images/ui/resources/classes/preview.png)) für jede Klasse. Das Infosymbol öffnet ein Dialogfeld, das eine Beschreibung der Klasse und der Branche enthält, der sie zugeordnet ist. Über das Vorschausymbol wird ein Vorschaudialogfeld für die Klasse geöffnet, die ein Schema-Diagramm und dessen Eigenschaften enthält.

![Eine Vorschau der ausgewählten Klasse mit hervorgehobenen Schemadiagramm- und Klasseneigenschaften.](../../images/ui/resources/classes/class-preview.png)

Wählen Sie eine beliebige Zeile aus, um eine Klasse auszuwählen, und wählen Sie dann **[!UICONTROL Nächste]** um Ihre Wahl zu bestätigen.

![Die [!UICONTROL Schema erstellen] Workflow mit einer Klasse, die aus der Tabelle der verfügbaren Klassen ausgewählt wurde, und [!UICONTROL Nächste] hervorgehoben.](../../images/ui/resources/classes/select-class.png)

Die [!UICONTROL Name und Überprüfung] angezeigt. Geben Sie in diesem Abschnitt einen Namen und eine Beschreibung ein, um Ihr Schema zu identifizieren. &#x200B;Die (von der Klasse bereitgestellte) Basisstruktur des Schemas wird auf der Arbeitsfläche angezeigt, damit Sie Ihre ausgewählte Klasse und Schemastruktur überprüfen und überprüfen können.

Geben Sie einen kurzen, beschreibenden, eindeutigen und benutzerfreundlichen Namen für die Klasse in der [!UICONTROL Anzeigename des Schemas] Textfeld. Geben Sie anschließend eine Beschreibung ein, um das Verhalten der vom Schema definierten Daten zu ermitteln. Wenn Sie Ihre Schemastruktur überprüft haben und mit Ihren Einstellungen zufrieden sind, wählen Sie **[!UICONTROL Beenden]** , um Ihr Schema zu erstellen.

![Die [!UICONTROL Name und Überprüfung] Abschnitt [!UICONTROL Schema erstellen] Workflow mit dem [!UICONTROL Anzeigename des Schemas], [!UICONTROL Beschreibung], und [!UICONTROL Beenden] hervorgehoben.](../../images/ui/resources/classes/name-and-review-class.png)

Der Schema-Editor wird angezeigt, wobei die Struktur des Schemas auf der Arbeitsfläche angezeigt wird. Sie können jetzt beginnen [Hinzufügen von Feldern zur Klasse](#add-fields).

![Der Schema-Editor mit der Struktur des Schemas wird auf der Arbeitsfläche angezeigt.](../../images/ui/resources/classes/edit.png)

## Felder zu einer Klasse hinzufügen {#add-fields}

Sobald Sie über ein Schema verfügen, das eine benutzerdefinierte Klasse verwendet, öffnen Sie im [!UICONTROL Schema Editor]können Sie damit beginnen, der Klasse Felder hinzuzufügen. Um ein neues Feld hinzuzufügen, wählen Sie die **plus (+)** neben dem Namen des Schemas.

>[!IMPORTANT]
>
>Denken Sie beim Erstellen eines Schemas, das eine von Ihrem Unternehmen definierte Klasse implementiert, daran, dass Schemafeldgruppen nur für kompatible Klassen verfügbar sind. Da die von Ihnen definierte Klasse neu ist, sind keine kompatiblen Feldergruppen in der **[!UICONTROL Feldergruppe hinzufügen]** angezeigt. Stattdessen müssen Sie [Erstellen neuer Feldergruppen](./field-groups.md#create) zur Verwendung mit dieser Klasse. Wenn Sie das nächste Mal ein Schema erstellen, das die neue Klasse implementiert, werden die von Ihnen definierten Feldergruppen aufgelistet und zur Verwendung verfügbar.

![Der Schema-Editor mit hervorgehobener Schaltfläche zum Hinzufügen.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Beachten Sie, dass alle Felder, die Sie zu einer Klasse hinzufügen, in allen Schemas verwendet werden, die diese Klasse verwenden. Daher sollten Sie sorgfältig überlegen, welche Felder in allen Anwendungsfällen des Schemas nützlich sein werden. Wenn Sie erwägen, ein Feld hinzuzufügen, das möglicherweise nur in einigen Schemas unter dieser Klasse verwendet wird, sollten Sie erwägen, es diesen Schemas durch [Erstellen einer Feldergruppe](./field-groups.md#create) anstatt.

Ein **[!UICONTROL Unbenanntes Feld]** Platzhalter wird in der Arbeitsfläche angezeigt und die rechte Leiste aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. under **[!UICONTROL Zuweisen zu]** auswählen **[!UICONTROL Klasse]**.

![Ein unbenanntes Feld auf der Arbeitsfläche des Schemaeditors mit der ausgewählten und hervorgehobenen Feldeigenschaft Zuweisen zur Klasse.](../../images/ui/resources/classes/assign-to-class.png)

Siehe Handbuch unter [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) für spezifische Schritte zum Konfigurieren und Hinzufügen des Felds zur Klasse. Fügen Sie der Klasse weiterhin beliebig viele Felder hinzu. Wählen Sie zum Abschluss **[!UICONTROL Speichern]** , um sowohl das Schema als auch die Klasse zu speichern.

![Das neu erstellte Schema auf der Arbeitsfläche des Schema-Editors mit [!UICONTROL Speichern] hervorgehoben.](../../images/ui/resources/classes/save.png)

Wenn Sie zuvor Schemas erstellt haben, die diese Klasse verwenden, werden die neu hinzugefügten Felder automatisch in diesen Schemata angezeigt.

## Ändern der Klasse eines Schemas {#schema}

Sie können die Klasse des Schemas jederzeit während des anfänglichen Erstellungsprozesses ändern, bevor es gespeichert wurde. Dies sollte jedoch mit Vorsicht erfolgen, da Feldgruppen nur mit bestimmten Klassen kompatibel sind. Durch das Ändern der Klasse werden die Arbeitsfläche und alle von Ihnen hinzugefügten Felder zurückgesetzt.
Siehe Handbuch unter [Erstellen und Bearbeiten von Schemata](./schemas.md#change-class) für weitere Informationen.

## Nächste Schritte {#next-steps}

In diesem Dokument wurde beschrieben, wie Klassen mithilfe der Platform-Benutzeroberfläche erstellt und bearbeitet werden. Weitere Informationen zu den Funktionen der [!UICONTROL Schemas] Arbeitsbereich, siehe [[!UICONTROL Schemas] Arbeitsbereich - Übersicht](../overview.md).

Informationen zum Verwalten von Klassen mithilfe der Schema Registry-API finden Sie in der [Endpunktleitfaden für Klassen](../../api/classes.md).
