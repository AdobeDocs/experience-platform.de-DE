---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: bcd52989-ef62-4ab9-866e-1d9e57b76a0c
source-git-commit: 703e49a20fae0fbf527275e1385f596d01642954
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 29%

---

# Adobe Experience Platform – Versionshinweise

**Releasedatum: 26. Januar 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Destinations]](#destinations)
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
| In-Kontext-Warnhinweise für Datenflüsse zu Quellen | Jetzt können Sie sich für den Empfang von Warnhinweisen zum Status Ihrer Datenflüsse während des Aufnahme-Workflows anmelden. Weitere Informationen finden Sie im Handbuch unter [Abrufen von Warnhinweisen zu Quellen über die Benutzeroberfläche](../../sources/tutorials/ui/alerts.md). |

Weitere Informationen zu Warnhinweisen in Platform finden Sie im Abschnitt [Warnungen - Übersicht](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, in denen Sie wichtige Informationen zu den Daten Ihres Unternehmens sehen, basierend auf täglichen Schnappschüssen der Daten.

| Funktion | Beschreibung |
| --- | --- |
| Intelligente Untertitel | Ein maschineller Lernalgorithmus bietet automatisch Einblicke in Ihre Profil- und Zielgruppendaten und veranschaulicht Muster und Trends über einen Zeitraum von 30 bis 90 Tagen oder 12 Monaten. Die Beschriftungen enthalten Informationen zu <ul><li>Gesamtform und Statistiken</li><li>Trends und abrupte Änderungen</li><li>Saisonale Muster</li><li>Unerwartete Anomalien</li></ul> Weitere Informationen finden Sie im [Profil-Dashboards](../../dashboards/guides/profiles.md#profiles-count-trend) und [Segmente-Dashboards](../../dashboards/guides/segments.md#audience-size-trend) Dokumentation. |
| Dashboards-Inventar | Greifen Sie auf die vorkonfigurierten Berichte der Profil-, Segment- und Ziel-Dashboards zu, einschließlich aller installierten Integrationen wie PowerBI, und zwar zentral. Weitere Informationen finden Sie unter [[!DNL Dashboards] Übersicht](../../dashboards/home.md). |
| PowerBI-Berichtsvorlagen | Erstellen, anpassen oder erweitern Sie Metriken aus den Datenmodellen für Profil-, Segment- und Zielberichtsdaten mithilfe neuer Power BI-Diagramme. Der automatisierte Installations-Workflow ermöglicht es Ihnen, innerhalb der PowerBI-Umgebung Ihre Marketing-Einblicke in Ihrem Unternehmen freizugeben. Weitere Informationen finden Sie unter [[!DNL Dashboards] Übersicht](../../dashboards/home.md). |

Weitere Informationen finden Sie unter [!DNL Dashboards], siehe [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Konsolidiertes Zuordnungserlebnis | Die neue Zuordnungsschnittstelle in der Platform-Benutzeroberfläche bietet Ihnen ein konsistentes Zuordnungserlebnis, um intelligente Zuordnungsempfehlungen zu nutzen, Zuordnungsregeln manuell zu konfigurieren und Fehler zu debuggen, die bei Ihren Zuordnungssätzen auftreten. Weitere Informationen finden Sie unter [[!DNL Data Prep] UI-Handbuch](../../data-prep/ui/mapping.md). |

Weitere Informationen finden Sie unter [!DNL Data Prep], siehe [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| Personalisierung auf derselben Seite und auf der nächsten Seite | Die [Personalisierungsfunktion für die gleiche Seite und die nächste Seite](../../destinations/ui/configure-personalization-destinations.md) bietet eine freigegebene, zielgruppenorientierte Ansicht von Benutzern für Anwendungen in Experience Edge, um die Konsistenz zwischen Marketing- und Kundenkanälen zu gewährleisten. Diese Personalisierung ist über die [Adobe Target-Verbindung](../../destinations/catalog/personalization/adobe-target-connection.md) und [Benutzerdefinierte Personalisierungsverbindung](../../destinations/catalog/personalization/custom-personalization.md). Informationen zum Konfigurieren Ihrer Personalisierungskampagnen für die gleiche Seite oder die nächste Seite finden Sie unter [dediziertes Tutorial](../../destinations/ui/configure-personalization-destinations.md). |
| Batch-Zielüberwachung und Metriken auf Segmentebene | Die Funktion zur Zielüberwachung wurde von Streaming-Zielen erweitert und umfasst jetzt auch Batch-Ziele und Metriken auf Segmentebene für Ihre Aktivierungsdatenflüsse. Weitere Informationen finden Sie unter [Dashboard für Überwachungsziele](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard) und [Ansicht auf Segmentebene](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Planen der Bearbeitung vorhandener Batch-Aktivierungsdatenflüsse in der Benutzeroberfläche | Mit dieser Version wird die Option eingeführt, den Zeitplan Ihrer vorhandenen Aktivierungsdaten für Batch-Ziele zu bearbeiten. Weitere Informationen finden Sie unter [Aktivieren von Profildaten für Batch-Profilziele](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Marketo-Zielverbesserungen | Experience Platform-Kunden, die Marketo Engage verwenden, können ihre Marketo-Datenbank maximieren, indem sie die neue Möglichkeit nutzen, neue Netto-Personendatensätze von Experience Platform aus per Push in Marketo Engage zu übertragen. [Marketo-Zielanschluss](/help/destinations/catalog/adobe/marketo-engage.md). <br> Beim Senden von Zielgruppensegmenten von Experience Platform zu Marketo Engage können Personen innerhalb des Segments, die noch nicht in Ihrer Marketo Engage-Datenbank vorhanden sind, automatisch hinzugefügt werden. Weitere Informationen finden Sie unter [Adobe Experience Platform-Segment in eine statische Marketo-Liste pushen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (Schritt 9 des Tutorials zeigt, wie Sie Netto-neue Personendatensätze in Marketo verschieben können). |

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [Adobe Target-Verbindung](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target ist eine Anwendung, die eine Echtzeit-Personalisierung und Experimentierfreudigkeit bei allen eingehenden Kundeninteraktionen über Websites, mobile Apps und mehr hinweg ermöglicht. Adobe Target ist eine Personalisierungsverbindung in Adobe Experience Platform. |
| [Benutzerdefinierte Personalisierungsverbindung](../../destinations/catalog/personalization/custom-personalization.md) | Diese Personalisierungsverbindung bietet eine Möglichkeit, Segmentinformationen von Adobe Experience Platform zu externen Personalisierungsplattformen, Content-Management-Systemen, Anzeigenservern und anderen Anwendungen abzurufen, die auf Kunden-Websites ausgeführt werden. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Query Service {#query-service}

[!DNL Query Service] ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus der [!DNL Data Lake] und erfassen Sie die Abfrageergebnisse als neuen Datensatz zur Verwendung in Berichten, Data Science Workspace oder zur Aufnahme in das Echtzeit-Kundenprofil.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Anonymer Block | Das anonyme Block-SQL-Konstrukt ermöglicht es Ihnen, groß angelegte Datenvorbereitungsaufträge in Query Service in kleinere Aufgaben aufzuschlüsseln, sie dann wiederzuverwenden und nacheinander zum inkrementellen Laden der Daten auszuführen. Weitere Informationen finden Sie unter [Query Service - Übersicht](../../query-service/home.md). |
| Datensatzorganisation | Bietet eine kohärente, logische Datenstruktur zur Organisation Ihrer Daten-Assets für die Verwendung mit Query Service, da die Anzahl der Daten-Assets innerhalb der Sandbox zunimmt. Weitere Informationen finden Sie unter [Query Service - Übersicht](../../query-service/home.md). |

Weitere Informationen finden Sie unter [!DNL Query Service], siehe [[!DNL Query Service] Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Darum stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen der Sandbox-Benutzeroberfläche | Der Sandbox-Indikator ist jetzt in die Kopfzeile für alle Platform-UI-Anwendungen integriert. Die Sandbox-Anzeige zeigt den Namen, die Region und den Typ der Sandbox an und ermöglicht Ihnen auch den Zugriff auf ein Dropdown-Menü, über das zwischen Sandboxes gewechselt werden kann. Weitere Informationen finden Sie unter [Handbuch zur Sandbox-Benutzeroberfläche](../../sandboxes/ui/user-guide.md). |

Weitere Informationen zu Sandboxes finden Sie im Abschnitt [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Segmentübereinstimmung | Segment Match ist ein Dienst für die Zusammenarbeit mit Daten, der es zwei oder mehr Platform-Benutzern ermöglicht, Daten basierend auf gemeinsamen Kennungen auf sichere, verwaltete und datenschutzfreundliche Weise auszutauschen. Segment Match verwendet Platform-Datenschutzstandards und persönliche IDs wie Hash-E-Mails, Hash-Telefonnummern und Geräte-IDs wie IDFAs und GAIDs. Weitere Informationen finden Sie unter [Übersicht über Segmentübereinstimmungen](../../segmentation/ui/segment-match/overview.md). |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierung – Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| Verbesserungen der [!DNL Event Hubs]-Quelle | Die [!DNL Event Hubs] -Quelle unterstützt jetzt den nicht-Root-SAS-Schlüsseltyp der Authentifizierung für die Verbindung und die Erstellung der Quellverbindung. Weitere Informationen finden Sie unter [[!DNL Event Hubs] Übersicht](../../sources/connectors/cloud-storage/eventhub.md). |
| Verbesserungen der [!DNL SFTP]-Quelle | Die [!DNL SFTP] -Quelle können Sie jetzt eine bestimmte Anzahl gleichzeitiger Verbindungen festlegen, mit denen ein Datenfluss eine Verbindung zum SFTP-Server herstellen kann. Weitere Informationen finden Sie unter [[!DNL SFTP] Übersicht](../../sources/connectors/cloud-storage/sftp.md). |
