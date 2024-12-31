---
keywords: Experience Platform;Startseite;beliebte Themen;Marketo Engage;Marketo Engage;Marketo
solution: Experience Platform
title: Marketo-Quell-Connector authentifizieren
description: Dieses Dokument enthält Informationen zum Generieren Ihrer Marketo-Authentifizierungsberechtigungen.
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# [!DNL Marketo Engage]-Quell-Connector authentifizieren

Bevor Sie einen [!DNL Marketo Engage]-Quell-Connector (im Folgenden als &quot;[!DNL Marketo]&quot; bezeichnet) erstellen können, müssen Sie zunächst über die [!DNL Marketo] einen benutzerdefinierten Service einrichten und Werte für Ihre Munchkin-ID, Client-ID und Ihr Client-Geheimnis abrufen.

Die folgende Dokumentation enthält Schritte zum Abrufen von Authentifizierungsdaten, um einen [!DNL Marketo]-Quell-Connector zu erstellen.

## Einrichten einer neuen Rolle

Der erste Schritt zum Erfassen Ihrer Authentifizierungsdaten besteht darin, über die [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1)-Oberfläche eine neue Rolle einzurichten.

Melden Sie sich bei [!DNL Marketo] an und wählen Sie **[!DNL Admin]** in der oberen Navigationsleiste aus.

![Admin für eine neue Rolle](../images/marketo/home.png)

Die Seite *[!DNL Users & Role]s* enthält Informationen zu Benutzern, Rollen und Anmeldeverlauf. Um eine neue Rolle zu erstellen, wählen Sie in der oberen Kopfzeile **[!DNL Roles]** und dann **[!DNL New Role]** aus.

![new-role](../images/marketo/new-role.png)

Das Dialogfeld **[!DNL Create New Role]** wird angezeigt. Geben Sie einen Namen und eine Beschreibung ein und wählen Sie dann die Berechtigungen aus, die Sie für diese Rolle gewähren möchten. Berechtigungen sind auf bestimmte Arbeitsbereiche beschränkt, und Benutzende können Aktionen nur in Arbeitsbereichen ausführen, in denen sie über Berechtigungen verfügen.

Nachdem Sie die Berechtigungen ausgewählt haben, die Sie gewähren möchten, wählen Sie **[!DNL Create]** aus.

![create-new-role](../images/marketo/create-new-role.png)

Beim Erstellen von Rollen mit [!DNL Marketo] können Sie eingeschränkte Berechtigungen für die API verwalten. Anstatt „Zugriff auf API“ auszuwählen, können Sie einer Rolle die Mindestzugriffsstufe zuweisen, indem Sie die folgenden Berechtigungen auswählen:

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

Ähnlich wie bei Rollen können Sie einen neuen Benutzer über die Seite **[!DNL Users & Roles]** einrichten. Die Seite **[!DNL Users]** enthält eine Liste der aktiven Benutzenden, die derzeit in Marketo bereitgestellt sind. Wählen Sie **[!DNL Invite New User]** aus, um einen neuen Benutzer bereitzustellen.

![invite-new-user](../images/marketo/invite-new-user.png)

Ein Popup-Dialogfeldmenü wird angezeigt. Geben Sie die entsprechenden Informationen für Ihre E-Mail, Ihren Vornamen, Nachnamen und den Grund an. In diesem Schritt können Sie auch ein Ablaufdatum für den Zugriff auf das neue Benutzerkonto festlegen, das Sie einladen. Wenn Sie fertig sind, wählen Sie **[!DNL Next]** aus.

>[!IMPORTANT]
>
>Beim Einrichten eines neuen Benutzers müssen Sie einem Benutzer Zugriff zuweisen, der ausschließlich dem benutzerdefinierten Service gewidmet ist, den Sie erstellen.

![user-info](../images/marketo/new-user-info.png)

Wählen Sie die entsprechenden Felder im **[!DNL Permissions]** aus und aktivieren Sie dann das Kontrollkästchen **[!DNL API Only]** , um dem neuen Benutzer eine API-Rolle bereitzustellen. Wählen Sie **[!DNL Next]** aus, um fortzufahren.

![Berechtigungen](../images/marketo/permissions.png)

Um den Vorgang abzuschließen, wählen Sie **[!DNL Send]** aus.

![message](../images/marketo/message.png)

## Einrichten eines benutzerdefinierten Services

Nachdem Sie einen neuen Benutzer eingerichtet haben, können Sie einen benutzerdefinierten Service einrichten, um Ihre neuen Anmeldeinformationen abzurufen. Wählen Sie auf der Seite Admin **[!DNL LaunchPoint]** aus.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

Die Seite **[!DNL Installed services]** enthält eine Liste der vorhandenen Services. Um einen neuen benutzerdefinierten Service zu erstellen, wählen Sie **[!DNL New]** und dann **[!DNL New Service]** aus.

![new-service](../images/marketo/new-service.png)

Geben Sie Ihrem neuen Service einen beschreibenden Anzeigenamen und wählen Sie dann **[!DNL Custom]** aus dem Dropdown-Menü **[!DNL Service]** aus. Geben Sie eine entsprechende Beschreibung ein und wählen Sie dann im Dropdown-Menü **[!DNL API Only User]** den Benutzer aus, den Sie bereitstellen möchten. Nachdem Sie die erforderlichen Details eingegeben haben, wählen Sie **[!DNL Create]** aus, um Ihren neuen benutzerdefinierten Service zu erstellen.

![Erstellen](../images/marketo/create.png)

## Abrufen von Client-ID und Client-Geheimnis

Nachdem ein neuer benutzerdefinierter Service erstellt wurde, können Sie jetzt Werte für Ihre Client-ID und Ihr Client-Geheimnis abrufen. Suchen Sie im Menü **[!DNL Installed Services]** den benutzerdefinierten Service, auf den Sie zugreifen möchten, und wählen Sie dann **[!DNL View Details]** aus.

![view-details](../images/marketo/view-details.png)

Ein Dialogfeld wird angezeigt, das Ihre Client-ID und Ihr Client-Geheimnis enthält.

![Anmeldeinformationen](../images/marketo/credentials.png)

## Munchkin-ID abrufen

Der letzte Schritt, den Sie ausführen müssen, um Ihren [!DNL Marketo]-Quell-Connector zu authentifizieren, besteht darin, Ihre Munchkin ID abzurufen. Wählen Sie auf der Admin-Seite **[!DNL Munchkin]** im **[!DNL Integration]** aus.

![admin-munchkin](../images/marketo/admin-munchkin.png)

Die Seite *[!DNL Munchkin]* wird angezeigt, wobei Ihre eindeutige Munchkin-ID oben im Bedienfeld aufgeführt ist.

![munchkin-id](../images/marketo/munchkin-id.png)

In Kombination mit Ihrer Client-ID und Ihrem Client-Geheimnis können Sie Ihre Munchkin-ID verwenden, um ein neues Konto zu konfigurieren und [eine neue  [!DNL Marketo] -Quellverbindung zu erstellen](../../../tutorials/ui/create/adobe-applications/marketo.md) auf Experience Platform.
