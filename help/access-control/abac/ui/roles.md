---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;attributbasierte Zugriffssteuerung;ABAC
title: Attributbasierte Zugriffssteuerung - Rolle erstellen
description: Dieses Dokument enthält Informationen zum Verwalten von Rollen über die Benutzeroberfläche „Berechtigungen“ in Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 31%

---

# Verwalten von Rollen

Rollen definieren den Zugriff, den Admins, Fachleute oder Endbenutzende auf Ressourcen in Ihrer Organisation haben. In einer rollenbasierten Zugriffssteuerungsumgebung erfolgt die Bereitstellung des Benutzerzugriffs über gemeinsame Zuständigkeiten und Anforderungen. Eine Rolle verfügt über bestimmte Berechtigungen, wobei Mitglieder Ihrer Organisation je nach dem Umfang des Lese- oder Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden können.

## Erstellen einer neuen Rolle {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Erstellen einer neuen Rolle"
>abstract="Erstellen Sie neue Rollen, um Benutzende, die mit Ihrer Experience Platform-Instanz interagieren, besser zu kategorisieren. Sie können beispielsweise eine Rolle für ein internes Marketing-Team erstellen und auf diese Rolle die Kennzeichnung „RHD“ (Regulated Health Data, regulierte Gesundheitsdaten) anwenden, sodass Ihr internes Marketing-Team auf PHI-Daten (Protected Health Information, geschützte Gesundheitsinformationen) zugreifen kann. Alternativ können Sie auch eine Rolle für eine externe Agentur erstellen und ihr diesen Rollenzugriff auf PHI-Daten verweigern, indem Sie die RHD-Kennzeichnung nicht auf diese Rolle anwenden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=de" text="Verwalten einer Rolle"
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="Anwenden von Kennzeichnungen auf eine Rolle"

Um eine neue Rolle zu erstellen, wählen Sie die Registerkarte **[!UICONTROL Roles]** in der Seitenleiste aus und klicken Sie auf **[!UICONTROL Create Role]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

Das Dialogfeld **[!UICONTROL Create a new role]** wird angezeigt, in dem Sie aufgefordert werden, einen Namen und eine optionale Beschreibung einzugeben.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Confirm]** aus.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Wählen Sie anschließend mithilfe des Dropdown-Menüs die Ressourcenberechtigungen aus, die Sie in die Rolle aufnehmen möchten.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Um zusätzliche Ressourcen hinzuzufügen, wählen Sie **[!UICONTROL Adobe Experience Platform]** im linken Navigationsbereich aus, der eine Liste mit Ressourcen anzeigt. Geben Sie alternativ den Ressourcennamen in die Suchleiste im linken Navigationsbereich ein.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Klicken und ziehen Sie die entsprechende Ressource in das Hauptbedienfeld.

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

Wählen Sie mithilfe des Dropdown-Menüs die Ressourcenberechtigungen aus, die Sie in die Rolle aufnehmen möchten. Wiederholen Sie dies für alle Ressourcen, die Sie für die Rolle einbeziehen möchten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Save and exit]** aus.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

Die neue Rolle wurde erfolgreich erstellt und Sie werden zur Seite **[!UICONTROL Roles]** weitergeleitet, wo die neu erstellte Rolle in der Liste angezeigt wird.

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

Weitere Informationen zum Verwalten [&#x200B; Rollenberechtigungen nach deren Erstellung finden &#x200B;](#manage-permissions-for-a-role) in den Abschnitten zum Verwalten von Berechtigungen für eine Rolle .

Im folgenden Video erfahren Sie, wie Sie eine neue Rolle erstellen und Benutzer für diese Rolle verwalten.

>[!VIDEO](https://video.tv.adobe.com/v/3475982/?captions=ger&learn=on)

## Duplizieren einer Rolle

Um eine vorhandene Rolle zu duplizieren, wählen Sie die Rolle auf der Registerkarte **[!UICONTROL Roles]** aus. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Rolle zu finden, die Sie duplizieren möchten.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Wählen Sie als Nächstes oben rechts im Bildschirm **[!UICONTROL Duplicate]** aus.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

Das Dialogfeld **[!UICONTROL Duplicate role]** wird angezeigt, in dem Sie aufgefordert werden, die Duplizierung zu bestätigen.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Als Nächstes gelangen Sie zur Detailseite der Rolle, auf der Sie den Namen und die Berechtigungen für die Rolle ändern können. Die Details, Beschriftungen und Sandboxes werden aus der vorherigen Rolle dupliziert. Benutzer müssen über die Registerkarte Benutzer hinzugefügt werden. Sie können das Dokument [Berechtigungen für eine Rolle verwalten](permissions.md) anzeigen, um mehr über das Hinzufügen von Details, Beschriftungen, Sandboxes und Benutzern zu einer Rolle zu erfahren.

Klicken Sie auf den Pfeil nach links, um zur Registerkarte **[!UICONTROL Roles]** zurückzukehren.

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

Die neue Rolle wird in der Liste auf der Seite **[!UICONTROL Roles]** angezeigt.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Löschen einer Rolle

Klicken Sie auf das Auslassungszeichen (`…`) neben dem Namen einer Rolle. In einem Dropdown-Menü werden dann Steuerelemente zum Bearbeiten, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie im Dropdown-Menü die Option „Löschen“ aus.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

Das Dialogfeld **[!UICONTROL Delete user role]** wird angezeigt, in dem Sie aufgefordert werden, den Löschvorgang zu bestätigen.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Sie werden zur Registerkarte **[!UICONTROL Roles]** zurückgeleitet.

## Nächste Schritte

Nachdem eine neue Rolle erstellt wurde, können Sie mit dem nächsten Schritt fortfahren, um [Berechtigungen für eine Rolle verwalten](permissions.md).
