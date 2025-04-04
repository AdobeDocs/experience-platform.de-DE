---
keywords: Experience Platform;Startseite;beliebte Themen;UI;Benutzeroberfläche;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;erkunden;Klasse;Feldergruppe;Datentyp;Schema;
solution: Experience Platform
title: Erkunden von Schema-Ressourcen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie vorhandene Schemata, Klassen, Schemafeldgruppen und Datentypen in der Benutzeroberfläche von Experience Platform untersuchen.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Erkunden von Schema-Ressourcen in der Benutzeroberfläche

In Adobe Experience Platform werden alle Schema-Ressourcen des Experience-Datenmodells (XDM) im [!DNL Schema Library] gespeichert, einschließlich der von Adobe bereitgestellten Standardressourcen und der von Ihrem Unternehmen definierten benutzerdefinierten Ressourcen. In der Experience Platform-Benutzeroberfläche können Sie die Struktur und die Felder jedes vorhandenen Schemas, jeder vorhandenen Klasse, jeder vorhandenen Feldergruppe oder jedes vorhandenen Datentyps in der [!DNL Schema Library] anzeigen. Dies ist besonders bei der Planung und Vorbereitung der Datenaufnahme nützlich, da die Benutzeroberfläche Informationen zu den erwarteten Datentypen und Anwendungsfällen jedes Felds bereitstellt, das von diesen XDM-Ressourcen bereitgestellt wird.

In diesem Tutorial werden die Schritte zum Untersuchen vorhandener Schemata, Klassen, Feldergruppen und Datentypen in der Experience Platform-Benutzeroberfläche beschrieben.

## Suchen einer Schema-Ressource {#lookup}

Wählen Sie in der Benutzeroberfläche von Experience Platform **[!UICONTROL Schemas]** im linken Navigationsbereich aus. Der Arbeitsbereich [!UICONTROL Schemata] bietet eine Registerkarte **[!UICONTROL Durchsuchen]**, auf der alle Schemata in Ihrer Organisation untersucht werden können, sowie zusätzliche dedizierte Registerkarten zum Durchsuchen von **[!UICONTROL Klassen]**, **[!UICONTROL Feldergruppen]**, **[!UICONTROL Datentypen]** und **[!UICONTROL Beziehungen]**.

![Der Arbeitsbereich „Schemata“ mit mehreren hervorgehobenen Registerkarten.](../images/ui/explore/tabs.png)

Das Filtersymbol (![Filtersymbol Bild](/help/images/icons/filter.png)) zeigt Steuerelemente in der linken Leiste an, um die aufgelisteten Ergebnisse einzugrenzen. Ressourcenfilter sind für Schemata und Beziehungen auf den Registerkarten **[!UICONTROL Durchsuchen]** und **[!UICONTROL Beziehungen]** verfügbar.

Auf der Registerkarte [!UICONTROL Durchsuchen] des Arbeitsbereichs [!UICONTROL Schemata] können Sie Ihren Schemabestand filtern. Verwenden Sie den Umschalter **[!UICONTROL Im Profil enthalten]**, um nur Schemata anzuzeigen, die für die Verwendung im [Echtzeit-Kundenprofil“ aktiviert ](../../profile/home.md). Verwenden Sie den Umschalter **[!UICONTROL Ad-hoc-]** anzeigen“, um die Liste der Schemata zu filtern, die mit Feldern mit Namespace erstellt wurden und nur von einem einzigen Datensatz verwendet werden können.

![Die Registerkarte [!UICONTROL Schemata] im Arbeitsbereich [!UICONTROL Durchsuchen] mit hervorgehobenem Filterbedienfeld.](../images/ui/explore/filters.png)

Auf der Registerkarte [!UICONTROL Beziehung] des Arbeitsbereichs [!UICONTROL Schemata] können Sie die Liste der Beziehungen nach vier Kriterien filtern. Die Filter umfassen [!UICONTROL Source], [!UICONTROL Zielschema], [!UICONTROL Source-] und die [!UICONTROL Zielklasse]. Die nachstehende Tabelle enthält eine Beschreibung der Filter.

| Filter | Beschreibung |
|-----------------------------------|------------|
| [!UICONTROL Source-Schema] | Um alle Beziehungen anzuzeigen, bei denen das ausgewählte Schema der Startpunkt oder „Quellpfad“ ist, wählen Sie ein Schema aus dem Dropdown-Menü [!UICONTROL Source] aus. |
| [!UICONTROL Zielschema] | Um alle Beziehungen anzuzeigen, bei denen das ausgewählte Schema das Ziel oder „Ziel“ ist, wählen Sie ein Schema aus dem Dropdown-Menü [!UICONTROL Zielschema] aus. |
| [!UICONTROL Source-Klasse] | Um Beziehungen nach der Klasse des initiierenden Schemas zu filtern, wählen Sie eine Klasse aus dem Dropdown-Menü [!UICONTROL Source-Klasse] aus. |
| [!UICONTROL Zielklasse] | Um Beziehungen anzuzeigen, die auf Schemata einer bestimmten Klasse enden, wählen Sie eine Klasse aus dem Dropdown[!UICONTROL Menü &quot;]&quot;. |

