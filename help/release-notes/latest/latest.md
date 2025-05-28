---
title: Adobe Experience Platform – Versionshinweise Mai 2025
description: Versionshinweise Mai 2025 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6ab9302a40547349c8d0390baafd8591ed6859e1
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 22%

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

**Veröffentlichungsdatum: Mittwoch, 20. Mai 2025**

Aktualisierungen vorhandener Funktionen und Dokumentationen in Adobe Experience Platform:

- [KI-Assistent](#ai-assistant)
- [Katalog-Service](#catalog-service)
- [Datenvorbereitung](#data-prep)
- [Ziele](#destinations)
- [Identity Service](#identity)
- [Abfrage-Service](#query-service)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## KI-Assistent {#ai-assistant}

Der KI-Assistent in Adobe Experience Platform ist ein Gesprächserlebnis, mit dem Sie Ihre Workflows in Adobe-Anwendungen beschleunigen können. Sie können den KI-Assistenten verwenden, um Produktkenntnisse besser zu verstehen, Probleme zu beheben oder Informationen zu durchsuchen und betriebliche Erkenntnisse zu gewinnen. Der KI-Assistent unterstützt Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit des Produktsupport-Agenten | Sie können jetzt den Produktsupport-Agenten im KI-Assistenten verwenden, um eine nahtlose Fehlerbehebung durchzuführen, ohne Ihre Workflows verlassen zu müssen. Support-Administratoren in Ihrer Organisation können jetzt den Produktsupport-Agenten verwenden, um Support-Tickets für Kunden zu erstellen, einschließlich Kontext- und Sitzungsdetails aus Ihren Interaktionen mit dem KI-Assistenten. <br><br>Der Zugriff auf den Product Support Agent ist bis zum 30. November 2025 verfügbar. Wenden Sie sich an Ihren Adobe-Kundenbetreuer, um den Produktsupport-Agent zu lizenzieren, und verwenden Sie die Funktion nach diesem Datum weiter. Weitere Informationen finden Sie in der [Dokumentation zum Product Support Agent](../../ai-assistant/new-features/customer-support.md). |

Weitere Informationen finden Sie unter [KI-Assistent - Übersicht](../../ai-assistant/landing.md).

## Katalog-Service {#catalog-service}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Alle in Experience Platform aufgenommenen Daten werden als Dateien und Ordner im Data Lake gespeichert. Catalog speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

| Funktion | Beschreibung |
| --- | --- |
| Optimieren der Datenspeicherung mit Aufbewahrungsregeln auf Datensatzebene | Verwalten Sie die Datenspeicherung effizient mit Aufbewahrungsrichtlinien, die veraltete Daten basierend auf Ihrem angegebenen Zeitraum löschen. <ul><li>**Datensatzaufbewahrung**: Definieren Sie Datensatzregeln, um veraltete Daten aus dem Data Lake und Profilspeicher zu entfernen.</li><li>**Speichereinblicke**: Überwachen Sie die Nutzung und stellen Sie die Einhaltung lizenzierter Berechtigungen durch Inline-Metriken sicher.</li><li>**Verbesserte Sichtbarkeit**: Verfolgen Sie die Datensatzaktivität von der Aufnahme bis zum Löschen mit verbesserter Überwachung.</li><li>**Optimiertes Management**: Zugriff auf Aufbewahrungseinstellungen, Überwachung, Auditprotokolle und Einblicke in einer zentralen Ansicht.</li></ul> Weitere Informationen finden Sie [ Handbuch unter ](../../catalog/datasets/user-guide.md#data-retention-policy) für die Datensatzaufbewahrung . |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Übersicht über den Katalog-Service](../../catalog/home.md).

## Datenvorbereitung {#data-prep}

Verwenden Sie die Datenvorbereitung zum Zuordnen, Transformieren und Validieren von Daten in und aus dem Experience-Datenmodell (XDM).

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für Import- und Exportzuordnungen für Adobe Analytics | Sie können jetzt beim Verwenden des Adobe Analytics-Quell-Connectors die Zuordnungsfunktionen zum Importieren und Exportieren für Ihre Adobe Analytics Report Suite-Daten verwenden. <br><br>Exportieren Sie Ihre Zuordnungen in eine CSV-Datei und konfigurieren Sie sie lokal in einer Tabelle. Sie können Ihre aktualisierten Zuordnungen dann über die Zuordnungsschnittstelle in der Benutzeroberfläche in Experience Platform importieren. Mit dieser Funktion können Sie eine große Anzahl von Zuordnungen konfigurieren, ohne sie manuell in der Benutzeroberfläche erstellen zu müssen. Darüber hinaus können Sie beim Erstellen eines neuen Datenflusses eine Kopie Ihrer Zuordnungen direkt in Experience Platform hochladen, um Ihren Workflow zu beschleunigen. <br><br>Weitere Informationen finden Sie im Handbuch unter [Verbinden von Adobe Analytics mit Experience Platform](../../sources/tutorials/ui/create/adobe-applications/analytics.md).</br> |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| --- | --- |
| [Benutzerdefinierte Facebook-Zielgruppe](../../destinations/catalog/social/facebook.md) Upgrade und Unterstützung für adressbezogene Kennungen | Ab dem 23. Mai 2025 und im Verlauf des Monats Juni 2025 werden im Zielkatalog möglicherweise vorübergehend zwei **[!DNL Facebook Custom Audience]** Zielkarten angezeigt, und zwar für bis zu einige Stunden. Dies liegt an einer internen Aktualisierung des Ziel-Services und an der Unterstützung neuer Felder für eine verbesserte Zielgruppenbestimmung und den Abgleich mit Profilen in den Facebook-Eigenschaften. Weitere Informationen zu den neuen Adressfeldern finden Sie im Abschnitt [Unterstützte Identitäten](#supported-identities) . <br><br>Wenn eine Karte mit der Bezeichnung **[!UICONTROL (Neue) benutzerdefinierte Facebook-Zielgruppe angezeigt wird]** verwenden Sie diese Karte für neue Aktivierungsdatenflüsse. Ihre vorhandenen Datenflüsse werden automatisch aktualisiert, sodass keine Aktion erforderlich ist. Alle Änderungen, die Sie während dieses Zeitraums an vorhandenen Datenflüssen vornehmen, bleiben nach dem Upgrade erhalten. Nach Abschluss des Upgrades wird die Zielkarte **[!UICONTROL (neue) benutzerdefinierte Facebook-]** in **[!DNL Facebook Custom Audience]** umbenannt. <br><br>Wenn Sie Datenflüsse mithilfe der [Flow Service-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) erstellen, müssen Sie Ihre [!DNL flow spec ID] und [!DNL connection spec ID] auf die folgenden Werte aktualisieren: <ul><li>Flussspezifikations-ID: `bb181d00-58d7-41ba-9c15-9689fdc831d3`</li><li>Verbindungsspezifikations-ID: `c8b97383-2d65-4b7a-9913-db0fbfc71727`</li></ul> |
| Unterstützung der mobilen Werbe-ID für das Ziel [Google Customer Match + Display &amp; Video 360](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities) | Sie können jetzt Zielgruppen für das Ziel [Google Customer Match + Display &amp; Video 360](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities) aktivieren, basierend auf mobilen Werbe-IDs wie [!DNL GAID] und [!DNL IDFA]. |
| Unterstützung zusätzlicher Kennungen für [Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md) | Das Google-Ziel für den Kundenabgleich unterstützt jetzt die Zuordnung von adressbezogenen Feldern, um die Übereinstimmungsraten in der Google-Plattform zu verbessern. <br><br>Um sicherzustellen, dass Google mit der Adresse übereinstimmt, müssen Sie alle vier Adressfelder (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` und `address_info_postal_code`) zuordnen und sicherstellen, dass in keinem dieser Felder Daten in den exportierten Profilen fehlen. <br> Wenn ein Feld entweder nicht zugeordnet ist oder fehlende Daten enthält, stimmt Google nicht mit der Adresse überein. |
| Spalte „Kontoablauf“ für [Facebook](../../destinations/catalog/social/facebook.md)-Verbindungen | Die Ablaufdaten des Facebook-Konto-Tokens werden jetzt auf den Registerkarten [Durchsuchen](../../destinations/ui/destinations-workspace.md#browse) und [Konten](../../destinations/ui/destinations-workspace.md#accounts) angezeigt. |
| API-erstellte Datensätze exportieren | Sie können jetzt API-erstellte Datensätze exportieren. Die vorherige Einschränkung, bei der nur in der Benutzeroberfläche erstellte Datensätze für den Export verfügbar waren, wurde aufgehoben. Weitere Informationen über [Exportieren von Datensätzen](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../../destinations/home.md).

## Identity Service {#identity}

Verwenden Sie den Adobe Experience Platform Identity Service, um sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhaltensweisen zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Identity Graph Linking Rules] | [!DNL Identity Graph Linking Rules] ist jetzt allgemein verfügbar. [!DNL Identity Graph Linking Rules] verhindern Sie das „Zusammenbrechen von Diagrammen“ und stellen Sie so eindeutige und präzise Kundenprofile für personalisiertes Marketing in Experience Platform und Programmen sicher. Zu den wichtigsten Funktionen gehören:<ul><li>[Graph Simulation Tool](../../identity-service/identity-graph-linking-rules/graph-simulation.md): Erkunden Sie den Algorithmus und testen Sie die Konfigurationen der Identitätseinstellungen.</li><li> [Identitätseinstellungen](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md): Konfigurieren eindeutiger Namespaces und Festlegen von Prioritäten.</li><li>[Identitäts-Dashboard](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs): Überwachen von Diagrammen und Überprüfen von Identitätseinstellungen.</li></ul> **Hinweis**: Ihre Daten werden erst geändert, wenn Sie Ihre Identitätseinstellungen manuell konfigurieren. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Identity Service - Übersicht](../../identity-service/home.md).

## Abfrage-Service {#query-service}

Abfragen von Daten im Data Lake von Adobe Experience Platform unter Verwendung von Standard-SQL mit dem Abfrage-Service. Nahtlose Kombination von Datensätzen und Generierung neuer Datensätze aus Ihren Abfrageergebnissen, um das Reporting zu optimieren, datenwissenschaftliche Workflows zu ermöglichen oder die Aufnahme in das Echtzeit-Kundenprofil zu erleichtern. Sie können beispielsweise Kundentransaktionsdaten mit Verhaltensdaten zusammenführen, um hochwertige Zielgruppen für zielgerichtete Marketing-Kampagnen zu identifizieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
|--------|-------------|
| Migration von JWT zu OAuth-Anmeldeinformationen | Nicht ablaufende JWT-Anmeldeinformationen müssen bis zum 30. Juni 2025 auf OAuth Server-zu-Server migriert werden, um Service-Unterbrechungen zu vermeiden. Diese Änderung verbessert die Sicherheit und Plattformkonsistenz. Weitere Informationen finden Sie [ Handbuch zur Migration von JWT zu OAuth Server-zu-Server](../../query-service/ui/migrate-jwt-to-oauth.md)Anmeldeinformationen . |
| Alte Ergebnistabelle (begrenzte Verfügbarkeit) | Benutzer, die auf Drag-to-Select-Workflows angewiesen sind, können Zugriff auf eine veraltete Ergebnistabelle anfordern, die das browsernative Auswahl- und Kopierverhalten unterstützt. Die eingefügte Ausgabe ist tabulatorgetrennt, sodass die Spalten in Excel ausgerichtet und lesbar bleiben, was die Überprüfung von Kalkulationstabellen und QA-Prozesse erleichtert. Weitere Informationen finden Sie [ Handbuch zur Benutzeroberfläche ](../../query-service/ui/user-guide.md#legacy-results-table) Abfrage-Editors . |

Weitere Informationen zu [!DNL Query Service] finden Sie in der [[!DNL Query Service] Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um diese Anforderung zu erfüllen, stellt Experience Platform Sandboxes bereit, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung der Erweiterung des Sandbox-Tooling-Plug-ins | Kampagnen können jetzt über Sandbox-Tools mit zusätzlichen abhängigen Objekten migriert werden, einschließlich Kanalkonfiguration, einheitlicher Entscheidungsfindung, Experimenteinstellungen/-varianten und mehr. Eine vollständige Liste der unterstützten Kampagnenobjekte sowie aller unterstützten Adobe Journey Optimizer-Objekte finden Sie im [Sandbox-Tools](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects)Handbuch. |

{style="table-layout:auto"}

Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Aktualisierung der Streaming-Segmentierungskriterien | Ab der Version vom Mai 2025 wurden die Kriterien aktualisiert, damit Ihre Zielgruppen für die Streaming-Segmentierung infrage kommen. Weitere Informationen zu diesen Änderungen finden Sie im Abschnitt Aktualisierung der [Kriterien für die Berechtigung zur Streaming-Segmentierung](../../segmentation/eligibility-criteria-update.md). |

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen in Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern aufzunehmen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung der einfachen Authentifizierung für [!DNL MySQL] | Sie können jetzt die Standardauthentifizierung verwenden, um Ihre [!DNL MySQL] mit Experience Platform zu verbinden. Weitere Informationen finden Sie [[!DNL MySQL]  &quot;](../../sources/connectors/databases/mysql.md)&quot;. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).