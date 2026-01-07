---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;attributbasierte Zugriffssteuerung;ABAC
title: Attributbasierte Zugriffssteuerung − Rollenberechtigungen verwalten
description: Erfahren Sie, wie Sie Rollen über die Benutzeroberfläche „Berechtigungen“ in Adobe Experience Cloud konfigurieren.
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 157fb27ae492971a48ad62c2d6b3eddd674167f4
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 36%

---

# Verwalten der Berechtigungen für eine Rolle {#manage-role-permissions}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Was sind Rollen?"
>abstract="Rollen definieren den Zugriff, den Admins, Fachleute oder Endbenutzende auf Ressourcen in Ihrer Organisation haben. Sie kategorisieren die Benutzenden, die mit Ihrer Experience Platform-Instanz interagieren, und sind die Bausteine der Richtlinien zur Zugriffssteuerung. Eine Rolle verfügt über bestimmte Berechtigungen, wobei Mitglieder Ihrer Organisation je nach dem Umfang des Lese- oder Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden können."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=de" text="Verwalten von Rollen"

>[!IMPORTANT]
>
>Die Zugriffssteuerung verwendet die Benutzer-ID (eine interne eindeutige ID, die einem Benutzer zugewiesen ist) zum Gewähren von Berechtigungen. Wenn eine Organisation von Adobe ID zu Business ID migriert wird, gehen alle für ihre Benutzer festgelegten Berechtigungen verloren, da sich die Benutzer-ID ändert und die Zugriffssteuerung die neu generierte Benutzer-ID verwendet. Wenn Ihre Organisation zu Business ID migriert wird, wenden Sie sich an den Adobe-Support-Mitarbeiter, um Ihre Benutzer-ID von Adobe ID zu Business ID zu migrieren.

Berechtigungen sind der Bereich von Experience Cloud, in dem Admins Benutzerrollen und Zugriffsrichtlinien definieren können, um Zugriffsberechtigungen für Funktionen und Objekte in einem Produktprogramm zu verwalten.

Über Berechtigungen können Sie Rollen erstellen und verwalten sowie die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen. Mit Berechtigungen können Sie auch die Labels, Sandboxes und Benutzende verwalten, die einer bestimmten Rolle zugeordnet sind.

Nach dem [Erstellen einer neuen Rolle](#create-a-new-role) werden Sie sofort zur Registerkarte **[!UICONTROL Roles]** zurückgeleitet. Wenn Sie Berechtigungen für eine vorhandene Rolle bearbeiten, wählen Sie die Rolle auf der Registerkarte **[!UICONTROL Roles]** aus. Alternativ können Sie die Filteroption verwenden, um die Ergebnisse zu filtern und nach einer Rolle zu suchen.

## Filtern von Rollen

Wählen Sie das Trichtersymbol (![Filtersymbol](/help/images/icons/filter.png)) aus, um eine Liste von Filterfeldern anzuzeigen, mit denen die Ergebnisse eingegrenzt werden können.

![Das Rollen-Dashboard in der Benutzeroberfläche „Berechtigungen“ mit hervorgehobenem Abschnitt „Rollen filtern“.](../../images/flac-ui/flac-filters.png)

In der Benutzeroberfläche sind folgende Filter für Rollen verfügbar:

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Created between] | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. |
| [!UICONTROL Created by] | Filtern Sie nach dem Rollenersteller, indem Sie einen Benutzer aus der Dropdown-Liste auswählen. |
| [!UICONTROL Modified between] | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. |
| [!UICONTROL Modified by] | Filtern Sie nach dem Rollenmodifikator, indem Sie einen Benutzer aus der Dropdown-Liste auswählen. |

Um einen Filter zu entfernen, klicken Sie auf das „X“ auf dem Symbol für den betreffenden Filter, oder wählen Sie **[!UICONTROL Clear all]** aus, um alle Filter zu entfernen.

