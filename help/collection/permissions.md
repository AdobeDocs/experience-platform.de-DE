---
title: Berechtigungsverwaltung für die Datenerfassung in Experience Platform
description: Eine allgemeine Übersicht darüber, wie Sie Berechtigungen verwalten und den Zugriff auf Datenerfassungsfunktionen in Adobe Experience Platform steuern können.
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: 60590a77859320891717244eec58b556935354b5
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 28%

---

# Berechtigungsverwaltung für die Datenerfassung in Experience Platform

[Die Datenerfassung in Adobe Experience Platform](./home.md) besteht aus mehreren verschiedenen Technologien, die zusammenarbeiten, um Ihre Daten zu erfassen und zu übertragen. Der Zugriff auf diese Technologien wird über granulare rollenbasierte Berechtigungen in Adobe Admin Console gesteuert.

In diesem Handbuch erfahren Sie, wie Sie Berechtigungen für Datenerfassungsfunktionen verwalten.

## Erste Schritte

Um die Zugriffskontrolle für die Datenerfassung zu konfigurieren, müssen Sie über Administratorrechte für ein Unternehmen verfügen, das über eine Produktintegration mit der Datenerfassung von Adobe Experience Platform verfügt. Die Mindestrolle, die Berechtigungen erteilen oder entziehen kann, ist ein **Produktprofiladministrator**. Andere Administratorrollen, die Berechtigungen verwalten können, sind **Produktadministratoren** (kann alle Profile innerhalb eines Produkts verwalten) und **Systemadministratoren** (keine Einschränkungen). Weitere Informationen finden Sie im Artikel über [Administrationsrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) im Adobe Unternehmens-Administrationshandbuch.

