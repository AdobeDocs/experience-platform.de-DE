---
title: Feldbasierte Workflows im Schema Editor
description: Erfahren Sie, wie Sie Ihren Experience-Datenmodell (XDM)-Schemas einzeln Felder aus vorhandenen Feldergruppen hinzufügen können.
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: b224783922c3b6c5e2045134be2512748ca2575b
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Feldbasierte Workflows im Schema Editor

Adobe Experience Platform bietet einen robusten Satz standardisierter [Feldergruppen](../schema/composition.md#field-group) zur Verwendung in Experience-Datenmodell (XDM)-Schemas. Die Struktur und die Semantik hinter diesen Feldergruppen sind sorgfältig darauf zugeschnitten, eine Vielzahl von Segmentierungsanwendungsfällen und anderen nachgelagerten Anwendungen in Platform zu erfüllen. Sie können auch eigene benutzerdefinierte Feldergruppen definieren, um individuelle Geschäftsanforderungen zu erfüllen.

Wenn Sie einem Schema eine Feldergruppe hinzufügen, übernimmt dieses Schema alle in dieser Gruppe enthaltenen Felder. Sie können Ihrem Schema jetzt jedoch einzelne Felder hinzufügen, ohne andere Felder aus der zugehörigen Feldergruppe einbeziehen zu müssen, die Sie möglicherweise nicht unbedingt verwenden.

In diesem Handbuch werden die verschiedenen Methoden zum Hinzufügen einzelner Felder zu einem Schema in der Platform-Benutzeroberfläche beschrieben.

## Voraussetzungen

In diesem Tutorial wird davon ausgegangen, dass Sie mit dem [Zusammensetzung von XDM-Schemas](../schema/composition.md) und wie Sie den Schema-Editor in der Platform-Benutzeroberfläche verwenden. Um fortzufahren, sollten Sie den Prozess von [Erstellen eines neuen Schemas](./resources/schemas.md) und Zuweisen zu einer Standardklasse, bevor Sie mit diesem Handbuch fortfahren.

## Felder, die zu Standardfeldgruppen hinzugefügt wurden, entfernen {#remove-field-group}

Nachdem Sie einem Schema eine Standardfeldgruppe hinzugefügt haben, können Sie alle nicht benötigten Standardfelder entfernen.

>[!NOTE]
>
>Das Entfernen von Feldern aus einer Standardfeldgruppe wirkt sich nur auf das bearbeitete Schema aus und hat keine Auswirkungen auf die Feldergruppe selbst. Wenn Sie Standardfelder in einem Schema entfernen, sind diese Felder weiterhin in allen anderen Schemas verfügbar, die dieselbe Feldergruppe verwenden.

Im folgenden Beispiel wird die Standardfeldgruppe **[!UICONTROL Demografische Details]** wurde zu einem Schema hinzugefügt. So entfernen Sie ein einzelnes Feld wie `taxId`, wählen Sie das Feld auf der Arbeitsfläche aus und klicken Sie auf **[!UICONTROL Entfernen]** in der rechten Leiste.

![Einzelnes Feld entfernen](../images/ui/field-based-workflows/remove-single-field.png)

Wenn Sie mehrere Felder entfernen möchten, können Sie die Feldergruppe als Ganzes verwalten. Wählen Sie auf der Arbeitsfläche ein Feld aus, das zur Gruppe gehört, und wählen Sie dann **[!UICONTROL Zugehörige Felder verwalten]** in der rechten Leiste.

![Zugehörige Felder verwalten](../images/ui/field-based-workflows/manage-related-fields.png)

Es wird ein Dialogfeld mit der Struktur der betreffenden Feldergruppe angezeigt. Hier können Sie die Kontrollkästchen verwenden, um die erforderlichen Felder auszuwählen oder die Auswahl aufzuheben. Wenn Sie zufrieden sind, wählen Sie **[!UICONTROL Bestätigen]**.

![Felder aus Feldergruppe auswählen](../images/ui/field-based-workflows/select-fields.png)

Die Arbeitsfläche wird nur mit den in der Schemastruktur ausgewählten Feldern wieder angezeigt.

![Felder hinzugefügt](../images/ui/field-based-workflows/fields-added.png)

## Standardfelder direkt zu einem Schema hinzufügen

Sie können Felder aus Standardfeldgruppen direkt zu einem Schema hinzufügen, ohne zuvor die entsprechende Feldergruppe kennen zu müssen. Um einem Schema ein Standardfeld hinzuzufügen, wählen Sie das Pluszeichen (**+**) neben dem Namen des Schemas in der Arbeitsfläche. Ein **[!UICONTROL Unbenanntes Feld]** Platzhalter wird in der Schemastruktur angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Feld-Platzhalter](../images/ui/field-based-workflows/root-custom-field.png)

under **[!UICONTROL Feldname]**, geben Sie den Namen des Felds ein, das Sie hinzufügen möchten. Das System sucht automatisch nach Standardfeldern, die mit der Abfrage übereinstimmen, und listet sie unter **[!UICONTROL Empfohlene Standardfelder]**, einschließlich der Feldergruppen, denen sie angehören.

![Empfohlene Standardfelder](../images/ui/field-based-workflows/standard-field-search.png)

Einige Standardfelder weisen denselben Namen auf, ihre Struktur kann jedoch von der Feldergruppe abhängen, aus der sie stammen. Wenn ein Standardfeld innerhalb eines übergeordneten Objekts in der Feldergruppenstruktur verschachtelt ist, wird das übergeordnete Feld auch im Schema enthalten sein, wenn das untergeordnete Feld hinzugefügt wird.

