---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Feldergruppe; Feldergruppen
solution: Experience Platform
title: Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Schemafeldgruppen in der Experience Platform-Benutzeroberfläche erstellen und bearbeiten.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 0375ddcb7d06208199bf1172b157aa6eb28811f6
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 8%

---

# Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="Standardfilter für benutzerdefinierte Feldergruppen"
>abstract="Die Liste der verfügbaren Feldergruppen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen den Optionen „Standard“ und „Benutzerdefiniert“ zu wählen. Die Option „Standard“ zeigt die von Adobe erstellten Entitäten an und die Option „Benutzerdefiniert“ zeigt die in Ihrem Unternehmen erstellten Entitäten an. Weitere Informationen zum Erstellen und Bearbeiten von Feldergruppen finden Sie in der Dokumentation."

Im Experience-Datenmodell (XDM) sind Schemafeldgruppen wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die bestimmte Funktionen wie persönliche Details, Hotelpräferenzen oder Adressen implementieren. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Eine Feldergruppe definiert, mit welcher Klasse(n) sie kompatibel ist, basierend auf dem Verhalten der Daten, die die Feldergruppe darstellt (Datensatz oder Zeitreihen). Das bedeutet, dass nicht alle Feldergruppen für alle Klassen verfügbar sind.

Adobe Experience Platform bietet viele Standardfeldgruppen, die eine Vielzahl von Marketing-Anwendungsfällen abdecken. Sie können jedoch auch eigene benutzerdefinierte Feldergruppen erstellen und bearbeiten, um zusätzliche Konzepte zu Ihrem Unternehmen in Ihren XDM-Schemas zu definieren. Dieses Handbuch bietet einen Überblick darüber, wie Sie benutzerdefinierte Feldergruppen für Ihre Organisation in der Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Siehe Abschnitt [XDM-Übersicht](../../home.md) für eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und [Grundlagen der Schemakomposition](../../schema/composition.md) für den Beitrag von Feldergruppen zu XDM-Schemas.

Für dieses Handbuch ist zwar nicht erforderlich, es wird jedoch empfohlen, auch das Tutorial zu [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) sich mit den verschiedenen Fähigkeiten der [!DNL Schema Editor].

## Neue Feldergruppe erstellen {#create}

