---
title: Adobe Experience Platform – Versionshinweise, Oktober 2024
description: Versionshinweise von Oktober 2024 für Adobe Experience Platform.
source-git-commit: a381bdc45ee9c3c7ffb32bb7a7ec43a1233d1556
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 31%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Mittwoch, 29. Oktober 2024**

Aktualisierungen vorhandener Funktionen und Dokumentationen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Segmentierungs-Service](#segmentation-service)
- [Sandboxes](#sandboxes)
- [Quellen](#sources)

<!-- ## Dashboards {#dashboards}

Experience Platform provides multiple dashboards through which you can view important insights about your organization's data, as captured during daily snapshots.

**New or updated features**

| Feature | Description |
| --- | --- |
| Data Distiller Templates | Explore multiple templates to gain structured insights into audience data. Use dashboards like **Advanced [!UICONTROL Audience Overlaps]**, **[!UICONTROL Audience Comparison]**, **[!UICONTROL Audience Trends]**, and **[!UICONTROL Audience Identity Overlaps]** to make data-driven decisions, optimize segmentation, and enhance engagement strategies. See the [Data Distiller Templates guide](../../dashboards/sql-insights-query-pro-mode/templates/overview.md) for more details. |
| Advanced Audience Overlaps | Quickly analyze audience intersections for specific audiences or view all overlaps to uncover valuable insights across your entire audience set. Use these insights to refine segmentation, reduce redundant messaging, and create more targeted campaigns for improved marketing efficiency. See the [Advanced Audience Overlaps guide](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md) for more details. |
| Audience Comparison enhancements | View a side-by-side comparison of key metrics between different audience groups using the **Audience Comparison** dashboard. With this dashboard you can select specific time frames and KPIs, such as audience size and identity composition, to make more informed decisions about audience segmentation and targeting strategies. Read the [Audience Comparison guide](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md) for more information. |
| Audience Trends Visualization | Analyze audience metrics over time with the **[!UICONTROL Audience Trends]** dashboard. Visualize trends for audience size, number of identities, and number of single identity profiles to help you monitor audience evolution, measure growth, and refine your engagement strategies. See the [Audience Trends guide](../../dashboards/sql-insights-query-pro-mode/templates/trends.md) for more details. |
| Identity Overlaps Analysis | Analyze identity overlaps in selected audiences with the **[!UICONTROL Audience Identity Overlaps]** dashboard. View identity trends and breakdowns to understand how different identity types relate within your audience, enhancing identity stitching and improving customer segmentation accuracy. Refer to the [Audience Identity Overlaps guide](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md) for more details. |

{style="table-layout:auto"}

For more information on dashboards, including how to grant access permissions and create custom widgets, begin by reading the [dashboards overview](../../dashboards/home.md). -->

## Datenerfassung {#collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie clientseitige Kundenerlebnisdaten erfassen und an das Experience Platform-Edge Network senden können, wo sie angereichert, transformiert und an Adobe- oder Nicht-Adobe-Ziele verteilt werden können.

**Neue Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Tags und Erweiterungen | Adobe Analytics JSON-Ansicht | Sie können jetzt die Adobe Analytics-Tag-Erweiterung verwenden, um eVars-, Props- und Ereigniseinstellungen als JSON zu untersuchen, das jetzt in die Web SDK-Erweiterung aufgenommen und zur Bearbeitung exportiert werden kann. Sie können diese Daten auch hochladen oder kopieren und auf Ihrem Gerät speichern. Weitere Informationen finden Sie in der Dokumentation zur Adobe Analytics-Erweiterung ](../../tags/extensions/client/analytics/overview.md) .[ |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Datenerfassung - Übersicht](../../collection/home.md) .

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| ----------- | ----------- |
| [Array-Exportunterstützung allgemein verfügbar](../../destinations/ui/export-arrays-calculated-fields.md) | Alle Kunden können jetzt die Option **[!UICONTROL Berechnetes Feld hinzufügen]** verwenden, wenn sie Zielgruppen *für dateibasierte Ziele aktivieren*, um ganze Arrays oder Elemente von Arrays zu exportieren. Beachten Sie, dass Sie weiterhin die Funktion `array_to_string` verwenden müssen, um das Array in eine Zeichenfolge in der Zieldatei zu reduzieren. <br> ![Fügen Sie eine berechnete Feldauswahl mit Funktionen und Feldern hinzu.](../2024/assets/october/array-export.gif "Fügen Sie ein berechnetes Feld mit einer Auswahl der Funktion array_to_string und des Organisations-Arrays hinzu."){width="250" align="center" zoomable="yes"} |
| [Verbesserungen der Berichtsgenauigkeit für Streaming-Ziele](/help/destinations/ui/export-datasets.md) | Ab Oktober 2024 führt Adobe eine Aktualisierung durch, um die Berichtsgenauigkeit für Streaming-Ziele zu erhöhen. Diese Verbesserung sorgt für eine bessere Abstimmung zwischen der Berichterstellung für Experience Platform und Zielplattformen. <br> Vor dieser Aktualisierung umfasste **[!UICONTROL Identitäten fehlgeschlagen]** alle Aktivierungsversuche. Nach dieser Aktualisierung ist nur der letzte Aktivierungsversuch in der Gesamtanzahl enthalten. <br> Diese Verbesserung gilt derzeit für das Ziel [Google-Kundenabgleich](../../destinations/catalog/advertising/google-customer-match.md), wird jedoch schrittweise für andere Experience Platform-Streaming-Ziele eingeführt. Nach dieser Verbesserung kann es bei Benutzern des Ziels [Google-Kundenabgleich](../../destinations/catalog/advertising/google-customer-match.md) zu einem erwarteten Rückgang der Anzahl der **[!UICONTROL fehlgeschlagenen Identitäten]** kommen. |
| Flexible Auswirkungen der Zielgruppenbewertung auf die [Batch-Zielgruppenaktivierung](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Wenn Sie die [flexible Zielgruppenbewertung](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) für Zielgruppen ausführen, die bereits nach der Segmentbewertung aktiviert werden sollen, werden die Zielgruppen aktiviert, sobald der flexible Zielgruppenbewertungsauftrag abgeschlossen ist, unabhängig von früheren täglichen Aktivierungsaufträgen. <br> Dies kann dazu führen, dass Zielgruppen mehrmals pro Tag exportiert werden, basierend auf Ihren Aktionen. |

{style="table-layout:auto"}

Lesen Sie für Weitere Informationen den [Überblick über die Ziele](../../destinations/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| [!BADGE Eingeschränkte Verfügbarkeit]{type=Informative} Flexible Zielgruppenbewertung | Flexible Zielgruppenevaluierung ermöglicht Ihnen, schnell neue Zielgruppen auf Anforderung für zeitkritische Kommunikation zu erstellen. Weitere Informationen zu dieser neuen Funktion finden Sie in der [Dokumentation zu Audience Portal](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) . |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierungsübersicht](../../segmentation/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um dies zu erreichen, stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Freigabe von Sandbox-Toolkits | Sie können jetzt Sandbox-Tools verwenden, um Sandbox-Konfigurationen zwischen Sandboxes mühelos unternehmensübergreifend zu exportieren und zu importieren. Es sind jetzt zwei Kategorien von freigegebenen Paketen verfügbar:<br><ul><li>**[Privates Paket](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** Verwenden Sie die private Paketfreigabe für Organisationen, die die Freigabeanforderung von der Quellorganisation genehmigt haben.</li><li>**[Öffentliches Paket](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** Öffentliche Pakete können ohne zusätzliche Genehmigungen freigegeben werden und können einfach mit der Payload des Pakets importiert werden.</li></ul><br>Weiterführende Informationen zu diesen Funktionen finden Sie im Handbuch zum Thema [Freigeben von Paketen in Unternehmen](../../sandboxes/ui/sharing-packages-across-orgs.md). |
| [Paketfreigabe](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) in der Sandbox-Tool-API | Verwenden Sie die Sandbox-Tool-API, um Anforderungen an zwei neue Endpunkte zu senden: `/handshake` und `/transfer` für die unternehmensübergreifende Freigabe, den Abruf und die Erstellung von Anfragen zur Paketfreigabe. Dem `/packages` -Endpunkt wurde eine zusätzliche Anfrage hinzugefügt, um die Payload eines Pakets abzurufen. |

{style="table-layout:auto"}

Weitere Informationen zu Sandboxes finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen in Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern aufzunehmen.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für das Filtern von standardmäßigen Aktivitätsentitäten in [!DNL Marketo Engage] | Sie können die [!DNL Flow Service] -API verwenden, um bei der Aufnahme von Daten aus Ihrer [!DNL Marketo Engage]-Quelle die standardmäßigen Aktivitätsentitäten zu filtern. Lesen Sie das Handbuch zum [Filtern [!DNL Marketo] standardmäßiger Aktivitätsdaten](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage) , um weitere Informationen zu erhalten. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).
