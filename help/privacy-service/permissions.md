---
title: Verwalten der Berechtigungen für den Privacy Service
description: Erfahren Sie, wie Sie die Benutzerrechte für den Adobe Experience Platform Privacy Service mit der Adobe Admin Console verwenden können.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: ebcfdc9f73fc9120cf3819169d72bd828d0b35a6
workflow-type: ht
source-wordcount: '964'
ht-degree: 100%

---

# Verwalten der Berechtigungen für den Privacy Service

Der Zugriff auf den [Adobe Experience Platform Privacy Service](./home.md) wird über granulare rollenbasierte Berechtigungen in der Adobe Admin Console gesteuert. Durch die Erstellung von Produktprofilen, die Gruppen von Benutzern Berechtigungen zuweisen, können Sie festlegen, wer auf welche Funktionen in der Privacy Service-[Benutzeroberfläche](./ui/overview.md) und der -[API](./api/overview.md) Zugriff hat.

>[!NOTE]
>
>Wenn Sie eine Integration für die Privacy Service-API erstellen, müssen Sie ein bestehendes Produktprofil auswählen, um zu bestimmen, für welche Funktionen oder Aktionen diese Integration Berechtigungen hat. Weitere Informationen finden Sie im Handbuch [Erste Schritte mit der Privacy Service-API](./api/getting-started.md).

Dieses Handbuch zeigt Ihnen, wie Sie die Berechtigungen für den Privacy Service verwalten.

## Erste Schritte

Um die Zugriffssteuerung für den Privacy Service zu konfigurieren, müssen Sie über Administratorrechte für eine Organisation verfügen, die über eine Produktintegration mit dem Adobe Experience Platform Privacy Service verfügt. Die Mindestrolle, die Berechtigungen erteilen oder entziehen kann, ist ein **Produktprofiladministrator**. Andere Administratorrollen, die Berechtigungen verwalten können, sind **Produktadministratoren** (kann alle Profile innerhalb eines Produkts verwalten) und **Systemadministratoren** (keine Einschränkungen). Weitere Informationen finden Sie im Artikel über [Administrationsrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) im Adobe Unternehmens-Administrationshandbuch.

