---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Objekt; Feld;
solution: Experience Platform
title: Definieren von Objektfeldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Experience Platform ein Objekt definieren.
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Definieren von Objektfeldern in der Benutzeroberfläche

Mit Adobe Experience Platform können Sie die Struktur Ihrer benutzerdefinierten Experience-Datenmodell (XDM)-Klassen, Schemafeldgruppen und Datentypen vollständig anpassen. Um verwandte Felder in benutzerdefinierten XDM-Ressourcen zu organisieren und zu verschachteln, können Sie Objekttypen definieren, die zusätzliche Unterfelder enthalten können.

Wann [Definieren eines neuen Felds](./overview.md#define) Verwenden Sie in der Benutzeroberfläche von Adobe Experience Platform die **[!UICONTROL Typ]** Dropdown-Liste auswählen[!UICONTROL Objekt]&quot; aus der Liste.

![](../../images/ui/fields/special/object.png)

Auswählen **[!UICONTROL Anwenden]** , um das Objekt zum Schema hinzuzufügen. Die Arbeitsfläche wird aktualisiert, um das neue Feld mit dem [!UICONTROL Objekt] angewendeter Datentyp, einschließlich der Steuerelemente zum Bearbeiten und Hinzufügen von Unterfeldern zum Objekt.

![](../../images/ui/fields/special/object-applied.png)

Um ein Unterfeld hinzuzufügen, wählen Sie die **plus (+)** neben dem Objektfeld auf der Arbeitsfläche. Unter dem Objekt wird ein neues Feld mit Steuerelementen zum Konfigurieren des Unterfelds in der rechten Leiste angezeigt.

![](../../images/ui/fields/special/object-add-field.png)

Nachdem Sie das Unterfeld konfiguriert und ausgewählt haben **[!UICONTROL Anwenden]** können Sie dem Objekt weiterhin Felder hinzufügen, indem Sie denselben Prozess verwenden. Sie können auch Unterfelder hinzufügen, die Objekte selbst sind, sodass Sie Felder beliebig tief verschachteln können.

Nachdem Sie die Erstellung des Objekts abgeschlossen haben, sollten Sie dessen Struktur möglicherweise in verschiedenen Klassen und Feldergruppen wiederverwenden. In diesem Fall können Sie das Objekt in einen Datentyp konvertieren. Siehe Abschnitt zu [Konvertieren von Objekten in Datentypen](../resources/data-types.md#convert) im UI-Handbuch für Datentypen finden Sie weitere Informationen.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie ein Objektfeld in der Benutzeroberfläche definiert wird. Siehe Übersicht unter [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special) , um zu erfahren, wie Sie andere XDM-Feldtypen im [!DNL Schema Editor].
