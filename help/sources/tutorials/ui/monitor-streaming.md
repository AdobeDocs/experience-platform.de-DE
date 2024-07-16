---
keywords: Experience Platform; home; beliebte Themen; Konten überwachen; Datenflüsse überwachen; Datenflüsse
description: Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten planmäßig zu erfassen. In diesem Tutorial werden Schritte zum Überwachen von Streaming-Datenflüssen aus dem Arbeitsbereich "Quellen"beschrieben.
title: Überwachen von Datenflüssen für Streaming-Quellen in der Benutzeroberfläche
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 24%

---

# Überwachen von Datenflüssen für Streaming-Quellen in der Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Überwachen von Datenflüssen für Streaming-Quellen mithilfe des Arbeitsbereichs [!UICONTROL Quellen] beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Datenflüsse](../../../dataflows/home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   * [Datenfluss-Ausführungen](../../notifications.md): Datenfluss-Ausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration ausgewählter Datenflüsse basieren.
* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Überwachen von Datenflüssen für Streaming-Quellen

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Um vorhandene Datenflüsse für Streaming-Quellen anzuzeigen, wählen Sie **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile aus.

![Katalog](../../images/tutorials/monitor-streaming/catalog.png)

Die Seite [!UICONTROL Datenflüsse] enthält eine Liste aller in Ihrem Unternehmen vorhandenen Datenflüsse, einschließlich Informationen zu den Quelldaten, dem Kontonamen und dem Ausführungsstatus des Datenflusses.

Wählen Sie den Namen des Datenflusses aus, den Sie anzeigen möchten.

![dataflows](../../images/tutorials/monitor-streaming/dataflows.png)

Die folgende Tabelle enthält weitere Informationen zu den Ausführungsstatus von Datenflüssen:

| Status | Beschreibung |
| ------ | ----------- |
| Abgeschlossen | Der Status &quot;`Completed`&quot; gibt an, dass alle Datensätze für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde verarbeitet wurden. Der Status &quot;`Completed`&quot;kann in Datenfluss-Ausführungen weiterhin Fehler enthalten. |
| Erfolgreich | Der Status &quot;`Success`&quot; gibt an, dass alle Datensätze für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde verarbeitet wurden und dass im Verlauf des Datenflusses keine Fehler aufgetreten sind. |
| Verarbeitung läuft | Der Status &quot;`Processing`&quot;zeigt an, dass ein Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf. |
| Fehler | Der Status `Error` gibt an, dass der Aktivierungsprozess eines Datenflusses unterbrochen wurde. |
| Keine Durchläufe | Der Status &quot;`No runs`&quot; gibt an, dass der Datenfluss erstellt wurde, aber keine Datenflug-Ausführungen gestartet wurden. |

Auf der Seite [!UICONTROL Datenfluss-Aktivität] werden spezifische Informationen zu Ihrem Streaming-Datenfluss angezeigt. Das obere Banner enthält die kumulative Anzahl der erfassten Datensätze und der fehlgeschlagenen Datensätze für alle Streaming-Datenfluss-Ausführungen in Ihrem ausgewählten Datumsbereich.

