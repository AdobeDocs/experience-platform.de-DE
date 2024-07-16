---
title: Feldbasierte Workflows im Schema Editor
description: Erfahren Sie, wie Sie Ihren Experience-Datenmodell (XDM)-Schemas einzeln Felder aus vorhandenen Feldergruppen hinzufügen können.
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: 19e0a26958ec57ccbc614be53b5aaacce7ce9450
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---

# Feldbasierte Workflows im Schema Editor

Adobe Experience Platform bietet einen robusten Satz standardisierter [Feldergruppen](../schema/composition.md#field-group) zur Verwendung in Experience-Datenmodell (XDM)-Schemas. Die Struktur und die Semantik hinter diesen Feldergruppen sind sorgfältig darauf zugeschnitten, eine Vielzahl von Segmentierungsanwendungsfällen und anderen nachgelagerten Anwendungen in Platform zu erfüllen. Sie können auch eigene benutzerdefinierte Feldergruppen definieren, um individuelle Geschäftsanforderungen zu erfüllen.

Wenn Sie einem Schema eine Feldergruppe hinzufügen, übernimmt dieses Schema alle in dieser Gruppe enthaltenen Felder. Sie können Ihrem Schema jetzt jedoch einzelne Felder hinzufügen, ohne andere Felder aus der zugehörigen Feldergruppe einbeziehen zu müssen, die Sie möglicherweise nicht unbedingt verwenden.

In diesem Handbuch werden die verschiedenen Methoden zum Hinzufügen einzelner Felder zu einem Schema in der Platform-Benutzeroberfläche beschrieben.

## Voraussetzungen

In diesem Tutorial wird davon ausgegangen, dass Sie mit der [Zusammensetzung von XDM-Schemas](../schema/composition.md) und der Verwendung des Schema-Editors in der Platform-Benutzeroberfläche vertraut sind. Anschließend sollten Sie den Prozess [Erstellen eines neuen Schemas](./resources/schemas.md) und dessen Zuweisung zu einer Standardklasse starten, bevor Sie mit diesem Handbuch fortfahren.

## Felder, die zu Standardfeldgruppen hinzugefügt wurden, entfernen {#remove-field-group}

Nachdem Sie einem Schema eine Standardfeldgruppe hinzugefügt haben, können Sie alle nicht benötigten Standardfelder entfernen.

>[!NOTE]
>
>Das Entfernen von Feldern aus einer Standardfeldgruppe wirkt sich nur auf das bearbeitete Schema aus und hat keine Auswirkungen auf die Feldergruppe selbst. Wenn Sie Standardfelder in einem Schema entfernen, sind diese Felder weiterhin in allen anderen Schemas verfügbar, die dieselbe Feldergruppe verwenden.

Im folgenden Beispiel wurde dem Schema die Standardfeldgruppe **[!UICONTROL Demografische Details]** hinzugefügt. Um ein einzelnes Feld wie `maritalStatus` zu entfernen, wählen Sie das Feld auf der Arbeitsfläche aus und klicken Sie dann in der rechten Leiste auf **[!UICONTROL Entfernen]** .

![Der Schema-Editor mit hervorgehobener Feldergruppe, markiertem Feld Familienstand und hervorgehobenem Entfernen.](../images/ui/field-based-workflows/remove-single-field.png)

Wenn Sie mehrere Felder entfernen möchten, können Sie die Feldergruppe als Ganzes verwalten. Wählen Sie auf der Arbeitsfläche ein Feld aus, das zur Gruppe gehört, und wählen Sie dann in der rechten Leiste **[!UICONTROL Zugehörige Felder verwalten]** aus.

![Der Schema-Editor mit einem Feld und hervorgehobene zugehörige Felder verwalten](../images/ui/field-based-workflows/manage-related-fields.png).

Es wird ein Dialogfeld mit der Struktur der betreffenden Feldergruppe angezeigt. Hier können Sie die Kontrollkästchen verwenden, um die erforderlichen Felder auszuwählen oder die Auswahl aufzuheben. Wenn Sie zufrieden sind, wählen Sie **[!UICONTROL Bestätigen]** aus.

![Das Dialogfeld Verknüpfte Felder verwalten mit dem Feldgruppendiagramm und Bestätigen hervorgehoben.](../images/ui/field-based-workflows/select-fields.png)

Die Arbeitsfläche wird nur mit den in der Schemastruktur ausgewählten Feldern wieder angezeigt.

![Der Schema-Editor mit der neu bearbeiteten Feldergruppe hervorgehoben.](../images/ui/field-based-workflows/fields-added.png)

## Standardfelder direkt zu einem Schema hinzufügen

Sie können Felder aus Standardfeldgruppen direkt zu einem Schema hinzufügen, ohne zuvor die entsprechende Feldergruppe kennen zu müssen. Um einem Schema ein Standardfeld hinzuzufügen, wählen Sie auf der Arbeitsfläche das Pluszeichen (**+**) neben dem Namen des Schemas aus. Ein Platzhalter **[!UICONTROL Unbenanntes Feld]** wird in der Schemastruktur angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Der Schema-Editor mit einem Platzhalter für Stammfelder hervorgehoben.](../images/ui/field-based-workflows/root-custom-field.png)

