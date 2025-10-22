---
keywords: Experience Platform;Datenspiegelung;relationales Schema;Datenerfassung ändern;Datenbanksynchronisierung;Primärschlüssel;Beziehungen
solution: Experience Platform
title: Übersicht über Data Mirror
description: Erfahren Sie, wie Data Mirror die Aufnahme von Änderungen auf Zeilenebene von externen Datenbanken in Adobe Experience Platform mithilfe von relationalen Schemata ermöglicht, die Eindeutigkeit, Beziehungen und Versionierung erzwingen.
badge: Eingeschränkte Verfügbarkeit
exl-id: bb92c77a-6c7a-47df-885a-794cf55811dd
source-git-commit: 57981d2e4306b2245ce0c1cdd9f696065c508a1d
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 1%

---

# Übersicht über Data Mirror

>[!AVAILABILITY]
>
>Data Mirror und relationale Schemata stehen Adobe Journey Optimizer-Lizenzinhabern **Orchestrierte Kampagnen** zur Verfügung. Sie sind auch als **eingeschränkte Version** für Customer Journey Analytics-Benutzer verfügbar, je nach Ihrer Lizenz und der Aktivierung von Funktionen. Wenden Sie sich an den Adobe-Support, um Zugang zu erhalten.

>[!NOTE]
>
>Relationale Schemata wurden in früheren Versionen der Adobe Experience Platform-Dokumentation zuvor als modellbasierte Schemata bezeichnet. Die Funktionalität bleibt gleich.

Data Mirror ist eine Adobe Experience Platform-Funktion, die die Aufnahme von Änderungen auf Zeilenebene aus externen Datenbanken in den Data Lake mithilfe relationaler Schemata ermöglicht. Sie behält Datenbeziehungen bei, erzwingt Eindeutigkeit und unterstützt die Versionierung, ohne dass vorgelagerte ETL-Prozesse (Extract, Transform, Load) erforderlich sind.

Verwenden Sie Data Mirror, um Einfügungen, Aktualisierungen und Löschungen (veränderliche Daten) aus externen Systemen wie [!DNL Snowflake], [!DNL Databricks] oder [!DNL BigQuery] direkt in Experience Platform zu synchronisieren. Auf diese Weise können Sie beim Importieren von Daten in Platform die Struktur Ihres vorhandenen Datenbankmodells und die Datenintegrität beibehalten.

## Funktionen und Vorteile

Data Mirror bietet die folgenden grundlegenden Funktionen für die Datenbanksynchronisierung:

* **Primäre Durchsetzung von Schlüsseln**: Stellt Eindeutigkeit innerhalb von Datensätzen sicher und verhindert doppelte Datensätze bei der Aufnahme.
* **Änderungsaufnahme auf Zeilenebene**: Unterstützt granulare Datenänderungen, einschließlich Upserts und Löschungen, mit Präzisionssteuerung.
* **Schemabeziehungen**: Aktiviert mithilfe von Deskriptoren Fremd- und Primärschlüsselbeziehungen zwischen Datensätzen.
* **Ereignisverarbeitung außerhalb der Reihenfolge**: Verarbeitet Änderungsereignisse mithilfe von Versions- und Zeitstempeldeskriptoren, auch wenn sie nicht in der Reihenfolge eintreffen.
* **Direct Warehouse-Integration**: Stellt eine Verbindung zu unterstützten Cloud-Data-Warehouses her, um eine nahezu in Echtzeit stattfindende Synchronisierung von Änderungen zu ermöglichen.

Verwenden Sie Data Mirror, um Änderungen direkt aus Ihren Quellsystemen aufzunehmen, die Schemaintegrität durchzusetzen und die Daten für Analysen, Journey-Orchestrierung und Compliance-Workflows verfügbar zu machen. Data Mirror eliminiert komplexe vorgelagerte ETL-Prozesse und beschleunigt die Implementierung durch die Möglichkeit der direkten Spiegelung vorhandener Datenbankmodelle.

Planen Sie beim Implementieren relationaler Schemata mit Data Mirror die Anforderungen für das Löschen und die Datenhygiene. Alle Programme müssen vor der Bereitstellung berücksichtigen, wie sich Löschungen auf zugehörige Datensätze, Compliance-Workflows und nachgelagerte Prozesse auswirken.

