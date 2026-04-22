---
title: Hinweise zu Vorabversionen von Experience Platform
description: Eine Vorschau der neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: d052230ec5ddc4a28495f4928ab32957bf9038ac
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 17%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/latest)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: April 2026**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Abfrage-Service](#query-service)
- [Real-Time CDP](#rtcdp)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Microsoft Ads-Kundenübereinstimmung](../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Abgleichen von Kunden nach E-Mail-Adresse und erneutes Kontaktieren mit ihnen in der gesamten [!DNL Microsoft Advertising Network], einschließlich Suche und Zielgruppenanzeigen. Verknüpfen Sie Ihr [!DNL Microsoft Advertising]-Konto mit Real-Time CDP, um die Erstellung und Verwaltung von Kundenauswahllisten direkt aus Experience Platform zu automatisieren. |
| [!BADGE Beta]{type=Informative} [Benutzerdefinierte Zielgruppe bearbeiten](../destinations/catalog/advertising/reddit-custom-audience.md) | Senden von Zielgruppen von Experience Platform an [!DNL Reddit Ads]. Verbinden Sie Ihr [!DNL Reddit]-Konto, ordnen Sie Identitäten zu und aktivieren Sie Zielgruppen, um Personen zu erreichen, die ihre Interessen auf [!DNL Reddit] aktiv erkunden. |
| [Amazon Ads v2](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2] ist das aktuelle Ziel für alle neuen [!DNL Amazon Ads]. Wenn Sie über eine bestehende [ (veraltete)  [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md) verfügen, funktioniert sie weiterhin ohne erforderliche Änderungen. [!DNL Amazon Ads v2] stellt eine Verbindung zu [!DNL Ads Data Manager] her, das erweiterte Identitätstypen, adressbezogene Felder und die Datenfreigabe über [!DNL Amazon Ads] Produkte hinweg unterstützt und so die Targeting- und Zielgruppen-Übereinstimmungsraten im Vergleich zu [ (veraltet) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md). |
| [!DNL Rokt] | Verwenden Sie [!DNL Rokt], um Experience Platform-Zielgruppen mit KI-gestützter Echtzeit-Entscheidungsfindung zu verbinden und so die Kampagnenleistung durch präziseres Targeting, Unterdrückung und Personalisierung zu verbessern. |

{style="table-layout:auto"}

**Fehlerbehebungen und Verbesserungen**

| Fehlerbehebung | Beschreibung |
| --- | --- |
| Benutzerdefinierte Personalization-Überwachungsunterstützung | Das Überwachungs-Dashboard für Ziele unterstützt jetzt [!DNL Custom Personalization] Ziele. Der Hinweis zur Einschränkung, der [!DNL Custom Personalization] von der Überwachung ausschließt, wurde entfernt. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, um Erkenntnisse schneller und besser integriert bereitzustellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Sichtbarkeit der Verwendung von Feldergruppen-Schemas | Zeigen Sie auf der Detailseite an, welche Schemata eine Feldergruppe verwenden, und erkunden Sie diese in einem sortierbaren Dialogfeld mit Schemadateien. Auf diese Weise können Sie Abhängigkeiten und Auswirkungen schnell bewerten, ohne die Seite zu verlassen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [XDM-System - Übersicht](../xdm/home.md).

## Abfrage-Service {#query-service}

Verwenden Sie den Abfrage-Service, um Daten in Adobe Experience Platform [!DNL Data Lake] mit Standard-SQL abzufragen. Schließen Sie beliebige Datensätze aus dem [!DNL Data Lake] zusammen und erfassen Sie Abfrageergebnisse als neuen Datensatz für Berichte, Data Science Workspace oder die Aufnahme in das Echtzeit-Kundenprofil.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Daten-Distiller-Beschleuniger | Führen Sie parametrisierte SQL-Vorlagen in der Benutzeroberfläche des Abfrage-Service aus, die von Adobe verwaltet werden, und planen Sie sie, um gängige Analysen durchzuführen, ohne SQL zu schreiben. Dies hilft Ihnen, Analytics-Workflows zu standardisieren und vertrauenswürdige Abfragelogik in Ihrem gesamten Unternehmen wiederzuverwenden. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Query Service - Übersicht](../query-service/home.md).

## Real-Time CDP {#rtcdp}

[!DNL Real-Time CDP] bietet einheitliche, umsetzbare Kundenprofile, indem Daten über mehrere Kanäle hinweg in Echtzeit aufgenommen, verarbeitet und aktiviert werden. Mit Real-Time CDP können Unternehmen von Experience Platform aus bestehende Datenquellen verbinden, umfangreiche Zielgruppen erstellen und aktivieren und eine datenschutzkonforme Aktivierung über Ziele hinweg sicherstellen. Dadurch können Marketing-Experten, Analysten und IT-Teams ihren Kunden durch nahtlose, kanalübergreifende Marketing-Kampagnen hochgradig personalisierte, zeitnahe Erlebnisse bereitstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Real-Time CDP MCP (Beta) | Verwenden Sie den Real-Time CDP-MCP, um Real-Time CDP in KI-Agenten und MCP-kompatible Clients zu integrieren, sodass Sie direkt über Ihr natives LLM-Erlebnis mit Real-Time CDP-Tools interagieren können. Durch Verbinden eines MCP-kompatiblen Clients (z. B. Claude, ChatGPT, Claude Code, Codex, Cursor oder VS Code) mit `https://rtcdp-mcp.adobe.io/mcp` können Sie die natürliche Sprache verwenden, um Zielgruppen, Zielkonfiguration und den Ausführungsverlauf der Aktivierung zu überprüfen, ohne Experience Platform REST-API-Aufrufe zu schreiben oder durch mehrere UI-Workflows zu navigieren. Nach Abschluss einer Browser-basierten Adobe-Anmeldung haben Sie schreibgeschützten Zugriff auf Tools, darunter: <ul><li>Durchsuchen vorhandener Zielgruppen</li><li>Vorschau der Zielgruppenzugehörigkeit</li><li>Auflisten der Zieltypen</li><li>Auflisten der konfigurierten Konten</li><li>Auflisten der konfigurierten Ziele</li><li>Auflisten von Source-Verbindungen</li><li>Auflisten der Zielverbindungen</li><li>Überprüfen von Aktivierungsdurchgängen</li></ul>. Für jede Anfrage sind `imsOrgId`- und `sandboxName` erforderlich, um sicherzustellen, dass Aktionen für Ihre Organisation und Sandbox gelten. Beachten Sie, dass Schreibvorgänge in dieser Beta-Version nicht unterstützt werden. |

{style="table-layout:auto"}

Weiterführende Informationen finden Sie in der Übersicht zu [Real-Time CDP](../rtcdp/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Eilexemplar | Verwenden Sie Express Copy , um Objekte in einer einzigen Aktion von der Sandbox-[-Benutzeroberfläche in eine Ziel-Sandbox zu ](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Abhängige Objekte werden automatisch erkannt und in der Ziel-Sandbox erstellt oder wiederverwendet, wenn sie bereits vorhanden sind. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Sandbox-Übersicht](../sandboxes/home.md).

## Segmentierungs-Service {#segmentation-service}

Verwenden Sie den Segmentierungs-Service, um Zielgruppen aus Ihren Kundendaten zu erstellen und deren gesamten Lebenszyklus in Experience Platform zu verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Überwachung der Streaming-Segmentierung | Überwachen Sie die Streaming-Segmentierung mit Echtzeit-Einblicken in Auswertungsraten, Aufnahmelatenz und Datenqualitätsmetriken auf Sandbox-, Datensatz- und Segmentebene. Anzeigen von Metriken einschließlich Auswertungsrate, P95-Aufnahmelatenz, empfangene, ausgewertete, fehlgeschlagene und übersprungene Datensätze. Zeigen Sie auch neue Profile an, die pro Segment qualifiziert und disqualifiziert sind. Verwenden Sie diese Einblicke, um Kapazitätsverletzungen und Aufnahmeprobleme zu identifizieren, bevor sie sich auf Ihre Daten auswirken. |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Zielgruppen - Übersicht](../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| Automatische Deaktivierung des Datenflusses | Datenflüsse zur Quellaufnahme, die 30 Tage lang kontinuierlich fehlschlagen, werden automatisch deaktiviert, was dazu beiträgt, fehlerhafte Datenflüsse aufzudecken und wiederholte fehlgeschlagene Ausführungen zu reduzieren. |
| [!DNL Delta Sharing] | Sie können die [!DNL Delta Sharing] verwenden, um Delta-Tabellen über ein sicheres, offenes Protokoll für die Datenfreigabe in Experience Platform zu importieren. Nachdem Sie eine [!DNL Delta Sharing]-Verbindung konfiguriert und die Freigaben und Tabellen ausgewählt haben, die Sie aufnehmen möchten, bringt Platform diese Daten automatisch in Ihre Datensätze ein, damit Sie sie für die Analyse, Segmentierung und Aktivierung verwenden können. |
| [!DNL Meta Ads] (Betaversion) | Sie können den [!DNL Meta Ads]-Quell-Connector (Beta) im Arbeitsbereich „Quellen“ verwenden, um sich bei [!DNL Meta] zu authentifizieren, Ihre Werbekonten auszuwählen und die Aufnahme [!DNL Meta Ads] Kampagnen- und Leistungsdaten in Experience Platform-Datensätze zu planen. |
| [!DNL Talon.One] | Sie können Experience Platform jetzt mit [!DNL Talon.One] verbinden, indem Sie die neuen [!DNL Talon.One]-Batch- und Streaming-Quellen verwenden. Verwenden Sie die neuen Quellen, um Treueprofildaten sowie Transaktions- und Treueprogramm-Aktivitätsereignisse in Experience Platform aufzunehmen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../sources/home.md).