![dataflow-activity](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Standardmäßig enthalten die angezeigten Daten die Aufnahmeraten der letzten sieben Tage. Wählen Sie **[!UICONTROL Letzte 7 Tage]** aus, um den Zeitrahmen der angezeigten Datensätze anzupassen.

Es wird ein Kalender-Popup-Fenster mit Optionen für alternative Erfassungszeitrahmen angezeigt. Sie können den Zeitrahmen für die Ausführung des Datenflusses so konfigurieren, dass die Flüsse der letzten sieben Tage oder der letzten 30 Tage angezeigt werden. Alternativ können Sie den interaktiven Kalender so konfigurieren, dass ein benutzerdefinierter Zeitrahmen Ihrer Wahl festgelegt wird. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![calendar](../../images/tutorials/monitor-streaming/calendar.png)

In der unteren Hälfte der Seite werden Informationen zur Anzahl der empfangenen, aufgenommenen und fehlgeschlagenen Datensätze pro Fluss angezeigt. Jeder Flusslauf wird in einem stündlichen Fenster aufgezeichnet.

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
>abstract="Einträge mit Warnhinweisen geben die Gesamtzahl der aufgenommenen Einträge mit Warnhinweisen für die Mapper-Transformation an. Alle Fehler bei der Mapper-Transformation werden als Warnhinweise protokolliert und Zeilen, die teilweise aufgenommen wurden, werden als erfolgreich erachtet, jedoch mit einem Warnhinweis versehen."
>text="Learn more in documentation"

Jeder einzelne Datenfluss zeigt die folgenden Details an:

* **[!UICONTROL Dataflow run start]**: Die Zeit, zu der der Datenfluss gestartet wurde.
* **[!UICONTROL Verarbeitungszeit]**: Die Zeit, die für die Verarbeitung des Datenflusses benötigt wurde.
* **[!UICONTROL Erhaltene Datensätze]**: Die Gesamtzahl der Datensätze, die im Datenfluss von einem Quell-Connector empfangen wurden.
* **[!UICONTROL Aufgenommene Datensätze]**: Die Gesamtzahl der in [!DNL Data Lake] erfassten Datensätze.
* **[!UICONTROL Datensätze mit Warnungen]**: Die Gesamtzahl der Datensätze mit erfassten Warnungen. Alle Mapper-Transformationsfehler werden als Warnungen gemeldet und Zeilen, die teilweise erfasst werden, werden mit einer Warnung als `success` gekennzeichnet. **Hinweis**: Die Unterstützung für die Aufnahme von Datensätzen mit Warnungen ist nur für Streaming-Quellen verfügbar.
* **[!UICONTROL Datensätze fehlgeschlagen]**: Die Anzahl der Datensätze, die aufgrund von Fehlern in den Daten nicht in [!DNL Data Lake] aufgenommen wurden.
* **[!UICONTROL Aufnahmerate]**: Die Erfolgsrate der in [!DNL Data Lake] erfassten Datensätze. Diese Metrik gilt, wenn [!UICONTROL Partielle Erfassung] aktiviert ist.
* **[!UICONTROL Status]**: Stellt den Status dar, in dem sich der Datenfluss befindet: entweder [!UICONTROL Abgeschlossen] oder [!UICONTROL Verarbeitung]. [!UICONTROL Abgeschlossen] bedeutet, dass alle Datensätze für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde verarbeitet wurden. [!UICONTROL Verarbeitung] bedeutet, dass die Ausführung des Datenflusses noch nicht abgeschlossen ist.

Die Seite mit der [!UICONTROL Übersicht über die Ausführung des Datenflusses] enthält zusätzliche Informationen zu Ihrem Datenfluss, z. B. die zugehörige ID für die Ausführung des Datenflusses, den Zieldatensatz und die Organisations-ID.

Ein Fluss mit Fehlern enthält auch das Bedienfeld [!UICONTROL Fehler bei Datenfluss-Ausführung] , in dem der bestimmte Fehler angezeigt wird, der zum Fehler bei der Ausführung geführt hat, sowie die Gesamtzahl der fehlgeschlagenen Datensätze.

![dataflow-run-overview](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Anzeigen von Datensätzen mit Warnhinweisen {#warnings}

[!UICONTROL Datensätze mit Warnungen] zeigt eine Liste der Mapper-Transformationswarnungen an, die während der Flussausführung aufgetreten sind. Zeilen, die teilweise erfasst werden, werden als erfolgreich betrachtet und mit Warnungen versehen, wenn Mapper-Transformationsfehler gefunden werden.

Standardmäßig werden alle Mapper-Transformationsfehler als Warnungen betrachtet, es sei denn, es handelt sich um einen der folgenden Fehler:

* Syntaxfehler
* Verweise auf nicht vorhandene Attribute
* Eine Abweichung von XDM-Datentypen

Um die Fehlerdiagnose anzuzeigen, wählen Sie **[!UICONTROL Vorschau der Fehlerdiagnose anzeigen]**.

![records-with-warning](../../images/tutorials/monitor-streaming/records-with-warnings.png)

Im Vorschaufenster für die [!UICONTROL Fehlerdiagnose] können Sie bis zu 100 Fehler und/oder Warnungen in Bezug auf Ihren Datenfluss in der Vorschau anzeigen. Von hier aus können Sie auch das Fehlermanifest für die Aufnahme herunterladen, um weitere Informationen mithilfe der [!DNL Data Access] -API zu erhalten.

![Diagnostics](../../images/tutorials/monitor-streaming/diagnostics.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] verwendet, um Ihre Streaming-Datenflüsse zu überwachen und die Fehler zu identifizieren, die zu fehlgeschlagenen Datenflüssen führten. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Quellen – Übersicht](../../home.md)
* [Datenflüsse – Übersicht](../../../dataflows/home.md)
