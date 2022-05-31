---
title: Datensatz-TTLs verwalten
description: Erfahren Sie, wie Sie in der Adobe Experience Platform-Benutzeroberfläche eine Live-Zeit (TTL) für einen Datensatz planen.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 22da9e39e168d9a995c7c134733aa7a1b3587749
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Datensatz-TTLs verwalten

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Adobe Shield für das Gesundheitswesen erworben haben.

Die [[!UICONTROL Datenhygiene] Arbeitsbereich](./overview.md) In der Adobe Experience Platform-Benutzeroberfläche können Sie eine Time to Live (TTL) für einen Datensatz planen.

In diesem Dokument wird beschrieben, wie Sie Datensatz-TTLs in der Platform-Benutzeroberfläche planen und verwalten.

## TTL planen

Um eine neue Anforderung zu erstellen, wählen Sie **[!UICONTROL Anforderung erstellen]** von der Hauptseite im Arbeitsbereich aus.

![Bild, das die [!UICONTROL Anforderung erstellen] Schaltfläche ausgewählt](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for TTL scheduling-->

### Datum und Datensatz auswählen

Das Dialogfeld für die Anforderungserstellung wird angezeigt. Unter dem **[!UICONTROL Aktion]** ein Datum auswählen, ab dem der Datensatz gelöscht werden soll. Sie können das Datum manuell eingeben (im Format `mm/dd/yyyy`) oder wählen Sie das Kalendersymbol (![Bild des Kalendersymbols](../images/ui/ttl/calendar-icon.png)), um das Datum aus einem Dialogfeld auszuwählen.

![Bild mit einem Ablaufdatum, das für die TTL festgelegt wird](../images/ui/ttl/select-date.png)

Weiter, unter **[!UICONTROL Datensatzdetails]** Wählen Sie das Datenbanksymbol (![Bild des Datenbanksymbols](../images/ui/ttl/database-icon.png)), um ein Dialogfeld zur Datensatzauswahl zu öffnen. Wählen Sie einen Datensatz aus der Liste aus, auf den die TTL angewendet werden soll, und wählen Sie dann **[!UICONTROL Fertig]**.

![Bild mit dem ausgewählten Datensatz](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Es werden nur Datensätze angezeigt, die zur aktuellen Sandbox gehören.

### Anfrage senden

Nachdem Sie einen Datensatz und ein TTL-Datum ausgewählt haben, wählen Sie **[!UICONTROL Einsenden]**.

![Bild, das die [!UICONTROL Einsenden] Schaltfläche ausgewählt](../images/ui/ttl/submit.png)

Sie werden aufgefordert, das Datum zu bestätigen, ab dem der Datensatz gelöscht wird. Auswählen **[!UICONTROL Einsenden]** , um fortzufahren.

Nachdem die Anfrage gesendet wurde, wird eine Arbeitsreihenfolge erstellt und auf der Registerkarte &quot;Haupt&quot;im [!UICONTROL Datenhygiene] Arbeitsbereich. Von hier aus können Sie den Status der Arbeitsreihenfolge bei der Verarbeitung der Anforderung überwachen.

## TTL bearbeiten oder abbrechen

Um eine TTL zu bearbeiten oder abzubrechen, wählen Sie **[!UICONTROL Datensatz]** auf der Hauptseite des Arbeitsbereichs und wählen Sie die TTL aus der Liste aus.

Auf der Detailseite der TTL zeigt die rechte Leiste Steuerelemente zum Bearbeiten oder Abbrechen des geplanten Löschvorgangs an.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie Datensatz-TTLs in der Experience Platform-Benutzeroberfläche planen. Informationen zum Planen von Datensatz-TTLs mithilfe der Data Hygiene API finden Sie im Abschnitt [Endpunktleitfaden für Datensatz-TTL](../api/ttl.md).
