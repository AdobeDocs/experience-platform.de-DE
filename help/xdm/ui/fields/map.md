---
title: Definieren von Zuordnungsfeldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche ein Zuordnungsfeld definieren.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: ee27fc42a1ee23ef650d320df64e5970a84d0d38
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Definieren von Zuordnungsfeldern in der Benutzeroberfläche

Mit Adobe Experience Platform können Sie die Struktur Ihrer benutzerdefinierten Experience-Datenmodell (XDM)-Klassen, Schemafeldgruppen und Datentypen vollständig anpassen.

Sie können auch Zuordnungsfelder im Schema Editor definieren, um flexible und dynamische Datenstrukturen zu modellieren oder eine Sammlung von Schlüssel-Wert-Paaren zu speichern.

Verwenden Sie beim Definieren eines neuen Felds in der Benutzeroberfläche von Platform das Dropdown-Menü **[!UICONTROL Typ]** und wählen Sie &quot;**[!UICONTROL Zuordnung]**&quot;aus der Liste aus.

![Der Schema-Editor mit dem Dropdown-Menü Typ und dem Wert Zuordnung hervorgehoben.](../../images/ui/fields/special/map.png)

Die Eigenschaft [!UICONTROL Map value type] wird angezeigt. Dieser Wert ist für [!UICONTROL Map] -Datentypen erforderlich. Verfügbare Werte für die Zuordnung sind [!UICONTROL String] und [!UICONTROL Integer]. Wählen Sie einen Wert aus der Dropdownliste der verfügbaren Optionen aus.

![Der Schema-Editor mit dem Dropdown-Menü [!UICONTROL Map value type] hervorgehoben.](../../images/ui/fields/special/map-value-type.png)

Nachdem Sie das Unterfeld konfiguriert haben, müssen Sie es einer Feldergruppe zuweisen. Verwenden Sie das Dropdownmenü **[!UICONTROL Feldergruppe]** oder das Suchfeld und wählen Sie **[!UICONTROL Anwenden]** aus. Sie können dem Objekt weiterhin Felder mit demselben Prozess hinzufügen oder **[!UICONTROL Speichern]** auswählen, um Ihre Einstellungen zu bestätigen.

![Eine Aufzeichnung der Feldgruppenauswahl und der angewendeten Einstellungen.](../../images/ui/fields/special/assign-to-field-group.gif)

## Nutzungsbeschränkungen {#restrictions}

XDM legt die folgenden Einschränkungen für die Verwendung dieses Datentyps fest:

* Zuordnungstypen MÜSSEN vom Typ `object` sein.
* Für Zuordnungstypen dürfen KEINE Eigenschaften definiert sein (d. h. sie definieren &quot;leere&quot;Objekte).
* Zuordnungstypen MÜSSEN ein `additionalProperties.type` -Feld enthalten, das die Werte beschreibt, die auf der Zuordnung platziert werden können, entweder `string` oder `integer`.
* Die Segmentierung mit mehreren Entitäten kann nur anhand der Zuordnungsschlüssel und nicht anhand der Werte definiert werden.
* Karten werden für Kontozielgruppen nicht unterstützt.

Stellen Sie sicher, dass Sie nur Felder vom Typ Zuordnung verwenden, wenn dies unbedingt erforderlich ist, da sie die folgenden Leistungsbeeinträchtigungen aufweisen:

* Die Antwortzeit von [Adobe Experience Platform Query Service](../../../query-service/home.md) wird für 100 Millionen Datensätze von drei Sekunden auf zehn Sekunden reduziert.
* Karten mit weniger als 16 Schlüsseln müssen vorhanden sein. Andernfalls besteht die Gefahr einer weiteren Verschlechterung.

>[!NOTE]
>
>Die Benutzeroberfläche von Platform weist Einschränkungen hinsichtlich der Extraktion der Schlüssel von Feldern vom Typ Zuordnung auf. Während Objekttypen erweitert werden können, werden Zuordnungen stattdessen als ein einzelnes Feld angezeigt. Über die Schema Registry-API erstellte Zuordnungsfelder, bei denen es sich nicht um Zeichenfolgen- oder Ganzzahldatentypen handelt, werden als Datentypen vom Typ &quot;[!UICONTROL Komplex]&quot;angezeigt.

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie jetzt in der Platform-Benutzeroberfläche Zuordnungsfelder definieren. Beachten Sie, dass Sie nur Klassen und Feldergruppen verwenden können, um Felder zu Schemas hinzuzufügen. Weitere Informationen zum Verwalten dieser Ressourcen in der Benutzeroberfläche finden Sie in den Handbüchern zum Erstellen und Bearbeiten von [Klassen](../resources/classes.md) und [Feldergruppen](../resources/field-groups.md).

Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie in der Übersicht über den Arbeitsbereich [[!UICONTROL Schemas] ](../overview.md) .
