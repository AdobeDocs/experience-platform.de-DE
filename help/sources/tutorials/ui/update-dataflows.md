---
keywords: Experience Platform;Startseite;beliebte Themen;Aktualisieren von Datenblättern;Zeitplan bearbeiten
description: In diesem Lernprogramm werden die Schritte zum Aktualisieren eines Datenflusszeitplans beschrieben, einschließlich der Erfassungsfrequenz und der Intervallrate, die mithilfe des Sources-Arbeitsbereichs vorgenommen werden.
solution: Experience Platform
title: Planen des Verbindungsdatafloms in der Benutzeroberfläche aktualisieren
topic: Übersicht
type: Tutorial
translation-type: tm+mt
source-git-commit: 31e4b15ad71a0d17278fbdb4d88ff42029cbe655
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 10%

---


# Aktualisieren von Datenflüssen in der Benutzeroberfläche

In diesem Lernprogramm werden die Schritte zum Aktualisieren eines Datenflusszeitplans beschrieben, einschließlich der Erfassungsfrequenz und der Intervallrate, wobei der Arbeitsbereich [!UICONTROL Quellen] verwendet wird.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
- [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Zeitplan bearbeiten

Wählen Sie in der Plattform-Benutzeroberfläche **[!UICONTROL Quellen]** aus der linken Navigation, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Wählen Sie **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile aus, um eine Liste der vorhandenen Datenflüsse Ansicht.

![Katalog](../../images/tutorials/update-dataflows/catalog.png)

Die Seite [!UICONTROL Datenflüsse] enthält eine Liste aller vorhandenen Datenflüsse, einschließlich Informationen zum Ausführungsstatus, zum Datum der letzten Ausführung und zum Kontonamen.

Wählen Sie oben links das Filtersymbol ![filter](../../images/tutorials/update/filter.png) aus, um das Sortierfeld zu starten.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Das Sortierungsbedienfeld bietet eine Liste aller verfügbaren Quellen. Sie können mehr als eine Quelle aus der Liste auswählen, um auf eine gefilterte Auswahl von Datenflüssen aus verschiedenen Quellen zuzugreifen.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Datenflüsse anzuzeigen. Nachdem Sie den Datendurchlauf identifiziert haben, den Sie neu planen möchten, wählen Sie die Auslassungspunkte (`...`) neben dem Kontonamen aus.

![umplanen](../../images/tutorials/update-dataflows/reschedule.png)

Es wird ein Dropdown-Menü angezeigt, in dem Sie die Optionen **[!UICONTROL Plan bearbeiten]**, **[!UICONTROL Datenpfad deaktivieren]**, **[!UICONTROL Ansicht bei der Überwachung]** und **[!UICONTROL Löschen]** haben. Wählen Sie **[!UICONTROL Plan bearbeiten]** aus dem Menü.

![edit-schedule](../../images/tutorials/update-dataflows/edit-schedule.png)

Das Dialogfeld **[!UICONTROL Plan bearbeiten]** enthält Optionen zum Aktualisieren der Erfassungsfrequenz und Intervallrate Ihres Datenflusses. Nachdem Sie die aktualisierten Werte für Häufigkeit und Intervall festgelegt haben, wählen Sie **[!UICONTROL Speichern]**.

>[!NOTE]
>
>Sie können einen Datenflug, der für eine einmalige Erfassung geplant war, nicht neu planen.

![schedule-dialog-box](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| Zeitplan | Beschreibung |
| ---------- | ----------- |
| Häufigkeit | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Folgende Werte sind für die Bearbeitung des Zeitplans für einen bereits vorhandenen Datenaflow zulässig: `minute`, `hour`, `day` oder `week`. |
| Intervall | Das Intervall gibt den Zeitraum zwischen zwei aufeinander folgenden Flussläufen an. Der Wert des Intervalls sollte eine Ganzzahl von nicht null sein und größer als oder gleich `15` sein. |

Nach einigen Augenblicken wird unten im Bildschirm ein Bestätigungsfeld angezeigt, um eine erfolgreiche Aktualisierung zu bestätigen.

![schedule-verify](../../images/tutorials/update-dataflows/schedule-confirm.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie den Arbeitsbereich [!UICONTROL Quellen] erfolgreich verwendet, um den Erfassungszeitplan eines Datenflusses zu aktualisieren.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mit der API [!DNL Flow Service] finden Sie im Lehrgang zu [Aktualisieren von Datenflüssen mit der Flow Service API](../../tutorials/api/update-dataflows.md).