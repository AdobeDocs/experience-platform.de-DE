---
title: SAP Hybris Source Overview
description: Erfahren Sie, wie Sie SAP Hybris mit Adobe Experience Platform über APIs oder die Benutzeroberfläche verbinden.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 32e2c13dcdbf2f13b4025354dfc50f5ccaf5f664
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 17%

---

# [!DNL SAP Hybris]

>[!NOTE]
>
>Die [!DNL SAP Hybris]-Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

[[!DNL SAP Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), eine Cloud-basierte E-Commerce-Plattform-Lösung für B2B- und B2C-Unternehmen, ist als Teil des SAP Customer Experience-Portfolios verfügbar. [[!DNL SAP] Abrechnung von Abonnements](https://www.sap.com/products/financial-management/subscription-billing.html) ist ein Produkt im Portfolio und ermöglicht ein komplettes Abonnement-Lebenszyklusmanagement mit vereinfachten Verkaufs- und Zahlungserlebnissen durch standardisierte Integrationen.

Die [!DNL SAP Hybris] -Quelle können Sie Kunden- und Kontaktinformationen aus dem [[!DNL SAP] Abrechnung von Abonnements](https://www.sap.com/products/financial-management/subscription-billing.html) Geschäftspartner-API-Endpunkte unten:

* [Kunden](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Kontakte](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Wenn [!DNL SAP Hybris] wird ausgeführt, um Kundendaten abzurufen, wird die [Kundenkontaktbeziehungen](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API wird auch aufgerufen, um die Kontaktinformationen des Kunden abzurufen.

## IP-Adressen-Zulassungsliste {#ip-allow-list}

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste möglicherweise eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre [!DNL SAP Hybris] -Daten an Experience Platform übermitteln, müssen Sie zunächst Folgendes sicherstellen:

* A [!DNL SAP Subscription Billing] -Konto. Wenn Sie noch kein gültiges Abrechnungskonto haben, wenden Sie sich an Ihren [!DNL SAP] Kundenbetreuer. Siehe Abschnitt [[!DNL SAP] Plattformkonfiguration](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) für weitere Details.

* [!DNL SAP] Dienstschlüssel. Die [!DNL SAP] -Dienstschlüssel ermöglicht Ihnen den Zugriff auf die [!DNL SAP Subscription Billing] API durch Experience Platform. [!DNL SAP Hybris] erfordert Folgendes:
   * Client-ID
   * Client-Geheimnis
   * URL. Das URL-Muster sieht wie folgt aus: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Dieser Wert wird später zum Abrufen von Werten für `region` und `tokenEndpoint` wenn Sie [Basisverbindung erstellen](../../tutorials/api/create/crm/sap-hybris.md#base-connection) Verwendung der API oder wenn Sie [Verbinden Sie Ihre [!DNL SAP Hybris] account](../../tutorials/ui/create/crm/sap-hybris.md#connect-account) über die Platform-Benutzeroberfläche.

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

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL SAP Hybris] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um [!DNL SAP Hybris] Daten an Platform mithilfe von APIs](../../tutorials/api/create/crm/sap-hybris.md).
* [Verbinden Sie Ihre [!DNL SAP Hybris] Konto für die Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/crm/sap-hybris.md).
* [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
