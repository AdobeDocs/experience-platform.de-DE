---
keywords: Experience Platform; Startseite; beliebte Themen; Konten überwachen; Datenflüsse überwachen; Datenflüsse
description: Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden Schritte zum Überwachen von Streaming-Datenflüssen aus dem Arbeitsbereich "Quellen"beschrieben.
solution: Experience Platform
title: Überwachen von Datenflüssen für Streaming-Quellen in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 12%

---

# Überwachen von Datenflüssen für Streaming-Quellen in der Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Überwachen von Datenflüssen für Streaming-Quellen mithilfe des Arbeitsbereichs [!UICONTROL Quellen] beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Datenflüsse](../../../dataflows/home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   * [Datenfluss wird ausgeführt](../../notifications.md): Datenfluss-Ausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration ausgewählter Datenflüsse basieren.
* [Quellen](../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Überwachen von Datenflüssen für Streaming-Quellen

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Um vorhandene Datenflüsse für Streaming-Quellen anzuzeigen, wählen Sie **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile aus.

![Katalog](../../images/tutorials/monitor-streaming/catalog.png)

Die Seite [!UICONTROL Datenflüsse] enthält eine Liste aller in Ihrem Unternehmen vorhandenen Datenflüsse, einschließlich Informationen zu ihren Quelldaten, Kontonamen und dem Ausführungsstatus des Datenflusses.

Wählen Sie den Namen des Datenflusses aus, den Sie anzeigen möchten.

![Datenflüsse](../../images/tutorials/monitor-streaming/dataflows.png)

Die folgende Tabelle enthält weitere Informationen zu den Ausführungsstatus von Datenflüssen:

| Status | Beschreibung |
| ------ | ----------- |
| Abgeschlossen | Der Status `Completed` gibt an, dass alle Datensätze für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde verarbeitet wurden. Der Status `Completed` kann bei Datenflüssen weiterhin Fehler enthalten. |
| Verarbeitung | Der Status `Processing` zeigt an, dass ein Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf. |
| Fehler | Der Status `Error` zeigt an, dass der Aktivierungsprozess eines Datenflusses unterbrochen wurde. |

Auf der Seite [!UICONTROL Dataflow Activity] werden spezifische Informationen zu Ihrem Streaming-Datenfluss angezeigt. Das obere Banner enthält die kumulative Anzahl der erfassten Datensätze und der fehlgeschlagenen Datensätze für alle Streaming-Datenfluss-Ausführungen in Ihrem ausgewählten Datumsbereich.

In der unteren Hälfte der Seite werden Informationen zur Anzahl der empfangenen, aufgenommenen und fehlgeschlagenen Datensätze pro Fluss angezeigt. Jeder Flusslauf wird in einem stündlichen Fenster aufgezeichnet.

![dataflow-activity](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Jeder einzelne Datenfluss zeigt die folgenden Details an:

* **[!UICONTROL Start]** des Datenflusses: Die Zeit, zu der der Datenfluss gestartet wurde.
* **[!UICONTROL Verarbeitungszeit]**: Die Zeitdauer, die die Verarbeitung des Datenflusses dauerte.
* **[!UICONTROL Erhaltene]** Datensätze: Die Gesamtzahl der Datensätze, die im Datenfluss von einem Quell-Connector empfangen wurden.
* **[!UICONTROL Aufgenommene]** Datensätze: Die Gesamtzahl der erfassten Datensätze in  [!DNL Data Lake].
* **[!UICONTROL Datensätze fehlgeschlagen]**: Die Anzahl der Datensätze, die  [!DNL Data Lake] aufgrund von Datenfehlern nicht in erfasst wurden.
* **[!UICONTROL Aufnahmerate]**: Die Erfolgsrate der erfassten Datensätze  [!DNL Data Lake]. Diese Metrik ist anwendbar, wenn [!UICONTROL Partielle Erfassung] aktiviert ist.
* **[!UICONTROL Status]**: Stellt den Status dar, in dem sich der Datenfluss befindet: entweder   Abgeschlossen oder  [!UICONTROL Verarbeitung].  Abgeschlossen bedeutet, dass alle Datensätze für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde verarbeitet wurden.  Verarbeitung bedeutet, dass der Datenfluss noch nicht abgeschlossen ist.

Standardmäßig enthalten die angezeigten Daten die Aufnahmeraten der letzten sieben Tage. Wählen Sie **[!UICONTROL Letzte 7 Tage]** aus, um den Zeitrahmen der angezeigten Datensätze anzupassen.

![change-time](../../images/tutorials/monitor-streaming/change-time.png)

Es wird ein Kalender-Popup-Fenster mit Optionen für alternative Erfassungszeitrahmen angezeigt. Wählen Sie **[!UICONTROL Letzte 30 Tage]** und dann **[!UICONTROL Anwenden]**.

![calendar](../../images/tutorials/monitor-streaming/calendar.png)

Um Details zu einem bestimmten Datenfluss-Lauf einschließlich dessen Fehlern anzuzeigen, wählen Sie die Startzeit der Ausführung aus der Liste aus.

![select-fail](../../images/tutorials/monitor-streaming/select-fail.png)

Die Seite [!UICONTROL Dataflow-Run-Übersicht] enthält zusätzliche Informationen zu Ihrem Datenfluss, z. B. die zugehörige Datenfluss-Ausführungskennung, den Zieldatensatz und die IMS-Organisations-ID.

Ein Fluss mit Fehlern enthält auch das Bedienfeld [!UICONTROL Fehler beim Ausführen des Datenflusses] , das den bestimmten Fehler anzeigt, der zum Fehler der Ausführung geführt hat, sowie die Gesamtzahl der fehlgeschlagenen Datensätze.

![Fehlgeschlagen](../../images/tutorials/monitor-streaming/failure.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Sources] verwendet, um Ihre Streaming-Datenflüsse zu überwachen und die Fehler zu identifizieren, die zu fehlgeschlagenen Datenflüssen führten. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Quellen – Übersicht](../../home.md)
* [Datenflüsse – Übersicht](../../../dataflows/home.md)
