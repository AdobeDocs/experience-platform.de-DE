---
title: Adobe Experience Platform – Versionshinweise Januar 2022
description: Versionshinweise Januar 2022 für Adobe Experience Platform.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 100%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 26. Januar 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Abfrage-Service](#query-service)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Warnhinweisregeln | Für Workflows, die sich auf Datenaufnahme, Identitäten, Profile, Segmentierung und Aktivierung beziehen, stehen jetzt verschiedene neue Warnhinweisregeln zur Verfügung. Die aktualisierte Liste der Warnhinweistypen finden Sie in der Übersicht zu [Warnhinweisregeln](../../observability/alerts/rules.md). |
| Kontextabhängige Warnhinweise für Quelldatenflüsse | Jetzt können Sie sich für den Empfang von Warnhinweisen zum Status Ihrer Datenflüsse während des Aufnahme-Workflows anmelden. Weitere Informationen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Quellen über die Benutzeroberfläche](../../sources/tutorials/ui/alerts.md). |

Weitere Informationen zu Warnhinweisen in Platform finden Sie im Abschnitt [Warnhinweise – Übersicht](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Insights zu den Daten Ihres Unternehmens erhalten, die in täglichen Snapshots erfasst werden.

| Funktion | Beschreibung |
| --- | --- |
| Intelligente Beschriftungen | Ein maschineller Lernalgorithmus bietet automatisch Einblicke zu Ihren Profil- und Zielgruppendaten und veranschaulicht Muster und Trends über einen Zeitraum von 30 bis 90 Tagen oder 12 Monaten. Die Beschriftungen enthalten Informationen zu <ul><li>Gesamtform und Statistiken</li><li>Trends und plötzlichen Veränderungen</li><li>Saisonalen Mustern</li><li>Unerwarteten Anomalien</li></ul> Weitere Informationen finden sich in der Dokumentation zu [Profil-Dashboards](../../dashboards/guides/profiles.md#profiles-count-trend) und [Segment-Dashboards](../../dashboards/guides/segments.md#audience-size-trend). |
| Dashboards-Inventar | Greifen Sie von einem zentralen Ort aus auf die vorkonfigurierten Berichte der Profil-, Segment- und Ziel-Dashboards zu, einschließlich aller installierten Integrationen wie Power BI. Weitere Informationen finden Sie in der [[!DNL Dashboards] Inventar-Dokumentation](../../dashboards/inventory.md). |
| Power BI-Berichtsvorlagen | Mit den neuen Power BI-Diagrammen können Sie Metriken aus den Profil-, Segment- und Ziel-Datenmodellen erstellen, anpassen oder erweitern. Der automatisierte Installations-Workflow ermöglicht es Ihnen, innerhalb der Power BI-Umgebung Ihre Marketing-Einblicke in Ihrem Unternehmen zu teilen. Weitere Informationen finden Sie in der [Dokumentation zu Power BI-Berichtsvorlagen](../../dashboards/integrations/power-bi.md). |

Weitere Informationen zu [!DNL Dashboards] finden Sie in der [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Konsolidiertes Zuordnungserlebnis | Die neue Zuordnungsschnittstelle in der Platform-Benutzeroberfläche bietet Ihnen ein konsistentes Zuordnungserlebnis, um intelligente Zuordnungsempfehlungen zu nutzen, Zuordnungsregeln manuell zu konfigurieren und Fehler zu beheben, die bei Ihren Zuordnungssätzen auftreten. Weitere Informationen finden Sie im [[!DNL Data Prep] Handbuch zur Benutzeroberfläche](../../data-prep/ui/mapping.md). |

Weitere Informationen zu [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| Personalisierung der gleichen Seite und der nächsten Seite | Die Funktion [Personalisierung der gleichen Seite und der nächsten Seite](../../destinations/ui/configure-personalization-destinations.md) bietet eine gemeinsame Ansicht von Benutzern für Programme in Experience Edge, um die Konsistenz zwischen Marketing- und Kundenkanälen zu gewährleisten. Diese Personalisierung ist über die [Adobe Target-Verbindung](../../destinations/catalog/personalization/adobe-target-connection.md) und [benutzerdefinierte Personalisierungsverbindung](../../destinations/catalog/personalization/custom-personalization.md) möglich. Informationen zum Konfigurieren Ihrer Kampagnen mit Personalisierung der gleichen Seite oder der nächsten Seite finden Sie im [spezifischen Tutorial](../../destinations/ui/configure-personalization-destinations.md). |
| Batch-Zielüberwachung und Metriken auf Segmentebene | Die Zielüberwachungsfunktionalität für Ihre Aktivierungsdatenströme wurde nun von Streaming-Zielen auf Batch-Ziele und Segmentmetriken erweitert. Weitere Informationen finden Sie unter [Dashboard für die Überwachung von Zielen](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [Dashboard für die Überwachung von Segmentvorgängen](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard) und [Ansicht auf Segmentebene](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Planen der Bearbeitung vorhandener Batch-Aktivierungsdatenflüsse in der Benutzeroberfläche | Mit dieser Version wird erstmals die Möglichkeit geboten, den Zeitplan Ihrer bestehenden Aktivierungsdatenflüsse für Batch-Ziele zu bearbeiten. Weitere Informationen finden Sie unter [Aktivieren von Profildaten für Batch-Profilziele](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Marketo-Zielverbesserungen | Experience Platform-Kunden, die Marketo Engage nutzen, können ihre Marketo-Datenbank optimieren, indem sie neue Personendatensätze von Experience Platform über den [Marketo-Ziel-Connector](/help/destinations/catalog/adobe/marketo-engage.md) per Push in Marketo Engage übertragen. <br> Beim Senden von Zielgruppensegmenten von Experience Platform zu Marketo Engage können Personen innerhalb des Segments, die noch nicht in Ihrer Marketo Engage-Datenbank vorhanden sind, automatisch hinzugefügt werden. Weitere Informationen finden Sie unter [Adobe Experience Platform-Segment in eine statische Marketo-Liste verschieben](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=de) (Schritt 9 des Tutorials zeigt, wie Sie neue Personendatensätze in Marketo verschieben können). |

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [Adobe Target-Verbindung](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht. Adobe Target ist eine Personalisierungsverbindung in Adobe Experience Platform. |
| [Benutzerdefinierte Personalisierungsverbindung](../../destinations/catalog/personalization/custom-personalization.md) | Diese Personalisierungsverbindung bietet eine Möglichkeit, Segmentinformationen von Adobe Experience Platform auf externe Personalisierungsplattformen, Content-Management-Systeme, Anzeigen-Server und andere Programme zu übertragen, die auf Kunden-Websites ausgeführt werden. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Abfrage-Service {#query-service}

[!DNL Query Service] ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Anonymer Block | Das anonyme Block-SQL-Konstrukt ermöglicht es Ihnen, umfangreiche Datenvorbereitungsvorgänge im Abfrage-Service in kleinere Aufgaben zu zerlegen, sie dann wiederzuverwenden und nacheinander zum inkrementellen Laden der Daten zu verwenden. Weitere Informationen finden Sie in der [Dokumentation zu Beispielabfragen für den anonymen Block](../../query-service/essential-concepts/anonymous-block.md). |
| Datensatzstruktur | Bietet eine kohärente, logische Datenstruktur zur Organisation Ihrer Datenelemente für die Verwendung mit dem Abfrage-Service, wenn die Anzahl der Datenelemente innerhalb der Sandbox zunimmt. Weitere Informationen finden Sie in der [Dokumentation zum Organisieren von Datenelementen](../../query-service/best-practices/organize-data-assets.md). |

Weitere Informationen zu [!DNL Query Service] finden Sie in der [[!DNL Query Service] Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Darum stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen der Sandbox-Benutzeroberfläche | Der Sandbox-Indikator ist jetzt für alle Programme der Platform-Benutzeroberfläche in die Kopfzeile integriert. Die Sandbox-Anzeige zeigt den Namen, die Region und den Typ der Sandbox an und ermöglicht Ihnen auch den Zugriff auf ein Dropdown-Menü, über das zwischen Sandboxes gewechselt werden kann. Weitere Informationen finden Sie im [Handbuch zur Sandbox-Benutzeroberfläche](../../sandboxes/ui/user-guide.md). |

Weiterführende Informationen zu Sandboxes finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Segment Match | Segment Match ist ein Service für die Zusammenarbeit mit Daten, der es zwei oder mehr Platform-Benutzern ermöglicht, Daten basierend auf gemeinsamen Kennungen auf sichere, verwaltete und datenschutzfreundliche Weise auszutauschen. Segment Match verwendet Platform-Datenschutzstandards und persönliche IDs wie Hash-E-Mails, Hash-Telefonnummern und Geräte-IDs wie IDFAs und GAIDs. Weiterführende Informationen finden Sie in der [Übersicht zu Segment Match](../../segmentation/ui/segment-match/overview.md). |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| Verbesserungen der [!DNL Event Hubs]-Quelle | Die [!DNL Event Hubs]-Quelle unterstützt jetzt die Authentifizierung über den Nicht-Root-SAS-Schlüssel zum Verbinden und Erstellen der Quellverbindung. Weiterführende Informationen finden Sie in der [[!DNL Event Hubs] Übersicht](../../sources/connectors/cloud-storage/eventhub.md). |
| Verbesserungen der [!DNL SFTP]-Quelle | Mit der [!DNL SFTP]-Quelle können Sie jetzt die maximale Anzahl gleichzeitiger Verbindungen festlegen, mit denen ein Datenfluss eine Verbindung zum SFTP-Server herstellen kann. Weiterführende Informationen finden Sie in der [[!DNL SFTP] Übersicht](../../sources/connectors/cloud-storage/sftp.md). |
