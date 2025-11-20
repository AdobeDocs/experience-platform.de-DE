---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Datenmodell;UI;Arbeitsbereich;Klasse;Klassen;
solution: Experience Platform
title: Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Experience Platform Klassen erstellen und bearbeiten.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: a05ee385694b028b513e2fa632079e665ba815bb
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 8%

---

# Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Standard- oder benutzerdefinierte Klassenfilter"
>abstract="Die Liste der verfügbaren Klassen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen den Optionen „Standard“ und „Benutzerdefiniert“ zu wählen. Die Standardoption zeigt von Adobe erstellte Entitäten an und umfasst sowohl XDM-Kontaktprofil- als auch XDM-Erlebnisereignis-Klassen. Die Option „Benutzerdefiniert“ zeigt Entitäten an, die innerhalb Ihres Unternehmens erstellt wurden. Weitere Informationen zum Erstellen und Bearbeiten von Klassen finden Sie in der Dokumentation."

In Adobe Experience Platform definiert die Klasse eines Schemas die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemata, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Adobe bietet mehrere Standardklassen („Kern„) des Experience-Datenmodells (XDM), einschließlich [XDM Individual Profile](../../classes/individual-profile.md) und [XDM ExperienceEvent](../../classes/experienceevent.md). Zusätzlich zu diesen Kernklassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihre Organisation zu beschreiben.

Dieses Dokument bietet einen Überblick darüber, wie Sie benutzerdefinierte Klassen in der Experience Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Grundverständnis des XDM-Systems voraus. Unter [XDM-Übersicht](../../home.md) finden Sie eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und die [Grundlagen der Schemakomposition](../../schema/composition.md) um zu erfahren, wie Klassen zu XDM-Schemata beitragen.

Obwohl dies für dieses Handbuch nicht erforderlich ist, wird empfohlen, auch das Tutorial zum Erstellen [ Schemas in der Benutzeroberfläche zu befolgen](../../tutorials/create-schema-ui.md) um sich mit den verschiedenen Funktionen des Schema-Editors vertraut zu machen.

## Erste Schritte {#getting-started}

Klicken Sie in der Benutzeroberfläche von Experience Platform im linken Navigationsbereich auf **[!UICONTROL Schemas]** , um den [!UICONTROL Schemas]-Arbeitsbereich zu öffnen, und wählen Sie dann die Registerkarte **[!UICONTROL Classes]** aus. Eine Liste der verfügbaren Klassen wird angezeigt.

![Die Anzahl der Klassen auf der Registerkarte &quot;[!UICONTROL Classes]&quot; der [!UICONTROL Schemas] von [!UICONTROL Classes] Workspace und [!UICONTROL Schemas] hervorgehoben.](../../images/ui/resources/classes/available-classes.png)

## Klassen filtern {#filter}

Die Liste der Klassen wird automatisch nach ihrer Erstellung gefiltert. Die Standardeinstellung zeigt die von Adobe definierten Klassen an. Sie können die Liste auch so filtern, dass die von Ihrem Unternehmen erstellten Listen angezeigt werden. Wählen Sie das Optionsfeld aus, um zwischen den Optionen [!UICONTROL Standard] und [!UICONTROL Custom] auszuwählen. Die Option [!UICONTROL Standard] zeigt Entitäten an, die von Adobe erstellt wurden, und die Option [!UICONTROL Custom] zeigt Entitäten an, die in Ihrem Unternehmen erstellt wurden.