![Das Rollen -Dashboard in der Benutzeroberfläche „Berechtigungen“ mit dem hervorgehobenen „X“ und „Alle Auswahlen löschen“ in den ausgewählten Filtern.](../../images/flac-ui/flac-clear-filters.png)

## Rollendetails {#role-details}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Rollenübersicht"
>abstract="Im Dialogfeld „Rollenübersicht“ werden Rollendetails angezeigt, wie etwa die Ressourcen und Sandboxes, auf die eine bestimmte Rolle zugreifen darf. Sie können Kennzeichnungen, Benutzende, Benutzergruppen und API-Anmeldeinformationen für die Rolle verwalten, indem Sie zur entsprechenden Registerkarte im Arbeitsbereich der Rolle navigieren."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-labels-for-a-role" text="Verwalten von Labels für eine Rolle"
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-users-for-a-role" text="Verwalten der Benutzenden für eine Rolle"

Wählen Sie auf der Registerkarte **[!UICONTROL Roles]** die Rolle aus. Daraufhin wird das [!UICONTROL Details]-Dashboard der Rolle geöffnet.

![Der Arbeitsbereich „Details“ für die ausgewählte Rolle wird mit hervorgehobenen Übersichtsinformationen angezeigt.](../../images/flac-ui/flac-details.png)

Das [!UICONTROL Details]-Dashboard bietet einen Überblick über die Rolle. In der Übersicht werden der Rollenname, die Beschreibung, der Ersteller und der letzte Modifikator sowie das Erstellungs- und Änderungsdatum angezeigt. Außerdem werden die mit der Rolle verbundenen Berechtigungen und die Liste der zugewiesenen Sandboxes angezeigt. Der Rollenname und die Beschreibung können bei Bedarf geändert werden.

## Verwalten von Labels für eine Rolle

Wählen Sie die Registerkarte **[!UICONTROL Labels]** aus, um den Arbeitsbereich für Rollenbezeichnungen zu öffnen, und wählen Sie dann **[!UICONTROL Add labels]** aus, um der Rolle Beschriftungen zuzuweisen.

![Der Arbeitsbereich Beschriftungen der Rolle wird angezeigt, wobei die Registerkarte Beschriftungen und die Schaltfläche Beschriftungen hinzufügen hervorgehoben sind.](../../images/flac-ui/flac-labels.png)

Das Dialogfeld **[!UICONTROL Apply Access and Data Governance Labels]** wird mit einer Liste von Kennzeichnungen angezeigt. In der Liste werden der Name des Labels, der Anzeigename, die Kategorie und die Beschreibung angezeigt.

Wählen Sie in der Liste die Beschriftungen aus, die Sie der Rolle hinzufügen möchten, und klicken Sie dann auf **[!UICONTROL Save]**

![Der Dialog „Zugriff anwenden“ und „Data Governance-Beschriftungen“ mit einer ausgewählten Beschriftung.](../../images/flac-ui/flac-add-labels.png)

Hinzugefügte Beschriftungen werden auf **[!UICONTROL Labels]** Registerkarte angezeigt.

![Der Arbeitsbereich „Beschriftungen“ der Rolle mit hervorgehobener hinzugefügter Beschriftung.](../../images/flac-ui/flac-added-labels.png)

Um eine Beschriftung von einer Rolle zu entfernen, wählen Sie die Beschriftung aus und klicken Sie dann auf **[!UICONTROL Remove Labels]**.

![Der Arbeitsbereich „Beschriftungen“ der Rolle, wobei eine Rolle ausgewählt ist und die Option „Beschriftungen entfernen“ hervorgehoben ist.](../../images/flac-ui/flac-delete-labels.png)

## Verwalten von Sandboxes für eine Rolle

Wählen Sie die Registerkarte **[!UICONTROL Details]** aus und navigieren Sie zum Abschnitt **[!UICONTROL Sandboxes]** . Wählen Sie **[!UICONTROL View All]** aus, um die vollständige Liste der der Rolle hinzugefügten Sandboxes anzuzeigen.

![Der Arbeitsbereich „Details“ der Rolle mit hervorgehobenem Abschnitt „Sandboxes“.](../../images/flac-ui/flac-sandboxes.png)

