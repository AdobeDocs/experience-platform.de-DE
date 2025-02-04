---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;attributbasierte Zugriffssteuerung;ABAC
title: Attributbasierte Zugriffssteuerung − Rollenberechtigungen verwalten
description: Dieses Dokument enthält Informationen dazu, wie Berechtigungen für eine Rolle über die Benutzeroberfläche „Berechtigungen“ in Adobe Experience Cloud konfiguriert werden
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 207317d16a21cc2461ebd3f7867735735227c173
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 35%

---

# Verwalten der Berechtigungen für eine Rolle {#manage-role-permissions}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Was sind Rollen?"
>abstract="Rollen definieren den Zugriff, den ein Administrator, ein Spezialist oder ein Endbenutzer auf Ressourcen in Ihrer Organisation hat. Sie kategorisieren die Benutzer, die mit Ihrer Platform-Instanz interagieren, und sind die Bausteine von Richtlinien zur Zugriffssteuerung. Eine Rolle verfügt über bestimmte Berechtigungen, wobei Mitglieder Ihrer Organisation je nach dem Umfang des Lese- oder Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden können."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=de" text="Verwalten von Rollen"

>[!IMPORTANT]
>
>Die Zugriffssteuerung verwendet die Benutzer-ID (eine interne eindeutige ID, die einem Benutzer zugewiesen ist) zum Gewähren von Berechtigungen. Wenn eine Organisation von Adobe ID zu Business ID migriert wird, gehen alle für ihre Benutzer festgelegten Berechtigungen verloren, da sich die Benutzer-ID ändert und die Zugriffssteuerung die neu generierte Benutzer-ID verwendet. Wenn Ihre Organisation zu Business ID migriert wird, wenden Sie sich an den Adobe-Support-Mitarbeiter, um Ihre Benutzer-ID von Adobe ID zu Business ID zu migrieren.

Berechtigungen sind der Bereich von Experience Cloud, in dem Admins Benutzerrollen und Zugriffsrichtlinien definieren können, um Zugriffsberechtigungen für Funktionen und Objekte in einem Produktprogramm zu verwalten.

Über Berechtigungen können Sie Rollen erstellen und verwalten sowie die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen. Mit Berechtigungen können Sie auch die Bezeichnungen, Sandboxes und Benutzende verwalten, die einer bestimmten Rolle zugeordnet sind. 

Nach dem [Erstellen einer neuen Rolle](#create-a-new-role) werden Sie sofort zur Registerkarte **[!UICONTROL Rollen]** zurückgeleitet. Wenn Sie Berechtigungen für eine vorhandene Rolle bearbeiten, wählen Sie die Rolle auf der Registerkarte **[!UICONTROL Rollen]** aus. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und nach einer Rolle zu suchen.

## Filtern von Rollen

Wählen Sie das Trichtersymbol (![Filtersymbol](/help/images/icons/filter.png)) aus, um eine Liste von Filterfeldern anzuzeigen, mit denen die Ergebnisse eingegrenzt werden können.

![Das Rollen-Dashboard in der Benutzeroberfläche „Berechtigungen“ mit hervorgehobenem Abschnitt „Rollen filtern“.](../../images/flac-ui/flac-filters.png)

In der Benutzeroberfläche sind folgende Filter für Rollen verfügbar:

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Erstellt zwischen] | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. |
| [!UICONTROL Erstellt von] | Filtern Sie nach dem Rollenersteller, indem Sie einen Benutzer aus der Dropdown-Liste auswählen. |
| [!UICONTROL Geändert zwischen] | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. |
| [!UICONTROL Geändert von] | Filtern Sie nach dem Rollenmodifikator, indem Sie einen Benutzer aus der Dropdown-Liste auswählen. |

Um einen Filter zu entfernen, klicken Sie auf das „X“ auf dem Symbol für den betreffenden Filter, oder wählen Sie **[!UICONTROL Alle löschen]** aus, um alle Filter zu entfernen.

![Das Rollen -Dashboard in der Benutzeroberfläche „Berechtigungen“ mit dem hervorgehobenen „X“ und „Alle Auswahlen löschen“ in den ausgewählten Filtern.](../../images/flac-ui/flac-clear-filters.png)

## Rollendetails {#role-details}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Rollenübersicht"
>abstract="Das Dialogfeld „Rollenübersicht“ zeigt die Details der Rolle an, einschließlich der Ressourcen und Sandboxes, auf die eine bestimmte Rolle zugreifen darf. Sie können Beschriftungen, Benutzer, Benutzergruppen und API-Anmeldeinformationen für die Rolle verwalten, indem Sie zur entsprechenden Registerkarte im Arbeitsbereich der Rolle navigieren."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-labels-for-a-role" text="Verwalten von Beschriftungen für eine Rolle"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-users-for-a-role" text="Verwalten von Benutzern für eine Rolle"