![Die Registerkarte &quot;[!UICONTROL Classes]&quot; des Arbeitsbereichs &quot;[!UICONTROL Schemas]&quot; mit hervorgehobenen [!UICONTROL Standard] und [!UICONTROL Custom].](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Verwenden Sie die Suchfunktionen, um eine Klasse anhand ihres Namens zu filtern oder zu finden. Weitere Informationen finden Sie im Handbuch [Erkunden von XDM](../explore.md)Ressourcen“.

## Erstellen einer neuen Klasse {#create}

Es gibt zwei Methoden, um eine Klasse in der Experience Platform-Benutzeroberfläche zu erstellen: über **[!UICONTROL Create class]** oder **[!UICONTROL Create schema]**.

### Klasse erstellen

Wählen Sie **[!UICONTROL Create class]** auf der Registerkarte [!UICONTROL Classes] im Arbeitsbereich [!UICONTROL Schemas] aus.

![Die Registerkarte &quot;[!UICONTROL Classes]&quot; des Arbeitsbereichs &quot;[!UICONTROL Schemas]&quot; mit hervorgehobener [!UICONTROL Create class]](../../images/ui/resources/classes/create-class.png)

Das Dialogfeld [!UICONTROL Create class] wird angezeigt. Geben Sie einen [!UICONTROL Display name] und einen [!UICONTROL Description] für Ihre Klasse ein und wählen Sie das beabsichtigte Verhalten Ihrer Klasse mit den Optionsfeldern aus. Klassen können vom Typ [!UICONTROL Record] oder [!UICONTROL Time-series] sein. Wählen Sie **[!UICONTROL Create]** aus, um Ihre Auswahl zu bestätigen und zur Registerkarte [!UICONTROL Classes] zurückzukehren.

![Das Dialogfeld &quot;[!UICONTROL Create class]&quot; mit hervorgehobener [!UICONTROL Create].](../../images/ui/resources/classes/create-class-dialog.png)

Die erstellte Klasse ist verfügbar und in der [!UICONTROL Classes] aufgeführt.

![Die Registerkarte &quot;[!UICONTROL Classes]&quot; des Arbeitsbereichs &quot;[!UICONTROL Schemas]&quot; mit der hervorgehobenen kürzlich erstellten Klasse.](../../images/ui/resources/classes/new-class-listing.png)

### Schema erstellen

Alternativ können Sie eine Klasse erstellen, indem Sie ein Schema manuell erstellen. Wählen Sie **[!UICONTROL Create schema]** auf der Registerkarte [!UICONTROL Classes] im Arbeitsbereich [!UICONTROL Schemas] aus.

![Die Registerkarte &quot;[!UICONTROL Classes]&quot; des Arbeitsbereichs &quot;[!UICONTROL Schemas]&quot; mit hervorgehobener [!UICONTROL Create schema]](../../images/ui/resources/classes/create-schema.png)

Wählen Sie **[!UICONTROL Manual]** im angezeigten [!UICONTROL Create a schema] aus.

>[!NOTE]
>
>Wenn Sie den Workflow zur Erstellung eines ML-unterstützten Schemas verwenden, können Sie eine Datei hochladen und ML-Algorithmen verwenden, um ein empfohlenes Schema zu generieren. In diesem Workflow zur Schemaerstellung müssen Sie die Basisklasse für Ihr Schema nicht angeben. Informationen dazu, wie ML eine Schemastruktur basierend auf einer CSV-Datei empfehlen kann, finden Sie im [Handbuch zur Erstellung von Schemata durch maschinelles Lernen](../ml-assisted-schema-creation.md).

![Das Dialogfeld „Schema erstellen“ mit den Workflow-Optionen und hervorgehobener Auswahl.](../../images/ui/resources/classes/manually-create-a-schema.png)

Der Workflow zur Schemaerstellung wird angezeigt. Wählen Sie im [!UICONTROL Schema details] Abschnitt **[!UICONTROL Other]** aus. Eine Liste der verfügbaren Klassen wird angezeigt. Wählen Sie **[!UICONTROL Create class]** aus.

![Der [!UICONTROL Create schema] Workflow mit hervorgehobener [!UICONTROL Other] im [!UICONTROL Schema details] Abschnitt.](../../images/ui/resources/classes/other-schema-details.png)

Das Dialogfeld [!UICONTROL Create class] wird angezeigt. Geben Sie einen [!UICONTROL Display name] und einen [!UICONTROL Description] für Ihre Klasse ein und wählen Sie das beabsichtigte Verhalten Ihrer Klasse mit den Optionsfeldern aus. Klassen können vom Typ [!UICONTROL Record] oder [!UICONTROL Time-series] sein. Wählen Sie **[!UICONTROL Create]** aus, um Ihre Auswahl zu bestätigen und zur Registerkarte [!UICONTROL Classes] zurückzukehren.

![Das Dialogfeld &quot;[!UICONTROL Create class]&quot; mit hervorgehobener [!UICONTROL Create].](../../images/ui/resources/classes/create-class-from-schema.png)

Die Klassenliste wird im Abschnitt [!UICONTROL Schema details] aktualisiert, und die neu erstellte Klasse wird automatisch ausgewählt. Wählen Sie **[!UICONTROL Next]** aus, um mit der Erstellung Ihres Schemas fortzufahren.

![Der [!UICONTROL Schema details] Abschnitt mit der ausgewählten neuen Klasse und [!UICONTROL Next] hervorgehobenen Option.](../../images/ui/resources/classes/select-new-class.png)

Nachdem Sie eine Klasse ausgewählt haben, wird der Abschnitt [!UICONTROL Name and review] angezeigt. In diesem Abschnitt geben Sie einen Namen und eine Beschreibung ein, um Ihr Schema zu identifizieren. &#x200B;Die Basisstruktur des Schemas (bereitgestellt von der -Klasse) wird auf der Arbeitsfläche angezeigt, damit Sie Ihre ausgewählte Klassen- und Schemastruktur überprüfen und überprüfen können.

Geben Sie eine benutzerfreundliche [!UICONTROL Schema display name] in das Textfeld ein. Geben Sie als Nächstes eine geeignete Beschreibung ein, um Ihr Schema zu identifizieren. Wenn Sie Ihre Schemastruktur überprüft haben und mit Ihren Einstellungen zufrieden sind, wählen Sie **[!UICONTROL Finish]** aus, um Ihr Schema zu erstellen.

![Der [!UICONTROL Name and review] Abschnitt des [!UICONTROL Create schema]-Workflows mit Hervorhebung von [!UICONTROL Schema display name], [!UICONTROL Description] und [!UICONTROL Finish].](../../images/ui/resources/classes/schema-details.png)

## Hinzufügen von Feldern zu einer Klasse {#add-fields}

Sobald Sie über ein Schema verfügen, das eine benutzerdefinierte Klasse verwendet, die im Schema-Editor geöffnet ist, können Sie damit beginnen, der Klasse Felder hinzuzufügen. Um ein neues Feld hinzuzufügen, wählen Sie das Symbol **Plus (+)** neben dem Namen des Schemas aus.

>[!IMPORTANT]
>
>Beachten Sie beim Erstellen eines Schemas, das eine von Ihrer Organisation definierte Klasse implementiert, dass Schemafeldgruppen nur für die Verwendung mit kompatiblen Klassen verfügbar sind. Da die definierte Klasse neu ist, werden im **[!UICONTROL Add field group]**-Dialogfeld keine kompatiblen Feldergruppen aufgelistet. Stattdessen müssen Sie [neue Feldergruppen erstellen](./field-groups.md#create) um sie mit dieser Klasse verwenden zu können. Wenn Sie das nächste Mal ein Schema erstellen, das die neue Klasse implementiert, werden die von Ihnen definierten Feldergruppen aufgelistet und stehen zur Verwendung zur Verfügung.

![Der Schema-Editor mit der hervorgehobenen Schaltfläche „Hinzufügen“.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Beachten Sie, dass alle Felder, die Sie einer Klasse hinzufügen, in allen Schemata verwendet werden, die diese Klasse verwenden. Sie sollten daher sorgfältig überlegen, welche Felder in allen Anwendungsfällen des Schemas nützlich sein werden. Wenn Sie ein Feld hinzufügen möchten, das möglicherweise nur in einigen Schemata dieser Klasse verwendet wird, sollten Sie es stattdessen diesen Schemata hinzufügen, indem Sie [eine Feldergruppe erstellen](./field-groups.md#create).

Auf der Arbeitsfläche wird ein **[!UICONTROL Untitled Field]** Platzhalter angezeigt, und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Wählen Sie unter **[!UICONTROL Assign to]** die Option **[!UICONTROL Class]**.

![Ein nicht benanntes Feld auf der Arbeitsfläche des Schema-Editors mit der ausgewählten und hervorgehobenen Eigenschaft &quot;[!UICONTROL Class] Feld zuweisen“.](../../images/ui/resources/classes/assign-to-class.png)

Spezifische Schritte zum Konfigurieren [ Hinzufügen des Felds zur Klasse finden ](../fields/overview.md#define) im Handbuch unter „Definieren von Feldern in der“. Fügen Sie der Klasse weiterhin so viele Felder wie nötig hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Save]** aus, um sowohl das Schema als auch die Klasse zu speichern.

![Das neu erstellte Schema auf der Arbeitsfläche des Schema-Editors, mit hervorgehobener [!UICONTROL Save].](../../images/ui/resources/classes/save.png)

Wenn Sie zuvor Schemata erstellt haben, die diese Klasse verwenden, werden die neu hinzugefügten Felder automatisch in diesen Schemata angezeigt.

## Bearbeiten einer Klasse {#edit-a-class}

>[!NOTE]
>
>Nur benutzerdefinierte Klassen, die von Ihrer Organisation definiert wurden, können vollständig bearbeitet und angepasst werden. Für von Adobe definierte Kernklassen können nur die Anzeigenamen für die Felder im Kontext einzelner Schemata bearbeitet werden. Weitere Informationen finden Sie [ Abschnitt „Bearbeiten von Anzeigenamen für ](./schemas.md#display-names)&quot;.
>
>Nachdem eine benutzerdefinierte Klasse gespeichert und bei der Datenaufnahme verwendet wurde, können anschließend nur noch additive Änderungen daran vorgenommen werden. Weitere Informationen finden [ unter „Regeln ](../../schema/composition.md#evolution) Schemaentwicklung“.

Sie können eine Klasse über den Schema-Workflow bearbeiten, indem Sie ein vorhandenes Schema bearbeiten, das die Klasse erweitert, oder indem Sie ein Schema manuell erstellen. Es ist nicht möglich, eine Klasse direkt zu bearbeiten. Wählen Sie auf der Registerkarte [!UICONTROL Browse] im Arbeitsbereich [!UICONTROL Schemas] eine vorhandene Klasse oder ein vorhandenes **[!UICONTROL Create a schema]** aus.

![Der Schema-Editor mit einer vorhandenen Klasse und dem hervorgehobenen [!UICONTROL Create a schema].](../../images/ui/resources/classes/edit-class-options.png)

Wenn Sie sich für die Erstellung eines neuen Schemas entscheiden, finden Sie weitere Details im Abschnitt [Erstellen eines ](#create-schema)&quot;. Nachdem Sie das Erstellen des Schemas abgeschlossen haben (oder nachdem Sie ein vorhandenes Schema ausgewählt haben), wird der Schema-Editor angezeigt. Um ein vorhandenes Klassenfeld zu aktualisieren, wählen Sie das Feld aus der Schemastruktur aus. Die Feldinformationen werden in der rechten Leiste angezeigt. Stellen Sie die [!UICONTROL Assign to] sicher
Option **[!UICONTROL Class]** ist ausgewählt, da andernfalls Ihre Aktualisierungen keine Auswirkungen auf die Klasse haben.

![Der Schema-Editor mit einem ausgewählten und hervorgehobenen Feld und der angezeigten rechten Leiste, wobei [!UICONTROL Assign to] hervorgehoben wird.](../../images/ui/resources/classes/edit-existing-field.png)

Nehmen Sie die gewünschten Änderungen am Feld vor, indem Sie in der rechten Leiste nach unten scrollen, um **[!UICONTROL Apply]** zum Speichern der Änderungen auszuwählen.

>[!IMPORTANT]
>
> Alle Aktualisierungen, die Sie an Feldern vornehmen, werden gemäß den [Regeln der Schemaentwicklung“ auf alle Schemata angewendet, die diese Klasse ](../../schema/composition.md#evolution).

![Der Schema-Editor mit einem ausgewählten Feld und der rechten Leiste, die angezeigt wird, wobei [!UICONTROL Apply] hervorgehoben wird.](../../images/ui/resources/classes/save-changes.png)

Um neue Felder hinzuzufügen, folgen Sie der Anleitung [Felder zu einer Klasse hinzufügen](#add-fields-to-a-class). Wenn Sie fertig sind, wählen Sie **[!UICONTROL Save]** aus, um sowohl das Schema als auch die Klasse zu speichern.

![Der Schema-Editor mit hervorgehobener [!UICONTROL Save].](../../images/ui/resources/classes/save-schema.png)

## Ändern der Klasse eines Schemas {#schema}

Sie können die Klasse des Schemas während des anfänglichen Erstellungsprozesses jederzeit ändern, bevor es gespeichert wurde. Dies sollte jedoch mit Vorsicht erfolgen, da Feldergruppen nur mit bestimmten Klassen kompatibel sind. Durch das Ändern der Klasse werden die Arbeitsfläche und alle hinzugefügten Felder zurückgesetzt.
Weitere Informationen finden Sie im Handbuch [Erstellen und Bearbeiten ](./schemas.md#change-class) Schemata“.

## Nächste Schritte {#next-steps}

In diesem Dokument wurde beschrieben, wie Klassen mithilfe der Experience Platform-Benutzeroberfläche erstellt und bearbeitet werden. Weiterführende Informationen zu den Funktionen von [!UICONTROL Schemas] Workspace finden Sie in der Übersicht zu [[!UICONTROL Schemas] Workspace ](../overview.md).

Informationen zum Verwalten von Klassen mithilfe der Schema Registry-API finden Sie im [Classes-Endpunkthandbuch](../../api/classes.md).
