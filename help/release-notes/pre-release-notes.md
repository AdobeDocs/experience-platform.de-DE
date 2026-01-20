---
title: Hinweise zu Vorabversionen von Experience Platform
description: Eine Vorschau der neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: acb8303673c3271794dcda87b149b473328a7a21
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 18%

---

# Hinweise zu Vorabversionen von Adobe Experience Platform

>[!IMPORTANT]
>
>Dieses Dokument ist als **Vorschau** der Versionshinweise für den aktuellen Monat gedacht. Release-Elemente können sich ändern und in der endgültigen Version hinzugefügt oder entfernt werden.

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/pre-release-notes)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: Januar 2026**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Ziele](#destinations)
- [Echtzeit-Kundenprofil](#real-time-customer-profile)
- [Schemata](#schemas)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## Agent Orchestrator {#agent-orchestrator}

Mit Agent Orchestrator können Sie KI-gestützte Agenten erstellen und bereitstellen, die Workflows automatisieren und kanalübergreifend mit Kunden interagieren können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Probeantrag für Agent Orchestrator | Agent Orchestrator bietet jetzt einen Testantrag an, mit dem Kunden den Service erkunden und testen können, bevor sie sich zu einem vollständigen Kauf verpflichten. Diese Try-before-you-buy-Option ermöglicht es Unternehmen, die Funktionen von Agent Orchestrator, einschließlich Fähigkeiten und Orchestrierungsfunktionen, in ihrer eigenen Umgebung zu bewerten. Die Testversion liefert praktische Erfahrungen beim Erstellen von KI-gestützten Agenten und zeigt, wie diese in bestehende Workflows integriert werden können. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der Dokumentation zu [Agent Orchestrator](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Die Limits für Leitplanken für das Adobe Target-Ziel wurden aktualisiert | Die maximale Anzahl von Zielgruppen, die einem einzelnen Adobe Target-Ziel zugeordnet werden können, wurde von 50 auf 250 erhöht. Dadurch wird Adobe Target an das standardmäßige Zielgruppenlimit für andere Ziele angepasst, was eine größere Flexibilität für Zielgruppenaktivierungs-Workflows bietet. Kunden können jetzt mehr Zielgruppen für Adobe Target-Ziele aktivieren, ohne mehrere Datenflüsse erstellen zu müssen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../destinations/home.md).

## Echtzeit-Kundenprofil {#real-time-customer-profile}

Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Durchsetzung der Streaming-Kapazität | Experience Platform erzwingt jetzt Streaming-Durchsatzkapazitäten für das Echtzeit-Kundenprofil und Identity Service. Wenn Kunden ihre vertraglich vereinbarte Streaming-Kapazität überschreiten, werden Daten in eine Warteschlange gestellt und in einer First-in-First-out-Weise verarbeitet. Dies stellt eine vorhersehbare Systemleistung sicher und verhindert, dass Kapazitätsverletzungen die Datenaufnahmequalität beeinträchtigen. Wichtige Hinweise: Streaming-Upserts sind im Data Lake nicht verfügbar, wenn die Kapazität überschritten wird. Diese Durchsetzung gilt nicht für Kunden mit Adobe Journey Optimizer-Lizenzen und Daten in der Warteschlange werden sequenziell verarbeitet, sobald die Kapazität verfügbar ist. |
| Einstellung des API-Zugriffs für Real-Time CDP Prime | Der API-Zugriff für Erlebnisereignisse wird jetzt für alle Kunden von Real-Time CDP Prime nicht mehr unterstützt. Diese Änderung wirkt sich auf die Möglichkeit aus, Erlebnisereignisse direkt über die API abzufragen. Kunden von Real-Time CDP Ultimate können über einen formalen Ausnahmeprozess eine Ausnahme anfordern, um den API-Zugriff auf Erlebnisereignisse zu aktivieren, falls dies für ihre Anwendungsfälle erforderlich ist. Diese Einstellung trägt zur Optimierung der Systemleistung bei und entspricht den Best Practices für Datenzugriffsmuster. |
| Überwachen der Datenflussausführung | Sie können jetzt den Fortschritt und die Bereitschaft der Datenflussausführungen im Profil überwachen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [[!DNL Real-Time Customer Profile] Übersicht](../profile/home.md).

## Schemata {#schemas}

Schemata dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen. Schemata bestehen aus einer Basisklasse und keiner oder mehreren Schemafeldgruppen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Modernisierung des Schema-Inventars mit Suche, Filter, Tags und Ordnern | Die Seite zum Durchsuchen von Schemata wurde modernisiert, um erweiterte Organisations- und Erkennungsfunktionen bereitzustellen. Zu den neuen Funktionen gehören erweiterte Such- und Filteroptionen, Unterstützung für benutzergenerierte Tags und Ordner zum Organisieren von Schemata sowie Inline-Aktionen zur Optimierung von Workflows. Zu den wichtigsten Verbesserungen gehören: aktualisierte Spalten (Name, Klasse, Datensätze, Identitäten, Beziehungen, Für Profil aktivieren, Verhalten, Schematyp, Tags, Erstellungsdatum, Datum der letzten Änderung), erweiterte Filter (Profile anzeigen, Schematyp, Klasse, Hat ein beliebiges Tag, Erstellungsdatum, Änderungsdatum, Hat primäre Identität, Hat Beziehung, Primären Identity-Namespace), Inline-Aktionen (Bearbeiten, Löschen, Anwenden von Kennzeichnungen, Datensatz für nicht-relationale Schemata erstellen, Tags verwalten, In Ordner verschieben, Zum Paket hinzufügen, JSON-Struktur kopieren, Beispieldatei herunterladen) und die Möglichkeit, Schemata mithilfe von Tags und Ordnern zu organisieren. Diese Verbesserungen bieten einen umfassenden Einblick in Schema-Ressourcen und ermöglichen ein effizienteres Schema-Management auf Sandbox-Ebene. |

Weitere Informationen finden Sie in der [[!DNL Schemas] Übersicht](../xdm/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Teilmenge von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Überwachung der Streaming-Segmentierung | Die Echtzeitüberwachung für Streaming-Segmentierung bietet Transparenz in Bezug auf Metriken zur Bewertungsrate, Latenz und Datenqualität auf Sandbox-, Datensatz- und Zielgruppenebene. Dies unterstützt proaktive Warnhinweise und umsetzbare Einblicke, um Dateningenieuren dabei zu helfen, Kapazitätsverletzungen und Aufnahmeprobleme zu identifizieren. Zu den Überwachungsmetriken gehören Auswertungsrate, P95-Aufnahmelatenz sowie empfangene, ausgewertete, fehlgeschlagene und übersprungene Datensätze. Die Funktionen für Datensatz- und Zielgruppenansicht bieten umfassende Einblicke in neue qualifizierte und disqualifizierte Profile. |
| Aktualisierung der TTL für externe Zielgruppen | Externe Zielgruppen (z. B. CSV-Uploads) unterstützen jetzt eine erzwungene Aktualisierungsfunktion für TTL-Einstellungen (Time-to-Live). Mit dieser Funktion können Benutzer die TTL-Gültigkeit für externe Zielgruppen manuell aktualisieren, was eine bessere Kontrolle über die Verwaltung des Zielgruppen-Lebenszyklus ermöglicht. Dies ist besonders nützlich für Zielgruppen, die über ihre ursprüngliche TTL-Periode hinaus bestehen bleiben müssen oder eine Reaktivierung erfordern, ohne die Daten erneut hochzuladen. |

Weitere Informationen finden Sie in der [[!DNL Segmentation Service] Übersicht](../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| [!DNL Oracle Eloqua] V2-Quelle | Ein neuer [!DNL Oracle Eloqua]-Quell-Connector ist jetzt verfügbar, der den veralteten Connector ersetzt. Dieser aktualisierte Connector bietet erweiterte Funktionen und eine höhere Zuverlässigkeit für die Aufnahme von Daten aus [!DNL Oracle Eloqua] in Experience Platform. Kunden, die den vorhandenen Connector verwenden, sollten zur neuen Implementierung migrieren, da bestehende Verbindungen nicht mehr funktionieren. Der neue Connector unterstützt alle Einrichtungs- und Konfigurationsschritte, die für die Verbindung mit [!DNL Oracle Eloqua] und die Aufnahme von Daten zur Marketing-Automatisierung erforderlich sind. |
| [!DNL Salesforce Marketing Cloud] V2-Quelle | Ein neuer [!DNL Salesforce Marketing Cloud]-Quell-Connector ist jetzt verfügbar, der den veralteten Connector ersetzt. Dieser aktualisierte Connector bietet eine verbesserte Leistung und zusätzliche Funktionen für die Aufnahme von Daten aus [!DNL Salesforce Marketing Cloud] in Experience Platform. Kunden, die den vorhandenen Connector verwenden, sollten zur neuen Implementierung wechseln. Der neue Connector enthält umfassende Einrichtungsanweisungen für die Verbindung mit [!DNL Salesforce Marketing Cloud] und die Aufnahme von Daten zur Marketing-Automatisierung. |

Weitere Informationen finden Sie unter [Quelle – Übersicht](../sources/home.md).

