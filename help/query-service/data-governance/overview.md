---
title: Data Governance in Query Service
description: In dieser Übersicht werden die wichtigsten Elemente der Data Governance in Experience Platform Query Service behandelt.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3142'
ht-degree: 1%

---

# Data Governance in Query Service

Adobe Experience Platform führt Daten aus verschiedenen Unternehmenssystemen zusammen und ermöglicht es Ihnen, die Daten über den Abfrage-Service Ihren Anforderungen entsprechend zu bereinigen, zu gestalten, zu bearbeiten und anzureichern. Dadurch können Marketing-Fachleute Kundinnen und Kunden besser identifizieren, verstehen und ansprechen. Die Sicherstellung einer angemessenen Data Governance ist ein wichtiger Aspekt beim Umgang mit personenbezogenen Daten, da bestimmte Daten Nutzungsbeschränkungen unterliegen können, die auf organisatorischen Richtlinien und gesetzlichen Vorschriften basieren. Es ist wichtig sicherzustellen, dass Ihre aufgenommenen Daten und die zugehörigen Vorgänge mit den definierten Datennutzungsrichtlinien konform sind.

Mit Data Governance in Query Service können Sie Kundendaten verwalten und bei der Datennutzung die Einhaltung von relevanten Vorschriften, Einschränkungen und Richtlinien sicherstellen. Dies spielt eine wichtige Rolle, wenn sichergestellt werden soll, dass die Nutzungsrichtlinien gemäß den von Ihrem Unternehmen festgelegten Vorschriften angewendet wurden.

Unternehmen, die routinemäßig Datenverarbeitung durchführen, werden empfohlen, diese Richtlinien zu skizzieren, zu praktizieren und durchzusetzen, um eine datenschutzbewusste Umgebung für alle Benutzer zu schaffen.

Die folgenden Kategorien sind bei der Einhaltung von Datenkonformitätsvorschriften bei der Verwendung von Query Service von entscheidender Bedeutung:

1. Sicherheit
1. Verfolgung
1. Datennutzung
1. Datenschutz   
1. Datenhygiene

In diesem Dokument werden die verschiedenen Governance-Bereiche untersucht und gezeigt, wie die Einhaltung der Datenrichtlinien bei der Verwendung von Abfrage-Service erleichtert werden kann. In der [Governance, Datenschutz und Sicherheit - Übersicht](../../landing/governance-privacy-security/overview.md) finden Sie weitere Informationen darüber, wie Sie mit Experience Platform Kundendaten verwalten und die Einhaltung von Vorschriften sicherstellen können.

## Sicherheit {#security}

Datensicherheit ist der Prozess des Schutzes von Daten vor unbefugtem Zugriff und der Gewährleistung eines sicheren Zugriffs während ihres gesamten Lebenszyklus. Der sichere Zugriff in Experience Platform wird durch die Anwendung von Rollen und Berechtigungen durch Funktionen wie rollenbasierte Zugriffssteuerung und attributbasierte Zugriffssteuerung gewährleistet. Anmeldeinformationen, SSL und Datenverschlüsselung werden ebenfalls verwendet, um den Datenschutz in Experience Platform sicherzustellen.

Die Sicherheit in Bezug auf den Abfrage-Service ist in die folgenden Kategorien unterteilt:

