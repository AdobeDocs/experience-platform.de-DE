---
title: Adobe Experience Platform – Versionshinweise Juli 2024
description: Versionshinweise Juli 2024 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c38f6845a4819b648abacea2c36a576dac61f38f
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 23%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: Mittwoch, 30. Juli 2024**

Neue Funktionen in Adobe Experience Platform:

- [!BADGE Eingeschränkte Verfügbarkeit]{type=Informative}[Zusammengestellte Zielgruppenkomposition](#federated-audience-composition)

Aktualisierungen vorhandener Funktionen und Dokumentationen in Experience Platform:

- [Erweiterte Lebenszyklusverwaltung](#advanced-data-lifecycle-management)
- [Datenerfassung](#data-collection)
- [Data Governance](#data-governance)
- [Ziele](#destinations)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)
- [Einheitliche Tags](#unified-tags)

## Komposition föderierter Zielgruppen {#federated-audience-composition}

Zusammengestellte Zielgruppenkomposition ermöglicht es Unternehmen, Daten für eine bessere Anwendung in verschiedenen Anwendungsfällen zu erstellen. Mit diesem neuen Ansatz können Sie als Adobe Real-time Customer Data Platform- und/oder Adobe Journey Optimizer-Benutzer Datensätze direkt aus Ihrem vorhandenen Data Warehouse verbinden, um Adobe Experience Platform-Zielgruppen und -Attribute in einem System zu erstellen und anzureichern.

Weitere Informationen finden Sie in der Dokumentation zur Zusammenstellung von Federated Audience](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/home).[

## Erweiterte Lebenszyklusverwaltung {#advanced-data-lifecycle-management}

Experience Platform bietet eine Reihe von Funktionen zur Datenhygiene, mit denen Sie Ihre gespeicherten Daten durch programmatische Löschung von Verbraucherdatensätzen und -datensätzen verwalten können. Mithilfe des Arbeitsbereichs &quot;Datenlebenszyklus&quot;in der Benutzeroberfläche oder über Aufrufe der Data Hygiene API können Sie Ihre Datenspeicher effektiv verwalten. Verwenden Sie diese Funktionen, um sicherzustellen, dass Informationen erwartungsgemäß verwendet, aktualisiert werden, wenn falsche Datenanforderungen behoben werden müssen, und gelöscht wird, wenn organisatorische Richtlinien dies für erforderlich halten.

**Neue Dokumentation**

| Neue Dokumentation | Beschreibung |
| --- | --- |
| Referenz [!DNL Data Hygiene API] | Verwenden Sie die Data Hygiene API, um Ihre Datenspeicher in Experience Platform effektiv zu verwalten. Mit diesen Funktionen können Sie sicherstellen, dass Informationen erwartungsgemäß verwendet, bei Unrichtigkeit aktualisiert und gelöscht werden, wenn dies von Richtlinien der Organisation für erforderlich gehalten wird.<br><br>Lesen Sie das Referenzdokument zur Data Hygiene API](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/) , um detaillierte Informationen zur Verwendung der API zu erhalten. [ Sie können die Data Hygiene API verwenden, um Ablaufdaten für Datensätze zu planen, gespeicherte personenbezogene Daten von Kunden programmatisch zu korrigieren oder zu löschen und Ihre Datenhygienekosten zu überprüfen. Das API-Referenzdokument enthält die verfügbaren Endpunkte, Anfrageparameter und Antwortformate, mit denen Sie Ihre gespeicherten Kundendaten effizient verwalten können.</br></br> |

Weiterführende Informationen finden Sie in der [Übersicht über die erweiterte Lebenszyklusverwaltung](../../hygiene/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie clientseitige Kundenerlebnisdaten erfassen und an das Experience Platform-Edge Network senden können, wo sie angereichert, transformiert und an Adobe- oder Nicht-Adobe-Ziele verteilt werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Web SDK | Vorschlagsinteraktionen automatisch verfolgen | Sie können jetzt die Eigenschaft `autoTrackPropositionInteractionsEnabled` im Web SDK verwenden, um zu bestimmen, ob das Web SDK automatisch Vorschlagsinteraktionen erfassen soll. Detaillierte Informationen finden Sie in der Dokumentation zu [`autoTrackPropositionInteractionsEnabled`](../../web-sdk/commands/configure/autotrackpropositioninteractionsenabled.md) . |

{style="table-layout:auto"}

**Neue oder aktualisierte Dokumentation**

| Neue oder aktualisierte Dokumentation | Beschreibung |
| --- | --- |
| Neue API-Endpunkte für die Reactor-API dokumentiert | Endpunkte für die Nutzungsberechtigungen von Erweiterungspaketen finden Sie jetzt in der [Referenzdokumentation zur Reactor-API](https://developer.adobe.com/experience-platform-apis/references/reactor/) . Eigentümer von Erweiterungen können Paketberechtigungen für ein Erweiterungspaket mit diesen Endpunkten hinzufügen, entfernen und abrufen. |
| Neues Dokument zu Berechtigungen zur Verwendung von Erweiterungspaketen-Endpunkten | Eine Übersicht darüber, wie Inhaber von Erweiterungspaketen anderen Unternehmen die Verwendung ihrer privaten Versionen der Pakete in der Reactor-API gestatten können, finden Sie in der Dokumentation zu Endpunkten mit den Nutzungsberechtigungen für Erweiterungspakete](/help/tags/api/endpoints/extension-package-usage-authorizations.md) .[ |
| Handbuch zur Freigabe privater Erweiterungen | Die Verfahren zur Erstellung, Genehmigung und Löschung von Erweiterungspaketen der Reactor-API werden in der Dokumentation zur [Freigabe privater Erweiterungen](/help/tags/api/guides/extension-packages.md) beschrieben. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Datenerfassung - Übersicht](../../collection/home.md) .

## Data Governance {#data-governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in Experience Platform auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffskontrolle für Daten bei Marketing-Aktionen.

**Neue Funktion**

| Funktion | Beschreibung |
| --- | --- |
| mTLS Service API | Die [mTLS Service API](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/overview) soll die Sicherheit für den Datenaustausch verbessern. Verwenden Sie diese API, um die öffentlichen Zertifikate, die von Adobe für die Anwendungen Ihres Unternehmens ausgestellt wurden, sicher abzurufen. Diese Zertifikate stellen sicher, dass alle Nachrichten authentifiziert und verschlüsselt sind und zur externen Überprüfung der Authentizität von Zertifikaten verwendet werden können. Lesen Sie das [Handbuch zum öffentlichen Zertifikatendpunkt](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/public-certificate-endpoint) , um zu erfahren, wie Sie öffentliche Zertifikate für die Adobe-Anwendungen Ihres Unternehmens sicher abrufen können. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Übersicht zur Data Governance](../../data-governance/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele** {#new-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [(Beta) Merkury Enterprise Connections](/help/destinations/catalog/data-partners/merkury-enterprise-connections.md) | Verwenden Sie das Ziel [!DNL Merkury Enterprise Connections] , um sicher Zielgruppen für [!DNL Merkury] bereitzustellen. [!DNL Merkury] bietet Marketing-Experten eine einfache Abstimmung und Bereitstellung personalbasierter Zielgruppen an die 80+ Premium-adressierbaren TV-/CTV-, Herausgeber- und Ad-Tech-Verbindungen von [!DNL Merkury]. [!DNL Merkury] basiert auf einem umfassenden US-Identitätsdiagramm für erwachsene Verbraucher mit mehr als 268 Millionen Einwohnern. |
| [(Beta) Merkury Enterprise Identity](/help/destinations/catalog/data-partners/merkury-enterprise-identity.md) | Verwenden Sie das Ziel &quot;[!DNL Merkury Enterprise Identity]&quot;, um genauere, umfassendere und aufschlussreichere Verbraucherprofile zu erstellen. Dank verbesserter Profildaten können Marketingexperten bessere Einblicke, Segmente und Modelle erzielen und so ein präziseres Targeting und eine präzisere prädiktive Modellierung ermöglichen. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Überwachung des Datenflusses auf Zielgruppenebene | Die Überwachung Ihrer Datenflüsse, gruppiert nach Zielgruppen, war zuvor nur für Batch-Ziele (dateibasiert) verfügbar. Ab dieser Version ist die Überwachung auf Zielgruppenebene auch für das Streaming-Ziel [ (Beta) Google Customer Match + DV360 ](/help/destinations/catalog/advertising/google-customer-match-dv360.md) verfügbar. Lesen Sie mehr über die Überwachung auf Zielgruppenebene ](/help/dataflows/ui/monitor-destinations.md#segment-level-view) und wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, wenn Sie dem Betaprogramm beitreten möchten, um das Google-Kundenabgleich + DV360-Ziel zu verwenden.[ |
| Unterstützung von Anreicherungsattributen in Zielgruppen-Metadatenmakros für die Destination SDK | Sie können jetzt über dedizierte Makros auf Anreicherungsattribute in den [Destination SDK Audience Metadatenvorlagen](../../destinations/destination-sdk/functionality/audience-metadata-management.md) zugreifen. Anreicherungsattribute sind nur für [benutzerdefinierte Upload-Zielgruppen](../../destinations/destination-sdk/functionality/destination-configuration/schema-configuration.md#external-audiences) verfügbar. Informationen zur Funktionsweise der Anreicherungsattribut-Auswahl finden Sie im [Batch-Zielgruppenaktivierungshandbuch](../../destinations/ui/activate-batch-profile-destinations.md#select-enrichment-attributes) . Weitere Informationen finden Sie in der Audience-Vorlage [macros list](../../destinations/destination-sdk/functionality/audience-metadata-management.md#macros) . |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Zielübersicht](../../destinations/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue Dokumentation**

| Neue Dokumentation | Beschreibung |
| ----------------- | ----------- | 
| [Audience Portal](../../segmentation/ui/audience-portal.md) | Erfahren Sie, wie Sie mit Audience Portal Zielgruppen in Adobe Experience Platform zentral anzeigen, verwalten und erstellen können. |

{style="table-layout:auto"}

## Quellen

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen im Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern zu erfassen.

**Aktualisierte Dokumentation**

| Aktualisierte Dokumentation | Beschreibung |
| --- | --- |
| Erweitertes Authentifizierungshandbuch für [[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md) | Lesen Sie das erweiterte Authentifizierungshandbuch für [!DNL Snowflake] , um zu erfahren, wie Sie die [Kontokennung](../../sources/connectors/databases/snowflake.md#retrieve-your-account-identifier) und den [privaten Schlüssel](../../sources/connectors/databases/snowflake.md#retrieve-your-private-key) zur Authentifizierung abrufen. Darüber hinaus finden Sie im erweiterten Authentifizierungshandbuch Anweisungen zum [Überprüfen der Warehouse- und Rollenkonfigurationen](../../sources/connectors/databases/snowflake.md#verify-configurations). |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Quellenübersicht](../../sources/home.md).

## Einheitliche Tags

Mit Unified Tags können Sie Ihre Geschäftsobjekte in Adobe Experience Platform kategorisieren und verwalten. Mit der Unified Tags-API können Sie sowohl Ordner als auch Tags erstellen, um Platform-Objekte wie Zielgruppen oder Datensätze besser zu organisieren.

**Neue Dokumentation**

| Neue Dokumentation | Beschreibung |
| ----------------- | ----------- |
| [API-Handbuch für Unified Tags](../../administrative-tags/api/overview.md) | Lesen Sie das Handbuch zur Unified Tags API , um zu erfahren, wie Sie Ordner und Tags erstellen, um Ihre Geschäftsobjekte zu sortieren. |
| [API-Referenz für Unified Tags](https://developer.adobe.com/experience-platform-apis/references/unified-tags/) | Verwenden Sie die Referenz-API für Unified Tags , um die Endpunkte für Unified Tags interaktiv auszuprobieren. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Übersicht über Unified Tags](../../administrative-tags/overview.md) .
