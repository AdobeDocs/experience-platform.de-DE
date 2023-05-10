---
keywords: Experience Platform;Tags verwalten;Tags;
title: Verwalten von einheitlichen Tags
description: Dieses Dokument enthält Informationen zum Verwalten von einheitlichen Tags in Adobe Experience Cloud
exl-id: 179b0618-3bd3-435c-9d17-63681177ca47
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 100%

---

# Handbuch zum Verwalten von administrativen Tags

Mit Tags können Sie Metadaten-Taxonomien verwalten, um Geschäftsobjekte zu klassifizieren und so die Erkennung und Kategorisierung zu erleichtern. Tags können dabei helfen, wichtige taxonomische Attribute für die Zielgruppen zu identifizieren, mit denen Ihr Team arbeitet, damit es sie schneller finden kann; außerdem können über einen Deskriptor gemeinsame Zielgruppen gruppiert werden. Sie sollten allgemeine Tag-Kategorien wie geografische Regionen, Geschäftseinheiten, Produktlinien, Projekte, Teams, Zeiträume (Quartale, Monate, Jahre) oder alles andere identifizieren, was Ihrem Team helfen kann, die Bedeutung zuzuordnen und die Zielgruppenfindung zu erleichtern. 

## Erstellen von Tags {#create-tag}

Um ein neues Tag zu erstellen, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Tags]** und wählen Sie dann die gewünschte Tag-Kategorie aus.

![Eine Tag-Kategorie auswählen](./images/tag-selection.png)

Wählen Sie **[!UICONTROL Tag erstellen]** aus, um ein neues Tag zu erstellen.

![Ein neues Tag erstellen](./images/new-tag.png)

Das Dialogfeld **[!UICONTROL Tag erstellen]** erscheint, in dem Sie zur Eingabe eines eindeutigen Tag-Namens aufgefordert werden. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Erstellen eines Tag-Dialogfelds mit neuem Tag-Namen](./images/create-tag-dialog.png)

Das neue Tag wurde erfolgreich erstellt und Sie werden zum Bildschirm „Tags“ weitergeleitet, wo das neu erstellte Tag in der Liste angezeigt wird.

![Neu erstelltes Tag für die Tag-Kategorie](./images/new-tag-listed.png)

## Bearbeiten eines Tags {#edit-tag}

Die Bearbeitung eines Tags ist nützlich, wenn Rechtschreibfehler, Aktualisierungen der Benennungskonvention oder Terminologieaktualisierungen vorliegen. Beim Bearbeiten eines Tags wird die Verknüpfung des Tags mit allen Objekten beibehalten, auf die sie derzeit angewendet werden.

Um ein vorhandenes Tag zu bearbeiten, klicken Sie in der Liste der Tag-Kategorien auf die Auslassungspunkte (`...`) neben dem Namen des Tags, das Sie bearbeiten möchten. In einer Dropdown-Liste werden Steuerelemente zum Bearbeiten, Verschieben oder Archivieren des Tags angezeigt. Wählen Sie **[!UICONTROL Bearbeiten]** aus dem Dropdown-Menü aus.

![Die Aktion „Bearbeiten“, angezeigt im Dropdown-Menü](./images/edit-action.png)

Das Dialogfeld **[!UICONTROL Tag bearbeiten]** erscheint, in dem Sie aufgefordert werden, den Tag-Namen zu bearbeiten. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Das Dialogfeld „Tag bearbeiten“ mit aktualisiertem Tag-Namen](./images/edit-dialog.png)

Der Tag-Name wurde erfolgreich aktualisiert und Sie werden zum Bildschirm „Tag“ weitergeleitet, wo das aktualisierte Tag in der Liste angezeigt wird.

![Aktualisiertes Tag für die Tag-Kategorie](./images/updated-tag-listed.png)

## Verschieben eines Tags zwischen Kategorien {#move-tag}

