---
title: SAP Commerce Source - Überblick
description: Erfahren Sie, wie Sie SAP Commerce über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 5%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>Die [!DNL SAP Commerce]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html) ist eine Cloud-basierte E-Commerce-Plattformlösung für B2B- und B2C-Unternehmen als Teil des SAP Customer Experience Portfolios verfügbar. [[!DNL SAP] Subscription Billing](https://www.sap.com/products/financial-management/subscription-billing.html) ist ein Produkt aus dem Portfolio und ermöglicht durch standardisierte Integrationen ein vollständiges Abonnement-Lifecycle-Management mit vereinfachten Verkaufs- und Zahlungserlebnissen.

Die [!DNL SAP Commerce] ermöglicht es Ihnen, Kunden- und Kontaktinformationen aus den folgenden API[[!DNL SAP] Endpunkten für Geschäftspartner (Abonnementabrechnung](https://www.sap.com/products/financial-management/subscription-billing.html) in Experience Platform aufzunehmen:

* [Kunden](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Kontakte](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Wenn [!DNL SAP Commerce] zum Abrufen von Kundendaten ausgeführt wird, wird außerdem die API [Kunden-Kontakt-Beziehungen](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) aufgerufen, um die Kontaktinformationen des Kunden abzurufen.

## Zulassungsliste von IP-Adressen {#ip-allow-list}

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre [!DNL SAP Commerce] Daten in Experience Platform übertragen können, müssen Sie zunächst sicherstellen, dass Folgendes vorhanden ist:

* Ein [!DNL SAP Subscription Billing]. Wenn Sie noch kein gültiges Abrechnungskonto haben, wenden Sie sich bitte an Ihren [!DNL SAP] Account Manager. Weitere Informationen finden Sie [[!DNL SAP]  Dokument ](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf)Platform-Konfiguration“.

* Service-Schlüssel [!DNL SAP]. Mit dem [!DNL SAP]-Dienstschlüssel können Sie über Experience Platform auf die [!DNL SAP Subscription Billing]-API zugreifen. [!DNL SAP Commerce] erfordert Folgendes:
   * Client-ID
   * Client-Geheimnis
   * URL. Das URL-Muster sieht wie folgt aus: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Dieser Wert wird später verwendet, um Werte für `region` und `tokenEndpoint` abzurufen, wenn Sie [Basisverbindung erstellen](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) die API verwenden oder wenn Sie [Ihr  [!DNL SAP Commerce]  verbinden](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) über die Experience Platform-Benutzeroberfläche.

+++Wählen Sie aus, um ein Beispiel für den Dienstschlüssel anzuzeigen

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## Nächste Schritte

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL SAP Commerce] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um  [!DNL SAP Commerce]  mithilfe von APIs in Experience Platform zu ](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Verbinden Ihres - [!DNL SAP Commerce]  mit Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Erstellen eines Datenflusses für eine Quelle mithilfe der Benutzeroberfläche](../../tutorials/ui/dataflow/ecommerce.md)
