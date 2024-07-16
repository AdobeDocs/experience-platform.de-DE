---
keywords: Experience Platform; home; beliebte Themen; Marketo Engage; marketo engage; marketo
solution: Experience Platform
title: Authentifizieren des Marketo-Quell-Connectors
description: Dieses Dokument enthält Informationen zum Generieren Ihrer Marketo-Authentifizierungsberechtigungen.
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Quellanschluss von [!DNL Marketo Engage] authentifizieren

Bevor Sie einen Quell-Connector vom Typ &quot;[!DNL Marketo Engage]&quot;(nachfolgend als &quot;[!DNL Marketo]&quot; bezeichnet) erstellen können, müssen Sie zunächst einen benutzerdefinierten Dienst über die Benutzeroberfläche von [!DNL Marketo] einrichten und Werte für Ihre Munchkin-ID, Client-ID und das Client-Geheimnis abrufen.

In der folgenden Dokumentation erfahren Sie, wie Sie Authentifizierungsberechtigungen abrufen können, um einen Quell-Connector vom Typ [!DNL Marketo] zu erstellen.

## Einrichten einer neuen Rolle

Der erste Schritt beim Erwerb Ihrer Authentifizierungsberechtigungen besteht darin, über die [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) -Benutzeroberfläche eine neue Rolle einzurichten.

Melden Sie sich bei [!DNL Marketo] an und wählen Sie in der oberen Navigationsleiste **[!DNL Admin]** aus.

![Admin für eine neue Rolle](../images/marketo/home.png)

Die Seite &quot;*[!DNL Users & Role]s*&quot;enthält Informationen zu Benutzern, Rollen und Anmeldungsverläufen. Um eine neue Rolle zu erstellen, wählen Sie **[!DNL Roles]** aus der oberen Kopfzeile und dann **[!DNL New Role]** aus.

![new-role](../images/marketo/new-role.png)

Das Dialogfeld **[!DNL Create New Role]** wird angezeigt. Geben Sie einen Namen und eine Beschreibung ein und wählen Sie dann die Berechtigungen aus, die Sie für diese Rolle gewähren möchten. Berechtigungen sind auf bestimmte Arbeitsbereiche beschränkt und Benutzer können nur Aktionen in Arbeitsbereichen durchführen, für die sie über Berechtigungen verfügen.

Nachdem Sie die Berechtigungen ausgewählt haben, die Sie gewähren möchten, wählen Sie **[!DNL Create]** aus.

![create-new-role](../images/marketo/create-new-role.png)

Beim Erstellen von Rollen mit [!DNL Marketo] können Sie eingeschränkte Berechtigungen für die API verwalten. Anstatt &quot;Access API&quot;auszuwählen, können Sie eine Rolle mit dem Mindestmaß an Zugriff bereitstellen, indem Sie die folgenden Berechtigungen auswählen:

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## Einrichten eines neuen Benutzers

Ähnlich wie Rollen können Sie einen neuen Benutzer über die Seite **[!DNL Users & Roles]** einrichten. Die Seite &quot;**[!DNL Users]**&quot; enthält eine Liste der aktiven Benutzer, die derzeit in Marketo bereitgestellt werden. Wählen Sie **[!DNL Invite New User]** aus, um einen neuen Benutzer bereitzustellen.

![invited-new-user](../images/marketo/invite-new-user.png)

Ein Popover-Dialogfeld wird angezeigt. Geben Sie die entsprechenden Informationen für Ihre E-Mail-Adresse, Vorname, Nachname und Grund an. In diesem Schritt können Sie auch ein Ablaufdatum für den Zugriff auf das neue Benutzerkonto festlegen, das Sie einladen. Wenn Sie fertig sind, wählen Sie **[!DNL Next]** aus.

>[!IMPORTANT]
>
>Beim Einrichten eines neuen Benutzers müssen Sie den Zugriff einem Benutzer zuweisen, der ausschließlich für den von Ihnen erstellten benutzerdefinierten Dienst vorgesehen ist.

![user-info](../images/marketo/new-user-info.png)

Wählen Sie die entsprechenden Felder im Schritt **[!DNL Permissions]** aus und aktivieren Sie dann das Kontrollkästchen **[!DNL API Only]** , um dem neuen Benutzer eine API-Rolle bereitzustellen. Wählen Sie **[!DNL Next]** aus, um fortzufahren.

![Berechtigungen](../images/marketo/permissions.png)

Um den Prozess abzuschließen, wählen Sie **[!DNL Send]** aus.

![message](../images/marketo/message.png)

## Einrichten eines benutzerdefinierten Dienstes

Nachdem Sie einen neuen Benutzer eingerichtet haben, können Sie einen benutzerdefinierten Dienst einrichten, um Ihre neuen Anmeldedaten abzurufen. Wählen Sie auf der Admin-Seite **[!DNL LaunchPoint]** aus.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

Die Seite &quot;**[!DNL Installed services]**&quot; enthält eine Liste der vorhandenen Dienste. Um einen neuen benutzerdefinierten Dienst zu erstellen, wählen Sie &quot;**[!DNL New]**&quot;und dann &quot;**[!DNL New Service]**&quot;.

![new-service](../images/marketo/new-service.png)

Geben Sie Ihrem neuen Dienst einen beschreibenden Anzeigenamen und wählen Sie dann **[!DNL Custom]** aus dem Dropdown-Menü **[!DNL Service]** aus. Geben Sie eine entsprechende Beschreibung ein und wählen Sie dann den Benutzer aus dem Dropdown-Menü **[!DNL API Only User]** aus, den Sie bereitstellen möchten. Nachdem Sie die erforderlichen Details ausgefüllt haben, wählen Sie **[!DNL Create]** aus, um Ihren neuen benutzerdefinierten Dienst zu erstellen.

![create](../images/marketo/create.png)

## Abrufen Ihrer Client-ID und des Client-Geheimnisses

Mit einem neuen benutzerdefinierten Dienst können Sie jetzt Werte für Ihre Client-ID und Ihr Client-Geheimnis abrufen. Suchen Sie im Menü **[!DNL Installed Services]** den benutzerdefinierten Dienst, auf den Sie zugreifen möchten, und wählen Sie dann **[!DNL View Details]** aus.

![view-details](../images/marketo/view-details.png)

Es wird ein Dialogfeld mit Ihrer Client-ID und dem Client-Geheimnis angezeigt.

![credentials](../images/marketo/credentials.png)

## Munchkin-ID abrufen

Der letzte Schritt, den Sie zum Authentifizieren Ihres [!DNL Marketo] Quell-Connectors durchführen müssen, besteht darin, Ihre Munchkin-ID abzurufen. Wählen Sie auf der Admin-Seite unter dem Bedienfeld **[!DNL Integration]** die Option **[!DNL Munchkin]** aus.

![admin-munchkin](../images/marketo/admin-munchkin.png)

Die Seite &quot;*[!DNL Munchkin]*&quot; wird angezeigt, wobei Ihre eindeutige Munchkin-ID oben im Bedienfeld aufgelistet ist.

![munchkin-id](../images/marketo/munchkin-id.png)

In Kombination mit Ihrer Client-ID und dem Client-Geheimnis können Sie Ihre Munchkin-ID verwenden, um ein neues Konto zu konfigurieren, und [eine neue  [!DNL Marketo] Quellverbindung](../../../tutorials/ui/create/adobe-applications/marketo.md) auf der Experience Platform erstellen.
