---
title: Adobe Experience Platform – Versionshinweise Februar 2025
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e8c1d7d3b5cc205b9258b4fec5dc7fa68d0d3b27
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 17%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: Mittwoch, 18. Februar 2025**

Aktualisierungen vorhandener Funktionen und Dokumentationen in Adobe Experience Platform:

- [KI-Assistent](#ai-assistant)
- [Katalog-Service](#catalog-service)
- [Datenvorbereitung](#data-prep)
- [Ziele](#destinations)
- [Federated-Audience-Komposition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes){target="_blank"}
- [Quellen](#sources)
- [Segmentierungs-Service](#segmentation)
- [Dokumentationsaktualisierungen](#documentation-updates)
   - [Edge Netzwerk- und Hub-Vergleich](#edge)
   - [Erweiterte Flow Service-API für Quellen](#flow-service)
   - [Sichern von Objektkonfigurationen mithilfe von Sandbox-Tools](#back-up-object-configurations)
   - [Aktivieren eines Kompetenzzentrums mithilfe von Sandbox-Tools](#center-of-excellence)
   - [Beibehaltung von Erlebnisereignis-Datensätzen im Data Lake](#experience-event-dataset-retention)

## KI-Assistent {#ai-assistant}

Der KI-Assistent in Adobe Experience Platform ist ein Gesprächserlebnis, mit dem Sie Ihre Workflows in Adobe-Anwendungen beschleunigen können. Sie können den KI-Assistenten verwenden, um Produktkenntnisse besser zu verstehen, Probleme zu beheben oder Informationen zu durchsuchen und betriebliche Erkenntnisse zu gewinnen. Der KI-Assistent unterstützt Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit von operativen Einblicken | Operative Einblicke in AI Assistant sind jetzt allgemein verfügbar. Operative Einblicke beziehen sich auf Antworten, die der KI-Assistent zu Ihren Metadatenobjekten (Attribute, Zielgruppen, Datenflüsse, Datensätze, Ziele, Journey, Schemata und Quellen) generiert, einschließlich Zählungen, Suchen und Auswirkungen auf die Herkunft. Operational Insights betrachtet keine Daten innerhalb der Sandbox. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche des KI-Assistenten](../../ai-assistant/ui-guide.md). |
| Unterstützung für automatische Vervollständigung von Fragen | Wenn Sie eine Frage in den KI-Assistenten eingeben, können Sie jetzt aus einer Liste empfohlener Fragen auswählen, die der KI-Assistent bereitstellt. Verwenden Sie diese Funktion, um Ihre Workflows mit dem KI-Assistenten weiter zu beschleunigen. Weitere Informationen finden Sie im Handbuch unter [Verwenden der automatischen Vervollständigung von Fragen mit dem KI-Assistenten](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Unterstützung der Datensatzbeobachtbarkeit | Sie können jetzt den KI-Assistenten verwenden, um Fragen zu bestimmten Datensatzmetriken wie Speichergrößen und Zeilenanzahl zu beantworten. Datenbeobachtungsfragen unterstützen Kriterien, mit denen Sie Ihre Abfragen nach einem bestimmten Zeitraum filtern können. Weitere Informationen finden Sie im [Handbuch zum KI-Assistenten](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [KI-Assistent - Übersicht](../../ai-assistant/home.md).

## Katalog-Service {#catalog-service}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Alle in Experience Platform aufgenommenen Daten werden als Dateien und Ordner im Data Lake gespeichert. Catalog speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

| Funktion | Beschreibung |
| --- | --- |
| Neuer API-Endpunkt | Verwalten Sie Ihre Adobe Experience Platform-Datensatzmetadaten effizienter mit dem neuen [Catalog Service API /v2/dataSets/{DATASET_ID}-Endpunkt](../../catalog/api/update-object.md#patch-v2-notation). Einfaches Aktualisieren komplexer, tief verschachtelter Datensatzattribute, da das System automatisch fehlende Pfadebenen erstellt, um Zeit zu sparen, manuelle Schritte zu reduzieren und Fehler zu minimieren. |

{style="table-layout:auto"}

Weitere Informationen zum Katalog-Service finden Sie im Abschnitt [Übersicht über den Katalog-Service](../../catalog/home.md).

## Datenvorbereitung {#data-prep}

Verwenden Sie die Datenvorbereitung zum Zuordnen, Transformieren und Validieren von Daten in und aus dem Experience-Datenmodell (XDM).

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserte Unterstützung für den Import und Export von Zuordnungen | Sie können jetzt Zuordnungen in eine CSV-Datei exportieren und lokal in einer Tabelle konfigurieren. Sie können Ihre aktualisierten Zuordnungen dann über die Zuordnungsschnittstelle in der Benutzeroberfläche in Experience Platform importieren. Mit dieser Funktion können Sie eine große Anzahl von Zuordnungen konfigurieren, ohne sie manuell in der Benutzeroberfläche erstellen zu müssen. Darüber hinaus können Sie beim Erstellen eines neuen Datenflusses eine Kopie Ihrer Zuordnungen direkt in Experience Platform hochladen, um Ihren Workflow zu beschleunigen. Weitere Informationen finden Sie im Handbuch unter [Importieren und Exportieren von Zuordnungen](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Ziele (aktualisiert am 20. Februar) {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Beschreibung |
| --- | --- |
| [(Beta) Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Verwenden Sie den [!DNL Marketo Engage Person Sync]-Connector, um Aktualisierungen von Personen-Zielgruppen zu den entsprechenden Datensätzen in Ihrer [!DNL Marketo Engage]-Instanz zu streamen. Dieser Ziel-Connector befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff anzufordern. |
| [The Trade Desk CRM-Verbindung](/help/destinations/catalog/advertising/tradedesk-emails.md) allgemeine Verfügbarkeit | [!DNL The Trade Desk CRM] Verbindung ist jetzt allgemein verfügbar. Verwenden Sie [!DNL The Trade Desk] CRM-Ziel, um Profile auf der Grundlage von CRM-Daten für das Targeting und die Unterdrückung von Zielgruppen in Ihrem [!DNL Trade Desk]-Konto zu aktivieren. |
| [RainFocus-Teilnehmerprofil-Verbindung](/help/destinations/catalog/marketing-automation/rainfocus.md) | Verwenden Sie das [!DNL RainFocus Attendee Profiles] Ziel, um Kundenprofile aus Adobe Experience Platform in die [!DNL RainFocus] zu streamen, um Teilnehmerprofile zu erstellen und zu aktualisieren. |
| [Criteo-Verbindung](/help/destinations/catalog/advertising/criteo.md) allgemeine Verfügbarkeit | Die [!DNL Criteo] ist jetzt allgemein verfügbar. Criteo ermöglicht vertrauenswürdige und wirkungsvolle Werbung, um jedem Verbraucher über das offene Internet ein reichhaltigeres Erlebnis zu bieten. Mit dem weltweit größten Commerce-Datensatz und der erstklassigen KI stellt Criteo sicher, dass jeder Touchpoint auf der Shopping-Journey personalisiert ist, um Kunden mit der richtigen Anzeige zum richtigen Zeitpunkt zu erreichen. |
| [[!DNL Amazon Ads] -Verbindung](../../destinations/catalog/advertising/amazon-ads.md) | Der [!DNL Amazon Ads]-Connector, der sich zuvor in der Betaphase befand, ist jetzt allgemein verfügbar. Der Connector wurde auch aktualisiert, um ein Einverständnissignal für alle Profile zu senden, die der Verwendung ihrer personenbezogenen Daten für die Werbung zugestimmt haben. Lesen Sie mehr über die neue Steuerung [Amazon Ads Consent Signal](../../destinations/catalog/advertising/amazon-ads.md#destination-details). |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| --- | --- |
| Verwenden von Zugriffsbeschriftungen zur Verwaltung des Benutzerzugriffs auf Zieldatenflüsse | Im Rahmen der [[!UICONTROL attributbasierten Zugriffssteuerung]](/help/access-control/abac/overview.md) in Real-Time CDP können Sie jetzt Zugriffsbeschriftungen auf [Ziel-Datenflüsse“ ](/help/dataflows/ui/monitor-destinations.md). Auf diese Weise können Sie sicherstellen, dass nur eine Teilmenge der Benutzenden in Ihrer Organisation Zugriff auf bestimmte Zieldatenflüsse erhält. <br> **Wichtig**: Bei der Suche nach Ziel-Datenflüssen mithilfe des Suchfelds oben in der Experience Platform-Benutzeroberfläche können die Ergebnisse Ziel-Datenflüsse enthalten, die aufgrund Ihrer Benutzerzugriffsbeschriftungen nicht angezeigt werden können. Dieses Verhalten wird in einer zukünftigen Aktualisierung korrigiert. |
| [Reporting auf Zielgruppenebene](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) für die [Marketo Engage-Verbindung](/help/destinations/catalog/adobe/marketo-engage.md) | Sie können jetzt [Informationen anzeigen](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) über die aktivierten, ausgeschlossenen oder fehlgeschlagenen Identitäten anzeigen, die auf Zielgruppenebene für jede Zielgruppe aufgeschlüsselt sind, die Teil der Datenflüsse für dieses Ziel ist. |
| Unterstützung externer Zielgruppen für die [TikTok](/help/destinations/catalog/social/tiktok.md)- und [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md)-Verbindungen | Sie können externe Zielgruppen für diese Ziele über [benutzerdefinierte Uploads](../../segmentation/ui/audience-portal.md#import-audience) und [Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences) aktivieren. |
| Exportieren von Arrays, Zuordnungen und Objekten in Cloud-Speicher-Ziele | Durch Verwendung des neuen Umschalters **[!UICONTROL Exportieren von Arrays, Zuordnungen, Objekten]** beim Herstellen einer Verbindung zu einem Cloud-Speicher-Ziel können Sie neue komplexe Objekte in ausgewählte Ziele exportieren. [Weitere Informationen](/help/destinations/ui/export-arrays-maps-objects.md) über die Funktion. |

{style="table-layout:auto"}

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

- Ein Problem in den Destination SDK-Test-Tools wurde behoben. Bei einigen Kunden oder Partnern traten Probleme mit dem [Tool zur Profilerstellung](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) auf, da das Format nicht unterstützt wird, wenn das für die Profilerstellung verwendete Schema Datentypen mit einem `No format`-Selektor enthielt.
- Ein Problem bei der Aktualisierung der `targetConnection` von Zielen mithilfe der Flow Service-API wurde behoben. In einigen Fällen verhält sich der PATCH-Vorgang ähnlich wie ein POST-Vorgang, wodurch vorhandene Datenflüsse beschädigt werden. Dieses Problem wurde jetzt behoben, und alle -Kunden können die Flow Service-API verwenden, um ihre `targetConnection` zu aktualisieren. [Weitere Informationen](/help/destinations/api/edit-destination.md#patch-target-connection).
- Beim Exportieren von Profilen an dateibasierte Ziele stellt die Deduplizierung sicher, dass nur ein Profil exportiert wird, wenn mehrere Profile denselben Deduplizierungsschlüssel und denselben Referenzzeitstempel verwenden. Diese Version umfasst eine Aktualisierung des Deduplizierungsprozesses, sodass aufeinander folgende Ausführungen mit denselben Koordinaten immer dieselben Ergebnisse liefern und die Konsistenz verbessert wird. [Weitere Informationen](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp).

Lesen Sie für Weitere Informationen den [Überblick über die Ziele](../../destinations/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Dauerhafte Aufspaltung | Die Zielgruppenkomposition unterstützt jetzt persistente Aufspaltungen. Durch Hinzufügen eines Identitäts-Namespace zu Ihrem Block Aufspaltung können Sie sicherstellen, dass Ihre aufgeteilten Zielgruppen bei der Aufspaltung nach Profil konstant bleiben. Weitere Informationen zu dieser Funktion finden Sie in der [Dokumentation zur Zielgruppenkomposition](../../segmentation/ui/audience-composition.md). |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen in Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern aufzunehmen.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für Ansichten in [!DNL Microsoft Dynamics] | Sie können jetzt `"entityType": "view"` aufnehmen, wenn Sie die [!DNL Microsoft Dynamics] verwenden. Weitere Informationen finden Sie im Handbuch unter [Verbinden einer - [!DNL Microsoft Dynamics]  mit Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).

## Dokumentationsaktualisierungen {#documentation-updates}

### Vergleich von Edge Network und Hub {#edge}

Der [Vergleich von Edge Network und Hub](../../landing/edge-and-hub-comparison.md) bietet einen Überblick über die Unterschiede zwischen den beiden Servertypen für Adobe Experience Platform (Hub und Edge Network), einschließlich der verfügbaren Services für jeden Servertyp, der Standorte der Server sowie empfohlener Szenarien für die Verwendung jedes Servertyps.

### Erweiterte Flow Service-API-Referenz für Quellen {#flow-service}

Die [[!DNL Flow Service] API-Referenz](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) für Quellen wurde mit neuen API-Anfrage- und Antwortbeispielen aktualisiert. Verwenden Sie den erweiterten API-Verweis, um Verbindungsspezifikationen zu erstellen und zu aktualisieren, wenn Sie Ihre eigene Quelle in Experience Platform integrieren. Sie können die erweiterte API-Referenz auch verwenden, um Statusübergänge an Ihren Quell-Entitäten durchzuführen, vorhandene Quell- und Zielverbindungen zu aktualisieren und Flüsse und Flussspezifikationen unter Berücksichtigung bestimmter Filterkriterien abzurufen.

### Sichern von Objektkonfigurationen mithilfe von Sandbox-Tools {#back-up-object-configurations}

Lesen Sie das [Handbuch zur Konfiguration des Sicherungsobjekts](../../sandboxes/use-cases/backup-object-configuration.md), um schrittweise Anweisungen zum Erstellen eines Sicherungspakets mithilfe von Sandbox-Tools zu erhalten, mit denen Sie sicherstellen können, dass Ihre Objektkonfigurationen gespeichert und gesichert werden.

### Aktivieren eines Kompetenzzentrums mithilfe von Sandbox-Tools {#center-of-excellence}

Lesen Sie das [Center of Excellence-Handbuch](../../sandboxes/use-cases/center-of-excellence.md), um schrittweise Anleitungen zur Erstellung eines „goldenen Sandbox“-Pakets zu erhalten, das als Kompetenzzentrum für die effiziente Freigabe wichtiger Konfigurationen fungiert.

### Beibehaltung von Erlebnisereignis-Datensätzen im Data Lake {#experience-event-dataset-retention}

Übernehmen Sie die Kontrolle über die Beibehaltung von Erlebnisereignis-Datensätzen in Adobe Experience Platform mithilfe von Time-to-Live (TTL). [Dieses Handbuch](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) führt Sie durch die Bewertung, Konfiguration und Verwaltung von TTL-Einstellungen, um veraltete Datensätze automatisch zu entfernen, den Speicher zu optimieren und Ihre Daten relevant zu halten. Entdecken Sie Best Practices, Anwendungsfälle aus der Praxis und wichtige Überlegungen zur Verbesserung des Lebenszyklus-Managements Ihrer Daten.
