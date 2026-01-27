---
keywords: Experience Platform;Startseite;beliebte Themen;Profile überwachen;Datenflüsse überwachen;Datenflüsse;Profil;Echtzeit-Kundenprofil;
description: Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. In diesem Tutorial erfahren Sie, wie Sie Datenflüsse mit Profilen mithilfe der Benutzeroberfläche von Experience Platform überwachen können.
title: Überwachen von Datenflüssen für Profile in der Benutzeroberfläche
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1d60afdf486642398a2d31302db339eb9cb45130
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 11%

---

# Überwachen von Datenflüssen für Profile in der Benutzeroberfläche

Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

Das Überwachungs-Dashboard bietet eine visuelle Darstellung der Datenaktivität im Profil, einschließlich des Status der Profile Ihrer Daten. In diesem Tutorial erfahren Sie, wie Sie mit dem Monitoring-Dashboard die Profile Ihrer Daten über die Experience Platform-Benutzeroberfläche überwachen und so den Status der Profilverarbeitung verfolgen können.

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Experience Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   - [Datenflussausführungen](../../sources/notifications.md): Datenflussausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Häufigkeitskonfiguration ausgewählter Datenflüsse basieren.
- [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

## Überwachen des Profil-Dashboards {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Profilverarbeitung"
>abstract="Die Profilverarbeitungs-Ansicht enthält Informationen zu den in den Profildienst aufgenommenen Einträgen, einschließlich der Anzahl der erstellten und aktualisierten Profilfragmente sowie der Gesamtzahl der Profilfragmente."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Details zur Datenflussausführung"
>abstract="Auf der Seite mit den Datenflussausführungs-Details werden weitere Informationen zur Ausführung des Profil-Datenflusses angezeigt, einschließlich der Organisations-ID und der Datenflussausführungs-ID."

Um auf das **[!UICONTROL Profiles]**-Dashboard zuzugreifen, wählen Sie **[!UICONTROL Monitoring]** in der linken Navigationsleiste aus. Wählen Sie auf der Seite **[!UICONTROL Monitoring]** die Karte **[!UICONTROL Profiles]** aus.

![Die Karte Profile . Informationen zur Anzahl der empfangenen Datensätze, zur Anzahl der erstellten und aktualisierten Profilfragmente und zur Erfolgsrate werden angezeigt.](../assets/ui/monitor-profiles/focus-card.png)

Im Dashboard **[!UICONTROL Profiles]** Hauptprofils enthält die **[!UICONTROL Profiles]** Informationen über die Gesamtzahl der empfangenen Datensätze, die Anzahl der erstellten und aktualisierten Profilfragmente sowie die Erfolgsrate der erstellten und aktualisierten Profilfragmente.

Das Dashboard selbst enthält Metriken zur Profilverarbeitung. Standardmäßig zeigt das Dashboard Details zur Profilverarbeitung für die Quellen Ihres Unternehmens in den letzten 24 Stunden an.

![Das Profile-Dashboard. Es werden Informationen zur Anzahl der pro Quelle empfangenen Profildatensätze angezeigt.](../assets/ui/monitor-profiles/sources.png)

Die [!UICONTROL Profile processing] enthält Informationen zu den in [!DNL Profile] aufgenommenen Datensätzen, einschließlich der Anzahl der erstellten und aktualisierten Profilfragmente sowie der Gesamtzahl der Profilfragmente.

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Source name]** | Der Name der Quelle. |
| **[!UICONTROL Records received]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Records failed]** | Die Anzahl der Datensätze, die aufgrund von Fehlern aufgenommen, aber nicht in [!DNL Profile] wurden. |
| **[!UICONTROL Profile fragments created]** | Die Anzahl der hinzugefügten neuen [!DNL Profile]. |
| **[!UICONTROL Profile fragments updated]** | Die Anzahl der aktualisierten vorhandenen [!DNL Profile]. |
| **[!UICONTROL Total Profile fragments]** | Die Gesamtzahl der in [!DNL Profile] geschriebenen Datensätze, einschließlich aller vorhandenen aktualisierten [!DNL Profile] und neu erstellten [!DNL Profile]. |
| **[!UICONTROL Total failed dataflows]** | Die Anzahl der fehlgeschlagenen Datenflussausführungen. |

