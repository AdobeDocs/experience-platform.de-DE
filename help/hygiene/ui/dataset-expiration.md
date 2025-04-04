---
title: Automatisierte Datensatzgültigkeiten
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform die Gültigkeit eines Datensatzes planen.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 49%

---

# Automatisierte Ablauffristen für Datensätze {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Löschen unerwünschter oder abgelaufener Kundendatensätze"
>abstract="<h2>Beschreibung</h2><p>Um den Lebenszyklus der Experience Platform-Daten unabhängig von der Einhaltung gesetzlicher Vorschriften zu verwalten, können Kundendatensätze gelöscht und Ablaufdaten für Datensätze geplant werden. Informationen zum Erstellen oder Verwalten von Anfragen betroffener Personen sind im Abschnitt über den Anwendungsfall „Berücksichtigen von Datenschutzanträgen betroffener Personen“ zu finden.</p>"

Der [[!UICONTROL Datenlebenszyklus]-Arbeitsbereich](./overview.md) in der Adobe Experience Platform-Benutzeroberfläche ermöglicht Ihnen, die Gültigkeitsdauer für Datensätze festzulegen. Wenn ein Datensatz sein Ablaufdatum erreicht, starten der Data Lake, der Identity Service und das Echtzeit-Kundenprofil separate Prozesse, um den Inhalt des Datensatzes aus den entsprechenden Services zu entfernen. Sobald die Daten aus allen drei Services gelöscht wurden, wird der Ablauf als abgeschlossen markiert.

>[!WARNING]
>
>Wenn ein Datensatz ausläuft, müssen alle Datenflüsse, die Daten in diesen Datensatz einspeisen, manuell geändert werden, damit Ihre nachgeschalteten Workflows nicht beeinträchtigt werden.

In diesem Dokument wird beschrieben, wie Sie Datensatzgültigkeiten in der Experience Platform-Benutzeroberfläche planen und automatisieren können.

>[!NOTE]
>
>Die Datensatzgültigkeit löscht derzeit keine Daten aus der Adobe Experience Platform Edge Network. Es ist jedoch nicht möglich, dass Daten nach Ablauf des Datensatzes innerhalb der Edge Network bleiben. Dies liegt daran, dass sich die 15-tägige Service-Lizenzvereinbarung für die Datensatzgültigkeit mit dem 14-tägigen Zeitraum überschneidet, in dem Daten innerhalb von Edge Network vorhanden sind, bevor sie verworfen werden.

Advanced Data Lifecycle Management unterstützt das Löschen von Datensätzen über den [Datensatzgültigkeits-Endpunkt](../api/dataset-expiration.md) und ID-Löschungen (Daten auf Zeilenebene) mithilfe primärer Identitäten über den [Arbeitsauftrags-Endpunkt](../api/workorder.md). Sie können auch Datensatzgültigkeiten und [Löschungen von Datensätzen](./record-delete.md) über die Experience Platform-Benutzeroberfläche verwalten. Weitere Informationen finden Sie in der verknüpften Dokumentation .

>[!NOTE]
>
>Der Datenlebenszyklus unterstützt keine Batch-Löschung.

## Planen einer Datensatzgültigkeit {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Anweisungen"
>abstract="<ul><li>Wählen Sie im linken Navigationsbereich <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=de">Datenlebenszyklus</a> und anschließend die Option <b>Anfrage erstellen</b> aus.</li><li>Wenn Sie Datensätze löschen möchten:</li>   <li>Wählen Sie <b>Datensatz</b> aus.</li>   <li>Wählen Sie einen bestimmten Datensatz aus, aus dem Datensätze gelöscht werden sollen, oder wählen Sie die Option aus, sie aus allen Datensätzen zu löschen.</li>   <li>Geben Sie die Identitäten der Personen an, deren Datensätze gelöscht werden sollen. Wählen Sie <b>Identität hinzufügen</b> aus, um die Identitäten einzeln anzugeben, oder wählen Sie <b>Dateien auswählen</b> aus, um stattdessen eine JSON-Datei mit Identitäten hochzuladen.</li>   <li>Wählen Sie bei Bedarf <b>Vorlage</b> aus, um das erwartete Format der JSON-Datei anzuzeigen.</li><li>Anweisungen zum <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=de#schedule-dataset-expiration">Planen von Ablaufdaten für Datensätze</a> finden Sie in der Dokumentation.</li></ul>"

Um eine Anfrage zu erstellen, wählen **[!UICONTROL auf der Hauptseite]** Arbeitsbereich die Option „Anfrage erstellen“ aus.

>[!IMPORTANT]
>
>Für Real-Time CDP-, Adobe Journey Optimizer- und Customer Journey Analytics-Benutzer stehen 20 Arbeitsaufträge zur Gültigkeit von Datensätzen aus. Benutzende von Healthcare Shield und Privacy and Security Shield haben 50 geplante Arbeitsaufträge zur Gültigkeit von Datensätzen. Das bedeutet, dass Sie 20 oder 50 Datensätze gleichzeitig löschen können.<br>Wenn Sie beispielsweise 20 geplante Datensatzgültigkeiten haben und ein Datensatz morgen gelöscht werden soll, können Sie keine weiteren Gültigkeiten festlegen, bis dieser Datensatz gelöscht wurde.

