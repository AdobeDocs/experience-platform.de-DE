---
title: Verwalten von Datensatzgültigkeiten
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform die Gültigkeit eines Datensatzes planen.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 5a12c75a54f420b2ca831dbfe05105dfd856dc4d
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 93%

---

# Verwalten von Datensatzgültigkeiten

>[!IMPORTANT]
>
>Die Datenhygiene-Funktionen in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Healthcare Shield erworben haben.

Der [[!UICONTROL Datenhygiene]-Arbeitsbereich](./overview.md) in der Adobe Experience Platform-Benutzeroberfläche bietet Ihnen die Möglichkeit, die Gültigkeit eines Datensatzes zu planen. Wenn ein Datensatz sein Ablaufdatum erreicht, beginnen der Data Lake, der Identity Service und das Echtzeit-Kundenprofil separate Prozesse, um den Inhalt des Datensatzes aus den entsprechenden Services zu entfernen. Sobald die Daten aus allen drei Services gelöscht wurden, wird der Ablauf als abgeschlossen markiert.

>[!WARNING]
>
>Wenn ein Datensatz abläuft, müssen Sie jeden Datenfluss, der Daten in diesen Datensatz erfasst, manuell ändern, damit Ihre nachgelagerten Workflows nicht negativ beeinflusst werden.

In diesem Dokument wird beschrieben, wie Sie Datensatzgültigkeiten in der Platform-Benutzeroberfläche planen und verwalten.

## Planen einer Datensatzgültigkeit

Um eine neue Anfrage zu erstellen, wählen Sie auf der Hauptseite im Arbeitsbereich die Option **[!UICONTROL Anfrage erstellen]** aus.

![Bild, das die ausgewählte Schaltfläche [!UICONTROL Anfrage erstellen] zeigt](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for dataset expiration scheduling-->

### Auswählen von Datum und Datensatz

Daraufhin öffnet sich das Dialogfeld für die Anfrageerstellung. Wählen Sie im Abschnitt **[!UICONTROL Aktion]** ein Datum aus, an dem der Datensatz gelöscht werden soll. Sie können das Datum manuell eingeben (im Format `mm/dd/yyyy`) oder das Kalendersymbol anklicken (![Bild des Kalendersymbols](../images/ui/ttl/calendar-icon.png)) und dann das Datum aus einem Dialogfeld auswählen.

![Bild, das zeigt, wie ein Ablaufdatum für das Dataset festgelegt wird](../images/ui/ttl/select-date.png)

Wählen Sie danach unter **[!UICONTROL Datensatzdetails]** das Datenbanksymbol (![Bild des Datenbanksymbols](../images/ui/ttl/database-icon.png)), um ein Dialogfeld zur Datensatzauswahl zu öffnen. Wählen Sie aus der Liste einen Datensatz aus, auf den die Gültigkeit angewendet werden soll, und klicken Sie danach auf **[!UICONTROL Fertig]**.

![Bild mit dem ausgewählten Datensatz](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Es werden nur Datensätze angezeigt, die zur aktuellen Sandbox gehören.

### Senden der Anfrage

Nachdem Sie einen Datensatz und ein Ablaufdatum ausgewählt haben, wählen Sie **[!UICONTROL Senden]**.

![Bild, das die ausgewählte Schaltfläche [!UICONTROL Senden] zeigt](../images/ui/ttl/submit.png)

Sie werden aufgefordert, das Datum zu bestätigen, an dem der Datensatz gelöscht werden soll. Wählen Sie **[!UICONTROL Senden]** aus, um fortzufahren.

Nachdem die Anfrage übermittelt wurde, wird ein Arbeitsauftrag erstellt und auf der Hauptregisterkarte des Arbeitsbereichs [!UICONTROL Datenhygiene] angezeigt. Hier können Sie den Fortschritt des Arbeitsauftrags überwachen.

## Bearbeiten oder Abbrechen einer Datensatzgültigkeit

Um eine Datensatzgültigkeit zu bearbeiten oder abzubrechen, wählen Sie auf der Hauptseite des Arbeitsbereichs **[!UICONTROL Datensatz]** und danach die jeweilige Datensatzgültigkeit aus der Liste aus.

Auf der Detailseite der Datensatzgültigkeit zeigt die rechte Leiste Steuerelemente zum Bearbeiten oder Abbrechen des geplanten Löschvorgangs an.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie in der Experience Platform-Benutzeroberfläche einen Zeitplan für Datensatzgültigkeiten erstellen können. Informationen zum Planen von Datensatzgültigkeiten mithilfe der Datenhygiene-API finden Sie im [Handbuch zum Datensatzgültigkeit-Endpunkt](../api/dataset-expiration.md).
