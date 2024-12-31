---
keywords: Experience Platform;Startseite;beliebte Themen;Profile überwachen;Datenflüsse überwachen;Datenflüsse;Profil;Echtzeit-Kundenprofil;
description: Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. In diesem Tutorial erfahren Sie, wie Sie Datenflüsse mit Profilen mithilfe der Experience Platform-Benutzeroberfläche überwachen können.
title: Überwachen von Datenflüssen für Profile in der Benutzeroberfläche
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 14%

---

# Überwachen von Datenflüssen für Profile in der Benutzeroberfläche

Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

Das Überwachungs-Dashboard bietet eine visuelle Darstellung der Datenaktivität im Profil, einschließlich des Status der Profile Ihrer Daten. In diesem Tutorial erfahren Sie, wie Sie mit dem Monitoring-Dashboard die Profile Ihrer Daten über die Experience Platform-Benutzeroberfläche überwachen und so den Status der Profilverarbeitung verfolgen können.

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   - [Datenflussausführungen](../../sources/notifications.md): Datenflussausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Häufigkeitskonfiguration ausgewählter Datenflüsse basieren.
- [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

## Überwachen des Profil-Dashboards {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Profilverarbeitung"
>abstract="Die Profilverarbeitungs-Ansicht enthält Informationen zu den in den Profildienst aufgenommenen Datensätzen, einschließlich der Anzahl der erstellten und aktualisierten Profilfragmente sowie der Gesamtzahl der Profilfragmente."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Details zur Datenflussausführung"
>abstract="Auf der Seite mit den Datenflussausführungs-Details werden weitere Informationen zur Ausführung des Profil-Datenflusses angezeigt, einschließlich der Organisations-ID und der Datenflussausführungs-ID."

Um auf das Dashboard **[!UICONTROL Profile]** zuzugreifen, wählen Sie **[!UICONTROL Monitoring]** in der linken Navigationsleiste aus. Wählen Sie auf der **[!UICONTROL Überwachung]** die Karte **[!UICONTROL Profile]** aus.

![Die Karte Profile . Informationen zur Anzahl der empfangenen Datensätze, zur Anzahl der erstellten und aktualisierten Profilfragmente und zur Erfolgsrate werden angezeigt.](../assets/ui/monitor-profiles/focus-card.png)

Im Hauptdashboard **[!UICONTROL Profile]** zeigt die Karte **[!UICONTROL Profile]** Informationen über die Gesamtzahl der empfangenen Datensätze, die Anzahl der erstellten und aktualisierten Profilfragmente sowie die Erfolgsrate der erstellten und aktualisierten Profilfragmente an.

Das Dashboard selbst enthält Metriken zur Profilverarbeitung. Standardmäßig zeigt das Dashboard Details zur Profilverarbeitung für die Quellen Ihres Unternehmens in den letzten 24 Stunden an.

![Das Profile-Dashboard. Es werden Informationen zur Anzahl der pro Quelle empfangenen Profildatensätze angezeigt.](../assets/ui/monitor-profiles/sources.png)

Die [!UICONTROL Profilverarbeitung] enthält Informationen zu Datensätzen, die in [!DNL Profile] aufgenommen wurden, darunter die Anzahl der erstellten und der aktualisierten Profilfragmente sowie die Gesamtzahl der Profilfragmente.

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Source-Name]** | Der Name der Quelle. |
| **[!UICONTROL Empfangene Datensätze]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Die Anzahl der Datensätze, die aufgrund von Fehlern aufgenommen, aber nicht in [!DNL Profile] wurden. |
| **[!UICONTROL Profilfragmente erstellt]** | Die Anzahl der hinzugefügten neuen [!DNL Profile]. |
| **[!UICONTROL Profilfragmente aktualisiert]** | Die Anzahl der aktualisierten vorhandenen [!DNL Profile]. |
| **[!UICONTROL Gesamtzahl der Profilfragmente]** | Die Gesamtzahl der in [!DNL Profile] geschriebenen Datensätze, einschließlich aller vorhandenen aktualisierten [!DNL Profile] und neu erstellten [!DNL Profile]. |
| **[!UICONTROL Gesamtzahl fehlgeschlagener Datenflüsse]** | Die Anzahl der fehlgeschlagenen Datenflussausführungen. |

Sie können das Filtersymbol ![Filtersymbol](/help/images/icons/filter.png) neben dem Quellnamen auswählen, um Profilinformationen zur Verarbeitung für die Datenflüsse dieser ausgewählten Quelle anzuzeigen.

![Das Filtersymbol ist hervorgehoben. Durch Auswahl dieses Symbols können Sie die Datenflüsse der ausgewählten Quelle anzeigen.](../assets/ui/monitor-profiles/sources-filter.png)

Alternativ können Sie auf **[!UICONTROL Datenflüsse]** im Umschalter klicken, um Details zur Profilverarbeitung für die Datenflüsse Ihres Unternehmens in den letzten 24 Stunden anzuzeigen.

