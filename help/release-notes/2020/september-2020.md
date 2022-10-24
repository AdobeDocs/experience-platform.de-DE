---
title: Adobe Experience Platform - Versionshinweise - September 2020
description: Die Versionshinweise für Adobe Experience Platform vom September 2020.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 38%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 9. September 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Data Governance](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Data Governance {#governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffssteuerung für Daten bei Marketing-Aktionen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbesserungen der Benutzeroberfläche für die Kennzeichnung von Datensätzen | Zur Benutzeroberfläche für die Kennzeichnung von Datensätzen wurden mehrere neue Sortier- und Filtersteuerelemente hinzugefügt, um die Arbeit mit großen Schemas zu vereinfachen: <ul><li>Sortieren Sie die Felder nach alphabetischer Reihenfolge basierend auf dem vollständigen Schemapfad.</li><li>Teilsuche nach Feldpfadnamen durchführen.</li><li>Filtern Sie Felder ohne Beschriftungen, mit einer ausgewählten Beschriftung oder mit einer Beschriftungskategorie.</li></ul> |

Weitere Informationen zu dem Service finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md).

## Ziele {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner nahtlos aktivieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| UX-Verbesserungen | Benutzer können auf Inline-Tabellenaktionen zugreifen, um den Zugriff auf primäre Aktionen wie das Hinzufügen von Daten, die Bearbeitung der Planung und das Hinzufügen von Segmenten zu erleichtern. Siehe [Zielarbeitsbereich](../../destinations/ui/destinations-workspace.md) für weitere Informationen. |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] ermöglicht Ihnen die Überwachung von Aktivitäten in Adobe Experience Platform mithilfe statistischer Metriken und Ereignisbenachrichtigungen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Adobe I/O-Ereignisbenachrichtigungen | [!DNL Observability Insights] nutzt Adobe I/O-Ereignisse , um Ereignisbenachrichtigungen für mehrere Experience Platform-Dienste zu erstellen. Benachrichtigungs-Payloads werden an einen konfigurierten Webhook gesendet, mit dem Sie dann weitere nachgelagerte Prozesse automatisieren können. |

Weitere Informationen zu dem Service finden Sie in der [[!DNL Observability Insights] Übersicht zu ](../../observability/home.md).

## [!DNL Privacy Service] {#privacy}

Verschiedene Rechts- und Verwaltungsvorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten aus Ihren Datenspeichern zuzugreifen oder diese zu löschen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie diese Datenanforderungen Ihrer Kunden verwalten können. Mit [!DNL Privacy Service]können Sie Anfragen zum Zugriff auf und zur Löschung von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, was die automatische Einhaltung gesetzlicher und organisatorischer Datenschutzbestimmungen erleichtert.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für LGPD (Brasilien) | Datenschutzaufträge können jetzt im Rahmen der [!DNL Lei Geral de Proteção de Dados] Verordnung (LGPD). Diese Aufträge werden unter dem Regelungscode nachverfolgt `lgpd_bra`. |

Siehe [Übersicht über Privacy Service](../../privacy-service/home.md) für weitere Informationen zum Dienst.

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Mit [!DNL Real-time Customer Profile]können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden anzeigen, die Daten aus mehreren Kanälen kombiniert, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten in einer einheitlichen Ansicht zusammenzufassen, die eine umsetzbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Profilansicht | Der Profil-Viewer in der Platform-Benutzeroberfläche wurde aktualisiert und ist jetzt ein Dashboard mit vollständiger Anpassung. Der Benutzer hat jetzt die Möglichkeit, die folgenden Aufgaben auszuführen: <ul><li>Aktualisieren Sie die ausgewählten standardmäßigen und benutzerdefinierten Attribute im Widget für grundlegende Informationen.</li><li>Erstellen, Bearbeiten und Entfernen benutzerdefinierter Widgets</li><li>Größe von Widgets ändern und neu anordnen</li></ul> |

Weitere Informationen finden Sie unter [!DNL Real-time Customer Profile], einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile] Daten lesen Sie bitte die [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren [!DNL Real-time Customer Profile]-Daten Zielgruppen generieren können. Diese Segmente werden zentral in [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Exportaufträge | Es wurde ein Flag hinzugefügt, mit dem Segmente im Rahmen eines Exportvorgangs ausgewertet werden können. Daher können Benutzer sowohl die Segmentierung als auch Exporte in einem einzigen Auftrag ausführen. |
| Zusammenführungsrichtlinien | In einem einzelnen Batch-Segmentierungsauftrag können mehrere Zusammenführungsrichtlinien enthalten sein. |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md)

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten strukturieren, beschriften und erweitern, indem es [!DNL Platform] Dienste. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatische Zuordnung | [!DNL Platform] bietet intelligente Empfehlungen für die automatische Zuordnung während des Datenerfassungs-Workflows, basierend auf einem vom Benutzer ausgewählten Zielschema oder Datensatz. Sie können flexible Regeln für die automatische Zuordnung manuell an Ihre Anwendungsfälle anpassen. |
| UX-Verbesserungen | Benutzer können auf Inline-Tabellenaktionen zugreifen, um den Zugriff auf primäre Aktionen wie das Hinzufügen von Daten, die Bearbeitung der Planung und das Hinzufügen von Segmenten zu erleichtern. Siehe [Überwachen von Datenflüssen](../../sources/tutorials/ui/monitor.md) für weitere Informationen. |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
