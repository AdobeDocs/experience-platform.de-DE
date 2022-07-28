---
title: Datensatz-TTL verwalten
description: Erfahren Sie, wie Sie in der Adobe Experience Platform-Benutzeroberfläche eine Time-to-Live (TTL) für einen Datensatz planen.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 95%

---

# Datensatz-TTL verwalten

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die den Gesundheitsschild erworben haben.

Sie können einen Zeitplan für die Time-to-Live (TTL) eines Datensatzes in der Adobe Experience Platform-Benutzeroberfläche im [[!UICONTROL Datenhygiene]-Arbeitsbereich](./overview.md) festlegen.

In diesem Dokument wird beschrieben, wie Sie Datensatz-TTLs in der Platform-Benutzeroberfläche planen und verwalten.

## Planen einer TTL

Um eine neue Anfrage zu erstellen, wählen Sie auf der Hauptseite im Arbeitsbereich die Option **[!UICONTROL Anfrage erstellen]** aus.

![Bild, das die ausgewählte Schaltfläche [!UICONTROL Anfrage erstellen] zeigt](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for TTL scheduling-->

### Auswählen von Datum und Datensatz

Daraufhin öffnet sich das Dialogfeld für die Anfrageerstellung. Wählen Sie im Abschnitt **[!UICONTROL Aktion]** ein Datum aus, an dem der Datensatz gelöscht werden soll. Sie können das Datum manuell eingeben (im Format `mm/dd/yyyy`) oder das Kalendersymbol anklicken (![Bild des Kalendersymbols](../images/ui/ttl/calendar-icon.png)) und dann das Datum aus einem Dialogfeld auswählen.

![Bild mit einem Ablaufdatum, das für die TTL festgelegt wird](../images/ui/ttl/select-date.png)

Wählen Sie danach unter **[!UICONTROL Datensatzdetails]** das Datenbanksymbol (![Bild des Datenbanksymbols](../images/ui/ttl/database-icon.png)), um ein Dialogfeld zur Datensatzauswahl zu öffnen. Wählen Sie aus der Liste einen Datensatz aus, auf den die TTL angewendet werden soll, und klicken Sie danach auf **[!UICONTROL Fertig]**.

![Bild mit dem ausgewählten Datensatz](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Es werden nur Datensätze angezeigt, die zur aktuellen Sandbox gehören.

### Senden der Anfrage

Nachdem Sie einen Datensatz und ein TTL-Datum ausgewählt haben, klicken Sie auf **[!UICONTROL Senden]**.

![Bild, das die ausgewählte Schaltfläche [!UICONTROL Senden] zeigt](../images/ui/ttl/submit.png)

Sie werden aufgefordert, das Datum zu bestätigen, an dem der Datensatz gelöscht werden soll. Wählen Sie **[!UICONTROL Senden]** aus, um fortzufahren.

Nachdem die Anfrage übermittelt wurde, wird ein Arbeitsauftrag erstellt und auf der Hauptregisterkarte des Arbeitsbereichs [!UICONTROL Datenhygiene] angezeigt. Hier können Sie den Fortschritt des Arbeitsauftrags überwachen.

## Bearbeiten oder Abbrechen einer TTL

Um eine TTL zu bearbeiten oder abzubrechen, wählen Sie auf der Hauptseite des Arbeitsbereichs **[!UICONTROL Datensatz]** und danach die jeweilige TTL aus der Liste aus.

Auf der Detailseite der TTL zeigt die rechte Leiste Steuerelemente zum Bearbeiten oder Abbrechen des geplanten Löschvorgangs an.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie in der Experience Platform-Benutzeroberfläche einen Zeitplan für Datensatz-TTLs erstellen können. Informationen zum Planen von Datensatz-TTLs mithilfe der Datenhygiene-API finden Sie im [Handbuch zum Datensatz-TTL-Endpunkt](../api/ttl.md).
