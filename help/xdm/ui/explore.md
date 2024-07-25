---
keywords: Experience Platform; home; beliebte Themen; ui; UI; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; erkunden; Klasse; Feldergruppe; Datentyp; Schema
solution: Experience Platform
title: Schema-Ressourcen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie vorhandene Schemas, Klassen, Schemafeldgruppen und Datentypen in der Experience Platform-Benutzeroberfläche untersuchen.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---

# Schema-Ressourcen in der Benutzeroberfläche

In Adobe Experience Platform werden alle Schemaressourcen des Experience-Datenmodells (XDM) im Ordner &quot;[!DNL Schema Library]&quot;gespeichert, einschließlich der von der Adobe bereitgestellten Standardressourcen und der von Ihrem Unternehmen definierten benutzerdefinierten Ressourcen. Auf der Experience Platform-Benutzeroberfläche können Sie die Struktur und die Felder eines vorhandenen Schemas, einer vorhandenen Klasse, einer Feldgruppe oder eines vorhandenen Datentyps im [!DNL Schema Library] anzeigen. Dies ist besonders nützlich bei der Planung und Vorbereitung der Datenerfassung, da die Benutzeroberfläche Informationen zu den erwarteten Datentypen und Anwendungsfällen der einzelnen Felder bereitstellt, die von diesen XDM-Ressourcen bereitgestellt werden.

In diesem Tutorial werden die Schritte zum Erkunden vorhandener Schemas, Klassen, Feldergruppen und Datentypen in der Experience Platform-Benutzeroberfläche beschrieben.

## Nach einer Schemaressource suchen {#lookup}

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Schemas]** aus. Der Arbeitsbereich [!UICONTROL Schemas] enthält eine Registerkarte **[!UICONTROL Durchsuchen]** , auf der alle Schemas in Ihrer Organisation durchsucht werden können. Außerdem stehen zusätzliche spezielle Registerkarten zum Erkunden der **[!UICONTROL Klassen]**, **[!UICONTROL Feldergruppen]** und **[!UICONTROL Datentypen]** zur Verfügung.

![](../images/ui/explore/tabs.png)

Das Filtersymbol (![Filtersymbol Bild](/help/images/icons/filter.png)) zeigt Steuerelemente in der linken Leiste an, um die aufgelisteten Ergebnisse einzuschränken. Die angezeigten Steuerelemente variieren je nach Ressourcentyp.

Um beispielsweise die Liste so zu filtern, dass nur die von Adobe bereitgestellten Standarddatentypen angezeigt werden, wählen Sie **[!UICONTROL Datentyp]** und **[!UICONTROL Adobe]** unter den Abschnitten **[!UICONTROL Typ]** und **[!UICONTROL Inhaber]** aus.

Mit dem Umschalter **[!UICONTROL Im Profil enthalten]** können Sie Ergebnisse filtern, um nur Ressourcen anzuzeigen, die in Schemas verwendet werden, die für die Verwendung im [Echtzeit-Kundenprofil](../../profile/home.md) aktiviert wurden. Mit dem Umschalter **[!UICONTROL Ad-hoc-Schemata anzeigen]** wird die Liste der Schemas gefiltert, die mit Feldern erstellt wurden, die nur für die Verwendung durch einen einzigen Datensatz benannt wurden.

![Die Registerkarte [!UICONTROL Schemas] Arbeitsbereich [!UICONTROL Durchsuchen] mit hervorgehobenem Filterbereich.](../images/ui/explore/filter.png)

Wenn Sie Ressourcen auf den Registerkarten **[!UICONTROL Klassen]**, **[!UICONTROL Feldergruppen]** oder **[!UICONTROL Datentypen]** auflisten, können Sie **[!UICONTROL Adobe]** auswählen, um nur Standardressourcen anzuzeigen, oder **[!UICONTROL Kunde]**, um nur die von Ihrem Unternehmen erstellten Ressourcen anzuzeigen.

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

### Standardklasse- und Feldergruppenanzeige {#standard-class-and-field-group-indicator}

Im Schema Editor werden Standardklassen (Adobe-generierte) und Feldgruppen mit dem Vorhängeschloss-Symbol (![Vorhängeschlosssymbol) angezeigt.](/help/images/icons/lock-closed.png). Das Vorhängeschloss wird in der linken Leiste neben dem Namen der Klasse oder Feldergruppe sowie neben jedem Feld im Schemadiagramm angezeigt, das Teil einer systemgenerierten Ressource ist.

![Der Schema-Editor mit dem Vorhängeschloss-Symbol hervorgehoben](../images/ui/explore/schema-editor-padlock-icon.png)

Eine Anleitung finden Sie in der Dokumentation [Hinzufügen benutzerdefinierter Felder zu Standardfeldgruppen](./resources/schemas.md) . Eine Standardklasse kann nicht bearbeitet werden.

### Systemgenerierte Felder {#system-fields}

