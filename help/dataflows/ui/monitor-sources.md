---
description: Erfahren Sie, wie Sie mit dem Monitoring-Dashboard die in den Data Lake aufgenommenen Daten überwachen können.
title: Überwachen der Data Lake-Aufnahme
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 75970d41a316c97d98ebf6cefd3bfa0e58173030
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 15%

---

# Überwachen der Data Lake-Aufnahme

>[!IMPORTANT]
>
>Streaming-Quellen wie die [HTTP-API-Quelle](../../sources/connectors/streaming/http.md) werden derzeit nicht vom Überwachungs-Dashboard unterstützt. Derzeit können Sie das Dashboard nur zur Überwachung von Batch-Quellen verwenden.

Sie können das Überwachungs-Dashboard in der Adobe Experience Platform-Benutzeroberfläche verwenden, um Metriken rund um Ihre Datenaufnahme und Datenaufbewahrungsprozesse im Data Lake abzurufen. Verwenden Sie die Diagramme in der -Benutzeroberfläche, um Aufnahme- und Aufbewahrungstrends im Laufe der Zeit zu überwachen und die Leistung über alle Quellen und Datenflüsse hinweg zusammenzufassen.

Lesen Sie dieses Dokument, um zu erfahren, wie Sie mit dem Monitoring-Dashboard die gesamte Datenverarbeitung im Data Lake überwachen können, einschließlich Aufnahme und Aufbewahrung.