Um einer Rolle weitere Sandboxes hinzuzufügen, wählen Sie oben rechts in der Benutzeroberfläche **[!UICONTROL Edit]** aus.

![Der Arbeitsbereich „Details“ der Rolle mit hervorgehobener Option „Bearbeiten“.](../../images/flac-ui/flac-add-sandboxes.png)

Im nächsten Bildschirm werden Sie aufgefordert, über die Dropdown-Liste auszuwählen, welche Sandbox-Ressourcen in die Rolle aufgenommen werden sollen. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Save]** und dann **[!UICONTROL Close]** aus.

![Das Ressourcen-Dashboard der Rolle mit hervorgehobenem Dropdown-Menü „Sandbox-Ressourcen“.](../../images/flac-ui/flac-add-role-permission.png)

## Verwalten der Benutzenden für eine Rolle

Wählen Sie die Registerkarte **[!UICONTROL Users]** aus, um die Rollen [!UICONTROL Users] Workspace zu öffnen, und wählen Sie dann **[!UICONTROL Add Users]** aus, um der Rolle Benutzer zuzuweisen.

![Der Arbeitsbereich Benutzer der Rolle wird angezeigt, wobei die Registerkarte Benutzer und die Option Benutzer hinzufügen hervorgehoben sind.](../../images/flac-ui/flac-users.png)

Das Dialogfeld **[!UICONTROL Add Users]** wird angezeigt. Wählen Sie die Benutzenden aus der Liste aus, die Sie der Rolle hinzufügen möchten. Alternativ können Sie in der Suchleiste nach dem Benutzer suchen, indem Sie dessen Namen oder E-Mail-Adresse eingeben. Klicken Sie dann auf **[!UICONTROL Save]**

![Das Dialogfeld „Benutzer hinzufügen“ mit ausgewähltem Benutzer und hervorgehobener Suchleiste und Speicheroption.](../../images/flac-ui/flac-add-users.png)

Hinzugefügte Benutzer erscheinen auf **[!UICONTROL Users]** Registerkarte.

![Der Arbeitsbereich Benutzer der Rolle mit den zur Rolle hinzugefügten Benutzern.](../../images/flac-ui/flac-added-users.png)

Um einen Benutzer aus einer Rolle zu entfernen, klicken Sie auf das Symbol **X** neben dem Namen des Benutzers.

![Der Arbeitsbereich „Benutzer“ der Rolle, in dem ein Benutzer mit hervorgehobener Option „X“ angezeigt wird.](../../images/flac-ui/flac-remove-users.png)

