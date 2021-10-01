---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Objekt; Feld;
solution: Experience Platform
title: Definieren von Objektfeldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Experience Platform ein Objekt definieren.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Definieren von Objektfeldern in der Benutzeroberfläche

Mit Adobe Experience Platform können Sie die Struktur Ihrer benutzerdefinierten Experience-Datenmodell (XDM)-Klassen, Schemafeldgruppen und Datentypen vollständig anpassen. Um verwandte Felder in benutzerdefinierten XDM-Ressourcen zu organisieren und zu verschachteln, können Sie Objekttypen definieren, die zusätzliche Unterfelder enthalten können.

Wenn Sie [ein neues Feld](./overview.md#define) in der Adobe Experience Platform-Benutzeroberfläche definieren, verwenden Sie das Dropdown-Menü **[!UICONTROL Typ]** und wählen Sie &quot;[!UICONTROL Objekt]&quot;aus der Liste aus.

![](../../images/ui/fields/special/object.png)

Wählen Sie **[!UICONTROL Apply]** aus, um das Objekt zum Schema hinzuzufügen. Die Arbeitsfläche wird aktualisiert und zeigt das neue Feld mit dem angewendeten Datentyp [!UICONTROL Objekt] an, einschließlich der Steuerelemente zum Bearbeiten und Hinzufügen von Unterfeldern zum Objekt.

![](../../images/ui/fields/special/object-applied.png)

Um ein Unterfeld hinzuzufügen, wählen Sie auf der Arbeitsfläche das Symbol **plus (+)** neben dem Objektfeld aus. Unter dem Objekt wird ein neues Feld mit Steuerelementen zum Konfigurieren des Unterfelds in der rechten Leiste angezeigt.

![](../../images/ui/fields/special/object-add-field.png)

Nachdem Sie das Unterfeld konfiguriert und **[!UICONTROL Anwenden]** ausgewählt haben, können Sie dem Objekt weiterhin Felder mit demselben Prozess hinzufügen. Sie können auch Unterfelder hinzufügen, die Objekte selbst sind, sodass Sie Felder beliebig tief verschachteln können.

![](../../images/ui/fields/special/object-nested.png)

Nachdem Sie die Erstellung des Objekts abgeschlossen haben, sollten Sie dessen Struktur möglicherweise in verschiedenen Klassen und Feldergruppen wiederverwenden. In diesem Fall können Sie das Objekt in einen Datentyp konvertieren. Weitere Informationen finden Sie im Abschnitt zu [Konvertieren von Objekten in Datentypen](../resources/data-types.md#convert) im UI-Handbuch zu Datentypen .

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie ein Objektfeld in der Benutzeroberfläche definiert wird. Informationen zum Definieren anderer XDM-Feldtypen im [!DNL Schema Editor] finden Sie in der Übersicht zu [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special).