{style="table-layout:auto"}

![Die Registerkarte „Beziehungen“ mit hervorgehobenem Filterabschnitt.](../images/ui/explore/relationships-filter.png)

Sie können die Suchleiste auch verwenden, um die Ergebnisse weiter einzugrenzen.

![Die Registerkarte „Durchsuchen“ des Arbeitsbereichs „Schemata“ mit hervorgehobenem Suchfeld.](../images/ui/explore/search.png)

Die in den Suchergebnissen angezeigten Ressourcen werden zuerst nach Übereinstimmungen mit dem Titel und dann nach der Beschreibung sortiert. Je mehr Wörter in einer dieser Kategorien übereinstimmen, desto höher wird die Ressource in der Liste angezeigt.

Wenn Sie die Ressource gefunden haben, die Sie untersuchen möchten, wählen Sie ihren Namen aus der Liste aus, um ihre Struktur auf der Arbeitsfläche anzuzeigen.

## Erkunden einer XDM-Ressource auf der Arbeitsfläche {#explore}

Wenn Sie eine Ressource auswählen, wird ihre Struktur auf der Arbeitsfläche geöffnet.

![Die Arbeitsfläche des Datentyp-Arbeitsbereichs mit dem Commerce-Datentyp.](../images/ui/explore/canvas.png)

Alle Felder vom Typ „Objekt“, die Untereigenschaften enthalten, werden standardmäßig reduziert, wenn sie zum ersten Mal auf der Arbeitsfläche erscheinen. Um die Untereigenschaften eines Felds anzuzeigen, klicken Sie auf das Symbol neben dem Namen des Felds.

![Die Arbeitsfläche des Datentyp-Arbeitsbereichs mit erweiterten Feldern und hervorgehobenen Untereigenschaften.](../images/ui/explore/field-expand.png)

### Indikator für Standardklasse und Feldergruppe {#standard-class-and-field-group-indicator}

Innerhalb des Schema-Editors werden Standardklassen (Adobe-generiert) und Feldergruppen mit dem Schlosssymbol (![Vorhängeschloss-Symbol) gekennzeichnet.](/help/images/icons/lock-closed.png). Das Vorhängeschloss wird in der linken Leiste neben dem Namen der Klasse oder Feldergruppe sowie neben einem beliebigen Feld im Schemadiagramm angezeigt, das Teil einer systemgenerierten Ressource ist.

![Der Schema-Editor mit hervorgehobenem Vorhängeschloss-Symbol](../images/ui/explore/schema-editor-padlock-icon.png)

Eine Anleitung [ Sie in der Dokumentation zum Hinzufügen benutzerdefinierter Felder ](./resources/schemas.md) Standardfeldgruppen . Eine Standardklasse kann nicht bearbeitet werden.

### Systemgenerierte Felder {#system-fields}

Einigen Feldnamen wird ein Unterstrich vorangestellt, z. B. `_repo` und `_id`. Diese stellen Platzhalter für Felder dar, die das System bei der Datenaufnahme automatisch generiert und zuweist.

