---
title: Gewähren von Benutzerzugriff
description: Richten Sie die Tag-Benutzerkonten und -Berechtigungen Ihrer Teammitglieder in Adobe Experience Platform ein.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 23%

---

# Gewähren von Benutzerzugriff

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Bevor Sie mit Ihrem „extension_package“ beginnen, müssen Sie für Ihre Team-Mitglieder Benutzerkonten und Berechtigungen einrichten. Sie verwenden dazu [Adobe Admin Console](https://adminconsole.adobe.com/).

In diesem Dokument wird beschrieben, wie Sie über Admin Console Zugriff auf Tags in Adobe Experience Platform gewähren.

## Voraussetzungen

In dieser Anleitung wird davon ausgegangen, dass Sie ein über Admin Console festgelegter Organisationsadministrator sind. Wenn Sie weitere Informationen zu Admin Console und zum Zuweisen von Rollen benötigen, finden Sie diese in den folgenden Ressourcen:

* [Administrations-Benutzerhandbuch](https://helpx.adobe.com/de/enterprise/administering/user-guide.html?topic=/enterprise/administering/morehelp/introduction.ug.js): Informationen zu allen Elementen und Funktionen von Admin Console
* [Unternehmensadministrationsrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html): Weitere Informationen zu den verschiedenen Arten von Administrationsrollen. In der nachstehenden Anleitung wird davon ausgegangen, dass Sie ein Organisationsadministrator sind.

## Unternehmen auswählen

Ihr Adobe Experience Cloud-Organisationsadministrator sollte sich bei [Admin Console](https://adminconsole.adobe.com/) anmelden. Der erste Bildschirm ist die Übersicht.

![Registerkarte &quot;Admin Console - Übersicht&quot;](../images/getting-started/admin-console-overview.png)

Einige von Ihnen haben möglicherweise Zugriff auf mehr als eine Organisation (Organisation). Um die Tag-Funktion zur richtigen Organisation hinzuzufügen, wählen Sie den Namen der Organisation aus, den Sie oben rechts im Bildschirm sehen. Wählen Sie als Nächstes die Organisation aus, in der Sie Tags aus der Dropdown-Liste verwenden möchten.

![Dropdown zur Auswahl der Admin Console-Organisation](../images/getting-started/admin-console-choose-org.png)

## Produktprofil erstellen

Ein Produktprofil ist eine Gruppe. Produktprofilen werden individuelle Rechte zugewiesen und alle Benutzer im Profil erben diese Rechte.

Wählen Sie oben den Link **[!UICONTROL Products]** und links **[!UICONTROL Experience Cloud]**. Wenn die Datenerfassungs-Benutzeroberfläche nicht aufgelistet ist, sollten sich Kunden an ihr Account-Team wenden und Partner sollten <ExchangeTechEC@adobe.com> per E-Mail versenden.

![Registerkarte &quot;Produkte der Admin Console&quot;](../images/getting-started/admin-console-products-launch.png)

Der obige Screenshot zeigt ein Beispielprofil, das Sie möglicherweise noch nicht haben. Um ein Profil zu erstellen, wählen Sie **[!UICONTROL Neues Profil]** aus. Fügen Sie im Bildschirm **Neues Profil erstellen** einfach einen **Profilnamen** (z. B. Datenerfassungstests) und eine optionale **Beschreibung** hinzu und wählen Sie **[!UICONTROL Speichern]**:

![Neue Profilanzeige erstellen](../images/getting-started/admin-console-create-a-new-profile.png)

Das Produktprofil wurde der Organisation hinzugefügt. Fügen Sie anschließend Benutzer zum Produktprofil hinzu.

## Benutzer zum Produktprofil zuweisen

Beachten Sie, dass das Produktprofil null für **ENTITLED-BENUTZER** und **ADMINS** anzeigt. Wählen Sie den Namen des von Ihnen erstellten Produktprofils aus (in unserem Beispiel Datenerfassungstests ).

![Anzeige von Produktprofilen](../images/getting-started/admin-console-profiles-add-user.png)

Wählen Sie die Registerkarte **[!UICONTROL Benutzer]** aus. Hier können Sie nach vorhandenen Adobe ID-Benutzern per E-Mail suchen oder diesem Produktprofil neue Benutzer hinzufügen. Wählen Sie **[!UICONTROL Benutzer-Link hinzufügen]** aus.

![Registerkarte &quot;Produktprofile - Benutzer&quot;](../images/getting-started/admin-console-add-launch-user.png)

Geben Sie einen Namen, eine Benutzergruppe oder eine E-Mail-Adresse in das entsprechende Textfeld ein. Es wird empfohlen, nach Möglichkeit einen Vor- und Nachnamen einzufügen. Wählen Sie **[!UICONTROL Save]** aus, um den Benutzer hinzuzufügen.

![Benutzer zur Profilanzeige hinzufügen](../images/getting-started/admin-console-add-user.png)

Wenn Sie alle Benutzer haben, die Sie in diesem Produktprofil benötigen, fügen wir Berechtigungen für sie hinzu. Wählen Sie die Registerkarte **[!UICONTROL Berechtigungen]** aus. Auf dem Bildschirm &quot;Berechtigungen&quot;sehen Sie **[!UICONTROL Eigenschaften]**, **[!UICONTROL Unternehmensrechte]** und **[!UICONTROL Eigenschaftsrechte]**. Wählen Sie **[!UICONTROL Bearbeiten]** aus.

![Registerkarte &quot;Berechtigungen für Produktprofile&quot;](../images/getting-started/admin-console-profile-permissions.png)

Um Erweiterungen erstellen zu können, muss Ihr Team über mindestens die folgenden Berechtigungen verfügen:

* &quot;Properties verwalten&quot;aus der Unternehmensgruppe.
* &quot;Erweiterungen verwalten&quot;, &quot;Umgebungen verwalten&quot;und &quot;Entwickeln&quot;aus der Eigenschaftsgruppe.

Sie können später weitere Produktprofile mit eingeschränkteren Rechten erstellen, aber zunächst einfach **[!UICONTROL + Alle hinzufügen]** für **Unternehmensrechte** und **Eigenschaftsrechte** auswählen. Stellen Sie sicher, dass Sie jeweils **[!UICONTROL Speichern]** auswählen.

![Verwalten von Eigenschaftsrechten](../images/getting-started/admin-console-add-all-property-rights.png)

![Verwalten von Unternehmensrechten](../images/getting-started/admin-console-add-all-company-rights.png)

Bisher haben wir die entsprechende Organisation ausgewählt, ein Produktprofil erstellt, Benutzer zum Produktprofil hinzugefügt und Berechtigungen zugewiesen.

Dadurch wird die erforderliche Einrichtung in Admin Console abgeschlossen. Sie und Ihre Team-Mitglieder, die als Benutzer eingerichtet wurden, können sich jetzt bei [der Datenerfassungs-Benutzeroberfläche](https://launch.adobe.com/) anmelden.

## Bereitstellung bestätigen

Nachdem Ihr Unternehmen Zugriff auf Tags erhalten und Ihre Benutzer wie oben beschrieben eingerichtet wurden, sollten Sie über die [Datenerfassungs-Benutzeroberfläche](https://launch.adobe.com/) auf die Produktionsumgebung zugreifen können. Wenn Sie für -Tags bereitgestellt wurden und die obigen Admin Consolen abgeschlossen haben, sich aber dennoch nicht bei der Datenerfassungs-Benutzeroberfläche anmelden können, wenden Sie sich an den Support-Mitarbeiter Ihrer Adobe.