Tags können in andere Tag-Kategorien verschoben werden. Wenn ein Tag verschoben wird, bleibt die Zuordnung des Tags zu Objekten, auf die es derzeit angewendet wird, erhalten.

Um ein vorhandenes Tag zu verschieben, klicken Sie in der Liste der Tag-Kategorien auf die Auslassungspunkte (`...`) neben dem Namen des Tags, das Sie verschieben möchten. In einer Dropdown-Liste werden Steuerelemente zum Bearbeiten, Verschieben oder Archivieren des Tags angezeigt. Wählen Sie **[!UICONTROL Bearbeiten]** aus dem Dropdown-Menü aus.

![Die Aktion „Verschieben“, angezeigt im Dropdown-Menü](./images/move-action.png)

Das Dialogfeld **[!UICONTROL Tag verschieben]** erscheint, in dem Sie aufgefordert werden, die Tag-Kategorie auszuwählen, in die das ausgewählte Tag verschoben werden soll.

Sie können einen Bildlauf durchführen und aus der Liste auswählen oder alternativ die Suchfunktion verwenden, um den Kategorienamen einzugeben. Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Verschieben]**.

![Das Dialogfeld „Verschieben“ mit Suchkriterien, um die Tag-Kategorie zu finden](./images/move-dialog.png)

Das Tag wurde erfolgreich verschoben und Sie werden zum Bildschirm „Tag“ weitergeleitet, wo die aktualisierte Tag-Liste angezeigt wird, in der das Tag nicht mehr angezeigt wird.

![Aktualisierte Tag-Liste für die aktuelle Tag-Kategorie](./images/current-tag-category.png)

Das Tag wird nun in der zuvor ausgewählten Tag-Kategorie angezeigt.

![Die Tag-Liste für die ausgewählte Tag-Kategorie, in die das Tag verschoben wird](./images/moved-to-tag-category.png)

## Archivieren eines Tags {#archive-tag}

Der Status eines Tags kann zwischen aktiv und archiviert umgeschaltet werden. Archivierte Tags werden nicht aus Objekten entfernt, auf die sie bereits angewendet wurden. Sie können jedoch nicht mehr auf neue Objekte angewendet werden. Für jedes Tag wird bei allen Objekten der gleiche Status angezeigt. Dies ist besonders hilfreich, wenn Sie aktuelle Tag-Objekt-Zuordnungen beibehalten möchten, aber nicht möchten, dass das Tag in Zukunft verwendet wird.

Um ein vorhandenes Tag zu archivieren, klicken Sie in der Liste der Tag-Kategorien auf die Auslassungspunkte (`...`) neben dem Namen des Tags, das Sie archivieren möchten. In einer Dropdown-Liste werden Steuerelemente zum Bearbeiten, Verschieben oder Archivieren des Tags angezeigt. Wählen Sie **[!UICONTROL Archivieren]** aus dem Dropdown-Menü aus.

![Die Aktion „Archivieren“, angezeigt in der Dropdown-Liste](./images/archive-action.png)

Das Dialogfeld **[!UICONTROL Tag archivieren]** erscheint, in dem Sie aufgefordert werden, die Archivierung des Tags zu bestätigen. Klicken Sie auf **[!UICONTROL Archivieren]**.

![Die Aktion „Tag archivieren“ mit Bestätigungsaufforderung](./images/archive-dialog.png)

Das Tag wurde erfolgreich archiviert und Sie werden zum Tag-Bildschirm weitergeleitet. Die aktualisierte Tag-Liste zeigt jetzt den Status des Tags als `Archived` an.

![Aktualisierte Tag-Liste für die aktuelle Tag-Kategorie, in der das Tag als archiviert angezeigt wird](./images/archive-status.png)

## Wiederherstellen eines archivierten Tags {#restore-archived-tag}

Wenn Sie ein `Archived`-Tag neuen Objekten zuordnen, muss das Tag den Status `Active` haben. Beim Wiederherstellen eines archivierten Tags kehrt ein Tag in den Status `Active` zurück.

