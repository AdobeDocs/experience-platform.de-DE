---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;XDM-System;Erlebnisdatenmodell;Datenmodell;ui;Workspace;mixin;mixins
solution: Experience Platform
title: Erstellen und Bearbeiten von Mixins in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Mixins in der Benutzeroberfläche "Experience Platform"erstellen und bearbeiten.
topic-legacy: user guide
exl-id: 240b857d-75ad-42fd-9249-050cbc5306a9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 5%

---

# Erstellen und Bearbeiten von Mixins in der Benutzeroberfläche

Im Experience Data Model (XDM) sind Mixins wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die bestimmte Funktionen implementieren, wie persönliche Details, Hotelpräferenzen oder Adressen. Mixins sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Ein Mixin definiert, mit welcher Klasse(n) es kompatibel ist, basierend auf dem Verhalten der Daten, die das Mixin darstellt (Datensatz oder Zeitreihen). Das bedeutet, dass nicht alle Mixins für alle Klassen verfügbar sind.

Adobe Experience Platform bietet viele Standardmischungen, die eine breite Palette von Anwendungsfällen für das Marketing abdecken. Sie können jedoch auch eigene benutzerdefinierte Mixins erstellen und bearbeiten, um zusätzliche Konzepte für Ihr Unternehmen in Ihren XDM-Schemas zu definieren. In diesem Handbuch wird beschrieben, wie Sie benutzerdefinierte Mixins für Ihr Unternehmen in der Plattform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

## Voraussetzungen

Dieses Handbuch erfordert ein funktionierendes Verständnis des XDM-Systems. Eine Einführung in die Rolle von XDM innerhalb des Experience Platform-Ökosystems finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schema-Komposition](../../schema/composition.md), wie Mixins zu XDM-Schemas beitragen.

Es wird empfohlen, das Tutorial zum [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) zu befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.

## Neues Mixin erstellen {#create}

Um ein neues Mixin zu erstellen, müssen Sie zunächst ein Schema auswählen, dem das Mixin hinzugefügt wird. Sie können entweder [ein neues Schema](./schemas.md#create) oder [ein vorhandenes Schema zur Bearbeitung auswählen.](./schemas.md#edit)

Wenn Sie das Schema in [!DNL Schema Editor] geöffnet haben, wählen Sie **[!UICONTROL Hinzufügen]** in der linken Leiste neben dem Abschnitt [!UICONTROL Mixins] aus.

![](../../images/ui/resources/mixins/add-mixin-button.png)

Es wird ein Dialogfeld mit einer Liste der vorhandenen Mixins für Ihr Unternehmen angezeigt. Wählen Sie im oberen Bereich des Dialogfelds **[!UICONTROL Neue Mischung erstellen]**. Hier können Sie einen **[!UICONTROL Anzeigenamen]** und **[!UICONTROL Beschreibung]** für das Mixin angeben. Wählen Sie **[!UICONTROL Hinzufügen mixin]** aus, wenn Sie fertig sind.

![](../../images/ui/resources/mixins/create-mixin.png)

Das [!DNL Schema Editor] wird wieder angezeigt, wobei das neue mixin der linken Leiste aufgeführt wird. Da es sich um ein brandneues Mixin handelt, werden dem Schema derzeit keine Felder zur Verfügung gestellt, sodass die Arbeitsfläche unverändert bleibt. Sie können nun Beginn [hinzufügen, um Felder zum mixin](#add-fields) hinzuzufügen.

## Bearbeiten einer vorhandenen Mischung {#edit}

>[!NOTE]
>
>Nur benutzerdefinierte Mixins, die von Ihrem Unternehmen definiert wurden, können vollständig bearbeitet und angepasst werden. Bei von der Adobe definierten Core-Mixins können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schema bearbeitet werden. Weitere Informationen finden Sie im Abschnitt [Bearbeiten von Anzeigenamen für Schema-Felder](./schemas.md#display-names).
>
>Nachdem ein benutzerdefiniertes Mixin gespeichert und in einem Schema zur Datenaufnahme verwendet wurde, können danach nur noch zusätzliche Änderungen am Mixin vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schema-Evolution](../../schema/composition.md#evolution).

Um ein vorhandenes Mixin zu bearbeiten, müssen Sie zunächst ein Schema öffnen, das das mixin innerhalb von [!DNL Schema Editor] verwendet. Sie können [ein vorhandenes Schema zur Bearbeitung auswählen oder [ein neues Schema](./schemas.md#create) erstellen und das betreffende Gemisch hinzufügen.](./schemas.md#edit)

Nachdem Sie das Schema im Editor geöffnet haben, können Sie den Beginn [Felder zum mixin](#add-fields) hinzufügen.

## hinzufügen von Feldern zu einer Mischung {#add-fields}

Um einem Mixin im Beginn [!DNL Schema Editor] Felder hinzuzufügen, wählen Sie in der linken Leiste den Namen des Mixins aus und klicken Sie dann auf das Symbol **plus (+)** neben dem Namen des Schemas auf der Arbeitsfläche.

![](../../images/ui/resources/mixins/add-field-button.png)

Ein **[!UICONTROL Neues Feld]** wird auf der Arbeitsfläche angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Genaue Schritte zum Konfigurieren und Hinzufügen des Felds zum Mixin finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define).

Fügen Sie dem Mixin weiterhin so viele Felder wie erforderlich hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]**, um das Schema und das Mixin zu speichern.

![](../../images/ui/resources/mixins/complete-mixin.png)

Wenn dieselbe Mischung bereits in anderen Schemas verwendet wird, werden die neu hinzugefügten Felder automatisch in diesen Schemas angezeigt.

## Nächste Schritte

In diesem Handbuch wurde das Erstellen und Bearbeiten von Mixins mithilfe der Plattform-Benutzeroberfläche behandelt. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schema] finden Sie unter [[!UICONTROL Schema] Arbeitsbereichsübersicht](../overview.md).

Informationen zum Verwalten von Mixins mit der API finden Sie im [!DNL Schema Registry]-Handbuch [mixins endpoint guide](../../api/mixins.md).
