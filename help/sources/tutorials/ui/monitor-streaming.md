---
keywords: Experience Platform;Startseite;beliebte Themen;Konten überwachen;Datenflüsse überwachen;Datenflüsse
description: Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen nach einem bestimmten Zeitplan aufzunehmen. In diesem Tutorial werden Schritte zum Überwachen von Streaming-Datenflüssen aus dem Arbeitsbereich Quellen beschrieben.
title: Überwachen von Datenflüssen für Streaming-Quellen in der Benutzeroberfläche
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 16%

---

# Überwachen von Datenflüssen für Streaming-Quellen in der Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Überwachen von Datenflüssen für Streaming-Quellen mithilfe des Arbeitsbereichs [!UICONTROL Quellen] beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Datenflüsse](../../../dataflows/home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Experience Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   * [Datenflussausführungen](../../notifications.md): Datenflussausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Häufigkeitskonfiguration ausgewählter Datenflüsse basieren.
* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Überwachen von Datenflüssen für Streaming-Quellen

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Um vorhandene Datenflüsse für Streaming-Quellen anzuzeigen, wählen Sie **[!UICONTROL Datenflüsse]** in der oberen Kopfzeile aus.

![Katalog](../../images/tutorials/monitor-streaming/catalog.png)

Die [!UICONTROL Datenflüsse] enthält eine Liste aller vorhandenen Datenflüsse in Ihrer Organisation, einschließlich Informationen zu ihren Quelldaten, ihrem Kontonamen und dem Ausführungsstatus des Datenflusses.

Wählen Sie den Namen des Datenflusses aus, den Sie anzeigen möchten.

![Datenflüsse](../../images/tutorials/monitor-streaming/dataflows.png)

Die folgende Tabelle enthält weitere Informationen zum Ausführungsstatus von Datenflüssen:

| Status | Beschreibung |
| ------ | ----------- |
| Abgeschlossen | Der `Completed` gibt an, dass alle Datensätze für die entsprechende Datenflussausführung innerhalb des Zeitraums von einer Stunde verarbeitet wurden. Ein `Completed` kann weiterhin Fehler in Datenflussausführungen enthalten. |
| Erfolgreich | Der `Success` gibt an, dass alle Datensätze für die entsprechende Datenflussausführung innerhalb des Zeitraums von einer Stunde verarbeitet wurden und dass im Verlauf der Datenflussausführung keine Fehler aufgetreten sind. |
| Verarbeitung läuft | Der `Processing` zeigt an, dass ein Datenfluss noch nicht aktiv ist. Dieser Status tritt häufig unmittelbar nach der Erstellung eines neuen Datenflusses auf. |
| Fehler | Der `Error` zeigt an, dass der Aktivierungsprozess eines Datenflusses unterbrochen wurde. |
| Keine Durchläufe | Der `No runs` gibt an, dass der Datenfluss erstellt, aber keine Datenflussausführungen gestartet wurden. |

Auf [!UICONTROL  Seite „Datenflussaktivität] werden spezifische Informationen zu Ihrem Streaming-Datenfluss angezeigt. Das obere Banner enthält die kumulative Anzahl der aufgenommenen und fehlgeschlagenen Datensätze für alle Streaming-Datenflussausführungen in Ihrem ausgewählten Datumsbereich.

