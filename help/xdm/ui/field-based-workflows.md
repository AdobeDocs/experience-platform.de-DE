---
title: Feldbasierte Workflows im Schema Editor (Beta)
description: Erfahren Sie, wie Sie Ihren Experience-Datenmodell (XDM)-Schemas einzeln Felder aus vorhandenen Feldergruppen hinzufügen können.
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: b7c6f37d3e6d824465713647b624473cff188378
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Feldbasierte Workflows im Schema Editor (Beta)

>[!IMPORTANT]
>
>Die in diesem Dokument beschriebenen Workflows befinden sich derzeit in der Beta-Phase. Die Funktionalität und Dokumentation können sich ändern.

Adobe Experience Platform bietet einen robusten Satz standardisierter [Feldergruppen](../schema/composition.md#field-group) zur Verwendung in Experience-Datenmodell (XDM)-Schemas. Die Struktur und die Semantik hinter diesen Feldergruppen sind sorgfältig darauf zugeschnitten, eine Vielzahl von Segmentierungsanwendungsfällen und anderen nachgelagerten Anwendungen in Platform zu erfüllen. Sie können auch eigene benutzerdefinierte Feldergruppen definieren, um individuelle Geschäftsanforderungen zu erfüllen.

Wenn Sie einem Schema eine Feldergruppe hinzufügen, übernimmt dieses Schema alle in dieser Gruppe enthaltenen Felder. Sie können Ihrem Schema jetzt jedoch einzelne Felder hinzufügen, ohne andere Felder aus der zugehörigen Feldergruppe einbeziehen zu müssen, die Sie möglicherweise nicht unbedingt verwenden.

In diesem Handbuch werden die verschiedenen Methoden zum Hinzufügen einzelner Felder zu einem Schema in der Platform-Benutzeroberfläche beschrieben.

## Voraussetzungen

In diesem Tutorial wird davon ausgegangen, dass Sie mit der [Zusammensetzung von XDM-Schemas](../schema/composition.md) und der Verwendung des Schema-Editors in der Platform-Benutzeroberfläche vertraut sind. Anschließend sollten Sie [ein neues Schema](./resources/schemas.md) erstellen und es einer Standardklasse zuweisen, bevor Sie mit diesem Handbuch fortfahren.

## Felder, die zu Standardfeldgruppen hinzugefügt wurden, entfernen

Nachdem Sie einem Schema eine Standardfeldgruppe hinzugefügt haben, können Sie alle nicht benötigten Standardfelder entfernen.

>[!NOTE]
>
>Das Entfernen von Feldern aus einer Standardfeldgruppe wirkt sich nur auf das bearbeitete Schema aus und hat keine Auswirkungen auf die Feldergruppe selbst. Wenn Sie Standardfelder in einem Schema entfernen, sind diese Felder weiterhin in allen anderen Schemas verfügbar, die dieselbe Feldergruppe verwenden.

Im folgenden Beispiel wurde einem Schema die Standardfeldgruppe **[!UICONTROL Demografische Details]** hinzugefügt. Um ein einzelnes Feld wie `taxId` zu entfernen, wählen Sie das Feld auf der Arbeitsfläche aus und klicken Sie dann in der rechten Leiste auf **[!UICONTROL Entfernen]**.

![Einzelnes Feld entfernen](../images/ui/field-based-workflows/remove-single-field.png)

Wenn Sie mehrere Felder entfernen möchten, können Sie die Feldergruppe als Ganzes verwalten. Wählen Sie auf der Arbeitsfläche ein Feld aus, das zur Gruppe gehört, und wählen Sie dann **[!UICONTROL Zugehörige Felder verwalten]** in der rechten Leiste aus.

![Zugehörige Felder verwalten](../images/ui/field-based-workflows/manage-related-fields.png)

Es wird ein Dialogfeld mit der Struktur der betreffenden Feldergruppe angezeigt. Hier können Sie die Kontrollkästchen verwenden, um die erforderlichen Felder auszuwählen oder die Auswahl aufzuheben. Wenn Sie zufrieden sind, wählen Sie **[!UICONTROL Felder hinzufügen]** aus.

![Felder aus Feldergruppe auswählen](../images/ui/field-based-workflows/select-fields.png)

Die Arbeitsfläche wird nur mit den in der Schemastruktur ausgewählten Feldern wieder angezeigt.

![Felder hinzugefügt](../images/ui/field-based-workflows/fields-added.png)

## Standardfelder direkt zu einem Schema hinzufügen

Sie können Felder aus Standardfeldgruppen direkt zu einem Schema hinzufügen, ohne zuvor die entsprechende Feldergruppe kennen zu müssen. Um einem Schema ein Standardfeld hinzuzufügen, wählen Sie auf der Arbeitsfläche das Pluszeichen (**+**) neben dem Namen des Schemas aus. Ein Platzhalter **[!UICONTROL Unbenanntes Feld]** wird in der Schemastruktur angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Feld-Platzhalter](../images/ui/field-based-workflows/root-custom-field.png)

