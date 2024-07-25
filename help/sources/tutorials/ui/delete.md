---
keywords: Experience Platform; home; beliebte Themen; Löschen von Datenflüssen
description: Der Arbeitsbereich "Quellen"bietet Ihnen die Möglichkeit, vorhandene Batch- und Streaming-Datenflüsse zu löschen, die Fehler enthalten oder mittlerweile veraltet sind.
solution: Experience Platform
title: Löschen von Datenflüssen in der Benutzeroberfläche
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 18%

---

# Löschen von Datenflüssen in der Benutzeroberfläche

Im Arbeitsbereich [!UICONTROL Quellen] können Sie vorhandene Batch- und Streaming-Datenflüsse löschen, die Fehler enthalten oder mittlerweile veraltet sind.

In diesem Tutorial werden Schritte zum Löschen von Datenflüssen mithilfe des Arbeitsbereichs [!UICONTROL Quellen] beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Löschen von Datenflüssen

Wählen Sie in der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com) im linken Navigationsbereich die Option **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen, und wählen Sie dann **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile aus.

![Katalog](../../images/tutorials/delete/catalog.png)

Die Seite **[!UICONTROL Datenflüsse]** wird angezeigt. Auf dieser Seite finden Sie eine Liste sichtbarer Datenflüsse, einschließlich Informationen zu ihrem Zieldatensatz, ihrer Quelle, dem Kontonamen und dem Erstellungsdatum.

Wählen Sie oben links das Filtersymbol (![filter-icon](/help/images/icons/filter.png)) aus, um das Sortierfeld zu starten.

![dataflows](../../images/tutorials/delete/dataflows.png)

Das Sortierungsfenster bietet eine Liste aller Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Datenflüssen zuzugreifen, die mit den ausgewählten Quellen verknüpft sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Datenflüsse anzuzeigen. Nachdem Sie den zu löschenden Datenfluss identifiziert haben, wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Datenflusses aus.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Es wird ein Dropdown-Menü angezeigt, in dem Sie Optionen zum Bearbeiten des Zeitplans Ihres Datenflusses, zum Deaktivieren des Datenflusses oder zum vollständigen Löschen haben.

Wählen Sie **[!UICONTROL Löschen]** aus, um den Datenfluss zu löschen.

![löschen](../../images/tutorials/delete/delete.png)

Ein letztes Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus, um den Vorgang abzuschließen.

![confirm](../../images/tutorials/delete/confirm.png)

Nach einigen Augenblicken wird unten im Bildschirm ein Bestätigungsfeld angezeigt, um eine erfolgreiche Löschung zu bestätigen.

![bestätigte](../../images/tutorials/delete/confirmed.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] zum Löschen eines vorhandenen Datenflusses verwendet.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe von API-Aufrufen finden Sie im Tutorial zum Löschen von Datenflüssen mit der Flow Service-API](../../tutorials/api/delete-dataflows.md) .[
