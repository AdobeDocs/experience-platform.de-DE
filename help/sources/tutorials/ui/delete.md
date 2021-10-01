---
keywords: Experience Platform; Homepage; beliebte Themen Datenflüsse löschen
description: Der Arbeitsbereich "Quellen"bietet Ihnen die Möglichkeit, vorhandene Batch- und Streaming-Datenflüsse zu löschen, die Fehler enthalten oder mittlerweile veraltet sind.
solution: Experience Platform
title: Löschen von Datenflüssen in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 11%

---

# Löschen von Datenflüssen in der Benutzeroberfläche

Der Arbeitsbereich [!UICONTROL Quellen] ermöglicht Ihnen das Löschen vorhandener Batch- und Streaming-Datenflüsse, die Fehler enthalten oder veraltet sind.

In diesem Tutorial werden Schritte zum Löschen von Datenflüssen mithilfe des Arbeitsbereichs [!UICONTROL Quellen] beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
- [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Datenflüsse löschen

Wählen Sie in der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com) **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen, und wählen Sie dann **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile aus.

![Katalog](../../images/tutorials/delete/catalog.png)

Die Seite **[!UICONTROL Datenflüsse]** wird angezeigt. Auf dieser Seite finden Sie eine Liste sichtbarer Datenflüsse, einschließlich Informationen zu ihrem Zieldatensatz, ihrer Quelle, dem Kontonamen und dem Erstellungsdatum.

Wählen Sie oben links das Filtersymbol (![filter-icon](../../images/tutorials/delete/filter.png)) aus, um das Sortierfeld zu starten.

![Datenflüsse](../../images/tutorials/delete/dataflows.png)

Das Sortierungsfenster bietet eine Liste aller Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Datenflüssen zuzugreifen, die mit den ausgewählten Quellen verknüpft sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Datenflüsse anzuzeigen. Nachdem Sie den Datenfluss identifiziert haben, den Sie löschen möchten, wählen Sie die Auslassungszeichen (`...`) neben dem Dataflow-Namen aus.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Es wird ein Dropdown-Menü angezeigt, in dem Sie Optionen zum Bearbeiten des Zeitplans Ihres Datenflusses, zum Deaktivieren des Datenflusses oder zum vollständigen Löschen haben.

Wählen Sie **[!UICONTROL Löschen]** aus, um den Datenfluss zu löschen.

![delete](../../images/tutorials/delete/delete.png)

Ein letztes Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus, um den Prozess abzuschließen.

![Bestätigen](../../images/tutorials/delete/confirm.png)

Nach einigen Augenblicken wird unten im Bildschirm ein Bestätigungsfeld angezeigt, um eine erfolgreiche Löschung zu bestätigen.

![bestätigt](../../images/tutorials/delete/confirmed.png)

## Nächste Schritte

In diesem Tutorial haben Sie den Arbeitsbereich [!UICONTROL Quellen] erfolgreich zum Löschen eines vorhandenen Datenflusses verwendet.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe von API-Aufrufen finden Sie im Tutorial zum Löschen von Datenflüssen mithilfe der Flow Service-API](../../tutorials/api/delete-dataflows.md) .[
