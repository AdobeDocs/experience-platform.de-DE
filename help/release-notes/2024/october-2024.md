---
title: Adobe Experience Platform – Versionshinweise, Oktober 2024
description: Versionshinweise von Oktober 2024 für Adobe Experience Platform.
exl-id: 5e2112b8-2a0a-4c1e-af3e-b00d8cc4f4cf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 26%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 29. Oktober 2024**

Aktualisierungen vorhandener Funktionen und Dokumentationen in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Datenerfassung](#data-collection-)
- [Ziele](#destinations)
- [Segmentierungs-Service](#segmentation-service)
- [Sandboxes](#sandboxes)
- [Quellen](#sources)

## Dashboards {#dashboards}

Experience Platform bietet mehrere Dashboards, in denen Sie wichtige Einblicke in die Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Data Distiller-Vorlagen | Erkunden Sie mehrere Vorlagen, um strukturierte Einblicke in Zielgruppendaten zu erhalten. Verwenden Sie Dashboards wie **Erweitert [!UICONTROL Zielgruppenüberschneidungen]**, **[!UICONTROL Zielgruppenvergleich]**, **[!UICONTROL Zielgruppentrends]** und **[!UICONTROL Zielgruppenidentitätsüberschneidungen]** um datengesteuerte Entscheidungen zu treffen, die Segmentierung zu optimieren und Interaktionsstrategien zu verbessern. Weitere Informationen finden [ im Handbuch zu Data Distiller](../../dashboards/sql-insights-query-pro-mode/templates/overview.md)Vorlagen . |
| Erweiterte Zielgruppenüberschneidungen | Analysieren Sie Zielgruppenüberschneidungen schnell für bestimmte Zielgruppen oder sehen Sie sich alle Überschneidungen an, um wertvolle Einblicke in Ihren gesamten Zielgruppensatz zu erhalten. Nutzen Sie diese Erkenntnisse, um die Segmentierung zu verfeinern, redundantes Messaging zu reduzieren und zielgerichtetere Kampagnen für eine verbesserte Marketing-Effizienz zu erstellen. Weitere Informationen finden Sie [ Handbuch ](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md) erweiterte Zielgruppenüberschneidungen . |
| Verbesserungen beim Zielgruppenvergleich | Zeigen Sie mithilfe des Dashboards **Zielgruppenvergleich“ einen Vergleich von Schlüsselmetriken zwischen verschiedenen Zielgruppengruppen**. Mit diesem Dashboard können Sie bestimmte Zeitrahmen und KPIs wie Zielgruppengröße und Identitätszusammensetzung auswählen, um fundiertere Entscheidungen über Zielgruppensegmentierung und Zielgruppenbestimmungsstrategien zu treffen. Weitere Informationen finden [ im Handbuch ](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md) Zielgruppenvergleich . |
| Visualisierung von Zielgruppen-Trends | Analysieren Sie Zielgruppenmetriken im Zeitverlauf mit dem Dashboard **[!UICONTROL Zielgruppentrends]**. Visualisieren Sie Trends für die Zielgruppengröße, die Anzahl der Identitäten und die Anzahl der einzelnen Identitätsprofile, um die Zielgruppenentwicklung zu überwachen, das Wachstum zu messen und Ihre Interaktionsstrategien zu verfeinern. Weitere Informationen finden Sie [ Handbuch ](../../dashboards/sql-insights-query-pro-mode/templates/trends.md) Zielgruppen-Trends . |
| Analyse der Identitätsüberschneidungen | Analysieren Sie Identitätsüberschneidungen in ausgewählten Zielgruppen mit dem Dashboard **[!UICONTROL Zielgruppenidentitätsüberschneidungen]** . Zeigen Sie Identitätstrends und -aufschlüsselungen an, um zu verstehen, wie verschiedene Identitätstypen innerhalb Ihrer Zielgruppe zusammenhängen, und verbessern Sie so die Identitätszuordnung und die Genauigkeit der Kundensegmentierung. Weitere Informationen finden Sie [ Handbuch zur ](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md) von Identitätsüberschneidungen der Zielgruppe . |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenerfassung {#collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an die Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Nicht-Adobe-Ziele verteilt werden können.

**Neue Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Tags und Erweiterungen | Adobe Analytics JSON-Ansicht | Sie können jetzt die Adobe Analytics-Tags-Erweiterung verwenden, um eVars, Props und Ereigniseinstellungen als JSON zu untersuchen, die jetzt in die Web-SDK-Erweiterung aufgenommen und zur Bearbeitung exportiert werden können. Sie können diese Daten auch hochladen oder kopieren und auf Ihrem Gerät speichern. Weitere Informationen finden Sie in der Dokumentation [&#128279;](../../tags/extensions/client/analytics/overview.md) Erweiterung Adobe Analytics . |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Übersicht über die Datenerfassung](../../collection/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| ----------- | ----------- |
| [Array-Exportunterstützung allgemein verfügbar](../../destinations/ui/export-arrays-maps-objects.md) | Alle -Kunden können jetzt die Option **[!UICONTROL Berechnetes Feld hinzufügen]** beim Aktivieren von Zielgruppen *für dateibasierte Ziele* verwenden, um ganze Arrays oder Elemente von Arrays zu exportieren. Beachten Sie, dass Sie weiterhin die Funktion `array_to_string` verwenden müssen, um das Array in der Zieldatei in eine Zeichenfolge zu reduzieren. <br> ![Hinzufügen der berechneten Feldauswahl mit Funktionen und Feldern.](../2024/assets/october/array-export.gif "Fügen Sie ein berechnetes Feld mit einer Auswahl der Funktion array_to_string und dem Array „Organisations“ hinzu."){width="250" align="center" zoomable="yes"} |
| [Verbesserungen der Berichtsgenauigkeit für Streaming-Ziele](/help/destinations/ui/export-datasets.md) | Ab Oktober 2024 führt Adobe ein Update ein, um die Berichtsgenauigkeit für Streaming-Ziele zu erhöhen. Durch diese Verbesserung wird eine bessere Abstimmung zwischen der Berichterstellung für Experience Platform und die Zielplattformen sichergestellt. <br> Vor diesem Update wurden bei **[!UICONTROL Identitäten fehlgeschlagen]** alle Aktivierungsversuche einbezogen. Nach diesem Update wird nur der letzte Aktivierungsversuch in die Gesamtanzahl einbezogen. <br> Diese Verbesserung gilt derzeit für das [Ziel von Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md) wird aber schrittweise für andere Experience Platform-Streaming-Ziele eingeführt. Nach dieser Verbesserung kann es bei Benutzenden des [Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md)Ziels zu einem erwarteten Rückgang der Anzahl **[!UICONTROL Identitäten fehlgeschlagen]** kommen. |
| Auswirkungen der flexiblen Zielgruppenauswertung auf [Batch-Zielgruppenaktivierung](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Wenn Sie [flexible Zielgruppenauswertung](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) für Zielgruppen ausführen, die bereits nach der Segmentauswertung aktiviert werden sollen, werden die Zielgruppen aktiviert, sobald der flexible Zielgruppenauswertungsauftrag abgeschlossen ist, unabhängig von vorherigen täglichen Aktivierungsaufträgen. <br> Dies kann dazu führen, dass Zielgruppen basierend auf Ihren Aktionen mehrmals täglich exportiert werden. |

{style="table-layout:auto"}

Lesen Sie für Weitere Informationen den [Überblick über die Ziele](../../destinations/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| [!BADGE Eingeschränkte Verfügbarkeit]{type=Informative} Flexible Zielgruppenauswertung | Mit der flexiblen Zielgruppenauswertung können Sie bei Bedarf schnell neue Zielgruppen für zeitkritische Kommunikation erstellen. Weitere Informationen zu dieser neuen Funktion finden Sie in der [Audience Portal-Dokumentation](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation). |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie unter [Segmentierung - Übersicht](../../segmentation/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um diese Anforderung zu erfüllen, stellt Experience Platform Sandboxes bereit, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Sandbox-Tooling-Paketfreigabe | Sie können jetzt Sandbox-Tools verwenden, um Sandbox-Konfigurationen zwischen Sandboxes über verschiedene Organisationen hinweg einfach zu exportieren und zu importieren. Es sind jetzt zwei Kategorien von freigegebenen Paketen verfügbar:<br><ul><li>**[Privates Paket](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** Verwenden Sie die private Paketfreigabe für Organisationen, die die Freigabeanfrage von der Quellorganisation genehmigt haben.</li><li>**[Öffentliches Paket](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** Öffentliche Pakete können ohne zusätzliche Genehmigungen freigegeben werden und können einfach über die Payload des Pakets importiert werden.</li></ul><br>Weitere Informationen zu diesen Funktionen finden Sie im Handbuch zum [Freigeben von Paketen in Unternehmen](../../sandboxes/ui/sharing-packages-across-orgs.md). |
| [Package-Freigabe](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) in der Sandbox-Tooling-API | Verwenden Sie die Sandbox-Tooling-API , um Anfragen an zwei neue Endpunkte zu senden: `/handshake` und `/transfer` für die organisationsübergreifende Freigabe, den Abruf und die Erstellung von Anfragen zur Paketfreigabe. Dem `/packages`-Endpunkt wurde eine zusätzliche Anfrage hinzugefügt, um die Payload eines Pakets abzurufen. |

{style="table-layout:auto"}

Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen in Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern aufzunehmen.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für das Filtern von standardmäßigen Aktivitätsentitäten in [!DNL Marketo Engage] | Sie können die [!DNL Flow Service]-API verwenden, um bei der Aufnahme von Daten aus Ihrer [!DNL Marketo Engage] Aktivitätsentitäten nach Standard-Aktivitätsentitäten zu filtern. Weitere Informationen finden Sie im Handbuch [Filtern [!DNL Marketo] standardmäßige ](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage)). |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).
