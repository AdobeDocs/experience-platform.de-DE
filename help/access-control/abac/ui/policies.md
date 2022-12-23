---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;attributbasierte Zugriffssteuerung;ABAC
title: Richtlinien zur Zugriffssteuerung verwalten
description: Dieses Dokument enthält Informationen zum Verwalten von Zugriffskontrollrichtlinien über die Benutzeroberfläche "Berechtigungen"in Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 86%

---

# Richtlinien zur Zugriffskontrolle verwalten

Zugriffskontrollrichtlinien sind Anweisungen, die Attribute zusammenführen, um zulässige und unzulässige Maßnahmen festzulegen. Zugriffsrichtlinien können entweder lokal oder global sein und andere Richtlinien überschreiben.

>[!IMPORTANT]
>
>Zugriffsrichtlinien dürfen nicht mit Datennutzungsrichtlinien verwechselt werden, die steuern, wie Daten in Adobe Experience Platform verwendet werden, anstatt welche Benutzer in Ihrem Unternehmen Zugriff darauf haben. Siehe Handbuch zum Erstellen [Datennutzungsrichtlinien](../../../data-governance/policies/create.md) für weitere Informationen.

## Erstellen einer neuen Richtlinie

Um eine neue Richtlinie zu erstellen, wählen Sie die Registerkarte **[!UICONTROL Richtlinien]** in der Seitenleiste aus und klicken Sie auf **[!UICONTROL Richtlinie erstellen]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

Das Dialogfeld **[!UICONTROL Neue Richtlinie erstellen]** wird angezeigt, in dem Sie aufgefordert werden, einen Namen und eine optionale Beschreibung einzugeben. Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Bestätigen]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Wählen Sie mithilfe des Dropdown-Pfeils aus, ob Sie **Zugriff auf eine Ressource zulassen** (![flac-permission-access-to](../../images/flac-ui/flac-permit-access-to.png)) oder **Zugriff auf eine Ressource verweigern** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) möchten.

Wählen Sie anschließend über das Dropdown-Menü die Ressource aus, die Sie in die Richtlinie aufnehmen möchten, und suchen Sie nach dem Zugriffstyp (Lesen oder Schreiben).

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Wählen Sie anschließend mithilfe des Dropdown-Pfeils die Bedingung aus, die Sie auf diese Richtlinie anwenden möchten: **Folgendes ist wahr** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) oder **Folgendes ist falsch** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Klicken Sie auf das Pluszeichen, um für die Ressource einen **Ausdruck für Übereinstimmungen** oder eine **Ausdrucksgruppe** hinzuzufügen.

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Wählen Sie mithilfe des Dropdown-Menüs die **Ressource** aus.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Wählen Sie anschließend mithilfe des Dropdown-Menüs die **Übereinstimmungen** aus.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Wählen Sie anschließend mithilfe des Dropdown-Menüs den Titel (**[!UICONTROL Core-Bezeichnung]** oder **[!UICONTROL Benutzerdefinierte Bezeichnung]**) aus, sodass er mit der dem Benutzer in den Rollen zugewiesenen Bezeichnung übereinstimmt.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Wählen Sie abschließend mithilfe des Dropdown-Menüs die **Sandbox** aus, auf die die Richtlinienbedingungen angewendet werden sollen.

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Wählen Sie **Ressource hinzufügen** aus, um weitere Ressourcen hinzuzufügen. Klicken Sie dann auf **[!UICONTROL Speichern und beenden]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Die neue Richtlinie wurde erfolgreich erstellt, und Sie werden zur Registerkarte **[!UICONTROL Richtlinien]** weitergeleitet, wo die neu erstellte Richtlinie in der Liste angezeigt wird.

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Bearbeiten einer Richtlinie

Um eine vorhandene Richtlinie zu bearbeiten, wählen Sie die Richtlinie auf der Registerkarte **[!UICONTROL Richtlinien]** aus. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Richtlinie zu finden, die Sie bearbeiten möchten.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Klicken Sie als Nächstes auf das Auslassungszeichen (`…`) neben dem Richtliniennamen. In einem Dropdown-Menü werden dann Steuerelemente zum Bearbeiten, Deaktivieren, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie „Bearbeiten“ aus dem Dropdown-Menü aus.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

Der Bildschirm „Richtlinienberechtigungen“ wird angezeigt. Nehmen Sie die Aktualisierungen vor und klicken Sie auf **[!UICONTROL Speichern und beenden]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Die Richtlinie wurde erfolgreich aktualisiert, und Sie werden zur Registerkarte **[!UICONTROL Richtlinien]** weitergeleitet.

## Duplizieren einer Richtlinie

Um eine vorhandene Richtlinie zu duplizieren, wählen Sie die Richtlinie auf der Registerkarte **[!UICONTROL Richtlinien]** aus. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Richtlinie zu finden, die Sie bearbeiten möchten.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Klicken Sie als Nächstes auf das Auslassungszeichen (`…`) neben einem Richtliniennamen. In einem Dropdown-Menü werden dann Steuerelemente zum Bearbeiten, Deaktivieren, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie „Duplizieren“ aus dem Dropdown-Menü aus.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

Das Dialogfeld **[!UICONTROL Richtlinie duplizieren]** wird angezeigt, in dem Sie aufgefordert werden, die Duplizierung zu bestätigen.

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Die neue Richtlinie wird in der Liste auf der Registerkarte **[!UICONTROL Richtlinien]** als Kopie des Originals angezeigt.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Löschen einer Richtlinie

Um eine vorhandene Richtlinie zu löschen, wählen Sie die Richtlinie auf der Registerkarte **[!UICONTROL Richtlinien]** aus. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Richtlinie zu finden, die Sie löschen möchten.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Klicken Sie als Nächstes auf das Auslassungszeichen (`…`) neben einem Richtliniennamen. Daraufhin werden in einem Dropdown-Menü Steuerelemente zum Bearbeiten, Deaktivieren, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie im Dropdown-Menü die Option „Löschen“ aus.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

Das Dialogfeld **[!UICONTROL Benutzerrichtlinie löschen]** wird angezeigt, in dem Sie aufgefordert werden, den Löschvorgang zu bestätigen.

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

Sie kehren zur Registerkarte **[!UICONTROL Richtlinien]** zurück, und ein Popup-Fenster mit einer Bestätigung des Löschvorgangs wird angezeigt.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## Aktivieren von Richtlinien

Um eine vorhandene Richtlinie zu aktivieren, wählen Sie die Richtlinie auf der Registerkarte **[!UICONTROL Richtlinien]** aus. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Richtlinie zu finden, die Sie löschen möchten.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Klicken Sie als Nächstes auf das Auslassungszeichen (`…`) neben einem Richtliniennamen. Daraufhin werden in einem Dropdown-Menü Steuerelemente zum Bearbeiten, Aktivieren, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie im Dropdown-Menü die Option „Aktivieren“ aus.

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

Das Dialogfeld **[!UICONTROL Benutzerrichtlinie aktivieren]** wird angezeigt, in dem Sie aufgefordert werden, die Aktivierung zu bestätigen.

![flac-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

Sie kehren zur Registerkarte **[!UICONTROL Richtlinien]** zurück, und ein Popup-Fenster mit einer Bestätigung der Aktivierung wird angezeigt. Als Richtlinienstatus wird „aktiv“ angegeben.

![flac-policy-activated](../../images/flac-ui/flac-policy-activated.png)

## Nächste Schritte

Nachdem eine neue Richtlinie erstellt wurde, können Sie im nächsten Schritt mit dem [Verwalten der Berechtigungen für eine Rolle](permissions.md) fortfahren.
