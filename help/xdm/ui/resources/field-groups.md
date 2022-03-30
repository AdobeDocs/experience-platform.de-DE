---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Arbeitsbereich; Feldergruppe; Feldergruppen
solution: Experience Platform
title: Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Schemafeldgruppen in der Benutzeroberfläche "Experience Platform"erstellen und bearbeiten.
topic-legacy: user guide
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 716250b8bcfa1b2d9c868aa80b3122da401553b9
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) sind Schemafeldgruppen wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die bestimmte Funktionen wie persönliche Details, Hotelpräferenzen oder Adressen implementieren. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Eine Feldergruppe definiert, mit welcher Klasse(n) sie kompatibel ist, basierend auf dem Verhalten der Daten, die die Feldergruppe darstellt (Datensatz oder Zeitreihen). Das bedeutet, dass nicht alle Feldergruppen für alle Klassen verfügbar sind.

Adobe Experience Platform bietet viele Standardfeldgruppen, die eine Vielzahl von Marketing-Anwendungsfällen abdecken. Sie können jedoch auch eigene benutzerdefinierte Feldergruppen erstellen und bearbeiten, um zusätzliche Konzepte zu Ihrem Unternehmen in Ihren XDM-Schemas zu definieren. Dieses Handbuch bietet einen Überblick darüber, wie Sie benutzerdefinierte Feldergruppen für Ihre Organisation in der Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Siehe Abschnitt [XDM-Übersicht](../../home.md) für eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und die [Grundlagen der Schemakomposition](../../schema/composition.md) für den Beitrag von Feldergruppen zu XDM-Schemas.

Für dieses Handbuch ist zwar nicht erforderlich, es wird jedoch empfohlen, auch das Tutorial zu [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) sich mit den verschiedenen Fähigkeiten der [!DNL Schema Editor].

## Neue Feldergruppe erstellen {#create}

Um eine neue Feldergruppe zu erstellen, müssen Sie zunächst ein Schema auswählen, dem die Feldergruppe hinzugefügt wird. Sie können zwischen [Erstellen eines neuen Schemas](./schemas.md#create) oder [ein vorhandenes Schema zur Bearbeitung auswählen](./schemas.md#edit).

Sobald Sie das Schema im [!DNL Schema Editor]auswählen **[!UICONTROL Hinzufügen]** neben dem [!UICONTROL Feldergruppen] in der linken Leiste.

![](../../images/ui/resources/field-groups/add-field-group.png)

Es wird ein Dialogfeld mit einer Liste der vorhandenen Feldergruppen für Ihre Organisation angezeigt. Wählen Sie oben im Dialogfeld die Option **[!UICONTROL Neue Feldergruppe erstellen]**. Hier können Sie eine **[!UICONTROL Anzeigename]** und **[!UICONTROL Beschreibung]** für die Feldergruppe. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Feldergruppe hinzufügen]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

Die [!DNL Schema Editor] wird erneut angezeigt, wobei die neue Feldergruppe in der linken Leiste aufgelistet ist. Da es sich um eine ganz neue Feldergruppe handelt, stellt sie dem Schema derzeit keine Felder bereit, weshalb die Arbeitsfläche unverändert bleibt. Sie können jetzt beginnen [Felder zur Feldergruppe hinzufügen](#add-fields).

## Vorhandene Feldergruppe bearbeiten {#edit}

>[!NOTE]
>
>Nur benutzerdefinierte Feldergruppen, die von Ihrer Organisation definiert wurden, können vollständig bearbeitet und angepasst werden. Für von Adobe definierte Hauptfeldgruppen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schemas bearbeitet werden. Siehe Abschnitt zu [Bearbeiten von Anzeigenamen für Schemafelder](./schemas.md#display-names) für Details.
>
>Nachdem eine benutzerdefinierte Feldergruppe gespeichert und in einem Schema zur Datenerfassung verwendet wurde, können anschließend nur noch additive Änderungen an der Feldergruppe vorgenommen werden. Siehe [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) für weitere Informationen.

Um eine vorhandene Feldergruppe zu bearbeiten, müssen Sie zunächst ein Schema öffnen, das die Feldergruppe innerhalb der [!DNL Schema Editor]. Sie können [ein vorhandenes Schema zur Bearbeitung auswählen](./schemas.md#edit)oder Sie können [Erstellen eines neuen Schemas](./schemas.md#create) und fügen Sie die betreffende Feldergruppe hinzu.

Sobald das Schema im Editor geöffnet ist, können Sie beginnen [Felder zur Feldergruppe hinzufügen](#add-fields).

## Felder zu einer Feldergruppe hinzufügen {#add-fields}

>[!NOTE]
>
>Dieser Abschnitt konzentriert sich auf das Hinzufügen von Feldern zu benutzerdefinierten Feldergruppen. Informationen zum Hinzufügen benutzerdefinierter Felder zu Standardfeldgruppen finden Sie im Abschnitt [Handbuch zur Schemabenutzeroberfläche](./schemas.md#custom-fields-for-standard-groups).

So fügen Sie Felder zu einer benutzerdefinierten Feldergruppe im [!DNL Schema Editor], wählen Sie zunächst den Namen der Feldergruppe in der linken Leiste aus und wählen Sie dann die **plus (+)** neben dem Namen des Schemas auf der Arbeitsfläche.

![](../../images/ui/resources/field-groups/add-field.png)

A **[!UICONTROL Neues Feld]** wird auf der Arbeitsfläche angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Siehe Handbuch unter [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) für spezifische Schritte zum Konfigurieren und Hinzufügen des Felds zur Feldergruppe.

Fügen Sie der Feldergruppe weiterhin beliebig viele Felder hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]** , um sowohl das Schema als auch die Feldergruppe zu speichern.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Wenn dieselbe Feldergruppe bereits in anderen Schemas verwendet wird, werden die neu hinzugefügten Felder automatisch in diesen Schemas angezeigt.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Feldergruppen mithilfe der Platform-Benutzeroberfläche erstellen und bearbeiten. Weitere Informationen zu den Funktionen der [!UICONTROL Schemas] Arbeitsbereich, siehe [[!UICONTROL Schemas] Arbeitsbereich - Übersicht](../overview.md).

So verwalten Sie Feldergruppen mit der [!DNL Schema Registry] API, siehe [Endpunktleitfaden für Feldergruppen](../../api/field-groups.md).
