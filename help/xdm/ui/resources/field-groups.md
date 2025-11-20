---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Datenmodell;UI;Arbeitsbereich;Feldergruppe;Feldergruppen;
solution: Experience Platform
title: Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Experience Platform Schemafeldgruppen erstellen und bearbeiten.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 9%

---

# Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="Filter für Gruppen von Standardfeldern oder benutzerdefinierten Feldern"
>abstract="Die Liste der verfügbaren Feldergruppen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen den Optionen „Standard“ und „Benutzerdefiniert“ zu wählen. Die Option „Standard“ zeigt die von Adobe erstellten Entitäten an und die Option „Benutzerdefiniert“ zeigt die in Ihrem Unternehmen erstellten Entitäten an. Weitere Informationen zum Erstellen und Bearbeiten von Feldergruppen finden Sie in der Dokumentation."

Im Experience-Datenmodell (XDM) sind Schemafeldgruppen wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, welche bestimmte Funktionen wie persönliche Details, Hotelvoreinstellungen oder Adressen implementieren. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Eine Feldergruppe definiert auf der Grundlage des Verhaltens der Daten, die die Feldergruppe darstellt (Datensatz oder Zeitreihe), mit welcher(n) Klasse(n) sie kompatibel ist. Das bedeutet, dass nicht alle Feldergruppen für die Verwendung mit allen Klassen verfügbar sind.