Geben Sie unter **[!UICONTROL Feldname]** den Namen des Felds ein, das Sie hinzufügen möchten. Das System sucht automatisch nach Standardfeldern, die mit der Abfrage übereinstimmen, und listet sie unter **[!UICONTROL Empfohlene Standardfelder]** auf, einschließlich der Feldergruppen, zu denen sie gehören.

![Der markierte Feldname und eine Liste empfohlener Standardfelder, die in den Feldeigenschaften des Schema-Editors angezeigt werden.](../images/ui/field-based-workflows/standard-field-search.png)

Einige Standardfelder weisen denselben Namen auf, ihre Struktur kann jedoch von der Feldergruppe abhängen, aus der sie stammen. Wenn ein Standardfeld innerhalb eines übergeordneten Objekts in der Feldergruppenstruktur verschachtelt ist, wird das übergeordnete Feld auch im Schema enthalten sein, wenn das untergeordnete Feld hinzugefügt wird.

Wählen Sie das Vorschausymbol (![Vorschau-Symbol](../images/ui/field-based-workflows/preview-icon.png)) neben einem Standardfeld aus, um die Struktur seiner Feldergruppe anzuzeigen und besser zu verstehen, wie sie möglicherweise verschachtelt ist. Um das Standardfeld zum Schema hinzuzufügen, wählen Sie das Pluszeichen (![Plussymbol](../images/ui/field-based-workflows/add-icon.png)) aus.

![Das Symbol zum Hinzufügen, das auf einem Element der vorgeschlagenen Standardfelder hervorgehoben ist.](../images/ui/field-based-workflows/add-standard-field.png)

Die Arbeitsfläche wird aktualisiert und zeigt das Standardfeld an, das dem Schema hinzugefügt wurde, einschließlich der übergeordneten Felder, unter denen es innerhalb der Feldergruppenstruktur verschachtelt ist. Der Name der Feldergruppe wird auch in der linken Leiste unter **[!UICONTROL Feldergruppen]** aufgeführt. Wenn Sie weitere Felder aus derselben Feldergruppe hinzufügen möchten, wählen Sie in der rechten Leiste **[!UICONTROL Zugehörige Felder verwalten]** aus.

![Der Schema-Editor mit hervorgehobenen Feldern &quot;Feldergruppe&quot;, &quot;Standardfeld&quot;und &quot;Zugehörige verwalten&quot;.](../images/ui/field-based-workflows/standard-field-added.png)

## Benutzerdefinierte Felder direkt zu einem Schema hinzufügen

Ähnlich wie beim Workflow für Standardfelder können Sie auch eigene benutzerdefinierte Felder direkt zu einem Schema hinzufügen.

Um Felder zur Stammebene eines Schemas hinzuzufügen, wählen Sie auf der Arbeitsfläche das Pluszeichen (**+**) neben dem Namen des Schemas aus. Ein Platzhalter **[!UICONTROL Unbenanntes Feld]** wird in der Schemastruktur angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Der Schema-Editor mit dem Hinzufügen-Symbol und einem unbenannten Feld auf der Stammebene hervorgehoben.](../images/ui/field-based-workflows/root-custom-field.png)