Um ein archiviertes Tag wiederherzustellen, wählen Sie in der Liste der Tag-Kategorien die Auslassungspunkte (`...`) neben dem Namen des Tags aus, das Sie wiederherstellen möchten. In einem Dropdown-Menü werden Steuerelemente zum Wiederherstellen oder Löschen des Tags angezeigt. Wählen Sie **[!UICONTROL Wiederherstellen]** aus dem Dropdown-Menü aus.

![Die Aktion „Wiederherstellen“ in der Dropdown-Liste](./images/restore-action.png)

Das Dialogfeld **[!UICONTROL Tag wiederherstellen]** erscheint, in dem Sie aufgefordert werden, die Wiederherstellung des Tags zu bestätigen. Klicken Sie auf **[!UICONTROL Wiederherstellen]**.

![Das Dialogfeld „Tag wiederherstellen“ mit Bestätigungsaufforderung](./images/restore-dialog.png)

Das Tag wurde erfolgreich wiederhergestellt und Sie werden zum Tag-Bildschirm weitergeleitet. Die aktualisierte Tag-Liste zeigt jetzt den Status des Tags als `Active` an.

![Aktualisierte Tag-Liste für die aktuelle Tag-Kategorie, in der das Tag als aktiv angezeigt wird](./images/restored-active-status.png)

## Löschen von Tags {#delete-tag}

>[!NOTE]
>
>Nur Tags mit Status `Archived`, die mit keinem Objekt verknüpft sind, können gelöscht werden.

Durch das Löschen eines Tags wird es vollständig aus dem System entfernt.

Um ein archiviertes Tag zu löschen, wählen Sie in der Liste der Tag-Kategorien die Auslassungspunkte (`...`) neben dem Namen des Tags aus, das Sie löschen möchten. In einem Dropdown-Menü werden Steuerelemente zum Wiederherstellen oder Löschen des Tags angezeigt. Wählen Sie im Dropdown-Menü die Option **[!UICONTROL Löschen]** aus.

![Die Aktion „Löschen“ im Dropdown-Menü](./images/delete-action.png)

Das Dialogfeld **[!UICONTROL Tag löschen]** erscheint, in dem Sie aufgefordert werden, die Löschung des Tags zu bestätigen. Wählen Sie **[!UICONTROL Löschen]** aus.

![Das Dialogfeld „Tag löschen“ mit Bestätigungsaufforderung](./images/delete-dialog.png)

Das Tag wurde erfolgreich gelöscht und Sie werden zum Tag-Bildschirm weitergeleitet. Das Tag wird nicht mehr in der Liste angezeigt und wurde vollständig entfernt.

![Aktualisierte Tag-Liste für die aktuelle Tag-Kategorie, in der das Tag nicht mehr zu sehen ist](./images/deleted-updated-list.png)

## Anzeigen getaggter Objekte {#view-tagged}

Jedes Tag verfügt über eine Detailseite, auf die über das Tag-Inventar zugegriffen werden kann. Auf dieser Seite werden alle Objekte aufgelistet, auf die dieses Tag angewendet wird, sodass Benutzende verwandte Objekte aus verschiedenen Apps und Funktionen in einer einzigen Ansicht sehen können.

Um die Liste der getaggten Objekte anzuzeigen, suchen Sie das Tag in einer Tag-Kategorie und wählen Sie es aus.

![Tag-Auswahl innerhalb der Tag-Kategorie](./images/view-tag-selection.png)

Das Dialogfeld [!UICONTROL Getaggte Objekte] erscheint, die Ihnen ein Inventar der getaggten Objekte zeigt.

![Inventar der getaggten Objekte](./images/tagged-objects.png)

## Nächste Schritte

Sie haben jetzt gelernt, wie Tags verwaltet werden. Eine allgemeine Übersicht zu Tags in Experience Platform finden Sie in der [Dokumentation „Übersicht zu Tags“](../overview.md).
