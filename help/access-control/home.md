---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;Adobe Admin Console
solution: Experience Platform
title: Zugangssteuerung – Übersicht
description: Die Zugangssteuerung für Adobe Experience Platform wird über Adobe Admin Console geboten. Diese Funktion nutzt Produktprofile in Admin Console, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 88bfcdef65b4a938d573b1beb1952c7e030ebc13
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 65%

---

# Zugangssteuerung – Übersicht

Die Zugriffskontrolle für Adobe Experience Platform wird über das **[!UICONTROL Berechtigungen]** in [Adobe Experience Cloud](https://experience.adobe.com/). Diese Funktion nutzt Rollen und Richtlinien, die Benutzer mit Berechtigungen und Sandboxes verknüpfen.

## Zugangssteuerung zu Hierarchie und Workflow

Um die Zugriffskontrolle für Experience Platform zu konfigurieren, müssen Sie über System- oder Produktadministratorberechtigungen für ein Unternehmen verfügen, das über ein Experience Platform-Produkt verfügt. Die Mindestrolle, die Berechtigungen erteilen oder entziehen kann, ist ein Produktadministrator. Andere Administratorrollen, die Berechtigungen verwalten können, sind Systemadministratoren (keine Einschränkungen). Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

>[!NOTE]
>
>Ab diesem Zeitpunkt beziehen sich alle Erwähnungen von &quot;Administrator&quot;in diesem Dokument auf einen Produktadministrator oder höher (wie oben beschrieben).

Ein Workflow auf hoher Ebene zum Abrufen und Zuweisen von Zugriffsberechtigungen kann wie folgt zusammengefasst werden:

- Nach der Lizenzierung von Adobe Experience Platform oder einem Programm-Service, der Experience Platform verwendet, wird eine E-Mail an den Administrator gesendet, der während der Lizenzierung angegeben wurde.
- Der Administrator meldet sich bei der [Adobe Admin Console](#adobe-admin-console) an und wählt **Adobe Experience Platform** aus der Liste der Produkte auf der Übersichtsseite aus.
- Um Zugriff auf Experience Platform zu gewähren, muss der Administrator dem standardmäßigen Produktprofil Benutzer hinzufügen: `AEP-Default-All-Users`.
- Unter Benutzerberechtigungen kann der Administrator neue Experience Platformen erstellen oder die Berechtigungen und Benutzer für bestehende Rollen bearbeiten.
- Beim Erstellen oder Bearbeiten einer Rolle fügt der Administrator Benutzer mithilfe der **[!UICONTROL Benutzer]** und gewährt diesen Benutzern Berechtigungen (z. B.[!UICONTROL Datensätze lesen]&quot; oder &quot;[!UICONTROL Verwalten von Schemas]&quot;) durch Bearbeiten der Rollenberechtigungen. Ebenso kann der Administrator Sandboxes Zugriff über dieselbe Bearbeitungsoption zuweisen.
- Wenn sich Benutzer bei der Experience Platform-Benutzeroberfläche anmelden, wird ihr Zugriff auf die Experience Platform-Funktionen von den Berechtigungen bestimmt, die ihnen aus dem vorherigen Schritt erteilt wurden. Wenn ein Benutzer beispielsweise nicht über die [!UICONTROL Anzeigen von Datensätzen] Berechtigung, die **[!UICONTROL Datensätze]** -Registerkarte im Seitenmenü für diesen Benutzer nicht sichtbar sein.

Detailliertere Anweisungen zum Verwalten der Zugriffskontrolle in Experience Platform finden Sie im [Benutzerhandbuch für die Zugriffskontrolle](./ui/overview.md).

Alle Aufrufe von Experience Platform-APIs werden auf Berechtigungen überprüft und geben Fehler zurück, wenn die entsprechenden Berechtigungen im aktuellen Benutzerkontext nicht gefunden wurden. In der Benutzeroberfläche werden Elemente je nach den dem aktuellen Benutzer zugewiesenen Berechtigungen ausgeblendet oder geändert.

## Berechtigungen {#platform-permissions}

[!UICONTROL Berechtigungen] bietet einen zentralen Speicherort für die Verwaltung des Unternehmenszugriffs auf Experience Platformen. bis [!UICONTROL Berechtigungen]können Sie Benutzergruppen Zugriffsberechtigungen für verschiedene Experience Platform-Funktionen erteilen, z. B. [!UICONTROL Datensätze verwalten], [!UICONTROL Anzeigen von Datensätzen]oder [!UICONTROL Profile verwalten].

### Rollen

Im [!UICONTROL Rollen] -Abschnitt, werden Benutzern Berechtigungen über die Verwendung von Rollen zugewiesen. Rollen ermöglichen es Ihnen, einem oder mehreren Benutzern Berechtigungen zu gewähren und enthalten auch deren Zugriff auf den Umfang der Sandboxes, die ihnen über Rollen zugewiesen werden. Benutzer können einer oder mehreren Rollen Ihres Unternehmens zugewiesen werden.

### Standardrollen

Experience Platform verfügt über zwei vorkonfigurierte Standardrollen. Die folgende Tabelle zeigt, was in den einzelnen Standardprofilen bereitgestellt wird, einschließlich der Sandbox, auf die sie Zugriff gewähren, sowie der Berechtigungen, die sie im Rahmen dieser Sandbox gewähren.

| Rolle | Sandbox-Zugriff | Berechtigungen |
| --- | --- | --- |
| Standardproduktion – Zugriff auf alles | Produktion | Alle für Experience Platform geltenden Berechtigungen mit Ausnahme der Sandbox-Administratorberechtigungen. |
| Sandbox-Administratoren | K. A. | Bietet nur Zugriff auf Sandbox-Administratorberechtigungen. |

## Sandboxes und Berechtigungen

Nicht-Produktion-Sandboxes sind eine Form der Datenvirtualisierung, mit der Sie Daten von anderen Sandboxes isolieren können und die üblicherweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. Mit den Berechtigungen einer Rolle erhalten die Benutzer der Rolle Zugriff auf Experience Platform-Funktionen in den Sandbox-Umgebungen, auf die ihnen Zugriff gewährt wurde. Mit einer Standardlizenz für Experience Platform erhalten Sie fünf Sandboxes (eine zur Produktion und vier zur Nicht-Produktion). Sie können Pakete von jeweils zehn Nicht-Produktions-Sandboxes bis zu insgesamt maximal 75 Sandboxes hinzufügen. Wenden Sie sich an die Admins Ihrer Organisation oder das Adobe-Vertriebspersonal, um weitere Informationen zu erhalten.

Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md).

### Zugriff auf Sandboxes

Der Zugriff auf Sandboxes wird über Rollen verwaltet. Ausführliche Anweisungen zum Aktivieren des Zugriffs auf eine Sandbox für eine Rolle finden Sie unter [Rollenanleitung zur attributbasierten Zugriffskontrolle](./abac/ui/roles.md).

Benutzern kann Zugriff auf eine oder mehrere Sandboxes innerhalb einer Rolle gewährt werden. Wenn ein Benutzer in zwei oder mehr Rollen enthalten ist, hat er Zugriff auf alle Sandboxes, die in diesen Rollen enthalten sind.

Die Berechtigung „Sandbox-Verwaltung“ ermöglicht Benutzern das Verwalten, Anzeigen oder Zurücksetzen von Sandboxes.

### Ressourcenberechtigungen {#permissions}

Die Ressource [!UICONTROL Berechtigungen] -Registerkarte in einer Rolle zeigt die Sandboxes und Berechtigungen an, die für diese Rolle aktiv sind:

![permissions-overview](./images/permissions.png)

Berechtigungen, die über die Ressourcenberechtigungen gewährt werden, werden nach Kategorie sortiert, wobei einige Berechtigungen Zugriff auf verschiedene Funktionen auf niedriger Ebene gewähren.

In der folgenden Tabelle sind die für die Experience Platform in der Rolle verfügbaren Berechtigungen mit Beschreibungen der spezifischen Experience Platform-Funktionen, auf die sie Zugriff gewähren, aufgeführt. Ausführliche Anweisungen zum Hinzufügen von Berechtigungen zu einer Rolle finden Sie unter [Rollenanleitung zur attributbasierten Zugriffskontrolle](./abac/ui/roles.md).

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL Warnhinweisverlauf anzeigen] | Schreibgeschützter Zugriff auf den Warnhinweisverlauf. |
| [!DNL Alerts] | [!UICONTROL Auflösen von Warnhinweisen] | Zugriff zum Lesen, Bearbeiten und Löschen von Warnhinweisen. |
| [!DNL Alerts] | [!UICONTROL Anzeigen von Warnhinweisen] | Schreibgeschützter Zugriff auf Warnhinweise |
| [!DNL Alerts] | [!UICONTROL Verwalten von Warnhinweisen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen des Warnhinweisverlaufs. |
| [!DNL Data Hygiene] | [!UICONTROL Anzeigen der Datenhygiene] | Schreibgeschützter Zugriff auf die Datenhygiene. |
| [!DNL Data Hygiene] | [!UICONTROL Verwalten der Datenhygiene] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen der Datenhygiene. |
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
| [!DNL Identity Management] | [!UICONTROL Verwalten von Identitäts-Namensräumen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identitäts-Namensräumen. |
| [!DNL Identity Management] | [!UICONTROL Anzeigen von Identitäts-Namensräumen] | Schreibgeschützter Zugriff für Identitäts-Namensräume. |
| [!DNL Identity Management] | [!UICONTROL Anzeigen von Identitätsdiagrammen] | Schreibgeschützter Zugriff für Identitätsdiagramme. |
| [!DNL Sandbox Administration] | [!UICONTROL Verwalten von Sandboxes] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Sandboxes. |
| [!DNL Sandbox Administration] | [!UICONTROL Anzeigen von Sandboxes] | Schreibgeschützter Zugriff für Sandboxes Ihrer Organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Zurücksetzen einer Sandbox] | Fähigkeit, eine Sandbox zurückzusetzen. |
| [!DNL Destinations] | [!UICONTROL Verwalten von Zielen] | Zugriff zum Lesen, Erstellen und Löschen von Zielaktivierungsflüssen und Zielkonten. |
| [!DNL Destinations] | [!UICONTROL Anzeigen von Zielen] | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Ziele auf der Registerkarte **[!UICONTROL Durchsuchen]**. |
| [!DNL Destinations] | [!UICONTROL Aktivieren von Zielen] | Ermöglicht Benutzerinnen und Benutzern das Aktivieren von Segmenten für vorhandene Ziele. Aktiviert den Zuordnungsschritt im Aktivierungs-Workflow. Für diese Berechtigung ist es erforderlich, dass Benutzenden, die Daten für Ziele aktivieren, entweder [!UICONTROL Ziele anzeigen] oder [!UICONTROL Ziele verwalten] gewährt wird. |
| [!DNL Destinations] | [!UICONTROL Segment ohne Zuordnung aktivieren] | Ermöglicht das Aktivieren von Segmenten für vorhandene Ziele, ohne den [Zuordnungsschritt](../destinations/ui/activate-batch-profile-destinations.md#mapping) anzuzeigen. Benutzerinnen  und Bbenutzer können in Aktivierungs-Workflows Segmente, jedoch keine zugeordneten Attribute oder Identitäten hinzufügen oder entfernen. Diese Berechtigung erfordert, dass Benutzenden, die Daten für Ziele aktivieren, die Berechtigung [!UICONTROL Ziele aktivieren] gewährt wird. |
| [!DNL Destinations] | [!UICONTROL Verwalten und Aktivieren von Datensatzzielen] | Fähigkeit zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Datensatzexport-Flüssen. Außerdem die Fähigkeit zum Aktivieren von Daten an aktiven Zielen, die erstellt wurden. |
| [!DNL Destinations] | [!UICONTROL Ziel-Authoring] | Möglichkeit, Ziele mithilfe des [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md) zu erstellen. |
| [!DNL Data Ingestion] | [!UICONTROL Verwalten von Quellen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| [!DNL Data Ingestion] | [!UICONTROL Anzeigen von Quellen] | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Quellen auf der Registerkarte **[!UICONTROL Durchsuchen]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Zugriff zum Erstellen, Akzeptieren und Ablehnen von Partner-Handshakes, um zwei Organisationen miteinander zu verbinden und [!DNL Segment Match]-Flüsse zu aktivieren. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Veröffentlichen von [!DNL Segment Match]-Feeds mit aktiven Partnern. |
| [!DNL Data Science Workspace] | [!UICONTROL Verwalten des Data Science Workspace] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen in [!DNL Data Science Workspace]. |
| Data Governance | [!UICONTROL Anwenden von Datennutzungskennzeichnungen] | Zugriff zum Lesen, Erstellen und Löschen von Datennutzungskennzeichnungen. |
| Data Governance | [!UICONTROL Verwalten von Datennutzungsrichtlinien] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datennutzungsrichtlinien. |
| Data Governance | [!UICONTROL Anzeigen von Datennutzungsrichtlinien] | Schreibgeschützter Zugriff auf Datennutzungsrichtlinien Ihres Unternehmens. |
| Data Governance | [!UICONTROL Anzeigen des Benutzer-Aktivitätspotokolls] | Schreibgeschützter Zugriff zur Anzeige aufgezeichneter [Administratorprotokolle](../landing/governance-privacy-security/audit-logs/overview.md) von Platform-Aktivitäten. |
| [!DNL Dashboards] | [!UICONTROL Anzeigen des Dashboards zur Lizenznutzung] | Schreibgeschützter Zugriff zum Anzeigen des Dashboards zur Lizenznutzung. |
| [!DNL Dashboards] | [!UICONTROL Standard-Dashboards verwalten] | Fügen Sie benutzerdefinierte Attribute hinzu, die sich noch nicht im Data Warehouse befinden. |
| [!DNL Query Service] | [!UICONTROL Verwalten von Abfragen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen strukturierter SQL-Abfragen für Platform-Daten. |
| [!DNL Query Service] | [!UICONTROL Verwalten der Integration des Abfrage-Service] | Zugriff auf das Erstellen, Aktualisieren und Löschen nicht ablaufender Anmeldeinformationen für den Zugriff auf den Abfrage-Service. |

## Nächste Schritte

Durch Lesen dieses Handbuchs wurden Sie mit den Hauptgrundsätzen der Zugriffskontrolle in Experience Platform vertraut gemacht. Sie können jetzt mit dem [Benutzerhandbuch zur attributbasierten Zugriffskontrolle](./abac/overview.md) für detaillierte Anweisungen zur Verwendung von Experience Cloud zum Erstellen von Rollen und zum Zuweisen von Berechtigungen für die Experience Platform.
