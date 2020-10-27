---
keywords: Experience Platform;home;popular topics; delete accounts
description: Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Löschen von Konten aus dem Quellarbeitsbereich.
solution: Experience Platform
title: Konten löschen
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: e0168c58e3279f27d45d10b79c130935e46afd3d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 9%

---


# Konten löschen

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Löschen von Konten aus dem **[!UICONTROL Quellarbeitsbereich]** .

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model] (XDM) System](../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Konten mithilfe der Benutzeroberfläche löschen

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den **[!UICONTROL Quellarbeitsbereich]** zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verschiedene Quellen angezeigt, für die Sie Konten und Datenflüsse erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Wählen Sie **[!UICONTROL Konten]** , um auf die Seite &quot; **[!UICONTROL Konten]** &quot;zuzugreifen.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

Eine Liste der vorhandenen Konten wird angezeigt. Auf dieser Seite finden Sie eine Liste sortierbarer Informationen zu bestehenden Konten wie Quelle, Benutzername, verknüpfte Datenflüsse und Erstellungsdatum. Wählen Sie das **Trichtersymbol** oben links, das sortiert werden soll.

![dataflows-Liste](../../images/tutorials/delete-accounts/accounts.png)

Das Sortierungsbedienfeld wird auf der linken Seite des Bildschirms mit einer Liste der verfügbaren Quellen angezeigt. Mit der Sortierfunktion können Sie mehrere Quellen auswählen.

Wählen Sie die Quelle aus, auf die Sie zugreifen möchten, und suchen Sie das Konto, das Sie löschen möchten, in der Liste der Konten in der Hauptoberfläche. In diesem Beispiel ist die ausgewählte Quelle **[!DNL Azure Blob Storage]** und der Kontoname ist **[!UICONTROL blobTestConnector]**. Wenn Sie mehrere Quellen aus dem Sortierungsbedienfeld auswählen, werden Ihre zuletzt erstellten Konten zuerst angezeigt, da die Liste nach dem erstellten Datum sortiert wird.

Wählen Sie das Konto aus, das Sie löschen möchten.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

Das Bedienfeld &quot; **[!UICONTROL Eigenschaften]** &quot;wird auf der rechten Seite des Bildschirms mit Informationen zum ausgewählten Konto angezeigt.

Wählen Sie die Auslassungspunkte (`...`) neben dem Namen des Kontos aus, das gelöscht werden soll. Es wird ein Popup-Bedienfeld mit Optionen zum **[!UICONTROL Hinzufügen von Daten]**, zum **[!UICONTROL Bearbeiten von Details]** und zum **[!UICONTROL Löschen]** angezeigt. Wählen Sie **[!UICONTROL Löschen]** , um das Konto zu löschen.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Ein abschließendes Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** , um den Vorgang abzuschließen.

![Löschen Sie](../../images/tutorials/delete-accounts/confirm.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie die **[!UICONTROL Quellarbeitsfläche]** erfolgreich zum Löschen vorhandener Konten verwendet.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service] API finden Sie im Lernprogramm zum [Löschen von Verbindungen mit der Flow Service API](../../tutorials/api/delete.md)