---
keywords: Experience Platform; home; beliebte Themen; Monitorprofile; Überwachen von Datenflüssen; Datenflüsse; profile; Echtzeit-Kundenprofil
description: Mit dem Echtzeit-Kundenprofil können Sie eine ganzheitliche Sicht auf jeden einzelnen Kunden anzeigen, indem Sie Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieter-Kanälen, kombinieren. In diesem Tutorial erfahren Sie, wie Sie Datenflüsse mit Profilen über die Experience Platform-Benutzeroberfläche überwachen können.
title: Überwachen von Datenflüssen für Profile in der Benutzeroberfläche
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 17%

---

# Überwachen von Datenflüssen auf Profile in der Benutzeroberfläche

Mit dem Echtzeit-Kundenprofil können Sie eine ganzheitliche Sicht auf jeden einzelnen Kunden anzeigen, indem Sie Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieter-Kanälen, kombinieren. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

Das Monitoring-Dashboard bietet eine visuelle Darstellung der Datenaktivität innerhalb des Profils, einschließlich des Status Ihrer Datenprofile. In diesem Tutorial erfahren Sie, wie Sie mithilfe des Monitoring-Dashboards die Profile Ihrer Daten mithilfe der Experience Platform-Benutzeroberfläche überwachen können. So können Sie den Status der Profilverarbeitung verfolgen.

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   - [Datenfluss-Abläufe](../../sources/notifications.md): Datenflüsse sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration ausgewählter Datenflüsse basieren.
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
>title="Datenflussausführungs-Details"
>abstract="Auf der Seite mit den Datenflussausführungs-Details werden weitere Informationen zur Ausführung des Profil-Datenflusses angezeigt, einschließlich der Organisations-ID und der Datenflussausführungs-ID."

So greifen Sie auf die **[!UICONTROL Profile]** Dashboard, auswählen **[!UICONTROL Überwachung]** in der linken Navigation. Einmal im **[!UICONTROL Überwachung]** Seite, wählen Sie die **[!UICONTROL Profile]** Karte.

![Die Karte Profile . Informationen zur Anzahl der empfangenen Datensätze, zur Anzahl der erstellten und aktualisierten Profilfragmente und zur Erfolgsrate werden angezeigt.](../assets/ui/monitor-profiles/focus-card.png)

Im Hauptmenü **[!UICONTROL Profile]** Dashboard, die **[!UICONTROL Profile]** enthält Informationen zur Gesamtzahl der empfangenen Datensätze, zur Anzahl der erstellten und aktualisierten Profilfragmente sowie zur Erfolgsrate der erstellten und aktualisierten Profilfragmente.

Das Dashboard selbst enthält Metriken zur Profilverarbeitung. Standardmäßig zeigt das Dashboard Details zur Profilverarbeitung für die Quellen Ihres Unternehmens in den letzten 24 Stunden an.

![Das Dashboard Profile . Informationen zur Anzahl der pro Quelle empfangenen Profildatensätze werden angezeigt.](../assets/ui/monitor-profiles/sources.png)

Die [!UICONTROL Profilverarbeitung] Seite enthält Informationen zu Datensätzen, die in [!DNL Profile], einschließlich der Anzahl der erstellten Profilfragmente, der aktualisierten Profilfragmente und der Gesamtzahl der Profilfragmente.

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Name der Quelle]** | Der Name der Quelle. |
| **[!UICONTROL Empfangene Einträge]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Fehlgeschlagene Einträge]** | Die Anzahl der Datensätze, die erfasst wurden, jedoch nicht in [!DNL Profile] aufgrund von Fehlern. |
| **[!UICONTROL Erstellen von Profilfragmenten]** | Die Zahl der neuen Nettoempfänger [!DNL Profile] Fragmente hinzugefügt. |
| **[!UICONTROL Profilfragmente aktualisiert]** | Die Anzahl der vorhandenen [!DNL Profile] Fragmente aktualisiert. |
| **[!UICONTROL Profilfragmente insgesamt]** | Die Gesamtzahl der in [!DNL Profile], einschließlich aller vorhandenen [!DNL Profile] Fragmente aktualisiert und neu [!DNL Profile] erstellte Fragmente. |
| **[!UICONTROL Gesamtzahl fehlgeschlagener Datenflüsse]** | Die Anzahl der fehlgeschlagenen Datenflüsse. |

Sie können das Filtersymbol auswählen ![Filtersymbol](../assets/ui/monitor-profiles/filter.png) neben dem Quellnamen, um Informationen zur Profilverarbeitung für die Datenflüsse der ausgewählten Quelle anzuzeigen.

![Das Filtersymbol wird hervorgehoben. Durch Auswahl dieses Symbols können Sie die Datenflüsse der ausgewählten Quelle anzeigen.](../assets/ui/monitor-profiles/sources-filter.png)

