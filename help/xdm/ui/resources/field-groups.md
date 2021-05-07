---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;XDM-System;Erlebnisdatenmodell;Datenmodell;ui;Arbeitsbereich;Feldgruppe;Feldgruppen;
solution: Experience Platform
title: Erstellen und Bearbeiten von Schema-Feldgruppen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Schema-Feldgruppen in der Benutzeroberfläche "Experience Platform"erstellen und bearbeiten.
topic: Benutzerhandbuch
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---


# Erstellen und bearbeiten Sie Schema-Feldgruppen in der Benutzeroberfläche

In Experience Data Model (XDM) sind Schema-Feldgruppen wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die bestimmte Funktionen implementieren, wie persönliche Details, Hotelpräferenzen oder Adressen. Feldgruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Eine Feldgruppe definiert, mit welcher Klasse(n) sie kompatibel ist (sind), basierend auf dem Verhalten der Daten, die die Feldgruppe darstellt (Datensatz oder Zeitreihen). Das bedeutet, dass nicht alle Feldgruppen für alle Klassen verfügbar sind.

Adobe Experience Platform bietet viele Standardfeldgruppen, die eine breite Palette von Anwendungsfällen für das Marketing abdecken. Sie können jedoch auch eigene benutzerspezifische Feldgruppen erstellen und bearbeiten, um zusätzliche Konzepte für Ihr Unternehmen in Ihren XDM-Schemas zu definieren. Dieses Handbuch bietet einen Überblick darüber, wie benutzerspezifische Feldgruppen für Ihr Unternehmen in der Plattform-Benutzeroberfläche erstellt, bearbeitet und verwaltet werden.

## Voraussetzungen 

Dieses Handbuch erfordert ein funktionierendes Verständnis des XDM-Systems. Eine Einführung in die Rolle von XDM innerhalb des Experience Platform-Ökosystems finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schema-Komposition](../../schema/composition.md), wie Feldgruppen zu XDM-Schemas beitragen.

Es wird empfohlen, das Tutorial zum [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) zu befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.

## Neue Feldgruppe {#create} erstellen

Um eine neue Feldgruppe zu erstellen, müssen Sie zunächst ein Schema auswählen, dem die Feldgruppe hinzugefügt wird. Sie können entweder [ein neues Schema](./schemas.md#create) oder [ein vorhandenes Schema zur Bearbeitung auswählen.](./schemas.md#edit)

Wenn Sie das Schema in [!DNL Schema Editor] geöffnet haben, wählen Sie **[!UICONTROL Hinzufügen]** in der linken Leiste neben dem Abschnitt [!UICONTROL Feldgruppen] aus.

![](../../images/ui/resources/field-groups/add-field-group.png)

Es wird ein Dialogfeld mit einer Liste der bestehenden Feldgruppen für Ihr Unternehmen angezeigt. Wählen Sie oben im Dialogfeld **[!UICONTROL Neue Feldgruppe erstellen]**. Hier können Sie einen **[!UICONTROL Anzeigenamen]** und **[!UICONTROL Beschreibung]** für die Feldgruppe angeben. Wählen Sie **[!UICONTROL Hinzufügen Feldgruppe]** aus, wenn Sie fertig sind.

![](../../images/ui/resources/field-groups/create-field-group.png)

Das [!DNL Schema Editor] wird wieder angezeigt, wobei die neue Feldgruppe in der linken Leiste aufgeführt wird. Da es sich um eine ganz neue Feldgruppe handelt, werden dem Schema derzeit keine Felder zur Verfügung gestellt, sodass die Arbeitsfläche unverändert bleibt. Sie können nun Beginn [Felder zur Feldgruppe](#add-fields) hinzufügen.

## Bearbeiten einer vorhandenen Feldgruppe {#edit}

>[!NOTE]
>
>Nur benutzerdefinierte Feldgruppen, die von Ihrem Unternehmen definiert wurden, können vollständig bearbeitet und angepasst werden. Bei von der Adobe definierten Kernfeldgruppen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schema bearbeitet werden. Weitere Informationen finden Sie im Abschnitt [Bearbeiten von Anzeigenamen für Schema-Felder](./schemas.md#display-names).
>
>Nachdem eine benutzerspezifische Feldgruppe gespeichert und in einem Schema zur Datenerfassung verwendet wurde, können danach nur noch zusätzliche Änderungen an der Feldgruppe vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schema-Evolution](../../schema/composition.md#evolution).

Um eine bestehende Feldgruppe zu bearbeiten, müssen Sie zunächst ein Schema öffnen, das die Feldgruppe innerhalb von [!DNL Schema Editor] verwendet. Sie können [ein vorhandenes Schema zur Bearbeitung auswählen oder [ein neues Schema ](./schemas.md#create) erstellen und die betreffende Feldgruppe hinzufügen.](./schemas.md#edit)

Nachdem Sie das Schema im Editor geöffnet haben, können Sie den Beginn [Felder zur Feldgruppe](#add-fields) hinzufügen.

## hinzufügen von Feldern zu einer Feldgruppe {#add-fields}

Um Felder zu einer Feldgruppe in [!DNL Schema Editor] hinzuzufügen, wählen Sie in dem Beginn in der linken Leiste den Feldnamen aus und klicken Sie dann auf das Symbol **plus (+)** neben dem Namen des Schemas auf der Arbeitsfläche.

![](../../images/ui/resources/field-groups/add-field.png)

Ein **[!UICONTROL Neues Feld]** wird auf der Arbeitsfläche angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Genaue Schritte zum Konfigurieren und Hinzufügen des Felds zur Feldgruppe finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define).

Fügen Sie der Feldgruppe weiterhin so viele Felder wie erforderlich hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]**, um das Schema und die Feldgruppe zu speichern.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Wenn dieselbe Feldgruppe bereits in anderen Schemas verwendet wird, werden die neu hinzugefügten Felder automatisch in diesen Schemas angezeigt.

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie Sie Feldgruppen mithilfe der Plattform-Benutzeroberfläche erstellen und bearbeiten. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schema] finden Sie unter [[!UICONTROL Schema] Arbeitsbereichsübersicht](../overview.md).

Informationen zum Verwalten von Feldgruppen mit der API finden Sie im Endpunktleitfaden [Feldgruppen](../../api/field-groups.md).[!DNL Schema Registry]