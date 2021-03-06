---
title: Data Governance in Query Service
description: Dieser Überblick behandelt die wichtigsten Elemente der Data Governance in Experience Platform Query Service.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: c1ec6f949bd0ab9ec3b1ccc58baf74d8c71deca0
workflow-type: tm+mt
source-wordcount: '2667'
ht-degree: 2%

---

# Data Governance in Query Service

Adobe Experience Platform führt Daten aus verschiedenen Unternehmenssystemen zusammen und ermöglicht es Ihnen, die Daten über Query Service entsprechend Ihren Anforderungen zu bereinigen, zu gestalten, zu bearbeiten und anzureichern. So können Marketing-Experten Kunden besser identifizieren, verstehen und ansprechen. Die Gewährleistung einer angemessenen Data Governance ist ein wichtiger Aspekt der Verarbeitung personenbezogener Daten, da bestimmte Daten Nutzungsbeschränkungen unterliegen können, die auf organisatorischen Richtlinien und gesetzlichen Vorschriften beruhen. Es ist wichtig sicherzustellen, dass Ihre erfassten Daten und die zugehörigen Vorgänge mit den definierten Datennutzungsrichtlinien konform sind.

Mit Data Governance in Query Service können Sie Kundendaten verwalten und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datennutzung sicherstellen. Dies spielt eine wichtige Rolle, wenn sichergestellt werden soll, dass die Nutzungsrichtlinien gemäß den von Ihrem Unternehmen festgelegten Vorschriften angewendet wurden.

Unternehmen, die routinemäßig Datenverarbeitung durchführen, sollten diese Richtlinien umreißen, praktizieren und durchsetzen, um eine datenschutzbewusste Umgebung für alle Benutzer zu schaffen.

Die folgenden Kategorien sind bei der Verwendung von Query Service für die Einhaltung von Vorschriften zur Datenkonformität von entscheidender Bedeutung:

1. Sicherheit
1. Verfolgung
1. Datennutzung
1. Datenschutz   
<!-- 1. Data hygiene -->

In diesem Dokument werden die verschiedenen Governance-Bereiche untersucht und aufgezeigt, wie die Einhaltung von Datenanforderungen bei der Verwendung von Query Service erleichtert werden kann. Siehe [Governance, Datenschutz und Sicherheitsübersicht](../../landing/governance-privacy-security/overview.md) für umfassendere Informationen darüber, wie Sie mit Experience Platform Kundendaten verwalten und Compliance sicherstellen können.

## Sicherheit

Die Datensicherheit ist der Prozess des Schutzes von Daten vor unbefugtem Zugriff und der Sicherstellung eines sicheren Zugriffs während des gesamten Lebenszyklus. Der sichere Zugriff wird in der Experience Platform durch die Anwendung von Rollen und Berechtigungen durch Funktionen wie rollenbasierte Zugriffssteuerung und attributbasierte Zugriffssteuerung aufrechterhalten. Berechtigungen, SSL und Datenverschlüsselung werden ebenfalls verwendet, um den Datenschutz in der gesamten Plattform sicherzustellen.

Die Sicherheit in Bezug auf Query Service ist in folgende Kategorien unterteilt:

