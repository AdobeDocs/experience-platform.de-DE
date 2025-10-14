---
title: Feldbasierte Workflows im Schema-Editor
description: Erfahren Sie, wie Sie Felder aus vorhandenen Feldergruppen einzeln zu Ihren Experience-Datenmodell(XDM)-Schemata hinzufügen.
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# Feldbasierte Workflows im Schema-Editor

Adobe Experience Platform bietet einen robusten Satz standardisierter [Feldergruppen](../schema/composition.md#field-group) zur Verwendung in Experience-Datenmodell(XDM)-Schemata. Die Struktur und Semantik hinter diesen Feldergruppen sind sorgfältig darauf zugeschnitten, eine Vielzahl von Segmentierungsanwendungsfällen und andere nachgelagerte Anwendungen in Experience Platform zu erfüllen. Sie können auch eigene benutzerdefinierte Feldergruppen definieren, um individuelle Geschäftsanforderungen zu erfüllen.

Wenn Sie eine Feldergruppe zu einem Schema hinzufügen, übernimmt dieses Schema alle in dieser Gruppe enthaltenen Felder. Sie können jetzt jedoch einzelne Felder zu Ihrem Schema hinzufügen, ohne andere Felder aus der zugehörigen Feldergruppe einbeziehen zu müssen, die Sie nicht unbedingt verwenden müssen.

In diesem Handbuch werden die verschiedenen Methoden zum Hinzufügen einzelner Felder zu einem Schema in der Experience Platform-Benutzeroberfläche behandelt.

## Voraussetzungen

In diesem Tutorial wird davon ausgegangen, dass Sie mit der [Komposition von XDM-Schemas](../schema/composition.md) und der Verwendung des Schema-Editors in der Experience Platform-Benutzeroberfläche vertraut sind. Um diesem Schritt zu folgen, sollten Sie mit dem [Erstellen eines neuen Schemas](./resources/schemas.md) und dem Zuweisen zu einer Standardklasse beginnen, bevor Sie mit diesem Handbuch fortfahren.

## Entfernen hinzugefügter Felder aus Standardfeldgruppen {#remove-field-group}

Nachdem Sie eine Standardfeldgruppe zu einem Schema hinzugefügt haben, können Sie alle Standardfelder entfernen, die Sie nicht benötigen.

>[!NOTE]
>
>Das Entfernen von Feldern aus einer Standardfeldgruppe wirkt sich nur auf das Schema aus, an dem gearbeitet wird, und nicht auf die Feldgruppe selbst. Wenn Sie Standardfelder in einem Schema entfernen, sind diese Felder weiterhin in allen anderen Schemata verfügbar, die dieselbe Feldergruppe verwenden.

Im folgenden Beispiel wurde die Standardfeldgruppe **[!UICONTROL Demografische Details]** zu einem Schema hinzugefügt. Um ein einzelnes Feld, z. B. `maritalStatus`, zu entfernen, wählen Sie das Feld auf der Arbeitsfläche und dann **[!UICONTROL Entfernen]** in der rechten Leiste aus.

![Der Schema-Editor mit der hervorgehobenen Feldergruppe, dem Feld „Familienstand“ und „Entfernen“.](../images/ui/field-based-workflows/remove-single-field.png)

Wenn mehrere Felder entfernt werden sollen, können Sie die Feldergruppe als Ganzes verwalten. Wählen Sie auf der Arbeitsfläche ein Feld aus, das zur Gruppe gehört, und wählen Sie dann **[!UICONTROL Verknüpfte Felder verwalten]** in der rechten Leiste aus.

![Der Schema-Editor mit einem hervorgehobenen Feld und „Verknüpfte Felder verwalten“.](../images/ui/field-based-workflows/manage-related-fields.png)

Es wird ein Dialogfeld mit der Struktur der betreffenden Feldergruppe angezeigt. Von hier aus können Sie die bereitgestellten Kontrollkästchen verwenden, um die erforderlichen Felder zu aktivieren oder die Auswahl aufzuheben. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Bestätigen]** aus.

![Das Dialogfeld „Verwandte Felder verwalten“ mit Hervorhebung des Feldergruppendiagramms und der Option „Bestätigen“.](../images/ui/field-based-workflows/select-fields.png)

