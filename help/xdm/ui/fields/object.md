---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;XDM-System;Erlebnisdatenmodell;Datenmodell;ui;Arbeitsbereich;Objekt;Feld;
solution: Experience Platform
title: Objektfelder in der Benutzeroberfläche definieren
description: Erfahren Sie, wie Sie ein Objekttypfeld in der Benutzeroberfläche "Experience Platform"definieren.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Definieren von Objektfeldern in der Benutzeroberfläche

Mit Adobe Experience Platform können Sie die Struktur Ihrer benutzerdefinierten Experience Data Model-Klassen (XDM), Schema-Feldgruppen und Datentypen vollständig anpassen. Um verwandte Felder in benutzerdefinierten XDM-Ressourcen zu organisieren und zu verschachteln, können Sie Objekttypfelder definieren, die zusätzliche Unterfelder enthalten können.

Wenn [ein neues Feld](./overview.md#define) in der Adobe Experience Platform-Benutzeroberfläche definiert wird, verwenden Sie das Dropdownmenü **[!UICONTROL Typ]** und wählen Sie &quot;[!UICONTROL Objekt]&quot;aus der Liste.

![](../../images/ui/fields/special/object.png)

Wählen Sie **[!UICONTROL Anwenden]**, um das Objekt dem Schema hinzuzufügen. Die Arbeitsfläche wird aktualisiert, um das neue Feld mit dem angewendeten Datentyp [!UICONTROL Object] anzuzeigen, einschließlich der Steuerelemente zum Bearbeiten und Hinzufügen von Unterfeldern zum Objekt.

![](../../images/ui/fields/special/object-applied.png)

Um ein Unterfeld hinzuzufügen, klicken Sie auf das Symbol **plus (+)** neben dem Objektfeld auf der Arbeitsfläche. Unter dem Objekt wird ein neues Feld mit Steuerelementen zum Konfigurieren des Unterfelds in der rechten Leiste angezeigt.

![](../../images/ui/fields/special/object-add-field.png)

Nachdem Sie das Unterfeld konfiguriert und **[!UICONTROL Apply]** ausgewählt haben, können Sie dem Objekt weiterhin Felder mit demselben Prozess hinzufügen. Sie können auch Unterfelder hinzufügen, die Objekte selbst sind, sodass Sie Felder so tief verschachteln können, wie Sie möchten.

![](../../images/ui/fields/special/object-nested.png)

Wenn Sie die Erstellung des Objekts abgeschlossen haben, können Sie feststellen, dass Sie seine Struktur in verschiedenen Klassen und Feldgruppen wiederverwenden möchten. In diesem Fall können Sie das Objekt in einen Datentyp konvertieren. Weitere Informationen finden Sie im Abschnitt zu [Objekte in Datentypen konvertieren](../resources/data-types.md#convert) in der Benutzeroberfläche für Datentypen.

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie Sie ein Objektfeld in der Benutzeroberfläche definieren. Informationen zum Definieren anderer XDM-Feldtypen im [!DNL Schema Editor] finden Sie in der Übersicht unter [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special).
