---
title: Berechtigungen für Privacy Service verwalten
description: Erfahren Sie, wie Sie mithilfe von Adobe Admin Console Benutzerberechtigungen für Adobe Experience Platform Privacy Service verwalten.
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 6%

---

# Berechtigungen für Privacy Service verwalten

Zugriff auf [Adobe Experience Platform Privacy Service](./home.md) wird über granulare rollenbasierte Berechtigungen in Adobe Admin Console gesteuert. Durch die Erstellung von Produktprofilen, die Benutzergruppen Berechtigungen zuweisen, können Sie bestimmen, wer Zugriff auf welche Funktionen im Privacy Service hat [Benutzeroberfläche](./ui/overview.md) und [API](./api/overview.md).

>[!NOTE]
>
>Beim Erstellen einer Integration für die Privacy Service-API müssen Sie ein vorhandenes Produktprofil auswählen, um zu bestimmen, für welche Funktionen oder Aktionen diese Integration berechtigt ist. Siehe Handbuch unter [Erste Schritte mit der Privacy Service-API](./api/getting-started.md) für weitere Informationen.

In diesem Handbuch erfahren Sie, wie Sie Berechtigungen für Privacy Service verwalten.

## Erste Schritte

Um die Zugriffskontrolle für Privacy Service zu konfigurieren, müssen Sie über Administratorberechtigungen für eine Organisation verfügen, die über eine Produktintegration mit Adobe Experience Platform Privacy Service verfügt. Die Mindestrolle, die Berechtigungen erteilen oder entziehen kann, ist eine **Produktprofil-Administrator**. Andere Administratorrollen, die Berechtigungen verwalten können, sind **Produktadministratoren** (kann alle Profile innerhalb eines Produkts verwalten) und **Systemadministratoren** (keine Einschränkungen). Weitere Informationen finden Sie im Artikel unter [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) Weitere Informationen finden Sie im Adobe Enterprise-Verwaltungshandbuch .

