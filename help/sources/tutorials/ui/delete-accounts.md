---
keywords: Experience Platform; Homepage; beliebte Themen Konten löschen
description: Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden Schritte zum Löschen von Konten aus dem Arbeitsbereich "Quellen"beschrieben.
solution: Experience Platform
title: Löschen von Quellverbindungskonten in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 12%

---

# Quell-Verbindungskonten löschen

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden Schritte zum Löschen von Konten aus dem Arbeitsbereich **[!UICONTROL Quellen]** beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Löschen von Konten über die Benutzeroberfläche

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** enthält eine Vielzahl von Quellen, für die Sie Konten und Datenflüsse erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Wählen Sie **[!UICONTROL Konten]** aus, um auf die Seite **[!UICONTROL Konten]** zuzugreifen.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

Eine Liste der vorhandenen Konten wird angezeigt. Auf dieser Seite finden Sie eine Liste sortierbarer Informationen für vorhandene Konten wie Quelle, Benutzername, verknüpfte Datenflüsse und Erstellungsdatum. Wählen Sie oben links das Trichtersymbol **oben links aus, das sortiert werden soll.**

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

Das Sortierungsfenster wird auf der linken Bildschirmseite mit einer Liste der verfügbaren Quellen angezeigt. Mithilfe der Sortierfunktion können Sie mehrere Quellen auswählen.

Wählen Sie die Quelle aus, auf die Sie zugreifen möchten, und suchen Sie das Konto, das Sie löschen möchten, in der Liste der Konten in der Hauptbenutzeroberfläche. Im Beispiel ist die ausgewählte Quelle **[!DNL Azure Blob Storage]** und der Kontoname ist **[!UICONTROL blobTestConnector]**. Bei der Auswahl mehrerer Quellen aus dem Sortierungsfenster werden die zuletzt erstellten Konten zuerst angezeigt, da die Liste nach dem Erstellungsdatum sortiert wird.

Wählen Sie das Konto aus, das Sie löschen möchten.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

Das Bedienfeld **[!UICONTROL Eigenschaften]** wird rechts im Bildschirm mit Informationen zum ausgewählten Konto angezeigt.

Wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Kontos aus, das Sie löschen möchten. Es wird ein Popup-Fenster mit Optionen für **[!UICONTROL Daten hinzufügen]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]** angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus, um das Konto zu löschen.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Ein letztes Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus, um den Vorgang abzuschließen.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich **[!UICONTROL Quellen]** zum Löschen vorhandener Konten verwendet.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service]-API finden Sie im Tutorial zum Löschen von Verbindungen mithilfe der Flow Service-API](../../tutorials/api/delete.md) .[
