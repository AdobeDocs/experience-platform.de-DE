---
title: Definieren von Zuordnungsfeldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Experience Platform ein Zuordnungsfeld definieren.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Definieren von Zuordnungsfeldern in der Benutzeroberfläche

Mit Adobe Experience Platform können Sie die Struktur Ihrer benutzerdefinierten Experience-Datenmodell (XDM)-Klassen, Schemafeldgruppen und Datentypen vollständig anpassen.

Sie können im Schema-Editor auch Zuordnungsfelder definieren, um flexible und dynamische Datenstrukturen zu modellieren oder eine Sammlung von Schlüssel-Wert-Paaren zu speichern.

Verwenden Sie beim Definieren eines neuen Felds in der Experience Platform-Benutzeroberfläche das Dropdown-Menü **[!UICONTROL Typ]** und wählen Sie &quot;**[!UICONTROL Zuordnung]** aus der Liste aus.

![Der Schemaeditor mit Hervorhebung der Dropdown-Liste „Typ“ und des Zuordnungswerts.](../../images/ui/fields/special/map.png)

Eine [!UICONTROL Map-Werttyp]-Eigenschaft wird angezeigt. Dieser Wert ist für [!UICONTROL Map]-Datentypen erforderlich. Verfügbare Werte für die Zuordnung sind [!UICONTROL Zeichenfolge] und [!UICONTROL Ganzzahl]. Wählen Sie einen Wert aus der Dropdown-Liste der verfügbaren Optionen aus.

![Der Schema-Editor mit hervorgehobenem [!UICONTROL Zuordnungs-Werttyp]-Dropdown.](../../images/ui/fields/special/map-value-type.png)

Nachdem Sie das Unterfeld konfiguriert haben, müssen Sie es einer Feldergruppe zuweisen. Verwenden Sie das **[!UICONTROL Feldergruppe]** Dropdown-Menü oder Suchfeld und wählen Sie **[!UICONTROL Anwenden]**. Sie können dem Objekt weiterhin Felder im selben Prozess hinzufügen oder auf **[!UICONTROL Speichern]** klicken, um Ihre Einstellungen zu bestätigen.

![Eine Aufzeichnung der Feldergruppenauswahl und der angewendeten Einstellungen.](../../images/ui/fields/special/assign-to-field-group.gif)

## Nutzungsbeschränkungen {#restrictions}

XDM setzt die folgenden Einschränkungen für die Verwendung dieses Datentyps:

* Zuordnungstypen MÜSSEN vom Typ `object` sein.
* Für Zuordnungstypen DÜRFEN KEINE Eigenschaften definiert sein (d. h. sie definieren „leere“ Objekte).
* Zuordnungstypen MÜSSEN ein `additionalProperties.type` enthalten, das die Werte beschreibt, die innerhalb der Zuordnung platziert werden können, entweder `string` oder `integer`.
* Die Segmentierung mehrerer Entitäten kann nur anhand der Zuordnungsschlüssel und nicht anhand der Werte definiert werden.
* Zuordnungen werden für Konto-Zielgruppen nicht unterstützt.

Stellen Sie sicher, dass Sie Felder vom Typ Zuordnung nur verwenden, wenn dies unbedingt erforderlich ist, da sie die folgenden Leistungseinbußen aufweisen:

* Die Reaktionszeit von [Adobe Experience Platform Query Service](../../../query-service/home.md) wird für 100 Millionen Datensätze von drei auf zehn Sekunden reduziert.
* Die Karten müssen weniger als 16 Schlüssel haben, da sonst eine weitere Beeinträchtigung droht.

>[!NOTE]
>
>Die Experience Platform-Benutzeroberfläche verfügt über Einschränkungen beim Extrahieren der Schlüssel von Feldern vom Typ Zuordnung . Während sich Felder vom Typ „Objekt“ erweitern lassen, werden Zuordnungen stattdessen als einzelnes Feld angezeigt. Zuordnungsfelder, die über die Schema Registry-API erstellt wurden und keine String- oder Integer-Datentypen sind, werden als &quot;[!UICONTROL &quot; &#x200B;].

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie jetzt Zuordnungsfelder in der Experience Platform-Benutzeroberfläche definieren. Denken Sie daran, dass Sie nur Klassen und Feldergruppen verwenden können, um Felder zu Schemata hinzuzufügen. Weitere Informationen zum Verwalten dieser Ressourcen in der Benutzeroberfläche finden Sie in den Handbüchern zum Erstellen und Bearbeiten [Klassen](../resources/classes.md) und [Feldergruppen](../resources/field-groups.md).

Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemata] finden Sie unter [[!UICONTROL Schemata] Arbeitsbereich - Übersicht](../overview.md).