In diesem Handbuch wird davon ausgegangen, dass Sie mit grundlegenden Konzepten der Admin Console wie Produktprofilen und der Art und Weise, wie diese Produktberechtigungen einzelnen Benutzern und Gruppen gewähren, vertraut sind. Weitere Informationen finden Sie unter [Benutzerhandbuch zu Admin Consolen](https://helpx.adobe.com/de/enterprise/using/admin-console.html).

## Verfügbare Berechtigungen

In der folgenden Tabelle sind die verfügbaren Berechtigungen für Privacy Service mit Beschreibungen der spezifischen Funktionen aufgeführt, auf die sie Zugriff gewähren:

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| [!UICONTROL Privacy Service-Berechtigungen] | [!UICONTROL Datenschutz - Leseberechtigung] | Bestimmt, ob der Benutzer vorhandene Zugriffs- und Löschanfragen zusammen mit den zugehörigen Details anzeigen kann. |
| [!UICONTROL Privacy Service-Berechtigungen] | [!UICONTROL Berechtigung für Datenschutz-Schreibzugriff] | Bestimmt, ob ein Benutzer neue Zugriffs- und Löschanfragen erstellen kann. |
| [!UICONTROL Privacy Service-Berechtigungen] | [!UICONTROL Berechtigung zum Lesen (Zugriff) der Inhaltsbereitstellung] | Wenn eine Zugriffsanfrage von einem Privacy Service verarbeitet wird, wird eine ZIP-Datei mit den Kundendaten an diesen Kunden gesendet. Beim Nachschlagen der Details einer Zugriffsanfrage bestimmt diese Berechtigung, ob der Benutzer auf den Downloadlink für die ZIP-Datei der Anfrage zugreifen kann. |
| [!UICONTROL Opt-out von Verkaufsberechtigungen] | [!UICONTROL Leseberechtigung - Opt-out vom Verkauf] | Bestimmt, ob der Benutzer vorhandene Opt-out-Kaufanfragen zusammen mit den zugehörigen Details anzeigen kann. |
| [!UICONTROL Opt-out von Verkaufsberechtigungen] | [!UICONTROL Schreibberechtigung - Opt-out vom Verkauf] | Bestimmt, ob ein Benutzer neue Opt-out-Kaufanfragen erstellen kann. |

{style=&quot;table-layout:auto&quot;}

## Verwalten von Berechtigungen {#manage}

Melden Sie sich bei an, um die Berechtigungen der Privacy Service zu verwalten [Admin Console](https://adminconsole.adobe.com/) und wählen Sie **[!UICONTROL Produkte]** aus der oberen Navigation. Wählen Sie von hier aus **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Bild mit der Privacy Service-Produktkarte in Admin Console](./images/permissions/privacy-service-card.png)

### Produktprofil auswählen oder erstellen

Im nächsten Bildschirm wird eine Liste der verfügbaren Produktprofile für den Privacy Service unter Ihrem Unternehmen angezeigt. Wenn keine Produktprofile vorhanden sind, wählen Sie **[!UICONTROL Neues Profil]** , um eine zu erstellen. Wenn Ihre Organisation über mehrere Rollen oder Benutzergruppen verfügt, für die unterschiedliche Zugriffsebenen benötigt werden, sollten Sie für jede dieser Rollen ein eigenes Produktprofil erstellen.

![Bild mit den Produktprofilen für den Privacy Service in Admin Console](./images/permissions/select-or-create-profile.png)

Nach Auswahl eines Produktprofils können Sie die **[!UICONTROL Berechtigungen]** Registerkarte zum Start [Berechtigungen bearbeiten](#edit-permissions) für das Profil oder wählen Sie die **[!UICONTROL Benutzer]** Registerkarte zum Start [Zuweisen von Benutzern](#assign-users) zum Profil.

![Bild mit der Registerkarte &quot;Berechtigungen&quot;für eine Produktprofil-Admin Console](./images/permissions/users-permissions-tabs.png)

### Berechtigungen für das Profil bearbeiten {#edit-permissions}

Im **[!UICONTROL Berechtigungen]** eine der angezeigten Berechtigungskategorien auswählen, um auf die Berechtigungs-Bearbeitungsansicht zuzugreifen.

Beim Bearbeiten von Berechtigungen für ein Profil werden die verfügbaren Berechtigungen in der linken Spalte aufgeführt, während die Berechtigungen, die im Profil enthalten sind, in der rechten Spalte aufgeführt sind. Wählen Sie die aufgelisteten Berechtigungen aus, um sie zwischen den Spalten zu verschieben.

![Bild mit den verfügbaren und eingeschlossenen Berechtigungsspalten](./images/permissions/edit-permissions.png)

Berechtigungen sind in Kategorien unterteilt. Um zwischen Kategorien zu wechseln, wählen Sie die gewünschte Kategorie aus der linken Navigation aus.

![Bild, das die [!UICONTROL Opt-out aus dem Verkauf] Abschnitt unter &quot;Berechtigungen&quot;](./images/permissions/switch-category.png)

Auswählen **[!UICONTROL Speichern]** nachdem Sie die Berechtigungen konfiguriert haben.

![Bild, das die für das Produktprofil zu speichernde Berechtigungskonfiguration anzeigt](./images/permissions/save-permissions.png)

Die Produktprofilansicht wird mit den hinzugefügten Berechtigungen erneut angezeigt.

![Bild mit den hinzugefügten Berechtigungen für das Produktprofil](./images/permissions/permissions-added.png)

### Zuweisen von Benutzern zum Profil {#assign-users}

Um dem Produktprofil Benutzer zuzuweisen (und ihnen die konfigurierten Berechtigungen des Profils zu erteilen), wählen Sie die **[!UICONTROL Benutzer]** Registerkarte, gefolgt von **[!UICONTROL Benutzer hinzufügen]**.

![Bild mit der Registerkarte &quot;Benutzer&quot;für ein Produktprofil in Admin Console](./images/permissions/manage-users.png)

Weitere Informationen zum Verwalten von Benutzern für ein Produktprofil finden Sie unter [Dokumentation zur Admin Console](https://helpx.adobe.com/de/enterprise/using/manage-product-profiles.html).

### Migrieren von Legacy-API-Anmeldeinformationen zum Profil {#migrate-tech-accounts}

>[!NOTE]
>
>Dieser Abschnitt gilt nur für bestehende API-Anmeldeinformationen, die erstellt wurden, bevor die Privacy Service-Berechtigungen in Adobe Admin Console integriert wurden. Bei neuen Anmeldedaten werden Produktprofile (und deren Berechtigungen) über zugewiesen. [Adobe Developer Console-Projekte](https://developer.adobe.com/developer-console/docs/guides/projects/) anstatt.<br><br>Siehe Abschnitt zu [Zuweisen von Produktprofilen zu einem Projekt](./api/getting-started.md#product-profiles) Weitere Informationen finden Sie im Erste-Schritte-Handbuch zur Privacy Service-API.

Um ältere API-Anmeldeinformationen in das Produktprofil zu migrieren, wählen Sie **[!UICONTROL API-Anmeldeinformationen]**, gefolgt von **[!UICONTROL API-Anmeldeinformationen hinzufügen]**.

![[!UICONTROL API-Anmeldeinformationen hinzufügen] in Admin Console unter dem [!UICONTROL API-Anmeldeinformationen] Registerkarte für ein Produktprofil](./images/permissions/api-credentials.png)

Wählen Sie die gewünschten Entwicklerkonsole-Projekte aus der Liste aus und wählen Sie dann **[!UICONTROL Speichern]** , um sie zum Produktprofil hinzuzufügen. Alle API-Aufrufe, die die Anmeldeinformationen aus diesen Projekten verwenden, erben die vom Produktprofil erteilten granularen Berechtigungen.

## Nächste Schritte

In diesem Handbuch wurden die verfügbaren Berechtigungen für Privacy Service und deren Verwaltung durch Admin Console behandelt.

Anweisungen zum Erstellen einer neuen API-Integration nach der Einrichtung von Produktprofilen finden Sie in der [Erste Schritte für die Privacy Service-API](./api/getting-started.md). Weitere Informationen zum Verwalten von Berechtigungen für andere Adobe Experience Platform-Funktionen finden Sie im Abschnitt [Zugriffssteuerungsdokumentation](../access-control/home.md).