## Erste Schritte {#get-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Experience Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   * [Datenflussausführungen](../../sources/notifications.md): Datenflussausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Häufigkeitskonfiguration ausgewählter Datenflüsse basieren.
* [Quellen](../../sources/home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Identity Service](../../identity-service/home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kundinnen und Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
* [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Verwenden des Dashboards „Monitoring“ zur Data-Lake-Aufnahme

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Quellaufnahme"
>abstract="Die Quellaufnahmen-Ansicht enthält Informationen zum Status der Datenaktivität und zu Metriken im Data-Lake-Dienst, einschließlich der aufgenommenen und fehlgeschlagenen Einträge. Weitere Informationen zu Metriken und Diagrammen finden Sie im Handbuch zur Metrikdefinition."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Details zur Datenflussausführung"
>abstract="Die Quellverarbeitung enthält Informationen zum Status der Datenaktivität und zu Metriken im Data-Lake-Dienst, einschließlich der aufgenommenen und fehlgeschlagenen Einträge. Weitere Informationen zu Metriken und Diagrammen finden Sie im Handbuch zur Metrikdefinition."
>text="Learn more in documentation"

Wählen Sie **[!UICONTROL Data lake]** aus der Hauptkopfzeile im Monitoring-Dashboard aus, um Ihre Data-Lake-Aufnahmerate anzuzeigen.

![Das Überwachungs-Dashboard mit der ausgewählten Quellenkarte.](../assets/ui/monitor-sources/data-lake.png)

Das [!UICONTROL Ingestion rate] Diagramm zeigt Ihre Datenaufnahmerate basierend auf Ihrem konfigurierten Zeitrahmen an. Standardmäßig zeigt das Überwachungs-Dashboard die Aufnahmeraten der letzten 24 Stunden an. Anweisungen zum Konfigurieren Ihres Zeitrahmens finden Sie im Handbuch unter [Konfigurieren des Zeitrahmens für die Überwachung](monitor.md#configure-monitoring-time-frame).

Das Diagramm ist standardmäßig für die Anzeige aktiviert. Um das Diagramm auszublenden, wählen Sie **[!UICONTROL Metrics and graphs]** aus, um den Umschalter zu deaktivieren und das Diagramm auszublenden.

![Das Diagramm mit den Metriken zur Aufnahmerate.](../assets/ui/monitor-sources/metrics-graph.png)

Im unteren Teil des Dashboards wird eine Tabelle angezeigt, die den aktuellen Metrikbericht für alle vorhandenen Datenflüsse der Quellen umreißt.

![Die Tabelle mit den Metriken des Monitoring-Dashboards.](../assets/ui/monitor-sources/metrics-table.png)

| Metriken | Beschreibung |
| --- | --- |
| Empfangene Einträge | Die Gesamtzahl der von einer bestimmten Quelle empfangenen Datensätze. |
| Aufgenommene Einträge | Die Gesamtzahl der in den Data Lake aufgenommenen Datensätze. |
| Gelöschte Einträge | Die Gesamtzahl der gelöschten Datensätze aufgrund von Data-Lake-Aufbewahrungseinstellungen oder geänderten Datenerfassungsvorgängen. |
| Übersprungene Einträge | Die Gesamtzahl der übersprungenen Datensätze. Ein übersprungener Datensatz bezieht sich auf Felder, die übersprungen wurden, weil sie für die Aufnahme nicht erforderlich waren. Wenn Sie beispielsweise einen Quelldatenfluss mit aktivierter partieller Aufnahme erstellen, können Sie einen akzeptablen Schwellenwert für die Fehlerrate konfigurieren. Während des Aufnahmevorgangs überspringt die Aufnahme Datensätze von Feldern, die nicht erforderlich sind, z. B. Identitätsfelder, solange sie sich innerhalb des Fehlerschwellenwerts befinden. |
| Fehlgeschlagene Einträge | Die Gesamtzahl der Datensätze, die aufgrund von Fehlern nicht aufgenommen werden konnten. |
| Aufgenommene Rate | Der Prozentsatz der aufgenommenen Datensätze auf der Basis der Gesamtzahl der empfangenen Datensätze. |
| Fehlgeschlagene Datenflüsse insgesamt | Die Gesamtzahl der fehlgeschlagenen Datenflüsse. |

{style="table-layout:auto"}

Sie können Ihre Daten mithilfe der Optionen weiter filtern, die oben in der Tabelle Metriken bereitgestellt werden:

| Filteroptionen | Beschreibung |
| --- | --- |
| Durchsuchen | Verwenden Sie die Suchleiste, um Ihre Ansicht nach einem einzelnen Quelltyp zu filtern. |
| Quellen | Wählen Sie **[!UICONTROL Sources]** aus, um Ihre Ansicht zu filtern und Metrikdaten nach Quelltyp anzuzeigen. Dies ist die Standardanzeige, die vom Monitoring-Dashboard verwendet wird. |
| Datenflüsse | Wählen Sie **[!UICONTROL Dataflows]** aus, um Ihre Ansicht zu filtern und Metrikdaten pro Datenfluss anzuzeigen. |
| Nur Fehlschläge zeigen | Wählen Sie **[!UICONTROL Show failures only]** aus, um Ihre Ansicht zu filtern und nur Datenflüsse anzuzeigen, die Aufnahmefehler gemeldet haben. |
| Meine Quellen | Sie können Ihre Ansicht mithilfe des Dropdown-Menüs [!UICONTROL My sources] weiter filtern. Verwenden Sie das Dropdown-Menü, um Ihre Ansicht nach Kategorie zu filtern. Alternativ können Sie **[!UICONTROL All sources]** auswählen, um Metriken für alle - oder -Quellen anzuzeigen, oder **[!UICONTROL My sources]** auswählen, um nur die Quellen anzuzeigen, für die Sie über ein entsprechendes -Konto verfügen. |

{style="table-layout:auto"}

Um die Anzeige der Spalten anzupassen, wählen Sie das Symbol für die Spalteneinstellungen ![Spalten-Symbol](/help/images/icons/column-settings.png).

![Das Monitoring-Dashboard mit ausgewähltem Symbol für die Spalteneinstellungen.](../assets/ui/monitor-sources/edit-columns.png)

Wählen Sie anschließend im Fenster *[!UICONTROL Customize table]* die Spalten aus, die Ihr Dashboard anzeigen soll. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Apply]** aus.

![Das Popup-Fenster „Spalte anpassen“ im Monitoring-Dashboard.](../assets/ui/monitor-sources/customize-table.png)

Um die Daten zu überwachen, die in einen bestimmten Datenfluss aufgenommen werden, wählen Sie das Filtersymbol (![) ](/help/images/icons/filter-add.png) einer Quelle aus.

>[!TIP]
>
>Sie können das Überwachungs-Dashboard verwenden, um Datenlöschmetriken für gelöschte Datensätze mithilfe von Datenspeicherungsrichtlinien zu überwachen. Weitere Informationen zur Datenaufbewahrung finden Sie im Handbuch unter [ von Richtlinien zur Datenaufbewahrung](../../catalog/datasets/user-guide.md#data-retention-policy).

![Überwachen Sie einen bestimmten Datenfluss, indem Sie das Filtersymbol neben einer bestimmten Quelle auswählen.](../assets/ui/monitor-sources/monitor-dataflow.png)

Die Tabelle Metriken wird in eine Tabelle mit aktiven Datenflüssen aktualisiert, die der ausgewählten Quelle entsprechen. In diesem Schritt können Sie zusätzliche Informationen zu Ihren Datenflüssen anzeigen, einschließlich des entsprechenden Datensatzes und Datentyps sowie eines Zeitstempels, der angibt, wann sie zuletzt aktiv waren.

Um einen Datenfluss weiter zu untersuchen, wählen Sie das Filtersymbol (![) ](/help/images/icons/filter-add.png) einem Datenfluss aus.

![Die Datenfluss-Tabelle im Monitoring-Dashboard.](../assets/ui/monitor-sources/select-dataflow.png)

Als Nächstes gelangen Sie zu einer Schnittstelle, die alle Iterationen der Datenflussausführung des ausgewählten Datenflusses auflistet.

Datenflussausführungen stellen eine Instanz der Datenflussausführung dar. Wenn ein Datenfluss beispielsweise so geplant ist, dass er stündlich um 9 :00, :00 Uhr und :00 Uhr morgens ausgeführt wird, gibt es drei Instanzen eines Flussdurchgangs. Flussausführungen sind spezifisch für Ihre bestimmte Organisation.

Um Metriken einer bestimmten Iteration der Datenflussausführung zu überprüfen, wählen Sie das Filtersymbol ![filter](/help/images/icons/filter-add.png) neben Ihrem Datenfluss aus.

![Die Metrikseite „Datenflussausführung“.](../assets/ui/monitor-sources/dataflow-page.png)

Auf der Seite mit den Datenflussausführungs-Details können Sie Metriken und Informationen der ausgewählten Iteration anzeigen.

![Die Seite mit den Datenflussausführungs-Details.](../assets/ui/monitor-sources/dataflow-run-details.png)

| Details zur Datenflussausführung | Beschreibung |
| --- | --- |
| Aufgenommene Einträge | Die Gesamtzahl der Datensätze, die aus der Datenflussausführung aufgenommen wurden. |
| Fehlgeschlagene Einträge | Die Gesamtzahl der Datensätze, die aufgrund von Fehlern in der Datenflussausführung nicht aufgenommen wurden. |
| Gesamtzahl der Dateien | Die Gesamtzahl der Dateien in der Datenflussausführung. |
| Datengröße | Die Gesamtgröße der in der Datenflussausführung enthaltenen Daten. |
| ID der Datenflussausführung | Die ID der Iteration der Datenflussausführung. |
| Organisations-ID | Die ID der Organisation, in der der Datenfluss erstellt wurde. |
| Status | Der Status der Datenflussausführung. |
| Anfang der Datenflussausführung | Ein Zeitstempel, der angibt, wann die Datenflussausführung gestartet wurde. |
| Ende der Datenflussausführung | Ein Zeitstempel, der angibt, wann die Datenflussausführung beendet wurde. |
| Datensatz | Der zum Erstellen des Datenflusses verwendete Datensatz. |
| Datentyp | Der Typ der Daten, die sich im Datenfluss befanden. |
| Teilweise Aufnahme | Die partielle Batch-Aufnahme bietet die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten konfigurierbaren Schwellenwert aufzunehmen. Mit dieser Funktion können Sie alle Ihre korrekten Daten erfolgreich in Experience Platform aufnehmen, während alle Ihre falschen Daten separat mit Informationen darüber, warum sie ungültig sind, in Batches erfasst werden. Sie können die partielle Aufnahme während des Erstellungsprozesses eines Datenflusses aktivieren. |
| Fehlerdiagnose | Fehlerdiagnose weist die Quelle an, Fehlerdiagnosen zu erstellen, auf die Sie später bei der Überwachung Ihrer Datensatzaktivität und des Datenflussstatus verweisen können. Sie können die Fehlerdiagnose während des Erstellungsprozesses eines Datenflusses aktivieren. |
| Fehlerzusammenfassung | Bei einer fehlgeschlagenen Datenflussausführung zeigt die Fehlerzusammenfassung einen Fehlercode und eine Beschreibung an, um zusammenzufassen, warum die Iteration der Ausführung fehlgeschlagen ist. |

{style="table-layout:auto"}

Wenn bei der Ausführung des Datenflusses Fehler auftreten, können Sie über die [!UICONTROL Dataflow run errors] nach unten auf der Seite scrollen.

Verwenden Sie den Abschnitt [!UICONTROL Records failed] , um Metriken zu Datensätzen anzuzeigen, die aufgrund von Fehlern nicht aufgenommen wurden. Um einen umfassenden Fehlerbericht anzuzeigen, wählen Sie **[!UICONTROL Preview error diagnostics]** aus. Um eine Kopie Ihrer Fehlerdiagnose und Ihres Dateimanifests herunterzuladen, wählen Sie **[!UICONTROL Download]** aus und kopieren Sie dann den Beispiel-API-Aufruf, der mit der [!DNL Data Access]-API verwendet werden soll.

>[!NOTE]
>
>Sie können die Fehlerdiagnose nur verwenden, wenn die Funktion während des Erstellungsprozesses der Quellverbindung aktiviert wurde.

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie gelernt, wie Sie die Data-Lake-Aufnahmerate mithilfe des **[!UICONTROL Monitoring]**-Dashboards überwachen. Außerdem haben Sie gelernt, Fehler zu identifizieren, die Datenflussfehler während der Aufnahme verursachen. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Identitätsdaten überwachen](./monitor-identities.md).
* [Überwachen von ](./monitor-profiles.md).
