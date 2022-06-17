---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 1dc97fa33fa8cb46184e11d311ef8246199b4f03
workflow-type: tm+mt
source-wordcount: '2409'
ht-degree: 73%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 25. Mai 2022**

Neue Funktionen in Adobe Experience Platform:

- [Attributbasierte Zugriffssteuerung](#abac)
- [Datenhygiene](#hygiene)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [Auditprotokolle](#audit-logs)
- [Dashboards](#dashbaords)
- [Datenerfassung](#data-collection)
- [Data Governance](#data-governance)
- [Datenvorbereitung](#data-prep)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Query Service](#query-service)
- [Quellen](#sources)

## Attributbasierte Zugriffssteuerung {#abac}

>[!IMPORTANT]
>
>Die attribut-basierte Zugriffskontrolle ist derzeit in einer eingeschränkten Version für US-Kunden im Gesundheitswesen verfügbar. Diese Funktion steht allen Real-time Customer Data Platform-Kunden nach der vollständigen Veröffentlichung zur Verfügung.

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, mit der Administratoren den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können. Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Ein Administrator definiert Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

Mithilfe der attributbasierten Zugriffskontrolle können Administratoren Ihres Unternehmens den Zugriff der Benutzer auf sowohl sensible persönliche Daten (EPPD) als auch personenbezogene Daten (PII) für alle Platform-Workflows und -Ressourcen steuern. Administratoren können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

| Funktion | Beschreibung |
| --- | --- |
| Attributbasierte Zugriffssteuerung | Mit der attributbasierten Zugriffskontrolle können Sie Experience-Datenmodell (XDM)-Schemafelder mit Bezeichnungen versehen, die Organisations- oder Datennutzungsbereiche definieren. Parallel dazu können Administratoren die Benutzeroberfläche zur Verwaltung von Benutzern und Rollen verwenden, um Zugriffsrichtlinien zu definieren, die XDM-Schemafelder abdecken, und den Zugriff, der Benutzern oder Benutzergruppen (interne, externe oder Drittanbieter-Benutzer) gewährt wird, besser verwalten. Darüber hinaus ermöglicht die attributbasierte Zugriffskontrolle Administratoren die Verwaltung des Zugriffs auf bestimmte Segmente. Weitere Informationen finden Sie unter [Attributbasierte Zugriffskontrolle - Übersicht](../../access-control/abac/overview.md). |
| Berechtigungen | Berechtigungen sind der Bereich des Experience Cloud, in dem Administratoren Benutzerrollen und Zugriffsrichtlinien definieren können, um Zugriffsberechtigungen für Funktionen und Objekte in einer Produktanwendung zu verwalten. Über Berechtigungen können Sie Rollen erstellen und verwalten sowie die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen. Mit Berechtigungen können Sie auch die Bezeichnungen, Sandboxes und Benutzer verwalten, die einer bestimmten Rolle zugeordnet sind. Weitere Informationen finden Sie unter [Handbuch zur Berechtigungs-UI](../../access-control/abac/ui/browse.md). |

Weitere Informationen zur attributbasierten Zugriffskontrolle finden Sie unter [Attributbasierte Zugriffskontrolle - Übersicht](../../access-control/abac/overview.md).

## Datenhygiene {#hygiene}

Experience Platform bietet eine Reihe von Funktionen zur Datenhygiene, mit denen Sie Ihre gespeicherten Daten durch programmatische Löschungen von Verbraucherdatensätzen und -datensätzen verwalten können. Verwenden Sie entweder die [!UICONTROL Datenhygiene] Workspace in der Benutzeroberfläche oder durch Aufrufe der Data Hygiene-API können Sie Ihre Datenspeicher verwalten, um sicherzustellen, dass Informationen erwartungsgemäß verwendet, bei der Korrektur falscher Daten aktualisiert und gelöscht werden, wenn dies von organisatorischen Richtlinien für erforderlich gehalten wird.

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene stehen derzeit nur Organisationen zur Verfügung, die das Zusatzangebot Adobe Shield for Healthcare erworben haben.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Time to Live (TTL) für Datensätze | [TTLs planen](../../hygiene/ui/ttl.md) für Platform-Datensätze. |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Auditprotokollen in Platform finden Sie im Abschnitt [Übersicht über die Datenhygiene](../../hygiene/home.md).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Aktualisierte Funktionen**

| Funktion | Warnhinweisregel | Beschreibung |
| --- | --- | --- |
| Neue Warnregel | Überspringrate überschreitet Schwellenwert | Jetzt können Sie den Warnhinweis verwenden, um Benachrichtigungen zu erhalten, wenn der Datenfluss Ihrer Quellen die Identitätsschwellen überschreitet. Die aktualisierte Liste der Warnhinweistypen finden Sie in der Übersicht zu [Warnhinweisregeln](../../observability/alerts/rules.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Warnungen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../../observability/home.md).

## Auditprotokolle {#audit-logs}

Mit Experience Platform können Sie die Benutzeraktivität in Verbindung mit verschiedenen Services und Funktionen überprüfen. Die Auditprotokolle enthalten Informationen darüber, wer wann was getan hat.

**Aktualisierte Funktionen**

| Funktion | Name | Beschreibung |
| --- | --- | --- |
| Ressourcen hinzugefügt | <ul><li> Zugriffssteuerungsrichtlinie </li><li> Rolle </li><li> Auditprotokolle </li><li> Arbeitsauftrag </li><li> Identity-Namespace </li><li> Identitätsdiagramm </li><li> Abfrage </li><li> Datensatz </li><li> Quelldatenfluss </li></ul> | Die Administratorprotokoll-Ressourcen werden automatisch aufgezeichnet, wenn die Aktivität stattfindet. Wenn die Funktion aktiviert ist, müssen Sie die Protokollerfassung nicht manuell aktivieren. |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Auditprotokollen in Platform finden Sie im Abschnitt [Übersicht über Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md).

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, in denen Sie wichtige Informationen zu den Daten Ihres Unternehmens sehen, basierend auf täglichen Schnappschüssen der Daten.

### Profile-Dashboards

Im Dashboard „Profile“ wird ein Schnappschuss der Attributdaten (Datensatzdaten) dargestellt, die sich in Ihrem Unternehmen im Profilspeicher in Experience Platform befinden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Zielgruppenüberschneidung durch Zusammenführungsrichtlinien-Widget | Dieses Widget stellt die visuelle Überschneidung von Segmentdefinitionen dar und ermöglicht es Ihnen, die Segmentierungsstrategie zu optimieren, indem Sie die Ähnlichkeiten zwischen Ihren Segmentdefinitionen untersuchen. |
| Änderung der Profilanzahl durch Identitäts-Widget | Dieses Widget hilft Ihnen bei der Verwaltung Ihrer Zielaktivierung, indem es das Wachstumsmuster der Profile darstellt, die nach der entsprechenden Identität gefiltert wurden. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Profilen finden Sie in der [Dokumentation zum Dashboard „Profile“](../../dashboards/guides/profiles.md).

### Ziele-Dashboards

Im Dashboard „Ziele“ finden Sie einen Schnappschuss der Ziele, die Ihr Unternehmen in Experience Platform aktiviert hat.

| Funktion | Beschreibung |
| --- | --- |
| Aktivierte Zielgruppen durch Ziel-Widget | Dieses Widget hilft Ihnen, auf einen Blick den Wert Ihrer Ziele anhand der Anzahl der aktivierten Zielgruppen zu erkennen. Außerdem erhalten Sie einfachen Zugriff auf detailliertere Informationen zu den Segmenten, die dem Ziel zugeordnet wurden. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Zielen finden Sie in der [Dokumentation zum Ziele-Dashboard](../../dashboards/guides/destinations.md).

### Segmente-Dashboards

Das Dashboard „Segmente“ bietet eine Benutzeroberfläche, in der wichtige, bei einem täglichen Schnappschuss erfasste Informationen zu Ihren Segmenten angezeigt werden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Zielgruppen-Überlappungs-Widget | Mit diesem Widget können Sie Ihre Segmentierungsstrategie optimieren, indem Sie die Ähnlichkeiten in den Ergebnissen Ihrer Segmentdefinitionen visualisieren. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Segmenten finden Sie in der [Dokumentation zum Segmente-Dashboard](../../dashboards/guides/segments.md).

## Datenerfassung {#data-collection}

Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe oder andere Ziele weitergegeben werden können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Kopieren von Datenströmen | [Zum Erstellen einer Kopie eines vorhandenen Datenstroms](../../edge/datastreams/overview.md#copy) und zur Anpassung der Konfiguration, sodass Sie nicht von Grund auf neu beginnen müssen. |
| Importieren von Datenstrom-Zuordnungsregeln | Bei der Durchführung der Datenvorbereitung für die Datenerfassung können Sie [die Zuordnungsregeln eines vorhandenen Datenstroms importieren](../../edge/datastreams/data-prep.md#import-mapping) anstatt jede Feldzuordnung manuell zu konfigurieren. |
| Unterstützung der Datenstrom-Zuordnung für das Mobile SDK | Sie können jetzt die Datenvorbereitung für die Datenerfassung für Datenströme konfigurieren, die für die Verwendung mit dem Experience Platform Mobile SDK vorgesehen sind. |
| Unterstützung der Datenstrom-Zuordnung für XDM-Objekte | Ordnen Sie [bei der Konfiguration der Datenvorbereitung für die Datenerfassung](../../edge/datastreams/data-prep.md#select-data) zusätzlich zu Datenschichtobjekten auch XDM-Objekte zu. |
| Integration mit Datenflüssen | Verwenden Sie den Quellenkatalog in Platform, um auf Ihre Daten in Platform Edge Network zuzugreifen, einschließlich der Datenvorbereitung für die Datenerfassung und der verbesserten Unterstützung für Datenvorbereitungs-Warnungen. Weitere Informationen erhalten Sie in der [Übersicht über die Adobe-Datenerfassungsquellen](../../sources/connectors/adobe-applications/data-collection.md). |

Weitere Informationen zur Datenerfassung in Platform finden Sie in der [Übersicht zur Datenerfassung](../../collection/home.md).

## Data Governance {#governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Sie spielt eine Schlüsselrolle in [!DNL Experience Platform] auf verschiedenen Ebenen, einschließlich Katalogisierung, Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffskontrolle auf Daten für Marketing-Aktionen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Durchsetzung von Einwilligungsrichtlinien (begrenzte Verfügbarkeit) | Wenn Ihr Unternehmen das Zusatzangebot Adobe Shield for Healthcare erworben hat, können Sie jetzt [Einverständnisrichtlinien erstellen](../../data-governance/policies/user-guide.md#consent-policy) automatisch [Kundenzustimmung und Voreinstellungen bei der Segmentbeteiligung durchsetzen](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation). |

{style=&quot;table-layout:auto&quot;}

Siehe [Data Governance - Übersicht](../../data-governance/home.md) für weitere Informationen zum Dienst.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Attributbasierte Zugriffssteuerung in [!DNL Data Prep] | Sie können jetzt nur Attribute zuordnen, auf die Sie Zugriff haben. Attribute, auf die Sie keinen Zugriff haben, können nicht in Pass-Through-Mappings und berechneten Feldern verwendet werden. Weitere Informationen finden Sie unter [attributbasierte Zugriffssteuerung in [!DNL Data Prep]](../../data-prep/home.md). **Hinweis**: Die attribut-basierte Zugriffskontrolle ist derzeit in einer eingeschränkten Version für US-Kunden im Gesundheitswesen verfügbar. Diese Funktion steht allen Real-time Customer Data Platform-Kunden nach der vollständigen Veröffentlichung zur Verfügung. |
| Lokalisierte Datenfehler | Mit [!DNL Data Prep] werden nun alle Umwandlungsfehler auf Attributebene lokalisiert (zuvor auf Zeilenebene). In Datenflüssen werden jetzt Teile von Zeilen aufgenommen, die mit Spalten gefüllt sind, die keine Transformationsfehler aufweisen, anstatt die gesamten Zeilen zu ignorieren. |
| Streamen von Upsert-Vorgängen nach [!DNL Profile Service] | Streamen Sie Upsert-Vorgänge mit [!DNL Data Prep], um Aktualisierungen von Teilzeilen mithilfe der Quelle [[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md), [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md) oder [[!DNL HTTP API]](../../sources/connectors/streaming/http.md) an Profile Service zu senden. Weitere Informationen dazu finden Sie im Handbuch zum [Streamen von Upserts](../../data-prep/upserts.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| Exportieren der neuesten Profilqualifikationen [nach täglicher Segmentbewertung](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Sie können jetzt einen Zeitplan für einen vollständigen einmalig oder täglich durchgeführten Dateiexport mit den neuesten Profilqualifikationen festlegen, nachdem die tägliche Segmentbewertung abgeschlossen ist. |
| Optionale Datenstrom-ID für [Adobe Target-Ziele](../../destinations/catalog/personalization/adobe-target-connection.md) | Um die Adobe Target-Personalisierung für Benutzer zu aktivieren, die das Experience Platform Web SDK nicht implementieren können, ist die Auswahl der Datenstrom-ID jetzt bei der Konfiguration von Adobe Target-Zielen optional. Wenn Sie keinen Datenstrom verwenden, unterstützen Segmente, die von Experience Platform nach Target exportiert werden, nur die Personalisierung der nächsten Sitzung, wenn die Edge-Segmentierung deaktiviert ist, sowie alle [Anwendungsfälle](../../destinations/ui/configure-personalization-destinations.md), die die Edge-Segmentierung benötigen. |

{style=&quot;table-layout:auto&quot;}

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [[!UICONTROL Change set]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/changeset.schema.json) | Erfasst Änderungen auf Zeilenebene, die von Datensätzen stammen oder für Datensätze gedacht sind. Diese Feldergruppe kann von jeder beliebigen Klasse verwendet werden. |
| Feldergruppe | [[!UICONTROL Reference keys]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-reference-keys.schema.json) | Erfasst Referenzschlüssel für ExperienceEvent-Schemas, mit denen Sie Beziehungen zu Schemas aufbauen können, die auf anderen Klassen basieren. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung der Aktualisierung |
| --- | --- | --- |
| Verhalten | [[!UICONTROL Time-series Schema]](https://github.com/surbhi114/xdm/blob/master/components/behaviors/time-series.schema.json) | `eventType` wurde aktualisiert und beinhaltet jetzt mehrere neue Ereignistypen im Zusammenhang mit Medien und einen Anwendungsfall mit einem eingehenden Web-Kanal für Adobe Journey Optimizer. |
| Globales Schema | [[!UICONTROL Ziel]](https://github.com/tumulurik/xdm/blob/master/schemas/destinations/destination.schema.json) | Enum-Werte wurden aus `xdm:destinationCategory` entfernt. |
| Feldergruppe | [[!UICONTROL Record Status]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/record-status.schema.json) | Der Feldergruppenstatus wurde von `experimental` auf `stable` aktualisiert. |
| Feldergruppe | (Mehrere) | Mehrere B2B-Feldergruppen wurden aktualisiert, sodass statt bestimmten ID-Feldern Schlüsselfelder verwendet werden, die den Datentyp [[!UICONTROL B2B-Quelle]](../../xdm/data-types/b2b-source.md) nutzen. Die früheren ID-Felder werden in der zukünftigen Aktualisierung nicht mehr unterstützt. Eine vollständige Liste der Änderungen an den Feldergruppen erhalten Sie über die folgende [Pull-Anfrage](https://github.com/adobe/xdm/pull/1533/files#diff-720c0bb1d1cbaf622f5656c2a4b62d35830c75f6563794da72a280a6a520fbc1). |
| Datentyp | [[!UICONTROL Browser-Details]](https://github.com/liljenback/xdm/blob/master/components/datatypes/browserdetails.schema.json) | Das neue Feld `xdm:userAgentClientHints` wurde hinzugefügt, das kontextbezogene Informationen über den Benutzeragenten erfasst, der mit dem Browser interagiert. |
| Datentyp | [[!UICONTROL Media information]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/media.schema.json) | Das Feld `xdm:playhead` wurde hinzugefügt, um die Abspielzeit eines Medieninhalts zu erfassen. Mustervalidierung für `xdm:videoSegment` wurde korrigiert. |
| Datentyp | [[!UICONTROL Rating]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/external/iptc/rating.schema.json) | `iptc4xmpExt:RatingSourceLink` ist kein erforderliches Feld mehr. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL data lake]. Sie können beliebige Datensätze aus dem [!DNL data lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Integration des Administratorprotokolls in Query Service | Durch die Integration des Administratorprotokolls in Query Service werden Datensätze zu abfragebezogenen Benutzeraktionen bereitgestellt, die zur Fehlerbehebung oder zur Einhaltung von Unternehmensrichtlinien zur Datenverwaltung und Regulierungsanforderungen verwendet werden können. Vollständige Informationen dazu finden Sie in der [Dokumentation zur Administratorprotokoll-Integration](../../query-service/data-governance/audit-log-guide.md). |
| SQL-Konstrukt ALTER TABLE | Verwenden Sie SQL, um primäre Identitäten in einem Ad-hoc-Datensatz festzulegen. Mit Query Service können Sie Datensatzspalten direkt über SQL mit dem Befehl `ALTER TABLE` entweder als primäre oder sekundäre Identitäten kennzeichnen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu den Funktionen von Query Service finden Sie in der [Übersicht zu Query Service](../../query-service/home.md).

<!--For more information on data governance in Query Service, see the [data governance overview](../../query-service/data-governance/overview.md).-->

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Attributbasierte Zugriffssteuerung in Quellen | Sie können jetzt den Zugriff auf einzelne Quellfelder und Attribute während der Erfassung verwalten und steuern. **Hinweis**: Die attribut-basierte Zugriffskontrolle ist derzeit in einer eingeschränkten Version für US-Kunden im Gesundheitswesen verfügbar. Diese Funktion steht allen Real-time Customer Data Platform-Kunden nach der vollständigen Veröffentlichung zur Verfügung. |
| Beta-Version der [!DNL Zendesk]-Quelle | Verwenden Sie die [!DNL Zendesk]-Quelle, um Benutzer-, Agenten- und Organisationsdaten aus Ihrer [!DNL Zendesk]-Instanz aufzunehmen, um [!DNL Profile] anzureichern. Informationen dazu finden Sie in der [[!DNL Zendesk] Übersicht zu Quellen](../../sources/connectors/customer-success/zendesk.md). |
| Allgemeine Verfügbarkeit von B2B [!DNL Microsoft Dynamics] source | Sie können jetzt die [!DNL Microsoft Dynamics] B2B-Objekte wie Konten, Chancen, Kampagnen, Marketinglisten und Mitglieder der Marketingliste aufnehmen. Informationen dazu finden Sie in der [[!DNL Microsoft Dynamics] Übersicht zu Quellen](../../sources/connectors/crm/ms-dynamics.md). |
| Unterstützung für die Adobe-Datenerfassung | Verwenden Sie den Quellenkatalog in Platform, um auf Ihre Daten in Platform Edge Network zuzugreifen, einschließlich der Datenvorbereitung für die Datenerfassung und der verbesserten Unterstützung für Datenvorbereitungs-Warnungen. Weitere Informationen erhalten Sie in der [Übersicht über die Adobe-Datenerfassungsquellen](../../sources/connectors/adobe-applications/data-collection.md). |
| Unterstützung für die Aufnahme von Dateien mit `ISO-8859-1`-Codierung | Verwenden Sie mithilfe der [!DNL Flow Service] API den `encoding`-Parameter zur Aufnahme von mit `ISO-8859-1` codierten Dateien von einer Cloud-Speicherquelle in Platform. Weitere Informationen finden Sie im Handbuch zum [Erstellen einer Cloud-Speicherplatz-Quellverbindung](../../sources/tutorials/api/collect/cloud-storage.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