* [Zugriffskontrolle](#access-control): Der Zugriff wird über Rollen und Berechtigungen gesteuert, einschließlich Berechtigungen auf Datensatz- und Spaltenebene.
* Sichern von Daten durch [Konnektivität](#connectivity): Die Daten werden über Platform und externe Clients gesichert, indem eine begrenzte Verbindung mit ablaufenden oder nicht ablaufenden Anmeldedaten hergestellt wird.
* Sichern von Daten durch [Verschlüsselung und Schlüssel auf Systemebene](#encryption): Die Datensicherheit wird durch Verschlüsselung sichergestellt, wenn die Daten im Ruhezustand sind.

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### Zugangssteuerung {#access-control}

Die Zugriffskontrolle in Adobe Experience Platform ermöglicht die Verwendung von [Adobe Admin Console](https://adminconsole.adobe.com/) , um den Zugriff auf Query Service-Funktionen mithilfe rollenbasierter Berechtigungen zu verwalten. Auf ähnliche Weise können Sie den Zugriff auf bestimmte Datenattribute durch die Beschriftungsverwaltung in Schemata und Datenfeldern steuern.

In diesem Abschnitt werden die erforderlichen Zugriffssteuerungsberechtigungen beschrieben, über die ein Benutzer verfügen muss, um die Funktionen von Query Service vollständig nutzen zu können. Weitere Informationen finden Sie in den Dokumenten unter [Berechtigungen verwalten](../../access-control/ui/permissions.md) und [Benutzer verwalten](../../access-control/ui/users.md) für detaillierte Anweisungen zur Zuweisung des Zugriffs auf ein Produktprofil.

#### Relevante Berechtigungen

Die entsprechenden Zugriffssteuerungsberechtigungen werden in den Tabellen unten entsprechend ihrem Umfang definiert.

**Ausführungsberechtigungen von Abfragen**

Zum Ausführen von Abfragen in Query Service muss einem Benutzer eine Rolle mit der folgenden Berechtigung zugewiesen werden:

| Berechtigung | Beschreibung |
|---|---|
| [!UICONTROL Verwalten von Abfragen] | Mit dieser Berechtigung können Benutzer Datenexploration und Batch-Abfragen ausführen, die entweder einen vorhandenen Datensatz lesen oder Daten in Datensätze schreiben können. Dies umfasst beide `CREATE TABLE AS SELECT` (`CTAS`) und `INSERT INTO AS SELECT` (`ITAS`). |

**Datensatzberechtigungen**

Dieser Abschnitt dient als Leitfaden für den ressourcenbasierten Zugriff, der für den Zugriff auf Datensätze beim Abfragen von Daten über Query Service erforderlich ist.

Über die Benutzeroberfläche &quot;Berechtigungen&quot;können Sie eine ressourcenbasierte Zugriffskontrolle für einen Datensatz und ein Schema mit den folgenden Berechtigungen definieren:

| Berechtigung | Beschreibung |
|---|---|
| [!UICONTROL Datensätze verwalten] | Diese Berechtigung bietet schreibgeschützten Zugriff für Schemas und ermöglicht den Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen zur Verwendung mit Query Service. |
| [!UICONTROL Anzeigen von Datensätzen] | Diese Berechtigung ermöglicht schreibgeschützten Zugriff für Datensätze und Schemas zur Verwendung mit Query Service. |

#### Zugriffskontrolle für Spalten/Felder

Die attributbasierte Zugriffssteuerungsfunktion ermöglicht es Query Service-Benutzern, den Zugriff auf wichtige Benutzerdaten zu beschränken. Der Zugriff kann je nach den einer Rolle zugewiesenen Berechtigungen gewährt oder eingeschränkt werden. Der Benutzerzugriff auf einzelne Spalten wird durch die entsprechenden Datennutzungsbezeichnungen und die Berechtigungssätze gesteuert, die auf die den Benutzern zugewiesenen Rollen angewendet werden.

Beim Tagging von Schemafeldgruppen und -klassen mit Datennutzungsbezeichnungen werden Datennutzungsbeschränkungen auf alle Schemas mit denselben Feldgruppen und -klassen angewendet. Siehe Übersicht unter [attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md) für umfassende Informationen zu dieser Funktion.

Mit dieser Funktion können Sie den von Ihnen ausgewählten Benutzergruppen Zugriffsrechte auf vertrauliche Spalten gewähren. Die Zugriffskontrolle auf eine Spalte kann die Lese- und Schreibfunktionen für einen bestimmten Benutzertyp einschränken.

Die Zugriffskontrolle für Spalten kann auf Schemaebene sowohl für Standard- als auch für Ad-hoc-Schemata angewendet werden. Wenden Sie Datennutzungsbezeichnungen auf XDM-Schemas an, um den Zugriff auf eine oder mehrere Spalten zu beschränken. Die Datenbeschriftung wird konsistent angewendet, auch für Datensätze, die über Query Service mithilfe eines vordefinierten Schemas oder eines Ad-hoc-Schemas erstellt werden, das im Rahmen des CTAS-Vorgangs generiert wurde.

Sobald die entsprechende Zugriffsebene mithilfe von Beschriftungen und Rollen angewendet wurde, tritt das folgende Systemverhalten auf, wenn ein Benutzer versucht, auf die nicht zugänglichen Daten zuzugreifen:

1. Wenn einem Benutzer der Zugriff auf eine der Spalten in einem Schema verweigert wurde, wird dem Benutzer auch die Berechtigung zum Lesen oder Schreiben in der eingeschränkten Spalte verweigert. Dies gilt für die folgenden gängigen Szenarien:

   * **1. Fall**: Wenn ein Benutzer versucht, eine Abfrage auszuführen, die nur eine eingeschränkte Spalte betrifft, gibt das System einen Fehler aus, dass die Spalte nicht vorhanden ist.
   * **2. Fall**: Wenn ein Benutzer versucht, eine Abfrage mit mehreren Spalten einschließlich einer eingeschränkten Spalte auszuführen, gibt das System nur die Ausgabe für alle nicht eingeschränkten Spalten zurück.

1. Wenn ein Benutzer versucht, auf ein berechnetes Feld zuzugreifen, muss der Benutzer Zugriff auf alle in der Komposition verwendeten Felder haben, oder das System verweigert auch den Zugriff auf das berechnete Feld.

#### Zugriffskontrollen für Ansichten

Query Service bietet die Möglichkeit, standardmäßige ANSI-SQL für [`CREATE VIEW`](../sql/syntax.md#create-view) -Anweisungen. Bei hochsensiblen Daten-Workflows müssen Sie beim Erstellen von Ansichten entsprechende Steuerelemente durchsetzen.

Die `CREATE VIEW` -Keyword definiert eine Ansicht einer Abfrage, aber die Ansicht ist nicht physisch materialisiert. Stattdessen wird die Abfrage jedes Mal ausgeführt, wenn in einer Abfrage auf die Ansicht verwiesen wird. Wenn ein Benutzer eine Ansicht aus einem Datensatz erstellt, sind die rollenbasierten und attributbasierten Zugriffssteuerungsregeln für den übergeordneten Datensatz **not** hierarchisch angewendet. Daher müssen Sie bei der Erstellung einer Ansicht explizit Berechtigungen für jede der Spalten festlegen.

### Konnektivität {#connectivity}

Der Zugriff auf Query Service erfolgt über die Platform-Benutzeroberfläche oder durch Herstellung einer Verbindung mit externen kompatiblen Clients. Der Zugriff auf alle verfügbaren Fronten wird durch eine Reihe von Anmeldedaten gesteuert.

#### Konnektivität über externe Clients

Für den Zugriff auf Query Service mithilfe eines Drittanbieter-Clients sind Anmeldeinformationen zur Autorisierung erforderlich. Diese Anmeldeinformationen sind für den Zugriff auf Query Service mit einem der kompatiblen externen Clients erforderlich. Sie können eine Verbindung zu externen Clients herstellen, indem Sie entweder [ablaufende Anmeldeinformationen](#expiring-credentials) oder [Nicht ablaufende Anmeldeinformationen](#non-expiring-credentials).

#### Eingeschränkte Verbindungszeit durch ablaufende Anmeldedaten {#expiring-credentials}

[Ablaufberechtigungen](../ui/credentials.md) Benutzern die Möglichkeit geben, eine temporäre Verbindung mit einem externen Client herzustellen. Dieser Satz von Anmeldedaten ist nur 24 Stunden gültig. Der Ablauf dieser Anmeldeinformationen wird zusammen mit der Registerkarte &quot;Anmeldedaten&quot;im Dashboard von Query Service angezeigt.

![Die Registerkarte &quot;Anmeldeinformationen&quot;im Query Service-Arbeitsbereich mit auslaufenden Anmeldeinformationen wird hervorgehoben.](../images/data-governance/overview/expiring-credentials.png)

#### Nicht ablaufende Anmeldeinformationen {#non-expiring-credentials}

[Nicht ablaufende Anmeldeinformationen](../ui/credentials.md#non-expiring-credentials) ermöglichen es Ihnen, eine permanente Verbindung mit einem externen Client herzustellen, wodurch die Verbindung mit Query Service erleichtert wird, ohne dass ein manuelles Kennwort erforderlich ist.

Um die Option zum Generieren nicht ablaufender Anmeldedaten zu aktivieren, müssen Sie die folgenden Schritte ausführen: [erforderlicher Workflow](../ui/credentials.md#prerequisites). Im Rahmen dieses Prozesses muss Ihr Organisationsadministrator Berechtigungen für das Produktprofil konfigurieren, damit der Administrator steuern kann, welche Konten Zugriff auf nicht ablaufende Anmeldeinformationen haben.

Technische Benutzerkonten mit nicht ablaufenden Berechtigungen können Rollen zugewiesen werden, um eine angemessene Data Governance sicherzustellen, indem der Umfang ihres Lese- und Schreibzugriffs auf der Grundlage ihrer Zuständigkeiten und Bedürfnisse definiert wird. Siehe vorherigen Abschnitt unter [Verwenden rollenbasierter Berechtigungen über die Zugriffssteuerung](#access-control) , um den Zugriff auf Query Service zu verwalten.

Nach Abschluss des erforderlichen Workflows können autorisierte Benutzer jetzt [die erforderlichen Verbindungsanmeldeinformationen generieren](../ui/credentials.md#generate-credentials).

#### SSL-Datenverschlüsselung

Für mehr Sicherheit bietet Query Service native Unterstützung für SSL-Verbindungen zum Verschlüsseln der Client-/Server-Kommunikation. Platform unterstützt verschiedene SSL-Optionen, um Ihren Datensicherheitsanforderungen gerecht zu werden und den Verarbeitungsaufwand für Verschlüsselung und Schlüsselaustausch auszugleichen.

Siehe Handbuch zu [SSL-Optionen für Client-Verbindungen von Drittanbietern mit Query Service](../clients/ssl-modes.md) für weitere Informationen, einschließlich der Verbindung mit dem `verify-full` SSL-Parameterwert.

### Encryption-Dienst {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

Verschlüsselung ist die Verwendung eines algorithmischen Prozesses, um Daten in kodierten und unlesbaren Text umzuwandeln, um sicherzustellen, dass die Informationen geschützt sind und ohne Entschlüsselungsschlüssel nicht zugänglich sind.

Die Datenkonformität von Query Service stellt sicher, dass Daten immer verschlüsselt werden. Daten-in-Transit sind immer HTTPS-konform und Daten im Ruhezustand werden in einem Azure Data Lake-Speicher mit Schlüsseln auf Systemebene verschlüsselt. Weitere Informationen finden Sie in der Dokumentation unter [Verschlüsseln von Daten in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html) für weitere Informationen. Weitere Informationen dazu, wie ruhende Daten in Azure Data Lake Storage verschlüsselt werden, finden Sie in der [offizielle Azure-Dokumentation](https://docs.microsoft.com/de-de/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## Verfolgung {#audit}

Query Service zeichnet die Benutzeraktivität auf und kategorisiert diese Aktivität in verschiedene Protokolltypen. Logs liefern Informationen zu **who** ausgeführt **what** Aktion und **when**. Jede in einem Protokoll aufgezeichnete Aktion enthält Metadaten, die den Aktionstyp, das Datum und die Uhrzeit, die E-Mail-ID des Benutzers, der die Aktion ausgeführt hat, und zusätzliche Attribute für den Aktionstyp angeben.

Eine beliebige Protokollkategorie kann von einem Platform-Benutzer angefordert werden. In diesem Abschnitt finden Sie Details zum Typ der für Query Service erfassten Informationen und wo auf diese Informationen zugegriffen werden kann.

### Abfrageprotokolle {#query-logs}

Über die Benutzeroberfläche der Abfrageprotokolle können Sie Ausführungsdetails für alle Abfragen überwachen und überprüfen, die entweder über den Abfrage-Editor oder die Query Service-API ausgeführt wurden. Dadurch erhalten Sie Transparenz bei Query Service-Aktivitäten, sodass Sie die Metadaten überprüfen können auf **all** die Abfragen, die in Query Service ausgeführt wurden. Sie enthält alle Arten von Abfragen, unabhängig davon, ob es sich um eine explorative, Batch- oder geplante Abfrage handelt.

Der Zugriff auf Abfrageprotokolle erfolgt über die Platform-Benutzeroberfläche im [!UICONTROL Protokolle] des [!UICONTROL Abfragen] Arbeitsbereich.

![Die Registerkarte &quot;Abfrage&quot;, auf der das Detailbedienfeld hervorgehoben ist.](../images/data-governance/overview/queries-log.png)

### Auditprotokolle {#audit-logs}

Audit-Protokolle enthalten detailliertere Informationen als Abfragelogs und ermöglichen es Ihnen, Protokolle nach Attributen wie Benutzer, Datum, Typ der Abfrage usw. zu filtern. Über die Details hinaus, die in der Benutzeroberfläche des Abfrageprotokolls verfügbar sind, speichert Auditprotokolle Details zu einzelnen Benutzern zusammen mit ihren Sitzungsdaten oder der Verbindung zu einem Drittanbieter-Client.

Durch die Bereitstellung eines exakten Datensatzes über Benutzeraktionen kann ein Audit-Protokoll bei der Fehlerbehebung helfen und Ihrem Unternehmen helfen, die Richtlinien zur Unternehmensdatenverwaltung und die gesetzlichen Anforderungen effektiv zu erfüllen. Auditprotokolle enthalten einen Datensatz aller Platform-Aktivitäten. Mithilfe von Auditprotokollen können Sie Benutzeraktionen im Zusammenhang mit der Ausführung von Abfragen, Vorlagen und geplanten Abfragen überprüfen, um die Transparenz und Sichtbarkeit von Aktionen zu erhöhen, die von Benutzern in Query Service ausgeführt werden.

In der folgenden Tabelle sind die von Prüfprotokollen erfassten Abfragekategorien und die von ihnen aufgezeichneten Aktionstypen aufgeführt:

| Kategorie | Aktionstyp |
|---|---|
| Abfrage | Execute |
| Abfragevorlage | Erstellen, Löschen, Aktualisieren |
| Geplante Abfrage | Erstellen, Löschen, Aktualisieren |

Nachfolgend finden Sie eine Liste mit drei erweiterten Serverprotokollen, die mehr Details enthalten als in den Abfrageprotokollen enthalten sind. Die erweiterten Protokolle befinden sich in den Abfragekategorien der Auditprotokolle:

1. **Meta-Abfrageprotokolle**: Wenn eine Abfrage ausgeführt wird, werden verschiedene zugehörige Backend-Unterabfragen (z. B. Parsing) ausgeführt. Diese Arten von Abfragen werden als &quot;Metadaten&quot;-Abfragen bezeichnet. Die entsprechenden Details finden Sie in den Prüfprotokollen.
1. **Sitzungsprotokolle**: Das System erstellt ein Sitzungseintragsprotokoll für einen Benutzer, wenn er sich bei Query Service anmeldet, unabhängig davon, ob er eine Abfrage ausführt.
1. **Clientverbindungsprotokolle von Drittanbietern**: Ein Konnektivitäts-Auditprotokoll wird generiert, wenn ein Benutzer Query Service erfolgreich mit einem Drittanbieter-Client verbindet.

Siehe [Übersicht über Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md) Weitere Informationen dazu, wie Prüfprotokolle bei der Einhaltung von Datenanforderungen durch Ihr Unternehmen helfen können.

## Datennutzung {#data-usage}

Das Data Governance-Framework in Platform bietet eine einheitliche Methode zur verantwortungsvollen Verwendung von Daten für alle Adobe-Lösungen, -Dienste und -Plattformen. Es koordiniert den systemischen Ansatz zur Erfassung, Kommunikation und Verwendung von Metadaten in der gesamten Adobe Experience Cloud. Dies wiederum hilft den Datenverantwortlichen bei der Beschriftung von Daten entsprechend den erforderlichen Marketing-Aktionen und den Einschränkungen, die diesen Daten aus diesen beabsichtigten Marketing-Aktionen auferlegt werden. Siehe Übersicht unter [Datennutzungsbezeichnungen](../../data-governance/labels/overview.md) Weitere Informationen dazu, wie Sie mit Data Governance Datennutzungsbezeichnungen auf Datensätze und Felder anwenden können.

Es ist Best Practice, in jeder Phase der Journey auf die Datenkonformität hinzuarbeiten. Zu diesem Zweck sollten abgeleitete Datensätze, die Ad-hoc-Schemas verwenden, als Teil des Data Governance-Frameworks angemessen gekennzeichnet werden. Es gibt zwei Arten von abgeleiteten Datensätzen, die von Query Service gebildet werden: Datensätze, die ein Standardschema verwenden, und Datensätze, die ein Ad-hoc-Schema verwenden.

>[!NOTE]
>
>Datensätze, die mit Query Service erstellt werden, werden als &quot;abgeleitete Datensätze&quot;bezeichnet.

Da Ad-hoc-Schemata von einem einzelnen Benutzer für einen bestimmten Zweck erstellt werden, sind die XDM-Schemafelder für diesen bestimmten Datensatz benannt und nicht für die Verwendung in verschiedenen Datensätzen vorgesehen. Daher sind Ad-hoc-Schemata nicht standardmäßig in der Experience Platform-Benutzeroberfläche sichtbar. Obwohl es keinen Unterschied bei der Anwendung von Datennutzungsbezeichnungen zwischen Standard- und Ad-hoc-Schemata gibt, müssen von Query Service zum Zweck der Beschriftung erstellte Ad-hoc-Schemata zunächst in der Platform-Benutzeroberfläche sichtbar gemacht werden. Siehe Handbuch unter [Ermitteln von Ad-hoc-Schemata in der Platform-Benutzeroberfläche](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) für weitere Details.

Nachdem Sie auf das Schema zugegriffen haben, können Sie [Beschriftungen auf einzelne Felder anwenden](../../xdm/tutorials/labels.md). Sobald ein Schema beschriftet wurde, übernehmen alle von diesem Schema abgeleiteten Datensätze diese Beschriftungen. Von hier aus können Sie Datennutzungsrichtlinien einrichten, die die Aktivierung bestimmter Bezeichnungen auf bestimmte Ziele beschränken können. Weitere Informationen finden Sie in der Übersicht unter [Datennutzungsrichtlinien](../../data-governance/policies/overview.md).

## Datenschutz    {#privacy}

[Privacy Service](../../privacy-service/home.md) hilft Ihnen bei der Verwaltung von Kundenanfragen beim Zugriff auf und beim Löschen ihrer Daten gemäß den gesetzlichen Datenschutzbestimmungen. Dazu durchsucht sie die Daten nach bereits vorhandenen Identifikatoren und greift je nach angefordertem Datenschutzauftrag auf diese Daten zu oder löscht sie. Die Daten müssen ordnungsgemäß gekennzeichnet werden, damit der Service feststellen kann, welche Felder während der Datenschutzaufträge aufgerufen oder gelöscht werden sollen. Daten, die Datenschutzanfragen unterliegen, müssen Kundenidentitätsinformationen enthalten, um die unterschiedlichen Daten mit der Person zu verknüpfen, für die die Datenschutzanfrage gilt. Query Service kann die von ihm verwendeten Daten mit einer eindeutigen Kennung anreichern, um Datenschutzaufträge zu erfüllen.

Datenschutzanfragen können an den Data Lake oder den Profildatenspeicher gesendet werden. Aus dem Data Lake gelöschte Datensätze führen nicht zum Löschen von Profilen, die aus diesen Datensätzen stammen. Außerdem löscht ein Datenschutzauftrag zum Löschen personenbezogener Daten aus dem Data Lake ihr Profil nicht, sodass alle nach Abschluss des Datenschutzauftrags erfassten Informationen (die diese Profil-ID enthalten) dieses Profil normal aktualisieren. Dies bestätigt die Notwendigkeit, die in den Einzelschemata verwendeten Daten ordnungsgemäß zu ermitteln.

Weitere Informationen finden Sie in der Dokumentation zum Privacy Service . [Identitätsdaten für Datenschutzanfragen](../../privacy-service/identity-data.md) und wie Sie Ihre Datenvorgänge konfigurieren und Adobe-Technologien nutzen können, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.

Funktionen von Query Service für Data Governance vereinfachen und optimieren die Datenkategorisierung und Einhaltung von Datennutzungsregeln. Sobald die Daten identifiziert wurden, können Sie mit Query Service die primäre Identität für alle Ausgabedatensätze zuweisen. You **must** Fügen Sie dem Datensatz Identitäten hinzu, um Datenschutzanfragen zu erleichtern und die Einhaltung von Datenanforderungen zu erreichen.

Schemadatenfelder können über die Platform-Benutzeroberfläche als Identitätsfeld festgelegt werden. Query Service ermöglicht Ihnen außerdem, [Kennzeichnen der primären Identitäten mithilfe des SQL-Befehls &quot;ALTER TABLE&quot;](../sql/syntax.md#alter-table). Festlegen einer Identität mithilfe der `ALTER TABLE` -Befehl ist insbesondere dann nützlich, wenn Datensätze mit SQL erstellt werden, anstatt über die Platform-Benutzeroberfläche direkt aus einem Schema zu gelangen. Anweisungen dazu finden Sie in der Dokumentation . [Identitätsfelder in der Benutzeroberfläche definieren](../../xdm/ui/fields/identity.md) bei der Verwendung von Standardschemata.

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
