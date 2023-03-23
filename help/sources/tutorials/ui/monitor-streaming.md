---
keywords: Experience Platform; Startseite; beliebte Themen; Konten überwachen; Datenflüsse überwachen; Datenflüsse
description: Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden Schritte zum Überwachen von Streaming-Datenflüssen aus dem Arbeitsbereich "Quellen"beschrieben.
title: Überwachen von Datenflüssen für Streaming-Quellen in der Benutzeroberfläche
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 14%

---

# Überwachen von Datenflüssen für Streaming-Quellen in der Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Überwachen von Datenflüssen für Streaming-Quellen mithilfe des [!UICONTROL Quellen] Arbeitsbereich.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Datenflüsse](../../../dataflows/home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   * [Datenfluss-Abläufe](../../notifications.md): Datenfluss-Ausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration ausgewählter Datenflüsse basieren.
* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Überwachen von Datenflüssen für Streaming-Quellen

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Um vorhandene Datenflüsse für Streaming-Quellen anzuzeigen, wählen Sie **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile.

![Katalog](../../images/tutorials/monitor-streaming/catalog.png)

Die [!UICONTROL Datenflüsse] -Seite enthält eine Liste aller in Ihrem Unternehmen vorhandenen Datenflüsse, einschließlich Informationen zu ihren Quelldaten, Kontonamen und dem Ausführungsstatus des Datenflusses.

Wählen Sie den Namen des Datenflusses aus, den Sie anzeigen möchten.

![Datenflüsse](../../images/tutorials/monitor-streaming/dataflows.png)

Die folgende Tabelle enthält weitere Informationen zu den Ausführungsstatus von Datenflüssen:

| Status | Beschreibung |
| ------ | ----------- |
| Abgeschlossen | Die `Completed` Der Status gibt an, dass alle Datensätze für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde verarbeitet wurden. A `Completed` -Status kann in Datenflug-Ausführungen weiterhin Fehler enthalten. |
| Erfolgreich | Die `Success` Der Status gibt an, dass alle Datensätze für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde verarbeitet wurden und dass im Verlauf des Datenflusses keine Fehler aufgetreten sind. |
| In Bearbeitung | Die `Processing` Status gibt an, dass ein Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf. |
| Fehler | Die `Error` Status gibt an, dass der Aktivierungsprozess eines Datenflusses unterbrochen wurde. |
| Keine Ausführungen | Die `No runs` Der Status gibt an, dass der Datenfluss erstellt wurde, aber keine Datenfluss-Ausführungen gestartet wurden. |

Die [!UICONTROL Datenflussaktivität] Seite zeigt spezifische Informationen zu Ihrem Streaming-Datenfluss an. Das obere Banner enthält die kumulative Anzahl der erfassten Datensätze und der fehlgeschlagenen Datensätze für alle Streaming-Datenfluss-Ausführungen in Ihrem ausgewählten Datumsbereich.

