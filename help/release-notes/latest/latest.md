---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 78f9b8434d577909ccb1c62211a802e05c8291e1
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 35%

---

# Adobe Experience Platform – Versionshinweise

**Releasedatum: 26. Januar 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Dashboards]](#dashboards)
- [Query Service](#query-service)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Warnhinweise {#alerts}

Experience Platform allows you to subscribe to event-based alerts for various Platform activities. Sie können unterschiedliche Regeln für Warnhinweise über die [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche angezeigt werden, und Sie können wählen, ob Warnhinweise in der Benutzeroberfläche selbst oder über E-Mail-Benachrichtigungen empfangen werden sollen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| New alert rules | Für Workflows, die sich auf die Datenerfassung, Identitäten, Profile, Segmentierung und Aktivierung beziehen, stehen jetzt verschiedene neue Warnhinweisregeln zur Verfügung. See the overview on [alert rules](../../observability/alerts/rules.md) for the updated list of alert types. |
| In-Kontext-Warnhinweise für Datenflüsse zu Quellen | You can now subscribe to receive alert messages regarding the status of your dataflows during the ingestion workflow. Weitere Informationen finden Sie im Handbuch unter [Abrufen von Warnhinweisen zu Quellen über die Benutzeroberfläche](../../sources/tutorials/ui/alerts.md). |

Weitere Informationen zu Warnhinweisen in Platform finden Sie im Abschnitt [Warnungen - Übersicht](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, in denen Sie wichtige Informationen zu den Daten Ihres Unternehmens sehen, basierend auf täglichen Schnappschüssen der Daten.

| Funktion | Beschreibung |
| --- | --- |
| Intelligente Untertitel | Ein maschineller Lernalgorithmus bietet automatisch Einblicke in Ihre Profil- und Zielgruppendaten und veranschaulicht Muster und Trends über einen Zeitraum von 30 bis 90 Tagen oder 12 Monaten. Die Beschriftungen enthalten Informationen zu <ul><li>Gesamtform und Statistiken</li><li>Trends und abrupte Änderungen</li><li>Seasonal patterns</li><li>Unerwartete Anomalien</li></ul> More information can be found on the [profiles dashboards](../../dashboards/guides/profiles.md#profiles-count-trend) and [segments dashboards](../../dashboards/guides/segments.md#audience-size-trend) documentation. |
| Dashboards Inventory | Greifen Sie auf die vorkonfigurierten Berichte der Profil-, Segment- und Ziel-Dashboards zu, einschließlich aller installierten Integrationen wie PowerBI, und zwar zentral. Weitere Informationen finden Sie unter [[!DNL Dashboards] Übersicht](../../dashboards/home.md). |
| PowerBI-Berichtsvorlagen | Erstellen, anpassen oder erweitern Sie Metriken aus den Datenmodellen für Profil-, Segment- und Zielberichtsdaten mithilfe neuer Power BI-Diagramme. Der automatisierte Installations-Workflow ermöglicht es Ihnen, innerhalb der PowerBI-Umgebung Ihre Marketing-Einblicke in Ihrem Unternehmen freizugeben. Weitere Informationen finden Sie unter [[!DNL Dashboards] Übersicht](../../dashboards/home.md). |

Weitere Informationen finden Sie unter [!DNL Dashboards], siehe [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Konsolidiertes Zuordnungserlebnis | The new mapping interface in the Platform UI provides you with a consistent mapping experience to take advantage of intelligent mapping recommendations, manually configure mapping rules, and debug any errors that occur to your mapping sets. For more information, see the [[!DNL Data Prep] UI guide](../../data-prep/ui/mapping.md). |

Weitere Informationen finden Sie unter [!DNL Data Prep], siehe [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

<!--

## [!DNL Destinations] {#destinations}

[!DNL Destinations] are pre-built integrations with destination platforms that allow for the seamless activation of data from Adobe Experience Platform. You can use destinations to activate your known and unknown data for cross-channel marketing campaigns, email campaigns, targeted advertising, and many other use cases.

| Feature | Description |
| ----------- | ----------- |
| Placeholder for next-hit personalization | Description |
| Placeholder for batch monitoring | Description |
| Placeholder for re-introducing scheduling in the UI | Description |
| Placeholder for Marketo destination update | Description |


**New destinations**

| Destination | Description |
| ----------- | ----------- |
| Placeholder for Target | Description |
| Placeholder for Custom Personalization | Description |

For more general information on destinations, refer to the [destinations overview](../../destinations/home.md).

-->

## Query Service {#query-service}

[!DNL Query Service] allows you to use standard SQL to query data in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus der [!DNL Data Lake] und erfassen Sie die Abfrageergebnisse als neuen Datensatz zur Verwendung in Berichten, Data Science Workspace oder zur Aufnahme in das Echtzeit-Kundenprofil.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Anonymer Block | The anonymous block SQL construct allows you to break down large scale data preparation jobs in Query Service into smaller tasks, then reuse and execute them in sequence for incremental data loading. Weitere Informationen finden Sie unter [Query Service - Übersicht](../../query-service/home.md). |
| Dataset Organization | Bietet eine kohärente, logische Datenstruktur zur Organisation Ihrer Daten-Assets für die Verwendung mit Query Service, da die Anzahl der Daten-Assets innerhalb der Sandbox zunimmt. Weitere Informationen finden Sie unter [Query Service - Übersicht](../../query-service/home.md). |

Weitere Informationen finden Sie unter [!DNL Query Service], siehe [[!DNL Query Service] Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Darum stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen der Sandbox-Benutzeroberfläche | Der Sandbox-Indikator ist jetzt in die Kopfzeile für alle Platform-UI-Anwendungen integriert. The sandbox indicator displays the sandbox name, region, and type and also allows you to access a dropdown menu to switch between sandboxes. Weitere Informationen finden Sie unter [Handbuch zur Sandbox-Benutzeroberfläche](../../sandboxes/ui/user-guide.md). |

Weitere Informationen zu Sandboxes finden Sie im Abschnitt [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Segmentübereinstimmung | Segment Match ist ein Dienst für die Zusammenarbeit mit Daten, der es zwei oder mehr Platform-Benutzern ermöglicht, Daten basierend auf gemeinsamen Kennungen auf sichere, verwaltete und datenschutzfreundliche Weise auszutauschen. Segment Match uses Platform privacy standards and personal identifiers such as hashed emails, hashed phone numbers, and device identifiers like IDFAs and GAIDs. For more information, see the [Segment Match overview](../../segmentation/ui/segment-match/overview.md). |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierung – Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| Verbesserungen der [!DNL Event Hubs]-Quelle | The [!DNL Event Hubs] source now supports non-root SAS key type of authentication to connect and create source connection. Weitere Informationen finden Sie unter [[!DNL Event Hubs] Übersicht](../../sources/connectors/cloud-storage/eventhub.md). |
| Verbesserungen der [!DNL SFTP]-Quelle | The [!DNL SFTP] source now allows you to a establish a set number of a maximum concurrent connections that a dataflow can use to connect to the SFTP server. Weitere Informationen finden Sie unter [[!DNL SFTP] Übersicht](../../sources/connectors/cloud-storage/sftp.md). |
