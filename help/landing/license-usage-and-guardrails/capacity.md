---
title: Lizenznutzung und -kapazität
description: Erfahren Sie mehr über Ihre Lizenznutzung und Kapazitätsbeschränkungen in Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 1a7a074a455542bb1438b2cbf199d79229142389
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 5%

---


# Lizenznutzung und -kapazitäten

>[!AVAILABILITY]
>
>Um diese Funktion verwenden zu können, müssen Sie über die folgenden Berechtigungen verfügen:
>
>- **Anzeigen des Dashboards zur Lizenznutzung**
>   - Mit dieser Berechtigung können **die Startseite** Kapazität anzeigen.
>- **Verwalten von Sandboxes**
>   - Mit dieser Berechtigung können **** Kapazitätszuweisungen „bearbeiten“.
>   - Darüber hinaus **muss** Zugriff auf alle Sandboxes zugewiesen werden, damit Sie (**)** Sandbox-Kapazität bearbeiten können.
>
>Weitere Informationen zu Berechtigungen in Experience Platform finden Sie unter [Zugriffssteuerung - Übersicht](/help/access-control/home.md#permissions)
>
>Wenn Sie außerdem eine Streaming-Segmentierung mit hohem Durchsatz erworben haben **können** Ihre Kapazitäten mithilfe von Kapazität zuweisen. Wenden Sie sich zur Aktualisierung Ihrer Kapazitäten an die Adobe-Kundenunterstützung.

In Adobe Experience Platform informieren Sie die -Kapazitäten, wenn Ihr Unternehmen eine Ihrer Leitplanken überschritten hat, und erhalten Informationen zur Behebung dieser Probleme.

Weitere Informationen zu Leitplanken in Experience Platform finden Sie in der Übersicht über [Real-Time CDP-Leitplanken](../../rtcdp/guardrails/overview.md).

## Kapazitätsverhalten {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Streaming-Durchsatz"
>abstract="Der Wert für den Streaming-Durchsatz misst die kombinierten Spitzenwerte der eingehenden Ereignisse pro Sekunde für die Streaming-Aufnahme in Profile in Produktions- und Entwicklungs-Sandboxes."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Anzahl der Streaming-Zielgruppen"
>abstract="Die maximale Anzahl von Streaming-Zielgruppen pro Sandbox. Diese Anzahl enthält auch die Anzahl der Edge-Zielgruppen in Ihrer Sandbox."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Edge-Zielgruppen"
>abstract="Die maximale Anzahl von Edge-Zielgruppen pro Sandbox."

Derzeit unterstützt Capacity die folgenden Services:

- Streaming-Segmentierung 
- Streaming-Aufnahme
- Edge-Segmentierung

Innerhalb dieser Services werden die folgenden Leitplanken verfolgt:

- Die maximale Anzahl von Streaming-Zielgruppen ist 500
- Die maximale Anzahl von Edge-Zielgruppen ist 150
- Der kombinierte anfängliche Durchsatz für die Streaming-Aufnahme beträgt 1500 Datensätze pro Sekunde (rps)
   - Dieser kombinierte Streaming-Durchsatz misst die kombinierten Spitzenwerte der eingehenden Ereignisse pro Sekunde für die Streaming-Aufnahme in das Echtzeit-Kundenprofil über Ihre Produktions- und Entwicklungs-Sandboxes hinweg.
   - Sie können zusätzliche Streaming-Segmentierungsunterstützung für bis zu 13.500 Datensätze pro Sekunde erwerben. Weitere Informationen zum Kauf zusätzlicher Berechtigungen finden Sie in der [Real-Time CDP-Produktbeschreibung](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
- Der kombinierte Durchsatz für die Edge-Segmentierung beträgt 1.500 Datensätze pro Sekunde (rps)

Die Zielgruppenkapazität befindet sich auf **Sandbox**-Ebene. Das bedeutet, dass Sie für jede Sandbox in Ihrem Unternehmen 500 Streaming-Zielgruppen haben können, davon 150 Edge-Zielgruppen.

Die Streaming-Durchsatzkapazität befindet sich auf **Organisations**-Ebene und kann an Ihre individuellen Sandboxes verteilt werden. Beispielsweise können Sie mit den 1.500 U/s für den Streaming-Aufnahme-Durchsatz Ihre Produktions-Sandbox auf 1.300 U/s und Ihre Entwicklungs-Sandbox auf 200 U/s festlegen.

Experience Platform berechnet den Durchsatz der Sandbox in rollierenden Intervallen von 15 Minuten. Dieser Durchsatz wird in Echtzeit gemessen, wobei die Daten alle 60 Sekunden aktualisiert werden.

Wenn Ihre Nutzung 80 % und 90 % Ihrer lizenzierten Kapazität erreicht, gibt Experience Platform einen Warnhinweis aus, der Sie darüber informiert, dass Sie die Höchstkapazität Ihrer angegebenen Kapazität erreichen. Sie können die Einstellungen ändern, um den Prozentsatz der Kapazität anzupassen, um den Warnhinweis zu erhalten, oder den Warnhinweis vollständig entfernen.

Wenn Ihre Nutzung 100 % Ihrer lizenzierten Kapazität überschreitet, wird dies als Verstoß gegen Ihre Kapazität angesehen. Wenn Sie Ihre Kapazität nicht einhalten, gelten die folgenden Einschränkungen:

>[!NOTE]
>
>Wenn Sie Zugriff auf Adobe Journey Optimizer haben, gelten **folgenden Einschränkungen**.

- Ereignisdaten **können** aus der Streaming-Personalisierung entfernt werden, wenn die Ereignisverarbeitungswarteschlange 12 Stunden überschreitet
- Entfernte Ereignisdaten werden **nicht** in das Profil aufgenommen
   - Sie können sehen, wann Ereignisse entfernt wurden
   - Ereignisse sind entsprechend Ihren Berechtigungen im Data Lake verfügbar
   - Sie *können* Abfrage-Service verwenden, um die Daten bei Bedarf direkt erneut aufzunehmen

## Zugriff {#access}

Um auf die Kapazitätsübersicht zuzugreifen, wählen Sie **[!UICONTROL License usage]** und dann **[!UICONTROL Capacity]** aus.

![Die Methode für den Zugriff auf den Abschnitt „Kapazität“ ist hervorgehoben.](/help/landing/images/capacity/access-capacity.png)

Die Seite „Kapazitätsübersicht“ wird angezeigt und enthält Informationen, einschließlich eines Verlaufs von Warnhinweisen sowie Details zu den Kapazitäten Ihres Unternehmens.

![Die Seite „Kapazitätsübersicht“ wird angezeigt, die den Warnhinweisverlauf und die Abschnitte mit den Kapazitätsdetails anzeigt.](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

### Warnhinweisverlauf {#alert-history}

Im Abschnitt **[!UICONTROL Alert history]** wird eine Liste der letzten Kapazitätsverletzungen in Ihrer Organisation angezeigt.

![Der Abschnitt Warnhinweisverlauf wird angezeigt.](/help/landing/images/capacity/alert-history.png)

| Spaltenname | Beschreibung |
| ----------- | ----------- |
| Sandbox | Der Name der Sandbox, in der die Kapazitätsverletzung aufgetreten ist. |
| Warnhinweis | Die Kapazität, die in der Sandbox verletzt wurde. |
| Zeitstempel | Die Daten und die Uhrzeit, zu der der Verstoß aufgetreten ist. |

Um einen vollständigen Verlauf der Warnhinweise für Ihre Organisation anzuzeigen, wählen Sie das ![Ellipsensymbol](/help/images/icons/more.png) gefolgt von **[!UICONTROL View all]** aus.

![Der vollständige Warnhinweisverlauf wird für eine Organisation angezeigt.](/help/landing/images/capacity/full-alert-history.png)

### Streaming-Kapazitäten {#streaming-capacities}

Im Abschnitt Streaming-Kapazitäten finden Sie Informationen zu den Streaming-Kapazitäten Ihres Unternehmens. Insbesondere werden in diesem Abschnitt Kapazitätsinformationen zum Streaming-Durchsatz und zu Streaming-Zielgruppen angezeigt. Sie können diese Informationen pro Sandbox filtern und den Lookback-Zeitraum ändern.

![Der Sandbox-Selektor und die Datumsauswahl für den Lookback-Zeitraum sind hervorgehoben.](/help/landing/images/capacity/filter-sandbox-and-date.png)

#### Streaming-Durchsatz {#streaming-throughput}

Im Abschnitt **[!UICONTROL Streaming throughput]** werden Informationen zum Streaming-Durchsatz in den Sandboxes Ihrer Organisation angezeigt. Der Wert für den Streaming-Durchsatz misst die kombinierten Spitzenwerte der eingehenden Ereignisse pro Sekunde für die Streaming-Aufnahme in Profile.

![Der Abschnitt Streaming-Durchsatz auf der Seite mit den Kapazitätsdetails wird angezeigt.](/help/landing/images/capacity/streaming-throughput-section.png)

| Spaltenname | Beschreibung |
| ----------- | ----------- |
| Sandbox | Der Name der Sandbox. |
| Dienste | Der Service, der von der Sandbox verwendet wird. Derzeit wird nur der Wert Profil unterstützt. |
| Nutzung (Spitzenwert) | Der maximale Streaming-Durchsatz von Daten in der Sandbox innerhalb des ausgewählten Lookback-Zeitraums. |
| Kapazität | Der maximale Spitzen-Streaming-Durchsatz für die Sandbox. |
| Verletzung | Wenn eine Verletzung aufgetreten ist, die Art der Verletzung für den Streaming-Durchsatz. |
| Empfohlene Aktionen | Eine Spalte, die die empfohlene Aktion zum Beheben des Verstoßes beschreibt. |

Sie können die einzelne Sandbox auswählen, um eine detailliertere Ansicht des Streaming-Durchsatzes der Sandbox anzuzeigen.

![Eine Sandbox ist im Abschnitt Streaming-Durchsatz hervorgehoben.](/help/landing/images/capacity/select-sandbox.png)

Die Seite mit den Streaming-Durchsatzdetails wird angezeigt. In einem Diagramm wird der Anforderungsdurchsatz im Vergleich zur Kapazitätsgrenze, eine Liste der Sandboxes und ihrer Durchsätze sowie eine Schaltfläche zur Zuordnung der Kapazitäten Ihres Unternehmens angezeigt.

![Die Seite Streaming-Durchsatz wird angezeigt und enthält detaillierte Informationen zum Streaming-Durchsatz für die ausgewählte Sandbox.](/help/landing/images/capacity/streaming-capacity-allocation.png)

Um die Streaming-Durchsatzkapazitäten der Organisation zu aktualisieren, wählen Sie **[!UICONTROL Allocate capacities]** aus.

![Die Schaltfläche „Kapazitäten zuweisen“ ist auf der Seite mit den Streaming-Durchsatzdetails hervorgehoben.](/help/landing/images/capacity/select-allocate.png)

Die Seite Zuordnung wird angezeigt. Auf dieser Seite können Sie die Kapazitäten für Ihre verschiedenen Sandboxes festlegen. Die Summe aller Kapazitäten **muss** der Gesamtkapazität der Organisation entsprechen.

![Die Seite „Kapazitätszuweisung“ wird angezeigt.](/help/landing/images/capacity/allocate-capacity.png)

>[!NOTE]
>
>Sie können die neue Kapazität nur in Bestellungen von **100** festlegen. Sie können beispielsweise den Wert der neuen Kapazität der Sandbox auf 300 oder 500 festlegen, diesen Wert jedoch **nicht** auf 450 festlegen.
>
>Wenn der Wert nicht in der Größenordnung von 100 liegt, wird er entsprechend auf- oder abgerundet.

Wählen Sie nach dem Aktualisieren der Kapazitätszuweisungen **[!UICONTROL Save]** aus, um die Aktualisierungen abzuschließen. Beachten Sie, dass es bis zu 10 Minuten dauern kann, bis die Änderungen in Ihrer Organisation übernommen werden.

#### Anzahl der Streaming-Zielgruppen {#streaming-audience-count}

Im Abschnitt **[!UICONTROL Streaming audience count]** werden die Anzahl der Streaming-Zielgruppen innerhalb der Sandbox sowie die maximale Anzahl der in der Sandbox zulässigen Streaming-Zielgruppen angezeigt.

![Die Abschnitte Zielgruppengröße werden angezeigt.](/help/landing/images/capacity/audience-count.png)

| Spaltenname | Beschreibung |
| ----------- | ----------- |
| Sandbox | Der Name der Sandbox. |
| Dienste | Der Service, der für die Sandbox verwendet wird. |
| Nutzung | Die Anzahl der Streaming-Zielgruppen in der Sandbox. |
| Kapazität | Die maximale Anzahl von Streaming-Zielgruppen, die in der Sandbox zulässig ist. |

### Edge-Kapazitäten {#edge-capacities}

Im **[!UICONTROL Edge capacities]** Abschnitt finden Sie Informationen zu den Edge-Kapazitäten Ihres Unternehmens. Insbesondere zeigt dieser Abschnitt Kapazitätsinformationen zum Durchsatz der Edge-Segmentierung und zu den Edge-Zielgruppen an. Sie können den Lookback-Zeitraum für die Edge-Kapazitäten der Organisation ändern.

![Der Abschnitt Edge-Kapazitäten wird angezeigt. Hier werden Informationen einschließlich des Durchsatzes der Edge-Segmentierung und der Edge-Zielgruppengröße beschrieben.](/help/landing/images/capacity/edge-capacities.png)

#### Edge-Segmentierungsdurchsatz {#edge-streaming-throughput}

Im Abschnitt **[!UICONTROL Edge segmentation throughput]** werden Informationen zum Durchsatz der Edge-Segmentierung innerhalb Ihrer Organisation und der Sandboxes Ihrer Organisation angezeigt. Der Durchsatzwert für die Edge-Segmentierung misst den kombinierten Spitzenwert der eingehenden Ereignisse pro Sekunde für die Edge-Aufnahme in das Profil.

![Der Durchsatzabschnitt zur Edge-Segmentierung wird angezeigt. Dadurch werden Informationen zum Durchsatz der Edge-Segmentierung innerhalb Ihrer Organisation und ihrer Sandboxes angezeigt.](/help/landing/images/capacity/edge-segmentation-throughput.png)

| Spaltenname | Beschreibung |
| ----------- | ----------- |
| Organisation | Der Name der Organisation. Die verfügbaren Sandboxes für die Organisation werden unter dem Namen der Organisation aufgeführt. |
| Nutzung RPS (Spitzenwert) | Der maximale Datendurchsatz in der Sandbox innerhalb des ausgewählten Lookback-Zeitraums. |
| Kapazität RPS | Der maximale Spitzendurchsatz für die Organisation. |
| Verletzung | Wenn eine Verletzung aufgetreten ist, die Art der Verletzung für den Durchsatz der Edge-Segmentierung. |
| Empfohlene Aktionen | Eine Spalte, die die empfohlene Aktion zum Beheben des Verstoßes beschreibt. |

Sie können die Organisation auswählen, um eine detailliertere Ansicht des Edge-Segmentierungsdurchsatzes der Organisation anzuzeigen.

![Die Organisation ist hervorgehoben.](/help/landing/images/capacity/select-organization.png)

Die Seite **[!UICONTROL Edge Segmentation Throughput]** wird angezeigt. Es wird ein Diagramm angezeigt, das den Anforderungsdurchsatz im Vergleich zum Kapazitätslimit anzeigt. Auf dieser Seite können Sie den Lookback-Zeitraum für das angezeigte Diagramm anpassen.

![Die Durchsatzseite &quot;Edge-Segmentierung“ wird angezeigt. In diesem Diagramm wird der Durchsatz im Vergleich zur Kapazitätsgrenze detailliert dargestellt.](/help/landing/images/capacity/edge-segmentation-throughput-details.png)

#### Größe der Edge-Zielgruppe {#edge-audience-count}

Im Abschnitt **[!UICONTROL Edge audience count]** werden die Anzahl der Edge-Zielgruppen in jeder Sandbox sowie die maximale Anzahl der Edge-Zielgruppen angezeigt, die in der Sandbox zulässig ist.

![Der Abschnitt Edge Zielgruppengröße wird angezeigt. Hier werden Informationen zur Edge-Zielgruppengröße angezeigt.](/help/landing/images/capacity/edge-audience-count.png)

| Spaltenname | Beschreibung |
| ----------- | ----------- |
| Sandbox | Der Name der Sandbox. |
| Dienste | Der Service, der für die Sandbox verwendet wird. |
| Nutzung | Die Anzahl der Zielgruppen des aufgelisteten Typs, die sich in der Sandbox befinden. |
| Kapazität | Die maximale Anzahl von Zielgruppen des aufgelisteten Typs, die in der Sandbox zulässig sind. |

## Best Practices für Streaming-Durchsatz {#streaming-throughput-suggestions}

Sie können Ihre Durchsatzverletzungen beheben, indem Sie eine der folgenden Empfehlungen umsetzen:

1. Erhöhen Sie die zugewiesene Kapazität für die Sandbox.
2. Ermitteln Sie Datenflüsse mit hohem Durchsatz im [Überwachungs-Dashboard](/help/dataflows/ui/monitor-streaming-profile.md) und wenden Sie bei Bedarf Einschränkungen oder Filter auf diese Datenflüsse an.
3. Optimieren Sie Ihre Aufnahme mithilfe der Batch-Aufnahme für Anwendungsfälle mit geringerer Latenz.

Darüber hinaus können Sie Ihre Datenflüsse betrachten und feststellen, ob Sie Ihre Datenstrategie optimieren können.

| Faktor | Was es ist | Auswirkungen auf Anwendungsfälle | Best Practices |
| --- | --- | --- | --- |
| Konvertierung von Batch zu Streaming | Batch-Workloads, die in Streaming konvertiert werden, können den Durchsatz erheblich erhöhen und sich auf die Leistung und Ressourcenzuweisung auswirken. Beispielsweise die Durchführung einer Massenaktualisierung von Profilen nach einem Ereignis ohne Ratenbeschränkungen. | Streaming-Strategien sind für Batch-Anwendungsfälle unnötig, wenn eine Verarbeitung mit geringer Latenz nicht erforderlich ist. | Bewerten Sie die Anforderungen an Anwendungsfälle. Für das Batch-Outbound-Marketing sollten Sie [Batch-Aufnahme](/help/ingestion/batch-ingestion/overview.md) anstelle von Streaming verwenden, um die Datenaufnahme effizienter zu verwalten. |
| Unnötige Datenaufnahme | Die Aufnahme von Daten, die nicht für die Personalisierung erforderlich sind, erhöht den Durchsatz, ohne einen Mehrwert zu erzielen, und verschwendet Ressourcen. Beispielsweise wird der gesamte Analytics-Traffic unabhängig von der Relevanz in Profile aufgenommen. | Übermäßige Mengen nicht relevanter Daten verursachen Rauschen, wodurch die Identifizierung wirkungsvoller Datenpunkte erschwert wird. Außerdem kann es beim Definieren und Verwalten von Audiences und Profilen zu Reibungen kommen. | Nehmen Sie nur Daten auf, die für Ihre Anwendungsfälle erforderlich sind. Stellen Sie sicher, dass Sie unnötige Daten herausfiltern.<ul><li>**Adobe Analytics**: Verwenden Sie [Filterung auf Zeilenebene](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) um die Datenaufnahme zu optimieren.</li><li>**Quellen**: Verwenden Sie die [[!DNL Flow Service] API zum Filtern von Daten auf Zeilenebene](/help/sources/tutorials/api/filter.md) für unterstützte Quellen wie [!DNL Snowflake] und [!DNL Google BigQuery].</li></li>**Edge-Datenstrom**: Konfigurieren Sie [dynamische ](/help/datastreams/configure-dynamic-datastream.md)), um Traffic aus WebSDK auf Zeilenebene zu filtern.</li></ul> |

## Best Practices für den Durchsatz der Edge-Segmentierung {#edge-best-practices}

Sie können Verstöße gegen den Durchsatz der Edge-Segmentierung beheben, indem Sie eine der folgenden Empfehlungen umsetzen:

1. Identifizieren Sie Datenströme mit hohem Durchsatz im [Monitoring-Dashboard](/help/dataflows/ui/monitor-edge.md) und wenden Sie bei Bedarf Einschränkungen oder Filter auf diese Datenströme an.
2. Optimieren Sie Ihre Aufnahme mithilfe der Batch-Aufnahme für Anwendungsfälle mit geringerer Latenz.
3. Wenden Sie sich an den Adobe-Kundendienst, wenn weiterhin Probleme auftreten.

## Videoüberblick {#video}

Das folgende Video bietet einen Überblick über die Kapazität.

>[!VIDEO](https://video.tv.adobe.com/v/3475272/?learn=on&enablevpops)

## Häufig gestellte Fragen {#faq}

Im folgenden Abschnitt werden häufig gestellte Fragen zu den Funktionen von beschrieben.

### Kann ich eine maximale kombinierte Durchsatzbegrenzung haben, die sich auf weniger als mein Zielmaximum summiert?

+++ Antwort

Nein. Die maximale kombinierte Durchsatzbegrenzung **muss** muss bis zur Leitplanke Ihres Unternehmens summiert werden.

+++

### Was passiert, wenn ich meine maximale Kapazität übertreffe?

+++ Antwort

Dies hängt davon ab, welche Kapazität überschritten wird.

Wenn Sie die maximal zulässige Anzahl von Zielgruppen überschreiten, sind Ihre übermäßigen Zielgruppen derzeit nicht betroffen. Die Möglichkeit, neue Zielgruppen zu erstellen, könnte jedoch in Zukunft eingeschränkt sein.

Wenn Sie Ihren Streaming-Durchsatz überschreiten, tritt bei Ihrer Aufnahme und Segmentierung eine Leistungslatenz auf.

+++

### Warum sollte ich meine maximalen Kapazitäten einhalten?

+++ Antwort

Das Arbeiten mit Ihren maximalen Kapazitäten stellt sicher, dass Ihre Daten konsistent bleiben und Ihre Datenintegrität intakt bleibt.

Sie stellen eine konsistente Leistung während Spitzenzeiten sicher und vermeiden technische Probleme, die sich negativ auf die Systemleistung auswirken und Ihre nachgelagerten Kundenerlebnisse beeinträchtigen könnten. Dies führt letztendlich zu einer Verbesserung Ihrer Datenhygiene und der Gesamtsystemleistung.

+++

### Was sind die Best Practices für die Verwaltung des Streaming-Aufnahmedurchsatzes?

+++ Antwort

Um den Durchsatz bei der Streaming-Aufnahme am besten zu verwalten, sollten Sie Ihre Datensätze bewerten, um sicherzustellen, dass sie Daten priorisieren, die für die Personalisierung erforderlich sind.


Wenn keine Echtzeitverarbeitung erforderlich ist, sollten Sie die Batch-Aufnahme anstelle der Streaming-Aufnahme verwenden.

+++