Um eine neue Feldergruppe zu erstellen, müssen Sie zunächst ein Schema auswählen, dem die Feldergruppe hinzugefügt wird. Sie können zwischen [Erstellen eines neuen Schemas](./schemas.md#create) oder [ein vorhandenes Schema zur Bearbeitung auswählen](./schemas.md#edit).

Sobald Sie das Schema im [!DNL Schema Editor]auswählen **[!UICONTROL Hinzufügen]** neben dem [!UICONTROL Feldergruppen] in der linken Leiste.

![](../../images/ui/resources/field-groups/add-field-group.png)

Wählen Sie im angezeigten Dialogfeld **[!UICONTROL Neue Feldergruppe erstellen]**. Hier können Sie eine **[!UICONTROL Anzeigename]** und **[!UICONTROL Beschreibung]** für die Feldergruppe. Wählen Sie zum Abschluss **[!UICONTROL Feldergruppen hinzufügen]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

Die [!DNL Schema Editor] wird erneut angezeigt, wobei die neue Feldergruppe in der linken Leiste aufgelistet ist. Da es sich um eine ganz neue Feldergruppe handelt, stellt sie dem Schema derzeit keine Felder bereit, weshalb die Arbeitsfläche unverändert bleibt. Sie können jetzt beginnen [Felder zur Feldergruppe hinzufügen](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Feldergruppen filtern {#filter}

Die Liste der verfügbaren Feldergruppen wird je nach ihrer Erstellung vorab gefiltert. Die Standardeinstellung zeigt die durch Adobe definierten Feldergruppen an. Sie können die Liste jedoch auch filtern, um die von Ihrer Organisation erstellten anzuzeigen. Wählen Sie das Optionsfeld aus, um zwischen dem [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert] Optionen. Die [!UICONTROL Standard] -Option zeigt die von Adobe erstellten Entitäten an und [!UICONTROL Benutzerdefiniert] -Option zeigt Entitäten an, die innerhalb Ihres Unternehmens erstellt wurden.

![Die [!UICONTROL Feldergruppen] des [!UICONTROL Schemas] Arbeitsbereich mit [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert] hervorgehoben.](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)

## Vorhandene Feldergruppe bearbeiten {#edit}

>[!NOTE]
>
>Nur benutzerdefinierte Feldergruppen, die von Ihrer Organisation definiert wurden, können vollständig bearbeitet und angepasst werden. Bei von Adobe definierten Kernfeldgruppen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schemas bearbeitet werden. Siehe Abschnitt zu [Bearbeiten von Anzeigenamen für Schemafelder](./schemas.md#display-names) für Details.
>
>Nachdem eine benutzerdefinierte Feldergruppe gespeichert und in einem Schema zur Datenerfassung verwendet wurde, können anschließend nur noch additive Änderungen an der Feldergruppe vorgenommen werden. Siehe [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) für weitere Informationen.

Um eine vorhandene Feldergruppe zu bearbeiten, müssen Sie zunächst ein Schema öffnen, das die Feldergruppe innerhalb der [!DNL Schema Editor]. Sie können [ein vorhandenes Schema zur Bearbeitung auswählen](./schemas.md#edit)oder Sie können [Erstellen eines neuen Schemas](./schemas.md#create) und fügen Sie die betreffende Feldergruppe hinzu.

Sobald Sie das Schema im Editor geöffnet haben, können Sie beginnen [Felder zur Feldergruppe hinzufügen](#add-fields).

## Felder zu einer Feldergruppe hinzufügen {#add-fields}

>[!NOTE]
>
>Dieser Abschnitt konzentriert sich auf das Hinzufügen von Feldern zu benutzerdefinierten Feldergruppen. Informationen zum Hinzufügen benutzerdefinierter Felder zu Standardfeldgruppen finden Sie im Abschnitt [Handbuch zur Schemabenutzeroberfläche](./schemas.md#custom-fields-for-standard-groups).

Um Felder zu einer benutzerdefinierten Feldergruppe hinzuzufügen, wählen Sie zunächst die **plus (+)** neben dem Namen des Schemas auf der Arbeitsfläche.

![](../../images/ui/resources/field-groups/add-field.png)

Ein **[!UICONTROL Unbenanntes Feld]** Platzhalter wird in der Arbeitsfläche angezeigt und die rechte Leiste aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Siehe Handbuch unter [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) für spezifische Schritte zur Konfiguration verschiedener Feldtypen.

under **[!UICONTROL Zuweisen zu]**, wählen Sie die **[!UICONTROL Feldergruppe]** und wählen Sie dann im Dropdown-Menü die gewünschte Feldergruppe aus der Liste aus. Sie können mit der Eingabe des Namens der Feldergruppe beginnen, um die Ergebnisse einzugrenzen.

![](../../images/ui/resources/field-groups/select-field-group.png)

under **[!UICONTROL Zuweisen zu]**, wählen Sie die **[!UICONTROL Feldergruppe]** und wählen Sie dann im Dropdown-Menü die gewünschte Feldergruppe aus der Liste aus. Sie können mit der Eingabe des Namens der Feldergruppe beginnen, um die Ergebnisse einzugrenzen.

![](../../images/ui/resources/field-groups/select-field-group.png)

Nachdem das Feld zum Schema hinzugefügt wurde, wird es der ausgewählten Feldergruppe zugewiesen. Fügen Sie der Feldergruppe weiterhin beliebig viele Felder hinzu. Wählen Sie zum Abschluss **[!UICONTROL Speichern]** , um sowohl das Schema als auch die Feldergruppe zu speichern.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Wenn dieselbe Feldergruppe bereits in anderen Schemas verwendet wird, werden die neu hinzugefügten Felder automatisch in diesen Schemas angezeigt.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Feldergruppen mithilfe der Platform-Benutzeroberfläche erstellen und bearbeiten. Weitere Informationen zu den Funktionen der [!UICONTROL Schemas] Arbeitsbereich, siehe [[!UICONTROL Schemas] Arbeitsbereich - Übersicht](../overview.md).

So verwalten Sie Feldergruppen mit der [!DNL Schema Registry] API, siehe [Endpunktleitfaden für Feldergruppen](../../api/field-groups.md).
