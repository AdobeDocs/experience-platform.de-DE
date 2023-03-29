---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;Adobe Admin Console
solution: Experience Platform
title: Zugangssteuerung – Übersicht
description: Die Zugangssteuerung für Adobe Experience Platform wird über Adobe Admin Console geboten. Diese Funktion nutzt Produktprofile in Admin Console, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 93%

---

# Zugangssteuerung – Übersicht

Die Zugangssteuerung für [!DNL Experience Platform] wird über [Adobe Admin Console](https://adminconsole.adobe.com) geboten. Diese Funktion nutzt Produktprofile in [!DNL Admin Console], um Anwender mit Berechtigungen und Sandboxes zu verknüpfen.

## Zugangssteuerung zu Hierarchie und Workflow

Zum Konfigurieren der Zugangssteuerung für [!DNL Experience Platform] müssen Sie Administratorrechte für ein Unternehmen haben, das über eine [!DNL Experience Platform]-Produktintegration verfügt. Die Mindestrolle, die Berechtigungen erteilt oder entzieht, ist ein Produktprofil-Administrator. Andere Administratorrollen, die Berechtigungen verwalten können, sind Produktadministratoren (kann alle Profile innerhalb eines Produkts verwalten) und Systemadministratoren (keine Einschränkungen). Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

>[!NOTE]
>
>Ab diesem Zeitpunkt beziehen sich alle Erwähnungen von „Administrator“ in diesem Dokument auf einen Produktadministrator oder höher (wie oben beschrieben).

Ein Workflow auf hoher Ebene zum Abrufen und Zuweisen von Zugriffsberechtigungen kann wie folgt zusammengefasst werden:

- Nach der Lizenzierung von Adobe Experience Platform oder einem Programm-Service, der Experience Platform verwendet, wird eine E-Mail an den Administrator gesendet, der während der Lizenzierung angegeben wurde.
- Der Administrator meldet sich bei der [Adobe Admin Console](#adobe-admin-console) an und wählt **Adobe Experience Platform** aus der Liste der Produkte auf der Übersichtsseite aus.
- Der Administrator kann die standardmäßigen [Produktprofile](#product-profiles) anzeigen oder bei Bedarf neue Kundenproduktprofile erstellen.
- Der Administrator kann die Berechtigungen und Benutzer für alle vorhandenen Profile bearbeiten.
- Beim Erstellen oder Bearbeiten eines Profils fügt der Administrator dem Profil über den Tab **[!UICONTROL Benutzer]** Benutzer hinzu und gewährt diesen Benutzern Berechtigungen (wie z. B. [!UICONTROL Datensätze lesen] oder [!UICONTROL Schemas verwalten]), indem er auf den Tab **[!UICONTROL Berechtigungen]** zugreift. Ebenso kann der Administrator über die gleiche Registerkarte „Berechtigungen“ Zugriff auf Sandboxes zuweisen.
- Wenn sich Benutzer bei der Benutzeroberfläche von [!DNL Experience Platform] anmelden, wird ihr Zugriff auf [!DNL Platform]-Funktionen durch die Berechtigungen gesteuert, die ihnen in Schritt 2 erteilt wurden. Wenn ein Benutzer beispielsweise nicht über die Zugriffsberechtigung [!UICONTROL Datensätze anzeigen] verfügt, ist der Tab **[!UICONTROL Datensätze]** im Seitenmenü für diesen Benutzer nicht sichtbar.

Detailliertere Anweisungen zum Verwalten der Zugangssteuerung in [!DNL Experience Platform] finden Sie im [Benutzerhandbuch für die Zugriffssteuerung](./ui/overview.md).

Alle Aufrufe von [!DNL Experience Platform]-APIs werden auf Berechtigungen überprüft und geben Fehler zurück, wenn die entsprechenden Berechtigungen im aktuellen Benutzerkontext nicht gefunden wurden. In der Benutzeroberfläche werden Elemente je nach den dem aktuellen Benutzer zugewiesenen Berechtigungen ausgeblendet oder geändert.

## Adobe Admin Console

Die Adobe Admin Console bietet einen zentralen Speicherort für die Verwaltung der Adobe-Produktberechtigungen und den Zugriff für Ihr Unternehmen. Über die Konsole können Sie Benutzergruppen Zugriffsberechtigungen für verschiedene [!DNL Platform]-Funktionen erteilen, wie z. B. [!UICONTROL Datensätze verwalten], [!UICONTROL Datensätze anzeigen] oder [!UICONTROL Profile verwalten].

### Produktprofile

In [!DNL Admin Console] werden Benutzern anhand der Verwendung von Produktprofilen Berechtigungen zugewiesen. Mit den Produktprofilen können Sie einem oder mehreren Benutzern Berechtigungen erteilen und auch deren Zugriff auf den Umfang der Sandboxes einschließen, die ihnen über Produktprofile zugewiesen werden. Benutzer können einem oder mehreren Produktprofilen Ihres Unternehmens zugewiesen werden.

### Standard-Produktprofile

[!DNL Experience Platform] verfügt über zwei vorkonfigurierte standardmäßige Produktprofile. Die folgende Tabelle zeigt, was in den einzelnen Standardprofilen bereitgestellt wird, einschließlich der Sandbox, auf die sie Zugriff gewähren, sowie der Berechtigungen, die sie im Rahmen dieser Sandbox gewähren.

| Produktprofile | Sandbox-Zugriff | Berechtigungen |
| --- | --- | --- |
| Standardproduktion – Zugriff auf alles | Produktion | Alle für [!DNL Experience Platform] geltenden Berechtigungen mit Ausnahme der Sandbox-Administrationsberechtigungen. |
| Sandbox-Administratoren | K. A. | Bietet nur Zugriff auf Sandbox-Administratorberechtigungen. |

## Sandboxes und Berechtigungen

Nicht-Produktion-Sandboxes sind eine Form der Datenvirtualisierung, mit der Sie Daten von anderen Sandboxes isolieren können und die üblicherweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. Die Berechtigungen eines Produktprofils geben den Benutzern des Profils Zugriff auf [!DNL Platform]-Funktionen innerhalb der Sandbox-Umgebungen, auf die ihnen Zugriff gewährt wurde. Mit einer Standardlizenz für Experience Platform erhalten Sie fünf Sandboxes (eine zur Produktion und vier zur Nicht-Produktion). Sie können Pakete von jeweils zehn Nicht-Produktions-Sandboxes bis zu insgesamt maximal 75 Sandboxes hinzufügen. Für weitere Informationen wenden Sie sich an Ihren IMS-Organisationsadministrator oder Ihren Adobe-Vertriebsmitarbeiter.

Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md).

### Zugriff auf Sandboxes

Der Zugriff auf Sandboxes wird über Produktprofile verwaltet. Ausführliche Anweisungen zum Aktivieren des Zugriffs auf eine Sandbox für ein Produktprofil finden Sie im [Benutzerhandbuch für die Zugangssteuerung](./ui/overview.md).

Benutzern kann Zugriff auf eine oder mehrere Sandboxes innerhalb eines Profils gewährt werden. Wenn ein Benutzer in zwei oder mehr Produktprofilen enthalten ist, hat er Zugriff auf alle in diesen Profilen enthaltenen Sandboxes.

Die Berechtigung „Sandbox-Verwaltung“ ermöglicht Benutzern das Verwalten, Anzeigen oder Zurücksetzen von Sandboxes.

### Berechtigungen {#permissions}

Auf der Registerkarte Berechtigungen in einem Produktprofil werden die Sandboxes und Berechtigungen angezeigt, die für dieses Profil aktiv sind:

![permissions-overview](./images/permissions.png)

Berechtigungen, die über die [!DNL Admin Console] gewährt werden, werden nach Kategorie sortiert. Einige dieser Berechtigungen gewähren Zugriff auf verschiedene Funktionen auf niedriger Ebene.

In der folgenden Tabelle sind die für [!DNL Experience Platform] in der [!DNL Admin Console] verfügbaren Berechtigungen mit Beschreibungen der spezifischen [!DNL Platform]-Funktionen aufgeführt, auf die sie Zugriff gewähren. Detaillierte Anweisungen zum Hinzufügen von Berechtigungen zu einem Produktprofil finden Sie im [Benutzerhandbuch für die Zugangssteuerung](./ui/overview.md).

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
| [!DNL Destinations] | [!UICONTROL Verwalten von Zielen] | Zugriff auf das Lesen, Erstellen und Löschen von Zielaktivierungsflüssen und Zielkonten. |
| [!DNL Destinations] | [!UICONTROL Anzeigen von Zielen] | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Ziele auf der Registerkarte **[!UICONTROL Durchsuchen]**. |
| [!DNL Destinations] | [!UICONTROL Aktivieren von Zielen] | Ermöglicht Benutzern das Aktivieren von Segmenten für vorhandene Ziele. Aktiviert den Zuordnungsschritt im Aktivierungs-Workflow. Diese Berechtigung erfordert entweder [!UICONTROL Ziele anzeigen] oder [!UICONTROL Ziele verwalten] wird dem Benutzer gewährt, der Daten für Ziele aktiviert. |
| [!DNL Destinations] | [!UICONTROL Segment ohne Zuordnung aktivieren] | Ermöglicht Benutzern das Aktivieren von Segmenten für vorhandene Ziele, ohne die [Zuordnungsschritt](../destinations/ui/activate-batch-profile-destinations.md#mapping). Benutzer können in Aktivierungs-Workflows Segmente hinzufügen und entfernen, jedoch keine zugeordneten Attribute oder Identitäten hinzufügen oder entfernen. Diese Berechtigung erfordert die [!UICONTROL Ziele aktivieren] -Berechtigung für den Benutzer, der Daten für Ziele aktiviert. |
| [!DNL Destinations] | [!UICONTROL Verwalten und Aktivieren von Datensatzzielen] | Fähigkeit zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Datensatzexport-Flüssen. Außerdem die Fähigkeit zum Aktivieren von Daten an aktiven Zielen, die erstellt wurden. |
| [!DNL Destinations] | [!UICONTROL Ziel-Authoring] | Möglichkeit, Ziele mithilfe des [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md) zu erstellen. |
| [!DNL Data Ingestion] | [!UICONTROL Verwalten von Quellen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| [!DNL Data Ingestion] | [!UICONTROL Anzeigen von Quellen] | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Quellen auf der Registerkarte **[!UICONTROL Durchsuchen]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Zugriff auf das Erstellen, Akzeptieren und Ablehnen von Partner-Handshakes, um zwei IMS-Organisationen miteinander zu verbinden und [!DNL Segment Match]-Flüsse zu aktivieren. |
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

Durch das Lesen dieses Handbuchs haben Sie sich mit den Hauptgrundsätzen der Zugangssteuerung in [!DNL Experience Platform] vertraut gemacht. Nun können Sie im [Benutzerhandbuch für die Zugangssteuerung](./ui/overview.md) ausführliche Schritte nachlesen, wie Sie die [!DNL Admin Console] zur Erstellung von Produktprofilen und zur Erteilung von Berechtigungen für [!DNL Platform] nutzen.