![dataflow-activity](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Standardmäßig enthalten die angezeigten Daten Aufnahmeraten der letzten sieben Tage. Wählen Sie **[!UICONTROL Letzte 7 Tage]**, um den Zeitrahmen der angezeigten Datensätze anzupassen.

Es wird ein Kalender-Popup-Fenster angezeigt, in dem Sie Optionen für alternative Erfassungszeitrahmen finden. Sie können den Zeitrahmen der Datenflussausführung konfigurieren, um die Flussausführungen der letzten sieben Tage oder der letzten 30 Tage anzuzeigen. Alternativ können Sie den interaktiven Kalender so konfigurieren, dass er einen benutzerdefinierten Zeitrahmen Ihrer Wahl festlegt. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![Kalender](../../images/tutorials/monitor-streaming/calendar.png)

Die untere Hälfte der Seite zeigt Informationen zur Anzahl der empfangenen, aufgenommenen und fehlgeschlagenen Datensätze pro Flussausführung an. Jeder Durchfluss wird innerhalb eines stündlichen Fensters aufgezeichnet.

![dataflow-run](../../images/tutorials/monitor-streaming/dataflow-run.png)

### Datenfluss-Ausführungsmetriken {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="Empfangene Einträge"
>abstract="Die Metrik „Empfangene Einträge“ gibt die Gesamtzahl der im Datenfluss empfangenen Einträge an."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="Aufgenommene Einträge"
>abstract="Die Metrik „Aufgenommene Einträge“ gibt die Gesamtzahl der in den Data Lake aufgenommenen Einträge an."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="Fehlgeschlagene Einträge"
>abstract="Die Metrik „Fehlgeschlagene Einträge“ gibt die Gesamtzahl der Einträge an, die aufgrund von Datenfehlern nicht in den Data Lake aufgenommen wurden."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="Einträge mit Warnhinweisen"
>abstract="Einträge mit Warnhinweisen geben die Gesamtzahl der aufgenommenen Einträge mit Warnhinweisen für die Mapper-Transformation an. Alle Fehler bei der Mapper-Transformation werden als Warnhinweise protokolliert und Zeilen, die teilweise aufgenommen wurden, werden als erfolgreich erachtet, jedoch mit einem Warnhinweis versehen"
>text="Learn more in documentation"

Jede einzelne Datenflussausführung zeigt die folgenden Details:

* **[!UICONTROL Start der Datenflussausführung]**: Die Zeit, zu der die Datenflussausführung gestartet wurde.
* **[!UICONTROL Verarbeitungszeit]**: Die Zeit, die für die Verarbeitung des Datenflusses benötigt wurde.
* **[!UICONTROL Empfangene Datensätze]**: Die Gesamtzahl der Datensätze, die im Datenfluss von einem Quell-Connector empfangen wurden.
* **[!UICONTROL Aufgenommene Datensätze]**: Die Gesamtzahl der in [!DNL Data Lake] aufgenommenen Datensätze.
* **[!UICONTROL Datensätze mit Warnungen]**: Die Gesamtzahl der aufgenommenen Datensätze mit Warnungen. Alle Mapper-Umwandlungsfehler werden als Warnungen gemeldet, und Zeilen, die teilweise aufgenommen werden, werden als `success` mit einer Warnung gekennzeichnet. **Hinweis**: Die Aufnahme von Datensätzen mit Warnungen wird nur von Streaming-Quellen unterstützt.
* **[!UICONTROL Fehlgeschlagene Datensätze]**: Die Anzahl der Datensätze, die aufgrund von Datenfehlern nicht in [!DNL Data Lake] aufgenommen wurden.
* **[!UICONTROL Aufnahmerate]**: Die Erfolgsrate der in [!DNL Data Lake] aufgenommenen Datensätze. Diese Metrik gilt, wenn [!UICONTROL Partielle Aufnahme] aktiviert ist.
* **[!UICONTROL Status]**: Gibt den Status des Datenflusses an: entweder [!UICONTROL Abgeschlossen] oder [!UICONTROL Verarbeitung]. [!UICONTROL Abgeschlossen] bedeutet, dass alle Datensätze für die entsprechende Datenflussausführung innerhalb des Zeitraums von einer Stunde verarbeitet wurden. [!UICONTROL Verarbeitung] bedeutet, dass die Ausführung des Datenflusses noch nicht abgeschlossen ist.

Die [!UICONTROL Übersicht über die Datenflussausführung] enthält zusätzliche Informationen zu Ihrem Datenfluss, z. B. die entsprechende Datenflussausführungs-ID, den Zieldatensatz und die Organisations-ID.

Eine Flussausführung mit Fehlern enthält auch das Bedienfeld [!UICONTROL Datenflussausführungsfehler], das den jeweiligen Fehler, der zum Fehlschlagen der Ausführung geführt hat, sowie die Gesamtzahl der fehlgeschlagenen Datensätze anzeigt.

![dataflow-run-overview](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Anzeigen von Datensätzen mit Warnungen {#warnings}

[!UICONTROL Datensätze mit Warnungen] zeigt eine Liste der Mapper-Umwandlungswarnungen an, die während der Flussausführung aufgetreten sind. Zeilen, die teilweise aufgenommen werden, werden als erfolgreich betrachtet und mit Warnungen versehen, wenn Fehler bei der Mapper-Transformation gefunden werden.

Standardmäßig werden alle Mapper-Umwandlungsfehler als Warnungen betrachtet, es sei denn, sie sind einer der folgenden:

* Syntaxfehler
* Verweise auf nicht vorhandene Attribute
* Nicht übereinstimmende XDM-Datentypen

Um die Fehlerdiagnose anzuzeigen, wählen Sie **[!UICONTROL Fehlerdiagnose in der Vorschau anzeigen]**.

![records-with-warning](../../images/tutorials/monitor-streaming/records-with-warnings.png)

Im Fenster [!UICONTROL Fehlerdiagnose-Vorschau] können Sie bis zu 100 Fehler und/oder Warnungen zu Ihrer Datenflussausführung in der Vorschau anzeigen. Von hier aus können Sie auch das Aufnahmefehlermanifest für weitere Informationen herunterladen, indem Sie die [!DNL Data Access]-API verwenden.

![Diagnose](../../images/tutorials/monitor-streaming/diagnostics.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] verwendet, um Ihre Streaming-Datenflüsse zu überwachen und die Fehler zu identifizieren, die zu fehlgeschlagenen Datenflüssen geführt haben. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Quellen – Übersicht](../../home.md)
* [Datenflüsse – Übersicht](../../../dataflows/home.md)
