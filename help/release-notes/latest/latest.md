---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform vom 9. September 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 312794af2cdb111fb81c0aa226dec68db2cbc374
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 28%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 9. September 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL-Datenverwaltung]](#governance)
- [[!DNL-Ziele]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL-Privacy Service]](#privacy)
- [[!DNL Echtzeit-Profil des Kunden]](#profile)
- [[!DNL-Segmentierungsdienst]](#segmentation)
- [[!DNL-Quellen]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbesserungen der Benutzeroberfläche für die Datenbeschriftung | Zur Vereinfachung der Arbeit mit großen Schemas wurden der Benutzeroberfläche für die Datenbeschriftung mehrere neue Steuerelemente zum Sortieren und Filtern hinzugefügt: <ul><li>Sortieren Sie die Schemas in alphabetischer Reihenfolge nach dem vollständigen Pfad.</li><li>Führen Sie Teilsuchen nach Feldpfadnamen durch.</li><li>Filtern Sie Felder ohne Beschriftungen, mit einer ausgewählten Beschriftung oder mit einer Beschriftung.</li></ul> |

Weitere Informationen zum Dienst finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md) .

## Ziele {#destinations}

In der [Adobe Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| UX-Verbesserungen | Benutzer können auf Aktionen für Inline-Tabellen zugreifen, um den Zugriff auf primäre Aktionen wie das Hinzufügen von Daten, das Bearbeiten von Zeitplänen und das Hinzufügen von Segmenten zu vereinfachen. See the [destinations workspace](../../rtcdp/destinations/destinations-workspace.md) document for more information. |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] ermöglicht Ihnen die Überwachung von Aktivitäten auf Adobe Experience Platform mithilfe von statistischen Metriken und Ereignis-Benachrichtigungen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| E/A-Ereignis-Benachrichtigungen der Adobe | [!DNL Observability Insights] nutzt Adobe-I/O-Ereignis, um Ereignis-Benachrichtigungen für mehrere Experience Platformen-Services zu erstellen. Benachrichtigungs-Nutzdaten werden an einen konfigurierten Webhop gesendet, mit dem Sie dann weitere nachgelagerte Prozesse automatisieren können. See the [notifications overview](../../observability/notifications/overview.md) for more information. |

Weitere Informationen zum Dienst finden Sie in der [[!DNL Observability Insights] Übersicht](../../observability/home.md) .

## [!DNL Privacy Service] {#privacy}

Verschiedene Rechts- und Verwaltungsvorschriften geben den Nutzern das Recht, auf ihre personenbezogenen Daten von Ihren Datenspeichern auf Anfrage zuzugreifen oder sie zu löschen. Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface to help you manage these data requests from your customers. With [!DNL Privacy Service], you can submit requests to access and delete private or personal customer data from Adobe Experience Cloud applications, facilitating automated compliance with legal and organizational privacy regulations.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für LGPD (Brasilien) | Datenschutzaufträge können nun im Rahmen der brasilianischen [!DNL Lei Geral de Proteção de Dados] (LGPD-)Verordnung geschaffen werden. Diese Aufträge werden unter dem Regelungskodex nachverfolgt `lgpd_bra`. |

Weitere Informationen zum Dienst finden Sie in der Übersicht über den [Privacy Service](../../privacy-service/home.md) .

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Profilansicht | Der Profil-Viewer in der Plattform-Benutzeroberfläche wurde aktualisiert, um ein Dashboard mit vollständiger Anpassung zu sein. Der Benutzer hat jetzt die Möglichkeit, die folgenden Aufgaben auszuführen: <ul><li>Aktualisieren Sie die ausgewählten Standard- und benutzerdefinierten Attribute im Widget &quot;Grundlegende Informationen&quot;.</li><li>Benutzerdefinierte Widgets erstellen, bearbeiten und entfernen</li><li>Widgets anpassen und neu anordnen</li></ul> |

Weitere Informationen [!DNL Real-time Customer Profile]einschließlich Übungen und Best Practices für die Arbeit mit [!DNL Profile] Daten finden Sie in der Übersicht über das [Echtzeit-Kundenerlebnis](../../profile/home.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], making them readily accessible by any Adobe application.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Exportaufträge | Es wurde ein Flag hinzugefügt, damit Segmente im Rahmen eines Exportauftrags ausgewertet werden können. Daher können Benutzer sowohl die Segmentierung als auch Exporte in einem einzigen Auftrag ausführen. |
| Zusammenführungsrichtlinien | Mehrere Zusammenführungsrichtlinien können in einem einzelnen Stapelsegmentierungsauftrag enthalten sein. |

For more information on [!DNL Segmentation Service], please see the [Segmentation overview](../../segmentation/home.md)

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatische Zuordnung | [!DNL Platform] bietet intelligente Empfehlungen für die automatische Zuordnung während des Datenerfassungs-Workflows, basierend auf einem benutzerspezifischen Zielgruppe-Schema oder einem Datensatz. Sie können flexible Regeln für die automatische Zuordnung manuell an Ihre Anwendungsfälle anpassen. |
| UX-Verbesserungen | Benutzer können auf Aktionen für Inline-Tabellen zugreifen, um den Zugriff auf primäre Aktionen wie das Hinzufügen von Daten, das Bearbeiten von Zeitplänen und das Hinzufügen von Segmenten zu vereinfachen. Weitere Informationen finden Sie im Dokument [zum Überwachen von Datenflüssen](../../sources/tutorials/ui/monitor.md) . |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