Geben Sie unter **[!UICONTROL Feldname]** den Namen des Felds ein, das Sie hinzufügen möchten. Das System sucht automatisch nach Standardfeldern, die mit der Abfrage übereinstimmen, und listet sie unter **[!UICONTROL Empfohlene Standardfelder]** auf, einschließlich der Feldergruppen, zu denen sie gehören.

![Empfohlene Standardfelder](../images/ui/field-based-workflows/standard-field-search.png)

Einige Standardfelder weisen denselben Namen auf, ihre Struktur kann jedoch je nach der Feldergruppe, aus der sie stammen, variieren. Wenn ein Standardfeld innerhalb eines übergeordneten Objekts in der Feldergruppenstruktur verschachtelt ist, wird das übergeordnete Feld auch im Schema enthalten sein, wenn das untergeordnete Feld hinzugefügt wird.

Wählen Sie das Vorschausymbol (![Vorschau-Symbol](../images/ui/field-based-workflows/preview-icon.png)) neben einem Standardfeld aus, um die Struktur seiner Feldergruppe anzuzeigen und besser zu verstehen, wie sie verschachtelt sein könnte. Um das Standardfeld zum Schema hinzuzufügen, wählen Sie das Pluszeichen (![Plus-Symbol](../images/ui/field-based-workflows/add-icon.png)) aus.

![Standardfeld hinzufügen](../images/ui/field-based-workflows/add-standard-field.png)

Die Arbeitsfläche wird aktualisiert und zeigt das Standardfeld an, das dem Schema hinzugefügt wurde, einschließlich der übergeordneten Felder, unter denen es innerhalb der Feldergruppenstruktur verschachtelt ist. Der Name der Feldergruppe wird auch in der linken Leiste unter **[!UICONTROL Feldergruppen]** aufgeführt. Wenn Sie weitere Felder aus derselben Feldergruppe hinzufügen möchten, wählen Sie **[!UICONTROL Zugehörige Felder verwalten]** in der rechten Leiste aus.

![Standardfeld hinzugefügt](../images/ui/field-based-workflows/standard-field-added.png)

## Benutzerdefinierte Felder direkt zu einem Schema hinzufügen

