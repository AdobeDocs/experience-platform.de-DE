---
keywords: Experience Platform; home; beliebte Themen; Identitäten überwachen; Datenflüsse überwachen; Datenflüsse; Datenflüsse; Identitäten;
description: Adobe Experience Platform Identity Service bietet Ihnen einen umfassenden Überblick über Ihre Kunden und ihr Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit für effektive, persönliche digitale Erlebnisse sorgen können. In diesem Tutorial erfahren Sie, wie Sie mithilfe der Experience Platform-Benutzeroberfläche Datenflüsse mit Identitäten überwachen können.
title: Überwachen von Datenflüssen auf Identitäten in der Benutzeroberfläche
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 15%

---

# Überwachen von Datenflüssen auf Identitäten in der Benutzeroberfläche

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

Das Monitoring-Dashboard bietet eine visuelle Darstellung der Datenaktivität innerhalb von Identitäten, einschließlich des Status der Identitäten Ihrer Daten. In diesem Tutorial erfahren Sie, wie Sie mithilfe des Monitoring-Dashboards die Identitäten Ihrer Daten mithilfe der Experience Platform-Benutzeroberfläche überwachen können, sodass Sie den Status der Identitätsverarbeitung verfolgen können.

## Erste Schritte {#getting-started}

- [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   - [Datenfluss-Ausführungen](../../sources/notifications.md): Datenfluss-Ausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration ausgewählter Datenflüsse basieren.
- [Identity Service](../../identity-service/home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kundinnen und Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

## Überwachen des Identitäten-Dashboards {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Identitätsverarbeitung"
>abstract="Die Identitätsverarbeitungs-Ansicht enthält Informationen zu den Datensätzen, die in den Identity Service aufgenommen werden, einschließlich der Anzahl der hinzugefügten Identitäten sowie der erstellten und aktualisierten Diagramme. Weitere Informationen zu Metriken und Diagrammen finden Sie im Handbuch zur Metrikdefinition."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Details zur Datenflussausführung"
>abstract="Auf der Seite mit den Datenflussausführungs-Details werden weitere Informationen zur Ausführung des Identitäts-Datenflusses angezeigt, einschließlich der Organisations-ID und der Datenflussausführungs-ID."

Um auf das Dashboard **[!UICONTROL Identitäten]** zuzugreifen, wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Überwachung]** aus. Wählen Sie auf der Seite **[!UICONTROL Überwachung]** die Karte **[!UICONTROL Identitäten]** aus.

![Die Karte Identitäten . Informationen zur Anzahl der empfangenen Datensätze, zur Anzahl der aufgenommenen Datensätze und zur Erfolgsrate werden angezeigt.](../assets/ui/monitor-identities/focus-card.png)

Im Dashboard **[!UICONTROL Identitäten]** enthält die Karte **[!UICONTROL Identitäten]** Informationen zur Gesamtzahl der empfangenen Datensätze, zur Anzahl der aufgenommenen Datensätze sowie zur Erfolgsrate der Datensatzaufnahme.

Das Dashboard selbst enthält Metriken zur Identitätsverarbeitung. Standardmäßig zeigt das Dashboard Details zur Identitätsverarbeitung für die Quellen Ihres Unternehmens in den letzten 24 Stunden an.

![Das Dashboard Identitäten . Informationen zur Anzahl der pro Quelle empfangenen Datensätze werden angezeigt.](../assets/ui/monitor-identities/sources.png)

Die Seite [!UICONTROL Identitätsverarbeitung] enthält Informationen zu in [!DNL Identity Service] erfassten Datensätzen, einschließlich der Anzahl hinzugefügter Identitäten, erstellter Diagramme und aktualisierter Diagramme.

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Identitätsmetriken | Beschreibung |
| ---------------- | ----------- |
| **[!UICONTROL empfangene Datensätze]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Die Anzahl der Datensätze, die aufgrund von Fehlern in den Daten nicht in Platform erfasst wurden. |
| **[!UICONTROL Übersprungene Datensätze]** | Die Anzahl der erfassten Datensätze, jedoch nicht in [!DNL Identity Service], da in der Datensatzzeile nur eine Kennung vorhanden war. |
| **[!UICONTROL Aufgenommene Datensätze]** | Die Anzahl der in [!DNL Identity Service] erfassten Datensätze. |
| **[!UICONTROL Hinzugefügte Identitäten]** | Die Anzahl neuer Kennungen, die [!DNL Identity Service] hinzugefügt wurden. |
| **[!UICONTROL Erstellte Diagramme]** | Die Anzahl neuer Identitätsdiagramme, die in [!DNL Identity Service] erstellt wurden. |
| **[!UICONTROL Diagramme aktualisiert]** | Die Anzahl vorhandener Identitätsdiagramme, die mit neuen Edges aktualisiert wurden. |
| **[!UICONTROL Gesamtzahl fehlgeschlagener Datenflüsse]** | Die Anzahl der fehlgeschlagenen Datenflüsse. |

Sie können das Filtersymbol ![Filtersymbol](/help/images/icons/filter.png) neben dem Quellnamen auswählen, um Informationen zur Identitätsverarbeitung für die Datenflüsse der ausgewählten Quelle anzuzeigen.

![Das Filtersymbol wird hervorgehoben. Wenn Sie dieses Symbol auswählen, können Sie die Datenflüsse der ausgewählten Quelle anzeigen.](../assets/ui/monitor-identities/sources-filter.png)

Alternativ können Sie **[!UICONTROL Datenflüsse]** auf dem Umschalter auswählen, um Details zur Identitätsverarbeitung für die Datenflüsse Ihrer Organisation in den letzten 24 Stunden anzuzeigen.

![Das Dashboard Identitäten . Informationen zur Anzahl der Identitäten, die pro Datenfluss empfangen werden, werden angezeigt.](../assets/ui/monitor-identities/dataflows.png)

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | Der Name des Datenflusses. |
| **[!UICONTROL Datensatz]** | Der Name des Datensatzes, in den der Datenfluss eingefügt wird. |
| **[!UICONTROL Source name]** | Der Name der Quelle, zu der der Datenfluss gehört. |
| **[!UICONTROL empfangene Datensätze]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Die Anzahl der Datensätze, die aufgrund von Fehlern in den Daten nicht in Platform erfasst wurden. |
| **[!UICONTROL Übersprungene Datensätze]** | Die Anzahl der erfassten Datensätze, jedoch nicht in [!DNL Identity Service], da in der Datensatzzeile nur eine Kennung vorhanden war. |
| **[!UICONTROL Aufgenommene Datensätze]** | Die Anzahl der in [!DNL Identity Service] erfassten Datensätze. |
| **[!UICONTROL Gesamte Datensätze]** | Die Gesamtzahl aller Datensätze, einschließlich fehlgeschlagener Datensätze, übersprungener Datensätze, hinzugefügter Identitäten und duplizierter Datensätze. |
| **[!UICONTROL Hinzugefügte Identitäten]** | Die Anzahl neuer Kennungen, die [!DNL Identity Service] hinzugefügt wurden. |
| **[!UICONTROL Erstellte Diagramme]** | Die Anzahl neuer Identitätsdiagramme, die in [!DNL Identity Service] erstellt wurden. |
| **[!UICONTROL Diagramme aktualisiert]** | Die Anzahl vorhandener Identitätsdiagramme, die mit neuen Edges aktualisiert wurden. |
| **[!UICONTROL Gesamtzahl fehlgeschlagener Datenflüsse]** | Die Anzahl der fehlgeschlagenen Datenflüsse. |

Wählen Sie das Filtersymbol ![filter](/help/images/icons/filter.png) neben der Startzeit des Datenflusses aus, um weitere Informationen zum Start des Datenflusses [!DNL Identity] anzuzeigen.

![Das Filtersymbol wird hervorgehoben. Durch Auswahl dieses Symbols können Sie Details zum ausgewählten Datenfluss anzeigen.](../assets/ui/monitor-identities/dataflows-filter.png)

Auf der Seite [!UICONTROL Datenfluss-Ausführungsdetails] werden weitere Informationen zu Ihrem [!DNL Identity]-Datenfluss angezeigt, einschließlich der Organisations-ID und der Kennung des Datenflusses. Auf dieser Seite werden auch der entsprechende Fehlercode und die Fehlermeldung angezeigt, die von [!DNL Identity Service] bereitgestellt werden, sollte es im Aufnahmeprozess zu Fehlern kommen.

![Ein Dashboard mit detaillierten Informationen zum ausgewählten Datenfluss wird angezeigt.](../assets/ui/monitor-identities/dataflow-run-details.png)

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL empfangene Datensätze]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Die Anzahl der Datensätze, die aufgrund von Fehlern in den Daten nicht in Platform erfasst wurden. |
| **[!UICONTROL Übersprungene Datensätze]** | Die Anzahl der erfassten Datensätze, jedoch nicht in [!DNL Identity Service], da in der Datensatzzeile nur eine Kennung vorhanden war. |
| **[!UICONTROL Aufgenommene Datensätze]** | Die Anzahl der in [!DNL Identity Service] erfassten Datensätze. |
| **[!UICONTROL Hinzugefügte Identitäten]** | Die Anzahl neuer Kennungen, die [!DNL Identity Service] hinzugefügt wurden. |
| **[!UICONTROL Erstellte Diagramme]** | Die Anzahl neuer Identitätsdiagramme, die in [!DNL Identity Service] erstellt wurden. |
| **[!UICONTROL Diagramme aktualisiert]** | Die Anzahl vorhandener Identitätsdiagramme, die mit neuen Edges aktualisiert wurden. |
| **[!UICONTROL Status]** | Definiert den Gesamtstatus eines Datenflusses. Mögliche Statuswerte sind: <ul><li>`Success`: Gibt an, dass ein Datenfluss aktiv ist und Daten gemäß dem Zeitplan erfasst, den er bereitgestellt hat.</li><li>`Failed`: Gibt an, dass die Aktivierung eines Datenflusses aufgrund von Fehlern unterbrochen wurde. </li><li>`Processing`: Gibt an, dass der Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf.</li></ul> |
| **[!UICONTROL Start des Datenflusses]** | Datum und Uhrzeit der Ausführung des Datenflusses. |
| **[!UICONTROL Zuletzt aktualisiert]** | Datum und Uhrzeit der letzten Aktualisierung des Datenflusses. |
| **[!UICONTROL Fehlerzusammenfassung]** | Wenn die Ausführung des Datenflusses fehlgeschlagen ist, werden ein Fehlercode und eine Zusammenfassung des Fehlers beim Ausführen des Datenflusses angezeigt. |
| **[!UICONTROL Dataflow run ID]** | Die Kennung des Datenflusses. |
| **[!UICONTROL IMS-Organisations-ID]** | Die Organisations-ID, zu der der Datenfluss gehört. |

Darüber hinaus können Sie die Umschaltfläche auswählen, um die fehlgeschlagenen oder übersprungenen Datensätze anzuzeigen. Der Abschnitt &quot;Fehler&quot;enthält Details zum Fehlercode und zur Anzahl der fehlgeschlagenen oder ausgeschlossenen Datensätze.
