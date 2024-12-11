---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Erlebnisdatenmodell; Datenmodell; ui; workspace; class; Klassen;
solution: Experience Platform
title: Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Klassen in der Experience Platform-Benutzeroberfläche erstellen und bearbeiten.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 02b709c01347c1d03f870132dff437b97f239a9c
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 7%

---

# Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Standard- oder benutzerdefinierte Klassenfilter"
>abstract="Die Liste der verfügbaren Klassen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen den Optionen „Standard“ und „Benutzerdefiniert“ zu wählen. Die Standardoption zeigt von Adobe erstellte Entitäten an und umfasst sowohl XDM-Kontaktprofil- als auch XDM-Erlebnisereignis-Klassen. Die Option „Benutzerdefiniert“ zeigt Entitäten an, die innerhalb Ihres Unternehmens erstellt wurden. Weitere Informationen zum Erstellen und Bearbeiten von Klassen finden Sie in der Dokumentation."

In Adobe Experience Platform definiert die Klasse eines Schemas die Verhaltensaspekte der Daten, die das Schema enthalten wird (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemata, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Adobe bietet mehrere standardmäßige (&quot;Core&quot;) Experience-Datenmodell (XDM)-Klassen, darunter [XDM Individual Profile](../../classes/individual-profile.md) und [XDM ExperienceEvent](../../classes/experienceevent.md). Zusätzlich zu diesen Core-Klassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihr Unternehmen zu beschreiben.

Dieses Dokument bietet einen Überblick darüber, wie benutzerdefinierte Klassen in der Experience Platform-Benutzeroberfläche erstellt, bearbeitet und verwaltet werden.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schemakomposition](../../schema/composition.md) , um zu erfahren, wie Klassen zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, Sie sollten jedoch auch das Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche ](../../tutorials/create-schema-ui.md) befolgen, um sich mit den verschiedenen Funktionen des Schema-Editors vertraut zu machen.[

## Erste Schritte {#getting-started}

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Schemas]** aus, um den Arbeitsbereich [!UICONTROL Schemas] zu öffnen, und wählen Sie dann die Registerkarte **[!UICONTROL Klassen]** aus. Eine Liste der verfügbaren Klassen wird angezeigt.

![Die der Klassen auf der Registerkarte [!UICONTROL Klassen] im Arbeitsbereich [!UICONTROL Schemas] Arbeitsbereich [!UICONTROL Klassen] und [!UICONTROL Schemas] wurden hervorgehoben.](../../images/ui/resources/classes/available-classes.png)

## Filterklassen {#filter}

Die Liste der Klassen wird automatisch nach ihrer Erstellung gefiltert. Die Standardeinstellung zeigt die durch Adobe definierten Klassen an. Sie können die Liste auch filtern, um die von Ihrer Organisation erstellten anzuzeigen. Wählen Sie das Optionsfeld aus, um zwischen den Optionen [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert] zu wählen. Die Option [!UICONTROL Standard] zeigt von Adobe erstellte Entitäten und die Option [!UICONTROL Benutzerdefiniert] zeigt Entitäten an, die innerhalb Ihres Unternehmens erstellt wurden.