## Voraussetzungen {#prerequisites}

Bevor Sie beginnen, sollten Sie die folgenden Komponenten von Experience Platform verstehen und sicherstellen, dass Ihre Umgebung die technischen und strukturellen Anforderungen erfüllt:

* [Erstellen von Schemata in der Experience Platform-](../ui/resources/schemas.md) oder [API](../api/schemas.md)
* [Konfigurieren von Cloud-Quellverbindungen](../../sources/home.md#cloud-storage)
* [Change Data Capture-Konzepte anwenden](../../sources/tutorials/api/change-data-capture.md) (Upserts, Löschvorgänge)
* Unterscheiden zwischen [Standard](../schema/composition.md) und [relationalen Schemata](../schema/relational.md)
* [Definieren struktureller Beziehungen mit Deskriptoren](../api/descriptors.md)

### Implementierungsanforderungen

Ihre Platform-Instanz und Quelldaten müssen bestimmte Anforderungen erfüllen, damit Data Mirror ordnungsgemäß funktioniert. Data Mirror erfordert **relationale Schemata** die flexible Datenstrukturen mit erzwungenen Einschränkungen sind.

Fügen Sie **Schema einen** Primärschlüssel und Versionsdeskriptor) hinzu. Wenn Sie mit einem Zeitreihenschema arbeiten, ist **ein &quot;**&quot; erforderlich.

Ihre externe Datenbank muss die Änderungsdatenerfassung unterstützen oder Metadaten bereitstellen, mit denen Einfügungen, Aktualisierungen und Löschungen identifiziert werden können. Source-Daten müssen **eindeutige Kennungen** entweder ein einzelnes Feld oder einen zusammengesetzten Primärschlüssel und **Versionsinformationen** enthalten, damit das System Aktualisierungen in der richtigen Reihenfolge anwenden kann.

Um Löschvorgänge zu erkennen, fügen Sie eine `_change_request_type` Spalte hinzu, die angibt, ob es sich bei jedem Datensatz um eine Upsert- oder eine Löschfunktion handelt.

## Implementieren von Data Mirror {#implementation-workflow}

Im Gegensatz zu standardmäßigen Aufnahmeansätzen behält Data Mirror Ihre Datenbankmodellstruktur im Data Lake von Experience Platform bei. Durch diese Konsistenz der Datenstruktur entfällt die Notwendigkeit für eine externe Vorverarbeitung. Im Folgenden finden Sie einen allgemeinen Implementierungs-Workflow für Data Mirror. Wählen Sie Ihre Implementierungsmethode basierend auf dem Workflow und dem Quellsystem Ihres Teams aus.

### Definieren der Schemastruktur

Erstellen Sie [relationale Schemata](../schema/relational.md) mit erforderlichen Deskriptoren (Metadaten, die das Schemaverhalten und die Einschränkungen definieren). Wählen Sie entweder über die Benutzeroberfläche oder direkt über die API eine Methode aus, die zum Workflow Ihres Teams passt.