Im folgenden Video erfahren Sie, wie Sie eine neue Rolle erstellen und Benutzer für diese Rolle verwalten.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Verwalten von API-Anmeldeinformationen für eine Rolle {#manage-api-credentials-for-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_apicredentials_about"
>title="Was sind API-Anmeldeinformationen?"
>abstract="API-Anmeldeinformationen werden Rollen zugewiesen, um Benutzenden und Entwickelnden Zugriff auf Experience Platform-APIs zu gewähren. Mithilfe von Experience Platform-APIs können Sie programmgesteuert grundlegende CRUD-Vorgänge (Create, Read, Update, Delete: Erstellen, Lesen, Aktualisieren, Löschen) für Daten durchführen, z. B. berechnete Attribute konfigurieren, auf Daten/Entitäten zugreifen, Daten exportieren oder nicht benötigte Daten oder Batches löschen."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/landing/platform-apis/api-guide" text="Handbuch zum Experience Platform-API"

>[!IMPORTANT]
>
> Um API-Anmeldeinformationen in [!UICONTROL Permissions] verwenden und verwalten zu können, müssen Benutzende über Systemadministratorrechte verfügen.

Um Experience Platform-APIs als Benutzer oder Entwickler verwenden zu können, muss ein Systemadministrator zusätzlich zu den einer Rolle zugewiesenen Berechtigungen API-Anmeldeinformationen hinzufügen. Eine vollständige Anleitung zum Erstellen und Zuweisen von API-Anmeldeinformationen sowie die erforderlichen Berechtigungen finden Sie im schrittweisen Tutorial unter [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md#generate-credentials).

Wählen Sie die Registerkarte **[!UICONTROL API credentials]** aus, um den Arbeitsbereich mit den API-Anmeldeinformationen für Rollen zu öffnen, und klicken Sie auf **[!UICONTROL Add API credentials]** , um der Rolle API-Anmeldeinformationen zuzuweisen.

![Der Arbeitsbereich mit den API-Anmeldeinformationen der Rolle mit hervorgehobener Option „Anmeldeinformationen hinzufügen“.](../../images/flac-ui/flac-api-credentials.png)

Das Dialogfeld **[!UICONTROL Add API credentials]** wird angezeigt. Wählen Sie API-Anmeldeinformationen aus der Liste aus, um sie der Rolle hinzuzufügen, und wählen Sie dann **[!UICONTROL Save]** aus.

![Das Dialogfeld „API-Anmeldeinformationen hinzufügen“ mit ausgewählten Anmeldeinformationen und hervorgehobener Option „Speichern“.](../../images/flac-ui/flac-add-api-credentials.png)

Hinzugefügte API-Anmeldeinformationen erscheinen auf **[!UICONTROL API credentials]** Registerkarte .

![Der Arbeitsbereich mit den API-Anmeldeinformationen der Rolle mit den hinzugefügten Anmeldeinformationen wird angezeigt.](../../images/flac-ui/flac-added-api-credentials.png)

Um API-Anmeldeinformationen aus einer Rolle zu entfernen, klicken Sie auf das Symbol **X** neben dem Namen der API-Anmeldeinformationen.

![Der Arbeitsbereich mit den API-Anmeldeinformationen der Rolle, wobei die Option X zum Entfernen einer Anmeldeinformation hervorgehoben ist.](../../images/flac-ui/flac-remove-api-credentials.png)

Das Dialogfeld **[!UICONTROL Remove API credentials]** wird angezeigt, in dem Sie aufgefordert werden, den Löschvorgang zu bestätigen. Wählen Sie **[!UICONTROL Confirm]** aus, um das Entfernen der ausgewählten Berechtigung abzuschließen.

![Das Popup zum Entfernen von Anmeldeinformationen, in dem Sie aufgefordert werden zu bestätigen, dass das Entfernen der Anmeldeinformationen hervorgehoben ist.](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Sie werden zur Registerkarte **[!UICONTROL API credentials]** zurückgeleitet.

## Verwalten von Benutzergruppen für eine Rolle {#manage-user-groups}

>[!CONTEXTUALHELP]
>id="platform_permissions_usergroups_about"
>title="Was sind Benutzergruppen?"
>abstract="Benutzergruppen sind Sammlungen mehrerer Benutzer, die Zugriff auf dieselben Funktionen haben. Der Zugriff auf Ressourcen innerhalb einer Organisation wird über Rollen verwaltet, die Benutzergruppen zugewiesen sind."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/access-control/abac/permissions-ui/roles" text="Verwalten von Rollen"

Benutzergruppen sind mehrere Benutzer, die gruppiert wurden und Zugriff haben, um dieselben Funktionen auszuführen.

Wählen Sie die Registerkarte **[!UICONTROL User groups]** aus, um den Arbeitsbereich Benutzergruppen der Rolle zu öffnen, und wählen Sie dann **[!UICONTROL Add Groups]** aus, um der Rolle Benutzergruppen zuzuweisen.

![Der Arbeitsbereich Benutzergruppen der Rolle mit der Option Gruppen hinzufügen ](../../images/flac-ui/flac-user-groups.png)

Das Dialogfeld **[!UICONTROL Add Groups]** wird angezeigt. Wählen Sie aus der Liste die Benutzergruppen aus, die Sie der Rolle hinzufügen möchten. Alternativ können Sie über die Suchleiste nach der Benutzergruppe suchen, indem Sie den Namen der Gruppe eingeben. Klicken Sie dann auf **[!UICONTROL Save]**

![Das Dialogfeld „Gruppen hinzufügen“ mit einer ausgewählten Benutzergruppe und der hervorgehobenen Option „Suchen und Speichern“.](../../images/flac-ui/flac-add-user-groups.png)

Hinzugefügte Benutzergruppe erscheinen auf **[!UICONTROL User groups]** Registerkarte.

![Der Arbeitsbereich Benutzergruppen der Rolle zeigt die Liste der hinzugefügten Benutzergruppen an.](../../images/flac-ui/flac-added-user-groups.png)

Um eine Benutzergruppe aus einer Rolle zu entfernen, wählen Sie das Symbol **X** neben dem Namen der Benutzergruppe aus.

![Der Arbeitsbereich Benutzergruppen der Rolle, wobei die Option X zum Entfernen einer bestimmten Benutzergruppe hervorgehoben ist.](../../images/flac-ui/flac-remove-user-groups.png)

Das Dialogfeld **[!UICONTROL Remove user group]** wird angezeigt, in dem Sie aufgefordert werden, den Löschvorgang zu bestätigen. Wählen Sie **[!UICONTROL Confirm]** aus, um die ausgewählte Benutzergruppe zu entfernen.

![Das Popup zum Entfernen einer Benutzergruppe wird angezeigt und hervorgehoben.](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Sie werden zur Registerkarte **[!UICONTROL User groups]** zurückgeleitet.

## Hinzufügen von Benutzern zu Experience Platform

Als Systemadministrator können Sie einem Benutzer Entwicklerzugriff gewähren, damit er in der Adobe Developer Console [Integrationen ](../../../landing/api-authentication.md#generate-credentials) kann.

Um eine Benutzer-Experience Platform hinzuzufügen, melden Sie sich bei der [Admin Console an ](https://adminconsole.adobe.com) wählen Sie **[!UICONTROL Add users]** aus.

![Das Adobe Admin Console-Dashboard mit hervorgehobener Option „Benutzer hinzufügen“.](../../images/flac-ui/product-profile-add-users.png)

Das Dialogfeld **[!UICONTROL Add users to your team]** wird angezeigt. Geben Sie die E-Mail-Adresse, den Vornamen (optional) und den Nachnamen (optional) des Benutzers ein. Wählen Sie dann **[!UICONTROL Products]** aus.

![Das Dialogfeld „Benutzer zum Team hinzufügen“ mit hervorgehobener Option „Benutzerfelder und Produkte“.](../../images/flac-ui/product-profile-add-users-to-your-team.png)

Das Dialogfeld **[!UICONTROL Select products]** wird angezeigt. Wählen Sie **[!UICONTROL Adobe Experience Platform]** aus.

![Das Dialogfeld „Produkte auswählen“ mit hervorgehobener Option &quot;Adobe Experience Platform&quot;.](../../images/flac-ui/product-profile-select-product.png)

Das Dialogfeld **[!UICONTROL Select product profiles]** wird angezeigt. Wählen Sie **[!UICONTROL AEP-Default-All-Users]** und dann **[!UICONTROL Save]** aus.

![Das Dialogfeld „Produktprofile auswählen“ mit hervorgehobener Option &quot;AEP-Default-All-Users“ und „Apply“.](../../images/flac-ui/product-profile-select-product-profiles.png)

Überprüfen Sie die Informationen und wählen Sie dann **[!UICONTROL Save]** aus, um den Benutzer hinzuzufügen.

![Der Dialog Benutzer zu Ihrem Team hinzufügen mit den Benutzerinformationen und ausgewählten Auswahlen und der hervorgehobenen Option „Speichern“.](../../images/flac-ui/product-profile-save-user.png)

## Nächste Schritte

Nachdem Sie die Berechtigungen festgelegt haben, können Sie mit dem nächsten Schritt, [Benutzer verwalten](users.md), fortfahren.