In dieser Anleitung wird davon ausgegangen, dass Sie mit den grundlegenden Konzepten der Admin Console vertraut sind, z. B. mit Produktprofilen und damit, wie Sie einzelnen Benutzern und Gruppen Produktberechtigungen erteilen. Weitere Informationen finden Sie im [Benutzerhandbuch für die Admin Console](https://helpx.adobe.com/de/enterprise/using/admin-console.html).

## Verfügbare Berechtigungen

In der folgenden Tabelle finden Sie eine Übersicht über die verfügbaren Berechtigungen für den Privacy Service mit Beschreibungen der spezifischen Funktionen, auf die sie Zugriff gewähren:

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| [!UICONTROL Privacy Service-Berechtigungen] | [!UICONTROL Datenschutz – Leseberechtigung] | Legt fest, ob Benutzende bestehende Zugriffs- und Löschanträge sowie deren Details einsehen können. |
| [!UICONTROL Privacy Service-Berechtigungen] | [!UICONTROL Datenschutz – Schreibberechtigung] | Legt fest, ob Benutzende neue Zugangs- und Löschanträge erstellen können. |
| [!UICONTROL Privacy Service-Berechtigungen] | [!UICONTROL Berechtigung zum Lesen (Zugriff) der Inhaltsbereitstellung] | Wenn eine Zugriffsanfrage vom Privacy Service verarbeitet wird, wird eine ZIP-Datei mit den Kundendaten an diesen Kunden gesendet. Wenn Sie sich die Details einer Zugriffsanfrage ansehen, bestimmt diese Berechtigung, ob die Benutzenden auf den Download-Link für die ZIP-Datei der Anfrage zugreifen können. |
| [!UICONTROL Opt-out von Verkaufsberechtigungen] | [!UICONTROL Leseberechtigung – Opt-out vom Verkauf] | Legt fest, ob Benutzende bestehende Opt-out-Anträge zusammen mit ihren Details einsehen können. |
| [!UICONTROL Opt-out von Verkaufsberechtigungen] | [!UICONTROL Schreibberechtigung – Opt-out vom Verkauf] | Legt fest, ob Benutzende neue Opt-out-Kaufanfragen erstellen können. |

{style=&quot;table-layout:auto&quot;}

## Verwalten von Berechtigungen {#manage}

Um die Berechtigungen für den Privacy Service zu verwalten, melden Sie sich bei [Admin Console](https://adminconsole.adobe.com/) an und wählen Sie **[!UICONTROL Produkte]** in der oberen Navigationsleiste. Wählen Sie von hier aus **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Bild mit der Privacy Service-Produktkarte in Admin Console](./images/permissions/privacy-service-card.png)

### Auswählen oder Erstellen eines Produktprofils

Auf dem nächsten Bildschirm sehen Sie eine Liste der verfügbaren Produktprofile für Privacy Service unter Ihrer Organisation. Wenn keine Produktprofile vorhanden sind, wählen Sie **[!UICONTROL Neues Profil]**, um eines zu erstellen. Wenn Sie in Ihrer Organisation mehrere Rollen oder Benutzergruppen haben, die unterschiedliche Zugriffsrechte benötigen, sollten Sie für jede dieser Gruppen ein eigenes Produktprofil erstellen.

![Bild mit den Produktprofilen für Privacy Service in Admin Console](./images/permissions/select-or-create-profile.png)

Nachdem Sie ein Produktprofil ausgewählt haben, können Sie auf der Registerkarte **[!UICONTROL Berechtigungen]** mit der [Bearbeitung der Berechtigungen](#edit-permissions) für das Profil beginnen oder auf der Registerkarte **[!UICONTROL Benutzer]** mit der [Zuweisung von Benutzern](#assign-users) für das Profil beginnen.

![Abbildung der Registerkarte „Berechtigungen“ für ein Produktprofil in Admin Console](./images/permissions/users-permissions-tabs.png)

### Bearbeiten der Berechtigungen für das Profil {#edit-permissions}

Wählen Sie auf der Registerkarte **[!UICONTROL Berechtigungen]** eine der angezeigten Berechtigungskategorien aus, um die Ansicht zur Bearbeitung von Berechtigungen aufzurufen.

Wenn Sie die Berechtigungen für ein Profil bearbeiten, werden die verfügbaren Berechtigungen in der linken Spalte aufgelistet, während diejenigen, die im Profil enthalten sind, in der rechten Spalte aufgeführt werden. Wählen Sie die aufgelisteten Berechtigungen aus, um sie zwischen den beiden Spalten zu verschieben.

![Bild mit den Spalten der verfügbaren und der eingeschlossenen Berechtigungen](./images/permissions/edit-permissions.png)

Berechtigungen sind in Kategorien unterteilt. Um zwischen Kategorien zu wechseln, wählen Sie die gewünschte Kategorie in der linken Navigationsleiste.

![Bild, das den Abschnitt [!UICONTROL Opt-out vom Verkauf] unter „Berechtigungen“ zeigt](./images/permissions/switch-category.png)

Wählen Sie **[!UICONTROL Speichern]**, sobald Sie die Konfiguration der Berechtigungen abgeschlossen haben.

![Bild, das die für das Produktprofil zu speichernde Berechtigungskonfiguration anzeigt](./images/permissions/save-permissions.png)

Die Ansicht des Produktprofils wird mit den hinzugefügten Berechtigungen wieder angezeigt.

![Bild mit den hinzugefügten Berechtigungen für das Produktprofil](./images/permissions/permissions-added.png)

### Zuweisen von Benutzern zum Profil {#assign-users}

Um dem Produktprofil Benutzer zuzuweisen (und ihnen die konfigurierten Berechtigungen des Profils zu gewähren), wählen Sie die Registerkarte **[!UICONTROL Benutzer]**, gefolgt von **[!UICONTROL Benutzer hinzufügen]**.

![Bild mit der Registerkarte „Benutzer“ für ein Produktprofil in Admin Console](./images/permissions/manage-users.png)

Weitere Informationen zur Verwaltung von Benutzern für ein Produktprofil finden Sie in der [Dokumentation zu Admin Console](https://helpx.adobe.com/de/enterprise/using/manage-product-profiles.html).

### Migrieren von Legacy-API-Anmeldeinformationen zum Profil {#migrate-tech-accounts}

>[!NOTE]
>
>Dieser Abschnitt gilt nur für bestehende API-Anmeldeinformationen, die erstellt wurden, bevor die Privacy Service-Berechtigungen in Adobe Admin Console integriert wurden. Für neue Anmeldeinformationen werden Produktprofile (und deren Berechtigungen) stattdessen über [Adobe Developer Console-Projekte](https://developer.adobe.com/developer-console/docs/guides/projects/) zugewiesen.<br><br>Weitere Informationen finden Sie im Abschnitt [Zuweisung von Produktprofilen zu einem Projekt](./api/getting-started.md#product-profiles) im Handbuch zu den ersten Schritten mit der Privacy Service-API.

Um ältere API-Anmeldeinformationen in das Produktprofil zu migrieren, wählen Sie **[!UICONTROL API-Anmeldeinformationen]**, gefolgt von **[!UICONTROL API-Anmeldeinformationen hinzufügen]**.

![[!UICONTROL API-Zugangsdaten hinzufügen] wird in Admin Console unter der Registerkarte [!UICONTROL API-Zugangsdaten] für ein Produktprofil ausgewählt](./images/permissions/api-credentials.png)

Wählen Sie die gewünschten Developer Console-Projekte aus der Liste aus und klicken Sie dann auf **[!UICONTROL Speichern]**, um sie zum Produktprofil hinzuzufügen. Alle API-Aufrufe, die die Anmeldeinformationen dieser Projekte verwenden, erben die vom Produktprofil gewährten detaillierten Berechtigungen.

## Nächste Schritte

In diesem Handbuch wurden die verfügbaren Berechtigungen für Privacy Service und deren Verwaltung durch Admin Console behandelt.

Anweisungen zum Erstellen einer neuen API-Integration nach der Einrichtung von Produktprofilen finden Sie im [Handbuch zu den ersten Schritten mit der Privacy Service-API](./api/getting-started.md). Weitere Informationen zur Verwaltung von Berechtigungen für andere Funktionen der Adobe Experience Platform finden Sie in der [Dokumentation zur Zugriffssteuerung](../access-control/home.md).