Wählen Sie auf der Registerkarte **[!UICONTROL Rollen]** die Rolle aus. Daraufhin wird das Dashboard [!UICONTROL Details] der Rolle geöffnet.

![Der Arbeitsbereich „Details“ für die ausgewählte Rolle wird mit hervorgehobenen Übersichtsinformationen angezeigt.](../../images/flac-ui/flac-details.png)

Das [!UICONTROL Details]-Dashboard bietet einen Überblick über die Rolle. In der Übersicht werden der Rollenname, die Beschreibung, der Ersteller und der letzte Modifikator sowie das Erstellungs- und Änderungsdatum angezeigt. Außerdem werden die mit der Rolle verbundenen Berechtigungen und die Liste der zugewiesenen Sandboxes angezeigt. Der Rollenname und die Beschreibung können bei Bedarf geändert werden.

## Verwalten von Beschriftungen für eine Rolle

Wählen Sie die Registerkarte **[!UICONTROL Bezeichnungen]** aus, um den Arbeitsbereich für Rollenbezeichnungen zu öffnen, und wählen Sie **[!UICONTROL Beschriftungen hinzufügen]** aus, um der Rolle Beschriftungen zuzuweisen.

![Der Arbeitsbereich Beschriftungen der Rolle wird angezeigt, wobei die Registerkarte Beschriftungen und die Schaltfläche Beschriftungen hinzufügen hervorgehoben sind.](../../images/flac-ui/flac-labels.png)

Das **[!UICONTROL Anwenden von Zugriffs- und Data Governance]** Beschriftungen“ wird angezeigt, das eine Liste von Beschriftungen enthält. In der Liste werden der Name der Beschriftung, der Anzeigename, die Kategorie und die Beschreibung angezeigt.

Wählen Sie in der Liste die Beschriftungen aus, die Sie der Rolle hinzufügen möchten, und klicken Sie dann auf **[!UICONTROL Speichern]**.

![Der Dialog „Zugriff anwenden“ und „Data Governance-Beschriftungen“ mit einer ausgewählten Beschriftung.](../../images/flac-ui/flac-add-labels.png)

Hinzugefügte Beschriftungen werden auf der Registerkarte **[!UICONTROL Beschriftungen]** angezeigt.

![Der Arbeitsbereich „Beschriftungen“ der Rolle mit hervorgehobener hinzugefügter Beschriftung.](../../images/flac-ui/flac-added-labels.png)

Um eine Beschriftung von einer Rolle zu entfernen, wählen Sie die Beschriftung aus und klicken Sie dann auf **[!UICONTROL Beschriftungen entfernen]**.

![Der Arbeitsbereich „Beschriftungen“ der Rolle, wobei eine Rolle ausgewählt ist und die Option „Beschriftungen entfernen“ hervorgehoben ist.](../../images/flac-ui/flac-delete-labels.png)

## Verwalten von Sandboxes für eine Rolle

Wählen Sie die **[!UICONTROL Details]** aus und navigieren Sie zum Abschnitt **[!UICONTROL Sandboxes]**. Wählen Sie **[!UICONTROL Alle anzeigen]** aus, um die vollständige Liste der der Rolle hinzugefügten Sandboxes anzuzeigen.

![Der Arbeitsbereich „Details“ der Rolle mit hervorgehobenem Abschnitt „Sandboxes“.](../../images/flac-ui/flac-sandboxes.png)

Um einer Rolle weitere Sandboxes hinzuzufügen, wählen Sie **[!UICONTROL Bearbeiten]** oben rechts in der Benutzeroberfläche aus.

![Der Arbeitsbereich „Details“ der Rolle mit hervorgehobener Option „Bearbeiten“.](../../images/flac-ui/flac-add-sandboxes.png)

Im nächsten Bildschirm werden Sie aufgefordert, über die Dropdown-Liste auszuwählen, welche Sandbox-Ressourcen in die Rolle aufgenommen werden sollen. Klicken Sie abschließend auf **[!UICONTROL Speichern]** und dann auf **[!UICONTROL Schließen]**.

![Das Ressourcen-Dashboard der Rolle mit hervorgehobenem Dropdown-Menü „Sandbox-Ressourcen“.](../../images/flac-ui/flac-add-role-permission.png)

## Verwalten von Benutzern für eine Rolle

Wählen Sie die Registerkarte **[!UICONTROL Benutzer]** aus, um die Rollen [!UICONTROL Benutzer] zu öffnen, und klicken Sie dann auf **[!UICONTROL Benutzer hinzufügen]**, um der Rolle Benutzer zuzuweisen.

![Der Arbeitsbereich Benutzer der Rolle wird angezeigt, wobei die Registerkarte Benutzer und die Option Benutzer hinzufügen hervorgehoben sind.](../../images/flac-ui/flac-users.png)

