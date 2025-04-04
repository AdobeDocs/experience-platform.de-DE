---
keywords: Experience Platform;Startseite;beliebte Themen;Square;Square
title: Erstellen einer Square-Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Square-Quellverbindung erstellen.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 44%

---

# Erstellen eines Quell-Connectors für [!DNL Square] in der Benutzeroberfläche

In diesem Tutorial finden Sie die Schritte zum Erstellen eines [!DNL Square]-Quell-Connectors mithilfe der Benutzeroberfläche von Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL Square]-Konto Experience Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Host | Die URL der [!DNL Square]. |
| Client-ID | Die mit Ihrem [!DNL Square]-Konto verknüpfte Client-ID. |
| Client-Geheimnis | Das mit Ihrem [!DNL Square]-Konto verknüpfte Client-Geheimnis. |
| Zugriffs-Token | Das Zugriffstoken wird verwendet, um Ihr [!DNL Square]-Konto mit OAuth 2.0-Authentifizierung zu authentifizieren. Das Zugriffstoken kann von [!DNL Square] abgerufen werden. |
| Token aktualisieren | Das Aktualisierungs-Token wird verwendet, um neue Zugriffs-Token zu generieren, sobald Ihr aktuelles Zugriffs-Token abläuft. Das Aktualisierungstoken kann von [!DNL Square] abgerufen werden. |

Weitere Informationen zu diesen Anmeldeinformationen und deren Abruf finden Sie unter [[!DNL Square] Dokumentation zu OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Square]-Konto mit Experience Platform zu verknüpfen.

## Verbinden Ihres [!DNL Square]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Zahlungen] die Option **[!UICONTROL Quadrat]** und dann **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/square/catalog.png)

Die **[!UICONTROL Mit Quadrat verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Square]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/square/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und die entsprechenden Werte für Ihre [!DNL Square]-Anmeldeinformationen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/square/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung zwischen Ihrem [!DNL Square]-Konto und Experience Platform authentifiziert und hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Erstellen eines Datenflusses, um Zahlungsdaten in Experience Platform zu importieren](../../dataflow/payments.md).
