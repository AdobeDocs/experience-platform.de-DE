---
title: Erstellen einer Google Ads Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie eine Google Ads-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 29%

---

# Erstellen einer Google Ads-Quellverbindung in der Benutzeroberfläche

>[!WARNING]
>
>Die Quelle [!DNL Google Ads] ist vorübergehend nicht verfügbar. Adobe arbeitet an der Lösung von Problemen mit dieser Quelle.

>[!NOTE]
>
>Die Google Ads-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .

In diesem Tutorial werden die Schritte zum Erstellen einer Google Ads-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige Google Ads-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [ fortfahren](../../dataflow/advertising.md)

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihre Google Ads-Kontoplattform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Client-Kunden-ID | Die Client-Kunden-ID ist die Kontonummer, die dem Google Ads-Kundenkonto entspricht, das Sie mit der Google Ads-API verwalten möchten. Diese ID folgt der Vorlage von `123-456-7890`. |
| Kunden-ID anmelden | Die Anmelde-Kunden-ID ist die Kontonummer, die Ihrem Google Ads Manager-Konto entspricht und zum Abrufen von Berichtsdaten von einem bestimmten Betriebssystemkunden verwendet wird. Weitere Informationen zur Anmelde-Kunden-ID finden Sie in der Dokumentation zur Google Ads-API ](https://developers.google.com/search-ads/reporting/concepts/login-customer-id).[ |
| Entwickler-Token | Mit dem Entwicklungstoken können Sie auf die Google Ads-API zugreifen. Sie können dasselbe Entwickler-Token verwenden, um Anforderungen für alle Ihre Google Ads-Konten zu stellen. Rufen Sie Ihr Entwickler-Token ab, indem Sie sich bei Ihrem Manager-Konto anmelden](https://ads.google.com/home/tools/manager-accounts/) und dann zur Seite &quot;API-Center&quot;navigieren.[ |
| Token aktualisieren | Das Aktualisierungstoken ist Teil der [!DNL OAuth2] -Authentifizierung. Mit diesem Token können Sie Ihre Zugriffstoken nach ihrem Ablauf neu generieren. |
| Client-ID | Die Client-ID wird zusammen mit dem Client-Geheimnis als Teil der [!DNL OAuth2]-Authentifizierung verwendet. Gemeinsam ermöglicht die Client-ID und das Client-Geheimnis Ihrer Anwendung die Ausführung Ihrer Kontoverbindung, indem Sie Ihre Anwendung für Google identifizieren. |
| Client-Geheimnis | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der [!DNL OAuth2]-Authentifizierung verwendet. Gemeinsam ermöglicht die Client-ID und das Client-Geheimnis Ihrer Anwendung die Ausführung Ihrer Kontoverbindung, indem Sie Ihre Anwendung für Google identifizieren. |

Weitere Informationen zu den ersten Schritten mit Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview) finden Sie im Dokument API-Übersicht .[

## Google Ads-Konto verbinden

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Advertising]** die Option **[!UICONTROL Google Ads]** und dann **[!UICONTROL Add data]**.

![Der Quellkatalog in der Experience Platform-Benutzeroberfläche.](../../../../images/tutorials/create/ads/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Google Ads herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein bestehendes Konto zu verbinden, wählen Sie das Google Ads-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]** , um fortzufahren.

![Die Auswahlseite für vorhandene Konten im Ursprungs-Workflow.](../../../../images/tutorials/create/ads/existing.png)

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre Google Ads-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle im Ursprungs-Workflow.](../../../../images/tutorials/create/ads/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem Google Ads-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss konfigurieren, um Werbedaten in Platform](../../dataflow/advertising.md) zu importieren.[
