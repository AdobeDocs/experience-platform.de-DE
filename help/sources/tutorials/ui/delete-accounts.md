---
keywords: Experience Platform;Startseite;beliebte Themen;Konten löschen
description: Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen nach einem bestimmten Zeitplan aufzunehmen. In diesem Tutorial werden Schritte zum Löschen von Konten aus dem Arbeitsbereich Quellen beschrieben.
solution: Experience Platform
title: Löschen von Source-Verbindungskonten in der Benutzeroberfläche
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 19%

---

# Quellverbindungskonten löschen

Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen nach einem bestimmten Zeitplan aufzunehmen. In diesem Tutorial werden Schritte zum Löschen von Konten aus dem Arbeitsbereich **[!UICONTROL Quellen]** beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Löschen von Konten über die Benutzeroberfläche

>[!TIP]
>
>Bevor Sie das Quellkonto löschen, müssen Sie zunächst alle damit verbundenen Datenflüsse löschen. Informationen zum Löschen vorhandener Datenflüsse finden Sie im Tutorial [Löschen von Quelldatenflüssen in der Benutzeroberfläche](./delete.md).

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie Konten und Datenflüsse erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und der mit ihnen verbundenen Datenflüsse an.

Wählen Sie **[!UICONTROL Konten]** aus, um auf die Seite **[!UICONTROL Konten]** zuzugreifen.

![Katalog-Konten](../../images/tutorials/delete-accounts/catalog.png)

Eine Liste der vorhandenen Konten wird angezeigt. Auf dieser Seite finden Sie eine Liste sortierbarer Informationen für vorhandene Konten wie Quelle, Benutzername, zugehörige Datenflüsse und Erstellungsdatum. Wählen Sie oben links **Trichtersymbol**, um zu sortieren.

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

Das Sortier-Bedienfeld wird auf der linken Seite des Bildschirms angezeigt und enthält eine Liste der verfügbaren Quellen. Mit der Sortierfunktion können Sie mehr als eine Quelle auswählen.

Wählen Sie die Quelle aus, auf die Sie zugreifen möchten, und suchen Sie das Konto, das Sie löschen möchten, aus der Liste der Konten in der Hauptbenutzeroberfläche. Im Beispiel ist die ausgewählte Quelle **[!DNL Azure Blob Storage]** und der Kontoname **[!UICONTROL blobTestConnector]**. Bei der Auswahl mehrerer Quellen im Sortierungsbereich werden Ihre zuletzt erstellten Konten zuerst angezeigt, da die Liste nach Erstellungsdatum sortiert ist.

Wählen Sie das Konto aus, das Sie löschen möchten.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

Das **[!UICONTROL Eigenschaften]**-Bedienfeld wird auf der rechten Seite des Bildschirms angezeigt, das Informationen zum ausgewählten Konto enthält.

Klicken Sie auf die Auslassungszeichen (`...`) neben dem Namen des Kontos, das Sie löschen möchten. Es wird ein Popup-Bedienfeld angezeigt, das Optionen für **[!UICONTROL Daten hinzufügen]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]** bietet. Wählen Sie **[!UICONTROL Löschen]** aus, um das Konto zu löschen.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Wählen Sie im daraufhin angezeigten Bestätigungsdialogfeld **[!UICONTROL Löschen]** aus, um den Vorgang abzuschließen.

![löschen](../../images/tutorials/delete-accounts/confirm.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich **[!UICONTROL Quellen]** zum Löschen vorhandener Konten verwendet.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service]-API finden Sie im Tutorial zum [Löschen von Verbindungen mithilfe der Flow Service-API](../../tutorials/api/delete.md)
