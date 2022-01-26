---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
source-git-commit: 9cd9307d54d0950d4f67d5d8cee9c6412a558275
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 27%

---

# Adobe Experience Platform – Versionshinweise

**Releasedatum: 26. Januar 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise {#alerts}](#alerts-alerts)
- [[!DNL Data Prep] {#data-prep}](#dnl-data-prep-data-prep)
- [[!DNL Dashboards] {#dashboards}](#dnl-dashboards-dashboards)
- [Query Service {#query-service}](#query-service-query-service)
- [Sandboxes {#sandboxes}](#sandboxes-sandboxes)
- [Segmentierungs-Service {#segmentation}](#segmentation-service-segmentation)

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Platform-Aktivitäten abonnieren. Sie können unterschiedliche Regeln für Warnhinweise über die [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche angezeigt werden, und Sie können wählen, ob Warnhinweise in der Benutzeroberfläche selbst oder über E-Mail-Benachrichtigungen empfangen werden sollen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Warnhinweisregeln | Für Workflows, die sich auf die Datenerfassung, Identitäten, Profile, Segmentierung und Aktivierung beziehen, stehen jetzt verschiedene neue Warnhinweisregeln zur Verfügung. Siehe Übersicht unter [Warnregeln](../../observability/alerts/rules.md) für die aktualisierte Liste der Warnungstypen. |

Weitere Informationen zu Warnhinweisen in Platform finden Sie im Abschnitt [Warnungen - Übersicht](../../observability/alerts/overview.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Konsolidiertes Zuordnungserlebnis | Die neue Zuordnungsschnittstelle in der Platform-Benutzeroberfläche bietet Ihnen ein konsistentes Zuordnungserlebnis, um intelligente Zuordnungsempfehlungen zu nutzen, Zuordnungsregeln manuell zu konfigurieren und Fehler zu debuggen, die bei Ihren Zuordnungssätzen auftreten. Weitere Informationen finden Sie unter [[!DNL Data Prep] UI-Handbuch](../../data-prep/home.md). |

Weitere Informationen finden Sie unter [!DNL Data Prep], siehe [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Dashboards] {#dashboards}

[!DNL Dashboards] macht hübsche Dinge.

| Funktion | Beschreibung |
|---------|-------------|
| Intelligente Untertitel | Ein maschineller Lernalgorithmus bietet automatisch Einblicke in Ihre Profil- und Zielgruppendaten und veranschaulicht Muster und Trends über einen Zeitraum von 30 bis 90 Tagen oder 12 Monaten. Die Beschriftungen enthalten Informationen zu <ul><li>Gesamtform und Statistiken</li><li>Trends und abrupte Änderungen</li><li>Saisonale Muster</li><li>Unerwartete Anomalien</li></ul> Weitere Informationen finden Sie im [Profil-Dashboards](../../dashboards/guides/profiles.md#profiles-count-trend) und [Segmente-Dashboards](../../dashboards/guides/segments.md#audience-size-trend) Dokumentation. |
| Dashboards-Inventar | Greifen Sie auf die vorkonfigurierten Berichte der Profil-, Segment- und Ziel-Dashboards zu, einschließlich aller installierten Integrationen wie PowerBI, und zwar zentral. Weitere Informationen finden Sie unter [[!DNL Dashboards] Übersicht](../../dashboards/home.md). |
| PowerBI-Berichtsvorlagen | Erstellen, anpassen oder erweitern Sie Metriken aus den Datenmodellen für Profil-, Segment- und Zielberichtsdaten mithilfe neuer Power BI-Diagramme. Der automatisierte Installations-Workflow ermöglicht es Ihnen, innerhalb der PowerBI-Umgebung Ihre Marketing-Einblicke in Ihrem Unternehmen freizugeben. Weitere Informationen finden Sie unter [[!DNL Dashboards] Übersicht](../../dashboards/home.md). |

Weitere Informationen finden Sie unter [!DNL Dashboards], siehe [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## Query Service {#query-service}

[!DNL Query Service] ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus der [!DNL Data Lake] und erfassen Sie die Abfrageergebnisse als neuen Datensatz zur Verwendung in Berichten, Data Science Workspace oder zur Aufnahme in das Echtzeit-Kundenprofil.

| Funktion | Beschreibung |
|----------------------|-----------------------|
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

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Segmentübereinstimmung | Segment Match ist ein Dienst für die Zusammenarbeit mit Daten, der es zwei oder mehr Platform-Benutzern ermöglicht, Daten basierend auf gemeinsamen Kennungen auf sichere, verwaltete und datenschutzfreundliche Weise auszutauschen. Weitere Informationen finden Sie unter [Übersicht über Segmentübereinstimmungen](../../segmentation/ui/segment-match/overview.md). |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierung – Übersicht](../../segmentation/home.md).