Einige Feldnamen erhalten einen Unterstrich, z. B. `_repo` und `_id`. Diese stellen Platzhalter für Felder dar, die das System automatisch generiert und zuweist, wenn Daten erfasst werden.

Daher sollten die meisten dieser Felder bei der Aufnahme in Platform aus der Datenstruktur ausgeschlossen werden. Die Hauptausnahme dieser Regel ist das [`_{TENANT_ID}` -Feld](../api/getting-started.md#know-your-tenant_id), in dem alle unter Ihrem Unternehmen erstellten XDM-Felder im Namespace angegeben werden müssen.

### Datentypen {#data-types}

Für jedes auf der Arbeitsfläche angezeigte Feld wird der zugehörige Datentyp neben dem Namen angezeigt, der auf einen Blick den Datentyp angibt, den das Feld für die Aufnahme erwartet.

![](../images/ui/explore/data-types.png)

Jeder Datentyp, der mit eckigen Klammern (`[]`) angehängt wird, stellt ein Array dieses bestimmten Datentyps dar. Beispielsweise zeigt der Datentyp **[!UICONTROL String]\[]** an, dass das Feld ein Array von Zeichenfolgenwerten erwartet. Der Datentyp **[!UICONTROL Zahlungselement]\[]** gibt ein Array von Objekten an, die dem Datentyp [!UICONTROL Zahlungselement] entsprechen.

Wenn ein Array-Feld auf einem Objekttyp basiert, können Sie das zugehörige Symbol auf der Arbeitsfläche auswählen, um die erwarteten Attribute für jedes Array-Element anzuzeigen.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Feldeigenschaften] {#field-properties}

Wenn Sie den Namen eines Felds auf der Arbeitsfläche auswählen, wird die rechte Leiste aktualisiert, um Details zu diesem Feld unter **[!UICONTROL Feldeigenschaften]** anzuzeigen. Dies kann eine Beschreibung des Verwendungsfalls des Felds, Standardwerte, Muster, Formate, unabhängig davon, ob das Feld erforderlich ist oder nicht, und mehr enthalten.

![](../images/ui/explore/field-properties.png)

Wenn es sich bei dem zu prüfenden Feld um ein Enum-Feld handelt, zeigt die rechte Leiste auch die akzeptablen Werte an, die das Feld erwartet.

![](../images/ui/explore/enum-field.png)

### Identitätsfelder {#identity}

Beim Prüfen von Schemas, die Identitätsfelder enthalten, werden diese Felder in der linken Leiste unter der Klasse oder Feldergruppe aufgelistet, die sie für das Schema bereitstellt. Wählen Sie in der linken Leiste den Namen des Identitätsfelds aus, um das Feld auf der Arbeitsfläche anzuzeigen, unabhängig davon, wie tief es verschachtelt ist.

Identitätsfelder werden auf der Arbeitsfläche mit einem Fingerabdrucksymbol (![Fingerabdruck-Symbol Bild](/help/images/icons/identity-service.png)) hervorgehoben. Wenn Sie den Namen des Identitätsfelds auswählen, können Sie zusätzliche Informationen wie den [Identitäts-Namespace](../../identity-service/features/namespaces.md) anzeigen und feststellen, ob das Feld die primäre Identität für das Schema ist.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Weiterführende Informationen zu Identitätsfeldern und deren Beziehung zu nachgelagerten Platform-Diensten finden Sie im Handbuch zu [Identitätsfeldern definieren](./fields/identity.md) .

### Beziehungsfelder {#relationship}

Wenn Sie ein Schema überprüfen, das ein Beziehungsfeld enthält, wird das Feld in der linken Leiste unter **[!UICONTROL Beziehungen]** aufgelistet. Wählen Sie in der linken Leiste den Namen des Beziehungsfelds aus, um das Feld auf der Arbeitsfläche anzuzeigen, unabhängig davon, wie tief es verschachtelt ist.

Die Beziehungsfelder werden auch auf der Arbeitsfläche eindeutig hervorgehoben und zeigen den Namen des Referenzschemas an, mit dem das Feld verknüpft ist. Wenn Sie den Namen des Beziehungsfelds auswählen, können Sie den Identitäts-Namespace der primären Identität des Referenzschemas in der rechten Leiste anzeigen.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Weitere Informationen zur Verwendung von Beziehungen in XDM-Schemas finden Sie im Tutorial zum Erstellen einer Beziehung in der Benutzeroberfläche [.](../tutorials/relationship-ui.md)

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie vorhandene XDM-Ressourcen in der Experience Platform-Benutzeroberfläche untersuchen. Weitere Informationen zu den verschiedenen Funktionen des Arbeitsbereichs [!UICONTROL Schemas] und des Arbeitsbereichs [!DNL Schema Editor] finden Sie in der Arbeitsbereichsübersicht [[!UICONTROL Schemas]](./overview.md).