Sie können das Filtersymbol ![Filtersymbol](/help/images/icons/filter.png) neben dem Quellnamen auswählen, um Profilinformationen zur Verarbeitung für die Datenflüsse dieser ausgewählten Quelle anzuzeigen.

Alternativ können Sie auf **[!UICONTROL Dataflows]** im Umschalter klicken, um Details zur Profilverarbeitung für die Datenflüsse Ihres Unternehmens in den letzten 24 Stunden anzuzeigen.

![Das Profile-Dashboard. Es werden Informationen zur Anzahl der pro Datenfluss empfangenen Profildatensätze angezeigt.](../assets/ui/monitor-profiles/dataflows.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | Der Name des Datenflusses. |
| **[!UICONTROL Dataset]** | Der Name des Datensatzes, in den der Datenfluss eingefügt wird. |
| **[!UICONTROL Source name]** | Der Name der Quelle, zu der der Datenfluss gehört |
| **[!UICONTROL Data type]** | Der Typ der Daten, die vom Datensatz empfangen werden. |
| **[!UICONTROL Records received**] | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Records failed]** | Die Anzahl der Datensätze, die aufgrund von Fehlern aufgenommen, aber nicht in [!DNL Profile] wurden. |
| **[!UICONTROL Profile fragments created]** | Die Anzahl der hinzugefügten neuen [!DNL Profile]. |
| **[!UICONTROL Profile fragments updated]** | Die Anzahl der aktualisierten vorhandenen [!DNL Profile] |
| **[!UICONTROL Total Profile fragments]** | Die Gesamtzahl der in [!DNL Profile] geschriebenen Datensätze, einschließlich aller vorhandenen aktualisierten [!DNL Profile] und neu erstellten [!DNL Profile]. |
| **[!UICONTROL Total failed flow runs]** | Die Anzahl der fehlgeschlagenen Datenflussausführungen. |
| **[!UICONTROL Last active]** | Der Zeitstempel, wann der Datenfluss zuletzt ausgeführt wurde. |

Wählen Sie das Filtersymbol ![filter](/help/images/icons/filter.png) neben der Startzeit des Datenflusses aus, um weitere Informationen zur Ausführung des [!DNL Profile] Datenflusses anzuzeigen.

Ein Dashboard mit allen Datenflussausführungen wird angezeigt. Dieses Dashboard enthält Metriken zu den Datenflussausführungen sowie Diagramme, die die Erfolgsrate, die erstellten Profilfragmente und die aktualisierten Profilfragmente zeigen.