![dataflow-activity](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Standardmäßig enthalten die angezeigten Daten die Aufnahmeraten der letzten sieben Tage. Auswählen **[!UICONTROL Letzte 7 Tage]** , um den Zeitrahmen der angezeigten Datensätze anzupassen.

Es wird ein Kalender-Popup-Fenster mit Optionen für alternative Erfassungszeitrahmen angezeigt. Sie können den Zeitrahmen für die Ausführung des Datenflusses so konfigurieren, dass die Flüsse der letzten sieben Tage oder der letzten 30 Tage angezeigt werden. Alternativ können Sie den interaktiven Kalender so konfigurieren, dass ein benutzerdefinierter Zeitrahmen Ihrer Wahl festgelegt wird. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![calendar](../../images/tutorials/monitor-streaming/calendar.png)

In der unteren Hälfte der Seite werden Informationen zur Anzahl der empfangenen, aufgenommenen und fehlgeschlagenen Datensätze pro Fluss angezeigt. Jeder Flusslauf wird in einem stündlichen Fenster aufgezeichnet.

![dataflow-run](../../images/tutorials/monitor-streaming/dataflow-run.png)

### Datenfluss-Ausführungsmetriken {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="Erhaltene Aufzeichnungen"
>abstract="Die Metrik &quot;Erhaltene Datensätze&quot;gibt die Gesamtzahl der im Datenfluss empfangenen Datensätze an."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="Aufgenommene Datensätze"
>abstract="Die Metrik Aufgenommene Datensätze gibt die Gesamtzahl der in den Data Lake erfassten Datensätze an."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="Fehlgeschlagene Datensätze"
>abstract="Die Metrik &quot;Datensätze fehlgeschlagen&quot;gibt die Gesamtzahl der Datensätze an, die aufgrund von Fehlern in den Daten nicht in den Daten-Pool aufgenommen wurden."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="Datensätze mit Warnungen"
>abstract="Datensätze mit Warnungen geben die Gesamtzahl der Datensätze an, die mit Mapper-Transformationswarnungen erfasst wurden. Alle Mapper-Transformationsfehler werden als Warnungen und teilweise aufgenommene Zeilen mit einer Warnung als erfolgreich gemeldet"
>text="Learn more in documentation"

Jeder einzelne Datenfluss zeigt die folgenden Details an:

* **[!UICONTROL Start des Datenflusses]**: Die Zeit, zu der der Datenfluss gestartet wurde.
* **[!UICONTROL Verarbeitungszeit]**: Die Zeitdauer, die die Verarbeitung des Datenflusses dauerte.
* **[!UICONTROL Erhaltene Datensätze]**: Die Gesamtzahl der Datensätze, die im Datenfluss von einem Quell-Connector empfangen wurden.
* **[!UICONTROL Aufgenommene Datensätze]**: Die Gesamtzahl der erfassten Datensätze in [!DNL Data Lake].
* **[!UICONTROL Datensätze mit Warnungen]**: Die Gesamtzahl der Datensätze mit Warnungen, die erfasst wurden. Alle Mapper-Transformationsfehler werden als Warnungen gemeldet und Zeilen, die teilweise erfasst werden, werden als `success` mit einer Warnung. **Hinweis**: Die Aufnahme von Datensätzen mit Warnungen wird nur für Streaming-Quellen unterstützt.
* **[!UICONTROL Datensätze fehlgeschlagen]**: Die Anzahl der Datensätze, die nicht erfasst wurden [!DNL Data Lake] aufgrund von Fehlern in den Daten.
* **[!UICONTROL Aufnahmerate]**: Die Erfolgsrate der Datensätze, die in [!DNL Data Lake]. Diese Metrik ist anwendbar, wenn [!UICONTROL Teilaufnahme] aktiviert ist.
* **[!UICONTROL Status]**: Stellt den Status dar, in dem sich der Datenfluss befindet: entweder [!UICONTROL Abgeschlossen] oder [!UICONTROL Verarbeitung]. [!UICONTROL Abgeschlossen] bedeutet, dass alle Datensätze für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde verarbeitet wurden. [!UICONTROL Verarbeitung] bedeutet, dass die Ausführung des Datenflusses noch nicht abgeschlossen ist.

Die [!UICONTROL Übersicht über Datenfluss] -Seite enthält zusätzliche Informationen zu Ihrem Datenfluss, z. B. die zugehörige Datenfluss-Ausführungskennung, den Zieldatensatz und die Organisations-ID.

Ein Fluss mit Fehlern enthält auch die [!UICONTROL Fehler bei Datenfluss-Ausführung] -Bedienfeld, das den bestimmten Fehler anzeigt, der zum Fehlschlagen der Ausführung geführt hat, sowie die Gesamtzahl der fehlgeschlagenen Datensätze.

![dataflow-run-overview](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Anzeigen von Datensätzen mit Warnhinweisen {#warnings}

[!UICONTROL Datensätze mit Warnungen] zeigt eine Liste der Mapper-Transformationswarnungen an, die während der Ausführung des Workflows aufgetreten sind. Zeilen, die teilweise erfasst werden, werden als erfolgreich betrachtet und mit Warnungen versehen, wenn Mapper-Transformationsfehler gefunden werden.

Standardmäßig werden alle Mapper-Transformationsfehler als Warnungen betrachtet, es sei denn, es handelt sich um einen der folgenden Fehler:

* Syntaxfehler
* Verweise auf nicht vorhandene Attribute
* Eine Nichtübereinstimmung von XDM-Datentypen

Um die Fehlerdiagnose anzuzeigen, wählen Sie **[!UICONTROL Vorschau der Fehlerdiagnose]**.

![records-with-warning](../../images/tutorials/monitor-streaming/records-with-warnings.png)

Die [!UICONTROL Fehlerdiagnose - Vorschau] -Fenster können Sie eine Vorschau von bis zu 100 Fehlern und/oder Warnungen bezüglich Ihres Datenflusses anzeigen. Von hier können Sie auch das Fehlermanifest für die Aufnahme herunterladen, um weitere Informationen zu erhalten, indem Sie die [!DNL Data Access] API.

![Diagnose](../../images/tutorials/monitor-streaming/diagnostics.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die [!UICONTROL Quellen] Arbeitsbereich zum Überwachen Ihrer Streaming-Datenflüsse und Identifizieren der Fehler, die zu fehlgeschlagenen Datenflüssen führten. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Quellen – Übersicht](../../home.md)
* [Datenflüsse – Übersicht](../../../dataflows/home.md)