Die Arbeitsfläche wird erneut angezeigt, wobei nur die ausgewählten Felder in der Schemastruktur vorhanden sind.

![Der Schema-Editor mit der hervorgehobenen neu bearbeiteten Feldergruppe.](../images/ui/field-based-workflows/fields-added.png)

## Hinzufügen von Standardfeldern direkt zu einem Schema

Sie können Felder aus Standardfeldgruppen direkt zu einem Schema hinzufügen, ohne die entsprechende Feldgruppe zuvor kennen zu müssen. Um ein Standardfeld zu einem Schema hinzuzufügen, klicken Sie auf das Pluszeichen (**+**) neben dem Namen des Schemas auf der Arbeitsfläche. Ein Platzhalter **[!UICONTROL Nicht benanntes Feld]** wird in der Schemastruktur angezeigt, und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Der Schema-Editor mit einem hervorgehobenen Platzhalter für ein Stammfeld.](../images/ui/field-based-workflows/root-custom-field.png)

Geben **[!UICONTROL unter]** den Namen des Felds ein, das Sie hinzufügen möchten. Das System sucht automatisch nach Standardfeldern, die mit der Abfrage übereinstimmen, und listet sie unter **[!UICONTROL Empfohlene Standardfelder]** auf, einschließlich der Feldergruppen, zu denen sie gehören.

![Der hervorgehobene Feldname und eine Liste empfohlener Standardfelder werden in den Feldeigenschaften des Schema-Editors angezeigt.](../images/ui/field-based-workflows/standard-field-search.png)

Während einige Standardfelder denselben Namen haben, kann ihre Struktur je nach der Feldergruppe, aus der sie stammen, variieren. Wenn ein Standardfeld in einem übergeordneten Objekt in der Feldergruppenstruktur verschachtelt ist, wird das übergeordnete Feld ebenfalls in das Schema aufgenommen, wenn das untergeordnete Feld hinzugefügt wird.

Wählen Sie das Vorschausymbol (![Vorschausymbol](/help/images/icons/preview.png)) neben einem Standardfeld aus, um die Struktur seiner Feldergruppe anzuzeigen und besser zu verstehen, wie sie verschachtelt werden könnte. Um das Standardfeld zum Schema hinzuzufügen, wählen Sie das Pluszeichen (![Pluszeichen](/help/images/icons/add-circle.png)) aus.

![Das hervorgehobene Symbol „Hinzufügen“ auf einem Element der vorgeschlagenen Standardfelder.](../images/ui/field-based-workflows/add-standard-field.png)

Die Arbeitsfläche wird aktualisiert und zeigt das zum Schema hinzugefügte Standardfeld an, einschließlich aller übergeordneten Felder, unter denen es in der Feldergruppenstruktur verschachtelt ist. Der Name der Feldergruppe wird auch unter **[!UICONTROL Feldergruppen]** in der linken Leiste aufgeführt. Wenn Sie mehr Felder aus derselben Feldergruppe hinzufügen möchten, wählen Sie **[!UICONTROL Verwandte Felder verwalten]** in der rechten Leiste aus.

![Der Schema-Editor mit der hervorgehobenen Option „Feldergruppe“, „Standardfeld“ und „Verknüpfte Felder verwalten“.](../images/ui/field-based-workflows/standard-field-added.png)

## Hinzufügen benutzerdefinierter Felder direkt zu einem Schema

Ähnlich wie beim Workflow für Standardfelder können Sie auch Ihre eigenen benutzerdefinierten Felder direkt zu einem Schema hinzufügen.

Um Felder zur Stammebene eines Schemas hinzuzufügen, klicken Sie auf das Pluszeichen (**+**) neben dem Namen des Schemas auf der Arbeitsfläche. Ein Platzhalter **[!UICONTROL Nicht benanntes Feld]** wird in der Schemastruktur angezeigt, und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Der Schema-Editor mit dem Hinzufügen-Symbol und einem unbenannten Feld auf Stammebene, das hervorgehoben ist.](../images/ui/field-based-workflows/root-custom-field.png)

Beginnen Sie mit der Eingabe des Namens des Felds, das Sie hinzufügen möchten, und das System beginnt automatisch mit der Suche nach übereinstimmenden Standardfeldern. Um stattdessen ein neues benutzerdefiniertes Feld zu erstellen, wählen Sie die obere Option aus, an die **angehängt ist ([!UICONTROL Neues Feld])**.

