---
keywords: Experience Platform;Startseite;beliebte Themen;hubspot;hubspot
solution: Experience Platform
title: Erstellen einer HubSpot-Source-Verbindung über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine HubSpot-Quellverbindung erstellen.
exl-id: 452b7290-b9e8-4728-8b58-0e0c76bd9449
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 45%

---

# Erstellen eines Quell-Connectors für [!DNL HubSpot] in der Benutzeroberfläche

Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen nach einem bestimmten Zeitplan aufzunehmen. In diesem Tutorial finden Sie die Schritte zum Erstellen eines [!DNL HubSpot]-Quell-Connectors mithilfe der [!DNL Experience Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL HubSpot] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [&#x200B; eines Datenflusses &#x200B;](../../dataflow/marketing-automation.md).

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL HubSpot]-Konto in [!DNL Experience Platform] zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `clientId` | Die mit Ihrem [!DNL HubSpot] Programm verknüpfte Client-ID. |
| `clientSecret` | Das mit Ihrer [!DNL HubSpot]-Anwendung verknüpfte Client-Geheimnis. |
| `accessToken` | Das Zugriffstoken, das beim ersten Authentifizieren Ihrer OAuth-Integration abgerufen wurde. |
| `refreshToken` | Das Aktualisierungstoken, das beim ersten Authentifizieren Ihrer OAuth-Integration abgerufen wurde. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL HubSpot] Dokument](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Verbinden Ihres [!DNL HubSpot]-Kontos

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL HubSpot]-Konto mit [!DNL Experience Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Marketing]** Automatisierung **[!UICONTROL die Option „HubSpot]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Wählen Sie andernfalls **[!UICONTROL Daten hinzufügen]** aus, um einen neuen [!DNL HubSpot]-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/hubspot/catalog.png)

Die **[!UICONTROL Verbindung zu HubSpot herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL HubSpot] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen **[!UICONTROL Verbinden]** und warten Sie dann einige Zeit, bis die neue Verbindung hergestellt ist.

![Verbinden](../../../../images/tutorials/create/hubspot/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL HubSpot] Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/hubspot/existing.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL HubSpot]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten zur Marketing-Automatisierung in zu importieren [!DNL Experience Platform]](../../dataflow/marketing-automation.md).