![Die Registerkarte [!UICONTROL Klassen] im Arbeitsbereich [!UICONTROL Schemas] mit den Werten [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert], hervorgehoben.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Verwenden Sie die Suchfunktionen, um eine Klasse anhand ihres Namens zu filtern oder zu finden. Weitere Informationen finden Sie im Handbuch zum [Erkunden von XDM-Ressourcen](../explore.md) .

## Erstellen einer neuen Klasse {#create}

Es gibt zwei Methoden zum Erstellen einer Klasse in der Platform-Benutzeroberfläche, über **[!UICONTROL Klasse erstellen]** oder **[!UICONTROL Schema erstellen]**.

### Klasse erstellen

Wählen Sie **[!UICONTROL Create class]** auf der Registerkarte [!UICONTROL Classes] im Arbeitsbereich [!UICONTROL Schemas] aus.

![Die Registerkarte [!UICONTROL Klassen] im Arbeitsbereich [!UICONTROL Schemas] mit dem Namen [!UICONTROL Klasse erstellen] hervorgehoben](../../images/ui/resources/classes/create-class.png)

Das Dialogfeld [!UICONTROL Klasse erstellen] wird angezeigt. Geben Sie einen [!UICONTROL Anzeigenamen] und eine [!UICONTROL Beschreibung] für Ihre Klasse ein und wählen Sie das gewünschte Verhalten Ihrer Klasse mit den Optionsfeldern aus. Klassen können vom Typ [!UICONTROL Datensatz] oder [!UICONTROL Zeitreihen] sein. Wählen Sie **[!UICONTROL Erstellen]** aus, um Ihre Auswahl zu bestätigen und zur Registerkarte [!UICONTROL Klassen] zurückzukehren.

![Das Dialogfeld [!UICONTROL Klasse erstellen] mit hervorgehobenem [!UICONTROL Erstellen]-Symbol.](../../images/ui/resources/classes/create-class-dialog.png)

Die von Ihnen erstellte Klasse ist verfügbar und wird in der Ansicht [!UICONTROL Klassen] aufgeführt.

![Die Registerkarte [!UICONTROL Klassen] im Arbeitsbereich [!UICONTROL Schemas] , wobei die kürzlich erstellte Klasse hervorgehoben ist.](../../images/ui/resources/classes/new-class-listing.png)

### Schema erstellen

Alternativ können Sie eine Klasse durch manuelles Erstellen eines Schemas erstellen. Wählen Sie **[!UICONTROL Schema erstellen]** auf der Registerkarte [!UICONTROL Klassen] im Arbeitsbereich [!UICONTROL Schemas] aus.

![Die Registerkarte [!UICONTROL Klassen] im Arbeitsbereich [!UICONTROL Schemas] mit dem Eintrag [!UICONTROL Schema erstellen] als ](../../images/ui/resources/classes/create-schema.png) markiert

Wählen Sie **[!UICONTROL Manuell]** im daraufhin angezeigten Dialogfeld [!UICONTROL Schema erstellen] aus.

>[!NOTE]
>
>Wenn Sie den Workflow zur Erstellung von ML-unterstützten Schemas verwenden, können Sie eine Datei hochladen und mithilfe von ML-Algorithmen ein empfohlenes Schema generieren. In diesem Workflow zur Schemaerstellung müssen Sie nicht die Basisklasse für Ihr Schema angeben. Informationen dazu, wie ML eine Schemastruktur auf der Basis einer CSV-Datei empfehlen kann, finden Sie im Leitfaden zur Erstellung von Schemas mit maschinellem Lernen](../ml-assisted-schema-creation.md).[

![Das Dialogfeld Schema erstellen mit den Workflow-Optionen und markieren hervorgehoben.](../../images/ui/resources/classes/manually-create-a-schema.png)

Der Workflow für die Schemaerstellung wird angezeigt. Wählen Sie im Abschnitt [!UICONTROL Schemadetails] die Option **[!UICONTROL Sonstige]**. Eine Liste der verfügbaren Klassen wird angezeigt. Wählen Sie **[!UICONTROL Create class]** aus.

![Der Workflow [!UICONTROL Schema erstellen] , wobei [!UICONTROL Sonstige] im Abschnitt [!UICONTROL Schemadetails] hervorgehoben ist.](../../images/ui/resources/classes/other-schema-details.png)

Das Dialogfeld [!UICONTROL Klasse erstellen] wird angezeigt. Geben Sie einen [!UICONTROL Anzeigenamen] und eine [!UICONTROL Beschreibung] für Ihre Klasse ein und wählen Sie das gewünschte Verhalten Ihrer Klasse mit den Optionsfeldern aus. Klassen können vom Typ [!UICONTROL Datensatz] oder [!UICONTROL Zeitreihen] sein. Wählen Sie **[!UICONTROL Erstellen]** aus, um Ihre Auswahl zu bestätigen und zur Registerkarte [!UICONTROL Klassen] zurückzukehren.

![Das Dialogfeld [!UICONTROL Klasse erstellen] mit hervorgehobenem [!UICONTROL Erstellen]-Symbol.](../../images/ui/resources/classes/create-class-from-schema.png)

Die Klassenliste wird im Abschnitt [!UICONTROL Schemadetails] aktualisiert und Ihre neu erstellte Klasse wird automatisch ausgewählt. Wählen Sie **[!UICONTROL Weiter]** aus, um mit der Erstellung Ihres Schemas fortzufahren.

![Der Abschnitt [!UICONTROL Schemadetails] mit der ausgewählten neuen Klasse und [!UICONTROL Weiter] hervorgehoben.](../../images/ui/resources/classes/select-new-class.png)

Nachdem Sie eine Klasse ausgewählt haben, wird der Abschnitt [!UICONTROL Name und Überprüfung] angezeigt. In diesem Abschnitt geben Sie einen Namen und eine Beschreibung ein, um Ihr Schema zu identifizieren. &#x200B;Die (von der Klasse bereitgestellte) Basisstruktur des Schemas wird auf der Arbeitsfläche angezeigt, damit Sie Ihre ausgewählte Klasse und Schemastruktur überprüfen und überprüfen können.

Geben Sie einen benutzerfreundlichen [!UICONTROL Anzeigenamen des Schemas] in das Textfeld ein. Geben Sie anschließend eine Beschreibung ein, die die Identifizierung Ihres Schemas erleichtert. Wenn Sie Ihre Schemastruktur überprüft haben und mit Ihren Einstellungen zufrieden sind, wählen Sie **[!UICONTROL Beenden]** aus, um Ihr Schema zu erstellen.

![Der Abschnitt [!UICONTROL Name und Überprüfung] des Workflows [!UICONTROL Schema erstellen] , in dem der [!UICONTROL Anzeigename des Schemas], die [!UICONTROL Beschreibung] und der Abschnitt [!UICONTROL Beenden] hervorgehoben sind.](../../images/ui/resources/classes/schema-details.png)

## Felder zu einer Klasse hinzufügen {#add-fields}

Sobald Sie über ein Schema verfügen, das eine benutzerdefinierte Klasse verwendet, die im Schema Editor geöffnet ist, können Sie damit beginnen, der Klasse Felder hinzuzufügen. Um ein neues Feld hinzuzufügen, wählen Sie das Symbol **Plus (+)** neben dem Namen des Schemas aus.

>[!IMPORTANT]
>
>Denken Sie beim Erstellen eines Schemas, das eine von Ihrem Unternehmen definierte Klasse implementiert, daran, dass Schemafeldgruppen nur für kompatible Klassen verfügbar sind. Da die von Ihnen definierte Klasse neu ist, sind keine kompatiblen Feldergruppen im Dialogfeld **[!UICONTROL Feldergruppe hinzufügen]** aufgeführt. Stattdessen müssen Sie [neue Feldergruppen erstellen](./field-groups.md#create), um sie mit dieser Klasse zu verwenden. Wenn Sie das nächste Mal ein Schema erstellen, das die neue Klasse implementiert, werden die von Ihnen definierten Feldergruppen aufgelistet und zur Verwendung verfügbar.

![Der Schema-Editor mit hervorgehobener Schaltfläche zum Hinzufügen.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Beachten Sie, dass alle Felder, die Sie zu einer Klasse hinzufügen, in allen Schemas verwendet werden, die diese Klasse verwenden. Daher sollten Sie sorgfältig überlegen, welche Felder in allen Anwendungsfällen des Schemas nützlich sein werden. Wenn Sie erwägen, ein Feld hinzuzufügen, das möglicherweise nur in einigen Schemas unter dieser Klasse verwendet wird, sollten Sie es diesen Schemas hinzufügen, indem Sie stattdessen [eine Feldergruppe](./field-groups.md#create) erstellen.

Auf der Arbeitsfläche wird ein Platzhalter **[!UICONTROL Unbenanntes Feld]** angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Wählen Sie unter &quot;**[!UICONTROL Zuweisen zu]**&quot;die Option &quot;**[!UICONTROL Klasse]**&quot;.

![Ein unbenanntes Feld auf der Arbeitsfläche des Schema-Editors mit der Feldeigenschaft &quot;Assign to [!UICONTROL Class]&quot;, ausgewählt und hervorgehoben.](../../images/ui/resources/classes/assign-to-class.png)

Spezifische Schritte zum Konfigurieren und Hinzufügen des Felds zur Klasse finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) . Fügen Sie der Klasse weiterhin beliebig viele Felder hinzu. Wählen Sie abschließend **[!UICONTROL Speichern]** aus, um sowohl das Schema als auch die Klasse zu speichern.

![Das neu erstellte Schema auf der Arbeitsfläche des Schema-Editors mit der Markierung [!UICONTROL Speichern].](../../images/ui/resources/classes/save.png)

Wenn Sie zuvor Schemas erstellt haben, die diese Klasse verwenden, werden die neu hinzugefügten Felder automatisch in diesen Schemata angezeigt.

## Bearbeiten einer Klasse (#edit-a-class)

>[!NOTE]
>
>Nur benutzerdefinierte Klassen, die von Ihrem Unternehmen definiert wurden, können vollständig bearbeitet und angepasst werden. Für von Adobe definierte Kernklassen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schemas bearbeitet werden. Weitere Informationen finden Sie im Abschnitt [Bearbeiten von Anzeigenamen für Schemafelder](./schemas.md#display-names) .
>
>Sobald eine benutzerdefinierte Klasse gespeichert und bei der Datenerfassung verwendet wurde, können danach nur noch additive Änderungen daran vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) .

Sie können eine Klasse über den Schema-Workflow bearbeiten, indem Sie ein vorhandenes Schema bearbeiten, das die Klasse erweitert, oder indem Sie manuell ein Schema erstellen. Es ist nicht möglich, eine Klasse direkt zu bearbeiten. Wählen Sie auf der Registerkarte [!UICONTROL Durchsuchen] im Arbeitsbereich [!UICONTROL Schemas] eine vorhandene Klasse oder **[!UICONTROL Schema erstellen]** aus.

![Der Schema-Editor mit einer vorhandenen Klasse und der [!UICONTROL Schema erstellen] hervorgehoben.](../../images/ui/resources/classes/edit-class-options.png)

Wenn Sie sich dafür entscheiden, ein neues Schema zu erstellen, finden Sie weitere Informationen im Abschnitt [Erstellen eines Schemas](#create-schema) . Nachdem Sie das Schema erstellt haben (oder ein vorhandenes Schema ausgewählt haben), wird der Schema-Editor angezeigt. Um ein vorhandenes Klassenfeld zu aktualisieren, wählen Sie das Feld aus der Schemastruktur aus. Die Informationen des Felds werden in der rechten Leiste angezeigt. Stellen Sie sicher, dass [!UICONTROL Zuweisen zu]
die Option **[!UICONTROL Klasse]** ausgewählt ist, sonst wirken sich Ihre Aktualisierungen nicht auf die Klasse aus.

![Der Schema-Editor mit einem ausgewählten und hervorgehobenen Feld und der rechten Leiste, der [!UICONTROL Zuweisen zu] markiert.](../../images/ui/resources/classes/edit-existing-field.png)

Nehmen Sie die gewünschten Änderungen am Feld vor und scrollen Sie in der rechten Leiste nach unten, um **[!UICONTROL Anwenden]** auszuwählen, um Ihre Änderungen zu speichern.

>[!IMPORTANT]
>
> Alle Aktualisierungen, die Sie an Feldern vornehmen, werden in allen Schemas angewendet, die diese Klasse verwenden. Befolgen Sie dabei die [Regeln der Schemaentwicklung](../../schema/composition.md#evolution).

![Der Schema-Editor mit einem ausgewählten Feld und der rechten Leiste, der [!UICONTROL Anwenden] markiert.](../../images/ui/resources/classes/save-changes.png)

Um neue Felder hinzuzufügen, befolgen Sie die Anleitung [Felder zu einer Klasse hinzufügen](#add-fields-to-a-class) . Wählen Sie abschließend **[!UICONTROL Speichern]** aus, um sowohl das Schema als auch die Klasse zu speichern.

![Der Schema-Editor mit [!UICONTROL Speichern] hervorgehoben.](../../images/ui/resources/classes/save-schema.png)

## Ändern der Klasse eines Schemas {#schema}

Sie können die Klasse des Schemas jederzeit während des anfänglichen Erstellungsprozesses ändern, bevor es gespeichert wurde. Dies sollte jedoch mit Vorsicht erfolgen, da Feldgruppen nur mit bestimmten Klassen kompatibel sind. Durch das Ändern der Klasse werden die Arbeitsfläche und alle von Ihnen hinzugefügten Felder zurückgesetzt.
Weitere Informationen finden Sie im Handbuch zum [Erstellen und Bearbeiten von Schemas](./schemas.md#change-class) .

## Nächste Schritte {#next-steps}

In diesem Dokument wurde beschrieben, wie Klassen mithilfe der Platform-Benutzeroberfläche erstellt und bearbeitet werden. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie in der Übersicht über den Arbeitsbereich [[!UICONTROL Schemas] ](../overview.md) .

Informationen zum Verwalten von Klassen mithilfe der Schema Registry-API finden Sie im [Klassen-Endpunkthandbuch](../../api/classes.md).