![Das Profile-Dashboard. Es werden Informationen zur Anzahl der pro Datenfluss empfangenen Profildatensätze angezeigt.](../assets/ui/monitor-profiles/dataflows.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Datenfluss]** | Der Name des Datenflusses. |
| **[!UICONTROL Datensatz]** | Der Name des Datensatzes, in den der Datenfluss eingefügt wird. |
| **[!UICONTROL Source-Name]** | Der Name der Quelle, zu der der Datenfluss gehört |
| **[!UICONTROL Empfangene Datensätze**] | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Die Anzahl der Datensätze, die aufgrund von Fehlern aufgenommen, aber nicht in [!DNL Profile] wurden. |
| **[!UICONTROL Profilfragmente erstellt]** | Die Anzahl der hinzugefügten neuen [!DNL Profile]. |
| **[!UICONTROL Profilfragmente aktualisiert]** | Die Anzahl der aktualisierten vorhandenen [!DNL Profile] |
| **[!UICONTROL Gesamtzahl der Profilfragmente]** | Die Gesamtzahl der in [!DNL Profile] geschriebenen Datensätze, einschließlich aller vorhandenen aktualisierten [!DNL Profile] und neu erstellten [!DNL Profile]. |
| **[!UICONTROL Gesamtzahl fehlgeschlagener Flussdurchgänge]** | Die Anzahl der fehlgeschlagenen Datenflussausführungen. |
| **[!UICONTROL Zuletzt aktiv]** | Der Zeitstempel, wann der Datenfluss zuletzt ausgeführt wurde. |

Wählen Sie das Filtersymbol ![filter](/help/images/icons/filter.png) neben der Startzeit des Datenflusses aus, um weitere Informationen zur Ausführung des [!DNL Profile] Datenflusses anzuzeigen.

![Das Filtersymbol ist hervorgehoben. Durch Auswahl dieses Symbols können Sie Details zum ausgewählten Datenfluss anzeigen.](../assets/ui/monitor-profiles/dataflows-filter.png)

Auf [!UICONTROL  Seite „Datenflussausführungs-]&quot; werden weitere Informationen zur Ausführung des [!DNL Profile]-Datenflusses angezeigt, einschließlich der Organisations-ID und der Datenflussausführungs-ID. Auf dieser Seite werden auch der entsprechende Fehlercode und die Fehlermeldung angezeigt, die von [!DNL Profile] bereitgestellt werden, falls während des Aufnahmevorgangs Fehler auftreten.

![Ein Dashboard mit detaillierten Informationen zum ausgewählten Datenfluss wird angezeigt.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Empfangene Datensätze]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Die Anzahl der Datensätze, die aufgrund von Fehlern aufgenommen, aber nicht in [!DNL Profile] wurden. |
| **[!UICONTROL Profilfragmente erstellt]** | Die Anzahl der hinzugefügten neuen [!DNL Profile]. |
| **[!UICONTROL Profilfragmente aktualisiert]** | Die Anzahl der aktualisierten vorhandenen [!DNL Profile]. |
| **[!UICONTROL Status]** | Definiert den Gesamtstatus eines Datenflusses. Mögliche Statuswerte sind: <ul><li>`Success`: Gibt an, dass ein Datenfluss aktiv ist und Daten gemäß dem bereitgestellten Zeitplan aufnimmt.</li><li>`Failed`: Zeigt an, dass der Aktivierungsprozess eines Datenflusses aufgrund von Fehlern unterbrochen wurde. </li><li>`Processing`: Gibt an, dass der Datenfluss noch nicht aktiv ist. Dieser Status tritt häufig unmittelbar nach der Erstellung eines neuen Datenflusses auf.</li></ul> |
| **[!UICONTROL Start der Datenflussausführung]** | Datum und Uhrzeit des Starts des Datenflusses. |
| **[!UICONTROL Zuletzt aktualisiert]** | Datum und Uhrzeit der letzten Aktualisierung des Datenflusses. |
| **[!UICONTROL Fehlerzusammenfassung]** | Wenn die Ausführung des Datenflusses fehlgeschlagen ist, wird ein Fehlercode und eine Zusammenfassung angezeigt, warum die Ausführung des Datenflusses fehlgeschlagen ist. |
| **[!UICONTROL Datenflussausführungs-ID]** | Die ID der Datenflussausführung. |
| **[!UICONTROL IMS-Organisations-ID]** | Die Organisations-ID, zu der der Datenfluss gehört. |

Darüber hinaus können Sie den Umschalter auswählen, um die fehlgeschlagenen oder übersprungenen Datensätze anzuzeigen. Der Abschnitt Fehler enthält Details zum Fehlercode und zur Anzahl der fehlgeschlagenen oder ausgeschlossenen Datensätze.
