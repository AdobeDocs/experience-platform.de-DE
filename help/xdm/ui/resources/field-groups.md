---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Feldergruppe; Feldergruppen
solution: Experience Platform
title: Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Schemafeldgruppen in der Experience Platform-Benutzeroberfläche erstellen und bearbeiten.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 8%

---

# Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="Filter für Gruppen von Standardfeldern oder benutzerdefinierten Feldern"
>abstract="Die Liste der verfügbaren Feldergruppen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen den Optionen „Standard“ und „Benutzerdefiniert“ zu wählen. Die Option „Standard“ zeigt die von Adobe erstellten Entitäten an und die Option „Benutzerdefiniert“ zeigt die in Ihrem Unternehmen erstellten Entitäten an. Weitere Informationen zum Erstellen und Bearbeiten von Feldergruppen finden Sie in der Dokumentation."

Im Experience-Datenmodell (XDM) sind Schemafeldgruppen wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die bestimmte Funktionen wie persönliche Details, Hotelpräferenzen oder Adressen implementieren. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Eine Feldergruppe definiert, mit welcher Klasse(n) sie kompatibel ist, basierend auf dem Verhalten der Daten, die die Feldergruppe darstellt (Datensatz oder Zeitreihen). Das bedeutet, dass nicht alle Feldergruppen für alle Klassen verfügbar sind.

