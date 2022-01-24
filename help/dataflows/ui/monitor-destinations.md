---
keywords: Experience Platform; Startseite; beliebte Themen; Konten überwachen; Datenflüsse überwachen; Datenflüsse; Ziele
description: Mit Zielen können Sie Ihre Daten von Adobe Experience Platform für unzählige externe Partner aktivieren. In diesem Tutorial erfahren Sie, wie Sie mithilfe der Experience Platform-Benutzeroberfläche Datenflüsse für Ihre Ziele überwachen können.
solution: Experience Platform
title: Überwachen von Datenflüssen für Ziele in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: b9f9e709fe51000a32eaea7a1a7c76488a36dd9b
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 3%

---

# Überwachen von Datenflüssen auf Ziele in der Benutzeroberfläche

Mit Zielen können Sie Ihre Daten von Adobe Experience Platform für unzählige externe Partner aktivieren. Platform erleichtert das Tracking des Datenflusses zu Ihren Zielen, indem Datenflüsse für Transparenz sorgen.

Das Monitoring-Dashboard bietet eine visuelle Darstellung des Journey eines Datenflusses, einschließlich des Ziels, für das die Daten aktiviert werden. In diesem Tutorial erfahren Sie, wie Sie Datenflüsse entweder direkt im Arbeitsbereich &quot;Ziele&quot;überwachen oder das Monitoring-Dashboard verwenden können, um Datenflüsse für Ihre Ziele mithilfe der Experience Platform-Benutzeroberfläche zu überwachen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   - [Datenfluss-Abläufe](../../sources/notifications.md): Datenfluss-Ausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration ausgewählter Datenflüsse basieren.
- [Ziele](../../destinations/home.md): Ziele sind vordefinierte Integrationen mit häufig verwendeten Anwendungen, die die nahtlose Aktivierung von Daten aus Platform für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle ermöglichen.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Überwachen von Datenflüssen im Arbeitsbereich &quot;Ziele&quot; {#monitor-dataflows-in-the-destinations-workspace}

Im **[!UICONTROL Ziele]** Navigieren Sie in der Platform-Benutzeroberfläche zum **[!UICONTROL Durchsuchen]** und wählen Sie den Namen eines Ziels aus, das Sie anzeigen möchten.

![](../assets/ui/monitor-destinations/select-destination.png)

Eine Liste der vorhandenen Datenflüsse wird angezeigt. Auf dieser Seite finden Sie eine Liste sichtbarer Datenflüsse, einschließlich Informationen zu Ziel, Benutzername, Anzahl der Datenflüsse und Status.

Weitere Informationen zu Status finden Sie in der folgenden Tabelle:

| Status | Beschreibung |
| ------ | ----------- |
| Aktiviert | The `Enabled` status indicates that a dataflow is active and is exporting data according to the schedule it was provided. |
| Deaktiviert | The `Disabled` status indicates that a dataflow is inactive and is not exporting any data. |
| In Bearbeitung | Die `Processing` Status gibt an, dass ein Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf. |
| Fehler | Die `Error` Status gibt an, dass der Aktivierungsprozess eines Datenflusses unterbrochen wurde. |

### Datenfluss-Ausführungen für Streaming-Ziele {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated"
>title="Identities activated"
>abstract="Die Anzahl der einzelnen Profilidentitäten, die erfolgreich für das ausgewählte Ziel aktiviert wurden."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded"
>title="Ausgeschlossene Identitäten"
>abstract="Die Anzahl der einzelnen Profildatensätze, die aufgrund fehlender Attribute und Zustimmungsverletzungen von der Aktivierung für das ausgewählte Ziel ausgeschlossen sind."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed"
>title="Identitäten fehlgeschlagen"
>abstract="Die Anzahl der individuellen Profilidentitäten, die für das ausgewählte Ziel fehlgeschlagen sind. Weitere Informationen finden Sie unter Fehlerdiagnose ."
>additional-url="https://adobe.com/go/destinations-monitor-dataflows-batch-en" text="Weitere Informationen finden Sie in der Dokumentation ."

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Datenfluss-Ausführungsdetails"
>abstract="Die Ausführungsdetails des Ziel-Datenflusses enthalten Informationen zum Aktivierungsstatus des Segments und zu den Metriken, die aus dem Echtzeit-Kundenprofil abgerufen wurden, um eindeutige Identitäten zu generieren. Weitere Informationen finden Sie im Handbuch Metrikdefinitionen ."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Vorgenommene Profile"
>abstract="Die Gesamtzahl der im Datenfluss empfangenen Profile. Dieser Wert wird alle 60 Minuten aktualisiert."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Aktivierte Identitäten"
>abstract="Die Anzahl der einzelnen Profilidentitäten, die erfolgreich für das ausgewählte Ziel aktiviert wurden."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Ausgeschlossene Identitäten"
>abstract="Die Anzahl der einzelnen Profildatensätze, die aufgrund fehlender Attribute und Zustimmungsverletzungen von der Aktivierung für das ausgewählte Ziel ausgeschlossen sind."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Identitäten fehlgeschlagen"
>abstract="Die Anzahl der individuellen Profilidentitäten, die für das ausgewählte Ziel fehlgeschlagen sind. Weitere Informationen finden Sie unter Fehlerdiagnose ."
>text="Learn more in documentation"

Bei Streaming-Zielen muss die Variable [!UICONTROL Datenfluss-Abläufe] -Tab bietet eine stündliche Aktualisierung für Metrikdaten zu Ihren Datenfluss-Läufen. Die auffälligsten gekennzeichneten Statistiken sind für Identitäten.

Identitäten stellen die verschiedenen Facetten eines Profils dar. Wenn beispielsweise ein Profil sowohl eine Telefonnummer als auch eine E-Mail-Adresse enthält, hat dieses Profil zwei Identitäten.

Es wird eine Liste einzelner Ausführungen und der jeweiligen Metriken mit den folgenden Gesamtwerten für Identitäten angezeigt:

- **[!UICONTROL Aktivierte Identitäten]**: Die Gesamtzahl der Profilidentitäten, die zur Aktivierung erstellt oder aktualisiert wurden.
- **[!UICONTROL Ausgeschlossene Identitäten]**: Die Gesamtzahl der Profilidentitäten, die zur Aktivierung aufgrund fehlender Attribute und Zustimmungsverstoßes übersprungen werden.
- **[!UICONTROL Identitäten fehlgeschlagen]**: Die Gesamtzahl der Profilidentitäten, die aufgrund von Fehlern nicht für das Ziel aktiviert werden.

![](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Jeder einzelne Datenfluss zeigt die folgenden Details an:

- **[!UICONTROL Dataflow run start]**: The time that the dataflow run started at.
- **[!UICONTROL Verarbeitungszeit]**: Die Zeitdauer, die die Verarbeitung des Datenflusses dauerte.
- **[!UICONTROL Vorgenommene Profile]**: Die Gesamtzahl der im Datenfluss empfangenen Profile.
- **[!UICONTROL Aktivierte Identitäten]**: Die Gesamtzahl der Profilidentitäten, die erfolgreich für das ausgewählte Ziel aktiviert wurden.
- **[!UICONTROL Ausgeschlossene Identitäten]**: Die Gesamtzahl der Profilidentitäten, die aufgrund fehlender Attribute und Zustimmungsverletzungen von der Aktivierung ausgeschlossen sind.
- **[!UICONTROL Identitäten fehlgeschlagen]** Die Gesamtzahl der Profilidentitäten, die aufgrund von Fehlern nicht für das Ziel aktiviert werden.
- **[!UICONTROL Aktivierungsrate]**: Der Prozentsatz der empfangenen Identitäten, die erfolgreich aktiviert oder übersprungen wurden. Die folgende Formel zeigt, wie dieser Wert berechnet wird:
   ![](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Stellt den Status dar, in dem sich der Datenfluss befindet: entweder [!UICONTROL Abgeschlossen] oder [!UICONTROL Verarbeitung]. [!UICONTROL Abgeschlossen] bedeutet, dass alle Identitäten für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde exportiert wurden. [!UICONTROL Verarbeitung] bedeutet, dass die Ausführung des Datenflusses noch nicht abgeschlossen ist.

Um die Details eines bestimmten Datenfluss-Laufs anzuzeigen, wählen Sie die Startzeit der Ausführung aus der Liste aus.

Die Detailseite für einen Datenfluss-Lauf enthält zusätzliche Informationen wie die Anzahl der empfangenen Profile, die Anzahl der aktivierten Identitäten, die Anzahl der fehlgeschlagenen Identitäten und die Anzahl der ausgeschlossenen Identitäten.

![](../assets/ui/monitor-destinations/dataflow-details-stream.png)

Auf der Detailseite wird auch eine Liste mit fehlgeschlagenen Identitäten und ausgeschlossenen Identitäten angezeigt. Es werden Informationen für die fehlgeschlagenen und ausgeschlossenen Identitäten angezeigt, einschließlich Fehlercode, Identitätsanzahl und Beschreibung. Standardmäßig werden in der Liste die fehlgeschlagenen Identitäten angezeigt. Um übersprungene Identitäten anzuzeigen, wählen Sie die **[!UICONTROL Ausgeschlossene Identitäten]** umschalten.

![](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### Datenfluss-Ausführung für Batch-Ziele {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received"
>title="Vorgenommene Profile"
>abstract="Die Gesamtzahl der im Datenfluss empfangenen Profile. Dieser Wert wird alle 60 Minuten aktualisiert."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_batch"
>title="Datenfluss-Ausführungsdetails"
>abstract="Die Ausführungsdetails des Ziel-Datenflusses enthalten Informationen zum Aktivierungsstatus des Segments und zu den Metriken, die aus dem Echtzeit-Kundenprofil abgerufen wurden, um eindeutige Identitäten zu generieren. Weitere Informationen finden Sie im Handbuch Metrikdefinitionen ."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Vorgenommene Profile"
>abstract="Die Gesamtzahl der im Datenfluss empfangenen Profile. Dieser Wert wird alle 60 Minuten aktualisiert."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Aktivierte Identitäten"
>abstract="The count of individual profile identities successfully activated to the selected destination."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Ausgeschlossene Identitäten"
>abstract="Die Anzahl der einzelnen Profildatensätze, die aufgrund fehlender Attribute und Zustimmungsverletzungen von der Aktivierung für das ausgewählte Ziel ausgeschlossen sind."
>text="Learn more in documentation"

For batch destinations, the [!UICONTROL Dataflow runs] tab provides metric data on your dataflow runs. Es wird eine Liste einzelner Ausführungen und der jeweiligen Metriken mit den folgenden Gesamtwerten für Identitäten angezeigt:

- **[!UICONTROL Identities activated]**: The count of individual profile identities successfully activated to the selected destination.
- **[!UICONTROL Ausgeschlossene Identitäten]**: Die Anzahl der einzelnen Profilidentitäten, die aufgrund fehlender Attribute und Zustimmungsverletzungen von der Aktivierung für das ausgewählte Ziel ausgeschlossen sind.

![](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Jeder einzelne Datenfluss zeigt die folgenden Details an:

- **[!UICONTROL Start des Datenflusses]**: Die Zeit, zu der der Datenfluss gestartet wurde.
- **[!UICONTROL Verarbeitungszeit]**: Die Zeit, die für die Verarbeitung des Datenflusses benötigt wurde.
- **[!UICONTROL Profiles received]**: The total number of profiles received in the dataflow. This value is updated every 60 minutes.
- **[!UICONTROL Aktivierte Identitäten]**: Die Gesamtzahl der Profilidentitäten, die erfolgreich für das ausgewählte Ziel aktiviert wurden.
- **[!UICONTROL Ausgeschlossene Identitäten]**: Die Gesamtzahl der Profilidentitäten, die aufgrund fehlender Attribute und Zustimmungsverletzungen von der Aktivierung ausgeschlossen sind.
- **[!UICONTROL Status]**: Stellt den Status dar, in dem sich der Datenfluss befindet. Dabei kann es sich um einen von drei Status handeln: [!UICONTROL Erfolg], [!UICONTROL Fehlgeschlagen]und [!UICONTROL Verarbeitung]. [!UICONTROL Erfolg] bedeutet, dass der Datenfluss aktiv ist und Daten gemäß dem bereitgestellten Zeitplan exportiert. [!UICONTROL Fehlgeschlagen] bedeutet, dass die Aktivierung der Daten aufgrund von Fehlern ausgesetzt wurde. [!UICONTROL Verarbeitung] bedeutet, dass der Datenfluss noch nicht aktiv ist und im Allgemeinen beim Erstellen eines neuen Datenflusses auftritt.

Um Details zu einem bestimmten Datenfluss-Lauf anzuzeigen, wählen Sie die Startzeit der Ausführung aus der Liste aus.

>[!NOTE]
>
>Datenflüsse werden basierend auf der Zeitplanfrequenz des Zieldatenflusses generiert. Für jede auf ein Segment angewendete Zusammenführungsrichtlinie wird ein separater Datenfluss ausgeführt.

Auf der Detailseite für einen Datenfluss werden neben den Details, die in der Liste der Datenflüsse angezeigt werden, spezifischere Informationen zum Datenfluss angezeigt:

- **[!UICONTROL Datengröße]**: Die Größe des Datenflusses, der exportiert wird.
- **[!UICONTROL Dateien insgesamt]**: Die Gesamtzahl der im Datenfluss exportierten Dateien.
- **[!UICONTROL Last updated]**: The time the dataflow run was last updated.

![](../assets/ui/monitor-destinations/dataflow-batch.png)

Auf der Detailseite wird auch eine Liste mit fehlgeschlagenen Identitäten und ausgeschlossenen Identitäten angezeigt. Es werden Informationen für die fehlgeschlagenen und ausgeschlossenen Identitäten angezeigt, einschließlich Fehlercode und Beschreibung. By default, the list displays the failed identities. Um ausgeschlossene Identitäten anzuzeigen, wählen Sie die **[!UICONTROL Ausgeschlossene Identitäten]** umschalten.

![](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## Dashboard &quot;Ziele überwachen&quot; {#monitoring-destinations-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activation"
>abstract="The destination activation contains information on the segment&#39;s activation status and metrics taken from Real-time Customer Profile to generate unique identities."

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Segmentaufträge"
>abstract="Das Dashboard für Segmentaufträge enthält Informationen zu den Evaluierungs- und Exportvorgängen für alle Ihre Segmente."

So greifen Sie auf die [!UICONTROL Überwachung] Dashboard, auswählen **[!UICONTROL Überwachung]** (![Überwachungssymbol](../assets/ui/monitor-destinations/monitoring-icon.png)) in der linken Navigation. Einmal im [!UICONTROL Überwachung] Seite, wählen Sie [!UICONTROL Ziele]. Die [!UICONTROL Überwachung] Dashboard enthält Metriken und Informationen zu den ausgeführten Zielaufträgen.

In der Mitte des Dashboards befindet sich das Bedienfeld Aktivierung , das Metriken und Diagramme enthält, die Daten zur Aktivierungsrate der Daten anzeigen, die an Ziele exportiert werden.

![](../assets/ui/monitor-destinations/dashboard-graph.png)


By default, the data displayed contains the activation rates from the last 24 hours. Auswählen **[!UICONTROL Letzte 24 Stunden]** , um den Zeitrahmen der angezeigten Datensätze anzupassen. Verfügbare Optionen umfassen **[!UICONTROL Letzte 24 Stunden]**, **[!UICONTROL Letzte 7 Tage]** und **[!UICONTROL Letzte 30 Tage]**. Alternatively, you can select the dates on the calendar pop-up window that appears. Nachdem Sie die Daten ausgewählt haben, wählen Sie **[!UICONTROL Anwenden]** , um den Zeitrahmen der angezeigten Informationen anzupassen.

>[!NOTE]
>
>Der folgende Screenshot zeigt die Aktivierungsrate der letzten 30 Tage anstelle der letzten 24 Stunden. Sie können den Zeitrahmen anpassen, indem Sie **[!UICONTROL Letzte 30 Tage]**.

![](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Das Diagramm wird standardmäßig angezeigt und Sie können es deaktivieren, um die Liste der Ziele unten zu erweitern. Wählen Sie die **[!UICONTROL Metriken und Diagramme]** Umschalten, um die Diagramme zu deaktivieren.

Die **[!UICONTROL Aktivierung]** zeigt eine Liste von Zielen an, die mindestens ein vorhandenes Konto enthalten. Diese Liste enthält auch Informationen zu empfangenen Profilen, aktivierten Profildatensätzen, fehlgeschlagenen Profildatensätzen, übersprungenen Profildatensätzen, insgesamt fehlgeschlagenen Datenflüssen und dem letzten aktualisierten Datum für diese Ziele.

![](../assets/ui/monitor-destinations/dashboard-destinations.png)

Sie können Ihre Zielliste auch so filtern, dass nur die ausgewählte Zielkategorie angezeigt wird. Wählen Sie die **[!UICONTROL Meine Ziele]** und wählen Sie den Zieltyp aus, nach dem Sie filtern möchten.

![](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Darüber hinaus können Sie ein Ziel in die Suchleiste eingeben, um es zu einem einzelnen Ziel zu isolieren. Wenn Sie die Datenflüsse des Ziels anzeigen möchten, können Sie den Filter auswählen ![filter](../assets/ui/monitor-destinations/filter.png) daneben, um eine Liste der aktiven Datenflüsse anzuzeigen.

![](../assets/ui/monitor-destinations/filtered-destinations.png)

Wenn Sie alle vorhandenen Datenflüsse über alle Ziele hinweg anzeigen möchten, wählen Sie **[!UICONTROL Datenflüsse]**.

Es wird eine Liste mit Datenflüssen angezeigt, die nach Zielgruppen gruppiert sind. Sie können zusätzliche Details für einen bestimmten Datenfluss anzeigen, indem Sie das Ziel, das Sie überwachen möchten, suchen und den Filter auswählen ![filter](../assets/ui/monitor-destinations/filter.png) daneben und anschließend den Filter auswählen ![filter](../assets/ui/monitor-destinations/filter.png) neben dem Datenfluss weitere Informationen.

![](../assets/ui/monitor-destinations/dashboard-dataflows.png)


Auf der Seite &quot;Datenfluss-Ausführung&quot;werden Informationen zu Ihren Datenfluss-Ausführungen angezeigt, einschließlich Startzeit des Datenflusses, Verarbeitungszeit, empfangene Profile, aktivierte Identitäten, ausgeschlossene Identitäten, fehlgeschlagene Identitäten, Aktivierungsrate und Status. Um weitere Details zu einem bestimmten Datenfluss-Lauf anzuzeigen, wählen Sie den Filter aus ![filter](../assets/ui/monitor-destinations/filter.png) neben der Startzeit des Datenflusses.

![](../assets/ui/monitor-destinations/dashboard-dataflows-filter.png)

Auf der Seite &quot;Datenfluss&quot;werden neben den Details, die in der Liste der Datenflüsse angezeigt werden, spezifischere Informationen zum Datenfluss angezeigt:

- **[!UICONTROL Dataflow-run-ID]**: Die Kennung des Datenflusses.
- **[!UICONTROL Kennung der IMS-Organisation]**: Die IMS-Organisation, zu der der Datenfluss gehört.
- **[!UICONTROL Letzte Aktualisierung]**: Die Zeit, zu der der Datenfluss zuletzt aktualisiert wurde.

Auf der Detailseite wird auch eine Liste mit fehlgeschlagenen Identitäten und ausgeschlossenen Identitäten angezeigt. Es werden Informationen für die fehlgeschlagenen und ausgeschlossenen Identitäten angezeigt, einschließlich Fehlercode, Identitätsanzahl und Beschreibung. Standardmäßig werden in der Liste die fehlgeschlagenen Identitäten angezeigt. Um übersprungene Identitäten anzuzeigen, wählen Sie die **[!UICONTROL Ausgeschlossene Identitäten]** umschalten.

![](../assets/ui/monitor-destinations/identities-excluded.png)

## Nächste Schritte

In diesem Handbuch erfahren Sie jetzt, wie Sie Datenflüsse für Batch- und Streaming-Ziele überwachen können, einschließlich aller relevanten Informationen wie Verarbeitungszeit, Aktivierungsrate und Status. Weitere Informationen zu Datenflüssen in Platform finden Sie im Abschnitt [Datenflüsse - Übersicht](../home.md). Weitere Informationen zu Zielen finden Sie im Abschnitt [Ziele - Übersicht](../../destinations/home.md).