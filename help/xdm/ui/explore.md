---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;explore;class;mixin;data type;schema;
solution: Experience Platform
title: XDM-Ressourcen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie vorhandene Schema, Klassen, Mixins und Datentypen in der Benutzeroberfläche der Experience Platform untersuchen.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: e5c5fea783aa4088d225f771905fa8b2098613cf
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# XDM-Ressourcen in der Benutzeroberfläche

In Adobe Experience Platform werden alle XDM-Ressourcen (Experience Data Model) im Ordner [!DNL Schema Library] gespeichert, einschließlich Standardressourcen, die durch Adoben und benutzerdefinierte Ressourcen bereitgestellt werden, die von Ihrem Unternehmen definiert werden. In der Benutzeroberfläche &quot;Experience Platform&quot;können Sie die Struktur und die Felder eines vorhandenen Schemas, einer vorhandenen Klasse, eines Mixins oder eines Datentyps im [!DNL Schema Library] Ansicht werden. Dies ist besonders bei der Planung und Vorbereitung der Datenerfassung nützlich, da die Benutzeroberfläche Informationen zu den erwarteten Datentypen und Anwendungsfällen der einzelnen Felder bereitstellt, die von diesen XDM-Ressourcen bereitgestellt werden.

Dieses Lernprogramm beschreibt die Schritte zum Erforschen vorhandener Schema, Klassen, Mixins und Datentypen in der Benutzeroberfläche der Experience Platform.

## Suchen Sie eine XDM-Ressource {#lookup}

Wählen Sie in der Benutzeroberfläche &quot;Plattform&quot;im linken Navigationsbereich **[!UICONTROL Schema]** aus. Der Arbeitsbereich [!UICONTROL Schemas] enthält die Registerkarte **[!UICONTROL Durchsuchen]**, um alle vorhandenen XDM-Ressourcen in Ihrem Unternehmen zu untersuchen, sowie weitere dedizierte Registerkarten zum Erforschen der **[!UICONTROL Klassen]**, **[!UICONTROL Mixins]** und **[!UICONTROL Datentypen]** speziell.

![](../images/ui/explore/tabs.png)

Auf der Registerkarte [!UICONTROL Durchsuchen] können Sie das Filtersymbol (![Filtersymbol Bild](../images/ui/explore/icon.png)) verwenden, um Steuerelemente in der linken Leiste anzuzeigen, um die aufgelisteten Ergebnisse einzuschränken.

Um beispielsweise die Liste so zu filtern, dass nur die von der Adobe bereitgestellten Standarddatentypen angezeigt werden, wählen Sie **[!UICONTROL Datentyp]** bzw. **[!UICONTROL Adobe]** unter den Abschnitten **[!UICONTROL Typ]** bzw. **[!UICONTROL Inhaber]** aus.

Mit dem Umschalter **[!UICONTROL In Profil]** eingeschlossen können Sie die Ergebnisse filtern, um nur die Ressourcen anzuzeigen, die in Schemas verwendet werden, die für die Verwendung in [Kundenkonto in Echtzeit](../../profile/home.md) aktiviert wurden.

![](../images/ui/explore/filter.png)

Sie können die Suchleiste auch verwenden, um die Ergebnisse auf Ressourcen zu beschränken, deren Namen mit der Abfrage übereinstimmen.

![](../images/ui/explore/search.png)

Wenn Sie die Ressource gefunden haben, die Sie untersuchen möchten, wählen Sie deren Namen aus der Liste aus, um die Struktur auf der Arbeitsfläche Ansicht.

## XDM-Ressource auf der Arbeitsfläche {#explore}

Nachdem Sie eine Ressource ausgewählt haben, wird ihre Struktur in der Arbeitsfläche geöffnet.

![](../images/ui/explore/canvas.png)

Alle Objekttypfelder, die Untereigenschaften enthalten, werden standardmäßig ausgeblendet, wenn sie zum ersten Mal auf der Arbeitsfläche angezeigt werden. Um die Untereigenschaften eines Felds anzuzeigen, wählen Sie das Symbol neben dem Namen aus.

![](../images/ui/explore/field-expand.png)

### Systemgenerierte Felder {#system-fields}

Einige Feldnamen werden mit einem Unterstrich versehen, z. B. `_repo` und `_id`. Diese stellen Platzhalter für Felder dar, die das System automatisch generiert und zuweist, wenn Daten erfasst werden.