Adobe Experience Platform bietet viele Standardfeldgruppen, die eine Vielzahl von Marketing-Anwendungsfällen abdecken. Sie können jedoch auch eigene benutzerdefinierte Feldergruppen erstellen und bearbeiten, um zusätzliche Konzepte zu Ihrem Unternehmen in Ihren XDM-Schemas zu definieren. Dieses Handbuch bietet einen Überblick darüber, wie Sie benutzerdefinierte Feldergruppen für Ihre Organisation in der Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schemakomposition](../../schema/composition.md) , wie Feldgruppen zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, Sie sollten jedoch auch das Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche ](../../tutorials/create-schema-ui.md) befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.[

## Neue Feldergruppe erstellen {#create}

Um eine neue Feldergruppe zu erstellen, müssen Sie zunächst ein Schema auswählen, dem die Feldergruppe hinzugefügt wird. Sie können [ein neues Schema erstellen](./schemas.md#create) oder [ein vorhandenes Schema auswählen, um](./schemas.md#edit) zu bearbeiten.

Nachdem Sie das Schema in [!DNL Schema Editor] geöffnet haben, wählen Sie in der linken Leiste neben dem Abschnitt [!UICONTROL Feldergruppen] die Option **[!UICONTROL Hinzufügen]** aus.

![](../../images/ui/resources/field-groups/add-field-group.png)

Wählen Sie im angezeigten Dialogfeld **[!UICONTROL Neue Feldergruppe erstellen]** aus. Hier können Sie einen **[!UICONTROL Anzeigenamen]** und eine **[!UICONTROL Beschreibung]** für die Feldergruppe angeben. Wählen Sie abschließend **[!UICONTROL Feldergruppen hinzufügen]** aus.

![](../../images/ui/resources/field-groups/create-field-group.png)

Die [!DNL Schema Editor] wird erneut angezeigt, wobei die neue Feldergruppe in der linken Leiste aufgelistet ist. Da es sich um eine ganz neue Feldergruppe handelt, stellt sie dem Schema derzeit keine Felder bereit, weshalb die Arbeitsfläche unverändert bleibt. Jetzt können Sie [Felder zur Feldergruppe hinzufügen](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Feldergruppen filtern {#filter}

Die Liste der verfügbaren Feldergruppen wird je nach ihrer Erstellung vorab gefiltert. Die Standardeinstellung zeigt die durch Adobe definierten Feldergruppen an. Sie können die Liste jedoch auch filtern, um die von Ihrer Organisation erstellten anzuzeigen. Wählen Sie das Optionsfeld aus, um zwischen den Optionen [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert] zu wählen. Die Option [!UICONTROL Standard] zeigt von Adobe erstellte Entitäten und die Option [!UICONTROL Benutzerdefiniert] zeigt Entitäten an, die innerhalb Ihres Unternehmens erstellt wurden.

![Die Registerkarte [!UICONTROL Feldergruppen] im Arbeitsbereich [!UICONTROL Schemas] mit den Werten [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert], hervorgehoben.](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)

## Vorhandene Feldergruppe bearbeiten {#edit}

>[!NOTE]
>
>Nur benutzerdefinierte Feldergruppen, die von Ihrer Organisation definiert wurden, können vollständig bearbeitet und angepasst werden. Bei von Adobe definierten Kernfeldgruppen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schemas bearbeitet werden. Sie werden im Schema Editor durch ein Vorhängeschloss-Symbol (![Vorhängeschloss-Symbol) gekennzeichnet.](/help/images/icons/lock-closed.png)). Weitere Informationen finden Sie im Abschnitt [Bearbeiten von Anzeigenamen für Schemafelder](./schemas.md#display-names) .
>
>Nachdem eine benutzerdefinierte Feldergruppe gespeichert und in einem Schema zur Datenerfassung verwendet wurde, können anschließend nur noch additive Änderungen an der Feldergruppe vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) .

Um eine vorhandene Feldergruppe zu bearbeiten, müssen Sie zunächst ein Schema öffnen, das die Feldergruppe innerhalb der [!DNL Schema Editor] verwendet. Sie können [ ein vorhandenes Schema zur Bearbeitung auswählen](./schemas.md#edit) oder [ein neues Schema erstellen](./schemas.md#create) und die betreffende Feldergruppe hinzufügen.

Sobald Sie das Schema im Editor geöffnet haben, können Sie [Felder zur Feldergruppe hinzufügen](#add-fields).

## Felder zu einer Feldergruppe hinzufügen {#add-fields}

>[!NOTE]
>
>Dieser Abschnitt konzentriert sich auf das Hinzufügen von Feldern zu benutzerdefinierten Feldergruppen. Informationen zum Hinzufügen benutzerdefinierter Felder zu Standardfeldgruppen finden Sie im Handbuch [Schemas UI_1}.](./schemas.md#custom-fields-for-standard-groups)

Um Felder zu einer benutzerdefinierten Feldergruppe hinzuzufügen, wählen Sie zunächst auf der Arbeitsfläche das Symbol **Plus (+)** neben dem Namen des Schemas aus.

![](../../images/ui/resources/field-groups/add-field.png)

Auf der Arbeitsfläche wird ein Platzhalter **[!UICONTROL Unbenanntes Feld]** angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Spezifische Schritte zum Konfigurieren verschiedener Feldtypen finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) .

Wählen Sie unter **[!UICONTROL Zuweisen zu]** die Option **[!UICONTROL Feldergruppe]** aus und wählen Sie dann mithilfe der Dropdown-Liste die gewünschte Feldergruppe aus der Liste aus. Sie können mit der Eingabe des Namens der Feldergruppe beginnen, um die Ergebnisse einzugrenzen.

![](../../images/ui/resources/field-groups/select-field-group.png)

Wählen Sie unter **[!UICONTROL Zuweisen zu]** die Option **[!UICONTROL Feldergruppe]** aus und wählen Sie dann mithilfe der Dropdown-Liste die gewünschte Feldergruppe aus der Liste aus. Sie können mit der Eingabe des Namens der Feldergruppe beginnen, um die Ergebnisse einzugrenzen.

![](../../images/ui/resources/field-groups/select-field-group.png)

Nachdem das Feld zum Schema hinzugefügt wurde, wird es der ausgewählten Feldergruppe zugewiesen. Fügen Sie der Feldergruppe weiterhin beliebig viele Felder hinzu. Wählen Sie abschließend **[!UICONTROL Speichern]** aus, um sowohl das Schema als auch die Feldergruppe zu speichern.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Wenn dieselbe Feldergruppe bereits in anderen Schemas verwendet wird, werden die neu hinzugefügten Felder automatisch in diesen Schemas angezeigt.

## Nächste Schritte {#next-steps}

In diesem Handbuch wurde beschrieben, wie Sie Feldergruppen mithilfe der Platform-Benutzeroberfläche erstellen und bearbeiten. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie in der Übersicht über den Arbeitsbereich [[!UICONTROL Schemas] ](../overview.md) .

Informationen zum Verwalten von Feldergruppen mithilfe der API [!DNL Schema Registry] finden Sie im Handbuch [Feldergruppen-Endpunkt-Handbuch](../../api/field-groups.md) .
