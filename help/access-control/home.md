---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;Adobe Admin Console
solution: Experience Platform
title: Zugangssteuerung – Übersicht
description: Die Zugangssteuerung für Adobe Experience Platform wird über Adobe Admin Console geboten. Diese Funktion nutzt Produktprofile in Admin Console, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '3279'
ht-degree: 30%

---

# Zugangssteuerung – Übersicht

Die Zugriffssteuerung für Adobe Experience Platform wird über die **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/) bereitgestellt. Diese Funktion nutzt Produktprofile und Richtlinien, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen.

## Zugangssteuerung zu Hierarchie und Workflow

Zum Konfigurieren der Zugriffssteuerung für Experience Platform müssen Sie system- oder produkbezogene Administratorrechte für ein Unternehmen besitzen, das über ein Experience Platform-Produkt verfügt. Zum Erteilen oder Entziehen von Berechtigungen ist mindestens eine Produktadmin-Rolle erforderlich. Zu einer anderen Administratorrolle, die Berechtigungen verwalten können, gehören die Systemadmins (keine Einschränkungen). Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

>[!NOTE]
>
>Von hier an beziehen sich alle Erwähnungen von Administrierenden in diesem Dokument auf Produktadmins oder höhere Rollen (wie oben beschrieben).

Ein Workflow auf hoher Ebene zum Abrufen und Zuweisen von Zugriffsberechtigungen kann wie folgt zusammengefasst werden:

- Nach der Lizenzierung von Adobe Experience Platform oder einem Programm-Service, der Experience Platform verwendet, wird eine E-Mail an den Administrator gesendet, der während der Lizenzierung angegeben wurde.
- Administrierende melden sich bei der [Adobe Admin Console](#adobe-admin-console) an und wählen **Adobe Experience Platform** aus der Liste der Produkte auf der Übersichtsseite aus.
- Um Zugriff auf Experience Platform zu gewähren, wird empfohlen, dass der Administrator Benutzer zum Standardproduktprofil hinzufügt: `AEP-Default-All-Users`.
- Über Experience Platform-Berechtigungen können Administrierende neue Rollen erstellen oder die Berechtigungen und Benutzenden für vorhandene Rollen bearbeiten.
- Beim Erstellen oder Bearbeiten einer Rolle fügt der Administrator der Rolle über die Registerkarte &quot;**[!UICONTROL users]**&quot; Benutzer hinzu und gewährt diesen Benutzern Berechtigungen (z. B. &quot;[!UICONTROL Read Datasets]&quot; oder &quot;[!UICONTROL Manage Schemas]„), indem er die Berechtigungen der Rolle bearbeitet. Ebenso können Administrierende mithilfe derselben Bearbeitungsoption Zugriff auf Sandboxes zuweisen.
- Wenn sich Benutzende bei der Benutzeroberfläche von Experience Platform anmelden, wird ihr Zugriff auf Experience Platform-Funktionen durch die Berechtigungen gesteuert, die ihnen im vorherigen Schritt erteilt wurden. Wenn ein Benutzer beispielsweise nicht über die Berechtigung [!UICONTROL View Datasets] verfügt, ist die Registerkarte **[!UICONTROL Datasets]** im Seitenmenü für diesen Benutzer nicht sichtbar.

Detailliertere Anweisungen zum Verwalten der Zugriffskontrolle in Experience Platform finden Sie im [Benutzerhandbuch für die Zugriffskontrolle](./ui/overview.md).

Alle Aufrufe von Experience Platform-APIs werden auf Berechtigungen überprüft und geben Fehler zurück, wenn die entsprechenden Berechtigungen im aktuellen Benutzerkontext nicht gefunden wurden. In der Benutzeroberfläche werden Elemente je nach den dem aktuellen Benutzer zugewiesenen Berechtigungen ausgeblendet oder geändert.

## Berechtigungen {#platform-permissions}

[!UICONTROL Permissions] bietet einen zentralen Speicherort für die Verwaltung des Experience Platform-Zugriffs für Ihr Unternehmen. Über [!UICONTROL Permissions] können Sie Benutzergruppen Zugriffsberechtigungen für verschiedene Experience Platform-Funktionen erteilen, z. B. [!UICONTROL Manage Datasets], [!UICONTROL View Datasets] oder [!UICONTROL Manage Profiles].

### Rollen

Im Abschnitt [!UICONTROL Roles] werden Benutzern mithilfe von Rollen Berechtigungen zugewiesen. Mithilfe von Rollen können Sie einer Benutzerin oder einem Benutzer bzw. mehreren Benutzenden Berechtigungen erteilen und zudem deren Zugriff auf die Sandboxes beschränken, die ihnen über Rollen zugewiesen sind. Benutzende können einer oder mehreren Rollen Ihres Unternehmens zugewiesen werden.

### Standardrollen

Experience Platform verfügt über zwei vorkonfigurierte Standardrollen. Die folgende Tabelle zeigt, was in den einzelnen Standardprofilen bereitgestellt wird, einschließlich der Sandbox, auf die sie Zugriff gewähren, sowie der Berechtigungen, die sie im Rahmen dieser Sandbox gewähren.

| Rolle | Sandbox-Zugriff | Berechtigungen |
| --- | --- | --- |
| Standardproduktion – Zugriff auf alles | prod | Alle für Experience Platform geltenden Berechtigungen mit Ausnahme der Sandbox-Administratorberechtigungen. |
| Sandbox-Administratoren | K. A. | Ermöglicht den Zugriff auf die Sandbox `Prod` und auf Sandbox-Administrationsberechtigungen. |

## Sandboxes und Berechtigungen

Nicht-Produktion-Sandboxes sind eine Form der Datenvirtualisierung, mit der Sie Daten von anderen Sandboxes isolieren können und die üblicherweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. Die Berechtigungen einer Rolle geben den Benutzenden der Rolle Zugriff auf Experience Platform-Funktionen innerhalb der Sandbox-Umgebungen, auf die ihnen Zugriff gewährt wurde. Mit einer Standardlizenz für Experience Platform erhalten Sie fünf Sandboxes (eine zur Produktion und vier zur Nicht-Produktion). Sie können Pakete von jeweils zehn Nicht-Produktions-Sandboxes bis zu insgesamt maximal 75 Sandboxes hinzufügen. Wenden Sie sich an die Admins Ihrer Organisation oder das Adobe-Vertriebspersonal, um weitere Informationen zu erhalten.

Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md).

