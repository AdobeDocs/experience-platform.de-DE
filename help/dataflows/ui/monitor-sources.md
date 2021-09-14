---
keywords: Experience Platform; Startseite; beliebte Themen; Konten überwachen; Datenflüsse überwachen; Datenflüsse; Quellen
description: In diesem Tutorial werden Schritte zur Überwachung Ihres Datenflusses beschrieben, wobei sowohl eine aggregierte Überwachungsansicht als auch eine dienstübergreifende Überwachung verwendet werden.
solution: Experience Platform
title: Überwachen von Datenflüssen für Quellen in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: a5b52d7cc2a39ce15b5a9568df14c86624ae069a
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 10%

---

# Überwachen von Datenflüssen auf Quellen in der Benutzeroberfläche

>[!IMPORTANT]
>
>Streaming-Quellen wie die [HTTP-API-Quelle](../../sources/connectors/streaming/http.md) werden derzeit nicht vom Monitoring-Dashboard unterstützt. Derzeit können Sie das Dashboard nur zur Überwachung der Batch-Quellen verwenden.

In Adobe Experience Platform werden Daten aus zahlreichen Quellen aufgenommen, analysiert und für eine Vielzahl an Zielen aktiviert. Plattform erleichtert das Tracking dieses potenziell nicht-linearen Datenflusses durch Transparenz.

Das Monitoring-Dashboard bietet eine visuelle Darstellung des Journey eines Datenflusses. Sie können eine aggregierte Überwachungsansicht verwenden und von der Quellebene zu einem Datenfluss und einem Datenfluss vertikal navigieren, sodass Sie die entsprechenden Metriken anzeigen können, die zum Erfolg oder Misserfolg eines Datenflusses beitragen. Sie können auch die dienstübergreifende Überwachungskapazität des Monitoring-Dashboards verwenden, um die Journey eines Datenflusses von einer Quelle bis zu [!DNL Identity Service] und bis [!DNL Profile] zu überwachen.

In diesem Tutorial werden Schritte zur Überwachung Ihres Datenflusses beschrieben, wobei sowohl eine aggregierte Überwachungsansicht als auch eine dienstübergreifende Überwachung verwendet werden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   * [Datenfluss wird ausgeführt](../../sources/notifications.md): Datenfluss-Ausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration ausgewählter Datenflüsse basieren.
* [Quellen](../../sources/home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Identity Service](../../identity-service/home.md): Sorgt für eine bessere Darstellung einzelner Kunden und deren Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Aggregierte Monitoring-Ansicht

