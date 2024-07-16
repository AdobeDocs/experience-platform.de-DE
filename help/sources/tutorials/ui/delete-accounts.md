---
keywords: Experience Platform; Homepage; beliebte Themen; Konten löschen
description: Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten planmäßig zu erfassen. In diesem Tutorial werden Schritte zum Löschen von Konten aus dem Arbeitsbereich "Quellen"beschrieben.
solution: Experience Platform
title: Löschen von Source-Verbindungskonten in der Benutzeroberfläche
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 19%

---

# Quell-Verbindungskonten löschen

Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten planmäßig zu erfassen. In diesem Tutorial werden Schritte zum Löschen von Konten aus dem Arbeitsbereich **[!UICONTROL Quellen]** beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Löschen von Konten über die Benutzeroberfläche

>[!TIP]
>
>Bevor Sie das Quellkonto löschen, müssen Sie zunächst alle damit verbundenen Datenflüsse löschen. Informationen zum Löschen vorhandener Datenflüsse finden Sie im Tutorial zum [Löschen von Datenflüssen aus Quellen in der Benutzeroberfläche](./delete.md).

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** enthält verschiedene Quellen, für die Sie Konten und Datenflüsse erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Wählen Sie **[!UICONTROL Konten]** aus, um auf die Seite **[!UICONTROL Konten]** zuzugreifen.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

Eine Liste der vorhandenen Konten wird angezeigt. Auf dieser Seite finden Sie eine Liste sortierbarer Informationen für vorhandene Konten wie Quelle, Benutzername, verknüpfte Datenflüsse und Erstellungsdatum. Wählen Sie oben links das **Trichtersymbol** aus, um es zu sortieren.

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

Das Sortierungsfenster wird auf der linken Bildschirmseite mit einer Liste der verfügbaren Quellen angezeigt. Mithilfe der Sortierfunktion können Sie mehrere Quellen auswählen.

Wählen Sie die Quelle aus, auf die Sie zugreifen möchten, und suchen Sie das Konto, das Sie löschen möchten, in der Liste der Konten in der Hauptbenutzeroberfläche. Im Beispiel ist die ausgewählte Quelle **[!DNL Azure Blob Storage]** und der Kontoname **[!UICONTROL blobTestConnector]**. Bei der Auswahl mehrerer Quellen aus dem Sortierungsfenster werden die zuletzt erstellten Konten zuerst angezeigt, da die Liste nach dem Erstellungsdatum sortiert wird.

Wählen Sie das Konto aus, das Sie löschen möchten.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

Das Bedienfeld **[!UICONTROL Eigenschaften]** wird rechts im Bildschirm mit Informationen zum ausgewählten Konto angezeigt.

Wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Kontos aus, das Sie löschen möchten. Es wird ein Popup-Fenster mit Optionen für **[!UICONTROL Daten hinzufügen]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]** angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus, um das Konto zu löschen.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Ein letztes Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus, um den Vorgang abzuschließen.

![löschen](../../images/tutorials/delete-accounts/confirm.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich **[!UICONTROL Quellen]** zum Löschen vorhandener Konten verwendet.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service]-API finden Sie im Tutorial zum [Löschen von Verbindungen mithilfe der Flow Service-API](../../tutorials/api/delete.md) .