Beginnen Sie mit der Eingabe des Namens des Felds, das Sie hinzufügen möchten, und das System beginnt automatisch mit der Suche nach entsprechenden Standardfeldern. Um stattdessen ein neues benutzerdefiniertes Feld zu erstellen, wählen Sie die obere Option aus, die an **([!UICONTROL Neues Feld])** angehängt ist.

![Der Feldname und der Vorschlag für ein neues Feld, die in den Feldeigenschaften des Schema-Editors hervorgehoben werden.](../images/ui/field-based-workflows/custom-field-search.png)

Geben Sie von hier aus einen Anzeigenamen und einen Datentyp für das Feld ein. Unter **[!UICONTROL Feldergruppe zuweisen]** müssen Sie eine Feldergruppe auswählen, mit der das neue Feld verknüpft werden soll. Beginnen Sie mit der Eingabe des Namens der Feldergruppe. Wenn Sie zuvor [benutzerdefinierte Feldergruppen erstellt haben,](./resources/field-groups.md#create) werden diese in der Dropdown-Liste angezeigt. Alternativ können Sie einen eindeutigen Namen in das Feld eingeben, um stattdessen eine neue Feldergruppe zu erstellen.

![Die im Schema Editor hervorgehobenen Einstellungen für Anzeigename, Typ und Zu Feld zuweisen .](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Wenn Sie eine vorhandene benutzerdefinierte Feldergruppe auswählen, übernehmen alle anderen Schemas, die diese Feldergruppe verwenden, auch das neu hinzugefügte Feld, nachdem Sie Ihre Änderungen gespeichert haben. Wählen Sie daher nur dann eine existierende Feldergruppe aus, wenn Sie diese Art von Vermehrung wünschen. Andernfalls sollten Sie stattdessen eine neue benutzerdefinierte Feldergruppe erstellen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![Anwenden wird in den Feldeigenschaften des Schema-Editors hervorgehoben.](../images/ui/field-based-workflows/apply-field.png)

Das neue Feld wird der Arbeitsfläche hinzugefügt und unter Ihrer [Mandanten-ID](../api/getting-started.md#know-your-tenant_id) als Namespace angegeben, um Konflikte mit Standard-XDM-Feldern zu vermeiden. Die Feldergruppe, mit der Sie das neue Feld verknüpft haben, wird auch in der linken Leiste unter **[!UICONTROL Feldergruppen]** angezeigt.

![Der Schema-Editor mit dem neuen Feld, das der Arbeitsfläche hinzugefügt wird, und dem Namespace unter Ihrer Mandanten-ID. Die Feldergruppe und das Feld werden hervorgehoben.](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Die übrigen von der ausgewählten benutzerdefinierten Feldergruppe bereitgestellten Felder werden standardmäßig aus dem Schema entfernt. Wenn Sie einige dieser Felder zum Schema hinzufügen möchten, wählen Sie ein Feld aus, das zur Gruppe gehört, und wählen Sie dann in der rechten Leiste **[!UICONTROL Zugehörige Felder verwalten]** aus.

### Fügen Sie benutzerdefinierte Felder zur Struktur von Standardfeldgruppen hinzu

Wenn das Schema, mit dem Sie arbeiten, ein Objekt enthält, das von einer Standardfeldgruppe bereitgestellt wird, können Sie diesem Standardobjekt eigene benutzerdefinierte Felder hinzufügen. Wählen Sie das Pluszeichen (**+**) neben dem Stamm des Objekts aus.

>[!IMPORTANT]
>
>Alle Felder, die einer Feldergruppe in einem Schema hinzugefügt werden, werden auch in allen anderen Schemas angezeigt, die dieselbe Feldergruppe verwenden.

![Der Schema-Editor mit dem Pluszeichen neben einem Standardobjekt hervorgehoben.](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Weitere Informationen zum Hinzufügen benutzerdefinierter Felder finden Sie im Abschnitt [Erstellen und Bearbeiten von Schemas im UI-Handbuch](./resources/schemas.md#custom-fields-for-standard-groups) .

## Nächste Schritte

In diesem Handbuch wurden die neuen feldbasierten Workflows für den Schema Editor in der Platform-Benutzeroberfläche behandelt. Weitere Informationen zum Verwalten von Schemas in der Benutzeroberfläche finden Sie in der [UI-Übersicht](./overview.md).