Alternativ können Sie **[!UICONTROL Datenflüsse]** auf den Umschalter klicken, um Details zur Profilverarbeitung für die Datenflüsse Ihrer Organisation in den letzten 24 Stunden anzuzeigen.

![Das Dashboard Profile . Es werden Informationen zur Anzahl der pro Datenfluss empfangenen Profildatensätze angezeigt.](../assets/ui/monitor-profiles/dataflows.png)

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Datenfluss]** | Der Name des Datenflusses. |
| **[!UICONTROL Datensatz]** | Der Name des Datensatzes, in den der Datenfluss eingefügt wird. |
| **[!UICONTROL Name der Quelle]** | Der Name der Quelle, zu der der Datenfluss gehört. |
| **[!UICONTROL Empfangene Einträge**] | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Fehlgeschlagene Einträge]** | Die Anzahl der Datensätze, die erfasst wurden, jedoch nicht in [!DNL Profile] aufgrund von Fehlern. |
| **[!UICONTROL Erstellen von Profilfragmenten]** | Die Zahl der neuen Nettoempfänger [!DNL Profile] Fragmente hinzugefügt. |
| **[!UICONTROL Profilfragmente aktualisiert]** | Die Anzahl der vorhandenen [!DNL Profile] Fragmente aktualisiert |
| **[!UICONTROL Profilfragmente insgesamt]** | Die Gesamtzahl der in [!DNL Profile], einschließlich aller vorhandenen [!DNL Profile] Fragmente aktualisiert und neu [!DNL Profile] erstellte Fragmente. |
| **[!UICONTROL Gesamtanzahl fehlgeschlagener Durchläufe]** | Die Anzahl der fehlgeschlagenen Datenflüsse. |
| **[!UICONTROL Letzte aktive]** | Der Zeitstempel, mit dem der Datenfluss zuletzt ausgeführt wurde. |

Filtersymbol auswählen ![filter](../assets/ui/monitor-profiles/filter.png) neben der Startzeit des Datenflusses, um weitere Informationen zu Ihrer [!DNL Profile] dataflow ausführen.

![Das Filtersymbol wird hervorgehoben. Wenn Sie dieses Symbol auswählen, können Sie Details zum ausgewählten Datenfluss anzeigen.](../assets/ui/monitor-profiles/dataflows-filter.png)

Die [!UICONTROL Datenfluss-Ausführungsdetails] Seite zeigt weitere Informationen zu Ihrer [!DNL Profile] dataflow-Ausführung, einschließlich der Organisations-ID und der Datenfluss-Start-ID. Auf dieser Seite werden auch der entsprechende Fehlercode und die entsprechende Fehlermeldung angezeigt, die von [!DNL Profile], falls im Aufnahmeprozess Fehler auftreten sollten.

![Ein Dashboard mit detaillierten Informationen zum ausgewählten Datenfluss wird angezeigt.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Empfangene Einträge]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Fehlgeschlagene Einträge]** | Die Anzahl der Datensätze, die erfasst wurden, jedoch nicht in [!DNL Profile] aufgrund von Fehlern. |
| **[!UICONTROL Erstellen von Profilfragmenten]** | Die Zahl der neuen Nettoempfänger [!DNL Profile] Fragmente hinzugefügt. |
| **[!UICONTROL Profilfragmente aktualisiert]** | Die Anzahl der vorhandenen [!DNL Profile] Fragmente aktualisiert. |
| **[!UICONTROL Status]** | Definiert den Gesamtstatus eines Datenflusses. Mögliche Statuswerte sind: <ul><li>`Success`: Gibt an, dass ein Datenfluss aktiv ist und Daten gemäß dem festgelegten Zeitplan erfasst.</li><li>`Failed`: Gibt an, dass der Aktivierungsprozess eines Datenflusses aufgrund von Fehlern unterbrochen wurde. </li><li>`Processing`: Gibt an, dass der Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf.</li></ul> |
| **[!UICONTROL Start des Datenflusses]** | Datum und Uhrzeit der Ausführung des Datenflusses. |
| **[!UICONTROL Zuletzt aktualisiert]** | Datum und Uhrzeit der letzten Aktualisierung des Datenflusses. |
| **[!UICONTROL Fehlerzusammenfassung]** | Wenn die Ausführung des Datenflusses fehlgeschlagen ist, werden ein Fehlercode und eine Zusammenfassung des Fehlers beim Ausführen des Datenflusses angezeigt. |
| **[!UICONTROL Dataflow-run-ID]** | Die Kennung des Datenflusses. |
| **[!UICONTROL Kennung der IMS-Organisation]** | Die Organisations-ID, zu der der Datenfluss gehört. |

Darüber hinaus können Sie die Umschaltfläche auswählen, um die fehlgeschlagenen oder übersprungenen Datensätze anzuzeigen. Der Abschnitt &quot;Fehler&quot;enthält Details zum Fehlercode und zur Anzahl der fehlgeschlagenen oder ausgeschlossenen Datensätze.
