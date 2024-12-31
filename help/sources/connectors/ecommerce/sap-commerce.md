---
title: SAP Commerce Source - Überblick
description: Erfahren Sie, wie Sie SAP Commerce über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 19%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>Die [!DNL SAP Commerce]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html) ist eine Cloud-basierte E-Commerce-Plattformlösung für B2B- und B2C-Unternehmen als Teil des SAP Customer Experience Portfolios verfügbar. [[!DNL SAP] Subscription Billing](https://www.sap.com/products/financial-management/subscription-billing.html) ist ein Produkt aus dem Portfolio und ermöglicht durch standardisierte Integrationen ein vollständiges Abonnement-Lifecycle-Management mit vereinfachten Verkaufs- und Zahlungserlebnissen.

Die [!DNL SAP Commerce] Quelle ermöglicht es Ihnen, Kunden- und Kontaktinformationen aus den folgenden API[[!DNL SAP] Endpunkten von Geschäftspartnern (Abonnementabrechnung](https://www.sap.com/products/financial-management/subscription-billing.html) in Platform aufzunehmen:

* [Kunden](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Kontakte](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Wenn [!DNL SAP Commerce] zum Abrufen von Kundendaten ausgeführt wird, wird außerdem die API [Kunden-Kontakt-Beziehungen](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) aufgerufen, um die Kontaktinformationen des Kunden abzurufen.

## IP-Adressen-Zulassungsliste {#ip-allow-list}

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste möglicherweise eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre [!DNL SAP Commerce] auf Experience Platform übertragen können, müssen Sie zunächst sicherstellen, dass Folgendes vorhanden ist:

* Ein [!DNL SAP Subscription Billing]. Wenn Sie noch kein gültiges Abrechnungskonto haben, wenden Sie sich bitte an Ihren [!DNL SAP] Account Manager. Weitere Informationen finden Sie [[!DNL SAP]  Dokument ](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf)Platform-Konfiguration“.

* Service-Schlüssel [!DNL SAP]. Mit dem [!DNL SAP]-Dienstschlüssel können Sie über Experience Platform auf die [!DNL SAP Subscription Billing]-API zugreifen. [!DNL SAP Commerce] erfordert Folgendes:
   * Client-ID
   * Client-Geheimnis
   * URL. Das URL-Muster sieht wie folgt aus: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Dieser Wert wird später verwendet, um Werte für `region` und `tokenEndpoint` abzurufen, wenn Sie [Basisverbindung erstellen](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) die API verwenden oder wenn Sie [Ihr  [!DNL SAP Commerce] -Konto verbinden](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) über die Platform-Benutzeroberfläche.

+++Wählen Sie aus, um ein Beispiel für den Dienstschlüssel anzuzeigen.

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

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL SAP Commerce] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um  [!DNL SAP Commerce]  mithilfe von APIs in Platform zu ](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Verbinden Sie Ihr - [!DNL SAP Commerce]  über die Benutzeroberfläche mit dem Experience Platform](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Erstellen eines Datenflusses für eine Quelle mithilfe der Benutzeroberfläche](../../tutorials/ui/dataflow/ecommerce.md)
