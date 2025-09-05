---
keywords: Experience Platform;Startseite;beliebte Themen;Überwachen von Identitäten;Überwachen von Datenflüssen;Datenflüsse;Identitäten;
description: Adobe Experience Platform Identity Service bietet Ihnen einen umfassenden Überblick über Ihre Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend zusammenführen und so wirkungsvolle, persönliche digitale Erlebnisse in Echtzeit bereitstellen können. In diesem Tutorial erfahren Sie, wie Sie Datenflüsse mit Identitäten mithilfe der Benutzeroberfläche von Experience Platform überwachen können.
title: Überwachen von Datenflüssen für Identitäten in der Benutzeroberfläche
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 14%

---

# Überwachen von Datenflüssen für Identitäten in der Benutzeroberfläche

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

Das Monitoring-Dashboard bietet Ihnen eine visuelle Darstellung der Datenaktivität innerhalb von Identitäten, einschließlich des Status der Identitäten Ihrer Daten. In diesem Tutorial erfahren Sie, wie Sie mit dem Überwachungs-Dashboard die Identitäten Ihrer Daten mithilfe der Experience Platform-Benutzeroberfläche überwachen und so den Status der Identitätsverarbeitung verfolgen können.

## Erste Schritte {#getting-started}

- [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Experience Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   - [Datenflussausführungen](../../sources/notifications.md): Datenflussausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Häufigkeitskonfiguration ausgewählter Datenflüsse basieren.
- [Identity Service](../../identity-service/home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kundinnen und Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

## Überwachen des Identitäten-Dashboards {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Identitätsverarbeitung"
>abstract="Die Identitätsverarbeitungs-Ansicht enthält Informationen zu den Einträgen, die in den Identity Service aufgenommen werden, einschließlich der Anzahl der hinzugefügten Identitäten sowie der erstellten und aktualisierten Diagramme. Weitere Informationen zu Metriken und Diagrammen finden Sie im Handbuch zur Metrikdefinition."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Details zur Datenflussausführung"
>abstract="Auf der Seite mit den Datenflussausführungs-Details werden weitere Informationen zur Ausführung des Identitäts-Datenflusses angezeigt, einschließlich der Organisations-ID und der Datenflussausführungs-ID."

Um auf das Dashboard **[!UICONTROL Identitäten]** zuzugreifen, wählen Sie **[!UICONTROL Monitoring]** in der linken Navigationsleiste aus. Wählen Sie auf der **[!UICONTROL Überwachung]** die Karte **[!UICONTROL Identitäten]** aus.

![Die Identitätskarte. Es werden Informationen über die Anzahl der empfangenen Datensätze, die Anzahl der aufgenommenen Datensätze und die Erfolgsrate angezeigt.](../assets/ui/monitor-identities/focus-card.png)

Im Haupt **[!UICONTROL Identitäten]**-Dashboard zeigt die Karte **[!UICONTROL Identitäten]** Informationen über die Gesamtzahl der empfangenen Datensätze, die Anzahl der aufgenommenen Datensätze sowie die Erfolgsrate der Datensatzaufnahme an.

Das Dashboard selbst enthält Metriken zur Identitätsverarbeitung. Standardmäßig zeigt das Dashboard Details zur Identitätsverarbeitung für die Quellen Ihrer Organisation in den letzten 24 Stunden an.

![Das Identitäts-Dashboard. Es werden Informationen zur Anzahl der pro Quelle empfangenen Datensätze angezeigt.](../assets/ui/monitor-identities/sources.png)

Die [!UICONTROL Identitätsverarbeitung] enthält Informationen zu Datensätzen, die in [!DNL Identity Service] aufgenommen werden, einschließlich der Anzahl der hinzugefügten Identitäten sowie der erstellten und aktualisierten Diagramme.

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Identitätsmetriken | Beschreibung |
| ---------------- | ----------- |
| **[!UICONTROL Empfangene Datensätze]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Die Anzahl der Datensätze, die aufgrund von Datenfehlern nicht in Experience Platform aufgenommen wurden. |
| **[!UICONTROL Datensätze übersprungen]** | Die Anzahl der Datensätze, die aufgenommen, aber nicht in [!DNL Identity Service], weil es nur eine Kennung in der Datensatzzeile gab. |
| **[!UICONTROL Aufgenommene Datensätze]** | Die Anzahl der Datensätze, die in [!DNL Identity Service] aufgenommen werden. |
| **[!UICONTROL Identitäten hinzugefügt]** | Die Anzahl der neu zu [!DNL Identity Service] hinzugefügten Kennungen. |
| **[!UICONTROL Diagramme erstellt]** | Die Anzahl der in [!DNL Identity Service] erstellten neuen Identitätsdiagramme. |
| **[!UICONTROL Diagramme aktualisiert]** | Die Anzahl der vorhandenen Identitätsdiagramme, die mit neuen Kanten aktualisiert wurden. |
| **[!UICONTROL Gesamtzahl fehlgeschlagener Datenflüsse]** | Die Anzahl der fehlgeschlagenen Datenflussausführungen. |

Sie können das Filtersymbol ![Filtersymbol](/help/images/icons/filter.png) neben dem Quellnamen auswählen, um Informationen zur Identitätsverarbeitung für die Datenflüsse dieser ausgewählten Quelle anzuzeigen.

![Das Filtersymbol ist hervorgehoben. Durch Auswahl dieses Symbols können Sie die Datenflüsse der ausgewählten Quelle anzeigen.](../assets/ui/monitor-identities/sources-filter.png)

Alternativ können Sie auf **[!UICONTROL Datenflüsse]** im Umschalter klicken, um Details zur Identitätsverarbeitung für die Datenflüsse Ihrer Organisation in den letzten 24 Stunden anzuzeigen.

![Das Identitäts-Dashboard. Es werden Informationen zur Anzahl der pro Datenfluss empfangenen Identitäten angezeigt.](../assets/ui/monitor-identities/dataflows.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Datenfluss]** | Der Name des Datenflusses. |
| **[!UICONTROL Datensatz]** | Der Name des Datensatzes, in den der Datenfluss eingefügt wird. |
| **[!UICONTROL Source-Name]** | Der Name der Quelle, zu der der Datenfluss gehört |
| **[!UICONTROL Empfangene Datensätze]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Die Anzahl der Datensätze, die aufgrund von Datenfehlern nicht in Experience Platform aufgenommen wurden. |
| **[!UICONTROL Datensätze übersprungen]** | Die Anzahl der Datensätze, die aufgenommen, aber nicht in [!DNL Identity Service], weil es nur eine Kennung in der Datensatzzeile gab. |
| **[!UICONTROL Aufgenommene Datensätze]** | Die Anzahl der Datensätze, die in [!DNL Identity Service] aufgenommen werden. |
| **[!UICONTROL Einträge insgesamt]** | Die Gesamtzahl aller Datensätze, einschließlich fehlgeschlagener, übersprungener, hinzugefügter Identitäten und duplizierter Datensätze. |
| **[!UICONTROL Identitäten hinzugefügt]** | Die Anzahl der neu zu [!DNL Identity Service] hinzugefügten Kennungen. |
| **[!UICONTROL Diagramme erstellt]** | Die Anzahl der in [!DNL Identity Service] erstellten neuen Identitätsdiagramme. |
| **[!UICONTROL Diagramme aktualisiert]** | Die Anzahl der vorhandenen Identitätsdiagramme, die mit neuen Kanten aktualisiert wurden. |
| **[!UICONTROL Gesamtzahl fehlgeschlagener Datenflüsse]** | Die Anzahl der fehlgeschlagenen Datenflussausführungen. |

Wählen Sie das Filtersymbol ![filter](/help/images/icons/filter.png) neben der Startzeit des Datenflusses aus, um weitere Informationen zur Ausführung des [!DNL Identity] Datenflusses anzuzeigen.

![Das Filtersymbol ist hervorgehoben. Durch Auswahl dieses Symbols können Sie Details zum ausgewählten Datenfluss anzeigen.](../assets/ui/monitor-identities/dataflows-filter.png)

Auf [!UICONTROL  Seite „Datenflussausführungs-]&quot; werden weitere Informationen zur Ausführung des [!DNL Identity]-Datenflusses angezeigt, einschließlich der Organisations-ID und der Datenflussausführungs-ID. Auf dieser Seite werden auch der entsprechende Fehlercode und die Fehlermeldung angezeigt, die von [!DNL Identity Service] bereitgestellt werden, falls während des Aufnahmevorgangs Fehler auftreten.

![Ein Dashboard mit detaillierten Informationen zum ausgewählten Datenfluss wird angezeigt.](../assets/ui/monitor-identities/dataflow-run-details.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| -------| ----------- |
| **[!UICONTROL Empfangene Datensätze]** | Die Anzahl der vom Data Lake empfangenen Datensätze. |
| **[!UICONTROL Datensätze fehlgeschlagen]** | Die Anzahl der Datensätze, die aufgrund von Datenfehlern nicht in Experience Platform aufgenommen wurden. |
| **[!UICONTROL Datensätze übersprungen]** | Die Anzahl der Datensätze, die aufgenommen, aber nicht in [!DNL Identity Service], weil es nur eine Kennung in der Datensatzzeile gab. |
| **[!UICONTROL Aufgenommene Datensätze]** | Die Anzahl der Datensätze, die in [!DNL Identity Service] aufgenommen werden. |
| **[!UICONTROL Identitäten hinzugefügt]** | Die Anzahl der neu zu [!DNL Identity Service] hinzugefügten Kennungen. |
| **[!UICONTROL Diagramme erstellt]** | Die Anzahl der in [!DNL Identity Service] erstellten neuen Identitätsdiagramme. |
| **[!UICONTROL Diagramme aktualisiert]** | Die Anzahl der vorhandenen Identitätsdiagramme, die mit neuen Kanten aktualisiert wurden. |
| **[!UICONTROL Status]** | Definiert den Gesamtstatus eines Datenflusses. Mögliche Statuswerte sind: <ul><li>`Success`: Gibt an, dass ein Datenfluss aktiv ist und Daten gemäß dem bereitgestellten Zeitplan aufnimmt.</li><li>`Failed`: Zeigt an, dass der Aktivierungsprozess eines Datenflusses aufgrund von Fehlern unterbrochen wurde. </li><li>`Processing`: Gibt an, dass der Datenfluss noch nicht aktiv ist. Dieser Status tritt häufig unmittelbar nach der Erstellung eines neuen Datenflusses auf.</li></ul> |
| **[!UICONTROL Start der Datenflussausführung]** | Datum und Uhrzeit des Starts des Datenflusses. |
| **[!UICONTROL Zuletzt aktualisiert]** | Datum und Uhrzeit der letzten Aktualisierung des Datenflusses. |
| **[!UICONTROL Fehlerzusammenfassung]** | Wenn die Ausführung des Datenflusses fehlgeschlagen ist, wird ein Fehlercode und eine Zusammenfassung angezeigt, warum die Ausführung des Datenflusses fehlgeschlagen ist. |
| **[!UICONTROL Datenflussausführungs-ID]** | Die ID der Datenflussausführung. |
| **[!UICONTROL IMS-Organisations-ID]** | Die Organisations-ID, zu der der Datenfluss gehört. |

Darüber hinaus können Sie den Umschalter auswählen, um die fehlgeschlagenen oder übersprungenen Datensätze anzuzeigen. Der Abschnitt Fehler enthält Details zum Fehlercode und zur Anzahl der fehlgeschlagenen oder ausgeschlossenen Datensätze.