![Der Feldname und der Vorschlag für ein neues Feld, die in den Feldeigenschaften des Schema-Editors hervorgehoben sind.](../images/ui/field-based-workflows/custom-field-search.png)

Geben Sie von hier aus einen Anzeigenamen und einen Datentyp für das Feld an. Unter **[!UICONTROL Feldergruppe zuweisen]** müssen Sie eine Feldergruppe auswählen, mit der das neue Feld verknüpft werden soll. Geben Sie den Namen der Feldergruppe ein. Wenn Sie zuvor [benutzerdefinierte Feldergruppen erstellt haben](./resources/field-groups.md#create) werden diese in der Dropdown-Liste angezeigt. Alternativ können Sie stattdessen einen eindeutigen Namen in das Feld eingeben, um eine neue Feldergruppe zu erstellen.

![Die hervorgehobenen Einstellungen „Anzeigename“, „Typ“ und „Zu Feld zuweisen“ im Schema-Editor.](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Wenn Sie eine vorhandene benutzerdefinierte Feldergruppe auswählen, erben alle anderen Schemata, die diese Feldergruppe verwenden, das neu hinzugefügte Feld ebenfalls, nachdem Sie Ihre Änderungen gespeichert haben. Wählen Sie daher nur dann eine vorhandene Feldergruppe aus, wenn Sie diese Art der Verbreitung wünschen. Andernfalls sollten Sie stattdessen eine neue benutzerdefinierte Feldergruppe erstellen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![Übernehmen wird in den Feldeigenschaften des Schema-Editors hervorgehoben.](../images/ui/field-based-workflows/apply-field.png)

Das neue Feld wird der Arbeitsfläche hinzugefügt und erhält einen Namespace unter Ihrer [Mandanten-ID](../api/getting-started.md#know-your-tenant_id), um Konflikte mit standardmäßigen XDM-Feldern zu vermeiden. Die Feldergruppe, mit der Sie das neue Feld verknüpft haben, wird auch unter **[!UICONTROL Feldergruppen]** in der linken Leiste angezeigt.

![Der Schema-Editor mit dem neuen Feld, das der Arbeitsfläche hinzugefügt und unter Ihrer Mandanten-ID mit einem Namespace versehen wird. Die Feldergruppe und das Feld sind hervorgehoben.](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Die übrigen Felder, die von der ausgewählten benutzerdefinierten Feldergruppe bereitgestellt werden, werden standardmäßig aus dem Schema entfernt. Wenn Sie einige dieser Felder zum Schema hinzufügen möchten, wählen Sie ein Feld aus der Gruppe aus und wählen Sie dann **[!UICONTROL Verwandte Felder verwalten]** in der rechten Leiste aus.

### Hinzufügen benutzerdefinierter Felder zur Struktur von Standardfeldgruppen

Wenn das Schema, an dem Sie arbeiten, ein Feld vom Typ „Objekt“ hat, das von einer Standardfeldgruppe bereitgestellt wird, können Sie diesem Standardobjekt Ihre eigenen benutzerdefinierten Felder hinzufügen. Klicken Sie auf das Pluszeichen (**+**) neben dem Stammverzeichnis des Objekts.

>[!IMPORTANT]
>
>Alle Felder, die einer Feldergruppe in einem Schema hinzugefügt wurden, werden auch in allen anderen Schemata angezeigt, die dieselbe Feldergruppe verwenden.

![Der Schema-Editor mit dem Pluszeichen neben einem Standardobjekt wird hervorgehoben.](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Weitere Informationen [&#x200B; Hinzufügen benutzerdefinierter Felder finden Sie im Handbuch zur Benutzeroberfläche &#x200B;](./resources/schemas.md#custom-fields-for-standard-groups)Erstellen und Bearbeiten von Schemata“.

## Nächste Schritte

In diesem Handbuch wurden die neuen feldbasierten Workflows für den Schema-Editor in der Experience Platform-Benutzeroberfläche behandelt. Weitere Informationen zum Verwalten von Schemata in der Benutzeroberfläche finden Sie unter [Benutzeroberfläche - Übersicht](./overview.md).
