---
description: Erfahren Sie, wie Sie mithilfe der Experience Platform-Benutzeroberfläche Datenflüsse für Ihre Ziele überwachen können.
solution: Experience Platform
title: Überwachen von Datenflüssen für Ziele in der Benutzeroberfläche
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 25dc27d890cb2e0e23f8fa797ac9edea929164fd
workflow-type: tm+mt
source-wordcount: '3639'
ht-degree: 11%

---

# Überwachen von Datenflüssen auf Ziele in der Benutzeroberfläche

Verwenden Sie die verschiedenen Ziele im Experience Platform-Katalog, um Ihre Daten von Platform für unzählige externe Partner zu aktivieren. Platform erleichtert das Tracking des Datenflusses zu Ihren Zielen, indem Datenflüsse für Transparenz sorgen.

Das Monitoring-Dashboard bietet eine visuelle Darstellung der Journey eines Datenflusses, einschließlich des Ziels, für das die Daten aktiviert werden, des angezeigten Datentyps, der exportierten Daten pro Datenfluss und vieles mehr.

In diesem Tutorial erfahren Sie, wie Sie Datenflüsse entweder direkt im Arbeitsbereich &quot;Ziele&quot;überwachen oder das Monitoring-Dashboard verwenden können, um Datenflüsse für Ihre Ziele mithilfe der Experience Platform-Benutzeroberfläche zu überwachen.

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   - [Datenfluss-Ausführungen](../../sources/notifications.md): Datenfluss-Ausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration ausgewählter Datenflüsse basieren.
- [Ziele](../../destinations/home.md): Ziele sind vordefinierte Integrationen mit häufig verwendeten Anwendungen, die die nahtlose Aktivierung von Daten aus Platform für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle ermöglichen.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

## Überwachen von Datenflüssen im Arbeitsbereich &quot;Ziele&quot; {#monitor-dataflows-in-the-destinations-workspace}

Navigieren Sie im Arbeitsbereich **[!UICONTROL Ziele]** in der Platform-Benutzeroberfläche zur Registerkarte **[!UICONTROL Durchsuchen]** und wählen Sie den Namen eines Ziels aus, das Sie anzeigen möchten.

![Wählen Sie die Zielansicht mit einer hervorgehobenen Zielverbindung aus](../assets/ui/monitor-destinations/select-destination.png)

Eine Liste der vorhandenen Datenflüsse wird angezeigt. Auf dieser Seite finden Sie eine Liste sichtbarer Datenflüsse, einschließlich Informationen zu Ziel, Benutzername, Anzahl der Datenflüsse und Status.

Weitere Informationen zu Status finden Sie in der folgenden Tabelle:

| Status | Beschreibung |
| ------ | ----------- |
| Aktiviert | Der Status &quot;`Enabled`&quot;zeigt an, dass ein Datenfluss aktiv ist und Daten gemäß dem Zeitplan exportiert, der ihm bereitgestellt wurde. |
| Deaktiviert | Der Status &quot;`Disabled`&quot;zeigt an, dass ein Datenfluss inaktiv ist und keine Daten exportiert. |
| Verarbeitung läuft | Der Status &quot;`Processing`&quot;zeigt an, dass ein Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf. |
| Fehler | Der Status `Error` gibt an, dass der Aktivierungsprozess eines Datenflusses unterbrochen wurde. |

### Datenflussausführungen für Streaming-Ziele {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Details zur Datenflussausführung"
>abstract="Die Details zur Ausführung des Ziel-Datenflusses enthalten Informationen zum Aktivierungsstatus einer Zielgruppe und Metriken, die aus dem Echtzeit-Kundenprofil abgerufen wurden, um eindeutige Identitäten zu generieren. Weitere Informationen finden Sie im Handbuch zu Metrikdefinitionen."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Empfangene Profile"
>abstract="Die Gesamtzahl der im Datenfluss empfangenen Profile. Dieser Wert wird alle 60 Minuten aktualisiert."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Aktivierte Identitäten"
>abstract="Die Anzahl der individuellen Profilidentitäten, die für das ausgewählte Ziel erfolgreich aktiviert wurden. Diese Metrik enthält Identitäten, die aus exportierten Zielgruppen erstellt, aktualisiert und entfernt werden."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Ausgeschlossene Identitäten"
>abstract="Die Anzahl individueller Profildatensätze, die aufgrund fehlender Attribute und Einverständnisverletzungen von der Aktivierung für das ausgewählte Ziel ausgeschlossen sind."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Fehlgeschlagene Identitäten"
>abstract="Die Anzahl individueller Profilidentitäten, deren Aktivierung für das ausgewählte Ziel fehlgeschlagen ist. Genauere Informationen dazu finden Sie in der Fehlerdiagnose."

Für Streaming-Ziele stellt die Registerkarte [!UICONTROL Datenfluss-Läufe] eine stündliche Aktualisierung für Metrikdaten zu Ihren Datenfluss-Läufen bereit. Die auffälligsten gekennzeichneten Statistiken sind für Identitäten.

