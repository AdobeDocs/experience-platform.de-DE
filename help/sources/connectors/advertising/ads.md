---
title: Übersicht über Google Ads Source
description: Erfahren Sie, wie Sie Google Ads mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: a0977e98219797eda14dd8d7ddb6cf3f1410cef0
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 18%

---

# [!DNL Google Ads]

>[!NOTE]
>
>Die [!DNL Google Ads]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Connectoren finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Experience Platform-Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Werbesystemen von Drittanbietern. Der Support für Werbeanbieter umfasst [!DNL Google Ads].

## Voraussetzungen {#prerequisites}

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

### Konfigurieren von Berechtigungen für Experience Platform

Sie müssen sowohl **[!UICONTROL Quellen anzeigen]** als auch **[!UICONTROL Quellen verwalten]** für Ihr Konto aktiviert haben, um Ihr [!DNL Google Ads]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/ui/overview.md).

### Sammeln erforderlicher Anmeldedaten

Sie müssen die entsprechenden Werte für die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Google Ads]-Konto erfolgreich mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `clientCustomerId` | Die Kunden-ID ist die Kontonummer, die dem [!DNL Google Ads] Kundenkonto entspricht, das Sie mit der [!DNL Google Ads]-API verwalten möchten. Diese ID folgt der Vorlage von `123-456-7890`. |
| `loginCustomerId` | Die Kunden-ID für die Anmeldung ist die Kontonummer, die Ihrem [!DNL Google Ads] Manager-Konto entspricht und zum Abrufen von Berichtsdaten von einem bestimmten aktiven Kunden verwendet wird. Weitere Informationen zur Anmelde-Kunden-ID finden Sie in der [[!DNL Google Ads] API-Dokumentation](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | Mit dem Entwickler-Token können Sie auf die [!DNL Google Ads]-API zugreifen. Sie können dasselbe Entwickler-Token verwenden, um Anfragen an alle Ihre [!DNL Google Ads]-Konten zu richten. Rufen Sie Ihr Entwickler-Token ab[ indem Sie sich bei Ihrem Manager-Konto ](https://ads.google.com/home/tools/manager-accounts/) und dann zur [!DNL API Center] navigieren. |
| `refreshToken` | Das Aktualisierungs-Token ist Teil [!DNL OAuth2] Authentifizierung. Mit diesem Token können Sie Ihre Zugriffs-Token nach ihrem Ablauf neu generieren. |
| `clientId` | Die Client-ID wird zusammen mit dem Client-Geheimnis im Rahmen [!DNL OAuth2] Authentifizierung verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre zu [!DNL Google] Anwendung identifizieren. |
| `clientSecret` | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil [!DNL OAuth2] Authentifizierung verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre zu [!DNL Google] Anwendung identifizieren. |
| `googleAdsApiVersion` | Die aktuelle von [!DNL Google Ads] unterstützte API-Version. Die neueste Version der [!DNL Google Ads]-API ist zwar v21, Experience Platform unterstützt jedoch derzeit Version v19 und höher. Stellen Sie sicher, dass Sie eine dieser unterstützten Versionen verwenden, um die Kompatibilität sicherzustellen. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Google Ads] lautet: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. Dieser Wert ist erforderlich, wenn Sie Ihr [!DNL Google Ads]-Konto über die [!DNL Flow Service]-API verbinden. |

## Verbinden von [!DNL Google Ads] mit Experience Platform

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Google Ads] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

### Verwenden von APIs

* [Erstellen einer Google Ads-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/advertising/ads.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Werbequelle mithilfe der Flow Service-API](../../tutorials/api/collect/advertising.md)

### Verwenden der Benutzeroberfläche

* [Erstellen einer Google Ads-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/advertising/ads.md)
* [Erstellen eines Datenflusses für eine Werbequellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/advertising.md)
