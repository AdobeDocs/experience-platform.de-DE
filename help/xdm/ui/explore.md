---
keywords: Experience Platform; Startseite; beliebte Themen; UI; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; erkunden; Klasse; Feldergruppe; Datentyp; Schema
solution: Experience Platform
title: Schema-Ressourcen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie vorhandene Schemas, Klassen, Schemafeldgruppen und Datentypen in der Experience Platform-Benutzeroberfläche untersuchen.
topic-legacy: tutorial
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 744d87c82b7e7e06782c6c1b9db2ec46a5444d28
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# Schema-Ressourcen in der Benutzeroberfläche

In Adobe Experience Platform werden alle Schemaressourcen des Experience-Datenmodells (XDM) im [!DNL Schema Library], einschließlich der Standardressourcen, die von der Adobe bereitgestellt werden, und der benutzerdefinierten Ressourcen, die von Ihrem Unternehmen definiert werden. In der Experience Platform-Benutzeroberfläche können Sie die Struktur und die Felder eines vorhandenen Schemas, einer vorhandenen Klasse, einer vorhandenen Feldergruppe oder eines vorhandenen Datentyps im [!DNL Schema Library]. Dies ist besonders nützlich bei der Planung und Vorbereitung der Datenerfassung, da die Benutzeroberfläche Informationen zu den erwarteten Datentypen und Anwendungsfällen der einzelnen Felder bereitstellt, die von diesen XDM-Ressourcen bereitgestellt werden.

In diesem Tutorial werden die Schritte zum Erkunden vorhandener Schemas, Klassen, Feldgruppen und Datentypen in der Experience Platform-Benutzeroberfläche beschrieben.

## Nach einer Schemaressource suchen {#lookup}

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Schemas]** in der linken Navigation. Die [!UICONTROL Schemas] Workspace bietet eine **[!UICONTROL Durchsuchen]** Registerkarte, um alle Schemas in Ihrer Organisation zu untersuchen, sowie zusätzliche spezielle Registerkarten zum Erkunden **[!UICONTROL Klassen]**, **[!UICONTROL Feldergruppen]** und **[!UICONTROL Datentypen]** bzw.

![](../images/ui/explore/tabs.png)

Das Filtersymbol (![Filtersymbol Bild](../images/ui/explore/icon.png)) zeigt Steuerelemente in der linken Leiste an, um die aufgelisteten Ergebnisse einzuschränken. Die angezeigten Steuerelemente variieren je nach Ressourcentyp.

Um beispielsweise die Liste so zu filtern, dass nur die von Adobe bereitgestellten Standarddatentypen angezeigt werden, wählen Sie **[!UICONTROL Datentyp]** und **[!UICONTROL Adobe]** unter **[!UICONTROL Typ]** und **[!UICONTROL Inhaber]** angegeben.

Die **[!UICONTROL Im Profil enthalten]** Mit Umschalten können Sie Ergebnisse filtern, sodass nur Ressourcen angezeigt werden, die in Schemas verwendet werden, die für die Verwendung in [Echtzeit-Kundenprofil](../../profile/home.md).

![](../images/ui/explore/filter.png)

Beim Auflisten von Ressourcen auf der **[!UICONTROL Klassen]**, **[!UICONTROL Feldergruppen]** oder **[!UICONTROL Datentypen]** Registerkarten, können Sie **[!UICONTROL Adobe]** nur Standardressourcen anzeigen oder **[!UICONTROL Kunde]** , um nur die von Ihrer Organisation erstellten Ressourcen anzuzeigen.

![](../images/ui/explore/filter-data-type.png)

Sie können die Suchleiste auch verwenden, um die Ergebnisse weiter einzugrenzen.

![](../images/ui/explore/search.png)

Die in den Suchergebnissen angezeigten Ressourcen werden zuerst nach Titel und dann nach Beschreibung geordnet. Je mehr Wörter in einer dieser Kategorien übereinstimmen, desto höher wird die Ressource in der Liste angezeigt.

Wenn Sie die Ressource gefunden haben, die Sie untersuchen möchten, wählen Sie deren Namen aus der Liste aus, um ihre Struktur auf der Arbeitsfläche anzuzeigen.

## XDM-Ressource auf der Arbeitsfläche durchsuchen {#explore}

Nachdem Sie eine Ressource ausgewählt haben, wird ihre Struktur auf der Arbeitsfläche geöffnet.

![](../images/ui/explore/canvas.png)

Alle Objekttypen, die Untereigenschaften enthalten, werden standardmäßig ausgeblendet, wenn sie zum ersten Mal auf der Arbeitsfläche angezeigt werden. Um die Untereigenschaften eines beliebigen Felds anzuzeigen, wählen Sie das Symbol neben seinem Namen aus.

![](../images/ui/explore/field-expand.png)

