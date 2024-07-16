---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;attributbasierte Zugriffssteuerung;ABAC
title: Attributbasierte Zugriffssteuerung Rolle erstellen
description: Dieses Dokument enthält Informationen zum Verwalten von Rollen über die Benutzeroberfläche "Berechtigungen"in Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: d8f72bb5ae56daf5a41c763f821ca6306514bc48
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 15%

---

# Verwalten von Rollen

Rollen definieren den Zugriff, den ein Administrator, ein Spezialist oder ein Endbenutzer auf Ressourcen in Ihrem Unternehmen hat. In einer rollenbasierten Zugriffssteuerungsumgebung erfolgt die Bereitstellung des Benutzerzugriffs über gemeinsame Zuständigkeiten und Anforderungen. Eine Rolle verfügt über bestimmte Berechtigungen, wobei Mitglieder Ihrer Organisation je nach dem Umfang des Lese- oder Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden können.

## Erstellen einer neuen Rolle

Um eine neue Rolle zu erstellen, wählen Sie in der Seitenleiste die Registerkarte **[!UICONTROL Rollen]** und danach **[!UICONTROL Rolle erstellen]** aus.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

Das Dialogfeld **[!UICONTROL Neue Rolle erstellen]** wird angezeigt, in dem Sie zur Eingabe eines Namens und einer optionalen Beschreibung aufgefordert werden.

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Bestätigen]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Wählen Sie anschließend mithilfe des Dropdown-Menüs die Ressourcenberechtigungen aus, die Sie in die Rolle einbeziehen möchten.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Um weitere Ressourcen hinzuzufügen, wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Adobe Experience Platform]** aus, wo eine Ressourcenliste angezeigt wird. Geben Sie alternativ den Ressourcennamen in die Suchleiste im linken Navigationsbereich ein.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Klicken Sie auf die gewünschte Ressource und ziehen Sie sie in den Hauptbereich.

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

Wählen Sie im Dropdown-Menü die Ressourcenberechtigungen aus, die Sie in die Rolle einbeziehen möchten. Wiederholen Sie diesen Vorgang für alle Ressourcen, die Sie für die Rolle einbeziehen möchten. Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Speichern und beenden]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

Die neue Rolle wurde erfolgreich erstellt und Sie werden zur Seite **[!UICONTROL Rollen]** weitergeleitet, auf der die neu erstellte Rolle in der Liste angezeigt wird.

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

Weitere Informationen zum Verwalten von Rollenberechtigungen nach ihrer Erstellung finden Sie in den Abschnitten zum [Verwalten von Berechtigungen für eine Rolle](#manage-permissions-for-a-role) .

Das folgende Video soll Ihnen dabei helfen, eine neue Rolle zu erstellen und Benutzer für diese Rolle zu verwalten.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Rolle duplizieren

Um eine vorhandene Rolle zu duplizieren, wählen Sie die Rolle auf der Registerkarte **[!UICONTROL Rollen]** aus. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Rolle zu finden, die Sie duplizieren möchten.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Wählen Sie dann oben rechts im Bildschirm **[!UICONTROL Duplizieren]** aus.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

Das Dialogfeld **[!UICONTROL Rolle duplizieren]** wird angezeigt und fordert Sie auf, die Duplizierung zu bestätigen.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Anschließend gelangen Sie zur Detailseite der Rolle, auf der Sie den Namen und die Berechtigungen für die Rolle ändern können. Die Details, Beschriftungen und Sandboxes werden aus der vorherigen Rolle dupliziert. Benutzer müssen über den Tab Benutzer hinzugefügt werden. Sie können das Dokument [Berechtigungen für eine Rolle verwalten](permissions.md) anzeigen, um mehr über das Hinzufügen von Details, Beschriftungen, Sandboxes und Benutzern zu einer Rolle zu erfahren.

Klicken Sie auf den linken Pfeil, um zur Registerkarte **[!UICONTROL Rollen]** zurückzukehren.

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

Die neue Rolle wird in der Liste auf der Seite **[!UICONTROL Benutzerrollen]** angezeigt.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Rollen löschen

Wählen Sie die Auslassungszeichen (`…`) neben dem Namen einer Rolle aus. Eine Dropdown-Liste zeigt Steuerelemente zum Bearbeiten, Löschen oder Duplizieren der Rolle an. Wählen Sie im Dropdown-Menü die Option „Löschen“ aus.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

Das Dialogfeld **[!UICONTROL Benutzerrolle löschen]** wird angezeigt und fordert Sie auf, den Löschvorgang zu bestätigen.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Sie werden zur Registerkarte **[!UICONTROL Rollen]** zurückgeleitet.

## Nächste Schritte

Nachdem eine neue Rolle erstellt wurde, können Sie mit dem nächsten Schritt &quot;[Berechtigungen für eine Rolle verwalten](permissions.md)&quot;fortfahren.
