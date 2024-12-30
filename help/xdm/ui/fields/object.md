---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Datenmodell;UI;Arbeitsbereich;Objekt;Feld;
solution: Experience Platform
title: Definieren von Objektfeldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche ein Feld vom Typ „Objekt“ definieren.
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Definieren von Objektfeldern in der Benutzeroberfläche

Mit Adobe Experience Platform können Sie die Struktur Ihrer benutzerdefinierten Experience-Datenmodell (XDM)-Klassen, Schemafeldgruppen und Datentypen vollständig anpassen. Um verwandte Felder in benutzerdefinierten XDM-Ressourcen zu organisieren und zu verschachteln, können Sie Felder vom Typ „Objekt“ definieren, die zusätzliche Unterfelder enthalten können.

Verwenden [ beim Definieren eines ](./overview.md#define) Felds in der Benutzeroberfläche von Adobe Experience Platform das **[!UICONTROL Typ]** und wählen Sie &quot;[!UICONTROL Objekt]&quot; aus der Liste aus.

![](../../images/ui/fields/special/object.png)

Wählen Sie **[!UICONTROL Anwenden]** aus, um das Objekt zum Schema hinzuzufügen. Die Arbeitsfläche wird aktualisiert und zeigt das neue Feld mit angewendetem [!UICONTROL Object]-Datentyp an, einschließlich Steuerelementen zum Bearbeiten und Hinzufügen von Unterfeldern zum Objekt.

![](../../images/ui/fields/special/object-applied.png)

Um ein Unterfeld hinzuzufügen, wählen Sie das Symbol **plus (+)** neben dem Objektfeld auf der Arbeitsfläche aus. Unter dem -Objekt wird ein neues Feld mit Steuerelementen zum Konfigurieren des -Unterfelds in der rechten Leiste angezeigt.

![](../../images/ui/fields/special/object-add-field.png)

Nachdem Sie das Unterfeld konfiguriert und **[!UICONTROL Anwenden]** ausgewählt haben, können Sie dem Objekt weitere Felder hinzufügen, indem Sie denselben Prozess verwenden. Sie können auch Unterfelder hinzufügen, die selbst Objekte sind, sodass Sie Felder beliebig tief verschachteln können.

Nachdem Sie die Erstellung des -Objekts abgeschlossen haben, möchten Sie möglicherweise seine Struktur in verschiedenen Klassen und Feldergruppen wiederverwenden. In diesem Fall können Sie das -Objekt in einen Datentyp konvertieren. Weitere Informationen finden Sie [ Abschnitt zum Konvertieren von Objekten in ](../resources/data-types.md#convert) im Handbuch zur Datentypbenutzeroberfläche.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein -Objektfeld in der Benutzeroberfläche definieren. In der Übersicht über [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special) erfahren Sie, wie Sie andere XDM-Feldtypen in der [!DNL Schema Editor] definieren.
