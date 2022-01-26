---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: bcd52989-ef62-4ab9-866e-1d9e57b76a0c
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

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Platform-Aktivitäten abonnieren. Sie können unterschiedliche Regeln für Warnhinweise über die [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche angezeigt werden, und Sie können wählen, ob Warnhinweise in der Benutzeroberfläche selbst oder über E-Mail-Benachrichtigungen empfangen werden sollen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Warnhinweisregeln | Für Workflows, die sich auf die Datenerfassung, Identitäten, Profile, Segmentierung und Aktivierung beziehen, stehen jetzt verschiedene neue Warnhinweisregeln zur Verfügung. Siehe Übersicht unter [Warnregeln](../../observability/alerts/rules.md) für die aktualisierte Liste der Warnungstypen. |
| In-context alerts for sources dataflows | Jetzt können Sie sich für den Empfang von Warnhinweisen zum Status Ihrer Datenflüsse während des Aufnahme-Workflows anmelden. For more information, see the guide on [subscribing to sources alerts in the UI](../../sources/tutorials/ui/alerts.md). |

Weitere Informationen zu Warnhinweisen in Platform finden Sie im Abschnitt [Warnungen - Übersicht](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, in denen Sie wichtige Informationen zu den Daten Ihres Unternehmens sehen, basierend auf täglichen Schnappschüssen der Daten.

| Funktion | Beschreibung |
| --- | --- |
| Intelligente Untertitel | Ein maschineller Lernalgorithmus bietet automatisch Einblicke in Ihre Profil- und Zielgruppendaten und veranschaulicht Muster und Trends über einen Zeitraum von 30 bis 90 Tagen oder 12 Monaten. Die Beschriftungen enthalten Informationen zu <ul><li>Gesamtform und Statistiken</li><li>Trends and abrupt changes</li><li>Saisonale Muster</li><li>Unerwartete Anomalien</li></ul> Weitere Informationen finden Sie im [Profil-Dashboards](../../dashboards/guides/profiles.md#profiles-count-trend) und [Segmente-Dashboards](../../dashboards/guides/segments.md#audience-size-trend) Dokumentation. |
| Dashboards Inventory | Access the pre-configured reports of profile, segments, and destinations dashboards including any installed integrations such as PowerBI, in a centralized location. For more information, see the [[!DNL Dashboards] overview](../../dashboards/home.md). |
| PowerBI-Berichtsvorlagen | Erstellen, anpassen oder erweitern Sie Metriken aus den Datenmodellen für Profil-, Segment- und Zielberichtsdaten mithilfe neuer Power BI-Diagramme. The automated installation workflow allows you to share your marketing insights across your organization from within the PowerBI environment. Weitere Informationen finden Sie unter [[!DNL Dashboards] Übersicht](../../dashboards/home.md). |

For more information on [!DNL Dashboards], please see the [[!DNL Dashboards] overview](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Konsolidiertes Zuordnungserlebnis | Die neue Zuordnungsschnittstelle in der Platform-Benutzeroberfläche bietet Ihnen ein konsistentes Zuordnungserlebnis, um intelligente Zuordnungsempfehlungen zu nutzen, Zuordnungsregeln manuell zu konfigurieren und Fehler zu debuggen, die bei Ihren Zuordnungssätzen auftreten. For more information, see the [[!DNL Data Prep] UI guide](../../data-prep/ui/mapping.md). |

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

[!DNL Query Service] ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. You can join any datasets from the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, Data Science Workspace, or for ingestion into Real-time Customer Profile.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Anonymer Block | The anonymous block SQL construct allows you to break down large scale data preparation jobs in Query Service into smaller tasks, then reuse and execute them in sequence for incremental data loading. Weitere Informationen finden Sie unter [Query Service - Übersicht](../../query-service/home.md). |
| Dataset Organization | Provides a coherent, logical data structure to organize your data assets for use with Query Service as the amount of data assets within the sandbox grows. Weitere Informationen finden Sie unter [Query Service - Übersicht](../../query-service/home.md). |

Weitere Informationen finden Sie unter [!DNL Query Service], siehe [[!DNL Query Service] Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Darum stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen der Sandbox-Benutzeroberfläche | The sandbox indicator is now integrated within the header for all Platform UI applications. The sandbox indicator displays the sandbox name, region, and type and also allows you to access a dropdown menu to switch between sandboxes. Weitere Informationen finden Sie unter [Handbuch zur Sandbox-Benutzeroberfläche](../../sandboxes/ui/user-guide.md). |

Weitere Informationen zu Sandboxes finden Sie im Abschnitt [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Segmentübereinstimmung | Segment Match is a data collaboration service that allows for two or more Platform users to exchange data, based on common identifiers, in a secure, governed, and privacy-friendly manner. Segment Match uses Platform privacy standards and personal identifiers such as hashed emails, hashed phone numbers, and device identifiers like IDFAs and GAIDs. For more information, see the [Segment Match overview](../../segmentation/ui/segment-match/overview.md). |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierung – Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| Verbesserungen der [!DNL Event Hubs]-Quelle | Die [!DNL Event Hubs] -Quelle unterstützt jetzt den nicht-Root-SAS-Schlüsseltyp der Authentifizierung für die Verbindung und die Erstellung der Quellverbindung. Weitere Informationen finden Sie unter [[!DNL Event Hubs] Übersicht](../../sources/connectors/cloud-storage/eventhub.md). |
| Verbesserungen der [!DNL SFTP]-Quelle | The [!DNL SFTP] source now allows you to a establish a set number of a maximum concurrent connections that a dataflow can use to connect to the SFTP server. For more information, see the [[!DNL SFTP] overview](../../sources/connectors/cloud-storage/sftp.md). |
