---
title: Adobe Experience Platform - Versionshinweise April 2026
description: Versionshinweise April 2026 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 9ebf498257378f4c5002276a84f104cf2d337601
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 18%

---

# Adobe Experience Platform – Versionshinweise

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/latest)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: 28. April 2026**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Abfrage-Service](#query-service)
- [Real-Time CDP](#rtcdp)
- [Sandboxes](#sandboxes)
- [Quellen](#sources)

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Build-Details anzeigen | Sie können jetzt entweder über eine Bibliothek oder eine Umgebung auf Builds und Build-Details zugreifen, um den derzeit aktiven Build anzuzeigen und die Inhalte (Erweiterungen, Datenelemente und Regeln) zu überprüfen. Weitere Informationen finden Sie unter [Builds - Übersicht](../../tags/ui/publishing/builds.md#build-details). |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Übersicht über die Datenerfassung](../../tags/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vordefinierte Integrationen mit Zielplattformen. Verwenden Sie Ziele, um Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle zu aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Microsoft Ads-Kundenübereinstimmung](../../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Abgleichen von Kunden nach E-Mail-Adresse und erneutes Kontaktieren mit ihnen in der gesamten [!DNL Microsoft Advertising Network], einschließlich Suche und Zielgruppenanzeigen. Verknüpfen Sie Ihr [!DNL Microsoft Advertising]-Konto mit Real-Time CDP, um die Erstellung und Verwaltung von Kundenauswahllisten direkt aus Experience Platform zu automatisieren. Wenden Sie sich an Ihren Adobe-Kundenbetreuer, um Zugriff zu erhalten. |
| [!BADGE Beta]{type=Informative} [Benutzerdefinierte Zielgruppe bearbeiten](../../destinations/catalog/advertising/reddit-custom-audience.md) | Senden von Zielgruppen von Experience Platform an [!DNL Reddit Ads]. Verbinden Sie Ihr [!DNL Reddit]-Konto, ordnen Sie Identitäten zu und aktivieren Sie Zielgruppen, um Personen zu erreichen, die ihre Interessen auf [!DNL Reddit] aktiv erkunden. |
| [Amazon Ads v2](../../destinations/catalog/advertising/amazon-ads-v2.md) | Verwenden Sie die [!DNL Amazon Ads v2] für alle neuen [!DNL Amazon Ads]. [!DNL Amazon Ads v2] stellt eine Verbindung zu [!DNL Ads Data Manager] her, das erweiterte Identitätstypen, adressbezogene Felder und die Datenfreigabe über [!DNL Amazon Ads] Produkte hinweg unterstützt und so die Targeting- und Zielgruppen-Übereinstimmungsraten verbessert. Der vorhandene [!DNL Amazon Ads]-Connector im Katalog wurde in [(alt) umbenannt [!DNL Amazon Ads]](../../destinations/catalog/advertising/amazon-ads.md). Wenn Sie über eine bestehende Legacy-Verbindung verfügen, funktioniert sie weiterhin ohne erforderliche Änderungen. |
| [[!DNL Rokt]](../../destinations/catalog/advertising/rokt.md) | Verwenden Sie [!DNL Rokt], um Experience Platform-Zielgruppen mit KI-gestützter Echtzeit-Entscheidungsfindung zu verbinden und so die Kampagnenleistung durch präziseres Targeting, Unterdrückung und Personalisierung zu verbessern. |
| [Acxiom-Zielgruppenverbindung](../../destinations/catalog/advertising/acxiom-audience-connection.md) | Das [!DNL Acxiom Audience Connection] ist jetzt allgemein verfügbar. Zielgruppen können mithilfe der [!DNL Acxiom's Real ID]-Technologie angereichert und für [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL Facebook], [!DNL Amazon], [!DNL Pinterest], [!DNL Vizio], [!DNL LG Ads], [!DNL Spectrum] und [!DNL Viant] aktiviert werden. |
| [Acxiom Real ID-Zielgruppenverbindung](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | Das [!DNL Acxiom Real ID Audience Connection] ist jetzt allgemein verfügbar. Aktivieren Sie damit Zielgruppen mithilfe von [!DNL Acxiom's Real ID] als Übereinstimmungsschlüssel für [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL Facebook], [!DNL Amazon], [!DNL Pinterest], [!DNL Vizio], [!DNL LG Ads], [!DNL Spectrum] und [!DNL Viant]. |

{style="table-layout:auto"}

**Fehlerbehebungen und Verbesserungen**

| Korrigieren | Beschreibung |
| --- | --- |
| Neue `TS` für [Snowflake-Streaming](../../destinations/catalog/warehouses/snowflake.md)-Ziele | Das Ziel [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) enthält jetzt eine `TS` Zeitstempelspalte in der freigegebenen Tabelle, die anzeigt, wann jede Zeile zuletzt aktualisiert wurde. Dieses Update wird bis Ende April eingeführt. |
| Monitoring-Unterstützung für [Custom Personalization](../../destinations/catalog/personalization/custom-personalization.md)-Ziele | Auf [&#x200B; Seite „Datenflussausführungen](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) werden jetzt Metriken für [benutzerdefinierte Personalization](../../destinations/catalog/personalization/custom-personalization.md)-Ziele angezeigt. Zuvor waren diese Metriken für diesen Zieltyp nicht verfügbar. Verwenden Sie sie, um zu überprüfen, ob die Zielgruppen erwartungsgemäß aktiviert werden, und um Probleme zu diagnostizieren. <br> ![Für ein benutzerdefiniertes Personalization-Ziel werden Metriken zu Datenflussausführungen angezeigt, die aktivierte, ausgeschlossene und fehlgeschlagene Identitäten anzeigen.](../2026/assets/april/dataflow-run-custom-personalization.png "Metriken für Datenflussausführungen für benutzerdefinierte Personalization-Ziele."){zoomable="yes"} |
| Anzahl der Profile im Überprüfungsschritt des Aktivierungs-Workflows | Der Überprüfungsschritt des Aktivierungs-Workflows zeigt jetzt die Profilanzahl für Zielgruppen an, die bereits aktiviert sind. Die Profilanzahl wird auch für [Streaming-Ziele](../../destinations/ui/activate-segment-streaming-destinations.md) angezeigt, nicht nur [Batch-Ziele](../../destinations/ui/activate-batch-profile-destinations.md). <br> ![Profilanzahl, die im Überprüfungsschritt des Aktivierungs-Workflows für bereits aktivierte und Streaming-Zielgruppen angezeigt wird.](../2026/assets/april/profile-count-review.png "Profilanzahl im Überprüfungsschritt des Aktivierungs-Workflows."){zoomable="yes"} |
| Sichtbarkeit des [!DNL Pinterest]-Tokens | Das [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md)-Ziel zeigt jetzt das Token-Ablaufdatum an, sodass Sie sehen können, wann eine erneute Authentifizierung erforderlich ist. [!DNL Pinterest]-Token laufen alle 30 Tage ab. Wenn ein Token abläuft, funktionieren Datenexporte nicht mehr. Um Unterbrechungen zu vermeiden, [Aktualisieren Sie Ihre Authentifizierungsdaten](../../destinations/catalog/advertising/pinterest.md#refresh-authentication-credentials) bevor das Token abläuft. |
| Exportdatei ist jetzt für abgelaufene Zeitpläne deaktiviert | Wenn Ihr Zielgruppen-Zeitplan abgelaufen ist, ist **[!UICONTROL Export file now]** jetzt deaktiviert, bevor Sie versuchen, ihn zu verwenden, und in einer QuickInfo wird erläutert, warum. Zuvor führte die Auswahl der Aktion zu einem Fehler. <br> ![Die Aktion „Datei exportieren“ wurde jetzt mit einer QuickInfo deaktiviert, die erklärt, warum die Aktion nicht verfügbar ist.](../2026/assets/april/export-file-now-disabled.png "Die Aktion „Datei exportieren“ ist jetzt deaktiviert."){zoomable="yes"} |
| Fehlerbehebung bei der Spaltensichtbarkeit im Aktivierungs-Workflow | Es wurde ein Problem behoben, bei dem das Ändern sichtbarer Spalten in einer Tabelle fälschlicherweise andere Tabellen im Aktivierungs-Workflow beeinflusste. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen bei der Nutzung und Erkennung von Feldergruppen | Zeigen Sie direkt in der Benutzeroberfläche an, welche Schemata eine Feldergruppe verwenden und auf Metadaten wie kompatible Klassen, erforderliche Attribute und Governance-Kennzeichnungen zugreifen. Sie können Feldergruppen auch nach Klassenkompatibilität und Branchen-Tags filtern, um relevante Ressourcen effizienter zu ermitteln und die Auswirkungen zu bewerten, bevor Sie Änderungen vornehmen. Weitere Informationen finden [&#x200B; im Handbuch zu &#x200B;](../../xdm/ui/explore.md#explore-field-groups.md) . |

Weitere Informationen finden Sie in der [XDM-Übersicht](../../xdm/home.md).

## Abfrage-Service {#query-service}

Verwenden Sie den Abfrage-Service, um Daten in Adobe Experience Platform [!DNL Data Lake] mit Standard-SQL abzufragen. Schließen Sie beliebige Datensätze aus dem [!DNL Data Lake] zusammen und erfassen Sie Abfrageergebnisse als neuen Datensatz für Berichte, Data Science Workspace oder die Aufnahme in das Echtzeit-Kundenprofil.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Sitzungsverwaltung des Abfrage-Service | Zeigen Sie auf der Registerkarte [!UICONTROL Admin] aktive Sitzungen des Abfrage-Service an und beenden Sie diese, um die Nutzung zu überwachen und die Sitzungskapazität im Leerlauf zu nutzen. Auf diese Weise können Administratoren zuverlässige Data Distiller-Workflows aufrechterhalten, indem sie Kapazitäten aus inaktiven Sitzungen zurückgewinnen. Weitere Informationen finden Sie [&#x200B; Handbuch &#x200B;](../../query-service/ui/session-management.md) Verwalten von Query Service-Sitzungen . |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Query Service - Übersicht](../../query-service/home.md).

## Real-Time CDP {#rtcdp}

Real-Time CDP bietet einheitliche, umsetzbare Kundenprofile, indem Daten über mehrere Kanäle hinweg in Echtzeit aufgenommen, verarbeitet und aktiviert werden. Mit Real-Time CDP können Unternehmen von Experience Platform aus bestehende Datenquellen verbinden, umfangreiche Zielgruppen erstellen und aktivieren und eine datenschutzkonforme Aktivierung über Ziele hinweg sicherstellen. Dadurch können Marketing-Experten, Analysten und IT-Teams ihren Kunden durch nahtlose, kanalübergreifende Marketing-Kampagnen hochgradig personalisierte, zeitnahe Erlebnisse bereitstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Real-Time CDP MCP (Beta) | Verwenden Sie den [Real-Time CDP MCP](../../rtcdp/rtcdp-mcp.md), um Real-Time CDP in KI-Agenten und MCP-kompatible Clients zu integrieren, sodass Sie direkt über Ihr natives LLM-Erlebnis mit Real-Time CDP-Tools interagieren können. Durch Verbinden eines MCP-kompatiblen Clients (z. B. Claude, ChatGPT, Claude Code, Codex, Cursor oder VS Code) mit dem von Ihrem Adobe-Support-Mitarbeiter bereitgestellten Endpunkt können Sie eine natürliche Sprache verwenden, um Zielgruppen, Zielkonfigurationen und den Ausführungsverlauf der Aktivierung zu überprüfen, ohne Experience Platform-REST-API-Aufrufe zu schreiben oder durch mehrere UI-Workflows zu navigieren. Nach Abschluss einer Browser-basierten Adobe-Anmeldung haben Sie schreibgeschützten Zugriff auf Tools, darunter: <ul><li>Durchsuchen vorhandener Zielgruppen</li><li>Vorschau der Zielgruppenzugehörigkeit</li><li>Auflisten der Zieltypen</li><li>Auflisten der konfigurierten Konten</li><li>Auflisten der konfigurierten Ziele</li><li>Auflisten von Source-Verbindungen</li><li>Auflisten der Zielverbindungen</li><li>Überprüfen von Aktivierungsdurchgängen</li></ul>. Für jede Anfrage sind `imsOrgId`- und `sandboxName` erforderlich, um sicherzustellen, dass Aktionen für Ihre Organisation und Sandbox gelten. **Hinweis**: Schreibvorgänge werden in dieser Beta-Version nicht unterstützt. |

{style="table-layout:auto"}

Weiterführende Informationen finden Sie in der Übersicht zu [Real-Time CDP](../../rtcdp/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Eilexemplar | Verwenden Sie Express Copy , um Objekte in einer einzigen Aktion von der Sandbox-[-Benutzeroberfläche in eine Ziel-Sandbox zu &#x200B;](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Abhängige Objekte werden automatisch erkannt und in der Ziel-Sandbox erstellt oder wiederverwendet, wenn sie bereits vorhanden sind. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.One] | Die [[!DNL Talon.One] Quelle](../../sources/connectors/loyalty/talon-one.md) für Experience Platform ist jetzt sowohl im Batch- als auch im Streaming-Modus verfügbar. Verwenden Sie die [[!DNL Talon.One Batch Source Connector]](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md), um regelmäßig geschlossene Sitzungen und frühere Treuetransaktionen aufzunehmen, und die [[!DNL Talon.One Streaming Events]](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md), um [!DNL Talon.One] Ereignisse nahezu in Echtzeit in Experience Platform zu importieren. Gemeinsam erleichtern sie das Laden und Aktivieren [!DNL Talon.One] Treueprogramm-Daten in Real-Time CDP, Adobe Journey Optimizer und Offer Decisioning. |
| Filterunterstützung auf Zeilenebene für [!DNL Salesforce], die SOQL verwenden | Sie können jetzt [!DNL Salesforce] SOQL-Filter (Object Query Language) direkt in [!DNL Salesforce] Quellverbindungen anwenden, sodass Sie Daten auf Zeilenebene einschränken können, bevor sie in Experience Platform aufgenommen werden. Verwenden Sie die -Funktion, um: <ul><li>Definieren von SOQL-WHERE-Klausel-Stilbedingungen für Salesforce-Objekte (z. B. führt nur mit E-Mail != null oder Opportunities in bestimmten Phasen)</li><li>Die Aufnahme auf die Zeilen beschränken, die Ihren Kriterien entsprechen, wodurch unnötige Datenverschiebung, Speicherung und nachgelagerte Verarbeitung reduziert werden</li><li>Die Experience Platform-Aufnahme enger an den Regeln für den Datenzugriff und die Compliance in Ihrem CRM auszurichten, indem kontrolliert wird, welche Datensätze an der Quelle in Experience Platform importiert werden</li></ul>. Weitere Informationen finden Sie im Handbuch unter [Filterung auf Zeilenebene nach Quellen](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).

<!--

| Data Distiller Accelerators | Run and schedule Adobe-managed, parameterized SQL templates in the Query Service UI to perform common analyses without writing SQL. This helps you standardize analytics workflows and reuse trusted query logic across your organization. See the [Data Distiller accelerators guide](../../query-service/ui/accelerators.md) for more details. |

| Automatic dataflow disabling | Sources ingestion dataflows that fail continuously for 30 days are automatically disabled, helping to surface unhealthy dataflows and reduce repeated failed runs. |

--->