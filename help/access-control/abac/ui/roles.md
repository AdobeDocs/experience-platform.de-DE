---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;attributbasierte Zugriffssteuerung;ABAC
title: Attributbasierte Zugriffssteuerung Rolle erstellen
description: Dieses Dokument enthält Informationen zum Verwalten von Rollen über die Benutzeroberfläche "Berechtigungen"in Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 16%

---

# Verwalten von Rollen

Rollen definieren den Zugriff, den ein Administrator, ein Spezialist oder ein Endbenutzer auf Ressourcen in Ihrem Unternehmen hat. In einer rollenbasierten Zugriffssteuerungsumgebung erfolgt die Bereitstellung des Benutzerzugriffs über gemeinsame Zuständigkeiten und Anforderungen. Eine Rolle verfügt über bestimmte Berechtigungen, wobei Mitglieder Ihrer Organisation je nach dem Umfang des Lese- oder Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden können.

## Erstellen einer neuen Rolle

Um eine neue Rolle zu erstellen, wählen Sie die **[!UICONTROL Rollen]** Registerkarte in der Seitenleiste und wählen Sie **[!UICONTROL Rolle erstellen]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

Die **[!UICONTROL Neue Rolle erstellen]** angezeigt, in dem Sie aufgefordert werden, einen Namen und eine optionale Beschreibung einzugeben.

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Bestätigen]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Wählen Sie anschließend mithilfe des Dropdown-Menüs die Ressourcenberechtigungen aus, die Sie in die Rolle einbeziehen möchten.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Um weitere Ressourcen hinzuzufügen, wählen Sie **[!UICONTROL Adobe Experience Platform]** über das linke Navigationsfenster, das eine Liste der Ressourcen anzeigt. Geben Sie alternativ den Ressourcennamen in die Suchleiste im linken Navigationsbereich ein.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Klicken Sie auf die gewünschte Ressource und ziehen Sie sie in den Hauptbereich.

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

Wählen Sie im Dropdown-Menü die Ressourcenberechtigungen aus, die Sie in die Rolle einbeziehen möchten. Wiederholen Sie diesen Vorgang für alle Ressourcen, die Sie für die Rolle einbeziehen möchten. Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Speichern und beenden]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

Die neue Rolle wurde erfolgreich erstellt und Sie werden zum **[!UICONTROL Rollen]** -Seite, auf der die neu erstellte Rolle in der Liste angezeigt wird.

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

Siehe die Abschnitte unter [Verwalten von Berechtigungen für eine Rolle](#manage-permissions-for-a-role) Weitere Informationen zum Verwalten von Rollenberechtigungen nach deren Erstellung.

## Rolle duplizieren

Um eine vorhandene Rolle zu duplizieren, wählen Sie die Rolle aus dem **[!UICONTROL Rollen]** Registerkarte. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Rolle zu finden, die Sie duplizieren möchten.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Wählen Sie als Nächstes **[!UICONTROL Duplizieren]** oben rechts im Bildschirm.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

Die **[!UICONTROL Rolle duplizieren]** angezeigt, in dem Sie aufgefordert werden, die Duplizierung zu bestätigen.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Anschließend gelangen Sie zur Detailseite der Rolle, auf der Sie den Namen und die Berechtigungen für die Rolle ändern können. Die Details, Beschriftungen und Sandboxes werden aus der vorherigen Rolle dupliziert. Benutzer müssen über den Tab Benutzer hinzugefügt werden. Sie können die [Berechtigungen für eine Rolle verwalten](permissions.md) -Dokument, um mehr über das Hinzufügen von Details, Beschriftungen, Sandboxes und Benutzern zu einer Rolle zu erfahren.

Klicken Sie auf den linken Pfeil, um zum **[!UICONTROL Rollen]** Registerkarte.

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

Die neue Rolle wird in der Liste auf der **[!UICONTROL Rollen]** Seite.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Rollen löschen

Wählen Sie die Auslassungszeichen (`…`) neben dem Namen einer Rolle angezeigt. In einer Dropdown-Liste werden Steuerelemente zum Bearbeiten, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie im Dropdown-Menü die Option „Löschen“ aus.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

Die **[!UICONTROL Benutzerrolle löschen]** angezeigt, in dem Sie aufgefordert werden, den Löschvorgang zu bestätigen.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Sie werden zum **[!UICONTROL Rollen]** Registerkarte.

## Nächste Schritte

Nachdem Sie eine neue Rolle erstellt haben, können Sie mit dem nächsten Schritt fortfahren, um [Berechtigungen für eine Rolle verwalten](permissions.md).