* [Zugriffssteuerung](#access-control): Der Zugriff wird über Rollen und Berechtigungen gesteuert, einschließlich Berechtigungen auf Datensatz- und Spaltenebene.
* Datensicherung über [Konnektivität](#connectivity): Daten werden über Experience Platform und externe Clients gesichert, indem eine eingeschränkte Verbindung mit ablaufenden oder nicht ablaufenden Anmeldeinformationen hergestellt wird.
* Datensicherung durch [Verschlüsselung und kundenverwaltete Schlüssel (CMK)](#encryption-and-customer-managed-keys): Der Zugriff wird durch Verschlüsselung gesteuert, wenn sich die Daten im Ruhezustand befinden.

### Zugangssteuerung {#access-control}

Mit der Zugriffssteuerung in Adobe Experience Platform können Sie [Adobe Admin Console](https://adminconsole.adobe.com/) verwenden, um den Zugriff auf Abfrage-Service-Funktionen mithilfe von rollenbasierten Berechtigungen zu verwalten. Auf ähnliche Weise können Sie den Zugriff auf bestimmte Datenattribute durch die Kennzeichnungsverwaltung in Schemata und Datenfeldern steuern.

In diesem Abschnitt werden die erforderlichen Zugriffssteuerungsberechtigungen beschrieben, die ein Benutzer besitzen muss, um die Funktionen des Abfrage-Service vollständig nutzen zu können. Detaillierte Anweisungen zum Zuweisen [ Zugriffs auf ein Produktprofil finden ](../../access-control/ui/permissions.md) in den Dokumenten [&#128279;](../../access-control/ui/users.md)Verwalten von Berechtigungen“ und &quot; von Benutzern“.

#### Relevante Berechtigungen

Die entsprechenden Zugriffssteuerungsberechtigungen werden in den folgenden Tabellen entsprechend ihrem Umfang definiert.

**Berechtigungen zum Ausführen von Abfragen**

Um Abfragen im Abfrage-Service auszuführen, muss einem Benutzer eine Rolle mit der folgenden Berechtigung zugewiesen werden:

| Berechtigung | Beschreibung |
|---|---|
| [!UICONTROL Verwalten von Abfragen] | Mit dieser Berechtigung können Benutzer Datenexploration und Batch-Abfragen ausführen, die entweder einen vorhandenen Datensatz lesen oder Daten in Datensätze schreiben können. Dazu gehören sowohl `CREATE TABLE AS SELECT` (`CTAS`) als auch `INSERT INTO AS SELECT` (`ITAS`) Abfragen. |

**Datensatzberechtigungen**

Dieser Abschnitt dient als Anleitung für den ressourcenbasierten Zugriff, der für den Zugriff auf Datensätze beim Abfragen von Daten über den Abfrage-Service erforderlich ist.

Über die Benutzeroberfläche Berechtigungen können Sie eine ressourcenbasierte Zugriffssteuerung für einen Datensatz und ein Schema mit den folgenden Berechtigungen definieren:

| Berechtigung | Beschreibung |
|---|---|
| [!UICONTROL Datensätze verwalten] | Diese Berechtigung bietet schreibgeschützten Zugriff für Schemata und ermöglicht den Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen zur Verwendung mit dem Abfrage-Service. |
| [!UICONTROL Anzeigen von Datensätzen] | Diese Berechtigung ermöglicht schreibgeschützten Zugriff für Datensätze und Schemata zur Verwendung mit dem Abfrage-Service. |

#### Zugriffssteuerung für Spalten/Felder

Die attributbasierte Zugriffssteuerungsfunktion ermöglicht es Benutzern von Query Service, den Zugriff auf kritische Benutzerdaten zu beschränken. Der Zugriff kann basierend auf den einer Rolle zugewiesenen Berechtigungen gewährt oder eingeschränkt werden. Der Benutzerzugriff auf einzelne Spalten wird durch die entsprechenden Datennutzungskennzeichnungen und die Berechtigungssätze gesteuert, die auf die den Benutzern zugewiesenen Rollen angewendet werden.

Durch das Tagging von Schemafeldgruppen und -klassen mit Datennutzungskennzeichnungen werden Datennutzungsbeschränkungen auf alle Schemata mit denselben Feldergruppen und -klassen angewendet. Umfassende Informationen zu [ Funktion finden Sie in der Übersicht ](../../access-control/abac/overview.md) (attributbasierte Zugriffssteuerung) .

Mit dieser Funktion können Sie den Benutzergruppen Ihrer Wahl Zugriffsrechte auf vertrauliche Spalten gewähren. Die Zugriffssteuerung für eine Spalte kann die Lese- und Schreibfunktionen für einen bestimmten Benutzertyp einschränken.

Die Zugriffssteuerung für Spalten kann sowohl für Standard- als auch für Ad-hoc-Schemata auf Schemaebene angewendet werden. Wenden Sie Datennutzungskennzeichnungen auf XDM-Schemata an, um den Zugriff auf eine oder mehrere Spalten zu beschränken. Die Datenkennzeichnung wird konsistent angewendet, auch für Datensätze, die über den Abfrage-Service mit einem vordefinierten Schema oder einem Ad-hoc-Schema erstellt wurden, das im Rahmen des CTAS-Vorgangs generiert wurde.

Nachdem die entsprechende Zugriffsebene mithilfe von Kennzeichnungen und Rollen angewendet wurde, tritt das folgende Systemverhalten auf, wenn ein Benutzer versucht, auf die nicht zugänglichen Daten zuzugreifen:

1. Wenn einem Benutzer der Zugriff auf eine der Spalten innerhalb eines Schemas verweigert wurde, wird dem Benutzer auch die Berechtigung zum Lesen oder Schreiben für die eingeschränkte Spalte verweigert. Dies gilt für die folgenden gängigen Szenarien:

   * **Fall 1**: Wenn ein(e) Benutzende(r) versucht, eine Abfrage auszuführen, die nur eine eingeschränkte Spalte betrifft, gibt das System den Fehler aus, dass die Spalte nicht vorhanden ist.
   * **Fall 2**: Wenn ein(e) Benutzende(r) versucht, eine Abfrage mit mehreren Spalten auszuführen, die eine eingeschränkte Spalte enthalten, gibt das System nur die Ausgabe für alle nicht eingeschränkten Spalten zurück.

1. Wenn ein(e) Benutzende(r) versucht, auf ein berechnetes Feld zuzugreifen, muss er/sie Zugriff auf alle in der Komposition verwendeten Felder haben, oder das System verweigert auch den Zugriff auf das berechnete Feld.

#### Zugriffssteuerungen für Ansichten

Query Service bietet die Möglichkeit, standardmäßige ANSI-SQL für [`CREATE VIEW`](../sql/syntax.md#create-view)-Anweisungen zu verwenden. Bei hochsensiblen Daten-Workflows müssen Sie beim Erstellen von Ansichten entsprechende Steuerelemente durchsetzen.

Das Keyword `CREATE VIEW` definiert eine Ansicht einer Abfrage, die Ansicht ist jedoch nicht physisch materialisiert. Stattdessen wird die Abfrage jedes Mal ausgeführt, wenn in einer Abfrage auf die Ansicht verwiesen wird. Wenn ein(e) Benutzende(r) eine Ansicht aus einem Datensatz erstellt, werden die rollen- und attributbasierten Zugriffssteuerungsregeln für den übergeordneten Datensatz **nicht** hierarchisch angewendet. Daher müssen Sie beim Erstellen einer Ansicht explizit Berechtigungen für jede der Spalten festlegen.

#### Erstellen von feldbasierten Zugriffsbeschränkungen für beschleunigte Datensätze {#create-field-based-access-restrictions-on-accelerated-datasets}

Mit der [attributbasierten Zugriffssteuerungsfunktion](../../access-control/abac/overview.md) können Sie Organisations- oder Datennutzungsbereiche für Fakten- und Dimensionsdatensätze im [beschleunigten Speicher](../data-distiller/sql-insights/send-accelerated-queries.md) definieren. Dadurch können Admins den Zugriff auf bestimmte Segmente verwalten und den Zugriff für Benutzende oder Benutzergruppen besser verwalten.

Um feldbasierte Zugriffsbeschränkungen für beschleunigte Datensätze zu erstellen, können Sie CTAS-Abfragen des Abfrage-Service verwenden, um beschleunigte Datensätze zu erstellen und diese Datensätze auf der Grundlage vorhandener XDM-Schemata oder Ad-hoc-Schemata zu strukturieren. Admins können dann [Datennutzungsbeschriftungen für das Schema hinzufügen und bearbeiten](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) oder [Ad-hoc-Schema](./ad-hoc-schema-labels.md#edit-governance-labels). Sie können Kennzeichnungen auf Ihre Schemata über den Arbeitsbereich [!UICONTROL Kennzeichnungen] in der Benutzeroberfläche [!UICONTROL Schemata] anwenden, erstellen und bearbeiten.

Datennutzungsbeschriftungen können auch über die Benutzeroberfläche Datensätze [angewendet oder direkt auf den Datensatz ](../../data-governance/labels/user-guide.md#add-labels)) oder über den Arbeitsbereich Zugriffssteuerung [!UICONTROL Beschriftungen] erstellt werden. Weitere Informationen finden Sie in der Anleitung zum [Erstellen einer neuen ](../../access-control/abac/ui/labels.md)&quot;.

Der Benutzerzugriff auf einzelne Spalten kann dann durch die angehängten Datennutzungskennzeichnungen und die Berechtigungssätze gesteuert werden, die auf die Rollen angewendet werden, die den Benutzern zugewiesen sind.

### Konnektivität {#connectivity}

Auf den Abfrage-Service kann über die Benutzeroberfläche von Experience Platform oder durch Herstellen einer Verbindung mit externen kompatiblen Clients zugegriffen werden. Der Zugriff auf alle verfügbaren Fronts wird durch einen Satz von Anmeldeinformationen gesteuert.

#### Konnektivität über externe Clients

Für den Zugriff auf den Abfrage-Service mit einem Drittanbieter-Client sind Anmeldeinformationen für die Autorisierung erforderlich. Diese Anmeldeinformationen sind obligatorisch, um mit einem der kompatiblen externen Clients auf den Abfrage-Service zuzugreifen. Sie können eine Verbindung zu externen Clients herstellen, indem Sie entweder [ablaufende Anmeldeinformationen](#expiring-credentials) oder [nicht ablaufende Anmeldeinformationen](#non-expiring-credentials) verwenden.

#### Begrenzte Verbindungszeit über ablaufende Anmeldedaten {#expiring-credentials}

[Ablaufende Anmeldeinformationen](../ui/credentials.md) ermöglichen es Benutzern, eine temporäre Verbindung mit einem externen Client herzustellen. Dieser Satz von Anmeldeinformationen ist nur 24 Stunden lang gültig. Der Ablauf dieser Arten von Anmeldeinformationen wird zusammen mit der Registerkarte Anmeldeinformationen im Dashboard des Abfrage-Services angezeigt.

![Die Registerkarte „Anmeldeinformationen“ in Query Service Workspace mit hervorgehobenen ablaufenden Anmeldeinformationen.](../images/data-governance/overview/expiring-credentials.png)

#### Unbefristete Anmeldedaten {#non-expiring-credentials}

[Nicht ablaufende Anmeldeinformationen](../ui/credentials.md#non-expiring-credentials) ermöglichen es Ihnen, eine permanente Verbindung mit einem externen Client herzustellen, was die Verbindung zum Abfrage-Service erleichtert, ohne dass ein manuelles Kennwort erforderlich ist.

Um die Option zum Generieren nicht ablaufender Zugangsdaten zu aktivieren, müssen Sie den beschriebenen [vorausgesetzte Workflow“ ](../ui/credentials.md#prerequisites). Im Rahmen dieses Prozesses muss Ihr Organisationsadministrator Berechtigungen für das Produktprofil konfigurieren, sodass der Administrator steuern kann, welche Konten Zugriff auf die Verwendung nicht ablaufender Anmeldeinformationen haben.

Technische Benutzerkonten mit unbefristeten Anmeldeinformationen können Rollen zugewiesen werden, um eine angemessene Data Governance sicherzustellen, indem der Umfang ihres Lese- und Schreibzugriffs auf der Grundlage ihrer Zuständigkeiten und Anforderungen definiert wird. Siehe vorherigen Abschnitt unter [Verwenden rollenbasierter Berechtigungen durch Zugriffssteuerung](#access-control) zum Verwalten des Zugriffs auf den Abfrage-Service.

Sobald der vorausgesetzte Workflow abgeschlossen ist, können autorisierte Benutzer jetzt [die erforderlichen Verbindungsanmeldeinformationen generieren](../ui/credentials.md#generate-credentials).

#### SSL-Datenverschlüsselung

Zur Erhöhung der Sicherheit bietet der Abfrage-Service native Unterstützung für SSL-Verbindungen zur Verschlüsselung der Client/Server-Kommunikation. Experience Platform unterstützt verschiedene SSL-Optionen, um Ihre Datensicherheitsanforderungen zu erfüllen und den Verarbeitungsaufwand für Verschlüsselung und Schlüsselaustausch auszugleichen.

Weitere Informationen, einschließlich der Verwendung [ SSL-Parameterwerts `verify-full`, finden Sie im Handbuch zu verfügbaren SSL](../clients/ssl-modes.md)Optionen für Clientverbindungen von Drittanbietern zum Abfrage-Service .

### Verschlüsselung und kundenverwaltete Schlüssel (CMK) {#encryption-and-customer-managed-keys}

Verschlüsselung ist die Verwendung eines algorithmischen Prozesses, um Daten in verschlüsselten und unlesbaren Text umzuwandeln, um sicherzustellen, dass die Informationen geschützt sind und ohne einen Entschlüsselungsschlüssel nicht zugänglich sind.

Die Datenkonformität des Abfrage-Service stellt sicher, dass Daten immer verschlüsselt werden. Daten in Übertragung sind immer HTTPS-konform und ruhende Daten werden in einem Azure Data Lake-Speicher mithilfe von Schlüsseln auf Systemebene verschlüsselt. Weitere Informationen finden Sie in der Dokumentation [So werden Daten in Adobe Experience Platform ](../../landing/governance-privacy-security/encryption.md). Einzelheiten dazu, wie Data-at-Rest im Azure Data Lake Storage verschlüsselt werden, finden Sie in der [offiziellen Azure-Dokumentation](https://docs.microsoft.com/de-de/azure/data-lake-store/data-lake-store-encryption).

Daten in Übertragung sind immer HTTPS-kompatibel. Wenn sich die Daten im Data Lake im Ruhezustand befinden, erfolgt die Verschlüsselung mit dem Customer Management Key (CMK), der bereits von Data Lake Management unterstützt wird. Die derzeit unterstützte Version ist TLS1.2. In der [Dokumentation Kundenverwaltete Schlüssel (CMK) ](../../landing/governance-privacy-security/customer-managed-keys/overview.md) Sie, wie Sie Ihre eigenen Verschlüsselungsschlüssel für in Adobe Experience Platform gespeicherte Daten einrichten.


## Verfolgung {#audit}

Der Abfrage-Service zeichnet Benutzeraktivitäten auf und kategorisiert diese Aktivitäten in verschiedene Protokolltypen. Die Protokolle geben Informationen darüber **wer** welche **ausgeführt** wann **.**. Jede in einem Protokoll aufgezeichnete Aktion enthält Metadaten, die den Aktionstyp, das Datum und die Uhrzeit, die E-Mail-ID des Benutzers, der die Aktion ausgeführt hat, und zusätzliche Attribute angeben, die für den Aktionstyp relevant sind.

Jede der Protokollkategorien kann von einem Experience Platform-Benutzer nach Bedarf angefordert werden. Dieser Abschnitt enthält Details zum Typ der für den Abfrage-Service erfassten Informationen und dazu, wo auf diese Informationen zugegriffen werden kann.

### Abfrageprotokolle {#query-logs}

Die Benutzeroberfläche für Abfrageprotokolle ermöglicht es Ihnen, Ausführungsdetails für alle Abfragen zu überwachen und zu überprüfen, die entweder über den Abfrage-Editor oder die Abfrage-Service-API ausgeführt wurden. Dies bringt Transparenz in die Aktivitäten des Abfrage-Service, sodass Sie die Metadaten auf (**)** Abfragen überprüfen können, die im gesamten Abfrage-Service ausgeführt wurden. Sie enthält alle Arten von Abfragen, unabhängig davon, ob es sich um eine explorative, Batch- oder geplante Abfrage handelt.

Auf Abfrageprotokolle kann entweder über die Experience Platform-Benutzeroberfläche auf der Registerkarte [!UICONTROL Protokolle] des Arbeitsbereichs [!UICONTROL Abfragen] zugegriffen werden.

![Die Registerkarte „Abfrageprotokoll“ mit hervorgehobenem Detailbereich.](../images/data-governance/overview/queries-log.png)

### Audit-Protokolle {#audit-logs}

Auditprotokolle enthalten detailliertere Informationen als Abfrageprotokolle und ermöglichen es Ihnen, Protokolle nach Attributen wie Benutzer, Datum, Art der Abfrage usw. zu filtern. Über die in der Benutzeroberfläche des Abfrageprotokolls verfügbaren Details hinaus werden in Audit-Protokollen Details zu einzelnen Benutzern sowie deren Sitzungsdaten oder Konnektivität zu einem Drittanbieter-Client gespeichert.

Durch die Bereitstellung einer genauen Aufzeichnung von Benutzeraktionen kann ein Audit-Protokoll bei der Fehlerbehebung helfen und Ihrem Unternehmen helfen, die Richtlinien zur Unternehmensdatenverwaltung und die gesetzlichen Anforderungen effektiv zu erfüllen. Auditprotokolle zeichnen alle Experience Platform-Aktivitäten auf. Mithilfe von Auditprotokollen können Sie Benutzeraktionen in Bezug auf die Ausführung von Abfragen, Vorlagen und geplante Abfragen überprüfen, um die Transparenz und Sichtbarkeit der von Benutzern in Query Service durchgeführten Aktionen zu erhöhen.

Die folgende Tabelle zeigt die von Audit-Protokollen erfassten Abfragekategorien und die aufgezeichneten Aktionstypen:

| Kategorie | Aktionstyp |
|---|---|
| Abfrage | Execute |
| Abfragevorlage | Erstellen, Löschen, Aktualisieren |
| Geplante Abfrage | Erstellen, Löschen, Aktualisieren |

Nachfolgend finden Sie eine Liste mit drei erweiterten Server-Protokollen, die mehr Details enthalten als die in den Abfrageprotokollen enthaltenen. Die erweiterten Protokolle befinden sich in den Abfragekategorien der Auditprotokolle:

1. **Meta-Abfrageprotokolle**: Wenn eine Abfrage ausgeführt wird, werden verschiedene zugehörige Backend-Unterabfragen (z. B. Parsing) ausgeführt. Diese Arten von Abfragen werden als „Metadatenabfragen“ bezeichnet. Ihre relevanten Details finden Sie in den Auditprotokollen.
1. **Sitzungsprotokolle**: Das System erstellt ein Sitzungseintragsprotokoll für einen Benutzer, wenn er sich beim Abfrage-Service anmeldet, unabhängig davon, ob er eine Abfrage ausführt.
1. **Verbindungsprotokolle von Drittanbietern**: Ein Verbindungsprüfprotokoll wird generiert, wenn ein Benutzer den Abfrage-Service erfolgreich mit einem Client eines Drittanbieters verbindet.

Weitere Informationen darüber[ wie Auditprotokolle Ihrem Unternehmen helfen können, die Einhaltung von Datenvorschriften zu gewährleisten, finden Sie ](../../landing/governance-privacy-security/audit-logs/overview.md) „Übersicht über Auditprotokolle“.

## Datennutzung {#data-usage}

Das Data Governance-Framework in Experience Platform bietet eine einheitliche Möglichkeit, Daten in allen Adobe-Lösungen, -Services und -Plattformen verantwortungsvoll zu verwenden. Sie koordiniert den systemischen Ansatz zur Erfassung, Kommunikation und Verwendung von Metadaten in Adobe Experience Cloud. Dies wiederum hilft Datenverantwortlichen dabei, Daten entsprechend den erforderlichen Marketing-Aktionen und den Einschränkungen zu kennzeichnen, die für diese Daten aus diesen beabsichtigten Marketing-Aktionen gelten. In der Übersicht zu [Datennutzungskennzeichnungen](../../data-governance/labels/overview.md) finden Sie weitere Informationen darüber, wie Sie mit Data Governance Datennutzungskennzeichnungen auf Datensätze und Felder anwenden können.

Es ist Best Practice, in jeder Phase des Journey der Daten auf die Einhaltung der Datenrichtlinien hinzuarbeiten. Zu diesem Zweck sollten abgeleitete Datensätze, die Ad-hoc-Schemata verwenden, im Rahmen des Data Governance-Frameworks entsprechend gekennzeichnet werden. Es gibt zwei Arten von abgeleiteten Datensätzen, die vom Abfrage-Service gebildet werden: Datensätze, die ein Standardschema verwenden, und Datensätze, die ein Ad-hoc-Schema verwenden.

>[!NOTE]
>
>Datensätze, die mit dem Abfrage-Service erstellt werden, werden als „abgeleitete Datensätze“ bezeichnet.

Da Ad-hoc-Schemata von einem einzelnen Benutzer für einen bestimmten Zweck erstellt werden, werden die XDM-Schemafelder für diesen bestimmten Datensatz mit einem Namespace versehen und sind nicht für die Verwendung in verschiedenen Datensätzen vorgesehen. Daher sind Ad-hoc-Schemata in der Experience Platform-Benutzeroberfläche standardmäßig nicht sichtbar. Obwohl es bei der Anwendung von Datennutzungskennzeichnungen keinen Unterschied zwischen Standard- und Ad-hoc-Schemata gibt, müssen Ad-hoc-Schemata, die vom Abfrage-Service zum Zweck der Kennzeichnung erstellt wurden, zunächst in der Experience Platform-Benutzeroberfläche sichtbar gemacht werden. Weitere Informationen finden Sie im Handbuch [Erkennen von Ad-hoc-Schemata in ](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) Experience Platform-Benutzeroberfläche“.

Nachdem Sie auf das Schema zugegriffen haben, können Sie [Kennzeichnungen auf einzelne Felder anwenden](../../xdm/tutorials/labels.md). Sobald ein Schema gekennzeichnet wurde, erben alle Datensätze, die von diesem Schema abgeleitet sind, diese Kennzeichnungen. Von hier aus können Sie Datennutzungsrichtlinien einrichten, die verhindern können, dass Daten mit bestimmten Beschriftungen für bestimmte Ziele aktiviert werden. Weitere Informationen finden Sie in der Übersicht zu [Datennutzungsrichtlinien](../../data-governance/policies/overview.md).

## Datenschutz    {#privacy}

[Privacy Service](../../privacy-service/home.md) unterstützt Sie bei der Verwaltung von Kundenanfragen zum Zugriff auf und zur Löschung ihrer Daten gemäß den gesetzlichen Datenschutzbestimmungen. Dies erfolgt, indem nach bereits vorhandenen Kennungen gesucht wird und je nach angefordertem Datenschutzauftrag entweder auf diese Daten zugreift oder sie löscht. Die Daten müssen ordnungsgemäß gekennzeichnet werden, damit der Service feststellen kann, welche Felder während der Datenschutzaufträge aufgerufen oder gelöscht werden sollen. Daten, die Gegenstand von Datenschutzanfragen sind, müssen Informationen zur Kundenidentität enthalten, um die unterschiedlichen Datenelemente mit der Person zu verknüpfen, für die die Datenschutzanfrage gilt. Query Service kann die von ihm verwendeten Daten mit einer eindeutigen Kennung anreichern, um Datenschutzaufträge zu erfüllen.

Datenschutzanfragen können an den Data Lake oder den Profildatenspeicher gesendet werden. Aus dem Data Lake gelöschte Datensätze führen nicht zum Löschen von Profilen, die aus diesen Datensätzen erstellt wurden. Ein Datenschutzauftrag zum Löschen personenbezogener Daten aus dem Data Lake löscht auch nicht sein Profil, sodass alle Informationen (die diese Profil-ID enthalten), die nach Abschluss des Datenschutzauftrags aufgenommen werden, dieses Profil wie gewohnt aktualisieren. Dies bekräftigt die Notwendigkeit, in Ad-hoc-Schemata verwendete Daten ordnungsgemäß zu identifizieren.

Weitere Informationen finden Sie in der Privacy Service[Dokumentation zu Identitätsdaten für Datenschutzanfragen und ](../../privacy-service/identity-data.md), wie Sie Ihre Datenvorgänge konfigurieren und Adobe-Technologien nutzen können, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.

Die Funktionen des Abfrage-Service für die Data Governance vereinfachen und optimieren den Prozess der Datenkategorisierung und die Einhaltung von Datennutzungsbestimmungen. Nachdem die Daten identifiziert wurden, können Sie mit dem Abfrage-Service die primäre Identität für alle Ausgabedatensätze zuweisen. Sie **müssen** Identitäten zum Datensatz hinzufügen, um Datenschutzanfragen zu erleichtern und auf die Einhaltung von Datenschutzbestimmungen hinzuarbeiten.

Schemadatenfelder können über die Experience Platform-Benutzeroberfläche als Identitätsfeld festgelegt werden. Darüber hinaus ermöglicht Ihnen der Abfrage-Service, die [ mithilfe des SQL-Befehls „ALTER TABLE“ zu ](../sql/syntax.md#alter-table). Das Festlegen einer Identität mit dem Befehl `ALTER TABLE` ist besonders dann hilfreich, wenn Datensätze mithilfe von SQL und nicht direkt aus einem Schema über die Experience Platform-Benutzeroberfläche erstellt werden. In der Dokumentation finden Sie Anweisungen zum [ von Identitätsfeldern in der Benutzeroberfläche bei ](../../xdm/ui/fields/identity.md) Verwendung von Standardschemata.

## Datenhygiene {#data-hygiene}

„Datenhygiene“ bezieht sich auf den Prozess der Reparatur oder Entfernung von Daten, die veraltet, ungenau, falsch formatiert, dupliziert oder unvollständig sind. Diese Prozesse stellen sicher, dass Datensätze systemübergreifend korrekt und konsistent sind. Es ist wichtig, eine angemessene Datenhygiene bei jedem Schritt des Journey der Daten und sogar vom ersten Datenspeicherort sicherzustellen. Im Abfrage-Service von Experience Platform ist dies entweder der Data Lake oder der beschleunigte Speicher.

Sie können einem abgeleiteten Datensatz eine Identität zuweisen, um die Datenverwaltung im Anschluss an die zentralisierten Datenhygiene-Services von Experience Platform zu ermöglichen.

Wenn Sie dagegen einen aggregierten Datensatz im beschleunigten Speicher erstellen, können die aggregierten Daten nicht zur Ableitung der Originaldaten verwendet werden. Durch diese Datenaggregation entfällt die Notwendigkeit, Anfragen zur Datenhygiene zu stellen.

Eine Ausnahme in diesem Szenario ist der Fall der Löschung. Wenn eine Datenhygiene-Löschung für einen Datensatz angefordert wird und bevor die Löschung abgeschlossen ist, eine andere abgeleitete Datensatzabfrage ausgeführt wird, erfasst der abgeleitete Datensatz Informationen aus dem ursprünglichen Datensatz. In diesem Fall müssen Sie beachten, dass Sie, wenn eine Anfrage zum Löschen eines Datensatzes gesendet wurde, keine neu abgeleiteten Datensatzabfragen mit derselben Datensatzquelle ausführen dürfen.

Weitere [ zur Datenhygiene in Adobe Experience Platform finden Sie ](../../hygiene/home.md) der Übersicht zur Datenhygiene .