Das **[!UICONTROL „Benutzer hinzufügen]** wird angezeigt. Wählen Sie die Benutzenden aus der Liste aus, die Sie der Rolle hinzufügen möchten. Alternativ können Sie in der Suchleiste nach dem Benutzer suchen, indem Sie dessen Namen oder E-Mail-Adresse eingeben. Klicken Sie dann auf **[!UICONTROL Speichern]**.

![Das Dialogfeld „Benutzer hinzufügen“ mit ausgewähltem Benutzer und hervorgehobener Suchleiste und Speicheroption.](../../images/flac-ui/flac-add-users.png)

Hinzugefügte Benutzer erscheinen auf der Registerkarte **[!UICONTROL Benutzer]**.

![Der Arbeitsbereich Benutzer der Rolle mit den zur Rolle hinzugefügten Benutzern.](../../images/flac-ui/flac-added-users.png)

Um einen Benutzer aus einer Rolle zu entfernen, klicken Sie auf das Symbol **X** neben dem Namen des Benutzers.

![Der Arbeitsbereich „Benutzer“ der Rolle, in dem ein Benutzer mit hervorgehobener Option „X“ angezeigt wird.](../../images/flac-ui/flac-remove-users.png)

Im folgenden Video erfahren Sie, wie Sie eine neue Rolle erstellen und Benutzer für diese Rolle verwalten.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Verwalten von API-Anmeldeinformationen für eine Rolle {#manage-api-credentials-for-role}

>[!IMPORTANT]
>
> Um API-Anmeldeinformationen in „Berechtigungen[!UICONTROL  verwenden ] verwalten zu können, müssen Benutzerinnen und Benutzer über Systemadministratorrechte verfügen.

Um Experience Platform-APIs als Anwender oder Entwickler verwenden zu können, muss ein Systemadministrator zusätzlich zu den einer Rolle zugewiesenen Berechtigungen API-Anmeldeinformationen hinzufügen. Eine vollständige Anleitung zum Erstellen und Zuweisen von API-Anmeldeinformationen sowie die erforderlichen Berechtigungen finden Sie im schrittweisen Tutorial unter [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md#generate-credentials).

Wählen Sie die Registerkarte **[!UICONTROL API-Anmeldeinformationen]** aus, um den Arbeitsbereich mit den Rollen-API-Anmeldeinformationen zu öffnen, und wählen Sie **[!UICONTROL API-Anmeldeinformationen hinzufügen]** aus, um der Rolle API-Anmeldeinformationen zuzuweisen.

![Der Arbeitsbereich mit den API-Anmeldeinformationen der Rolle mit hervorgehobener Option „Anmeldeinformationen hinzufügen“.](../../images/flac-ui/flac-api-credentials.png)

Das **[!UICONTROL API-Anmeldeinformationen hinzufügen]** wird angezeigt. Wählen Sie API-Anmeldeinformationen aus der Liste aus, um der Rolle hinzuzufügen, und wählen Sie dann **[!UICONTROL Speichern]**

![Das Dialogfeld „API-Anmeldeinformationen hinzufügen“ mit ausgewählten Anmeldeinformationen und hervorgehobener Option „Speichern“.](../../images/flac-ui/flac-add-api-credentials.png)

Hinzugefügte API-Anmeldeinformationen erscheinen auf **[!UICONTROL Registerkarte]** API-Anmeldeinformationen“.

![Der Arbeitsbereich mit den API-Anmeldeinformationen der Rolle mit den hinzugefügten Anmeldeinformationen wird angezeigt.](../../images/flac-ui/flac-added-api-credentials.png)

Um API-Anmeldeinformationen aus einer Rolle zu entfernen, klicken Sie auf das Symbol **X** neben dem Namen der API-Anmeldeinformationen.

![Der Arbeitsbereich mit den API-Anmeldeinformationen der Rolle, wobei die Option X zum Entfernen einer Anmeldeinformation hervorgehoben ist.](../../images/flac-ui/flac-remove-api-credentials.png)

Das **[!UICONTROL API-Anmeldeinformationen entfernen]** wird angezeigt, in dem Sie aufgefordert werden, den Löschvorgang zu bestätigen. Wählen Sie **[!UICONTROL Bestätigen]** aus, um das Entfernen der ausgewählten Berechtigung abzuschließen.

![Das Popup zum Entfernen von Anmeldeinformationen, in dem Sie aufgefordert werden zu bestätigen, dass das Entfernen der Anmeldeinformationen hervorgehoben ist.](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Sie werden zur Registerkarte **[!UICONTROL API-Anmeldedaten]** zurückgeleitet.

## Verwalten von Benutzergruppen für eine Rolle

Benutzergruppen sind mehrere Benutzer, die gruppiert wurden und Zugriff haben, um dieselben Funktionen auszuführen.

Wählen Sie die **[!UICONTROL Benutzergruppen]** aus, um den Arbeitsbereich Benutzergruppen der Rolle zu öffnen, und wählen Sie dann **[!UICONTROL Gruppen hinzufügen]**, um der Rolle Benutzergruppen zuzuweisen.

![Der Arbeitsbereich Benutzergruppen der Rolle mit der Option Gruppen hinzufügen ](../../images/flac-ui/flac-user-groups.png)

Das **[!UICONTROL Gruppen hinzufügen]** wird angezeigt. Wählen Sie aus der Liste die Benutzergruppen aus, die Sie der Rolle hinzufügen möchten. Alternativ können Sie über die Suchleiste nach der Benutzergruppe suchen, indem Sie den Namen der Gruppe eingeben. Klicken Sie dann auf **[!UICONTROL Speichern]**.

![Das Dialogfeld „Gruppen hinzufügen“ mit einer ausgewählten Benutzergruppe und der hervorgehobenen Option „Suchen und Speichern“.](../../images/flac-ui/flac-add-user-groups.png)

Hinzugefügte Benutzergruppe erscheinen auf der Registerkarte **[!UICONTROL Benutzergruppen]**.

![Der Arbeitsbereich Benutzergruppen der Rolle zeigt die Liste der hinzugefügten Benutzergruppen an.](../../images/flac-ui/flac-added-user-groups.png)

Um eine Benutzergruppe aus einer Rolle zu entfernen, wählen Sie das Symbol **X** neben dem Namen der Benutzergruppe aus.

![Der Arbeitsbereich Benutzergruppen der Rolle, wobei die Option X zum Entfernen einer bestimmten Benutzergruppe hervorgehoben ist.](../../images/flac-ui/flac-remove-user-groups.png)

Der **[!UICONTROL Benutzergruppe entfernen]** erscheint, in dem Sie aufgefordert werden, den Löschvorgang zu bestätigen. Klicken Sie **[!UICONTROL Bestätigen]**, um die ausgewählte Benutzergruppe zu entfernen.

![Das Popup zum Entfernen einer Benutzergruppe wird angezeigt und hervorgehoben.](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Sie werden zur Registerkarte **[!UICONTROL Benutzergruppen]** zurückgeleitet.

## Benutzer zum Experience Platform hinzufügen

Als Systemadministrator können Sie einem Benutzer Entwicklerzugriff gewähren, damit er in der Adobe Developer Console [Integrationen ](../../../landing/api-authentication.md#generate-credentials) kann.

Um eine Benutzer-Experience Platform hinzuzufügen, melden Sie sich bei der Admin Console [](https://adminconsole.adobe.com) an und wählen Sie **[!UICONTROL Benutzer hinzufügen]** aus.

![Das Adobe Admin Console-Dashboard mit hervorgehobener Option „Benutzer hinzufügen“.](../../images/flac-ui/product-profile-add-users.png)

Das Dialogfeld **[!UICONTROL Benutzer zum Team hinzufügen]** wird angezeigt. Geben Sie die E-Mail-Adresse, den Vornamen (optional) und den Nachnamen (optional) des Benutzers ein. Wählen Sie dann **[!UICONTROL Produkte]** aus.

![Das Dialogfeld „Benutzer zum Team hinzufügen“ mit hervorgehobener Option „Benutzerfelder und Produkte“.](../../images/flac-ui/product-profile-add-users-to-your-team.png)

Das **[!UICONTROL Produkte auswählen]** wird angezeigt. **[!UICONTROL Adobe Experience Platform]**.

![Das Dialogfeld „Produkte auswählen“ mit hervorgehobener Option &quot;Adobe Experience Platform&quot;.](../../images/flac-ui/product-profile-select-product.png)

Das **[!UICONTROL Produktprofile auswählen]** wird angezeigt. Wählen Sie **[!UICONTROL AEP-Default-All-Users]** und dann **[!UICONTROL Speichern]** aus.

![Das Dialogfeld „Produktprofile auswählen“ mit hervorgehobener Option „AEP-Default-All-Users“ und „Apply“.](../../images/flac-ui/product-profile-select-product-profiles.png)

Überprüfen Sie die Informationen und wählen Sie dann **[!UICONTROL Speichern]** aus, um den Benutzer hinzuzufügen.

![Der Dialog Benutzer zu Ihrem Team hinzufügen mit den Benutzerinformationen und ausgewählten Auswahlen und der hervorgehobenen Option „Speichern“.](../../images/flac-ui/product-profile-save-user.png)

## Nächste Schritte

Nachdem Sie die Berechtigungen festgelegt haben, können Sie mit dem nächsten Schritt, [Benutzer verwalten](users.md), fortfahren.
