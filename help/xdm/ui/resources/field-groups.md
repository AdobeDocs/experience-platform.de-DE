---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Arbeitsbereich; Feldergruppe; Feldergruppen
solution: Experience Platform
title: Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Schemafeldgruppen in der Benutzeroberfläche "Experience Platform"erstellen und bearbeiten.
topic-legacy: user guide
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) sind Schemafeldgruppen wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die bestimmte Funktionen wie persönliche Details, Hotelpräferenzen oder Adressen implementieren. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Eine Feldergruppe definiert, mit welcher Klasse(n) sie kompatibel ist, basierend auf dem Verhalten der Daten, die die Feldergruppe darstellt (Datensatz oder Zeitreihen). Das bedeutet, dass nicht alle Feldergruppen für alle Klassen verfügbar sind.

Adobe Experience Platform bietet viele Standardfeldgruppen, die eine Vielzahl von Marketing-Anwendungsfällen abdecken. Sie können jedoch auch eigene benutzerdefinierte Feldergruppen erstellen und bearbeiten, um zusätzliche Konzepte zu Ihrem Unternehmen in Ihren XDM-Schemas zu definieren. Dieses Handbuch bietet einen Überblick darüber, wie Sie benutzerdefinierte Feldergruppen für Ihre Organisation in der Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schemakomposition](../../schema/composition.md) , wie Feldgruppen zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, Sie sollten jedoch auch das Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.[

## Neue Feldergruppe erstellen {#create}

Um eine neue Feldergruppe zu erstellen, müssen Sie zunächst ein Schema auswählen, dem die Feldergruppe hinzugefügt wird. Sie können [ein neues Schema](./schemas.md#create) oder [ein vorhandenes Schema zum Bearbeiten](./schemas.md#edit) auswählen.

Nachdem Sie das Schema in [!DNL Schema Editor] geöffnet haben, wählen Sie **[!UICONTROL Hinzufügen]** neben dem Abschnitt [!UICONTROL Feldergruppen] in der linken Leiste aus.

![](../../images/ui/resources/field-groups/add-field-group.png)

Es wird ein Dialogfeld mit einer Liste der vorhandenen Feldergruppen für Ihre Organisation angezeigt. Wählen Sie oben im Dialogfeld **[!UICONTROL Neue Feldergruppe erstellen]** aus. Hier können Sie einen **[!UICONTROL Anzeigenamen]** und **[!UICONTROL Beschreibung]** für die Feldergruppe angeben. Wählen Sie abschließend **[!UICONTROL Feldergruppe hinzufügen]** aus.

![](../../images/ui/resources/field-groups/create-field-group.png)

Das [!DNL Schema Editor] wird erneut angezeigt, wobei die neue Feldergruppe in der linken Leiste aufgelistet ist. Da es sich um eine ganz neue Feldergruppe handelt, stellt sie dem Schema derzeit keine Felder bereit, weshalb die Arbeitsfläche unverändert bleibt. Jetzt können Sie [Felder zur Feldergruppe](#add-fields) hinzufügen.

## Vorhandene Feldergruppe bearbeiten {#edit}

>[!NOTE]
>
>Nur benutzerdefinierte Feldergruppen, die von Ihrer Organisation definiert wurden, können vollständig bearbeitet und angepasst werden. Für von Adobe definierte Hauptfeldgruppen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schemas bearbeitet werden. Weitere Informationen finden Sie im Abschnitt [Bearbeiten von Anzeigenamen für Schemafelder](./schemas.md#display-names) .
>
>Nachdem eine benutzerdefinierte Feldergruppe gespeichert und in einem Schema zur Datenerfassung verwendet wurde, können anschließend nur noch additive Änderungen an der Feldergruppe vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) .

Um eine vorhandene Feldergruppe zu bearbeiten, müssen Sie zunächst ein Schema öffnen, das die Feldergruppe innerhalb von [!DNL Schema Editor] verwendet. Sie können [ein vorhandenes Schema zum Bearbeiten](./schemas.md#edit) auswählen oder [ein neues Schema](./schemas.md#create) erstellen und die betreffende Feldergruppe hinzufügen.

Sobald das Schema im Editor geöffnet ist, können Sie [Felder zur Feldergruppe](#add-fields) hinzufügen.

## Felder zu einer Feldergruppe hinzufügen {#add-fields}

Um einer Feldergruppe in [!DNL Schema Editor] Felder hinzuzufügen, wählen Sie zunächst den Namen der Feldergruppe in der linken Leiste aus und klicken Sie dann auf das Symbol **plus (+)** neben dem Namen des Schemas auf der Arbeitsfläche.

![](../../images/ui/resources/field-groups/add-field.png)

Ein **[!UICONTROL Neues Feld]** wird auf der Arbeitsfläche angezeigt und die rechte Leiste aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Spezifische Schritte zum Konfigurieren und Hinzufügen des Felds zur Feldergruppe finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) .

Fügen Sie der Feldergruppe weiterhin beliebig viele Felder hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]** aus, um sowohl das Schema als auch die Feldergruppe zu speichern.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Wenn dieselbe Feldergruppe bereits in anderen Schemas verwendet wird, werden die neu hinzugefügten Felder automatisch in diesen Schemas angezeigt.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Feldergruppen mithilfe der Platform-Benutzeroberfläche erstellen und bearbeiten. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie unter [[!UICONTROL Schemas] Workspace - Übersicht](../overview.md).

Informationen zum Verwalten von Feldergruppen mithilfe der [!DNL Schema Registry]-API finden Sie im [Handbuch für Feldergruppen-Endpunkte](../../api/field-groups.md).