Daher sollten die meisten dieser Felder bei der Eingabe in die Plattform aus der Datenstruktur ausgeschlossen werden. Die Hauptausnahme dieser Regel ist das Feld [`_{TENANT_ID}`](../api/getting-started.md#know-your-tenant_id), unter dem alle XDM-Felder, die unter Ihrem Unternehmen erstellt wurden, benannt werden müssen.

### Datentypen {#data-types}

Für jedes auf der Arbeitsfläche angezeigte Feld wird der zugehörige Datentyp neben dem Namen angezeigt, der auf einen Blick den Datentyp angibt, den das Feld für die Erfassung erwartet.

![](../images/ui/explore/data-types.png)

Jeder Datentyp, der mit eckigen Klammern (`[]`) angehängt wird, stellt ein Array dieses bestimmten Datentyps dar. Ein Datentyp von **[!UICONTROL String]\[]** gibt beispielsweise an, dass das Feld ein Array von Zeichenfolgenwerten erwartet. Ein Datentyp von **[!UICONTROL Zahlungselement]\[]** gibt ein Array von Objekten an, die dem Datentyp [!UICONTROL Zahlungselement] entsprechen.

Wenn ein Array-Feld auf einem Objekttyp basiert, können Sie das zugehörige Symbol auf der Arbeitsfläche auswählen, um die erwarteten Attribute für jedes Array-Element anzuzeigen.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Feldeigenschaften] {#field-properties}

Wenn Sie den Namen eines Felds auf der Arbeitsfläche auswählen, wird die rechte Leiste aktualisiert, um Details zu diesem Feld unter **[!UICONTROL Feldeigenschaften]** anzuzeigen. Dies kann eine Beschreibung der Verwendungsart des Felds, Standardwerte, Muster, Formate, unabhängig davon, ob das Feld erforderlich ist oder nicht, usw. umfassen.

![](../images/ui/explore/field-properties.png)

Wenn das geprüfte Feld ein Enum-Feld ist, zeigt die rechte Leiste auch die akzeptablen Werte an, die das Feld erwartet.

![](../images/ui/explore/enum-field.png)

### Identitätsfelder {#identity}

Beim Prüfen von Schemas, die Identitätsfelder enthalten, werden diese Felder in der linken Leiste unter der Klasse oder dem Mixin aufgelistet, die bzw. das sie dem Schema bereitstellt. Wählen Sie in der linken Leiste den Namen des Identitätsfeldes aus, um das Feld auf der Arbeitsfläche unabhängig davon anzuzeigen, wie tief es verschachtelt ist.

Identitätsfelder werden auf der Arbeitsfläche mit einem Fingerabdrucksymbol (![Fingerabdrucksymbol Bild](../images/ui/explore/identity-symbol.png)) markiert. Wenn Sie den Namen des Identitätsfelds auswählen, können Sie zusätzliche Informationen wie den [Identitätsname](../../identity-service/namespaces.md) und ob das Namensraum die primäre Identität für das Schema ist oder nicht, Ansicht vornehmen.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Weitere Informationen zu Identitätsfeldern und deren Beziehung zu den nachgeschalteten Plattformdiensten finden Sie im Handbuch [Identitätsfelder definieren](./fields/identity.md).

### Beziehungsfelder {#relationship}

Wenn Sie ein Schema überprüfen, das ein Beziehungsfeld enthält, wird das Feld in der linken Leiste unter **[!UICONTROL Beziehungen]** aufgeführt. Wählen Sie in der linken Leiste den Namen des Beziehungsfelds aus, um das Feld auf der Arbeitsfläche anzuzeigen, unabhängig davon, wie tief es verschachtelt ist.

Die Beziehungsfelder werden auch auf der Arbeitsfläche eindeutig hervorgehoben und zeigen den Namen des Schemas an, auf das das Feld verweist. Wenn Sie den Namen des Beziehungsfelds auswählen, können Sie den Identitäts-Namensraum der primären Identität des Schemas in der rechten Leiste Ansicht werden.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Weitere Informationen zur Verwendung von Beziehungen in XDM-Schemas finden Sie im Tutorial zu [Erstellen einer Beziehung in der Benutzeroberfläche](../tutorials/create-schema-ui.md).

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie vorhandene XDM-Ressourcen in der Benutzeroberfläche der Experience Platform untersuchen. Weitere Informationen zu den verschiedenen Funktionen des Arbeitsbereichs [!UICONTROL Schema] und [!DNL Schema Editor] finden Sie unter [[!UICONTROL Schema] Arbeitsbereichsübersicht](./overview.md).