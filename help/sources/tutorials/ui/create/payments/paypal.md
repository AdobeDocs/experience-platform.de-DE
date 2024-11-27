---
keywords: Experience Platform;home;popular topics;paypal;Paypal
solution: Experience Platform
title: Erstellen einer PayPal-Source-Verbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine PayPal-Quellverbindung erstellen.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 43%

---

# Erstellen eines Quell-Connectors für [!DNL PayPal] in der Benutzeroberfläche

>[!WARNING]
>
>Die Quelle [!DNL PayPal] wird Ende Juni 2025 eingestellt.

Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten planmäßig zu erfassen. In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für [!DNL PayPal] mithilfe der Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL PayPal] -Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [ fortfahren.](../../dataflow/payments.md)

### Sammeln erforderlicher Anmeldedaten

Um auf Ihre [!DNL PayPal] -Kontoplattform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Die URL der [!DNL PayPal] -Instanz. |
| `clientID` | Die mit Ihrer [!DNL PayPal] -Anwendung verknüpfte Client-ID. |
| `clientSecret` | Das Client-Geheimnis, das Ihrer [!DNL PayPal]-Anwendung zugeordnet ist. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL PayPal] Dokument](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Verbinden Ihres [!DNL PayPal]-Kontos

Nachdem Sie die erforderlichen Anmeldedaten zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL PayPal]-Konto mit Platform zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Zahlungen]** die Option **[!UICONTROL PayPal]** aus. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Klicken Sie andernfalls auf **[!UICONTROL Daten hinzufügen]** , um einen neuen [!DNL PayPal]-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/paypal/catalog.png)

Die Seite **[!UICONTROL Verbindung zu PayPal herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre [!DNL PayPal]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/paypal/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL PayPal]-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]** , um fortzufahren.

![vorhanden](../../../../images/tutorials/create/paypal/existing.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL PayPal]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss [konfigurieren, um Zahlungsdaten in Platform](../../dataflow/payments.md) zu importieren.
