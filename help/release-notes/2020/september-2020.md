---
title: Adobe Experience Platform – Versionshinweise, September 2020
description: Versionshinweise September 2020 zu Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 38%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Donnerstag, 9. September 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Data Governance](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Data Governance {#governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffssteuerung für Daten bei Marketing-Aktionen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbesserungen der Benutzeroberfläche für Datensatzbeschriftungen | Mehrere neue Sortierungs- und Filtersteuerelemente wurden der Benutzeroberfläche für die Datensatzbeschriftung hinzugefügt, um die Arbeit mit großen Schemata zu erleichtern: <ul><li>Sortieren Sie Felder nach alphabetischer Reihenfolge basierend auf dem vollständigen Schemapfad.</li><li>Führen Sie eine Teilsuche nach Feldpfadnamen durch.</li><li>Filtern Sie Felder ohne Kennzeichnungen, ausgewählte Kennzeichnungen oder eine Kennzeichnungskategorie.</li></ul> |

Weitere Informationen zu dem Service finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md).

## Ziele {#destinations}

In [Real-Time Customer Data Platform](../../rtcdp/overview.md) sind Ziele vorgefertigte Integrationen mit Zielplattformen, die Daten nahtlos für diese Partner aktivieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| UX-Verbesserungen | Benutzer können auf Inline-Tabellenaktionen zugreifen, um den Zugriff auf primäre Aktionen zu erleichtern, z. B. das Hinzufügen von Daten, das Bearbeiten von Zeitplänen und das Hinzufügen von Segmenten. Weitere Informationen finden [ im Dokument ](../../destinations/ui/destinations-workspace.md)Arbeitsbereich“. |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

Mit [!DNL Observability Insights] können Sie Aktivitäten in Adobe Experience Platform mithilfe von statistischen Metriken und Ereignisbenachrichtigungen überwachen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Adobe I/O-Ereignisbenachrichtigungen | [!DNL Observability Insights] nutzt Adobe I/O Events zum Erstellen von Ereignisbenachrichtigungen für mehrere Experience Platform-Services. Benachrichtigungs-Payloads werden an einen konfigurierten Webhook gesendet, mit dem Sie dann weitere nachgelagerte Prozesse automatisieren können. |

Weitere Informationen [[!DNL Observability Insights]  Service finden ](../../observability/home.md) in der Übersicht .

## [!DNL Privacy Service] {#privacy}

Verschiedene gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen oder sie aus Ihren Datenspeichern zu löschen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung dieser Datenanfragen Ihrer Kunden unterstützen. Mit [!DNL Privacy Service] können Sie Anfragen für den Zugriff auf und die Löschung von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Programmen stellen, was die automatische Einhaltung gesetzlicher und unternehmensinterner Datenschutzbestimmungen erleichtert.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für LGPD (Brasilien) | Datenschutzaufträge können jetzt im Rahmen der [!DNL Lei Geral de Proteção de Dados] (LGPD)-Verordnung erstellt werden. Diese Aufträge werden unter dem Regulierungs-Code `lgpd_bra` verfolgt. |

Weitere Informationen zu dem Service finden Sie in ](../../privacy-service/home.md) [Übersicht über Privacy Service .

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das [!DNL Real-Time Customer Profile] ermöglicht eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. [!DNL Profile] können Sie Ihre unterschiedlichen Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Profilansicht | Der Profil-Viewer in der Experience Platform-Benutzeroberfläche wurde zu einem Dashboard mit vollständiger Anpassung aktualisiert. Der Benutzer hat jetzt die Möglichkeit, die folgenden Aufgaben auszuführen: <ul><li>Aktualisieren Sie die ausgewählten Standard- und benutzerdefinierten Attribute im Widget „Grundlegende Informationen“.</li><li>Erstellen, Bearbeiten und Entfernen benutzerdefinierter Widgets</li><li>Größe von Widgets ändern und neu anordnen</li></ul> |

Weitere Informationen zu [!DNL Real-Time Customer Profile], einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile]-Daten, finden [ in der Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen generieren können. Diese Segmente werden zentral in [!DNL Experience Platform] konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Exportaufträge | Es wurde eine Markierung hinzugefügt, mit der Segmente als Teil eines Exportvorgangs bewertet werden können. Daher können Benutzer sowohl die Segmentierung als auch die Exporte in einem einzigen Auftrag ausführen. |
| Zusammenführungsrichtlinien | Ein einzelner Batch-Segmentierungsauftrag kann mehrere Zusammenführungsrichtlinien enthalten. |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierung - Übersicht](../../segmentation/home.md)

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatische Zuordnung | [!DNL Experience Platform] bietet intelligente Empfehlungen für die automatische Zuordnung während des Workflows der Datenaufnahme, basierend auf einem vom Benutzer ausgewählten Zielschema oder Datensatz. Sie können flexible automatische Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. |
| UX-Verbesserungen | Benutzer können auf Inline-Tabellenaktionen zugreifen, um den Zugriff auf primäre Aktionen wie das Hinzufügen von Daten, das Bearbeiten von Zeitplänen und das Hinzufügen von Segmenten zu erleichtern. Weitere Informationen finden [ im Dokument ](../../sources/tutorials/ui/monitor.md)Überwachen von Datenflüssen“. |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
