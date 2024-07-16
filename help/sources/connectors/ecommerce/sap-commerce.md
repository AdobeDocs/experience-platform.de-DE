---
title: Übersicht über SAP Commerce Source
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
>Die [!DNL SAP Commerce]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), eine Cloud-basierte E-Commerce-Plattform-Lösung für B2B- und B2C-Unternehmen, ist als Teil des SAP Customer Experience-Portfolios verfügbar. [[!DNL SAP] Abonnement-Abrechnung](https://www.sap.com/products/financial-management/subscription-billing.html) ist ein Produkt im Portfolio und ermöglicht ein vollständiges Abonnementlebenszyklusmanagement mit vereinfachten Verkaufs- und Zahlungserlebnissen durch standardisierte Integrationen.

Mit der Quelle [!DNL SAP Commerce] können Sie Kunden- und Kontaktinformationen aus den unten stehenden API-Endpunkten für die [[!DNL SAP] Abonnementabrechnung](https://www.sap.com/products/financial-management/subscription-billing.html)-Geschäftspartner in Platform erfassen:

* [Customers](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contacts](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Wenn [!DNL SAP Commerce] ausgeführt wird, um Kundendaten abzurufen, wird außerdem die API [Kundenkontaktbeziehungen](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) aufgerufen, um die Kontaktinformationen des Kunden abzurufen.

## IP-Adressen-Zulassungsliste {#ip-allow-list}

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste möglicherweise eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre [!DNL SAP Commerce] -Daten auf Experience Platform bringen können, müssen Sie zunächst sicherstellen, dass Sie über Folgendes verfügen:

* Ein [!DNL SAP Subscription Billing] -Konto. Wenn Sie noch kein gültiges Rechnungskonto haben, wenden Sie sich an Ihren [!DNL SAP] -Kundenbetreuer. Weitere Informationen finden Sie im Dokument [[!DNL SAP] Plattformkonfiguration](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) .

* [!DNL SAP] Dienstschlüssel. Mit dem Dienstschlüssel [!DNL SAP] können Sie über Experience Platform auf die [!DNL SAP Subscription Billing] -API zugreifen. [!DNL SAP Commerce] erfordert Folgendes:
   * Client-ID
   * Client-Geheimnis
   * URL. Das URL-Muster lautet wie folgt: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Dieser Wert wird später zum Abrufen von Werten für `region` und `tokenEndpoint` verwendet, wenn Sie [Basisverbindung erstellen](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) mit der API oder wenn Sie [Ihr [!DNL SAP Commerce] Konto verbinden](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) über die Platform-Benutzeroberfläche verbinden.

+++Auswählen , um ein Beispiel des Dienstschlüssels anzuzeigen

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

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um  [!DNL SAP Commerce] Daten mithilfe von APIs an Platform zu bringen](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Verbinden Sie Ihr [!DNL SAP Commerce] Konto über die Benutzeroberfläche](../../tutorials/ui/create/ecommerce/sap-commerce.md) mit dem Experience Platform.
* [Erstellen eines Datenflusses für eine Quelle mithilfe der Benutzeroberfläche](../../tutorials/ui/dataflow/ecommerce.md)
