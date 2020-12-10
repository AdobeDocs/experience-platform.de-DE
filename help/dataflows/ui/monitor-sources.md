---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;sources
description: Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Anzeigen vorhandener Datenflüsse aus dem Quellarbeitsbereich.
solution: Experience Platform
title: Überwachen von Datenflüssen
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 4d99526a592e173e3b46e1fa2a3f869b1fe5d4f2
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 3%

---


# Überwachen von Datenflüssen auf Quellen in der Benutzeroberfläche

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Anzeigen vorhandener Datenflüsse aus dem [!UICONTROL Sources] -Arbeitsbereich.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../sources/home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

## Überwachen von Datenflüssen

Melden Sie sich bei der Benutzeroberfläche [der](https://platform.adobe.com) Experience Platform an und wählen Sie dann im linken Navigationsbereich die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den [!UICONTROL Quellarbeitsbereich] zuzugreifen. Wählen Sie **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile zur Ansicht vorhandener Datenflüsse.

![catalog-dataflows](../assets/ui/monitor-sources/catalog-dataflows.png)

Eine Liste der vorhandenen Datenflüsse wird angezeigt. Auf dieser Seite finden Sie eine Liste mit anzeigbaren Datenflüssen, einschließlich Informationen zu Quelle, Benutzername, Anzahl der Datenflüsse und Status.

Weitere Informationen zu Status finden Sie in der folgenden Tabelle:

| Status | Beschreibung |
| ------ | ----------- |
| Aktiviert | Der `Enabled` Status gibt an, dass ein Datendurchlauf aktiv ist und Daten gemäß dem bereitgestellten Zeitplan erfasst. |
| Deaktiviert | Der `Disabled` Status gibt an, dass ein Dataflow inaktiv ist und keine Daten aufnimmt. |
| Verarbeitung | Der `Processing` Status gibt an, dass ein Datenflug noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf. |
| Fehler | Der `Error` Status gibt an, dass die Aktivierung eines Datenflusses unterbrochen wurde. |

Wählen Sie das Trichtersymbol oben links, das sortiert werden soll.

![dataflows-Liste](../assets/ui/monitor-sources/dataflows-list.png)

Das Sortierfeld wird angezeigt. Wählen Sie im Bildlaufmenü die Quelle aus, auf die Sie zugreifen möchten, und wählen Sie dann in der Liste auf der rechten Seite den Datendurchlauf aus. Sie können auch die Schaltfläche &quot;Ellipsen&quot;(`...`) auswählen, um mehr verfügbare Optionen für den ausgewählten Datendurchlauf anzuzeigen.

![sort-dataflows](../assets/ui/monitor-sources/dataflows-sort.png)

Auf der Seite &quot; **[!UICONTROL Dataflow-Aktivität]** &quot;finden Sie Angaben zur Anzahl der erfassten und fehlgeschlagenen Datensätze sowie Informationen zum Datenaflow-Status und zur Verarbeitungszeit. Wählen Sie das Kalendersymbol oberhalb des Datenflusses aus, um den Zeitraum Ihrer Erfassungsdatensätze anzupassen.

![datflow-Aktivität](../assets/ui/monitor-sources/dataflow-activity.png)

Der Kalender ermöglicht die Ansicht der verschiedenen Zeitrahmen für erfasste Datensätze. Sie können zwischen den beiden voreingestellten Optionen &quot;[!UICONTROL Letzte 7 Tage]&quot;und &quot;[!UICONTROL Letzte 30 Tage]&quot;wählen. Alternativ können Sie einen benutzerdefinierten Zeitraum mithilfe des Kalenders festlegen. Wählen Sie den gewünschten Zeitraum aus und wählen Sie &quot; **[!UICONTROL Anwenden]** &quot;, um fortzufahren.

![flow-calendar](../assets/ui/monitor-sources/flow-calendar.png)

Standardmäßig wird in der Aktivität **[!UICONTROL &quot;]** Dataflow&quot;das Bedienfeld &quot; **[!UICONTROL Eigenschaften]** &quot;angezeigt, das mit dem Datenflug verknüpft ist. Wählen Sie den Fluss aus, der von der Liste ausgeführt wird, um die zugehörigen Metadaten einschließlich Informationen zur eindeutigen Ausführen-ID anzuzeigen.

Wählen Sie &quot; **[!UICONTROL Datenaflow-Run-Beginn]** &quot;aus, um auf die **[!UICONTROL Datenaflow-Übersicht]** zuzugreifen.

![laufend](../assets/ui/monitor-sources/run-metadata.png)

Die Übersicht über den **[!UICONTROL Datenfluss]** enthält Informationen zum Datendurchlauf, einschließlich Metadaten, des Teilaufzeichnungsstatus und des zugewiesenen Fehlerschwellenwerts. Die obere Kopfzeile enthält auch eine Fehlerzusammenfassung. Die **[!UICONTROL Fehlerzusammenfassung]** enthält den spezifischen Fehler der obersten Ebene, der anzeigt, in welchem Schritt beim Erfassungsvorgang ein Fehler aufgetreten ist.

![dataflow-run-overview](../assets/ui/monitor-sources/dataflow-run-overview.png)

In der folgenden Tabelle finden Sie Fehler, die in der **[!UICONTROL Fehlerzusammenfassung]** angezeigt werden können.

| Fehler | Beschreibung |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Beim Kopieren von Daten aus einer Quelle ist ein Fehler aufgetreten. |
| `CONNECTOR-2001-500` | Während der Verarbeitung kopierter Daten zu [!DNL Platform]ist ein Fehler aufgetreten. Dieser Fehler kann bei der Analyse, Validierung oder Transformation auftreten. |

Die untere Hälfte des Bildschirms enthält Informationen zu **[!UICONTROL Dataflow-Ausführungsfehlern]**. Von hier aus können Sie auch die erfassten Dateien Ansicht, die Fehlerdiagnose für Vorschau und Download durchführen oder das Dateimanifest herunterladen.

Im Abschnitt &quot; **[!UICONTROL Datenflussausführungsfehler]** &quot;werden der Fehlercode, die Anzahl der fehlgeschlagenen Datensätze und die Informationen zum Fehler angezeigt.

Wählen Sie **[!UICONTROL Fehlerdiagnose]** für Vorschauen aus, um weitere Informationen zum Erfassungsfehler anzuzeigen.

![Datenflusslauffehler](../assets/ui/monitor-sources/dataflow-run-errors.png)

Das Fenster **[!UICONTROL Vorschau]** für die Fehlerdiagnose wird angezeigt. In diesem Bildschirm werden spezifische Informationen zum Erfassungsfehler angezeigt, einschließlich Dateiname, Fehlercode, Name der Spalte, in der der Fehler aufgetreten ist, und Beschreibung des Fehlers.

Dieser Abschnitt enthält auch eine Vorschau der Spalte, die den Fehler enthält.

>[!IMPORTANT]
>
>Zur Aktivierung der **[!UICONTROL Fehlerdiagnose-Vorschau]** müssen Sie beim Konfigurieren eines Datenflusses die **[!UICONTROL teilweise Erfassung]** und **[!UICONTROL Fehlerdiagnose]** aktivieren. Dadurch kann das System alle während der Ausführung erfassten Datensätze überprüfen.

![Vorschau-Fehlerdiagnose](../assets/ui/monitor-sources/preview-error-diagnostics.png)

Nach der Vorschau der Fehler können Sie im Übersichtsbedienfeld für **[!UICONTROL Datenfelder]** , auf die Sie zugreifen möchten, die Option &quot; **[!UICONTROL Herunterladen]** &quot;wählen, um die Fehlerdiagnose vollständig aufzurufen und das Dateimanifest herunterzuladen. Weitere Informationen finden Sie in den Dokumenten zur [Fehlerdiagnose](../../ingestion/batch-ingestion/partial.md#retrieve-errors) und zum [Herunterladen von Metadaten](../../ingestion/batch-ingestion/partial.md#download-metadata) .

![Vorschau-Fehlerdiagnose](../assets/ui/monitor-sources/download.png)

Weitere Informationen zur Überwachung von Datenflüssen und zur Erfassung finden Sie im Lernprogramm zur [Überwachung von Streaming-Datenflüssen](../../ingestion/quality/monitor-data-ingestion.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich auf vorhandene Konten und Datenflüsse im **[!UICONTROL Sources]** -Arbeitsbereich zugegriffen. Eingehende Daten können nun von nachgelagerten [!DNL Platform] Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]genutzt werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md)
- [Übersicht über den Data Science Workspace](../../data-science-workspace/home.md)
