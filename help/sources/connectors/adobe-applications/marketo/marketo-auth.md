---
keywords: Experience Platform;Startseite;beliebte Themen;Marketo Engage;Markieren;Markieren
solution: Experience Platform
title: Authentifizieren Sie Ihren Marketo-Quellanschluss.
topic: overview
description: Dieses Dokument enthält Informationen zum Generieren Ihrer Marketo-Authentifizierungsberechtigungen.
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---


# (Beta) Authentifizieren Sie den [!DNL Marketo Engage]-Quellanschluss.

>[!IMPORTANT]
>
>Die [!DNL Marketo Engage]-Quelle befindet sich derzeit in der Betaphase. Seine Funktionen und die Dokumentation können sich ändern.

Bevor Sie einen [!DNL Marketo Engage]-Quellanschluss (nachfolgend als &quot;[!DNL Marketo]&quot;bezeichnet) erstellen können, müssen Sie zunächst einen benutzerdefinierten Dienst über die [!DNL Marketo]-Schnittstelle einrichten und Werte für Ihre Munchkin-ID, Client-ID und das Clientgeheimnis abrufen.

Die nachstehende Dokumentation beschreibt, wie Sie Authentifizierungsberechtigungen erfassen, um einen [!DNL Marketo]-Quellanschluss zu erstellen.

## Neue Rolle einrichten

Der erste Schritt beim Erwerb Ihrer Authentifizierungsdaten besteht darin, über die [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1)-Schnittstelle eine neue Rolle einzurichten.

Melden Sie sich bei [!DNL Marketo] an und wählen Sie **[!DNL Admin]** in der oberen Navigationsleiste aus.

![Administrator für eine neue Rolle](../images/marketo/home.png)

Die Seite *[!DNL Users & Role]s* enthält Informationen zu Benutzern, Rollen und Anmeldungshistorien. Um eine neue Rolle zu erstellen, wählen Sie **[!DNL Roles]** in der oberen Kopfzeile und dann **[!DNL New Role]** aus.

![new-role](../images/marketo/new-role.png)

Das Dialogfeld **[!DNL Create New Role]** wird angezeigt. Geben Sie einen Namen und eine Beschreibung ein und wählen Sie dann die Berechtigungen, die Sie für diese Rolle gewähren möchten. Berechtigungen sind auf bestimmte Arbeitsbereiche beschränkt, und Benutzer können nur Aktionen in Arbeitsbereichen durchführen, für die sie Berechtigungen besitzen.

Nachdem Sie die gewünschten Berechtigungen ausgewählt haben, wählen Sie **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

Sie können eingeschränkte Berechtigungen für die API verwalten, wenn Sie Rollen mit [!DNL Marketo] erstellen. Statt &quot;API-Zugriff&quot;auszuwählen, können Sie eine Rolle mit der Mindestzugriffsstufe bereitstellen, indem Sie die folgenden Berechtigungen auswählen:

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

## Neuen Benutzer einrichten

Ähnlich wie Rollen können Sie einen neuen Benutzer auf der Seite **[!DNL Users & Roles]** einrichten. Die Seite **[!DNL Users]** enthält eine Liste aktiver Benutzer, die derzeit in Marketo bereitgestellt werden. Wählen Sie **[!DNL Invite New User]**, um einen neuen Benutzer bereitzustellen.

![invited-new-user](../images/marketo/invite-new-user.png)

Ein Popupmenü wird angezeigt. Geben Sie die entsprechenden Informationen für Ihre E-Mail-Adresse, Ihren Vornamen, Ihren Nachnamen und Ihre Begründung ein. In diesem Schritt können Sie auch ein Ablaufdatum für den Zugriff auf das neue Benutzerkonto festlegen, das Sie einladen. Wenn Sie fertig sind, wählen Sie **[!DNL Next]**.

>[!IMPORTANT]
>
>Bei der Einrichtung eines neuen Benutzers müssen Sie den Zugriff einem Benutzer zuweisen, der ausschließlich dem von Ihnen erstellten benutzerdefinierten Dienst gewidmet ist.

![user-info](../images/marketo/new-user-info.png)

Wählen Sie im Schritt **[!DNL Permissions]** die entsprechenden Felder aus und aktivieren Sie dann das Kontrollkästchen **[!DNL API Only]**, um dem neuen Benutzer eine API-Rolle bereitzustellen. Wählen Sie **[!DNL Next]** aus, um fortzufahren.

![Berechtigungen](../images/marketo/permissions.png)

Um den Prozess abzuschließen, wählen Sie **[!DNL Send]**.

![angezeigt](../images/marketo/message.png)

## Einrichten eines benutzerdefinierten Dienstes

Nachdem Sie einen neuen Benutzer eingerichtet haben, können Sie einen benutzerdefinierten Dienst einrichten, um Ihre neuen Anmeldeinformationen abzurufen. Wählen Sie auf der Admin-Seite **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

Die Seite **[!DNL Installed services]** enthält eine Liste der vorhandenen Dienste. Um einen neuen benutzerdefinierten Dienst zu erstellen, wählen Sie **[!DNL New]** und dann **[!DNL New Service]**.

![new-service](../images/marketo/new-service.png)

Geben Sie dem neuen Dienst einen beschreibenden Anzeigenamen und wählen Sie dann **[!DNL Custom]** aus dem Dropdown-Menü **[!DNL Service]**. Geben Sie eine entsprechende Beschreibung ein und wählen Sie dann im Dropdown-Menü **[!DNL API Only User]** den gewünschten Benutzer aus. Nachdem Sie die erforderlichen Details ausgefüllt haben, wählen Sie **[!DNL Create]** aus, um Ihren neuen benutzerdefinierten Dienst zu erstellen.

![create](../images/marketo/create.png)

## Abrufen der Client-ID und des Clientgeheimnisses

Mit einem neuen benutzerdefinierten Dienst können Sie jetzt Werte für Ihre Client-ID und Ihr Clientgeheimnis abrufen. Suchen Sie im Menü **[!DNL Installed Services]** den benutzerdefinierten Dienst, auf den Sie zugreifen möchten, und wählen Sie **[!DNL View Details]**.

![Ansicht-Details](../images/marketo/view-details.png)

Es wird ein Dialogfeld mit Ihrer Client-ID und Ihrem Clientgeheimnis angezeigt.

![credentials](../images/marketo/credentials.png)

## Ihre Munchkin-ID abrufen

Der letzte Schritt, den Sie zum Authentifizieren Ihres [!DNL Marketo]-Quellconnectors ausführen müssen, ist das Abrufen Ihrer Munchkin-ID. Wählen Sie auf der Admin-Seite unter dem Bedienfeld **[!DNL Integration]** die Option **[!DNL Munchkin]**.

![admin-munchkin](../images/marketo/admin-munchkin.png)

Die Seite *[!DNL Munchkin]* mit Ihrer eindeutigen Munchkin-ID wird oben im Bedienfeld angezeigt.

![munchkin-id](../images/marketo/munchkin-id.png)

In Verbindung mit Ihrer Client-ID und Ihrem Clientgeheimnis können Sie Ihre Munchkin-ID verwenden, um ein neues Konto zu konfigurieren und [eine neue  [!DNL Marketo] Quellverbindung](../../../tutorials/ui/create/adobe-applications/marketo.md) auf der Experience Platform erstellen.
