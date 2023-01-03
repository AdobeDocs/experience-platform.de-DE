---
keywords: Experience Platform; Homepage; beliebte Themen Konten löschen
description: Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden Schritte zum Löschen von Konten aus dem Arbeitsbereich "Quellen"beschrieben.
solution: Experience Platform
title: Löschen von Quellverbindungskonten in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 19%

---

# Quell-Verbindungskonten löschen

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden Schritte zum Löschen von Konten aus dem **[!UICONTROL Quellen]** Arbeitsbereich.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Löschen von Konten über die Benutzeroberfläche

>[!TIP]
>
>Bevor Sie das Quellkonto löschen, müssen Sie zunächst alle damit verbundenen Datenflüsse löschen. Informationen zum Löschen vorhandener Datenflüsse finden Sie im Tutorial unter [Löschen von Datenflüssen für Quellen in der Benutzeroberfläche](./delete.md).

Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die **[!UICONTROL Quellen]** Arbeitsbereich. Die **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, für die Sie Konten und Datenflüsse erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Auswählen **[!UICONTROL Konten]** , um auf die **[!UICONTROL Konten]** Seite.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

Eine Liste der vorhandenen Konten wird angezeigt. Auf dieser Seite finden Sie eine Liste sortierbarer Informationen für vorhandene Konten wie Quelle, Benutzername, verknüpfte Datenflüsse und Erstellungsdatum. Wählen Sie die **Trichtersymbol** oben links, um zu sortieren.

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

Das Sortierungsfenster wird auf der linken Bildschirmseite mit einer Liste der verfügbaren Quellen angezeigt. Mithilfe der Sortierfunktion können Sie mehrere Quellen auswählen.

Wählen Sie die Quelle aus, auf die Sie zugreifen möchten, und suchen Sie das Konto, das Sie löschen möchten, in der Liste der Konten in der Hauptbenutzeroberfläche. In diesem Beispiel ist die ausgewählte Quelle **[!DNL Azure Blob Storage]** und der Kontoname lautet **[!UICONTROL blobTestConnector]**. Bei der Auswahl mehrerer Quellen aus dem Sortierungsfenster werden die zuletzt erstellten Konten zuerst angezeigt, da die Liste nach dem Erstellungsdatum sortiert wird.

Wählen Sie das Konto aus, das Sie löschen möchten.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

Die **[!UICONTROL Eigenschaften]** wird rechts im Bildschirm angezeigt und enthält Informationen zum ausgewählten Konto.

Wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Kontos, das Sie löschen möchten. Ein Popup-Bedienfeld wird angezeigt, das Optionen für **[!UICONTROL Daten hinzufügen]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]**. Auswählen **[!UICONTROL Löschen]** , um das Konto zu löschen.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Ein letztes Bestätigungsdialogfeld wird angezeigt, wählen Sie **[!UICONTROL Löschen]** , um den Prozess abzuschließen.

![löschen](../../images/tutorials/delete-accounts/confirm.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die **[!UICONTROL Quellen]** Arbeitsbereich zum Löschen vorhandener Konten.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mit dem [!DNL Flow Service] API, siehe Tutorial zu [Löschen von Verbindungen mithilfe der Flow Service-API](../../tutorials/api/delete.md)