In dieser Anleitung wird davon ausgegangen, dass Sie mit den grundlegenden Konzepten der Admin Console vertraut sind, z. B. mit Produktprofilen und damit, wie Sie einzelnen Benutzern und Gruppen Produktberechtigungen erteilen. Weitere Informationen finden Sie im [Benutzerhandbuch für die Admin Console](https://helpx.adobe.com/de/enterprise/using/admin-console.html).

## Verfügbare Berechtigungen

Die entsprechenden Berechtigungen für die Datenerfassung werden über zwei Produktbezeichnungen in Admin Console bereitgestellt: **Adobe Experience Platform** und **Adobe Experience Platform-Datenerfassung**. In den folgenden Abschnitten werden die Berechtigungen beschrieben, die unter den einzelnen Produkten gewährt werden, sowie die spezifischen Funktionen, auf die sie Zugriff gewähren.

### Adobe Experience Platform-Berechtigungen

Zu den Berechtigungen unter Adobe Experience Platform gehört der Zugriff auf Datenspeicher, Identitäten, Schemas und Sandboxes. Anweisungen zum Konfigurieren von Adobe Experience Platform-Berechtigungen finden Sie im Benutzerhandbuch zur Zugriffskontrolle [.](../access-control/ui/overview.md)

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| Sandboxes | (Nicht angegeben) | Abhängig von den unter Ihrem Unternehmen erstellten [Sandboxes](../sandboxes/home.md) können Sie den Zugriff auf alle Sandboxes über diese Berechtigungskategorie in Admin Console steuern. |
| Datenmodellierung | Verwalten von Schemata | Ermöglicht das Anzeigen, Erstellen und Bearbeiten von [Experience-Datenmodell (XDM)-Schemas](../xdm/home.md). |
| Datenmodellierung | Anzeigen von Schemata | Gewährt schreibgeschützten Zugriff auf Schemas. |
| Identity Management | Verwalten von Identitäts-Namensräumen | Ermöglicht das Anzeigen, Erstellen und Bearbeiten von [Identitäts-Namespaces](../identity-service/features/namespaces.md). |
| Identity Management | Anzeigen von Identitäts-Namensräumen | Ermöglicht schreibgeschützten Zugriff auf Identitäts-Namespaces. |
| Datenerfassung | Verwalten von Datenspeichern | Ermöglicht das Anzeigen, Erstellen und Bearbeiten von [Datastreams](../datastreams/overview.md). |
| Datenerfassung | Anzeigen von Datenspeichern | Ermöglicht schreibgeschützten Zugriff auf Datenspeicher. |

{style="table-layout:auto"}

### Adobe Experience Platform-Datenerfassungsberechtigungen

Berechtigungen unter der Datenerfassung von Adobe Experience Platform steuern den Zugriff auf Tags und Funktionen zur Ereignisweiterleitung, einschließlich Eigenschaften, Erweiterungen und Umgebungen. Anweisungen zum Konfigurieren von Adobe Experience Platform-Datenerfassungsberechtigungen finden Sie im Abschnitt [unter ](#manage).

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| Plattformen | Web | Gewährt Zugriff auf [Web-Eigenschaften](../tags/ui/administration/companies-and-properties.md), wenn diese mit anderen Eigenschaftsrechten kombiniert werden. |
| Plattformen | Mobile | Gewährt Zugriff auf [mobile Eigenschaften](../tags/ui/administration/companies-and-properties.md), wenn diese mit anderen Eigenschaftsrechten kombiniert werden. |
| Plattformen | Edge | Gewährt Zugriff auf die [Ereignisweiterleitung für Edge-Eigenschaften](../tags/ui/event-forwarding/getting-started.md) in Kombination mit anderen Eigenschaftsrechten. |
| Properties | (Nicht angegeben) | Je nach den Eigenschaften, die unter Ihrer Organisation erstellt wurden, können Sie den Zugriff auf jede dieser Eigenschaften über diese Berechtigungskategorie in Admin Console steuern.<br><br>Die zugewiesenen Eigenschaftsrechte eines Benutzers gelten nur für die Eigenschaften, auf die ihm über diese Berechtigungskategorie Zugriff gewährt wurde. |
| Eigenschaftsrechte | Genehmigen | Ermöglicht die Genehmigung eines Bibliotheks-Builds als Teil des [Veröffentlichungsflusses](../tags/ui/publishing/publishing-flow.md). |
| Eigenschaftsrechte | Entwickeln | Ermöglicht die Entwicklung eines Bibliotheks-Builds als Teil des [Veröffentlichungsflusses](../tags/ui/publishing/publishing-flow.md). |
| Eigenschaftsrechte | Eigenschaft bearbeiten | Ermöglicht die Bearbeitung der grundlegenden Konfiguration für die Eigenschaften, auf die ein Benutzer Zugriff hat. |
| Eigenschaftsrechte | Umgebungen verwalten | Ermöglicht die Verwaltung der [Umgebungen](../tags/ui/publishing/environments.md) für die Eigenschaften, auf die ein Benutzer Zugriff hat. |
| Eigenschaftsrechte | Erweiterungen verwalten | Ermöglicht die Verwaltung der [Erweiterungen](../tags/ui/managing-resources/extensions/overview.md) für die Eigenschaften, auf die ein Benutzer Zugriff hat. |
| Eigenschaftsrechte | Veröffentlichen Sie | Ermöglicht die Veröffentlichung eines Bibliotheks-Builds als Teil des [Veröffentlichungsflusses](../tags/ui/publishing/publishing-flow.md). |
| Unternehmensrechte | Entwickeln von Erweiterungen | Ermöglicht das Erstellen und Ändern von Erweiterungspaketen, die Ihrem Unternehmen gehören, einschließlich privater Versionen und Anforderungen zur öffentlichen Veröffentlichung. |
| Unternehmensrechte | Mobile-App-Konfigurationen verwalten | Diese Berechtigung gilt nur, wenn Sie über eine Lizenz für Adobe Journey Optimizer oder eine andere Lösung verfügen, die Zugriff auf mobile In-App- und Push-Nachrichten gewährt. Auf diese Weise können Sie Apps verwalten, von denen Adobe Experience Cloud weiß, sowie die erforderlichen Push-Anmeldeinformationen, die für die Kommunikation mit dem Firebase Cloud Messaging-Dienst und dem Apple-Push-Benachrichtigungsdienst erforderlich sind. |
| Unternehmensrechte | Eigenschaften verwalten | Ermöglicht Ihnen die Erstellung und Verwaltung von Tags (Webeigenschaft), Ereignisweiterleitung (Edge-Eigenschaft) und mobilen Eigenschaften. |

{style="table-layout:auto"}

>[!NOTE]
>
>Weitere Informationen dazu, wie sich diese Berechtigungen auf Funktionen in Tags auswirken, einschließlich Verwaltungsstrategien für gängige Szenarien, finden Sie in der Tag-Dokumentation zu [Benutzerberechtigungen](../tags/ui/administration/user-permissions.md).

## Verwalten von Berechtigungen {#manage}

Berechtigungen für die Datenerfassung werden über zwei Produktbezeichnungen verwaltet: **Adobe Experience Platform** und **Adobe Experience Platform-Datenerfassung**.

In den folgenden Unterabschnitten erfahren Sie, wie Sie die entsprechenden Berechtigungen für die einzelnen Produkte in der Admin Console verwalten:

* [Adobe Experience Platform-Berechtigungen](#manage-platform)
* [Adobe Experience Platform-Datenerfassungsberechtigungen](#manage-collection)

### Verwalten von Berechtigungen unter Adobe Experience Platform {#manage-platform}

>[!NOTE]
>
>Zum Verwalten von Berechtigungen für eine Rolle benötigen Sie Administratorrechte. Wenn Sie keine Administratorberechtigungen haben, wenden Sie sich an Ihren Systemadministrator.

Im Abschnitt &quot;Berechtigungen&quot;]**können Sie Benutzerrollen und Richtlinien definieren, um den Zugriff auf Funktionen und Objekte in einer Produktanwendung zu verwalten.**[!UICONTROL 

Über [!UICONTROL Berechtigungen] können Sie Rollen erstellen und verwalten und die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen.

![Adobe Experience Cloud, das das Berechtigungsprodukt hervorhebt.](./images/permissions/permissions-product.png)

Um auf Datenerfassungsfunktionen zugreifen zu können, müssen Sie alle Berechtigungen in den Kategorien **[!UICONTROL Sandboxes]**, **[!UICONTROL Datenmodellierung]**, **[!UICONTROL Identity Management]** und **[!UICONTROL Datenerfassung]** aktivieren.

![Bild, das die Datenerfassungs-Produktkarte in Admin Console anzeigt](./images/permissions/platform-permission-card.png)

Detaillierte Anweisungen zum Verwalten von Plattformberechtigungen finden Sie im Leitfaden zur Benutzeroberfläche für die Zugriffskontrolle ](../access-control/ui/overview.md).[

>[!NOTE]
>
>Je nach den Produkt-SKUs, auf die Ihr Unternehmen Zugriff hat, stehen Ihnen möglicherweise nicht alle Platform-Berechtigungen zur Verfügung.

### Verwalten von Berechtigungen unter Adobe Experience Platform-Datenerfassung {#manage-collection}

Um diese Berechtigungen zu verwalten, melden Sie sich bei Admin Console an und wählen Sie in der oberen Navigationsleiste **[!UICONTROL Artikel]** aus. Wählen Sie dann **[!UICONTROL Adobe Experience Platform-Datenerfassung]** aus.

![Bild, das die Datenerfassungs-Produktkarte in Admin Console anzeigt](./images/permissions/data-collection-card.png)

#### Auswählen oder Erstellen eines Produktprofils

Der nächste Bildschirm zeigt eine Liste der verfügbaren Produktprofile für die Datenerfassung unter Ihrer Organisation, wobei das Standardprofil **[!DNL Default Data Collection All Access]** ist. Sie können bei Bedarf das standardmäßige Produktprofil bearbeiten oder **[!UICONTROL Neues Profil]** auswählen, um ein Profil zu erstellen. Wenn Sie in Ihrer Organisation mehrere Rollen oder Benutzergruppen haben, die unterschiedliche Zugriffsrechte benötigen, sollten Sie für jede dieser Gruppen ein eigenes Produktprofil erstellen.

![Bild, das die Produktprofile für die Datenerfassung in Admin Console anzeigt](./images/permissions/new-profile.png)

Nachdem Sie ein Produktprofil ausgewählt oder erstellt haben, können Sie die Symbole **[!UICONTROL Bearbeiten]** verwenden, um [Berechtigungen zu bearbeiten](#edit-permissions) für das Profil zu starten, oder Sie können die Registerkarte **[!UICONTROL Benutzer]** auswählen, um [Benutzer](#assign-users) dem Profil zuzuweisen.

![Abbildung der Registerkarte „Berechtigungen“ für ein Produktprofil in Admin Console](./images/permissions/edit-permission-categories.png)

#### Berechtigungen für das Produktprofil bearbeiten {#edit-permissions}

Wenn Sie die Berechtigungen für ein Profil bearbeiten, werden die verfügbaren Berechtigungen in der linken Spalte aufgelistet, während diejenigen, die im Profil enthalten sind, in der rechten Spalte aufgeführt werden. Wählen Sie die aufgelisteten Berechtigungen aus, um sie zwischen den beiden Spalten zu verschieben.

![Bild mit Berechtigungen, die unter der eingeschlossenen Spalte hinzugefügt wurden](./images/permissions/added-permissions.png)

Berechtigungen sind in Kategorien unterteilt. Um zwischen Kategorien zu wechseln, wählen Sie die gewünschte Kategorie in der linken Navigationsleiste.

![Bild, das den Abschnitt &quot;Unternehmensrechte&quot;unter &quot;Berechtigungen&quot;anzeigt](./images/permissions/switch-category.png)

Wählen Sie **[!UICONTROL Speichern]**, sobald Sie die Konfiguration der Berechtigungen abgeschlossen haben.

![Bild, das die für das Produktprofil zu speichernde Berechtigungskonfiguration anzeigt](./images/permissions/save-permissions.png)

Die Ansicht des Produktprofils wird mit den hinzugefügten Berechtigungen wieder angezeigt.

![Bild mit den hinzugefügten Berechtigungen für das Produktprofil](./images/permissions/permissions-added.png)

#### Zuweisen von Benutzern zum Produktprofil {#assign-users}

Um dem Produktprofil Benutzer zuzuweisen (und ihnen die konfigurierten Berechtigungen des Profils zu gewähren), wählen Sie die Registerkarte **[!UICONTROL Benutzer]**, gefolgt von **[!UICONTROL Benutzer hinzufügen]**.

![Bild mit der Registerkarte „Benutzer“ für ein Produktprofil in Admin Console](./images/permissions/manage-users.png)

Weitere Informationen zur Verwaltung von Benutzern für ein Produktprofil finden Sie in der [Dokumentation zu Admin Console](https://helpx.adobe.com/de/enterprise/using/manage-product-profiles.html).

## Nächste Schritte

In diesem Handbuch wurden die verfügbaren Berechtigungen für die Datenerfassung und deren Verwaltung über die Admin Console behandelt. Weitere Informationen zur Verwaltung von Berechtigungen für andere Funktionen der Adobe Experience Platform finden Sie in der [Dokumentation zur Zugriffssteuerung](../access-control/home.md).