![Das Dashboard für Datenflussausführungen. Es werden Informationen zu den Datenflussausführungen angezeigt.](../assets/ui/monitor-profiles/dataflow-run.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

>[!NOTE]
>
>Wenn sich die Datenflussausführung im **[!UICONTROL Processing]** befindet, können Sie Informationen zur Bereitschaft anzeigen, indem Sie die Checkpoint-Status im Aufnahmeprozess sehen.
>
>![Die Sprechblase „Bereitschaft für die Profilaufnahme“ wird angezeigt.](../assets/ui/monitor-profiles/profile-ingestion-readiness.png){zoomable="yes" width="300"}

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Dataflow run start]** | Die Zeit, zu der die Datenflussausführung in UTC gestartet wurde. |
| **[!UICONTROL Data type]** | Der Typ der vom Datenfluss empfangenen Daten. |
| **[!UICONTROL Records received]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Records failed]** | Die Anzahl der Datensätze, die aufgrund von Fehlern aufgenommen, aber nicht in [!DNL Profile] wurden. |
| **[!UICONTROL Profile fragments created]** | Die Anzahl der hinzugefügten neuen [!DNL Profile]. |
| **[!UICONTROL Profile fragments updated]** | Die Anzahl der aktualisierten vorhandenen [!DNL Profile]. |
| **[!UICONTROL Total profile fragments]** | Die Gesamtzahl der in [!DNL Profile] geschriebenen Datensätze, einschließlich aller vorhandenen aktualisierten [!DNL Profile] und neu erstellten [!DNL Profile]. |
| **[!UICONTROL Processing time]** | Die Zeit, die für die Verarbeitung der Datenflussausführung benötigt wurde. |
| **[!UICONTROL Status]** | Der Status der Datenflussausführung. Zu den möglichen Werten gehören [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] und [!UICONTROL Processing]. |
| **[!UICONTROL Ready for customer segmentation]** | Ein Status, der anzeigt, ob die aufgenommenen Datensätze für die Verwendung in der Kundensegmentierung bereit sind. Zu den möglichen Werten gehören [!UICONTROL Yes], [!UICONTROL Failed], [!UICONTROL Queued] und [!UICONTROL Processing]. Selbst wenn der **Status** des Datenflusses verarbeitet wird, können Sie die Profile in der Kundensegmentierung verwenden, wenn der Wert dieses Felds „Ja“ lautet. |
| **[!UICONTROL Ready for lookup]** | Ein Status, der anzeigt, ob die aufgenommenen Datensätze für die Verwendung bei der Adobe Journey Optimizer-Suche bereit sind.  Zu den möglichen Werten gehören [!UICONTROL Yes], [!UICONTROL Failed], [!UICONTROL Queued] und [!UICONTROL Processing]. Selbst wenn der **Status** des Datenflusses verarbeitet wird, können Sie bei einem Wert dieses Felds von „Ja“ die Profile in der Journey Optimizer-Suche verwenden. |

Auf der Seite [!UICONTROL Dataflow run details] werden weitere Informationen zur Ausführung des [!DNL Profile]-Datenflusses angezeigt, einschließlich der Organisations-ID und der Datenflussausführungs-ID. Auf dieser Seite werden auch der entsprechende Fehlercode und die Fehlermeldung angezeigt, die von [!DNL Profile] bereitgestellt werden, falls während des Aufnahmevorgangs Fehler auftreten.

![Ein Dashboard mit detaillierten Informationen zum ausgewählten Datenfluss wird angezeigt.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Records received]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Records failed]** | Die Anzahl der Datensätze, die aufgrund von Fehlern aufgenommen, aber nicht in [!DNL Profile] wurden. |
| **[!UICONTROL Profile fragments created]** | Die Anzahl der hinzugefügten neuen [!DNL Profile]. |
| **[!UICONTROL Profile fragments updated]** | Die Anzahl der aktualisierten vorhandenen [!DNL Profile]. |
| **[!UICONTROL Status]** | Definiert den Gesamtstatus eines Datenflusses. Mögliche Statuswerte sind: <ul><li>`Success`: Gibt an, dass ein Datenfluss aktiv ist und Daten gemäß dem bereitgestellten Zeitplan aufnimmt.</li><li>`Failed`: Zeigt an, dass der Aktivierungsprozess eines Datenflusses aufgrund von Fehlern unterbrochen wurde. </li><li>`Processing`: Gibt an, dass der Datenfluss noch nicht aktiv ist. Dieser Status tritt häufig unmittelbar nach der Erstellung eines neuen Datenflusses auf.</li></ul> |
| **[!UICONTROL Dataflow run start]** | Datum und Uhrzeit des Starts des Datenflusses. |
| **[!UICONTROL Last updated]** | Datum und Uhrzeit der letzten Aktualisierung des Datenflusses. |
| **[!UICONTROL Error summary]** | Wenn die Ausführung des Datenflusses fehlgeschlagen ist, wird ein Fehlercode und eine Zusammenfassung angezeigt, warum die Ausführung des Datenflusses fehlgeschlagen ist. |
| **[!UICONTROL Dataflow run ID]** | Die ID der Datenflussausführung. |
| **[!UICONTROL IMS org ID]** | Die Organisations-ID, zu der der Datenfluss gehört. |

Darüber hinaus können Sie den Umschalter auswählen, um die fehlgeschlagenen oder übersprungenen Datensätze anzuzeigen. Der Abschnitt Fehler enthält Details zum Fehlercode und zur Anzahl der fehlgeschlagenen oder ausgeschlossenen Datensätze.
