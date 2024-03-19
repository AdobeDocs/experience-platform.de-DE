---
title: Definieren von Zuordnungsfeldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche ein Zuordnungsfeld definieren.
source-git-commit: 8eea73c91d0671b1ddaeb8da0dc18b3e5e306f57
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Definieren von Zuordnungsfeldern in der Benutzeroberfläche

Mit Adobe Experience Platform können Sie die Struktur Ihrer benutzerdefinierten Experience-Datenmodell (XDM)-Klassen, Schemafeldgruppen und Datentypen vollständig anpassen.

Sie können auch Zuordnungsfelder im Schema Editor definieren, um flexible und dynamische Datenstrukturen zu modellieren oder eine Sammlung von Schlüssel-Wert-Paaren zu speichern. Die Struktur der Zuordnungsdaten ermöglicht effiziente und schnelle Suchen, Einfügen und Löschen, wo Informationen basierend auf eindeutigen Kennungen organisiert und aufgerufen werden.

Verwenden Sie beim Definieren eines neuen Felds in der Benutzeroberfläche von Platform die **[!UICONTROL Typ]** Dropdown-Liste auswählen **[!UICONTROL Zuordnung]**&quot; aus der Liste.

![Der Schemaeditor mit der Dropdown-Liste Typ und dem Wert Zuordnung hervorgehoben.](../../images/ui/fields/special/map.png)

A [!UICONTROL Map value type] -Eigenschaft angezeigt. Dieser Wert ist erforderlich für [!UICONTROL Zuordnung] Datentypen. Verfügbare Werte für die Zuordnung sind [!UICONTROL Zeichenfolge] und [!UICONTROL Ganzzahl]. Wählen Sie einen Wert aus der Dropdownliste der verfügbaren Optionen aus.

![Der Schema-Editor mit dem [!UICONTROL Map value type] hervorgehoben.](../../images/ui/fields/special/map-value-type.png)

Nachdem Sie das Unterfeld konfiguriert haben, müssen Sie es einer Feldergruppe zuweisen. Verwenden Sie die **[!UICONTROL Feldergruppe]** Dropdown-Menü oder Suchfeld aus und wählen Sie **[!UICONTROL Anwenden]**. Sie können dem Objekt weiterhin Felder mit demselben Prozess hinzufügen oder **[!UICONTROL Speichern]** um Ihre Einstellungen zu bestätigen.

![Eine Aufzeichnung der Feldgruppenauswahl und der angewendeten Einstellungen.](../../images/ui/fields/special/assign-to-field-group.gif)

>[!NOTE]
>
>Die Benutzeroberfläche von Platform weist Einschränkungen hinsichtlich der Extraktion der Schlüssel von Feldern vom Typ Zuordnung auf. Während Objekttypen erweitert werden können, werden Zuordnungen stattdessen als ein einzelnes Feld angezeigt. Über die Schema Registry-API erstellte Zuordnungsfelder, bei denen es sich nicht um Zeichenfolgen- oder Ganzzahldatentypen handelt, werden als[!UICONTROL Komplex]&quot;Datentypen.

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie jetzt in der Platform-Benutzeroberfläche Zuordnungsfelder definieren. Beachten Sie, dass Sie nur Klassen und Feldergruppen verwenden können, um Felder zu Schemas hinzuzufügen. Weitere Informationen zum Verwalten dieser Ressourcen in der Benutzeroberfläche finden Sie in den Handbüchern zum Erstellen und Bearbeiten [classes](../resources/classes.md) und [Feldergruppen](../resources/field-groups.md).

Weitere Informationen zu den Funktionen der [!UICONTROL Schemas] Arbeitsbereich, siehe [[!UICONTROL Schemas] Arbeitsbereich - Übersicht](../overview.md).