Wählen Sie in der [Platform UI](https://platform.adobe.com) **[!UICONTROL Monitoring]** aus dem linken Navigationsbereich aus, um auf das Dashboard [!UICONTROL Monitoring] zuzugreifen. Das Dashboard [!UICONTROL Monitoring] enthält Metriken und Informationen zu allen Datenflüssen aus Quellen, einschließlich Einblicken in den Zustand des Datenverkehrs von einer Quelle bis [!DNL Identity Service] und bis [!DNL Profile].

Im Mittelpunkt des Dashboards steht das Bedienfeld [!UICONTROL Quellaufnahme], das Metriken und Diagramme enthält, die Daten zu erfassten Datensätzen und fehlgeschlagenen Datensätzen anzeigen.

![monitoring-dashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

Standardmäßig enthalten die angezeigten Daten die Aufnahmeraten der letzten 24 Stunden. Wählen Sie **[!UICONTROL Letzte 24 Stunden]** aus, um den Zeitrahmen der angezeigten Datensätze anzupassen.

![change-date](../assets/ui/monitor-sources/change-date.png)

Es wird ein Kalender-Popup-Fenster mit Optionen für alternative Erfassungszeitrahmen angezeigt. Wählen Sie **[!UICONTROL Letzte 30 Tage]** und dann **[!UICONTROL Anwenden]** aus.

![Zeitrahmen anpassen](../assets/ui/monitor-sources/adjust-timeframe.png)

Die Diagramme sind standardmäßig aktiviert und Sie können sie deaktivieren, um die Liste der unten aufgeführten Quellen zu erweitern. Wählen Sie den Umschalter **[!UICONTROL Metriken und Diagramme]** aus, um die Diagramme zu deaktivieren.

![metrics-and-graphs](../assets/ui/monitor-sources/metrics-graphs.png)

| Quellaufnahme | Beschreibung |
| ---------------- | ----------- |
| [!UICONTROL Aufgenommene Datensätze  ] | Die Gesamtzahl der erfassten Datensätze. |
| [!UICONTROL Fehlgeschlagene Datensätze] | Die Gesamtzahl der Datensätze, die aufgrund von Fehlern in den Daten nicht erfasst wurden. |
| [!UICONTROL Gesamtzahl fehlgeschlagener Datenflüsse] | Die Gesamtzahl der Datenflüsse mit dem Status `failed` . |

In der Liste der Quellerfassung werden alle Quellen angezeigt, die mindestens ein vorhandenes Konto enthalten. Die Liste enthält außerdem Informationen zur Erfassungsrate jeder Quelle, zur Anzahl fehlgeschlagener Datensätze und zur Gesamtzahl fehlgeschlagener Datenflüsse basierend auf dem von Ihnen angewendeten Zeitraum.

![Quellaufnahme](../assets/ui/monitor-sources/source-ingestion.png)

Um die Liste der Quellen zu sortieren, wählen Sie **[!UICONTROL Meine Quellen]** und dann Ihre gewünschte Kategorie aus dem Dropdown-Menü aus. Um sich beispielsweise auf Cloud-Speicher zu konzentrieren, wählen Sie **[!UICONTROL Cloud-Speicher]** aus.

![sort-by-category](../assets/ui/monitor-sources/sort-by-category.png)

Um alle vorhandenen Datenflüsse für alle Quellen anzuzeigen, wählen Sie **[!UICONTROL Datenflüsse]** aus.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

Alternativ können Sie eine Quelle in die Suchleiste eingeben, um eine einzelne Quelle zu isolieren. Nachdem Sie die Quelle identifiziert haben, wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) daneben aus, um eine Liste der aktiven Datenflüsse anzuzeigen.

![Suchen](../assets/ui/monitor-sources/search.png)

Eine Liste der Datenflüsse wird angezeigt. Um die Liste einzuschränken und sich auf Datenflüsse mit Fehlern zu konzentrieren, wählen Sie **[!UICONTROL Fehler nur anzeigen]** aus.

![show-failures-only](../assets/ui/monitor-sources/show-failures-only.png)

Suchen Sie den zu überwachenden Datenfluss und wählen Sie dann das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) daneben aus, um weitere Informationen zum Ausführungsstatus anzuzeigen.

![dataflow](../assets/ui/monitor-sources/dataflow.png)

Auf der Seite &quot;Datenfluss-Ausführung&quot;werden Informationen zum Startdatum des Datenflusses, zur Datengröße, zum Status und zur Verarbeitungsdauer angezeigt. Wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) neben der Startzeit des Datenflusses aus, um die Details des Datenflusses anzuzeigen.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

Auf der Seite [!UICONTROL Datenfluss-Ausführungsdetails] werden Informationen zu den Metadaten des Datenflusses, zum partiellen Erfassungsstatus und zur Fehlerzusammenfassung angezeigt. Die Fehlerzusammenfassung enthält den spezifischen Fehler der obersten Ebene, der anzeigt, in welchem Schritt beim Aufnahmevorgang ein Fehler aufgetreten ist.

Scrollen Sie nach unten, um genauere Informationen zum aufgetretenen Fehler anzuzeigen.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

Im Bedienfeld [!UICONTROL Fehler beim Ausführen des Datenflusses] werden der spezifische Fehler- und Fehlercode angezeigt, der zum Erfassungsfehler des Datenflusses führte. In diesem Szenario trat ein Fehler bei der Zuordnungsumwandlung auf, der dazu führte, dass 24 Datensätze fehlschlugen.

Wählen Sie **[!UICONTROL Dateien]** aus, um weitere Informationen zu erhalten.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

Das Bedienfeld [!UICONTROL Dateien] enthält Informationen zum Dateinamen und Pfad.

Wählen Sie **[!UICONTROL Vorschau der Fehlerdiagnose]** aus, um den Fehler detaillierter darzustellen.

![files](../assets/ui/monitor-sources/files.png)

Das Fenster [!UICONTROL Vorschau der Fehlerdiagnose] wird mit einer Vorschau von bis zu 100 Fehlern im Datenfluss angezeigt. Sie können **[!UICONTROL Download]** auswählen, um einen curl-Befehl abzurufen, mit dem Sie dann die Fehlerdiagnose herunterladen können.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Close]** aus.

![Fehlerdiagnose](../assets/ui/monitor-sources/error-diagnostics.png)