Identitäten stellen die verschiedenen Facetten eines Profils dar. Wenn beispielsweise ein Profil sowohl eine Telefonnummer als auch eine E-Mail-Adresse enthält, hat dieses Profil zwei Identitäten.

Es wird eine Liste einzelner Ausführungen und der jeweiligen Metriken mit den folgenden Gesamtwerten für Identitäten angezeigt:

- **[!UICONTROL Identitäten aktiviert]**: Die Gesamtzahl der für das ausgewählte Ziel erfolgreich aktivierten Profilidentitäten. Diese Metrik enthält Identitäten, die aus exportierten Zielgruppen erstellt, aktualisiert und entfernt werden.
- **[!UICONTROL Ausgeschlossene Identitäten]**: Die Gesamtzahl der Profilidentitäten, die zur Aktivierung aufgrund fehlender Attribute und Zustimmungsverletzungen übersprungen werden.
- **[!UICONTROL Identitäten fehlgeschlagen]**: Die Gesamtzahl der Profilidentitäten, die für das Ziel aufgrund von Fehlern nicht aktiviert werden.

![Datenfluss führt Details für Streaming-Ziele aus.](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Jeder einzelne Datenfluss zeigt die folgenden Details an:

- **[!UICONTROL Start des Datenflusses]**: Der Zeitpunkt, zu dem der Datenfluss gestartet wurde. Für Streaming-Datenfluss-Ausführungen erfasst Experience Platform Metriken basierend auf dem Start des Datenflusses in Form von stündlichen Metriken. Das bedeutet, dass die Metrik für Streaming-Datenflüsse die Startzeit auf 22:00 Uhr in der Benutzeroberfläche als 22:00 Uhr anzeigt, wenn beispielsweise ein Datenfluss um 23:30 Uhr gestartet wurde.
- **[!UICONTROL Verarbeitungszeit]**: Die Zeit, die für die Verarbeitung des Datenflusses benötigt wurde.
   - Für die Ausführung von **[!UICONTROL completed]** wird in der Verarbeitungszeitmetrik immer eine Stunde angezeigt.
   - Bei Datenfluss-Ausführungen, die sich noch im Status **[!UICONTROL processing]** befinden, bleibt das Fenster zum Erfassen aller Metriken länger als eine Stunde geöffnet, um alle Metriken zu verarbeiten, die dem Datenfluss entsprechen. Beispielsweise kann ein Datenfluss, der um 9:30 Uhr gestartet wurde, eine Stunde und dreißig Minuten lang im Verarbeitungsstatus bleiben, um alle Metriken zu erfassen und zu verarbeiten. Sobald das Verarbeitungsfenster geschlossen und der Status des Datenflusses auf **completed** aktualisiert wird, wird die angezeigte Verarbeitungszeit auf eine Stunde geändert.
- **[!UICONTROL empfangenen Profile]**: Die Gesamtzahl der im Datenfluss empfangenen Profile.
- **[!UICONTROL Aktivierte Identitäten]**: Die Gesamtzahl der Profilidentitäten, die im Rahmen der Datenfluss-Ausführung erfolgreich für das ausgewählte Ziel aktiviert wurden. Diese Metrik enthält Identitäten, die aus exportierten Zielgruppen erstellt, aktualisiert und entfernt werden.
- **[!UICONTROL Ausgeschlossene Identitäten]**: Die Gesamtzahl der Profilidentitäten, die aufgrund fehlender Attribute und einer Verletzung der Einwilligung von der Aktivierung ausgeschlossen sind.
- **[!UICONTROL Identitäten fehlgeschlagen]** Die Gesamtzahl der Profilidentitäten, die für das Ziel aufgrund von Fehlern nicht aktiviert werden.

  >[!IMPORTANT]
  >
  > Ab Oktober 2024 führt Adobe eine Aktualisierung durch, um die Berichtsgenauigkeit für Streaming-Ziele zu erhöhen. Diese Verbesserung sorgt für eine bessere Abstimmung zwischen der Berichterstellung für Experience Platform und Zielplattformen.
  >
  > Vor dieser Aktualisierung umfasste **[!UICONTROL fehlgeschlagene Identitäten]** alle Aktivierungsversuche. Nach dieser Aktualisierung ist nur der letzte Aktivierungsversuch in der Gesamtanzahl enthalten.
  > 
  > Diese Verbesserung gilt derzeit für das Ziel [Google-Kundenabgleich](../../destinations/catalog/advertising/google-customer-match.md) , wird jedoch schrittweise für andere Experience Platform-Streaming-Ziele eingeführt.
  > Nach dieser Verbesserung kann es bei Benutzern des Ziels [Google-Kundenabgleich](../../destinations/catalog/advertising/google-customer-match.md) zu einem erwarteten Rückgang der Anzahl der **[!UICONTROL fehlgeschlagenen Identitäten]** kommen.


- **[!UICONTROL Aktivierungsrate]**: Der Prozentsatz der empfangenen Identitäten, die erfolgreich aktiviert oder übersprungen wurden. Die folgende Formel zeigt, wie dieser Wert berechnet wird:
  ![ Formel der Aktivierungsrate.](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Stellt den Status dar, in dem sich der Datenfluss befindet: entweder [!UICONTROL Abgeschlossen] oder [!UICONTROL Verarbeitung]. [!UICONTROL Abgeschlossen] bedeutet, dass alle Identitäten für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde exportiert wurden. [!UICONTROL Verarbeitung] bedeutet, dass die Ausführung des Datenflusses noch nicht abgeschlossen ist.

Um die Details eines bestimmten Datenflusses anzuzeigen, wählen Sie die Startzeit der Ausführung aus der Liste aus.

Die Detailseite für einen Datenfluss-Lauf enthält zusätzliche Informationen wie die Anzahl der empfangenen Profile, die Anzahl der aktivierten Identitäten, die Anzahl der fehlgeschlagenen Identitäten und die Anzahl der ausgeschlossenen Identitäten.

![Datenflamdetails für Streaming-Ziele.](../assets/ui/monitor-destinations/dataflow-details-stream.png)

Auf der Detailseite wird auch eine Liste mit fehlgeschlagenen Identitäten und ausgeschlossenen Identitäten angezeigt. Es werden Informationen für die fehlgeschlagenen und ausgeschlossenen Identitäten angezeigt, einschließlich Fehlercode, Identitätsanzahl und Beschreibung. Standardmäßig werden in der Liste die fehlgeschlagenen Identitäten angezeigt. Um übersprungene Identitäten anzuzeigen, wählen Sie den Umschalter **[!UICONTROL Ausgeschlossene Identitäten]** aus.

![Datenfluss-Datensätze für Streaming-Ziele mit hervorgehobener Fehlermeldung.](../assets/ui/monitor-destinations/dataflow-records-stream.png)

#### (Beta) Überwachung des Datenflusses auf Zielgruppenebene für Streaming-Ziele {#audience-level-dataflow-runs-for-streaming-destinations}

Sie können Informationen zu den aktivierten, ausgeschlossenen oder fehlgeschlagenen Identitäten auf Zielgruppenebene für jede Zielgruppe anzeigen, die Teil des Datenflusses ist. Die Überwachung auf Zielgruppenebene für Streaming-Ziele ist derzeit nur für [[!DNL Google Customer Match + Display & Video 360] Ziel](/help/destinations/catalog/advertising/google-customer-match-dv360.md) verfügbar.

![Überwachung auf Zielgruppenebene für Streaming-Ziele.](/help/dataflows/assets/ui/monitor-destinations/audience-level-monitoring-streaming.png)

>[!NOTE]
>
>Die Nummer **[!UICONTROL empfangenen Profile]** auf der Registerkarte **[!UICONTROL Zielgruppen]** stimmt möglicherweise nicht immer mit der Anzahl der Profile überein, die für den Datenfluss empfangen wurden. Dies liegt daran, dass ein bestimmtes Profil Teil von mehr als einer Zielgruppe sein kann, die in der Datenfluss-Ausführung aktiviert wird.

### Datenflussausführungen für Batch-Ziele {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Details zur Datenflussausführung"
>abstract="Die Details zur Ausführung des Ziel-Datenflusses enthalten Informationen zum Aktivierungsstatus einer Zielgruppe und Metriken, die aus dem Echtzeit-Kundenprofil abgerufen wurden, um eindeutige Identitäten zu generieren. Weitere Informationen finden Sie im Handbuch zu Metrikdefinitionen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html?lang=de#dataflow-runs-for-streaming-destinations" text="Datenflussausführungen für Streaming-Ziele"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Empfangene Profile"
>abstract="Die Gesamtzahl der im Datenfluss empfangenen Profile. Dieser Wert wird alle 60 Minuten aktualisiert."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Aktivierte Identitäten"
>abstract="Die Anzahl der individuellen Profilidentitäten, die für das ausgewählte Ziel erfolgreich aktiviert wurden. Diese Metrik enthält Identitäten, die aus exportierten Zielgruppen erstellt, aktualisiert und entfernt werden."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Ausgeschlossene Identitäten"
>abstract="Die Anzahl individueller Profildatensätze, die aufgrund fehlender Attribute und Einverständnisverletzungen von der Aktivierung für das ausgewählte Ziel ausgeschlossen sind."

Für Batch-Ziele stellt die Registerkarte [!UICONTROL Datenfluss-Läufe] Metrikdaten für Ihre Datenflug-Läufe bereit. Es wird eine Liste einzelner Ausführungen und der jeweiligen Metriken mit den folgenden Gesamtwerten für Identitäten angezeigt:

- **[!UICONTROL Identitäten aktiviert]**: Die Gesamtzahl der für das ausgewählte Ziel erfolgreich aktivierten Profilidentitäten. Diese Metrik enthält Identitäten, die aus exportierten Zielgruppen erstellt, aktualisiert und entfernt werden.
- **[!UICONTROL Ausgeschlossene Identitäten]**: Die Anzahl der einzelnen Profilidentitäten, die von der Aktivierung für das ausgewählte Ziel ausgeschlossen sind, basierend auf fehlenden Attributen und der Verletzung der Einwilligung.

![Datenfluss führt die Ansicht für Batch-Ziele aus.](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Jeder einzelne Datenfluss zeigt die folgenden Details an:

- **[!UICONTROL Start des Datenflusses]**: Der Zeitpunkt, zu dem der Datenfluss gestartet wurde.
- **[!UICONTROL Audience]**: Der Name der Audience, die mit jedem Datenfluss verknüpft ist.
- **[!UICONTROL Verarbeitungszeit]**: Die Zeit, die für die Verarbeitung des Datenflusses benötigt wurde.
- **[!UICONTROL empfangenen Profile]**: Die Gesamtzahl der im Datenfluss empfangenen Profile. Dieser Wert wird alle 60 Minuten aktualisiert.
- **[!UICONTROL Aktivierte Identitäten]**: Die Gesamtzahl der Profilidentitäten, die im Rahmen der Datenfluss-Ausführung erfolgreich für das ausgewählte Ziel aktiviert wurden. Diese Metrik enthält Identitäten, die aus exportierten Zielgruppen erstellt, aktualisiert und entfernt werden.
- **[!UICONTROL Ausgeschlossene Identitäten]**: Die Gesamtzahl der Profilidentitäten, die aufgrund fehlender Attribute und einer Verletzung der Einwilligung von der Aktivierung ausgeschlossen sind.
- **[!UICONTROL Status]**: Stellt den Status dar, in dem sich der Datenfluss befindet. Dabei kann es sich um einen von drei Status handeln: [!UICONTROL Erfolg], [!UICONTROL Fehlgeschlagen] und [!UICONTROL Verarbeitung]. [!UICONTROL Erfolg] bedeutet, dass der Datenfluss aktiv ist und Daten gemäß dem bereitgestellten Zeitplan exportiert. [!UICONTROL Fehlgeschlagen] bedeutet, dass die Aktivierung der Daten aufgrund von Fehlern ausgesetzt wurde. [!UICONTROL Verarbeitung] bedeutet, dass der Datenfluss noch nicht aktiv ist und im Allgemeinen beim Erstellen eines neuen Datenflusses auftritt.

Um Details zu einem bestimmten Datenfluss anzuzeigen, wählen Sie die Startzeit der Ausführung aus der Liste aus.

>[!NOTE]
>
>Datenflüsse werden basierend auf der Zeitplanfrequenz des Zieldatenflusses generiert. Für jede [Zusammenführungsrichtlinie](../../profile/merge-policies/overview.md), die auf eine Zielgruppe angewendet wird, wird ein separater Datenfluss ausgeführt.

Auf der Detailseite für einen Datenfluss werden neben den Details, die in der Liste der Datenflüsse angezeigt werden, spezifischere Informationen zum Datenfluss angezeigt:

- **[!UICONTROL Datengröße]**: Die Größe des Datenflusses, der exportiert wird.
- **[!UICONTROL Dateien insgesamt]**: Die Gesamtzahl der im Datenfluss exportierten Dateien.
- **[!UICONTROL Letzte Aktualisierung]**: Der Zeitpunkt, zu dem der Datenfluss zuletzt aktualisiert wurde.

![Datenfluss-Ausführungsdetails für Batch-Ziele.](../assets/ui/monitor-destinations/dataflow-batch.png)

Auf der Detailseite wird auch eine Liste mit fehlgeschlagenen Identitäten und ausgeschlossenen Identitäten angezeigt. Es werden Informationen für die fehlgeschlagenen und ausgeschlossenen Identitäten angezeigt, einschließlich Fehlercode und Beschreibung. Standardmäßig werden in der Liste die fehlgeschlagenen Identitäten angezeigt. Um ausgeschlossene Identitäten anzuzeigen, wählen Sie den Umschalter **[!UICONTROL Ausgeschlossene Identitäten]** aus.

![Datenfluss-Datensätze für Batch-Ziele mit hervorgehobener Fehlermeldung.](../assets/ui/monitor-destinations/dataflow-records-batch.png)

### Überwachungsansicht {#view-in-monitoring}

Sie können auch auswählen, ob im Monitoring-Dashboard umfassende Informationen über einen bestimmten Datenfluss und dessen Datenfluss angezeigt werden sollen. So zeigen Sie Informationen zu einem Datenfluss im Monitoring-Dashboard an:

1. Navigieren Sie zur Registerkarte **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** .
2. Navigieren Sie zum Datenfluss, den Sie überprüfen möchten.
3. Wählen Sie das Auslassungszeichen und das Überwachungssymbol ![](/help/images/icons/monitoring.png) **[!UICONTROL In Überwachung anzeigen]** aus.

![Wählen Sie im Ziel-Workflow die Option In Überwachung anzeigen aus, um weitere Informationen zu einem Datenfluss zu erhalten.](/help/dataflows/assets/ui/monitor-destinations/view-in-monitoring.png)

>[!SUCCESS]
>
>Sie können jetzt Informationen zum Datenfluss und den zugehörigen Datenflüssen im Monitoring-Dashboard anzeigen. Weitere Informationen finden Sie im folgenden Abschnitt.

## Dashboard „Ziele überwachen“ {#monitoring-destinations-dashboard}

>[!NOTE]
>
>Die Funktion zur Zielüberwachung wird derzeit für alle Ziele in Experience Platform *unterstützt, mit Ausnahme von* den Zielen [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) und [Benutzerdefinierte Personalisierung](/help/destinations/catalog/personalization/custom-personalization.md).

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activation"
>abstract="Die Zielaktivierungsansicht enthält Informationen zum Aktivierungsstatus einer Zielgruppe und Metriken, die aus dem Echtzeit-Kundenprofil abgerufen wurden, um eindeutige Identitäten zu generieren."

Um auf das Dashboard [!UICONTROL Überwachung] zuzugreifen, wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Überwachung]** (![Überwachungssymbol](/help/images/icons/monitoring.png)) aus. Wählen Sie auf der Seite [!UICONTROL Überwachung] einmal [!UICONTROL Ziele] aus. Das Dashboard [!UICONTROL Überwachung] enthält Metriken und Informationen zu den Zielausführungsaufträgen.

Verwenden Sie das Dashboard [!UICONTROL Ziele] , um einen Überblick über den Zustand Ihrer Aktivierungsflüsse zu erhalten. Rufen Sie zunächst Einblicke in eine aggregierte Ebene für alle Batch- und Streaming-Ziele ab und führen Sie dann einen Drilldown in detaillierten Ansichten für Datenflüsse, Datenfluss-Ausführungen und aktivierte Zielgruppen durch, um Ihre Aktivierungsdaten eingehend zu untersuchen. Die Bildschirme im Dashboard [!UICONTROL Überwachung] bieten praktische Einblicke über Metriken und Fehlerbeschreibungen, mit denen Sie Probleme beheben können, die in Ihren Aktivierungsszenarien auftreten können.

Sie können die angezeigten Informationen nach Datentyp (Kunden, Konten (nur für Adobe Real-Time CDP B2B edition), Perspektiven und Kontoanreicherung) filtern. Weitere Informationen zu diesen Optionen finden Sie im Leitfaden zum [Monitoring-Dashboard](/help/dataflows/ui/monitor.md#monitoring-dashboard-overview).

![In der Monitoring-Dashboard-Ansicht hervorgehobener Filter vom Datentyp.](/help/dataflows/assets/ui/monitor-destinations/add-data-filter.png)

Im Mittelpunkt des Dashboards steht das Bedienfeld [!UICONTROL Aktivierung] , das Metriken und Diagramme enthält, die Daten zur Aktivierungsrate der Daten anzeigen, die an Streaming-Ziele exportiert werden, sowie über die fehlgeschlagenen Batch-Datenflüsse, die an Batch-Ziele ausgeführt werden.

![In der Überwachungsansicht hervorgehobene Diagramme für Streaming- und Batch-Aktivierung.](../assets/ui/monitor-destinations/dashboard-graph.png)


Standardmäßig enthalten die angezeigten Daten die Aktivierungsinformationen der letzten 24 Stunden. Wählen Sie **[!UICONTROL Letzte 24 Stunden]** aus, um den Zeitrahmen der angezeigten Datensätze anzupassen. Zu den verfügbaren Optionen gehören **[!UICONTROL Letzte 24 Stunden]**, **[!UICONTROL Letzte 7 Tage]** und **[!UICONTROL Letzte 30 Tage]**. Alternativ können Sie die Datumsangaben im daraufhin angezeigten Kalender-Popup-Fenster auswählen. Nachdem Sie die Daten ausgewählt haben, wählen Sie **[!UICONTROL Anwenden]** aus, um den Zeitrahmen der angezeigten Informationen anzupassen.

>[!NOTE]
>
>Der folgende Screenshot zeigt die Aktivierungsrate und den Batch-Datenfluss für die letzten 30 Tage anstelle der letzten 24 Stunden. Sie können den Zeitraum anpassen, indem Sie **[!UICONTROL Letzte 30 Tage]** auswählen.

![Änderung der für aktivierte Ziele hervorgehobenen Kontrolle des Lookback-Datumsbereichs](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Verwenden Sie das Pfeilsymbol (![Pfeilsymbol](/help/images/icons/chevron-up.png)), um die Karten oben im Bildschirm zu erweitern oder zu schließen, die anhand des Zieltyps - Streaming oder Batch - einen Überblick über die Aktivierungsdetails bieten:

- **[!UICONTROL Streaming-Aktivierungsrate]**: Stellt den Prozentsatz der empfangenen Identitäten dar, die erfolgreich aktiviert oder übersprungen wurden. Die Formel zur Berechnung dieses Prozentsatzes wird weiter oben auf dieser Seite im Abschnitt [Datenfluss wird für Streaming-Ziele ausgeführt](#dataflow-runs-for-streaming-destinations) beschrieben.
- **[!UICONTROL Batch failed dataflow running]**: Stellt die Anzahl der fehlgeschlagenen Datenfluss-Ausführungen im ausgewählten Zeitintervall dar.

![ Zeigt Karten oben auf der Seite an oder verwirft sie.](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

Das Diagramm **[!UICONTROL Aktivierung]** wird standardmäßig angezeigt und Sie können es deaktivieren, um die Liste der Ziele unten zu erweitern. Wählen Sie den Umschalter **[!UICONTROL Metriken und Diagramme]** aus, um die Diagramme zu deaktivieren.

Im Bedienfeld **[!UICONTROL Aktivierung]** wird eine Liste von Zielen angezeigt, die mindestens ein vorhandenes Konto enthalten. Diese Liste enthält auch Informationen zu den empfangenen Profilen, aktivierten Identitäten, fehlgeschlagenen Identitäten, ausgeschlossenen Identitäten, Aktivierungsrate, insgesamt fehlgeschlagenen Datenflüssen und dem letzten aktualisierten Datum für diese Ziele. Nicht alle Metriken sind für alle Zieltypen verfügbar. In der folgenden Tabelle sind die Metriken und Informationen aufgeführt, die pro Zieltyp verfügbar sind.

| Metrik | Typ des Ziels |
|--------------------------------------|-----------------------|
| **[!UICONTROL empfangene Datensätze]** | Streaming und Batch |
| **[!UICONTROL Aktivierte Datensätze]** | Streaming und Batch |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Streaming |
| **[!UICONTROL Übersprungene Datensätze]** | Streaming und Batch |
| **[!UICONTROL Datentyp]** | Streaming und Batch |
| **[!UICONTROL Aktivierungsrate]** | Streaming |
| **[!UICONTROL Gesamtzahl fehlgeschlagener Datenflüsse]** | Batch |
| **[!UICONTROL Zuletzt aktualisiert]** | Streaming und Batch |

{style="table-layout:auto"}

![Überwachen des Dashboards mit allen aktivierten Zielen hervorgehoben.](../assets/ui/monitor-destinations/dashboard-destinations.png)

Sie können Ihre Zielliste auch so filtern, dass nur die ausgewählte Zielkategorie angezeigt wird. Wählen Sie das Dropdown-Menü **[!UICONTROL Meine Ziele]** aus und wählen Sie die [Zielkategorie](/help/destinations/destination-types.md#categories) aus, nach der Sie filtern möchten.

![Ziele mithilfe des Dropdown-Selektors filtern](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Darüber hinaus können Sie ein Ziel in die Suchleiste eingeben, um es zu einem einzelnen Ziel zu isolieren. Wenn Sie die Datenflüsse des Ziels anzeigen möchten, können Sie den Filter ![filter](/help/images/icons/filter-add.png) daneben auswählen, um eine Liste der aktiven Datenflüsse anzuzeigen.

![Filtern Sie Ziele mithilfe der in der Überwachungsansicht hervorgehobenen Suchleiste.](../assets/ui/monitor-destinations/filtered-destinations.png)

Wenn Sie alle vorhandenen Datenflüsse für alle Ziele anzeigen möchten, wählen Sie **[!UICONTROL Datenflüsse]** aus.

Es wird eine Liste mit Datenflüssen angezeigt, die nach der letzten Ausführung des Datenflusses sortiert sind. Sie können zusätzliche Details für einen bestimmten Datenfluss anzeigen, indem Sie das zu überwachende Ziel suchen, den Filter ![filter](/help/images/icons/filter-add.png) daneben auswählen und anschließend den Filter ![filter](/help/images/icons/filter-add.png) neben dem Datenfluss auswählen, über den Sie weitere Informationen erhalten möchten.

![Alle im Monitoring-Dashboard hervorgehobenen Datenflüsse.](../assets/ui/monitor-destinations/dashboard-dataflows.png)

Nachdem Sie einen Datenfluss für eine weitere Überprüfung ausgewählt haben, enthält die Seite mit den Datenflug-Details einen Umschalter, mit dem Sie die aktivierten Daten im Datenfluss anzeigen können, aufgeschlüsselt nach Datenflüssen oder Zielgruppen.

### Datenfluss-Ausführungsansicht {#dataflow-runs-view}

Wenn **[!UICONTROL Datenfluss ausgeführt wird]** ausgewählt ist, können Sie eine Liste der Datenfluss-Läufe für den ausgewählten Datenfluss und weitere Informationen zu den einzelnen Läufen sehen.

>[!INFO]
>
>Bei Datenflüssen an Streaming-Ziele wird ein Datenfluss in stündliche Fenster unterteilt. Jedes stündliche Fenster generiert eine entsprechende Datenfluss-ID.
>
>Für Datenflüsse an Batch-Ziele wird für jede Zielgruppe ein entsprechender Datenfluss generiert, der auf der geplanten Häufigkeit der Zielgruppenaktivierung basiert. Wenn Sie beispielsweise eine tägliche geplante Aktivierung für fünf Zielgruppen im selben Ziel-Datenfluss einrichten, werden täglich fünf separate Datenfluss-Läufe generiert.

![Der Datenfluss-Bedienfeld wird ausgeführt, wobei mehrere Ausführungen hervorgehoben sind.](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Verwenden Sie den Umschalter **[!UICONTROL Fehler nur anzeigen]** , um nur die fehlgeschlagenen Ausführungen für einen Datenfluss anzuzeigen.

![Datenfluss führt die Ansicht aus, während die Fehler anzeigen nur hervorgehoben wurden](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Ansicht auf Zielgruppenebene {#segment-level-view}

Wenn **[!UICONTROL Zielgruppen]** ausgewählt ist, wird eine Liste der Zielgruppen angezeigt, die für den ausgewählten Datenfluss innerhalb des ausgewählten Zeitraums aktiviert wurden. Dieser Bildschirm enthält Informationen auf Zielgruppenebene zu den aktivierten Datensätzen, den ausgeschlossenen Datensätzen sowie zum Status und zur Uhrzeit des letzten Datenflusses. Durch Überprüfung der Metriken für ausgeschlossene und aktivierte Datensätze können Sie überprüfen, ob eine Zielgruppe erfolgreich aktiviert wurde.

Sie aktivieren beispielsweise eine Zielgruppe mit dem Namen &quot;Mitglieder des Treueprogramms in Kalifornien&quot;für ein Amazon S3-Ziel &quot;Mitglieder des Treueprogramms, Kalifornien, Dezember&quot;. Angenommen, die ausgewählte Zielgruppe enthält 100 Profile, aber nur 80 von 100 Datensätzen enthalten Loyalitäts-ID-Attribute. Sie haben die Exportzuordnungsregeln als &quot;0&quot; definiert. `loyalty.id` In diesem Fall werden auf Zielgruppenebene 80 Datensätze aktiviert und 20 Datensätze ausgeschlossen.

>[!IMPORTANT]
>
>Beachten Sie die aktuellen Einschränkungen im Zusammenhang mit Metriken auf Zielgruppenebene:
>- Die Ansicht auf Zielgruppenebene ist derzeit nur für Batch-(dateibasierte) Ziele und das Streaming-Ziel [Google-Kundenabgleich DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) verfügbar. Rollout ist für weitere Streaming-Ziele geplant.
>- Bei Batch-Zielen werden die Metriken auf Zielgruppenebene derzeit nur für erfolgreiche Datenfluss-Ausführungen aufgezeichnet. Sie werden nicht für fehlgeschlagene Datenfluss-Ausführungen und ausgeschlossene Datensätze aufgezeichnet. Für Datenflüsse, die zu Streaming-Zielen ausgeführt werden, werden Metriken erfasst und für aktivierte und ausgeschlossene Datensätze angezeigt.

![Im Datenfluss-Bedienfeld hervorgehobene Zielgruppen.](../assets/ui/monitor-destinations/dashboard-segments-view.png)

In der Ansicht auf Zielgruppenebene werden die Metriken über mehrere Datenfluss-Läufe innerhalb des ausgewählten Zeitraums aggregiert. Wenn mehrere Datenfluss-Läufe vorhanden sind, können Sie einen Drilldown aus der Zielgruppenebene durchführen, um die Aufschlüsselung für jeden Datenfluss anzuzeigen, gefiltert nach der ausgewählten Zielgruppe.
Verwenden Sie die Filterschaltfläche &quot;![filter](/help/images/icons/filter-add.png)&quot;, um einen Drilldown in die Datenfluss-Ansicht für jede Zielgruppe im Datenfluss durchzuführen.

### Seite mit Datenfluss-Ausführungen {#dataflow-runs-page}

Auf der Seite &quot;Datenfluss-Ausführung&quot;werden Informationen zu Ihren Datenfluss-Ausführungen angezeigt, einschließlich Startzeit des Datenflusses, Verarbeitungszeit, empfangene Datensätze, aktivierte Datensätze, ausgeschlossene Datensätze, fehlgeschlagene Datensätze, Aktivierungsrate und Status.

Wenn Sie über die Ansicht [auf Zielgruppenebene](#segment-level-view) einen Drilldown in die Seite mit den Datenflüssen durchführen, haben Sie die Möglichkeit, den Datenfluss nach folgenden Optionen zu filtern:

- **[!UICONTROL Datenfluss wird mit fehlgeschlagenen Datensätzen ausgeführt]**: Für die ausgewählte Zielgruppe listet diese Option alle Datenfluss-Ausführungen auf, die bei der Aktivierung fehlgeschlagen sind. Informationen dazu, warum Datensätze in einem bestimmten Datenfluss fehlschlugen, finden Sie auf der Seite [Datenfluss-Ausführungsdetails](#dataflow-run-details-page) für diesen Datenfluss.
- **[!UICONTROL Datenfluss wird mit ausgeschlossenen Datensätzen ausgeführt]**: Für die ausgewählte Zielgruppe listet diese Option alle Datenfluss-Vorgänge auf, bei denen einige Datensätze nicht vollständig aktiviert und einige Profile übersprungen wurden. Um zu überprüfen, warum Datensätze in einem bestimmten Datenfluss übersprungen wurden, lesen Sie die Seite [Datenfluss-Ausführungsdetails](#dataflow-run-details-page) für diesen Datenfluss.
- **[!UICONTROL Datenfluss wird mit aktivierten Datensätzen ausgeführt]**: Für die ausgewählte Zielgruppe listet diese Option alle Datenfluss-Ausführungen mit Datensätzen auf, die erfolgreich aktiviert wurden.

![Optionsfelder, die zeigen, wie Datenflüsse für Zielgruppen gefiltert werden.](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Um weitere Details zu einer bestimmten Ausführung des Datenflusses anzuzeigen, wählen Sie den Filter &quot;![filter](/help/images/icons/filter-add.png)&quot;neben der Startzeit des Datenflusses aus, um die Seite mit den Ausführungsdetails des Datenflusses anzuzeigen.

![Datenfluss führt Filter im Monitoring-Dashboard aus, um weitere Informationen für einen bestimmten Datenfluss zu suchen.](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Seite mit Datenfluss-Ausführungsdetails {#dataflow-run-details-page}

Auf der Seite mit den Ausführungsdetails des Datenflusses werden zusätzlich zu den Details, die in der Liste der Datenflüsse angezeigt werden, spezifischere Informationen zum Datenfluss angezeigt:

- **[!UICONTROL Datenfluss-ID]**: Die Kennung des Datenflusses.
- **[!UICONTROL IMS-Organisations-ID]**: Die Organisation, zu der der Datenfluss gehört.
- **[!UICONTROL Letzte Aktualisierung]**: Der Zeitpunkt, zu dem der Datenfluss zuletzt aktualisiert wurde.

Auf der Detailseite können Sie auch zwischen Datenfluss-Ausführungsfehlern und Zielgruppen wechseln. Diese Option ist nur für Datenfluss-Ausführungen in Batch-Zielen und für das Streaming-Ziel [Google-Kundenabgleich DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) verfügbar.

Die Ansicht &quot;Fehler bei Datenfluss&quot;zeigt eine Liste mit fehlgeschlagenen Datensätzen und Datensätzen an, die übersprungen wurden. Informationen zu den fehlgeschlagenen und übersprungenen Datensätzen werden angezeigt, einschließlich Fehlercode, Identitätsanzahl und Beschreibung. Standardmäßig werden in der Liste die fehlgeschlagenen Datensätze angezeigt. Um übersprungene Datensätze anzuzeigen, wählen Sie den Umschalter **[!UICONTROL Übersprungene Datensätze]** aus.

![Ausgeschlossene Identitäten - Umschalter, der in der Überwachungsansicht hervorgehoben ist](../assets/ui/monitor-destinations/identities-excluded.png)

Wenn **[!UICONTROL Zielgruppen]** ausgewählt ist, wird eine Liste der Zielgruppen angezeigt, die im ausgewählten Datenfluss aktiviert wurden. Dieser Bildschirm enthält Informationen auf Zielgruppenebene zu den aktivierten Datensätzen, den ausgeschlossenen Datensätzen sowie zum Status und zur Uhrzeit des letzten Datenflusses.

![Ansicht &quot;Zielgruppen&quot;im Bildschirm mit den Ausführungsdetails des Datenflusses.](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Nächste Schritte {#next-steps}

In diesem Handbuch erfahren Sie jetzt, wie Sie Datenflüsse für Batch- und Streaming-Ziele überwachen können, einschließlich aller relevanten Informationen wie Verarbeitungszeit, Aktivierungsrate und Status. Weiterführende Informationen zu Datenflüssen in Platform finden Sie in der [Übersicht über Datenflüsse](../home.md) . Weitere Informationen zu Zielen finden Sie in der [Zielübersicht](../../destinations/home.md).