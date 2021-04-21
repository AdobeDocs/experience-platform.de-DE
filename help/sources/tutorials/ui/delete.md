---
keywords: Experience Platform;Home;beliebte Themen; dataflows löschen
description: Der Arbeitsbereich "Quellen"bietet Ihnen die Möglichkeit, vorhandene Batch- und Streaming-Datenflüsse zu löschen, die Fehler enthalten oder veraltet sind.
solution: Experience Platform
title: Datenflüsse in der Benutzeroberfläche löschen
topic-legacy: overview
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 5%

---

# Löschen von Datenflüssen in der Benutzeroberfläche

Im Arbeitsbereich [!UICONTROL Quellen] können Sie vorhandene Batch- und Streaming-Datenflüsse löschen, die Fehler enthalten oder veraltet sind.

Dieses Lernprogramm enthält Schritte zum Löschen von Datenflüssen mithilfe des Arbeitsbereichs [!UICONTROL Quellen].

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
- [Sandboxen](../../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

## Datenflüsse löschen

Wählen Sie in der Benutzeroberfläche [Experience Platform](https://platform.adobe.com) **[!UICONTROL Quellen]** aus der linken Navigation aus, um den Arbeitsbereich [!UICONTROL Quellen] aufzurufen, und wählen Sie dann **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile.

![Katalog](../../images/tutorials/delete/catalog.png)

Die Seite **[!UICONTROL Datenflüsse]** wird angezeigt. Auf dieser Seite finden Sie eine Liste anzeigbarer Datenflüsse, einschließlich Informationen zu ihrem Dataset, ihrer Quelle, ihrem Kontonamen und dem Erstellungsdatum.

Wählen Sie oben links das Filtersymbol (![filter-icon](../../images/tutorials/delete/filter.png)), um das Sortierfeld zu starten.

![Datenflüsse](../../images/tutorials/delete/dataflows.png)

Der Sortierbereich bietet eine Liste aller Quellen. Sie können mehr als eine Quelle aus der Liste auswählen, um auf eine gefilterte Auswahl von Datenflüssen zuzugreifen, die mit den ausgewählten Quellen verknüpft sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Datenflüsse anzuzeigen. Nachdem Sie den zu löschenden Datenpfad identifiziert haben, wählen Sie die Auslassungspunkte (`...`) neben dem Datenfeldnamen aus.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Es wird ein Dropdown-Menü angezeigt, mit Optionen zum Bearbeiten des Zeitplans des Datenflusses, zum Deaktivieren des Datenflusses oder zum vollständigen Löschen.

Wählen Sie **[!UICONTROL Löschen]**, um den Datendurchlauf zu löschen.

![Löschen Sie](../../images/tutorials/delete/delete.png)

Ein Dialogfeld zur letzten Bestätigung wird angezeigt. Wählen Sie **[!UICONTROL Löschen]**, um den Prozess abzuschließen.

![bestätigen](../../images/tutorials/delete/confirm.png)

Nach einigen Augenblicken wird unten im Bildschirm ein Bestätigungsfeld angezeigt, um einen erfolgreichen Löschvorgang zu bestätigen.

![bestätigt](../../images/tutorials/delete/confirmed.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] zum Löschen eines vorhandenen Datenflusses verwendet.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe von API-Aufrufen finden Sie im Lernprogramm zum Löschen von Datenflüssen mithilfe der Flow Service API](../../tutorials/api/delete-dataflows.md).[
