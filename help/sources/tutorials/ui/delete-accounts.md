---
keywords: Experience Platform;Home;beliebte Themen; Konten löschen
description: Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Löschen von Konten aus dem Quellarbeitsbereich.
solution: Experience Platform
title: Quellverbindungskonten in der Benutzeroberfläche löschen
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 9%

---

# Quellverbindungskonten löschen

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Löschen von Konten aus dem Arbeitsbereich **[!UICONTROL Quellen]**.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Konten mithilfe der Benutzeroberfläche löschen

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie Konten und Datenflüsse erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Wählen Sie **[!UICONTROL Konten]**, um auf die Seite **[!UICONTROL Konten]** zuzugreifen.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

Eine Liste der vorhandenen Konten wird angezeigt. Auf dieser Seite finden Sie eine Liste sortierbarer Informationen zu bestehenden Konten wie Quelle, Benutzername, verknüpfte Datenflüsse und Erstellungsdatum. Wählen Sie das Trichtersymbol **oben links zum Sortieren aus.**

![dataflows-Liste](../../images/tutorials/delete-accounts/accounts.png)

Das Sortierungsbedienfeld wird auf der linken Seite des Bildschirms mit einer Liste der verfügbaren Quellen angezeigt. Mit der Sortierfunktion können Sie mehrere Quellen auswählen.

Wählen Sie die Quelle aus, auf die Sie zugreifen möchten, und suchen Sie das Konto, das Sie löschen möchten, in der Liste der Konten in der Hauptoberfläche. Im Beispiel ist **[!DNL Azure Blob Storage]** als Quelle ausgewählt und der Kontoname **[!UICONTROL blobTestConnector]**. Wenn Sie mehrere Quellen aus dem Sortierungsbedienfeld auswählen, werden Ihre zuletzt erstellten Konten zuerst angezeigt, da die Liste nach dem erstellten Datum sortiert wird.

Wählen Sie das Konto aus, das Sie löschen möchten.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

Das Bedienfeld **[!UICONTROL Eigenschaften]** wird auf der rechten Seite des Bildschirms mit Informationen zum ausgewählten Konto angezeigt.

Wählen Sie die Auslassungspunkte (`...`) neben dem Namen des Kontos aus, das gelöscht werden soll. Es wird ein Popupfenster mit Optionen für **[!UICONTROL Hinzufügen Daten]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]** angezeigt. Wählen Sie **[!UICONTROL Löschen]**, um das Konto zu löschen.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Ein abschließendes Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]**, um den Prozess abzuschließen.

![Löschen Sie](../../images/tutorials/delete-accounts/confirm.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich den Arbeitsbereich **[!UICONTROL Quellen]** zum Löschen vorhandener Konten verwendet.

Anweisungen zum programmatischen Ausführen dieser Vorgänge mit der API [!DNL Flow Service] finden Sie im Lehrgang zum [Löschen von Verbindungen mit der Flow Service API](../../tutorials/api/delete.md)