Adobe Experience Platform bietet viele Standardfeldgruppen, die eine Vielzahl von Marketing-Anwendungsfällen abdecken. Sie können jedoch auch eigene benutzerdefinierte Feldergruppen erstellen und bearbeiten, um zusätzliche Konzepte zu definieren, die sich auf Ihr Unternehmen in Ihren XDM-Schemata beziehen. Dieses Handbuch bietet einen Überblick darüber, wie Sie benutzerdefinierte Feldergruppen für Ihr Unternehmen in der Experience Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Grundverständnis des XDM-Systems voraus. Eine Einführung in die Rolle [&#x200B; XDM im Experience Platform-Ökosystem &#x200B;](../../home.md) Sie in der Übersicht zu XDM und in die [Grundlagen der Schemakomposition](../../schema/composition.md) wie Feldergruppen zu XDM-Schemata beitragen.

Obwohl dies für dieses Handbuch nicht erforderlich ist, wird empfohlen, auch das Tutorial zum Erstellen [&#x200B; Schemas in der Benutzeroberfläche zu befolgen](../../tutorials/create-schema-ui.md) um sich mit den verschiedenen Funktionen des [!DNL Schema Editor] vertraut zu machen.

## Erstellen einer neuen Feldergruppe {#create}

Um eine neue Feldergruppe zu erstellen, müssen Sie zunächst ein Schema auswählen, dem die Feldergruppe hinzugefügt werden soll. Sie können zwischen [Erstellen eines neuen Schemas](./schemas.md#create) oder [Auswählen eines vorhandenen Schemas zur Bearbeitung](./schemas.md#edit) wählen.

Nachdem Sie das Schema in der [!DNL Schema Editor] geöffnet haben, wählen Sie **[!UICONTROL Add]** neben dem Abschnitt [!UICONTROL Field groups] in der linken Leiste aus.

![](../../images/ui/resources/field-groups/add-field-group.png)

Wählen Sie im angezeigten Dialogfeld die Option **[!UICONTROL Create new field group]** aus. Hier können Sie eine **[!UICONTROL Display name]** und einen **[!UICONTROL Description]** für die Feldergruppe angeben. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Add field groups]** aus.

![](../../images/ui/resources/field-groups/create-field-group.png)

Der [!DNL Schema Editor] wird erneut angezeigt, wobei die neue Feldergruppe in der linken Leiste aufgeführt wird. Da es sich um eine brandneue Feldergruppe handelt, stellt sie derzeit keine Felder für das Schema bereit. Daher bleibt die Arbeitsfläche unverändert. Sie können jetzt [Felder zur Feldergruppe hinzufügen](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Feldergruppen filtern {#filter}

Die Liste der verfügbaren Feldergruppen wird je nach ihrer Erstellung vorab gefiltert. Die Standardeinstellung zeigt die von Adobe definierten Feldergruppen an. Sie können die Liste jedoch auch so filtern, dass die von Ihrem Unternehmen erstellten Listen angezeigt werden. Wählen Sie das Optionsfeld aus, um zwischen den Optionen [!UICONTROL Standard] und [!UICONTROL Custom] auszuwählen. Die Option [!UICONTROL Standard] zeigt Entitäten an, die von Adobe erstellt wurden, und die Option [!UICONTROL Custom] zeigt Entitäten an, die in Ihrem Unternehmen erstellt wurden.

![Die Registerkarte &quot;[!UICONTROL Field groups]&quot; des Arbeitsbereichs &quot;[!UICONTROL Schemas]&quot; mit hervorgehobenen [!UICONTROL Standard] und [!UICONTROL Custom].](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)

## Bearbeiten einer vorhandenen Feldergruppe {#edit}

>[!NOTE]
>
>Nur benutzerdefinierte Feldergruppen, die von Ihrer Organisation definiert wurden, können vollständig bearbeitet und angepasst werden. Für von Adobe definierte Kernfeldgruppen können nur die Anzeigenamen für die Felder im Kontext einzelner Schemata bearbeitet werden. Sie werden im Schema-Editor durch ein Vorhängeschloss-Symbol (![Vorhängeschloss-Symbol) gekennzeichnet.](/help/images/icons/lock-closed.png)). Weitere Informationen finden Sie [&#x200B; Abschnitt „Bearbeiten von Anzeigenamen für &#x200B;](./schemas.md#display-names)&quot;.
>
>Nachdem eine benutzerdefinierte Feldergruppe gespeichert und in einem Schema für die Datenaufnahme verwendet wurde, können anschließend nur noch additive Änderungen an der Feldergruppe vorgenommen werden. Weitere Informationen finden [&#x200B; unter „Regeln &#x200B;](../../schema/composition.md#evolution) Schemaentwicklung“.

Um eine vorhandene Feldergruppe zu bearbeiten, müssen Sie zunächst ein Schema öffnen, das die Feldergruppe innerhalb der [!DNL Schema Editor] verwendet. Sie können [ein vorhandenes Schema zur Bearbeitung auswählen](./schemas.md#edit) oder [ein neues Schema erstellen](./schemas.md#create) und die betreffende Feldergruppe hinzufügen.

Sobald Sie das Schema im Editor geöffnet haben, können Sie beginnen [Felder zur Feldergruppe hinzuzufügen](#add-fields).

## Hinzufügen von Feldern zu einer Feldergruppe {#add-fields}

>[!NOTE]
>
>In diesem Abschnitt wird das Hinzufügen von Feldern zu benutzerdefinierten Feldergruppen beschrieben. Informationen zum Hinzufügen benutzerdefinierter Felder zu Standardfeldgruppen finden Sie im [Handbuch zur Benutzeroberfläche von Schemata](./schemas.md#custom-fields-for-standard-groups).

Um Felder zu einer benutzerdefinierten Feldergruppe hinzuzufügen, wählen Sie zunächst das Symbol **Plus (+)** neben dem Namen des Schemas auf der Arbeitsfläche aus.

![](../../images/ui/resources/field-groups/add-field.png)

Auf der Arbeitsfläche wird ein **[!UICONTROL Untitled Field]** Platzhalter angezeigt, und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Spezifische Schritte zum Konfigurieren [&#x200B; verschiedenen Feldtypen finden Sie &#x200B;](../fields/overview.md#define) Handbuch unter „Definieren von Feldern in der Benutzeroberfläche“.

Wählen Sie unter **[!UICONTROL Assign to]** die Option **[!UICONTROL Field Group]** aus und wählen Sie dann im Dropdown-Menü die gewünschte Feldergruppe aus der Liste aus. Sie können damit beginnen, den Namen der Feldergruppe einzugeben, um die Ergebnisse einzugrenzen.

![](../../images/ui/resources/field-groups/select-field-group.png)

Wählen Sie unter **[!UICONTROL Assign to]** die Option **[!UICONTROL Field Group]** aus und wählen Sie dann im Dropdown-Menü die gewünschte Feldergruppe aus der Liste aus. Sie können damit beginnen, den Namen der Feldergruppe einzugeben, um die Ergebnisse einzugrenzen.

![](../../images/ui/resources/field-groups/select-field-group.png)

Nachdem das Feld zum Schema hinzugefügt wurde, wird es der ausgewählten Feldergruppe zugewiesen. Fügen Sie der Feldergruppe weiterhin so viele Felder wie nötig hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Save]** aus, um sowohl das Schema als auch die Feldergruppe zu speichern.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Wenn dieselbe Feldergruppe bereits in anderen Schemata verwendet wird, werden die neu hinzugefügten Felder automatisch in diesen Schemata angezeigt.

## Nächste Schritte {#next-steps}

In diesem Handbuch wurde beschrieben, wie Sie Feldergruppen mithilfe der Experience Platform-Benutzeroberfläche erstellen und bearbeiten. Weiterführende Informationen zu den Funktionen von [!UICONTROL Schemas] Workspace finden Sie in der Übersicht zu [[!UICONTROL Schemas] Workspace &#x200B;](../overview.md).

Informationen zum Verwalten von Feldergruppen mithilfe der [!DNL Schema Registry]-API finden Sie im [Handbuch zu Feldergruppen-Endpunkten](../../api/field-groups.md).
