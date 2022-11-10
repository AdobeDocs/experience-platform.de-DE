---
keywords: Experience Platform; Startseite; beliebte Themen; Zugriffskontrolle; attributbasierte Zugriffskontrolle; ABAC
title: Attributbasierte Zugriffssteuerung Erstellen einer Richtlinie
description: Dieses Dokument enthält Informationen zum Verwalten von Richtlinien über die Benutzeroberfläche "Berechtigungen"in Adobe Experience Cloud
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 1a755fa5480e036bde50617f01440cfabbaf64c2
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# Richtlinien verwalten

Richtlinien sind Aussagen, die Attribute zusammenbringen, um zulässige und unzulässige Handlungen festzustellen. Richtlinien können lokal oder global sein und andere Richtlinien überschreiben.

## Neue Richtlinie erstellen

Um eine neue Richtlinie zu erstellen, wählen Sie die **[!UICONTROL Richtlinien]** Registerkarte in der Seitenleiste und wählen Sie **[!UICONTROL Richtlinie erstellen]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

Die **[!UICONTROL Neue Richtlinie erstellen]** angezeigt, in dem Sie aufgefordert werden, einen Namen und eine optionale Beschreibung einzugeben. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Bestätigen]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Wählen Sie mithilfe des Dropdown-Pfeils aus, ob Sie **Zugriff auf** (![flac-permission-access-to](../../images/flac-ui/flac-permit-access-to.png)) eine Ressource oder **Zugriff auf verweigern** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) eine Ressource.

Wählen Sie anschließend über das Dropdown-Menü die Ressource aus, die Sie in die Richtlinie aufnehmen möchten, und suchen Sie nach dem Zugriffstyp (Lesen oder Schreiben).

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Wählen Sie anschließend mithilfe des Dropdown-Pfeils die Bedingung aus, die Sie auf diese Richtlinie anwenden möchten. **Folgendes ist wahr** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) oder **Folgendes ist falsch** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Wählen Sie das Pluszeichen aus, um **Ausdruck für Übereinstimmungen hinzufügen** oder **Ausdrucksgruppe hinzufügen** für die Ressource.

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Wählen Sie mithilfe des Dropdown-Menüs die **Ressource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Wählen Sie anschließend mithilfe der Dropdown-Liste die **Stimmt überein mit**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Wählen Sie anschließend mithilfe des Dropdown-Menüs den Titel (**[!UICONTROL Core-Bezeichnung]** oder **[!UICONTROL Eigene Bezeichnung]**), um die dem Benutzer in den Rollen zugewiesene Bezeichnung zu übernehmen.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Wählen Sie abschließend die **Sandbox** die mithilfe des Dropdown-Menüs angewendet werden sollen.

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Auswählen **Ressource hinzufügen** , um weitere Ressourcen hinzuzufügen. Wählen Sie nach Abschluss **[!UICONTROL Speichern und beenden]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Die neue Richtlinie wurde erfolgreich erstellt und Sie werden zum **[!UICONTROL Richtlinien]** -Registerkarte, wo die neu erstellte Richtlinie in der Liste angezeigt wird.

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Richtlinie bearbeiten

Um eine vorhandene Richtlinie zu bearbeiten, wählen Sie die Richtlinie aus dem **[!UICONTROL Richtlinien]** Registerkarte. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Richtlinie zu finden, die Sie bearbeiten möchten.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Wählen Sie als Nächstes die Auslassungszeichen (`…`) neben dem Richtliniennamen und in einem Dropdown-Menü werden Steuerelemente zum Bearbeiten, Deaktivieren, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie im Dropdown-Menü Bearbeiten aus.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

Der Bildschirm &quot;Richtlinienberechtigungen&quot;wird angezeigt. Nehmen Sie die Aktualisierungen vor und wählen Sie **[!UICONTROL Speichern und beenden]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Die Richtlinie wurde erfolgreich aktualisiert und Sie werden zum **[!UICONTROL Richtlinien]** Registerkarte.

## Richtlinie duplizieren

Um eine vorhandene Richtlinie zu duplizieren, wählen Sie die Richtlinie aus dem **[!UICONTROL Richtlinien]** Registerkarte. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Richtlinie zu finden, die Sie bearbeiten möchten.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Wählen Sie als Nächstes die Auslassungszeichen (`…`) neben einem Richtliniennamen und in einem Dropdown-Menü werden Steuerelemente zum Bearbeiten, Deaktivieren, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie Duplikat aus der Dropdown-Liste aus.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

Die **[!UICONTROL Richtlinie duplizieren]** angezeigt, in dem Sie aufgefordert werden, die Duplizierung zu bestätigen.

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Die neue Richtlinie wird in der Liste als Kopie des Originals auf der **[!UICONTROL Richtlinien]** Registerkarte.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Löschen einer Richtlinie

Um eine vorhandene Richtlinie zu löschen, wählen Sie die Richtlinie aus dem **[!UICONTROL Richtlinien]** Registerkarte. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Richtlinie zu finden, die Sie löschen möchten.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Wählen Sie als Nächstes die Auslassungszeichen (`…`) neben einem Richtliniennamen und in einem Dropdown-Menü werden Steuerelemente zum Bearbeiten, Deaktivieren, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie Löschen aus der Dropdown-Liste aus.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

Die **[!UICONTROL Benutzerrichtlinie löschen]** angezeigt, in dem Sie aufgefordert werden, den Löschvorgang zu bestätigen.

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

Sie kehren zum **[!UICONTROL policies]** und ein Popup-Fenster zum Löschen wird angezeigt.

![flac-policy-delete-validation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## Richtlinie aktivieren

Um eine vorhandene Richtlinie zu aktivieren, wählen Sie die Richtlinie aus dem **[!UICONTROL Richtlinien]** Registerkarte. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und die Richtlinie zu finden, die Sie löschen möchten.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Wählen Sie als Nächstes die Auslassungszeichen (`…`) neben einem Richtliniennamen und in einem Dropdown-Menü werden Steuerelemente zum Bearbeiten, Aktivieren, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie im Dropdown-Menü Aktivieren aus.

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

Die **[!UICONTROL Benutzerrichtlinie aktivieren]** angezeigt, in dem Sie aufgefordert werden, die Aktivierung zu bestätigen.

![flac-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

Sie kehren zum **[!UICONTROL policies]** und ein Aktivierungs-Pop-over wird angezeigt. Der Richtlinienstatus wird als aktiv angezeigt.

![flac-policy-activated](../../images/flac-ui/flac-policy-activated.png)

## Nächste Schritte

Nachdem Sie eine neue Richtlinie erstellt haben, können Sie mit dem nächsten Schritt fortfahren, um [Berechtigungen für eine Rolle verwalten](permissions.md).