### Systemgenerierte Felder {#system-fields}

Bei einigen Feldnamen wird ein Unterstrich vorangestellt, z. B. `_repo` und `_id`. Diese stellen Platzhalter für Felder dar, die das System automatisch generiert und zuweist, wenn Daten erfasst werden.

Daher sollten die meisten dieser Felder bei der Aufnahme in Platform aus der Datenstruktur ausgeschlossen werden. Die wichtigste Ausnahme für diese Regel ist die [`_{TENANT_ID}` field](../api/getting-started.md#know-your-tenant_id), unter dem alle unter Ihrem Unternehmen erstellten XDM-Felder im Namespace angegeben werden müssen.

### Datentypen {#data-types}

Für jedes auf der Arbeitsfläche angezeigte Feld wird der zugehörige Datentyp neben dem Namen angezeigt, der auf einen Blick den Datentyp angibt, den das Feld für die Aufnahme erwartet.

![](../images/ui/explore/data-types.png)

Jeder Datentyp, der mit eckigen Klammern (`[]`) stellt ein Array dieses bestimmten Datentyps dar. Beispielsweise kann ein Datentyp **[!UICONTROL Zeichenfolge]\[]** gibt an, dass das Feld ein Array von Zeichenfolgenwerten erwartet. Ein Datentyp von **[!UICONTROL Zahlungselement]\[]** gibt ein Array von Objekten an, die dem [!UICONTROL Zahlungselement] Datentyp.

Wenn ein Array-Feld auf einem Objekttyp basiert, können Sie das zugehörige Symbol auf der Arbeitsfläche auswählen, um die erwarteten Attribute für jedes Array-Element anzuzeigen.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Feldeigenschaften] {#field-properties}

Wenn Sie den Namen eines Felds auf der Arbeitsfläche auswählen, wird die rechte Leiste aktualisiert und zeigt Details zu diesem Feld unter **[!UICONTROL Feldeigenschaften]**. Dies kann eine Beschreibung des Verwendungsfalls des Felds, Standardwerte, Muster, Formate, unabhängig davon, ob das Feld erforderlich ist oder nicht, und mehr enthalten.

![](../images/ui/explore/field-properties.png)

Wenn es sich bei dem zu prüfenden Feld um ein Enum-Feld handelt, zeigt die rechte Leiste auch die akzeptablen Werte an, die das Feld erwartet.

![](../images/ui/explore/enum-field.png)

### Identitätsfelder {#identity}

Beim Prüfen von Schemas, die Identitätsfelder enthalten, werden diese Felder in der linken Leiste unter der Klasse oder Feldergruppe aufgelistet, die sie für das Schema bereitstellt. Wählen Sie in der linken Leiste den Namen des Identitätsfelds aus, um das Feld auf der Arbeitsfläche anzuzeigen, unabhängig davon, wie tief es verschachtelt ist.

Identitätsfelder werden auf der Arbeitsfläche mit einem Fingerabdrucksymbol (![Fingerabdrucksymbol Bild](../images/ui/explore/identity-symbol.png)). Wenn Sie den Namen des Identitätsfelds auswählen, können Sie zusätzliche Informationen anzeigen, z. B. die [Identitäts-Namespace](../../identity-service/namespaces.md) und ob das Feld die primäre Identität für das Schema ist.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Siehe Handbuch unter [Identitätsfelder definieren](./fields/identity.md) für weitere Informationen zu Identitätsfeldern und deren Beziehung zu nachgelagerten Platform-Diensten.

### Beziehungsfelder {#relationship}

Wenn Sie ein Schema überprüfen, das ein Beziehungsfeld enthält, wird das Feld in der linken Leiste unter **[!UICONTROL Beziehungen]**. Wählen Sie in der linken Leiste den Namen des Beziehungsfelds aus, um das Feld auf der Arbeitsfläche anzuzeigen, unabhängig davon, wie tief es verschachtelt ist.

Die Beziehungsfelder werden auch auf der Arbeitsfläche eindeutig hervorgehoben und zeigen den Namen des Zielschemas an, auf das das Feld verweist. Wenn Sie den Namen des Beziehungsfelds auswählen, können Sie den Identitäts-Namespace der primären Identität des Zielschemas in der rechten Leiste anzeigen.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Siehe Tutorial zu [Erstellen einer Beziehung in der Benutzeroberfläche](../tutorials/relationship-ui.md) für weitere Informationen zur Verwendung von Beziehungen in XDM-Schemas.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie vorhandene XDM-Ressourcen in der Experience Platform-Benutzeroberfläche untersuchen. Weitere Informationen zu den verschiedenen Funktionen der [!UICONTROL Schemas] Arbeitsbereich und [!DNL Schema Editor], siehe [[!UICONTROL Schemas] Arbeitsbereich - Übersicht](./overview.md).
