---
keywords: Experience Platform;Startseite;beliebte Themen;Datenflüsse löschen
description: Der Arbeitsbereich Quellen bietet Ihnen die Möglichkeit, vorhandene Batch- und Streaming-Datenflüsse zu löschen, die Fehler enthalten oder veraltet sind.
solution: Experience Platform
title: Löschen von Datenflüssen in der Benutzeroberfläche
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 18%

---

# Löschen von Datenflüssen in der Benutzeroberfläche

Der [!UICONTROL Quellen]-Arbeitsbereich ermöglicht das Löschen vorhandener Batch- und Streaming-Datenflüsse, die Fehler enthalten oder veraltet sind.

In diesem Tutorial werden Schritte zum Löschen von Datenflüssen mithilfe des [!UICONTROL Quellen]-Arbeitsbereichs beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Löschen von Datenflüssen

Wählen Sie in der [Experience Platform](https://platform.adobe.com)-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen, und wählen Sie dann **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile aus.

![Katalog](../../images/tutorials/delete/catalog.png)

Die **[!UICONTROL Datenflüsse]** wird angezeigt. Auf dieser Seite finden Sie eine Liste der anzeigbaren Datenflüsse, einschließlich Informationen zu ihrem Zieldatensatz, ihrer Quelle, ihrem Kontonamen und dem Erstellungsdatum.

Wählen Sie das Filtersymbol (![filter-icon](/help/images/icons/filter.png)) oben links aus, um das Sortier-Bedienfeld zu starten.

![Datenflüsse](../../images/tutorials/delete/dataflows.png)

Das Sortier-Bedienfeld bietet eine Liste aller Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Datenflüssen zuzugreifen, die mit den ausgewählten Quellen verknüpft sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Datenflüsse anzuzeigen. Nachdem Sie den zu löschenden Datenfluss identifiziert haben, wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Datenflusses aus.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Es wird ein Dropdown-Menü angezeigt, in dem Sie Optionen zum Bearbeiten des Zeitplans Ihres Datenflusses, zum Deaktivieren des Datenflusses oder zum vollständigen Löschen finden.

Wählen Sie **[!UICONTROL Löschen]** aus, um den Datenfluss zu löschen.

![löschen](../../images/tutorials/delete/delete.png)

Ein letztes Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus, um den Vorgang abzuschließen.

![Bestätigen](../../images/tutorials/delete/confirm.png)

Nach einigen Augenblicken wird am unteren Bildschirmrand ein Bestätigungsfeld angezeigt, um eine erfolgreiche Löschung zu bestätigen.

![Bestätigt](../../images/tutorials/delete/confirmed.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] zum Löschen eines vorhandenen Datenflusses verwendet.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe [ API-Aufrufen finden Sie ](../../tutorials/api/delete-dataflows.md) Tutorial zum Löschen von Datenflüssen mithilfe der Flow Service-API .