Daher sollten die meisten dieser Felder bei der Aufnahme in Experience Platform aus der Datenstruktur ausgeschlossen werden. Die wichtigste Ausnahme von dieser Regel ist das [`_{TENANT_ID}` Feld](../api/getting-started.md#know-your-tenant_id) unter dem alle XDM-Felder, die unter Ihrer Organisation erstellt wurden, einen Namespace erhalten müssen.

### Datentypen {#data-types}

Für jedes auf der Arbeitsfläche angezeigte Feld wird der entsprechende Datentyp neben dem Namen angezeigt, was auf einen Blick den Datentyp angibt, den das Feld für die Aufnahme erwartet.

![Der auf der Arbeitsfläche angezeigte Datentyp „Postanschrift“ mit hervorgehobenen zugehörigen Datentypen.](../images/ui/explore/data-types.png)

Jeder Datentyp, der mit eckigen Klammern (`[]`) angehängt wird, stellt ein Array dieses bestimmten Datentyps dar. Beispielsweise gibt ein Datentyp von **[!UICONTROL String]\[]** an, dass das Feld ein Array von Zeichenfolgenwerten erwartet. Ein Datentyp von **[!UICONTROL Zahlungsposten]\[]** gibt ein Array von Objekten an, die dem Datentyp [!UICONTROL Zahlungsposten] entsprechen.

Wenn ein Array-Feld auf einem Objekttyp basiert, können Sie auf der Arbeitsfläche auf sein Symbol klicken, um die erwarteten Attribute für jedes Array-Element anzuzeigen.

![Ein Objekt auf der Arbeitsfläche mit einem hervorgehobenen Array-Feld und den für jedes Array-Element erwarteten Attributen.](../images/ui/explore/array-type.png)

### [!UICONTROL Feldeigenschaften] {#field-properties}

Wenn Sie den Namen eines Felds auf der Arbeitsfläche auswählen, wird die rechte Leiste aktualisiert, um Details zu diesem Feld unter „Feldeigenschaften **[!UICONTROL anzuzeigen]**. Dies kann eine Beschreibung des vorgesehenen Anwendungsfalls des Felds, Standardwerte, Muster, Formate, unabhängig davon, ob das Feld erforderlich ist oder nicht, und mehr umfassen.

![Ein aus dem Commerce-Datentyp ausgewähltes Feld mit hervorgehobenen Feldeigenschaften.](../images/ui/explore/field-properties.png)

Wenn es sich bei dem überprüften Feld um ein Aufzählungsfeld handelt, zeigt die rechte Leiste auch die akzeptablen Werte an, die das Feld erwartet.

![Der Schema-Editor mit einem ausgewählten Feld und den hervorgehobenen Aufzählungswerten und Anzeigenamen in der Leiste „Feldeigenschaften“.](../images/ui/explore/enum-field.png)

### Identitätsfelder {#identity}

Beim Überprüfen von Schemata, die Identitätsfelder enthalten, werden diese Felder in der linken Leiste unter der Klasse oder Feldergruppe aufgeführt, die sie für das Schema bereitstellt. Wählen Sie den Namen des Identitätsfelds in der linken Leiste aus, um das Feld auf der Arbeitsfläche anzuzeigen, unabhängig davon, wie tief es verschachtelt ist.

Identitätsfelder werden auf der Arbeitsfläche mit einem Fingerabdrucksymbol (![Fingerabdrucksymbol) ](/help/images/icons/identity-service.png). Wenn Sie den Namen des Identitätsfelds auswählen, können Sie zusätzliche Informationen anzeigen, z. B. den [Identity-Namespace](../../identity-service/features/namespaces.md) und ob das Feld die primäre Identität für das Schema ist oder nicht.

![Der Schema-Editor mit der hervorgehobenen Identität des Schemas in der linken Leiste, dem hervorgehobenen Feld im Schemadiagramm und dem hervorgehobenen Identity-Namespace in den Feldeigenschaften.](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Weitere Informationen zu Identitätsfeldern und [ Beziehung zu nachgelagerten Experience Platform](./fields/identity.md)Services finden Sie im Handbuch unter „Definieren von Identitätsfeldern“.

### Beziehungsfelder {#relationship}

Wenn Sie ein Schema überprüfen, das ein Beziehungsfeld enthält, wird das Feld in der linken Leiste unter &quot;**[!UICONTROL &quot;]**. Wählen Sie den Namen des Beziehungsfelds in der linken Leiste aus, um das Feld auf der Arbeitsfläche anzuzeigen, unabhängig davon, wie tief es verschachtelt ist. Beziehungsfelder werden auch auf der Arbeitsfläche eindeutig hervorgehoben, sodass der Name des Referenzschemas angezeigt wird, auf das das Feld verweist. Für Organisationen mit B2B-Funktionen können benutzerdefinierte Beziehungsnamen geschrieben werden, die in diesen Fällen auf der Arbeitsfläche angezeigt werden.

![Der Schema-Editor mit dem hervorgehobenen Beziehungsfeld und der hervorgehobenen Option „Beziehung bearbeiten“](../images/ui/explore/relationship-field.png)

Um den Identity-Namespace der primären Identität des Referenzschemas anzuzeigen, wählen Sie das Beziehungsfeld und dann **[!UICONTROL Beziehung bearbeiten]** in der Seitenleiste [!UICONTROL Feldeigenschaften] aus. Die Parameter für die Beziehung werden im Dialogfeld [!UICONTROL Beziehung bearbeiten] angezeigt.

![Das Dialogfeld „Beziehung bearbeiten“ mit den angezeigten Beziehungsparametern.](../images/ui/explore/edit-relationship-dialog.png)

Weitere Informationen zur Verwendung von [ in XDM-Schemata finden Sie ](../tutorials/relationship-ui.md) Tutorial zum Erstellen einer Beziehung in der Benutzeroberfläche .

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie vorhandene XDM-Ressourcen in der Experience Platform-Benutzeroberfläche erkunden. Weitere Informationen zu den verschiedenen Funktionen des Arbeitsbereichs [!UICONTROL Schemata] und der [!DNL Schema Editor] finden Sie in der Übersicht über den Arbeitsbereich [[!UICONTROL Schemata]Übersicht](./overview.md).
