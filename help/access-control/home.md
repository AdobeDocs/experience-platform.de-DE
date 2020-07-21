---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zugriffskontrolle – Übersicht
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 66%

---


# Zugriffskontrolle – Übersicht

Access control for [!DNL Experience Platform] is provided through the [Adobe Admin Console](https://adminconsole.adobe.com). This functionality leverages product profiles in [!DNL Admin Console], which link users with permissions and sandboxes.

## Zugriffskontrolle auf Hierarchie und Workflow

In order to configure access control for [!DNL Experience Platform], you must have administrator privileges for an organization that has an [!DNL Experience Platform] product integration. Die Mindestrolle, die Berechtigungen erteilt oder entzieht, ist ein **[!UICONTROL Produktprofil-Administrator]**. Andere Administratorrollen, die Berechtigungen verwalten können, sind **[!UICONTROL Produktadministratoren]** (kann alle Profile innerhalb eines Produkts verwalten) und **[!UICONTROL Systemadministratoren]** (keine Einschränkungen). Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

>[!NOTE]
>
>Ab diesem Zeitpunkt beziehen sich alle Erwähnungen von „Administrator“ in diesem Dokument auf einen Produktadministrator oder höher (wie oben beschrieben).

Ein Workflow auf hoher Ebene zum Abrufen und Zuweisen von Zugriffsberechtigungen kann wie folgt zusammengefasst werden:

- Nach dem Abonnement für Adobe Experience Platform wird eine E-Mail an den Administrator gesendet, der im Registrierungsformular angegeben ist.
- Der Administrator meldet sich bei der [Adobe Admin Console](#adobe-admin-console) an und wählt **Adobe Experience Platform** aus der Liste der Produkte auf der Übersichtsseite aus.
- Der Administrator kann die standardmäßigen [Produktprofile](#product-profiles) anzeigen oder bei Bedarf neue Kundenproduktprofile erstellen.
- Der Administrator kann die Berechtigungen und Benutzer für alle vorhandenen Profile bearbeiten.
- When creating or editing a product profile, the administrator adds users to the profile using the **[!UICONTROL users]** tab, and grants permissions to these users (such as &quot;[!UICONTROL Read Datasets]&quot; or &quot;[!UICONTROL Manage Schemas]&quot;) by accessing the **[!UICONTROL permissions]** tab. Ebenso kann der Administrator über die gleiche Registerkarte „ „Berechtigungen“ Zugriff auf Sandboxen zuweisen.
- When users log in to the [!DNL Experience Platform] user interface, their access to [!DNL Platform] capabilities is driven by the permissions that have been granted to them from Step 2. For example, if a user does not have the &quot;[!UICONTROL View Datasets]&quot; permission, the *[!UICONTROL Datasets]* tab in the side menu will not be visible to that user.

For more detailed steps on how to manage access control in [!DNL Experience Platform], see the [access control user guide](./ui/overview.md).

All calls to [!DNL Experience Platform] APIs are validated for permissions, and will return errors if the appropriate permission(s) are not found in the current user context. In der Benutzeroberfläche werden Elemente je nach den dem aktuellen Benutzer zugewiesenen Berechtigungen ausgeblendet oder geändert.

## Adobe Admin Console

Die Adobe Admin Console bietet einen zentralen Speicherort für die Verwaltung der Adobe-Produktberechtigungen und den Zugriff für Ihr Unternehmen. Through the console, you can grant groups of users access permissions for various [!DNL Platform] capabilities, such as &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot;, or &quot;[!UICONTROL Manage Profiles]&quot;.

### Produktprofile

In the [!DNL Admin Console], permissions are assigned to users through the use of **[!UICONTROL product profiles]**. Mit den Produktprofilen können Sie einem oder mehreren Benutzern Berechtigungen erteilen und auch deren Zugriff auf den Umfang der Sandboxen einschließen, die ihnen über Produktprofile zugewiesen werden. Benutzer können einem oder mehreren Produktprofilen Ihres Unternehmens zugewiesen werden.

### Standard-Produktprofile

[!DNL Experience Platform] enthält zwei vorkonfigurierte Standard-Profil. Die folgende Tabelle zeigt, was in den einzelnen Standardprofilen bereitgestellt wird, einschließlich der Sandbox, auf die sie Zugriff gewähren, sowie der Berechtigungen, die sie im Rahmen dieser Sandbox gewähren.

| Produktprofile | Sandbox-Zugriff | Zugriffsberechtigung |
| --- | --- | --- |
| Standardproduktion – Zugriff auf alles | Produktion | All permissions applicable to [!DNL Experience Platform], except for Sandbox Administration permissions. |
| Standard-Sandbox-Administration | K. A. | Bietet nur Zugriff auf Sandbox-Administratorberechtigungen. |

## Sandboxen und Berechtigungen

[!DNL Experience Platform] bietet Zugriff auf eine Produktions-Sandbox und ermöglicht Ihnen das Erstellen von Nicht-Produktion- **Sandboxen**. Nicht-Produktion-Sandboxen sind eine Form der Datenvirtualisierung, mit der Sie Daten von anderen Sandboxen isolieren können und die üblicherweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. A product profile&#39;s **[!UICONTROL permissions]** give the profile&#39;s users access to [!DNL Platform] features within the sandbox environments to which they&#39;ve been granted access to.

For more information about sandboxes in [!DNL Experience Platform], please refer to the [sandboxes overview](../sandboxes/home.md).

### Zugriff auf Sandboxen

Der Zugriff auf Sandboxen wird über Produktprofile verwaltet. Ausführliche Anweisungen zum Aktivieren des Zugriffs auf eine Sandbox für ein Produktprofil finden Sie im [Benutzerhandbuch für die Zugriffskontrolle](./ui/overview.md).

Benutzern kann Zugriff auf eine oder mehrere Sandboxen innerhalb eines Profils gewährt werden. Wenn ein Benutzer in zwei oder mehr Produktprofilen enthalten ist, hat er Zugriff auf alle in diesen Profilen enthaltenen Sandboxen.

Die Berechtigung „Sandbox-Verwaltung“ ermöglicht Benutzern das Verwalten, Anzeigen oder Zurücksetzen von Sandboxen.

### Zugriffsberechtigung

Auf der Registerkarte **Berechtigungen** in einem Produktprofil werden die Sandboxen und Berechtigungen angezeigt, die für dieses Profil aktiv sind:

![](./images/permissions-overview.png)

Permissions that are granted through the [!DNL Admin Console] are sorted by category, with some permissions granting access to several low-level functionalities.

The following table outlines the available permissions for [!DNL Experience Platform] in the [!DNL Admin Console], with descriptions of the specific [!DNL Platform] capabilities they grant access to. Detaillierte Anweisungen zum Hinzufügen von Berechtigungen zu einem Produktprofil finden Sie im [Benutzerhandbuch für die Zugriffskontrolle](./ui/overview.md).

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Verwalten von Schemas] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Schemas und zugehörigen Ressourcen. |
| [!DNL Data Modeling] | [!UICONTROL Anzeigen von Schemas] | Schreibgeschützter Zugriff auf Schemas und zugehörige Ressourcen. |
| [!DNL Data Management] | [!UICONTROL Datensätze verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen. Schreibgeschützter Zugriff auf Schemas. |
| [!DNL Data Management] | [!UICONTROL Anzeigen von Datensätzen] | Schreibgeschützter Zugriff auf Datensätze und Schemas. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Schreibgeschützter Zugriff auf das Monitoring von Datensätzen und Streams. |
| [!DNL Profile Management] | [!UICONTROL Verwalten von Profilen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen, die für Kundenprofile verwendet werden. Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL Anzeigen von Profilen] | Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL Exportieren der Zielgruppe für das Segment] | Fähigkeit, eine ausgewertetes Zielgruppensegment in einen Datensatz zu exportieren. |
| [!DNL Identities] | [!UICONTROL Verwalten von Identitäts-Namensräumen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identitäts-Namensräumen. |
| [!DNL Identities] | [!UICONTROL Anzeigen von Identitäts-Namensräumen] | Schreibgeschützter Zugriff für Identitäts-Namensräume. |
| [!DNL Sandbox Administration] | [!UICONTROL Verwalten von Sandboxen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Sandboxen. |
| [!DNL Sandbox Administration] | [!UICONTROL Anzeigen von Sandboxen] | Schreibgeschützter Zugriff für Sandboxen Ihrer Organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Zurücksetzen einer Sandbox] | Fähigkeit, eine Sandbox zurückzusetzen. |
| [!DNL Destinations] | [!UICONTROL Verwalten von Zielen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Zielen.* |
| [!DNL Destinations] | [!UICONTROL Anzeigen von Zielen] | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte *[!UICONTROL Katalog]* und authentifizierte Ziele auf der Registerkarte *[!UICONTROL Durchsuchen]*.* |
| [!DNL Destinations] | [!UICONTROL Aktivieren von Zielen] | Fähigkeit zur Aktivierung von Daten an aktiven Zielen, die erstellt wurden. This permission requires either “View Destinations” or “Manage [!UICONTROL Destinations”] to be granted to the user who will activate destinations.* |
| [!DNL Data Ingestion] | [!UICONTROL Verwalten von Quellen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| [!DNL Data Ingestion] | [!UICONTROL Anzeigen von Quellen] | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte *[!UICONTROL Katalog]* und authentifizierte Quellen auf der Registerkarte *[!UICONTROL Durchsuchen]*. |
| [!DNL Data Science Workspace] | [!UICONTROL Verwalten des Data Science Workspace] | Access to read, create, edit, and delete in [!DNL Data Science Workspace]. |

_(*) Für diese Erlaubnis sind Bestimmungen erforderlich, die dies erfordern[!DNL Real-time Customer Data Platform]. Für weitere Informationen zu Echtzeit-CDP lesen Sie bitte zunächst die[Echtzeit-CDP – Übersicht](https://docs.adobe.com/content/help/de-DE/experience-platform/rtcdp/overview.html)._

## Nächste Schritte

By reading this guide, you have been introduced to the main principles of access control in [!DNL Experience Platform]. You can now continue to the [access control user guide](./ui/overview.md) for detailed steps on how use the [!DNL Admin Console] to create product profiles and assign permissions for [!DNL Platform].