Sie können das Breadcrumb-System oben in der Kopfzeile verwenden, um zurück zum Dashboard [!UICONTROL Monitoring] zu navigieren. Wählen Sie **[!UICONTROL Start ausführen: 14.02.2021, 21:47 PM]**, um zur vorherigen Seite zurückzukehren, und wählen Sie dann **[!UICONTROL Datenfluss: Demo zur Datenerfassung im Treueprogramm - Fehlgeschlagen]** , um zur Dataflows-Seite zurückzukehren.

![Breadcrumbs](../assets/ui/monitor-sources/breadcrumbs.png)

## Dienstübergreifende Überwachung

Der obere Teil des Dashboards enthält eine Darstellung des Aufnahmeflusses von der Quellebene über [!DNL Identity Service] bis hin zu [!DNL Profile]. Jede Zelle enthält eine Punktmarke, die das Vorhandensein von Fehlern anzeigt, die in dieser Aufnahmephase aufgetreten sind. Ein grüner Punkt bedeutet eine fehlerfreie Aufnahme, während ein roter Punkt bedeutet, dass in dieser bestimmten Aufnahmephase ein Fehler aufgetreten ist.

![dienstübergreifende Überwachung](../assets/ui/monitor-sources/cross-service-monitoring.png)

Suchen Sie auf der Seite &quot;Datenflüsse&quot;einen erfolgreichen Datenfluss und wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) daneben aus, um die Informationen zum Datenfluss anzuzeigen.

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

Die Seite [!UICONTROL Quellaufnahme] enthält Informationen, die die erfolgreiche Erfassung Ihres Datenflusses bestätigen. Von hier aus können Sie die Überwachung der Journey Ihres Datenflusses von der Quellebene über [!DNL Identity Service] bis zu [!DNL Profile] starten.

Wählen Sie **[!UICONTROL Identitäten]** aus, um die Aufnahme in der Phase [!UICONTROL Identitäten] anzuzeigen.

![sources](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] Metriken

Die Seite [!UICONTROL Identitätsverarbeitung] enthält Informationen zu Datensätzen, die in [!DNL Identity Service] erfasst werden, einschließlich der Anzahl hinzugefügter Identitäten, erstellter Diagramme und aktualisierter Diagramme.

Wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) neben der Startzeit des Datenflusses aus, um weitere Informationen zu Ihrem [!DNL Identity]-Datenfluss anzuzeigen.

![identities](../assets/ui/monitor-sources/identities.png)

| Identitätsmetriken | Beschreibung |
| ---------------- | ----------- |
| [!UICONTROL Erhaltene Aufzeichnungen] | Die Anzahl der von [!DNL Data Lake] empfangenen Datensätze. |
| [!UICONTROL Fehlgeschlagene Datensätze] | Die Anzahl der Datensätze, die aufgrund von Fehlern in den Daten nicht in Platform erfasst wurden. |
| [!UICONTROL Übersprungene Datensätze] | Die Anzahl der Datensätze, die erfasst wurden, jedoch nicht in [!DNL Identity Service], da in der Datensatzzeile nur eine Kennung vorhanden war. |
| [!UICONTROL Aufgenommene Datensätze] | Die Anzahl der Datensätze, die in [!DNL Identity Service] aufgenommen werden. |
| [!UICONTROL Datensätze insgesamt] | Die Gesamtzahl aller Datensätze, einschließlich fehlgeschlagener Datensätze, übersprungener Datensätze, hinzugefügter [!DNL Identities] und duplizierter Datensätze. |
| [!UICONTROL Hinzugefügte Identitäten] | Die Anzahl neuer Kennungen, die [!DNL Identity Service] hinzugefügt wurden. |
| [!UICONTROL Erstellte Diagramme] | Die Anzahl neuer Identitätsdiagramme, die in [!DNL Identity Service] erstellt wurden. |
| [!UICONTROL Diagramme aktualisiert] | Die Anzahl vorhandener Identitätsdiagramme, die mit neuen Edges aktualisiert wurden. |
| [!UICONTROL Fehlgeschlagene Datenfluss-Ausführungen] | Die Anzahl der fehlgeschlagenen Datenflüsse. |
| [!UICONTROL Verarbeitungszeit] | Der Zeitstempel vom Beginn der Aufnahme bis zum Abschluss. |
| [!UICONTROL Status] | Definiert den Gesamtstatus eines Datenflusses. Mögliche Statuswerte sind: <ul><li>`Success`: Gibt an, dass ein Datenfluss aktiv ist und Daten gemäß dem festgelegten Zeitplan erfasst.</li><li>`Failed`: Gibt an, dass der Aktivierungsprozess eines Datenflusses aufgrund von Fehlern unterbrochen wurde. </li><li>`Processing`: Gibt an, dass der Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf.</li></ul> |

