---
keywords: Experience Platform;Startseite;beliebte Themen;Aktualisieren von Datenblättern;Zeitplan bearbeiten
description: In diesem Lernprogramm werden die Schritte zum Aktualisieren eines Datenflusszeitplans beschrieben, einschließlich der Erfassungsfrequenz und der Intervallrate, die mithilfe des Sources-Arbeitsbereichs vorgenommen werden.
solution: Experience Platform
title: Aktualisieren eines Quellverbindungsdatafloms in der Benutzeroberfläche
topic: Übersicht
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
translation-type: tm+mt
source-git-commit: 3a36996b43760bc9161b8d4750a1121e9ada8d30
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 7%

---

# Aktualisieren von Datenflüssen in der Benutzeroberfläche

In diesem Lernprogramm erfahren Sie, wie Sie einen Datenpfad für vorhandene Quellen aktualisieren, einschließlich Informationen zum Bearbeiten eines Datenflussplans und der Zuordnung mithilfe des Arbeitsbereichs [!UICONTROL Quellen].

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
- [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Zuordnung bearbeiten

>[!NOTE]
>
>Die Funktion zum Bearbeiten von Zuordnungen wird derzeit nicht für die folgenden Quellen unterstützt: Adobe Analytics, Adobe Audience Manager, HTTP API und [!DNL Marketo Engage].

Wählen Sie in der Plattform-Benutzeroberfläche **[!UICONTROL Quellen]** aus der linken Navigation, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Wählen Sie **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile aus, um eine Liste der vorhandenen Datenflüsse Ansicht.

![Katalog](../../images/tutorials/update-dataflows/catalog.png)

Die Seite [!UICONTROL Datenflüsse] enthält eine Liste aller vorhandenen Datenflüsse, einschließlich Informationen zum Ausführungsstatus, zum Datum der letzten Ausführung und zum Kontonamen.

Wählen Sie oben links das Filtersymbol ![filter](../../images/tutorials/update/filter.png) aus, um das Sortierfeld zu starten.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Das Sortierungsbedienfeld bietet eine Liste aller verfügbaren Quellen. Sie können mehr als eine Quelle aus der Liste auswählen, um auf eine gefilterte Auswahl von Datenflüssen aus verschiedenen Quellen zuzugreifen.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Datenflüsse anzuzeigen. Nachdem Sie den zu aktualisierenden Datendurchlauf identifiziert haben, wählen Sie die Auslassungspunkte (`...`) neben dem Kontonamen aus.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Es wird ein Dropdown-Menü mit Optionen zum Aktualisieren des ausgewählten Datenflusses angezeigt. Von hier aus können Sie die Zuordnungssätze und den Erfassungszeitplan eines Datenflusses aktualisieren. Sie können auch Optionen zum Prüfen des Datenflusses im Überwachungs-Dashboard sowie zum Deaktivieren oder Löschen des Datenflusses auswählen.

Wählen Sie **[!UICONTROL Quelle bearbeiten]**, um die Zuordnung zu aktualisieren.

![edit-dataflow](../../images/tutorials/update-dataflows/edit-dataflow.png)

Der Schritt [!UICONTROL Daten hinzufügen] wird angezeigt. Wählen Sie das geeignete Datenformat, um den Inhalt der ausgewählten Daten zu überprüfen, und wählen Sie dann **[!UICONTROL Weiter]**, um fortzufahren.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

Die Seite [!UICONTROL Zuordnung] bietet eine Schnittstelle, über die Sie Zuordnungssätze hinzufügen und entfernen können, die mit Ihrem Datensatz verknüpft sind.

>[!TIP]
>
>Zuordnungsaktualisierungen werden nur auf in der Zukunft geplante Datenflussabläufe angewendet.

Wählen Sie **[!UICONTROL Hinzufügen neue Zuordnung]**, um einen neuen Zuordnungssatz hinzuzufügen.

![add-new-mapping](../../images/tutorials/update-dataflows/add-new-mapping.png)

Geben Sie als Nächstes das entsprechende Quell-Feld-Attribut und die Zielgruppe-XDM-Feldwerte ein, um Ihren zusätzlichen Zuordnungssatz abzuschließen. Wählen Sie **[!UICONTROL Weiter]**, um fortzufahren.

![new-mapping-added](../../images/tutorials/update-dataflows/new-mapping-added.png)

Der Schritt [!UICONTROL Einplanen] wird angezeigt, mit dem Sie den Erfassungszeitplan Ihres Datenflusses aktualisieren und die ausgewählten Quelldaten automatisch mit den aktualisierten Zuordnungen erfassen können.

>[!NOTE]
>
>Sie können keine Zuordnungssätze für Datenflüsse aktualisieren, die für die einmalige Erfassung geplant waren und die Beginn in der Vergangenheit liegen.

![scheduling](../../images/tutorials/update-dataflows/scheduling.png)

Auf der Seite [!UICONTROL Datenfelddetails] können Sie einen aktualisierten Namen und eine Beschreibung für Ihren Datenaflow angeben und den Fehlerschwellenwert Ihres Datenflusses neu konfigurieren.

Nachdem Sie die aktualisierten Werte angegeben haben, wählen Sie **[!UICONTROL Weiter]**.

![dataflow-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie Ihren Datenbogen überprüfen können, bevor er aktualisiert wird.

Nachdem Sie den Datenfluss überprüft haben, wählen Sie **[!UICONTROL Fertig stellen]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses mit den neuen Zuordnungssätzen zu.

![überprüfen](../../images/tutorials/update-dataflows/review.png)

## Zeitplan bearbeiten

Um den Erfassungszeitplan eines vorhandenen Datenflusses zu bearbeiten, wählen Sie die Auslassungspunkte (`...`) neben dem Namen des Datenflusses und dann **[!UICONTROL Plan bearbeiten]** aus dem Dropdown-Menü.

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

In diesem Lernprogramm haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] verwendet, um den Erfassungszeitplan und die Zuordnungssätze Ihres Datenflusses zu aktualisieren.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mit der API [!DNL Flow Service] finden Sie im Lehrgang zu [Aktualisieren von Datenflüssen mit der Flow Service API](../../tutorials/api/update-dataflows.md).
