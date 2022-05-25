---
title: Datensatz-TTLs verwalten
description: Erfahren Sie, wie Sie in der Adobe Experience Platform-Benutzeroberfläche eine Live-Zeit (TTL) für einen Datensatz planen.
source-git-commit: 931b847761e649696aa8433d53233593efd4d1ee
workflow-type: tm+mt
source-wordcount: '412'
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

Das Dialogfeld für die Anforderungserstellung wird angezeigt. Unter dem **[!UICONTROL Aktion]** Bereich, wählen Sie **[!UICONTROL Datensatz]** , um die verfügbaren Steuerelemente für die TTL-Planung zu aktualisieren.

![Bild, das die [!UICONTROL Datensatz] Auswahl](../images/ui/ttl/create-request-button.png)

### Datum und Datensatz auswählen

Unter dem **[!UICONTROL Aktion]** ein Datum auswählen, ab dem der Datensatz gelöscht werden soll. Sie können das Datum manuell eingeben (im Format `mm/dd/yyyy`) oder wählen Sie das Kalendersymbol (![Bild des Kalendersymbols](../images/ui/ttl/calendar-icon.png)), um das Datum aus einem Dialogfeld auszuwählen.

![Bild mit einem Ablaufdatum, das für die TTL festgelegt wird](../images/ui/ttl/select-date.png)

Weiter, unter **[!UICONTROL Datensatzdetails]** Wählen Sie das Datenbanksymbol (![Bild des Datenbanksymbols](../images/ui/ttl/database-icon.png)), um ein Dialogfeld zur Datensatzauswahl zu öffnen. Wählen Sie einen Datensatz aus der Liste aus, auf den die TTL angewendet werden soll, und wählen Sie dann **[!UICONTROL Fertig]**.

![Bild mit dem ausgewählten Datensatz](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Es werden nur Datensätze angezeigt, die zur aktuellen Sandbox gehören.

### Anfrage senden

Nachdem Sie einen Datensatz und ein TTL-Datum ausgewählt haben, wählen Sie **[!UICONTROL Einsenden]**.

![Bild, das die [!UICONTROL Einsenden] Schaltfläche ausgewählt](../images/ui/ttl/select-dataset.png)

Sie werden aufgefordert, das Datum zu bestätigen, ab dem der Datensatz gelöscht wird. Auswählen **[!UICONTROL Einsenden]** , um fortzufahren.

Nachdem die Anfrage gesendet wurde, wird eine Arbeitsreihenfolge erstellt und auf der [!UICONTROL Verbraucher] des [!UICONTROL Datenhygiene] Arbeitsbereich. Von hier aus können Sie den Status der Arbeitsreihenfolge bei der Verarbeitung der Anforderung überwachen.

## TTL bearbeiten oder abbrechen

Um eine TTL zu bearbeiten oder abzubrechen, wählen Sie **[!UICONTROL Datensatz]** auf der Hauptseite des Arbeitsbereichs und wählen Sie die TTL aus der Liste aus.

Auf der Detailseite der TTL zeigt die rechte Leiste Steuerelemente zum Bearbeiten oder Abbrechen des geplanten Löschvorgangs an.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie Datensatz-TTLs in der Experience Platform-Benutzeroberfläche planen. Weitere Informationen zur Durchführung anderer Datenhygieneaufgaben in der Benutzeroberfläche finden Sie im Abschnitt [Übersicht über die Benutzeroberfläche der Datenhygiene](./overview.md).

Informationen zum Planen von Datensatz-TTLs mithilfe der Data Hygiene API finden Sie im Abschnitt [Endpunktleitfaden für Datensatz-TTL](../api/ttl.md).
