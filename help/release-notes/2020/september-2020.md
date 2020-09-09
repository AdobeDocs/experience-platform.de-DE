---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform vom 9. September 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 64b6b59923d549cdcbf35d2e375529aec8cf81b8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 41%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 9. September 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [[!DNL-Datenverwaltung]](#governance)
* [[!DNL-Ziele]](#destinations)
* [[!DNL-Quellen]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen der Benutzeroberfläche für die Datenbeschriftung | Zur Vereinfachung der Arbeit mit großen Schemas wurden der Benutzeroberfläche für die Datenbeschriftung mehrere neue Steuerelemente zum Sortieren und Filtern hinzugefügt: <ul><li>Sortieren Sie die Schemas in alphabetischer Reihenfolge nach dem vollständigen Pfad.</li><li>Führen Sie Teilsuchen nach Feldpfadnamen durch.</li><li>Filtern Sie Felder ohne Beschriftungen, mit einer ausgewählten Beschriftung oder mit einer Beschriftung.</li></ul> |

Weitere Informationen zum Dienst finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md) .

## Ziele {#destinations}

In der [Adobe Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| UX-Verbesserungen | Benutzer können auf Aktionen für Inline-Tabellen zugreifen, um den Zugriff auf primäre Aktionen wie das Hinzufügen von Daten, das Bearbeiten von Zeitplänen und das Hinzufügen von Segmenten zu vereinfachen. See the [destinations workspace](../../rtcdp/destinations/destinations-workspace.md) document for more information. |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../rtcdp/destinations/destinations-overview.md)

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatische Zuordnung | [!DNL Platform] bietet intelligente Empfehlungen für die automatische Zuordnung während des Datenerfassungs-Workflows, basierend auf einem benutzerspezifischen Zielgruppe-Schema oder einem Datensatz. Sie können flexible Regeln für die automatische Zuordnung manuell an Ihre Anwendungsfälle anpassen. |
| UX-Verbesserungen | Benutzer können auf Aktionen für Inline-Tabellen zugreifen, um den Zugriff auf primäre Aktionen wie das Hinzufügen von Daten, das Bearbeiten von Zeitplänen und das Hinzufügen von Segmenten zu vereinfachen. Weitere Informationen finden Sie im Dokument [zum Überwachen von Datenflüssen](../../sources/tutorials/ui/monitor.md) . |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).