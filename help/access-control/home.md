---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;Adobe Admin Console
solution: Experience Platform
title: Zugangssteuerung – Übersicht
description: Die Zugangssteuerung für Adobe Experience Platform wird über Adobe Admin Console geboten. Diese Funktion nutzt Produktprofile in Admin Console, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 84%

---

# Zugangssteuerung – Übersicht

Die Zugriffssteuerung für Adobe Experience Platform erfolgt über die **[!UICONTROL Berechtigungen]** in [Adobe Experience Cloud](https://experience.adobe.com/). Diese Funktion nutzt Produktprofile und Richtlinien, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen.

## Zugangssteuerung zu Hierarchie und Workflow

Zum Konfigurieren der Zugriffssteuerung für Experience Platform müssen Sie system- oder produkbezogene Administratorrechte für ein Unternehmen besitzen, das über ein Experience Platform-Produkt verfügt. Zum Erteilen oder Entziehen von Berechtigungen ist mindestens eine Produktadmin-Rolle erforderlich. Zu einer anderen Administratorrolle, die Berechtigungen verwalten können, gehören die Systemadmins (keine Einschränkungen). Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

>[!NOTE]
>
>Von hier an beziehen sich alle Erwähnungen von Administrierenden in diesem Dokument auf Produktadmins oder höhere Rollen (wie oben beschrieben).

Ein Workflow auf hoher Ebene zum Abrufen und Zuweisen von Zugriffsberechtigungen kann wie folgt zusammengefasst werden:

- Nach der Lizenzierung von Adobe Experience Platform oder einem Programm-Service, der Experience Platform verwendet, wird eine E-Mail an den Administrator gesendet, der während der Lizenzierung angegeben wurde.
- Administrierende melden sich bei der [Adobe Admin Console](#adobe-admin-console) an und wählen **Adobe Experience Platform** aus der Liste der Produkte auf der Übersichtsseite aus.
- Um Zugriff auf Experience Platform zu gewähren, müssen Administrierende dem standardmäßigen Produktprofil `AEP-Default-All-Users` Benutzende hinzufügen.
- Über Experience Platform-Berechtigungen können Administrierende neue Rollen erstellen oder die Berechtigungen und Benutzenden für vorhandene Rollen bearbeiten.
- Beim Erstellen oder Bearbeiten einer Rolle fügen Administrierende der Rolle über die Registerkarte **[!UICONTROL Benutzende]** Benutzende hinzu und gewähren durch Bearbeiten der Rollenberechtigungen diesen Benutzenden Berechtigungen (z. B. [!UICONTROL Datensätze lesen] oder [!UICONTROL Schemata verwalten]). Ebenso können Administrierende mithilfe derselben Bearbeitungsoption Zugriff auf Sandboxes zuweisen.
- Wenn sich Benutzende bei der Benutzeroberfläche von Experience Platform anmelden, wird ihr Zugriff auf Experience Platform-Funktionen durch die Berechtigungen gesteuert, die ihnen im vorherigen Schritt erteilt wurden. Wenn eine Benutzerin oder ein Benutzer beispielsweise nicht über die Berechtigung [!UICONTROL Datensätze anzeigen] verfügt, ist im Seitenmenü die Registerkarte **[!UICONTROL Datensätze]** für diese Benutzerin oder diesen Benutzer nicht sichtbar.

Detailliertere Anweisungen zum Verwalten der Zugriffskontrolle in Experience Platform finden Sie im [Benutzerhandbuch für die Zugriffskontrolle](./ui/overview.md).

Alle Aufrufe von Experience Platform-APIs werden auf Berechtigungen überprüft und geben Fehler zurück, wenn die entsprechenden Berechtigungen im aktuellen Benutzerkontext nicht gefunden wurden. In der Benutzeroberfläche werden Elemente je nach den dem aktuellen Benutzer zugewiesenen Berechtigungen ausgeblendet oder geändert.

## Berechtigungen {#platform-permissions}

Der Bereich [!UICONTROL Berechtigungen] bietet einen zentralen Ort für die Verwaltung des Experience Platform-Zugriffs für Ihr Unternehmen. Über [!UICONTROL Berechtigungen] können Sie Benutzergruppen Zugriffsberechtigungen für verschiedene Experience Platform-Funktionen erteilen, wie z. B. [!UICONTROL Datensätze verwalten], [!UICONTROL Datensätze anzeigen] oder [!UICONTROL Profile verwalten].

### Rollen

Im Abschnitt [!UICONTROL Rollen] werden Benutzenden durch die Verwendung von Rollen Berechtigungen zugewiesen. Mithilfe von Rollen können Sie einer Benutzerin oder einem Benutzer bzw. mehreren Benutzenden Berechtigungen erteilen und zudem deren Zugriff auf die Sandboxes beschränken, die ihnen über Rollen zugewiesen sind. Benutzende können einer oder mehreren Rollen Ihres Unternehmens zugewiesen werden.

### Standardrollen

Experience Platform verfügt über zwei vorkonfigurierte Standardrollen. Die folgende Tabelle zeigt, was in den einzelnen Standardprofilen bereitgestellt wird, einschließlich der Sandbox, auf die sie Zugriff gewähren, sowie der Berechtigungen, die sie im Rahmen dieser Sandbox gewähren.

| Rolle | Sandbox-Zugriff | Berechtigungen |
| --- | --- | --- |
| Standardproduktion – Zugriff auf alles | Produktion | Alle für Experience Platform geltenden Berechtigungen mit Ausnahme der Sandbox-Administratorberechtigungen. |
| Sandbox-Administratoren | K. A. | Bietet nur Zugriff auf Sandbox-Administratorberechtigungen. |

## Sandboxes und Berechtigungen

Nicht-Produktion-Sandboxes sind eine Form der Datenvirtualisierung, mit der Sie Daten von anderen Sandboxes isolieren können und die üblicherweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. Die Berechtigungen einer Rolle geben den Benutzenden der Rolle Zugriff auf Experience Platform-Funktionen innerhalb der Sandbox-Umgebungen, auf die ihnen Zugriff gewährt wurde. Mit einer Standardlizenz für Experience Platform erhalten Sie fünf Sandboxes (eine zur Produktion und vier zur Nicht-Produktion). Sie können Pakete von jeweils zehn Nicht-Produktions-Sandboxes bis zu insgesamt maximal 75 Sandboxes hinzufügen. Wenden Sie sich an die Admins Ihrer Organisation oder das Adobe-Vertriebspersonal, um weitere Informationen zu erhalten.

Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md).

### Zugriff auf Sandboxes

Der Zugriff auf Sandboxes wird über Rollen verwaltet. Ausführliche Anweisungen zum Aktivieren des Zugriffs auf eine Sandbox für eine Rolle finden Sie unter [„Rollen“ im Handbuch zur attributbasierten Zugriffssteuerung](./abac/ui/roles.md).

Benutzenden kann Zugriff auf eine oder mehrere Sandboxes innerhalb einer Rolle gewährt werden. Wenn eine Benutzerin oder ein Benutzer in zwei oder mehr Rollen enthalten ist, hat diese Person Zugriff auf alle in diesen Rollen enthaltenen Sandboxes.

Die Berechtigung „Sandbox-Verwaltung“ ermöglicht Benutzenden das Verwalten, Anzeigen oder Zurücksetzen von Sandboxes.

### Ressourcenberechtigungen {#permissions}

Auf der Registerkarte für [!UICONTROL Ressourcenberechtigungen] innerhalb einer Rolle werden die Sandboxes und Berechtigungen angezeigt, die für diese Rolle aktiv sind:

![permissions-overview](./images/permissions.png)

Berechtigungen, die über die Ressourcenberechtigungen gewährt werden, werden nach Kategorie sortiert. Einige dieser Berechtigungen gewähren Zugriff auf verschiedene Funktionen niedriger Ebene.

In der folgenden Tabelle stehen die verfügbaren Berechtigungen für Experience Platform in der Rolle, einschließlich Beschreibungen der spezifischen Experience Platform-Funktionen, auf die sie Zugriff gewähren. Ausführliche Anweisungen zum Hinzufügen von Berechtigungen zu einer Rolle finden Sie unter [„Rollen“ im Handbuch zur attributbasierten Zugangssteuerung](./abac/ui/roles.md).

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL Warnhinweisverlauf anzeigen] | Schreibgeschützter Zugriff auf den Warnhinweisverlauf. |
| [!DNL Alerts] | [!UICONTROL Auflösen von Warnhinweisen] | Zugriff zum Lesen, Bearbeiten und Löschen von Warnhinweisen. |
| [!DNL Alerts] | [!UICONTROL Anzeigen von Warnhinweisen] | Schreibgeschützter Zugriff auf Warnhinweise |
| [!DNL Alerts] | [!UICONTROL Verwalten von Warnhinweisen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen des Warnhinweisverlaufs. |
| [!DNL Computed Attributes] | [!UICONTROL Berechnete Attribute anzeigen] | Schreibgeschützter Zugriff für die Registerkarte, den Bestand und Details berechneter Attribute. |
| [!DNL Computed Attributes] | [!UICONTROL Berechnete Attribute verwalten] | Zugriff auf das Lesen, Erstellen, Löschen und Deaktivieren berechneter Attribute. |
| [!DNL Data Lifecycle] | [!UICONTROL Datenlebenszyklus anzeigen] | Schreibgeschützter Zugriff für den Datenlebenszyklus. |
| [!DNL Data Lifecycle] | [!UICONTROL Data Lebenszyklus verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen des Datenlebenszyklus. |
| [!DNL Data Modeling] | [!UICONTROL Verwalten von Schemas] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Schemas und zugehörigen Ressourcen. |
| [!DNL Data Modeling] | [!UICONTROL Anzeigen von Schemas] | Schreibgeschützter Zugriff auf Schemas und zugehörige Ressourcen. |
| [!DNL Data Modeling] | [!UICONTROL Verwalten von Beziehungen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Schema-Beziehungen. |
| [!DNL Data Modeling] | [!UICONTROL Verwalten von Identitätsmetadaten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identitätsmetadaten für Schemata. |
| [!DNL Data Management] | [!UICONTROL Datensätze verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen. Schreibgeschützter Zugriff auf Schemas. |
| [!DNL Data Management] | [!UICONTROL Anzeigen von Datensätzen] | Schreibgeschützter Zugriff auf Datensätze und Schemas. |
| [!DNL Data Management] | [!UICONTROL Datenüberwachung] | Schreibgeschützter Zugriff auf das Monitoring von Datensätzen und Streams. |
| [!DNL Profile Management] | [!UICONTROL Verwalten von Profilen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen, die für Kundenprofile verwendet werden. Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL Anzeigen von Profilen] | Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL Segmente verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Segmenten. |
| [!DNL Profile Management] | [!UICONTROL Anzeigen von Segmenten] | Schreibgeschützter Zugriff auf verfügbare Segmente. |
| [!DNL Profile Management] | [!UICONTROL Verwalten von Zusammenführungsrichtlinien] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Zusammenführungsrichtlinien. |
| [!DNL Profile Management] | [!UICONTROL Anzeigen von Zusammenführungsrichtlinien] | Schreibgeschützter Zugriff auf verfügbare Zusammenführungsrichtlinien. |
| [!DNL Profile Management] | [!UICONTROL Exportieren der Zielgruppe für das Segment] | Fähigkeit, eine ausgewertetes Zielgruppensegment in einen Datensatz zu exportieren. |
| [!DNL Profile Management] | [!UICONTROL Auswerten von Segmenten für eine Zielgruppe] | Möglichkeit, Profile für eine Zielgruppe zu generieren, indem eine Segmentdefinition ausgewertet wird. |
| [!DNL Profile Management] | [!UICONTROL B2B AI anzeigen] | Schreibgeschützter Zugriff auf Einstellungen und Konfigurationen für alle B2B AI/ML-Dienste. |
| [!DNL Profile Management] | [!UICONTROL B2B AI verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Einstellungen und Konfigurationen für alle B2B AI/ML-Dienste. |
| [!DNL Profile Management] | [!UICONTROL B2B-Profil anzeigen] | Schreibgeschützter Zugriff auf B2B-Entitätsprofile (z. B. Konto, Chancen usw.), Einstellungen und Konfigurationen für alle B2B AI/ML-Dienste und B2B-Dashboard-Widgets. |
| [!DNL Profile Management] | [!UICONTROL B2B-Profil verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von B2B-Entitätsprofilen (z. B. Konto, Chancen usw.). Schreibgeschützter Zugriff für Einstellungen und Konfigurationen für alle B2B AI/ML-Dienste und B2B-Dashboard-Widgets. |
| [!DNL Identity Management] | [!UICONTROL Verwalten von Identitäts-Namensräumen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identitäts-Namensräumen. |
| [!DNL Identity Management] | [!UICONTROL Anzeigen von Identitäts-Namensräumen] | Schreibgeschützter Zugriff für Identitäts-Namensräume. |
| [!DNL Identity Management] | [!UICONTROL Anzeigen von Identitätsdiagrammen] | Schreibgeschützter Zugriff für Identitätsdiagramme. |
| [!DNL Sandbox Administration] | [!UICONTROL Verwalten von Sandboxes] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Sandboxes. |
| [!DNL Sandbox Administration] | [!UICONTROL Anzeigen von Sandboxes] | Schreibgeschützter Zugriff für Sandboxes Ihrer Organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Zurücksetzen einer Sandbox] | Fähigkeit, eine Sandbox zurückzusetzen. |
| [!DNL Destinations] | [!UICONTROL Anzeigen von Zielen] | Schreibgeschützter Zugriff zur Anzeige der verfügbaren Ziele im **[!UICONTROL Katalog]** Registerkarte und authentifizierte Ziele im **[!UICONTROL Durchsuchen]** Registerkarte. |
| [!DNL Destinations] | [!UICONTROL Verwalten von Zielen] | Zugriff auf das Lesen, Erstellen und Löschen von Zielverbindungen und Zielkonten. |
| [!DNL Destinations] | [!UICONTROL Aktivieren von Zielen] | Ermöglicht Benutzerinnen und Benutzern das Aktivieren von Segmenten für vorhandene Ziele. Aktiviert den Zuordnungsschritt im Aktivierungs-Workflow. Diese Berechtigung erfordert auch die [!UICONTROL Ziele anzeigen] -Berechtigung für den Benutzer, der Daten für Ziele aktiviert. |
| [!DNL Destinations] | [!UICONTROL Segment ohne Zuordnung aktivieren] | Ermöglicht das Aktivieren von Segmenten für vorhandene Ziele, ohne den [Zuordnungsschritt](../destinations/ui/activate-batch-profile-destinations.md#mapping) anzuzeigen. Benutzerinnen  und Bbenutzer können in Aktivierungs-Workflows Segmente, jedoch keine zugeordneten Attribute oder Identitäten hinzufügen oder entfernen. Diese Berechtigung erfordert auch die [!UICONTROL Ziele anzeigen] -Berechtigung für den Benutzer, der Daten für Ziele aktiviert. |
| [!DNL Destinations] | [!UICONTROL Verwalten und Aktivieren von Datensatzzielen] | Fähigkeit zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Datensatzexport-Flüssen. Möglichkeit, auch Daten für aktive Datensätze zu aktivieren, die erstellt wurden. Diese Berechtigung erfordert auch die [!UICONTROL Ziele anzeigen] -Berechtigung für den Benutzer, der Daten für Ziele aktiviert. |
| [!DNL Destinations] | [!UICONTROL Ziel-Authoring] | Möglichkeit, Ziele mithilfe des [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md) zu erstellen. |
| [!DNL Data Ingestion] | [!UICONTROL Verwalten von Quellen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| [!DNL Data Ingestion] | [!UICONTROL Anzeigen von Quellen] | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Quellen auf der Registerkarte **[!UICONTROL Durchsuchen]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Zugriff zum Erstellen, Akzeptieren und Ablehnen von Partner-Handshakes, um zwei Organisationen miteinander zu verbinden und [!DNL Segment Match]-Flüsse zu aktivieren. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Veröffentlichen von [!DNL Segment Match]-Feeds mit aktiven Partnern. |
| [!DNL Data Science Workspace] | [!UICONTROL Verwalten des Data Science Workspace] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen in [!DNL Data Science Workspace]. |
| Data Governance | [!UICONTROL Nutzungsbezeichnungen verwalten] | Zugriff zum Lesen, Erstellen und Löschen von Datennutzungskennzeichnungen. |
| Data Governance | [!UICONTROL Verwalten von Datennutzungsrichtlinien] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datennutzungsrichtlinien. |
| Data Governance | [!UICONTROL Anzeigen von Datennutzungsrichtlinien] | Schreibgeschützter Zugriff auf Datennutzungsrichtlinien Ihres Unternehmens. |
| Data Governance | [!UICONTROL Anzeigen des Benutzer-Aktivitätspotokolls] | Schreibgeschützter Zugriff zur Anzeige aufgezeichneter [Administratorprotokolle](../landing/governance-privacy-security/audit-logs/overview.md) von Platform-Aktivitäten. |
| [!DNL Dashboards] | [!UICONTROL Anzeigen des Dashboards zur Lizenznutzung] | Schreibgeschützter Zugriff zum Anzeigen des Dashboards zur Lizenznutzung. |
| [!DNL Dashboards] | [!UICONTROL Standard-Dashboards verwalten] | Fügen Sie benutzerdefinierte Attribute hinzu, die sich noch nicht im Data Warehouse befinden. |
| [!DNL Query Service] | [!UICONTROL Verwalten von Abfragen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen strukturierter SQL-Abfragen für Platform-Daten. |
| [!DNL Query Service] | [!UICONTROL Verwalten der Integration des Abfrage-Service] | Zugriff auf das Erstellen, Aktualisieren und Löschen nicht ablaufender Anmeldeinformationen für den Zugriff auf den Abfrage-Service. |

## Nächste Schritte

Durch Lesen dieses Handbuchs wurden Sie mit den Hauptgrundsätzen der Zugriffskontrolle in Experience Platform vertraut gemacht. Sie können jetzt mit dem [Benutzerhandbuch zur attributbasierten Zugriffssteuerung](./abac/overview.md) fortfahren. Darin finden Sie ausführliche Anweisungen dazu, wie Sie mit Experience Cloud Rollen erstellen und Berechtigungen für Experience Platform zuweisen können.