### Zugriff auf Sandboxes

Der Zugriff auf Sandboxes wird über Rollen verwaltet. Ausführliche Anweisungen zum Aktivieren des Zugriffs auf eine Sandbox für eine Rolle finden Sie unter [„Rollen“ im Handbuch zur attributbasierten Zugriffssteuerung](./abac/ui/roles.md).

Benutzenden kann Zugriff auf eine oder mehrere Sandboxes innerhalb einer Rolle gewährt werden. Wenn eine Benutzerin oder ein Benutzer in zwei oder mehr Rollen enthalten ist, hat diese Person Zugriff auf alle in diesen Rollen enthaltenen Sandboxes.

Die Berechtigung „Sandbox-Verwaltung“ ermöglicht Benutzenden das Verwalten, Anzeigen oder Zurücksetzen von Sandboxes.

### Ressourcenberechtigungen {#permissions}

Ressourcenberechtigungen gewähren Zugriff auf bestimmte Experience Platform-Funktionen. Ressourcen sind in Kategorien unterteilt, die einen Satz relevanter Berechtigungen enthalten, die Rollen einzeln zugewiesen werden können.

[!UICONTROL Permissions] zeigt der Arbeitsbereich Ressourcen einer Rolle die Sandboxes und Berechtigungen an, die für diese Rolle aktiv sind:

![Ressourcenarbeitsbereich einer Rolle mit einer Liste ausgewählter Kategorien und Berechtigungen.](./images/permissions.png)

In der folgenden Tabelle sind die verfügbaren Ressourcenkategorien für Experience Platform und Programme aufgeführt, die über Berechtigungen verwaltet werden:

