---
keywords: Experience Platform;home;popular topics;access control;adobe admin console
solution: Experience Platform
topic: overview
title: Zugriffskontrolle – Übersicht
description: Die Zugriffskontrolle für Adobe Experience Platform erfolgt über die Adobe Admin Console. Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen.
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 61%

---


# Zugriffskontrolle – Übersicht

Access control for [!DNL Experience Platform] is provided through the [Adobe Admin Console](https://adminconsole.adobe.com). This functionality leverages product profiles in [!DNL Admin Console], which link users with permissions and sandboxes.

## Zugriffskontrolle auf Hierarchie und Workflow

In order to configure access control for [!DNL Experience Platform], you must have administrator privileges for an organization that has an [!DNL Experience Platform] product integration. Die Mindestrolle, die Berechtigungen erteilt oder entzieht, ist ein Produktprofil-Administrator. Andere Administratorrollen, die Berechtigungen verwalten können, sind Produktadministratoren (kann alle Profile innerhalb eines Produkts verwalten) und Systemadministratoren (keine Einschränkungen). Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

>[!NOTE]
>
>Ab diesem Zeitpunkt beziehen sich alle Erwähnungen von „Administrator“ in diesem Dokument auf einen Produktadministrator oder höher (wie oben beschrieben).

Ein Workflow auf hoher Ebene zum Abrufen und Zuweisen von Zugriffsberechtigungen kann wie folgt zusammengefasst werden:

- Nach der Lizenzierung von Adobe Experience Platform oder einem Anwendungs-/App-Dienst, der Experience Platform verwendet, wird eine E-Mail an den Administrator gesendet, der während der Lizenzierung angegeben wurde.
- Der Administrator meldet sich bei der [Adobe Admin Console](#adobe-admin-console) an und wählt **Adobe Experience Platform** aus der Liste der Produkte auf der Übersichtsseite aus.
- Der Administrator kann die standardmäßigen [Produktprofile](#product-profiles) anzeigen oder bei Bedarf neue Kundenproduktprofile erstellen.
- Der Administrator kann die Berechtigungen und Benutzer für alle vorhandenen Profile bearbeiten.
- When creating or editing a product profile, the administrator adds users to the profile using the **[!UICONTROL users]** tab, and grants permissions to these users (such as &quot;[!UICONTROL Read Datasets]&quot; or &quot;[!UICONTROL Manage Schemas]&quot;) by accessing the **[!UICONTROL permissions]** tab. Ebenso kann der Administrator über die gleiche Registerkarte „ „Berechtigungen“ Zugriff auf Sandboxes zuweisen.
- When users log in to the [!DNL Experience Platform] user interface, their access to [!DNL Platform] capabilities is driven by the permissions that have been granted to them from Step 2. For example, if a user does not have the &quot;[!UICONTROL View Datasets]&quot; permission, the **[!UICONTROL Datasets]** tab in the side menu will not be visible to that user.

For more detailed steps on how to manage access control in [!DNL Experience Platform], see the [access control user guide](./ui/overview.md).

All calls to [!DNL Experience Platform] APIs are validated for permissions, and will return errors if the appropriate permission(s) are not found in the current user context. In der Benutzeroberfläche werden Elemente je nach den dem aktuellen Benutzer zugewiesenen Berechtigungen ausgeblendet oder geändert.

## Adobe Admin Console

Die Adobe Admin Console bietet einen zentralen Speicherort für die Verwaltung der Adobe-Produktberechtigungen und den Zugriff für Ihr Unternehmen. Through the console, you can grant groups of users access permissions for various [!DNL Platform] capabilities, such as &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot;, or &quot;[!UICONTROL Manage Profiles]&quot;.

### Produktprofile

In the [!DNL Admin Console], permissions are assigned to users through the use of product profiles. Mit den Produktprofilen können Sie einem oder mehreren Benutzern Berechtigungen erteilen und auch deren Zugriff auf den Umfang der Sandboxes einschließen, die ihnen über Produktprofile zugewiesen werden. Benutzer können einem oder mehreren Produktprofilen Ihres Unternehmens zugewiesen werden.

### Standard-Produktprofile

[!DNL Experience Platform] enthält zwei vorkonfigurierte Standard-Profil. Die folgende Tabelle zeigt, was in den einzelnen Standardprofilen bereitgestellt wird, einschließlich der Sandbox, auf die sie Zugriff gewähren, sowie der Berechtigungen, die sie im Rahmen dieser Sandbox gewähren.

| Produktprofile | Sandbox-Zugriff | Berechtigungen |
| --- | --- | --- |
| Standardproduktion – Zugriff auf alles | Produktion | All permissions applicable to [!DNL Experience Platform], except for Sandbox Administration permissions. |
| Standard-Sandbox-Administration | K. A. | Bietet nur Zugriff auf Sandbox-Administratorberechtigungen. |

## Sandboxes und Berechtigungen

Nicht-Produktion-Sandboxes sind eine Form der Datenvirtualisierung, mit der Sie Daten von anderen Sandboxes isolieren können und die üblicherweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. A product profile&#39;s permissions give the profile&#39;s users access to [!DNL Platform] features within the sandbox environments to which they&#39;ve been granted access to. Mit einer Standardlizenz für Experience Platformen erhalten Sie fünf Sandboxen (eine Produktion und vier Nicht-Produktion). Sie können Pakete von zehn Nicht-Produktions-Sandboxen bis zu maximal 75 Sandboxen hinzufügen. Für weitere Informationen wenden Sie sich bitte an Ihren IMS-Organisationsadministrator oder Ihren Vertriebsmitarbeiter für Adoben.

For more information about sandboxes in [!DNL Experience Platform], please refer to the [sandboxes overview](../sandboxes/home.md).

### Zugriff auf Sandboxes

Der Zugriff auf Sandboxes wird über Produktprofile verwaltet. Ausführliche Anweisungen zum Aktivieren des Zugriffs auf eine Sandbox für ein Produktprofil finden Sie im [Benutzerhandbuch für die Zugriffskontrolle](./ui/overview.md).

Benutzern kann Zugriff auf eine oder mehrere Sandboxes innerhalb eines Profils gewährt werden. Wenn ein Benutzer in zwei oder mehr Produktprofilen enthalten ist, hat er Zugriff auf alle in diesen Profilen enthaltenen Sandboxes.

Die Berechtigung „Sandbox-Verwaltung“ ermöglicht Benutzern das Verwalten, Anzeigen oder Zurücksetzen von Sandboxes.

### Berechtigungen

Auf der Registerkarte Berechtigungen in einem Produktprofil werden die Sandboxes und Berechtigungen angezeigt, die für dieses Profil aktiv sind:

![](./images/permissions-overview.png)

Permissions that are granted through the [!DNL Admin Console] are sorted by category, with some permissions granting access to several low-level functionalities.

The following table outlines the available permissions for [!DNL Experience Platform] in the [!DNL Admin Console], with descriptions of the specific [!DNL Platform] capabilities they grant access to. Detaillierte Anweisungen zum Hinzufügen von Berechtigungen zu einem Produktprofil finden Sie im [Benutzerhandbuch für die Zugriffskontrolle](./ui/overview.md).

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Verwalten von Schemas] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Schemas und zugehörigen Ressourcen. |
| [!DNL Data Modeling] | [!UICONTROL Anzeigen von Schemas] | Schreibgeschützter Zugriff auf Schemas und zugehörige Ressourcen. |
| [!DNL Data Management] | [!UICONTROL Datensätze verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen. Schreibgeschützter Zugriff auf Schemas. |
| [!DNL Data Management] | [!UICONTROL Anzeigen von Datensätzen] | Schreibgeschützter Zugriff auf Datensätze und Schemas. |
| [!DNL Data Management] | [!UICONTROL Datenüberwachung] | Schreibgeschützter Zugriff auf das Monitoring von Datensätzen und Streams. |
| [!DNL Profile Management] | [!UICONTROL Verwalten von Profilen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen, die für Kundenprofile verwendet werden. Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL Anzeigen von Profilen] | Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL Exportieren der Zielgruppe für das Segment] | Fähigkeit, eine ausgewertetes Zielgruppensegment in einen Datensatz zu exportieren. |
| [!DNL Identities] | [!UICONTROL Verwalten von Identitäts-Namensräumen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identitäts-Namensräumen. |
| [!DNL Identities] | [!UICONTROL Anzeigen von Identitäts-Namensräumen] | Schreibgeschützter Zugriff für Identitäts-Namensräume. |
| [!DNL Sandbox Administration] | [!UICONTROL Verwalten von Sandboxes] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Sandboxes. |
| [!DNL Sandbox Administration] | [!UICONTROL Anzeigen von Sandboxes] | Schreibgeschützter Zugriff für Sandboxes Ihrer Organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Zurücksetzen einer Sandbox] | Fähigkeit, eine Sandbox zurückzusetzen. |
| [!DNL Destinations] | [!UICONTROL Verwalten von Zielen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Zielen.* |
| [!DNL Destinations] | [!UICONTROL Anzeigen von Zielen] | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Ziele auf der Registerkarte **[!UICONTROL Durchsuchen]**.* |
| [!DNL Destinations] | [!UICONTROL Aktivieren von Zielen] | Fähigkeit zur Aktivierung von Daten an aktiven Zielen, die erstellt wurden. This permission requires either “View Destinations” or “Manage [!UICONTROL Destinations”] to be granted to the user who will activate destinations.* |
| [!DNL Data Ingestion] | [!UICONTROL Verwalten von Quellen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| [!DNL Data Ingestion] | [!UICONTROL Anzeigen von Quellen] | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Quellen auf der Registerkarte **[!UICONTROL Durchsuchen]**. |
| [!DNL Data Science Workspace] | [!UICONTROL Verwalten des Data Science Workspace] | Access to read, create, edit, and delete in [!DNL Data Science Workspace]. |

_(*) Für diese Erlaubnis sind Bestimmungen erforderlich, die dies erfordern[!DNL Real-time Customer Data Platform]. Für weitere Informationen zur Echtzeit-Kundendatenplattform lesen Sie bitte zunächst die[Echtzeit-Kundendatenplattform – Übersicht](https://docs.adobe.com/content/help/de-DE/experience-platform/rtcdp/overview.html)._

## Nächste Schritte

By reading this guide, you have been introduced to the main principles of access control in [!DNL Experience Platform]. You can now continue to the [access control user guide](./ui/overview.md) for detailed steps on how use the [!DNL Admin Console] to create product profiles and assign permissions for [!DNL Platform].