Wählen Sie das Vorschausymbol (![Vorschausymbol](../images/ui/field-based-workflows/preview-icon.png)) neben einem Standardfeld klicken, um die Struktur seiner Feldergruppe anzuzeigen und besser zu verstehen, wie sie verschachtelt sein könnte. Um das Standardfeld zum Schema hinzuzufügen, wählen Sie das Pluszeichen (![Plus-Symbol](../images/ui/field-based-workflows/add-icon.png)).

![Standardfeld hinzufügen](../images/ui/field-based-workflows/add-standard-field.png)

Die Arbeitsfläche wird aktualisiert und zeigt das Standardfeld an, das dem Schema hinzugefügt wurde, einschließlich der übergeordneten Felder, unter denen es innerhalb der Feldergruppenstruktur verschachtelt ist. Der Name der Feldergruppe wird auch unter **[!UICONTROL Feldergruppen]** in der linken Leiste. Wenn Sie weitere Felder aus derselben Feldergruppe hinzufügen möchten, wählen Sie **[!UICONTROL Zugehörige Felder verwalten]** in der rechten Leiste.

![Standardfeld hinzugefügt](../images/ui/field-based-workflows/standard-field-added.png)

## Benutzerdefinierte Felder direkt zu einem Schema hinzufügen

Ähnlich wie beim Workflow für Standardfelder können Sie auch eigene benutzerdefinierte Felder direkt zu einem Schema hinzufügen.

Um Felder zur Stammebene eines Schemas hinzuzufügen, wählen Sie das Pluszeichen (**+**) neben dem Namen des Schemas in der Arbeitsfläche. Ein **[!UICONTROL Unbenanntes Feld]** Platzhalter wird in der Schemastruktur angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Benutzerdefiniertes Stammfeld](../images/ui/field-based-workflows/root-custom-field.png)

Beginnen Sie mit der Eingabe des Namens des Felds, das Sie hinzufügen möchten, und das System beginnt automatisch mit der Suche nach entsprechenden Standardfeldern. Um stattdessen ein neues benutzerdefiniertes Feld zu erstellen, wählen Sie die obere Option, die an **([!UICONTROL Neues Feld])**.

![Neues Feld](../images/ui/field-based-workflows/custom-field-search.png)

Geben Sie von hier aus einen Anzeigenamen und einen Datentyp für das Feld ein. under **[!UICONTROL Feldergruppe zuweisen]** müssen Sie eine Feldergruppe für das neue Feld auswählen, mit dem verknüpft werden soll. Beginnen Sie mit der Eingabe des Namens der Feldergruppe, und falls Sie zuvor [erstellte benutzerdefinierte Feldgruppen](./resources/field-groups.md#create) werden sie in der Dropdown-Liste angezeigt. Alternativ können Sie einen eindeutigen Namen in das Feld eingeben, um stattdessen eine neue Feldergruppe zu erstellen.

![Feldgruppe auswählen](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Wenn Sie eine vorhandene benutzerdefinierte Feldergruppe auswählen, übernehmen alle anderen Schemas, die diese Feldergruppe verwenden, auch das neu hinzugefügte Feld, nachdem Sie Ihre Änderungen gespeichert haben. Wählen Sie daher nur dann eine existierende Feldergruppe aus, wenn Sie diese Art von Vermehrung wünschen. Andernfalls sollten Sie stattdessen eine neue benutzerdefinierte Feldergruppe erstellen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![Feld anwenden](../images/ui/field-based-workflows/apply-field.png)

Das neue Feld wird der Arbeitsfläche hinzugefügt und unter Ihrem [Mandanten-ID](../api/getting-started.md#know-your-tenant_id) um Konflikte mit Standard-XDM-Feldern zu vermeiden. Die Feldergruppe, mit der Sie das neue Feld verknüpft haben, wird ebenfalls unter **[!UICONTROL Feldergruppen]** in der linken Leiste.

![Mandanten-ID](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Die übrigen von der ausgewählten benutzerdefinierten Feldergruppe bereitgestellten Felder werden standardmäßig aus dem Schema entfernt. Wenn Sie einige dieser Felder zum Schema hinzufügen möchten, wählen Sie ein Feld aus, das zur Gruppe gehört, und wählen Sie dann **[!UICONTROL Zugehörige Felder verwalten]** in der rechten Leiste.

### Fügen Sie benutzerdefinierte Felder zur Struktur von Standardfeldgruppen hinzu

Wenn das Schema, mit dem Sie arbeiten, ein Objekt enthält, das von einer Standardfeldgruppe bereitgestellt wird, können Sie diesem Standardobjekt eigene benutzerdefinierte Felder hinzufügen. Wählen Sie das Pluszeichen (**+**) neben dem Stamm des Objekts und geben Sie die Details des benutzerdefinierten Felds in der rechten Leiste an.

![Feld zum Standardobjekt hinzufügen](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Nachdem Sie Ihre Änderungen angewendet haben, wird das neue Feld unter Ihrem Mandanten-ID-Namespace innerhalb des Standardobjekts angezeigt. Dieser verschachtelte Namespace verhindert Konflikte mit Feldnamen innerhalb der Feldergruppe selbst, um Änderungen in anderen Schemas zu vermeiden, die dieselbe Feldergruppe verwenden.

![Feld zum Standardobjekt hinzugefügt](../images/ui/field-based-workflows/added-to-standard-object.png)

## Nächste Schritte

In diesem Handbuch wurden die neuen feldbasierten Workflows für den Schema Editor in der Platform-Benutzeroberfläche behandelt. Weitere Informationen zum Verwalten von Schemas in der Benutzeroberfläche finden Sie unter [Übersicht über die Benutzeroberfläche](./overview.md).