| Kategorie | Beschreibung |
| --- | --- |
| [!DNL Adobe Mix Modeler] | Konfigurieren, Verwalten und Anzeigen von Berechtigungen für [!DNL Adobe Mix Modeler]. |
| [!DNL AI Assistant] | Konfigurieren Sie Berechtigungen für [!DNL AI Assistant]. |
| [!DNL Alerts] | Konfigurieren, Verwalten, Auflösen und Anzeigen von Berechtigungen für Warnhinweise und den Warnhinweisverlauf. |
| [!DNL B2B Account Lists] | Konfigurieren, Verwalten, Anzeigen und Veröffentlichen von Berechtigungen für B2B-Kontolisten, einschließlich Aktionen wie Hinzufügen, Entfernen, Importieren und Löschen von Konten aus Kontolisten. |
| [!DNL B2B Admin Configurations] | Konfigurieren und verwalten Sie Berechtigungen für B2B-Admin-Konfigurationen, einschließlich Digital-Asset-Management-Verbindungen, Asset-Repositorys und Ereignissen. |
| [!DNL B2B Assets] | Konfigurieren und verwalten Sie Berechtigungen für B2B-Assets, einschließlich E-Mails, SMS, Landingpages, Fragmente, Vorlagen und Bildern. |
| [!DNL B2B Buying Groups] | Konfigurieren und verwalten Sie Berechtigungen für B2B-Einkaufsgruppen, einschließlich Funktionen wie Lösungsinteressen, Rollenvorlagen und Kaufgruppenstatus. |
| [!DNL B2B Channel Configurations] | Konfigurieren und verwalten Sie Berechtigungen für B2B-Kanal-Konfigurationen, einschließlich Einstellungen wie Kommunikationsbeschränkungen, API-Anmeldeinformationen und Sicherheitseinstellungen. |
| [!DNL B2B Dashboards] | Konfigurieren Sie Ansichtsberechtigungen für B2B-Dashboards, einschließlich Funktionen wie Kontointeraktion, Kaufgruppenphasen, steigende Anzahl von Konten und Kontaktabdeckung. |
| [!DNL B2B Journeys] | Konfigurieren und verwalten Sie Berechtigungen zum Anzeigen und Veröffentlichen für B2B-Journey, einschließlich Funktionen wie Konto- und Personenaktionen, Ereignis-Listener und Aufspaltungspfade. |
| [!DNL Campaigns] | Konfigurieren, Verwalten, Veröffentlichen und Anzeigen von Berechtigungen für Kampagnen in Journey Optimizer. |
| [!DNL Channel Configurations] | Konfigurieren, Verwalten und Exportieren von Kanalkonfigurationsfunktionen wie Subdomains, IP-Pools, Nachrichtenvoreinstellungen, PTR-Einträge, Unterdrückungslisten, Landingpage-Einstellungen, SMS-Einstellungen und Datei-Routing. |
| [!DNL Collaborations] | Konfigurieren und Verwalten von Berechtigungen für Funktionen von Real-time Customer Data Profile Collaboration. |
| [!DNL Computed Attributes] | Konfigurieren und verwalten Sie Berechtigungen zum Entwerfen oder Veröffentlichen berechneter Attribute. |
| [!DNL Customer Managed Keys] | Konfigurieren und Verwalten von Berechtigungen für kundenverwaltete Schlüssel. |
| [!DNL Dashboards] | Konfigurieren und Verwalten von Berechtigungen für standardmäßige, benutzerdefinierte und lizenzierte Dashboards. |
| [!DNL Data Collection] | Konfigurieren und Verwalten von Berechtigungen für Datenströme. |
| [!DNL Data Governance] | Konfigurieren, Verwalten, Anwenden und Anzeigen von Berechtigungen für Data-Governance-Funktionen wie Beschriftungen, Richtlinien und Aktivitätsprotokolle. |
| [!DNL Data Ingestion] | Konfigurieren und Verwalten von Berechtigungen für Datenaufnahmefunktionen wie Quellen und Zielgruppenfreigabe. |
| [!DNL Data Lifecycle] | Konfigurieren und Verwalten von Berechtigungen für Datenhygiene-Funktionen. |
| [!DNL Data Management] | Konfigurieren und verwalten Sie Berechtigungen für Datenverwaltungsfunktionen wie Datensätze und überwachen Sie Datensätze und Streams. |
| [!DNL Data Modeling] | Konfigurieren und verwalten Sie Berechtigungen für Datenmodellierungsfunktionen wie Schemata, Beziehungen und Identitätsmetadaten. |
| [!DNL Data Science Workspace] | Konfigurieren und Verwalten von Berechtigungen zum [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | Konfigurieren und verwalten Sie Berechtigungen für Entscheidungen, Angebote und Ranking-Strategie-Funktionen im Entscheidungs-Management. |
| [!DNL Destinations] | Konfigurieren und verwalten Sie Berechtigungen für Ziele, einschließlich Funktionen wie Aktivierung und Authoring mit Destinations SDK. |
| [!DNL Federated Data] | Konfigurieren und Verwalten von Berechtigungen für Federated Data-Funktionen. |
| [!DNL Identity Management] | Konfigurieren und verwalten Sie Berechtigungen für Identity Service-Funktionen wie Identity-Namespaces und das Identitätsdiagramm. |
| [!DNL Intelligent Service] | Konfigurieren und verwalten Sie Berechtigungen für Attributions-KI und Kunden-KI in Intelligent Service. |
| [!DNL IP Warmup Configurations] | Konfigurieren und verwalten Sie Berechtigungen für IP-Aufwärmpläne und zeigen Sie Berechtigungen zum Anzeigen von IP-Aufwärmberichten an. |
| [!DNL Journey Optimizer Library] | Konfigurieren und Verwalten von Berechtigungen für Bibliothekselemente in Adobe Journey Optimizer. |
| [!DNL Journey Optimizer Rules] | Konfigurieren und Verwalten von Berechtigungen für Häufigkeitsregeln in Adobe Journey Optimizer. |
| [!DNL Journeys] | Konfigurieren Sie Berechtigungen zum Verwalten, Veröffentlichen und Anzeigen für Journey, einschließlich Funktionen wie Journey-Berichte, Ereignisse, Datenquellen und Aktionen. |
| [!DNL Messages] | Konfigurieren Sie Berechtigungen zum Verwalten, Veröffentlichen und Anzeigen von Nachrichten, einschließlich Funktionen wie Nachrichtenvorschau und Tests. |
| [!DNL Privacy Service] | Konfigurieren und Verwalten von Berechtigungen für Privacy Service-Funktionen. |
| [!DNL Profile Management] | Konfigurieren Sie Berechtigungen zum Verwalten, Anzeigen, Exportieren und Auswerten für Profil-Service-Funktionen wie Zielgruppen, Profile und Zusammenführungsrichtlinien. |
| [!DNL Prospects] | Konfigurieren und verwalten Sie Berechtigungen für Interessenten, Schemata, Profile und Audiences, einschließlich Funktionen wie der Anzeige des Akkordeons „Interessent“. |
| [!DNL Query Service] | Konfigurieren und verwalten Sie Berechtigungen für Abfrage-Service-Funktionen wie nicht ablaufende Anmeldedaten und strukturierte SQL-Abfragen. |
| [!DNL Reports] | Konfigurieren Sie Ansichtsberechtigungen für Kanalberichte. |
| [!DNL Run and Operate] | Konfigurieren Sie Anzeigeberechtigungen für die Funktionen „Ausführen“ und „Betrieb“, z. B. Konsistenzprüfungen und Auftragsplanungen. |
| [!DNL Sandbox Administration] | Konfigurieren, Verwalten, Anzeigen und Zurücksetzen von Berechtigungen beim Verwalten von Sandboxes. |
| [!DNL Traits Configuration] | Konfigurieren und verwalten Sie Eigenschaften über die Benutzeroberfläche für berechnete Attribute. |
| [!DNL Translation Services] | Konfigurieren und verwalten Sie Berechtigungen für Übersetzungs-Services für Projekte, Aufgaben, Überprüfungen, interne Tests, Einstellungen und Anbieter. |

In der folgenden Tabelle stehen die verfügbaren Berechtigungen für Experience Platform in der Rolle, einschließlich Beschreibungen der spezifischen Experience Platform-Funktionen, auf die sie Zugriff gewähren. Ausführliche Anweisungen zum Hinzufügen von Berechtigungen zu einer Rolle finden Sie unter [„Rollen“ im Handbuch zur attributbasierten Zugangssteuerung](./abac/ui/roles.md).

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Harmonized Data] | Die Möglichkeit, harmonisierte Daten anzuzeigen und zu ändern. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Harmonized Data] | Schreibgeschützter Zugriff auf harmonisierte Daten. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Configurations] | Die Möglichkeit, Modellkonfigurationen anzuzeigen und zu ändern. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Configurations] | Schreibgeschützter Zugriff auf Modellkonfigurationen. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Plans Configurations] | Die Möglichkeit, Pläne und Konfigurationen anzuzeigen und zu ändern. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Plans Configurations] | Schreibgeschützter Zugriff auf Plankonfigurationen. |
| [!DNL AI Assistant] | [!UICONTROL Enable AI Assistant] | Möglichkeit, die [!DNL [AI assistant]](../ai-assistant/access.md) Fragen zu stellen. |
| [!DNL AI Assistant] | [!UICONTROL View Operational Insights] | Zugriff auf den Abruf von Antworten [ Abfragen ](../ai-assistant/home.md##operational-insights)operative Insights). |
| [!DNL AI Assistant] | [!UICONTROL Generate Content] | Benutzern ermöglichen, Inhalte mithilfe der [!DNL AI Assistant] zu generieren. |
| [!DNL AI Assistant] | [!UICONTROL Manage Brand Kit] | Ermöglichen Sie Benutzern, Markenrichtlinien mithilfe der [!DNL AI Assistant] zu erstellen. |
| [!DNL Alerts] | [!UICONTROL View Alerts History] | Schreibgeschützter Zugriff auf den Warnhinweisverlauf. |
| [!DNL Alerts] | [!UICONTROL Resolve Alerts] | Zugriff zum Lesen, Bearbeiten und Löschen von Warnhinweisen. |
| [!DNL Alerts] | [!UICONTROL View Alerts] | Schreibgeschützter Zugriff auf Warnhinweise |
| [!DNL Alerts] | [!UICONTROL Manage Alerts] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Warnhinweisen. |
| [!DNL B2B Account Lists] | [!UICONTROL Manage B2B Account Lists] | Möglichkeit, **[!UICONTROL Account Lists]** im linken Navigationsbereich anzuzeigen und darauf zuzugreifen. Benutzer mit Zugriff auf **[!UICONTROL Account Lists]** sollten Zugriff auf alle CRUD-Funktionen von Kontolisten haben: `/accounts-list`. |
| [!DNL B2B Admin Configurations] | [!UICONTROL Manage B2B Admin Configurations] | Möglichkeit, **[!UICONTROL B2B Admin Configurations]** im linken Navigationsbereich anzuzeigen und darauf zuzugreifen. Benutzer mit Zugriff auf **[!UICONTROL B2B Admin Configurations]** sollten Zugriff auf alle SMS-API-Anmeldeinformationen für CRUD-Funktionen haben: `/admin-configs`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Assets] | Möglichkeit, **[!UICONTROL Assets]** im linken Navigationsbereich anzuzeigen und darauf zuzugreifen. Benutzende mit Zugriff auf **[!UICONTROL Assets]** sollten Zugriff auf alle Assets CRUD-Funktionen haben: `/assets-listing`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Templates] | Möglichkeit, **[!UICONTROL Templates]** im linken Navigationsbereich anzuzeigen und darauf zuzugreifen. Benutzer mit Zugriff auf **[!UICONTROL Templates]** sollten Zugriff auf alle CRUD-Vorlagenfunktionen haben: `/b2b-content-templates`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Fragments] | Möglichkeit, **[!UICONTROL Fragments]** im linken Navigationsbereich anzuzeigen und darauf zuzugreifen. Benutzende mit Zugriff auf **[!UICONTROL Fragments]** sollten Zugriff auf alle CRUD-Funktionen für Fragmente haben: `/fragments`. |
| [!DNL B2B Buying Groups] | [!UICONTROL Manage B2B Buying Groups] | Möglichkeit, **[!UICONTROL Buying Groups]** im linken Navigationsbereich anzuzeigen und darauf zuzugreifen. Benutzer mit Zugriff auf **[!UICONTROL Buying Groups]** sollten Zugriff auf alle CRUD-Funktionen für Einkaufsgruppen haben: `/buying-groups`. |
| [!DNL B2B Dashboards] | [!UICONTROL Manage B2B Engagement Dashboards] | Möglichkeit, **[!UICONTROL Dashboard]** im linken Navigationsbereich anzuzeigen und darauf zuzugreifen. Benutzer mit Zugriff auf **[!UICONTROL Dashboards]** sollten Zugriff auf alle CRUD-Funktionen von Dashboards haben: `/insights-dashboard`. |
| [!DNL B2B Channel Configurations] | [!UICONTROL Manage B2B Channels Configurations] | Möglichkeit, **[!UICONTROL Channels]** im linken Navigationsbereich anzuzeigen und darauf zuzugreifen. Benutzende mit Zugriff auf **[!UICONTROL Channels]** sollten Zugriff auf alle Channel CRUD-Funktionen haben: `/channels-config`. |
| [!DNL B2B Journeys] | [!UICONTROL Manage B2B Account Journeys] | Möglichkeit, **[!UICONTROL Account Journeys]** im linken Navigationsbereich anzuzeigen und darauf zuzugreifen. Benutzende mit Zugriff auf **[!UICONTROL Account Journeys]** sollten Zugriff auf alle CRUD-Funktionen der Konto-Journey haben: `/account-journeys`. |
| [!DNL Campaigns] | [!UICONTROL Manage Campaigns] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Kampagnen. |
| [!DNL Campaigns] | [!UICONTROL Approve and Publish Campaigns] | Die Möglichkeit, Kampagnen zu genehmigen und zu veröffentlichen. |
| [!DNL Campaigns] | [!UICONTROL Publish Campaigns] | Möglichkeit zur Veröffentlichung von Kampagnen. |
| [!DNL Campaigns] | [!UICONTROL View Campaigns] | Schreibgeschützter Zugriff auf Kampagnen. |
| [!DNL Campaigns] | [!UICONTROL View Campaigns Report] | Schreibgeschützter Zugriff auf Kampagnenberichte. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages General Settings] | Schreibgeschützter Zugriff auf allgemeine Einstellungen für Nachrichten. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Subdomains Delegations] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Subdomain-Zuweisungen. |
| [!DNL Channel Configurations] | [!UICONTROL Manage IP Pools] | Zugriff auf das Lesen, Erstellen und Bearbeiten von IP-Pools. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages General Settings] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen allgemeiner Einstellungen für Nachrichten. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages Presets] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Nachrichtenvoreinstellungen. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages Presets] | Schreibgeschützter Zugriff auf Nachrichtenvoreinstellungen. |
| [!DNL Channel Configurations] | [!UICONTROL Manage PTR Records] | Zugriff auf das Lesen und Bearbeiten von PTR-Einträgen. |
| [!DNL Channel Configurations] | [!UICONTROL View PTR Records] | Schreibgeschützter Zugriff auf PTR-Einträge. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Suppression] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Unterdrückungsregeln. |
| [!DNL Channel Configurations] | [!UICONTROL View Suppression List] | Schreibgeschützter Zugriff auf die Unterdrückungsliste. |
| [!DNL Channel Configurations] | [!UICONTROL Export Suppression List] | Zugriff zum Exportieren der Unterdrückungsliste als CSV-Datei. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Landing Page Settings] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen der Einstellungen für Landingpages. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Settings] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen der SMS-Einstellungen. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Subdomains] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von SMS-Subdomains. |
| [!DNL Channel Configurations] | [!UICONTROL Manage File Routing] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Datei-Routing. |
| [!DNL Channel Configurations] | [!UICONTROL View File Routing] | Schreibgeschützter Zugriff auf Datei-Routing. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Seedlist] | Die Möglichkeit, die Seed-Liste zu erstellen und zu bearbeiten. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Language Settings] | Möglichkeit zum Erstellen und Bearbeiten der Spracheinstellungen. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Web Subdomains] | Die Möglichkeit, CJM-Web-Subdomains zu erstellen und zu bearbeiten. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Push Credentials] | Die Möglichkeit zum Erstellen, Bearbeiten und Löschen von Push-Anmeldeinformationen. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Instances] | Anzeigen, Erstellen, Aktualisieren und Löschen der Collaboration-Instanzen einer Organisation. Entdecken Sie die Instanzen für die Zusammenarbeit anderer Organisationen. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Instances] | Lesen Sie die Instanzen für die Zusammenarbeit einer Organisation und entdecken Sie die Instanzen für die Zusammenarbeit anderer Organisationen. |
| [!DNL Collaborations] | [!UICONTROL Manage Connection Invites] | Von Ihrem Unternehmen initiierte Verbindungseinladungen anzeigen, erstellen und löschen. Akzeptieren und Ablehnen von Verbindungseinladungen, die von anderen Organisationen initiiert wurden |
| [!DNL Collaborations] | [!UICONTROL Read Connection Invites] | Schreibgeschützter Zugriff auf Einladungen zur Verbindung. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Connections] | Ein Advertiser kann Einstellungen anzeigen, erstellen und aktualisieren sowie Verbindungen senden und löschen. Ein Publisher kann Verbindungen anzeigen, akzeptieren oder ablehnen. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Connections] | Schreibgeschützter Zugriff auf Verbindungen. |
| [!DNL Collaborations] | [!UICONTROL Manage Audience Data] | Onboarden und Entdecken von Zielgruppen. Aktualisieren Sie öffentliche, private und benutzerdefinierte Zielgruppen und verwalten Sie die Metadateneinstellungen des Zielgruppeninventars. |
| [!DNL Collaborations] | [!UICONTROL Read Audience Data] | Lesen und Entdecken von Zielgruppen. |
| [!DNL Collaborations] | [!UICONTROL Manage Measurement Data] | Messdaten integrieren, aktualisieren und löschen. |
| [!DNL Collaborations] | [!UICONTROL Read Measurement Data] | Schreibgeschützter Zugriff auf Messdaten. |
| [!DNL Collaborations] | [!UICONTROL Manage Projects] | Anzeigen, Erstellen, Aktualisieren und Löschen von Projekten für alle Discover-, Share-, Activate- und Measurement-Aktivitäten. |
| [!DNL Collaborations] | [!UICONTROL Read Projects] | Zeigen Sie Projekte für beliebige Aktivitäten zum Entdecken, Freigeben, Aktivieren und Messen an. |
| [!DNL Collaborations] | [!UICONTROL Read User Activities] | Schreibgeschützter Zugriff auf Benutzeraktivitäten. |
| [!DNL Collaborations] | [!UICONTROL Export User Activities] | Exportieren Sie Benutzeraktivitäten. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Credit Monitoring] | Kreditüberwachung auf Organisations- und Instanzebene. |
| [!DNL Computed Attributes] | [!UICONTROL View Computed attributes] | Schreibgeschützter Zugriff für die Registerkarte „Berechnete Attribute“, den Bestand und Details. |
| [!DNL Computed Attributes] | [!UICONTROL Manage Computed attributes] | Zugriff auf das Lesen, Erstellen, Löschen von Entwürfen und Deaktivieren berechneter Attribute. |
| [!DNL Customer Managed Keys] | [!UICONTROL Manage Customer Managed Keys] | Zugriff zum Anzeigen und Konfigurieren kundenverwalteter Schlüssel. |
| [!DNL Dashboards] | [!UICONTROL View License Usage Dashboard] | Schreibgeschützter Zugriff zum Anzeigen des Dashboards zur Lizenznutzung. |
| [!DNL Dashboards] | [!UICONTROL Manage Standard Dashboards] | Fügen Sie benutzerdefinierte Attribute hinzu, die sich noch nicht im Data Warehouse befinden. |
| [!DNL Dashboards] | [!UICONTROL View Standard Dashboards] | Schreibgeschützter Zugriff auf die Dashboards Profile, Ziele und Segmente . Ermöglicht auch den Zugriff auf Dashboards im linken Navigationsbereich und auf der Registerkarte Dashboards - Inventar und Integrationen . |
| [!DNL Dashboards] | [!UICONTROL Manage Custom Dashboards] | Zugriff zum Erstellen oder Bearbeiten eines Dashboards. |
| [!DNL Dashboards] | [!UICONTROL View Custom Dashboards] | Schreibgeschützter Zugriff auf benutzerdefinierte Dashboards. |
| [!DNL Dashboards] | [!UICONTROL Manage Report Schedules] | Möglichkeit zum Erstellen von Zeitplänen. |
| [!DNL Dashboards] | [!UICONTROL Export Dashboard Data] | Steuert die Fähigkeit eines Benutzers, tabellarische Daten aus Dashboards im Abfragemodus zu exportieren. |
| [!DNL Data Collection] | [!UICONTROL Manage Datastreams] | Zugriff auf das Lesen, Erstellen und Bearbeiten von Datenströmen. |
| [!DNL Data Collection] | [!UICONTROL View Datastreams] | Schreibgeschützter Zugriff auf Datenströme. |
| [!DNL Data Governance] | [!UICONTROL Manage Usage Labels] | Zugriff zum Lesen, Erstellen und Löschen von Datennutzungs-Labels. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datennutzungsrichtlinien. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Schreibgeschützter Zugriff auf Datennutzungsrichtlinien Ihres Unternehmens. |
| [!DNL Data Governance] | [!UICONTROL View User Activity Log] | Schreibgeschützter Zugriff zur Anzeige aufgezeichneter [Auditprotokolle](../landing/governance-privacy-security/audit-logs/overview.md) von Experience Platform-Aktivitäten. |
| [!DNL Data Governance] | [!UICONTROL View Privacy Console] | Schreibgeschützter Zugriff auf Datenschutzkonsolen. |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte **[!UICONTROL Catalog]** und authentifizierte Quellen auf der Registerkarte **[!UICONTROL Browse]** . |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Zugriff zum Erstellen, Akzeptieren und Ablehnen der Partnerfreigabe, um zwei Organisationen miteinander zu verbinden und [!DNL Segment Match] zu aktivieren. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Veröffentlichen von [!DNL Segment Match]-Feeds mit aktiven Partnern. |
| [!DNL Data Lifecycle] | [!UICONTROL View Data Lifecycle] | Schreibgeschützter Zugriff für den Datenlebenszyklus. |
| [!DNL Data Lifecycle] | [!UICONTROL Manage Data Lifecycle] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen des Datenlebenszyklus. |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Schemata und zugehörigen Ressourcen. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Schreibgeschützter Zugriff auf Schemata und zugehörige Ressourcen. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Schema-Beziehungen. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identitätsmetadaten für Schemata. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen. Schreibgeschützter Zugriff auf Schemata. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Schreibgeschützter Zugriff auf Datensätze und Schemata. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Schreibgeschützter Zugriff auf das Monitoring von Datensätzen und Streams. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen in [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | [!UICONTROL Manage Experience Decisioning] | Möglichkeit zum Verwalten von Experience Decisioning-Entitäten. |
| [!DNL Decision Management] | [!UICONTROL View Experience Decisioning] | Schreibgeschützter Zugriff auf Experience Decisioning-Entitäten. |
| [!DNL Decision Management] | [!UICONTROL Manage Decisions] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Entscheidungsentitäten. |
| [!DNL Decisions Management] | [!UICONTROL View Decisions] | Schreibgeschützter Zugriff auf Entscheidungsentitäten. |
| [!DNL Decision Management] | [!UICONTROL Manage Offers] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen aller Angebote und Komponenten. Schreibgeschützter Zugriff auf Entscheidungen und Sammlungen. |
| [!DNL Decsion Management] | [!UICONTROL Manage Ranking Strategies] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen benutzerdefinierter Berichte und auf die Verwendung von Aktionsfunktionen. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Schreibgeschützter Zugriff zum Anzeigen verfügbarer Ziele auf der Registerkarte **[!UICONTROL Catalog]** und authentifizierter Ziele auf der Registerkarte **[!UICONTROL Browse]** . |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Zugriff auf das Lesen, Erstellen und Löschen von Zielverbindungen und Zielkonten. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Fähigkeit zur Aktivierung von Daten an aktiven Zielen, die erstellt wurden. Für diese Berechtigung ist es außerdem erforderlich, dass Benutzenden, die Ziele aktivieren, entweder [!UICONTROL View Destinations] oder [!UICONTROL Manage Destinations] gewährt wird. |
| [!DNL Destinations] | [!UICONTROL Activate Segment without Mapping] | Die Möglichkeit, Zielgruppen für vorhandene Ziele zu aktivieren, ohne den [Zuordnungsschritt“ ](../destinations/ui/activate-batch-profile-destinations.md#mapping). Benutzende können Zielgruppen in Aktivierungs-Workflows hinzufügen und entfernen, jedoch keine zugeordneten Attribute oder Identitäten hinzufügen oder entfernen. Diese Berechtigung erfordert auch, dass Benutzenden, die Daten für Ziele aktivieren, die [!UICONTROL View Destinations] Berechtigung erteilt wird. |
| [!DNL Destinations] | [!UICONTROL Manage and Activate Dataset Destinations] | Fähigkeit zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Datensatzexport-Flüssen. Außerdem die Möglichkeit, Daten für aktive Datensätze zu aktivieren, die erstellt wurden. Diese Berechtigung erfordert auch, dass Benutzenden, die Daten für Ziele aktivieren, die [!UICONTROL View Destinations] Berechtigung erteilt wird. |
| [!DNL Destinations] | [!UICONTROL Destination Authoring] | Möglichkeit, Ziele mithilfe des [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md) zu erstellen. |
| [!DNL Federated Data] | [!UICONTROL Manage Federated Data] | Die Möglichkeit, auf alle Federated Data-Funktionen zuzugreifen, z. B. das Erstellen von Schemas, Modellen und Kompositionen. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identity-Namespaces. |
| [!DNL Identity Management] | [!UICONTROL View Identity Namespaces] | Schreibgeschützter Zugriff für Identity-Namespaces. |
| [!DNL Identity Management] | [!UICONTROL View Identity Graph] | Schreibgeschützter Zugriff für Identitätsdiagramme. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Settings] | Zugriff auf das Lesen, Erstellen und Bearbeiten von Identitätseinstellungen. |
| [!DNL Identity Management] | [!UICONTROL View Identity Settings] | Schreibgeschützter Zugriff auf Identitätseinstellungen. |
| [!DNL Intelligent Services] | [!UICONTROL View Attribution AI] | Schreibgeschützter Zugriff für Attributions-KI-Einstellungen und -Einblicke. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Attribution AI] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Attribution AI-Modellen. |
| [!DNL Intelligent Services] | [!UICONTROL View Customer AI] | Zugriff auf das Lesen oder Anzeigen von Kunden-KI-Modellen. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Customer AI] | Zugriff zum Erstellen, Aktualisieren, Löschen, Aktivieren oder Deaktivieren von Kunden-KI-Modellen. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Plans] | Schreibgeschützter Zugriff auf IP-Aufwärmpläne. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Manage IP Warmup Plans] | Die Möglichkeit, IP-Aufwärmpläne zu verwalten. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Reports] | Schreibgeschützter Zugriff auf IP-Aufwärmberichte. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Journey. |
| [!DNL Journeys] | [!UICONTROL View Journeys] | Schreibgeschützter Zugriff auf Journey. |
| [!DNL Journeys] | [!UICONTROL View Journeys Report] | Schreibgeschützter Zugriff auf den Bericht &quot;Journey&quot;. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys Events, Data Sources and Actions] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Ereignissen, Datenquellen oder Aktionen. |
| [!DNL Journeys] | [!UICONTROL View Journeys Events, Data Sources and Actions] | Schreibgeschützter Zugriff auf Ereignisse, Datenquellen oder Aktionen. |
| [!DNL Journeys] | [!UICONTROL Approve and Publish Journeys] | Möglichkeit, Journey beim Anwenden einer Richtlinie zu genehmigen und zu veröffentlichen. |
| [!DNL Journeys] | [!UICONTROL Publish Journeys] | Möglichkeit, Journey zu veröffentlichen. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Manage Library Items] | Die Möglichkeit, gespeicherte Ausdrücke hinzuzufügen und zu löschen. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Publish Fragments] | Die Möglichkeit, Inhaltsfragmente zu veröffentlichen. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Simulate Content] | Zugriff auf die Option „Inhalt simulieren“ für Vorschau und Proofing. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL View Frequency Rules] | Schreibgeschützter Zugriff auf Häufigkeitsregeln. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Manage Frequency Rules] | Zugriff auf das Lesen, Erstellen, Bearbeiten oder Löschen von Häufigkeitsregeln. |
| [!DNL Messages] | [!UICONTROL Manage Messages] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Nachrichten. |
| [!DNL Messages] | [!UICONTROL View Messages] | Schreibgeschützter Zugriff auf Nachrichten. |
| [!DNL Messages] | [!UICONTROL View Messages Report] | Zugriff auf das Lesen und Bearbeiten von Nachrichtenberichten. |
| [!DNL Messages] | [!UICONTROL Publish Messages] | Möglichkeit zum Veröffentlichen von Nachrichten. |
| [!DNL Messages] | [!UICONTROL Manage Messages Preview and Test] | Möglichkeit, bei Anwendung einer Richtlinie Nachrichten zu genehmigen und zu veröffentlichen. |
| [!DNL Privacy Service] | [!UICONTROL Manage Privacy Service] | Zugriff auf das Lesen und Schreiben von Datenschutz-Workflows. |
| [!DNL Privacy Service] | [!UICONTROL View Privacy Service] | Schreibgeschützter Zugriff auf Datenschutz-Workflows. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen, die für Kundenprofile verwendet werden. Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Zielgruppen. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Schreibgeschützter Zugriff auf verfügbare Zielgruppen. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Zusammenführungsrichtlinien. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Schreibgeschützter Zugriff auf verfügbare Zusammenführungsrichtlinien. |
| [!DNL Profile Management] | [!UICONTROL Import Audiences] | Möglichkeit, den CSV-Upload-Workflow zum Importieren neuer Zielgruppen zu verwenden. |
| [!DNL Profile Management] | [!UICONTROL Export Audience Segment] | Möglichkeit, eine ausgewertete Zielgruppe in einen Datensatz zu exportieren. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | Möglichkeit zum Generieren von Profilen für eine Zielgruppe durch Auswertung einer Segmentdefinition. |
| [!DNL Profile Management] | [!UICONTROL View B2B AI] | Schreibgeschützter Zugriff auf Einstellungen und Konfigurationen für alle B2B-KI-/ML-Services. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B AI] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Einstellungen und Konfigurationen für alle B2B-KI-/ML-Services. |
| [!DNL Profile Management] | [!UICONTROL View B2B Profile] | Schreibgeschützter Zugriff auf B2B-Entitätsprofile (z. B. Konto, Opportunity usw.), Einstellungen und Konfigurationen für alle B2B-KI-/ML-Services und B2B-Dashboard-Widgets. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B Profile] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von B2B-Entitätsprofilen (z. B. Konto, Opportunity usw.). Schreibgeschützter Zugriff für Einstellungen und Konfigurationen für alle B2B-KI-/ML-Services und B2B-Dashboard-Widgets. |
| [!DNL Profile Management] | [!UICONTROL Manage Lookalikes] | Möglichkeit zum Erstellen oder Löschen von Lookalike-Zielgruppen. |
| [!DNL Profile Management] | [!UICONTROL View B2B Experience] | Möglichkeit, B2B-Profile und -Attribute anzuzeigen. |
| [!DNL Profile Management] | [!UICONTROL View Profile Settings] | Schreibgeschützter Zugriff auf alle Profileinstellungen. |
| [!DNL Profile Management] | [!UICONTROL Manage Profile Settings] | Zugriff auf das Lesen und Bearbeiten aller Profileinstellungen. |
| [!DNL Prospects] | [!UICONTROL View Prospects] | Schreibgeschützter Zugriff auf Schemas, Profile, Zielgruppen und das Akkordeon potenzieller Kunden. |
| [!DNL Prospects] | [!UICONTROL Manage Prospects] | Möglichkeit zum Erstellen und Verwalten von Interessentenschemata, Profilen und Audiences. Schreibgeschützter Zugriff auf das Akkordeon des potenziellen Kunden. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen strukturierter SQL-Abfragen für Experience Platform-Daten. |
| [!DNL Query Service] | [!UICONTROL Manage Query Service Integration] | Zugriff auf das Erstellen, Aktualisieren und Löschen nicht ablaufender Anmeldedaten für den Zugriff auf den Abfrage-Service. |
| [!DNL Query Service] | [!UICONTROL Manage Query Sessions] | Möglichkeit, vorhandene Sitzungen zu entfernen. |
| [!DNL Query Service] | [!UICONTROL Manage Allow List] | Möglichkeit, IP-Einschränkungen für Ihre Organisation zu verwalten. |
| [!DNL Reports] | [!UICONTROL View Channel Reports] | Die Möglichkeit, Kanalberichte anzuzeigen und zu ändern. |
| [!DNL Run and Operate] | [!UICONTROL View Health Checks] | Schreibgeschützter Zugriff auf Konsistenzprüfungen. |
| [!DNL Run and Operate] | [!UICONTROL View Job Schedules] | Schreibgeschützter Zugriff auf Auftragspläne. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Sandboxes. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Schreibgeschützter Zugriff für Sandboxes Ihrer Organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Fähigkeit, eine Sandbox zurückzusetzen. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Packages] | Zugriff zum Erstellen, Importieren oder Exportieren von Paketen. |
| [!DNL Sandbox Administration] | [!UICONTROL Share Packages] | Zugriff auf die Freigabe von Paketen über verschiedene Organisationen hinweg. |
| [!DNL Traits Configurations] | [!UICONTROL View Traits] | Schreibgeschützter Zugriff für Eigenschaften. |
| [!DNL Traits Configurations] | [!UICONTROL Manage Traits] | Zugriff zum Verwalten von Eigenschaften. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Projects] | Die Möglichkeit, Übersetzungsprojekte zu verwalten. |
| [!DNL Translation Service] | [!UICONTROL View Translation Projects] | Schreibgeschützter Zugriff auf Übersetzungsprojekte. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Tasks] | Die Möglichkeit, Übersetzungsaufgaben zu verwalten. |
| [!DNL Translation Service] | [!UICONTROL View Translation Tasks] | Schreibgeschützter Zugriff auf Übersetzungsaufgaben. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Reviews] | Die Möglichkeit, Übersetzungsüberprüfungen zu verwalten. |
| [!DNL Translation Service] | [!UICONTROL View Translation Reviews] | Schreibgeschützter Zugriff auf Übersetzungsüberprüfungen. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation In-house] | Die Möglichkeit, Übersetzungen intern zu verwalten. |
| [!DNL Translation Service] | [!UICONTROL View Translation In-house] | Schreibgeschützter Zugriff auf interne Übersetzungen. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Settings] | Die Möglichkeit für Administratoren, Übersetzungseinstellungen zu verwalten. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Providers] | Die Möglichkeit, Übersetzungsdienstleister zu verwalten. |

## Nächste Schritte

Durch Lesen dieses Handbuchs wurden Sie mit den Hauptgrundsätzen der Zugriffskontrolle in Experience Platform vertraut gemacht. Sie können jetzt mit dem [Benutzerhandbuch zur attributbasierten Zugriffssteuerung](./abac/overview.md) fortfahren. Darin finden Sie ausführliche Anweisungen dazu, wie Sie mit Experience Cloud Rollen erstellen und Berechtigungen für Experience Platform zuweisen können.