Auf der Seite [!UICONTROL Datenfluss-Ausführungsdetails] werden weitere Informationen zu Ihrem [!DNL Identity]-Datenfluss angezeigt, einschließlich der IMS-Organisations-ID und der Datenfluss-Start-ID. Auf dieser Seite werden auch der entsprechende Fehlercode und die Fehlermeldung angezeigt, die von [!DNL Identity Service] bereitgestellt werden, sollte es im Aufnahmeprozess zu Fehlern kommen.

Wählen Sie **[!UICONTROL Start ausführen: 14.02.2021, 21:47 PM]** , um zur vorherigen Seite zurückzukehren.

![identities-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Wählen Sie auf der Seite [!UICONTROL Identitätsverarbeitung] die Option **[!UICONTROL Profile]** aus, um den Status der Datensatzaufnahme in der Phase [!UICONTROL Profile] anzuzeigen.

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] Metriken

Die Seite [!UICONTROL Profilverarbeitung] enthält Informationen zu Datensätzen, die in [!DNL Profile] erfasst werden, einschließlich der Anzahl der erstellten Profilfragmente, der aktualisierten Profilfragmente und der Gesamtzahl der Profilfragmente.

Wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) neben der Startzeit des Datenflusses aus, um weitere Informationen zu Ihrem [!DNL Profile]-Datenfluss anzuzeigen.

![profiles](../assets/ui/monitor-sources/profiles.png)

| Profilmetriken | Beschreibung |
| --------------- | ----------- |
| [!UICONTROL Erhaltene Aufzeichnungen] | Die Anzahl der von [!DNL Data Lake] empfangenen Datensätze. |
| [!UICONTROL Fehlgeschlagene Datensätze  ] | Die Anzahl der Datensätze, die aufgrund von Fehlern erfasst, aber nicht in [!DNL Profile] aufgenommen wurden. |
| [!UICONTROL Profilfragmente hinzugefügt] | Die Anzahl der neu hinzugefügten [!DNL Profile] Fragmente. |
| [!UICONTROL Profilfragmente aktualisiert] | Die Anzahl vorhandener [!DNL Profile] Fragmente wurde aktualisiert. |
| [!UICONTROL Profilfragmente insgesamt] | Die Gesamtzahl der in [!DNL Profile] geschriebenen Datensätze, einschließlich aller vorhandenen [!DNL Profile] Fragmente, die aktualisiert wurden, und neuer [!DNL Profile] Fragmente. |
| [!UICONTROL Fehlgeschlagene Datenfluss-Ausführungen] | Die Anzahl der fehlgeschlagenen Datenflüsse. |
| [!UICONTROL Verarbeitungszeit] | Der Zeitstempel vom Beginn der Aufnahme bis zum Abschluss. |
| [!UICONTROL Status] | Definiert den Gesamtstatus eines Datenflusses. Mögliche Statuswerte sind: <ul><li>`Success`: Gibt an, dass ein Datenfluss aktiv ist und Daten gemäß dem festgelegten Zeitplan erfasst.</li><li>`Failed`: Gibt an, dass der Aktivierungsprozess eines Datenflusses aufgrund von Fehlern unterbrochen wurde. </li><li>`Processing`: Gibt an, dass der Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf.</li></ul> |

Auf der Seite [!UICONTROL Datenfluss-Ausführungsdetails] werden weitere Informationen zu Ihrem [!DNL Profile]-Datenfluss angezeigt, einschließlich der IMS-Organisations-ID und der Datenfluss-Start-ID. Auf dieser Seite werden auch der entsprechende Fehlercode und die Fehlermeldung angezeigt, die von [!DNL Profile] bereitgestellt werden, sollte es im Aufnahmeprozess zu Fehlern kommen.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Nächste Schritte

In diesem Tutorial haben Sie den Datenfluss der Aufnahme von der Quellebene über das Dashboard **[!UICONTROL Überwachung]** bis [!DNL Profile] erfolgreich überwacht. [!DNL Identity Service] Sie haben auch erfolgreich Fehler identifiziert, die zum Fehlschlagen von Datenflüssen während des Aufnahmevorgangs beigetragen haben. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md)
* [Data Science Workspace – Übersicht](../../data-science-workspace/home.md)