* **UI-Ansatz**: [Erstellen relationaler Schemata im Schema-Editor](../ui/resources/schemas.md#create-relational-schema)
* **API-Ansatz**: [Erstellen von Schemata über die Schema Registry-API](../api/schemas.md#create-relational-schema)

### Zuordnen von Beziehungen und Definieren des Daten-Managements

Definieren von Verbindungen zwischen Datensätzen mithilfe von Beziehungsdeskriptoren. Verwalten Sie Beziehungen und behalten Sie die Datenqualität in allen Datensätzen bei. Diese Aufgaben stellen konsistente Joins sicher und unterstützen die Einhaltung von Datenhygiene-Anforderungen.

* **Schemabeziehungen**: [Definieren von Beziehungen zwischen Datensätzen mithilfe von Deskriptoren](../api/descriptors.md)
* **Datensatzhygiene**: [Verwalten von Präzisionsdatensatzlöschungen für Datensätze, die auf relationalen Schemata basieren](../../hygiene/ui/record-delete.md#relational-record-delete)

### Konfigurieren der Quellverbindung

Wählen Sie eine Aufnahmemethode basierend auf Ihrem Quellsystem und Ihrem Anwendungsfall aus. Jede Option unterstützt verschiedene Ebenen der Automatisierung, Transformation und Skalierbarkeit.

* [**Konfigurieren von Cloud-Quellverbindungen**](../../sources/home.md#cloud-storage)
* **SQL-Aufnahme**: Verwenden von Data Distiller zum Schreiben in relationale Datensätze
* [**Datei-Upload**](../ui/resources/schemas.md#upload-ddl-file): Manuelles Hochladen von Dateien für die Batch- oder einmalige Aufnahme

### Aufnahme von Änderungsdaten aktivieren

Einrichten von Verbindungen zur Datenerfassung für Änderungen mit unterstützten Cloud-Data-Warehouses. Nehmen Sie Änderungen auf Zeilenebene auf, während Sie die Eindeutigkeit beibehalten und Aktualisierungen in der richtigen Reihenfolge anwenden.

* **Datenerfassung ändern**: [Aktivieren der Datenerfassung für Änderungen in Quellverbindungen](../../sources/tutorials/api/change-data-capture.md)

## Häufige Anwendungsfälle {#use-cases}

Gehen Sie die unten aufgeführten gängigen Anwendungsfälle durch, in denen Data Mirror eine präzise Datensynchronisation und die Beibehaltung von Beziehungen unterstützt. Jedes Szenario zeigt, wie Data Mirror gängige Geschäftsanforderungen für Analysen, Orchestrierung und Compliance unterstützt.

### Relationale Datenmodellierung

Verwenden Sie [relationale Schemata](../schema/relational.md) in Data Mirror, um Entitäten darzustellen, Einfügungen, Aktualisierungen und Löschungen auf Zeilenebene zu verarbeiten und die in Ihren Datenquellen vorhandenen Primär- und Fremdschlüsselbeziehungen zu pflegen. Dieser Ansatz bringt relationale Datenmodellierungsprinzipien in Experience Platform ein und stellt die strukturelle Konsistenz über alle Datensätze hinweg sicher.

### Synchronisierung von Warehouse zu Lake

Spiegeln von Ereignisdaten, Kundeninteraktionsprotokollen, Kampagnenereignissen und Zusatzdaten aus unterstützten Cloud-Data-Warehouses in Experience Platform. Dies unterstützt die Kampagneneignung, die Zielgruppenpräzision und die Nachrichtensequenzierung. Journey Optimizer und Real-Time CDP B2B nutzen dies für nahezu in Echtzeit ausgeführte Orchestrierungslogik.

### Customer Journey Analytics-Integration

Synchronisieren Sie Zeitreihenereignisse wie Web-Klicks, Produktansichten, Käufe und Support-Interaktionen von Systemen wie Callcentern oder Chat-Protokollen. Ein vollständiger Änderungsverlauf unterstützt eine genaue Trendanalyse und Verhaltenssegmentierung. Experience Platform Data Mirror für Customer Journey Analytics verwendet dies, um Upserts und Löschvorgänge aus Quellsystemen widerzuspiegeln.

### B2B-Beziehungsmodellierung

Beziehungen wie Konto-zu-Kontakt-, Abonnement-zu-Konto- oder Kontakt-zu-Region-Hierarchien beibehalten. Diese unterstützen die Segmentierung, Lead-Bewertung, Opportunity-Tracking und Multi-Channel-Koordination. Im Gegensatz zur Standardaufnahme, die Beziehungen reduziert, verwaltet Data Mirror sie nativ mithilfe von Deskriptoren für eine genauere Modellierung.

### Abonnementverwaltung

Verfolgen Sie Ereignisse wie Verlängerungen, Stornierungen, Upgrades, Downgrades und Planänderungen mit vollständigem Versionsverlauf. Dies unterstützt Aufbewahrungskampagnen, Abwanderungsprognosen und lebenszyklusbasierte Segmentierung. Der vollständige Verlauf ermöglicht verhaltensbezogene Einblicke und präzises Targeting.

### Datenhygienevorgänge

Verwenden Sie die Änderungsdatenerfassung, um präzise Löschungen auf Datensatzebene für Compliance-Zwecke (z. B. regulierte Branchen) und Bereinigungs-Workflows zu ermöglichen. Data Mirror wendet Löschungen präzise an und behält gleichzeitig die zugehörigen Daten in allen verbundenen Datensätzen bei.

## Wichtige Überlegungen {#considerations}

Überprüfen Sie diese wichtigen Überlegungen, um sicherzustellen, dass Ihre Implementierung mit unterstützten Schemaverhaltensweisen, Aufnahmemethoden und Beziehungsmustern übereinstimmt. Eine ordnungsgemäße Planung hilft, Integrationsprobleme zu vermeiden, und stellt eine genaue Datenmodellierung sicher.

### Datenlöschung und Hygieneanforderungen

Alle Programme, die relationale Schemata und Data Mirror verwenden, müssen mit den Auswirkungen des Löschens von Daten vertraut sein. Relationale Schemata ermöglichen präzise Löschvorgänge auf Datensatzebene, die sich auf verknüpfte Daten in verbundenen Datensätzen auswirken können. Diese Löschfunktionen wirken sich unabhängig von Ihrem spezifischen Anwendungsfall auf die Datenintegrität, die Compliance und das nachgelagerte Anwendungsverhalten aus. Überprüfen Sie [Datenhygiene-Anforderungen für Datensätze, die auf relationalen Schemata &#x200B;](../../hygiene/ui/record-delete.md#relational-record-delete), und planen Sie Löschszenarien vor der Implementierung.

### Auswahl des Schemaverhaltens

Relationale Schemata verwenden standardmäßig **Datensatzverhalten** das den Entitätsstatus erfasst (Kunden, Konten usw.). Wenn Sie **Zeitreihenverhalten** für die Ereignisverfolgung benötigen, müssen Sie dies explizit konfigurieren.

### Vergleich der Aufnahmemethoden

Verwenden Sie diese Vergleichstabelle, um die beste Aufnahmemethode für Ihre Datenanforderungen auszuwählen, unabhängig davon, ob Sie eine Echtzeit-Synchronisierung, eine SQL-basierte Transformation oder manuelle Datei-Uploads benötigen.

| Aufnahmemethode | Anwendungsfall |
| ----------------------- | -------------------------------------------------------------- |
| **Datenerfassung ändern** | Echtzeit-Synchronisierung aus unterstützten Cloud-Warehouses |
| **Daten-Distiller** | SQL-basierte Aufnahme- und Umwandlungs-Workflows |
| **Datei-Upload** | Batch-/manuelle Aufnahme, wenn keine Quellintegration verfügbar ist |

### Einschränkungen von Beziehungen

Data Mirror unterstützt **Eins-zu-eins** und **Viele-zu-eins**-Beziehungen mit Deskriptoren. **Viele-zu-viele**-Beziehungen erfordern eine zusätzliche Modellierung und werden nicht direkt unterstützt.

## Nächste Schritte

Nachdem Sie diese Übersicht gelesen haben, sollten Sie in der Lage sein, festzustellen, ob Data Mirror zu Ihrem Anwendungsfall passt, und die Anforderungen für die Implementierung zu verstehen. Erste Schritte:

1. **Datenarchitekten** sollten Ihr Datenmodell bewerten, um sicherzustellen, dass es Primärschlüssel, Versionierung und Änderungsverfolgungsfunktionen unterstützt.
2. **Stakeholder** sollten bestätigen, dass Ihre Lizenz relationale Schemaunterstützung und erforderliche Experience Platform-Editionen enthält.
3. **Schema-Designer** sollten Ihre Schemastruktur planen, um die erforderlichen Deskriptoren, Feldbeziehungen und Data Governance-Anforderungen zu identifizieren.
4. **Implementierungs-Teams** sollten eine Aufnahmemethode basierend auf Ihren Quellsystemen, Echtzeitanforderungen und operativen Workflows auswählen.

Details zur Implementierung finden Sie in der [Dokumentation zu relationalen Schemata](../schema/relational.md).