Wenn Sie zuvor [benutzerdefinierte Feldergruppen](./resources/field-groups.md#create) erstellt haben, können Sie benutzerdefinierte Felder direkt zum Schema hinzufügen, ohne sie zuvor separat zu einer benutzerdefinierten Feldergruppe hinzufügen zu müssen.

>[!WARNING]
>
>Wenn Sie ein benutzerdefiniertes Feld zu einem Schema hinzufügen, müssen Sie weiterhin eine vorhandene benutzerdefinierte Feldergruppe auswählen, damit sie verknüpft werden kann. Damit Sie einem Schema benutzerdefinierte Felder direkt hinzufügen können, muss zuvor mindestens eine benutzerdefinierte Feldergruppe in der Sandbox definiert sein, in der Sie arbeiten. Darüber hinaus übernehmen alle anderen Schemas, die diese benutzerdefinierte Feldergruppe verwenden, auch das neu hinzugefügte Feld, nachdem Sie Ihre Änderungen gespeichert haben.

Um der Stammebene eines Schemas Felder hinzuzufügen, wählen Sie auf der Arbeitsfläche das Pluszeichen (**+**) neben dem Namen des Schemas aus. Ein Platzhalter **[!UICONTROL Unbenanntes Feld]** wird in der Schemastruktur angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren des Felds anzuzeigen.

![Benutzerdefiniertes Stammfeld](../images/ui/field-based-workflows/root-custom-field.png)

Beginnen Sie mit der Eingabe des Namens des benutzerdefinierten Felds, das Sie hinzufügen möchten, und das System beginnt automatisch mit der Suche nach entsprechenden Standardfeldern. Um stattdessen ein neues benutzerdefiniertes Feld zu erstellen, wählen Sie die obere Option aus, die an **([!UICONTROL Neues Feld])** angehängt wird.

![Neues Feld](../images/ui/field-based-workflows/custom-field-search.png)

Geben Sie von hier aus einen Anzeigenamen und einen Datentyp für das Feld ein. Wählen Sie unter **[!UICONTROL Feldergruppe zuweisen]** die benutzerdefinierte Feldergruppe aus, mit der das neue Feld verknüpft werden soll.

![Feldgruppe auswählen](../images/ui/field-based-workflows/select-field-group.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Apply]**.

![Feld anwenden](../images/ui/field-based-workflows/apply-field.png)

Das neue Feld wird der Arbeitsfläche hinzugefügt und unter Ihrer [Mandanten-ID](../api/getting-started.md#know-your-tenant_id) benannt, um Konflikte mit Standard-XDM-Feldern zu vermeiden. Die Feldergruppe, mit der Sie das neue Feld verknüpft haben, wird auch unter **[!UICONTROL Feldergruppen]** in der linken Leiste angezeigt.

![Mandanten-ID](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Die übrigen von der ausgewählten benutzerdefinierten Feldergruppe bereitgestellten Felder werden standardmäßig aus dem Schema entfernt. Wenn Sie einige dieser Felder zum Schema hinzufügen möchten, wählen Sie ein Feld aus, das zur Gruppe gehört, und wählen Sie dann **[!UICONTROL Zugehörige Felder verwalten]** in der rechten Leiste aus.

### Fügen Sie benutzerdefinierte Felder zur Struktur von Standardfeldgruppen hinzu

Wenn das Schema, mit dem Sie arbeiten, ein Objekt enthält, das von einer Standardfeldgruppe bereitgestellt wird, können Sie diesem Standardobjekt eigene benutzerdefinierte Felder hinzufügen. Wählen Sie das Pluszeichen (**+**) neben dem Stamm des Objekts aus und geben Sie die Details des benutzerdefinierten Felds in der rechten Leiste an.

![Feld zum Standardobjekt hinzufügen](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Nachdem Sie Ihre Änderungen angewendet haben, wird das neue Feld unter Ihrem Mandanten-ID-Namespace innerhalb des Standardobjekts angezeigt. Dieser verschachtelte Namespace verhindert Konflikte mit Feldnamen innerhalb der Feldergruppe selbst, um Änderungen in anderen Schemas zu vermeiden, die dieselbe Feldergruppe verwenden.

## Nächste Schritte

In diesem Handbuch wurden die neuen feldbasierten Workflows für den Schema Editor in der Platform-Benutzeroberfläche behandelt. Weitere Informationen zum Verwalten von Schemas in der Benutzeroberfläche finden Sie unter [UI overview](./overview.md).
