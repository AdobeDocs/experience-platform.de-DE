---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform vom 9. September 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 30%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: 9. September 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Governance]](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Es spielt eine Schlüsselrolle innerhalb von [!DNL Experience Platform] auf verschiedenen Ebenen, einschließlich Katalogisierung, Datenbindung, Datenbeschriftung, Datenzugriffsrichtlinien und Zugriffskontrolle von Daten für Marketingaktionen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbesserungen der Benutzeroberfläche für die Datenbeschriftung | Zur Vereinfachung der Arbeit mit großen Schemas wurden der Benutzeroberfläche für die Datenbeschriftung mehrere neue Steuerelemente zum Sortieren und Filtern hinzugefügt: <ul><li>Sortieren Sie die Schemas in alphabetischer Reihenfolge nach dem vollständigen Pfad.</li><li>Führen Sie Teilsuchen nach Feldpfadnamen durch.</li><li>Filtern Sie Felder ohne Beschriftungen, mit einer ausgewählten Beschriftung oder mit einer Beschriftung.</li></ul> |

Weitere Informationen zum Dienst finden Sie unter [Übersicht über die Datenverwaltung](../../data-governance/home.md).

## Ziele {#destinations}

In der [ Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| UX-Verbesserungen | Benutzer können auf Aktionen für Inline-Tabellen zugreifen, um den Zugriff auf primäre Aktionen wie das Hinzufügen von Daten, das Bearbeiten von Zeitplänen und das Hinzufügen von Segmenten zu vereinfachen. Weitere Informationen finden Sie im Dokument [Ziel-Arbeitsbereich](../../destinations/ui/destinations-workspace.md). |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] ermöglicht Ihnen die Überwachung von Aktivitäten auf Adobe Experience Platform mithilfe von statistischen Metriken und Ereignis-Benachrichtigungen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Adobe I/O-Ereignis-Benachrichtigungen | [!DNL Observability Insights] nutzt Adobe I/O-Ereignis, um Ereignis-Benachrichtigungen für verschiedene Experience Platformen-Services zu erstellen. Benachrichtigungs-Nutzdaten werden an einen konfigurierten Webhop gesendet, mit dem Sie dann weitere nachgelagerte Prozesse automatisieren können. Weitere Informationen finden Sie unter [Benachrichtigungsübersicht](../../observability/notifications/overview.md). |

Weitere Informationen zum Dienst finden Sie unter [[!DNL Observability Insights] overview](../../observability/home.md).

## [!DNL Privacy Service] {#privacy}

Verschiedene Rechts- und Verwaltungsvorschriften geben den Nutzern das Recht, auf ihre personenbezogenen Daten von Ihren Datenspeichern auf Anfrage zuzugreifen oder sie zu löschen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung dieser Datenanforderungen von Ihren Kunden unterstützen. Mit [!DNL Privacy Service] können Sie Anfragen zum Zugriff und Löschen von persönlichen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für LGPD (Brasilien) | Datenschutzaufträge können nun unter Brasiliens [!DNL Lei Geral de Proteção de Dados]-Verordnung (LGPD) erstellt werden. Diese Aufträge werden unter dem Regelcode `lgpd_bra` verfolgt. |

Weitere Informationen zum Dienst finden Sie unter [Übersicht über Privacy Service](../../privacy-service/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Mit [!DNL Real-time Customer Profile] können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden sehen, die Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombiniert. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Profilansicht | Der Profil-Viewer in der Plattform-Benutzeroberfläche wurde aktualisiert, um ein Dashboard mit vollständiger Anpassung zu sein. Der Benutzer hat jetzt die Möglichkeit, die folgenden Aufgaben auszuführen: <ul><li>Aktualisieren Sie die ausgewählten Standard- und benutzerdefinierten Attribute im Widget &quot;Grundlegende Informationen&quot;.</li><li>Benutzerdefinierte Widgets erstellen, bearbeiten und entfernen</li><li>Widgets anpassen und neu anordnen</li></ul> |

Weitere Informationen zu [!DNL Real-time Customer Profile], einschließlich Übungen und Best Practices für die Arbeit mit [!DNL Profile]-Daten, finden Sie im [Überblick über das Echtzeit-Profil des Kunden](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren [!DNL Real-time Customer Profile]-Daten generieren können. Diese Adoben werden zentral auf [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Exportaufträge | Es wurde ein Flag hinzugefügt, damit Segmente im Rahmen eines Exportauftrags ausgewertet werden können. Daher können Benutzer sowohl die Segmentierung als auch Exporte in einem einzigen Auftrag ausführen. |
| Zusammenführungsrichtlinien | Mehrere Zusammenführungsrichtlinien können in einem einzelnen Stapelsegmentierungsauftrag enthalten sein. |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierungsübersicht](../../segmentation/home.md)

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe der [!DNL Platform]-Dienste strukturieren, beschriften und erweitern können. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatische Zuordnung | [!DNL Platform] bietet intelligente Empfehlungen für die automatische Zuordnung während des Datenerfassungs-Workflows, basierend auf einem benutzerspezifischen Zielgruppe-Schema oder einem Datensatz. Sie können flexible Regeln für die automatische Zuordnung manuell an Ihre Anwendungsfälle anpassen. |
| UX-Verbesserungen | Benutzer können auf Aktionen für Inline-Tabellen zugreifen, um den Zugriff auf primäre Aktionen wie das Hinzufügen von Daten, das Bearbeiten von Zeitplänen und das Hinzufügen von Segmenten zu vereinfachen. Weitere Informationen finden Sie im Dokument [Datenflüsse überwachen](../../sources/tutorials/ui/monitor.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