![Der Arbeitsbereich [!UICONTROL Datenlebenszyklus] mit [!UICONTROL  hervorgehobenen ]Anfrage erstellen“](../images/ui/ttl/create-request-button.png)

Der Workflow zur Anfrageerstellung wird angezeigt. Wählen Sie im Abschnitt [!UICONTROL Angeforderte Aktion] die Option **[!UICONTROL Datensatz löschen]** aus, um die Steuerelemente für die Planung der Datensatzgültigkeit zu aktualisieren.

![Der Workflow zur Anfrageerstellung mit der hervorgehobenen [!UICONTROL Datensatz löschen] Option.](../images/ui/ttl/dataset-selected.png)

### Auswählen von Datum und Datensatz {#select-date-and-dataset}

Wählen Sie im Abschnitt **[!UICONTROL Angeforderte Aktion]** ein Datum aus, an dem der Datensatz gelöscht werden soll. Sie können das Datum manuell eingeben (im Format `mm/dd/yyyy`) oder das Kalendersymbol auswählen (![ Kalendersymbol).](/help/images/icons/calendar.png)), um das Datum aus einem Dialogfeld auszuwählen.

![Ein Kalenderdialogfeld mit ausgewähltem Ablaufdatum, das für den Datensatz hervorgehoben ist.](../images/ui/ttl/select-date.png)

Wählen Sie anschließend unter **[!UICONTROL Datensatzdetails]** das Datenbanksymbol (![Datenbanksymbol).](/help/images/icons/database.png)), um ein Dialogfeld zur Datensatzauswahl zu öffnen. Wählen Sie aus der Liste einen Datensatz aus, auf den die Gültigkeit angewendet werden soll, und klicken Sie danach auf **[!UICONTROL Fertig]**.

![Das Dialogfeld [!UICONTROL Datensatz auswählen] mit einem ausgewählten Datensatz und [!UICONTROL Fertig] hervorgehoben.](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Es werden nur Datensätze angezeigt, die zur aktuellen Sandbox gehören.

### Senden der Anfrage {#submit-request}

Der Abschnitt [!UICONTROL Datensatzdetails] wird ausgefüllt und enthält die primäre Identität und das Schema für den ausgewählten Datensatz. Geben Sie unter **[!UICONTROL Anfrageeinstellungen]** einen Namen und eine optionale Beschreibung für die Anfrage ein und wählen Sie dann **[!UICONTROL Senden]**.

![Eine abgeschlossene Datensatz-Gültigkeitsanfrage mit der hervorgehobenen Schaltfläche [!UICONTROL Anfrageeinstellungen] und [!UICONTROL Senden].](../images/ui/ttl/submit.png)

Ein [!UICONTROL Anfrage bestätigen]Dialogfeld wird angezeigt. Sie werden aufgefordert, den Datensatznamen und das Datum zu bestätigen, an dem der Datensatz gelöscht werden soll. Wählen Sie **[!UICONTROL Senden]** aus, um fortzufahren.

Nachdem die Anfrage gesendet wurde, wird ein Arbeitsauftrag erstellt und auf der Hauptregisterkarte des Arbeitsbereichs [!UICONTROL Datenlebenszyklus] angezeigt. Hier können Sie den Fortschritt des Arbeitsauftrags überwachen.

>[!NOTE]
>
>Der Abschnitt mit der Übersicht über [Timelines und Transparenz](../home.md#dataset-expiration-transparency) enthält Details dazu, wie die Gültigkeit von Datensätzen verarbeitet wird, nachdem sie abgelaufen ist.

## Bearbeiten oder Abbrechen einer Datensatzgültigkeit {#edit-or-cancel}

Um eine Datensatzgültigkeit zu bearbeiten oder abzubrechen, wählen Sie auf der Hauptseite des Arbeitsbereichs **[!UICONTROL Datensatz]** und danach die jeweilige Datensatzgültigkeit aus der Liste aus.

Auf der Detailseite der Datensatzgültigkeit zeigt die rechte Leiste Steuerelemente zum Bearbeiten oder Abbrechen des geplanten Löschvorgangs an.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie in der Experience Platform-Benutzeroberfläche einen Zeitplan für Datensatzgültigkeiten erstellen können. Weitere Informationen zur Durchführung anderer Datenminimierungsaufgaben in der Benutzeroberfläche finden Sie im Abschnitt [Übersicht über die Datenlebenszyklus-Benutzeroberfläche](./overview.md).

Informationen zum Planen von Datensatzgültigkeiten mithilfe der Datenhygiene-API finden Sie im [Handbuch zum Datensatzgültigkeits-Endpunkt](../api/dataset-expiration.md).
