---
title: Erstellen einer SAP Commerce-Quellverbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Commerce-Quellverbindung für SAP erstellen.
badge: Beta
exl-id: 6484e51c-77cd-4dbd-9c68-0a4e3372da33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 28%

---

# Erstellen eines Quell-Connectors für [!DNL SAP Commerce] in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL SAP Commerce]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

Das folgende Tutorial führt Sie durch die Schritte zum Erstellen einer [!DNL SAP Commerce] Quellverbindung, um [[!DNL SAP] Abonnementabrechnung“, Kontakte ](https://www.sap.com/products/financial-management/subscription-billing.html) Kundendaten über die Benutzeroberfläche von Adobe Experience Platform zu übertragen.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL SAP Commerce]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/ecommerce.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten {#gather-credentials}

Um [!DNL SAP Commerce] mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Client-ID | Der Wert von `clientId` aus dem Service-Schlüssel. |
| Client-Geheimnis | Der Wert von `clientSecret` aus dem Service-Schlüssel. |
| Token-Endpunkt | Der Wert von `url` aus dem Service-Schlüssel ähnelt `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Region | Ihr Rechenzentrumsstandort. Die Region befindet sich in der `url` und hat einen ähnlichen Wert wie `eu10` oder `us10`. Wenn der `url` beispielsweise `https://eu10.revenue.cloud.sap/api` ist, benötigen Sie `eu10`. |

Weitere Informationen finden Sie in der [[!DNL SAP Commerce] Dokumentation](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

### Erstellen eines Experience Platform-Schemas {#create-platform-schema}

Bevor Sie eine [!DNL SAP Commerce] Quellverbindung erstellen, müssen Sie auch sicherstellen, dass Sie zunächst ein Experience Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Eine ausführliche Anleitung zum Erstellen [ Schemas finden Sie ](../../../../../xdm/schema/composition.md) Tutorial zum Erstellen eines Experience Platform-Schemas .

Erweitern Sie den folgenden Abschnitt, um ein Beispielschema anzuzeigen.

+++ Beispiel für ein Schema anzeigen

```
{
  "_extconndev": {
    "addresses": [
      {
        "addressUUID": "{ADDRESS_UUID}",
        "city": "Burnaby",
        "country": "Canada",
        "email": "chandni@acme.com",
        "houseNumber": "27",
        "isDefault": false,
        "phone": "123-456-7890",
        "postalCode": "V3J 1X9",
        "state": "British Columbia",
        "street": "Beresford"
      }
    ],
    "changedAt": "1687204041",
    "changedBy": "vero@acme.com",
    "contactNumber": "123-456-7980",
    "corporateInfo": {
      "company": "acme"
    },
    "createAt": "1687204041",
    "createdBy": "vero@acme.com",
    "customReferences": [
      {
        "id": "Sample value",
        "typeCode": "Sample value"
      }
    ],
    "customerNumber": "Sample value",
    "customerType": "Sample value",
    "defaultAddress": {
      "addressUUID": "Sample value",
      "city": "North Vancouver",
      "country": "Canada",
      "email": "chandni@acme.come",
      "houseNumber": "34",
      "isDefault": false,
      "phone": "123-456-7890",
      "postalCode": "V7H 2P1",
      "state": "British Columbia",
      "street": "Maple"
    },
    "externalObjectReferences": [
      {
        "externalId": "{EXTERNAL_ID}",
        "externalIdTypeCode": "{EXTERNAL_ID_TYPE_CODE}",
        "externalSystemId": "{EXTERNAL_SYSTEM_ID}"
      }
    ],
    "markets": [
      {
        "active": false,
        "country": "USA",
        "currency": "USD",
        "marketId": "Sample value",
        "priceinfo": {
          "incoterms": "{INCO_TERMS}",
          "incotermsLocation": "{INCO_TERMS_LOCATION}",
          "priceGroup": "{PRICE_GROUP}",
          "priceListType": "{PRICE_LIST_TYPE}"
        },
        "salesArea": {
          "distributionChannel": "{DISTRIBUTION_CHANNEL}",
          "division": "{DIVISION}",
          "salesOrganization": "{SALES_ORGANIZATION}"
        }
      }
    ],
    "personalInfo": {
      "firstName": "Chandni",
      "lastName": "Kaur"
    }
  },
  "_id": "/uri-reference",
  "_repo": {
    "createDate": "2004-10-23T12:00:00-06:00",
    "modifyDate": "2004-10-23T12:00:00-06:00"
  },
  "createdByBatchID": "/uri-reference",
  "modifiedByBatchID": "/uri-reference",
  "personID": "{PERSON_ID}",
  "repositoryCreatedBy": "kevin@acme.com",
  "repositoryLastModifiedBy": "kevin@acme.com"
}
```

+++

## Verbinden Ihres [!DNL SAP Commerce]-Kontos {#connect-account}

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter *eCommerce*-Kategorie die Option **[!UICONTROL SAP Commerce]** und dann **[!UICONTROL Daten hinzufügen]**.

![Screenshot der Experience Platform-Benutzeroberfläche für den Katalog mit der SAP Commerce-Karte](../../../../images/tutorials/create/ecommerce/sap-commerce/catalog-card.png)

Die **[!UICONTROL Verbinden des SAP Commerce-Kontos]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto {#existing-account}

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL SAP Commerce]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Screenshot der Experience Platform-Benutzeroberfläche zum Verbinden des SAP Commerce-Kontos mit einem bestehenden Konto](../../../../images/tutorials/create/ecommerce/sap-commerce/existing.png)

### Neues Konto {#new-account}

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldeinformationen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Screenshot der Experience Platform-Benutzeroberfläche zum Verbinden des SAP Commerce-Kontos mit einem neuen Konto](../../../../images/tutorials/create/ecommerce/sap-commerce/new.png)

### Daten auswählen {#select-data}

Schließlich müssen Sie den Objekttyp auswählen, den Sie in Experience Platform aufnehmen möchten.

| Objekttyp | Beschreibung |
| --- | --- |
| `Customers` | Die Entitäten, die Abonnements haben. |
| `Contacts` | Die Kontaktdaten für Kunden. |

>[!BEGINTABS]

>[!TAB Kunden]

Um Kundendaten aufzunehmen, wählen Sie **[!UICONTROL Kunden]** als Objekttyp aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![Screenshot der Experience Platform-Benutzeroberfläche für SAP Commerce mit Konfiguration mit ausgewählter Option „Kunden“](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-customers.png)

>[!TAB Kontakte]

Um Kontaktdaten aufzunehmen, wählen Sie **[!UICONTROL Kontakte]** als Objekttyp aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![Screenshot der Experience Platform-Benutzeroberfläche für SAP Commerce mit Konfiguration mit ausgewählter Option „Kontakte“](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-contacts.png)

>[!ENDTABS]

## Nächste Schritte {#next-steps}

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL SAP Commerce]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Experience Platform zu importieren](../../dataflow/ecommerce.md).

## Zusätzliche Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der [!DNL SAP Commerce] verweisen können.

### Zuordnung {#mapping}

Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle und berechneter Felder finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

Die Zuordnungskonfigurationen für Ihren Datenfluss unterscheiden sich je nach Schema und Objekttyp, den Sie aufnehmen möchten.

>[!BEGINTABS]

>[!TAB Kunden]

Für Kundendaten verwendet [!DNL SAP Commerce] die Endpunkte [Kunden](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers) und der [Beziehungen zwischen Kunden und ](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts)) der [!DNL SAP Business Partners]-API, um die Daten abzurufen

Im Folgenden finden Sie ein Beispiel für Zuordnungskonfigurationen für [!DNL SAP Commerce] Datenfluss für Kundendaten:

| Zielfeld | Beschreibung |
| --- | --- |
| `customerNumber` | Die Kundennummer. |
| `corporateInfo` | Die Kundennummer. |
| `customerType` | Der Kundentyp. |
| `createdAt` | Ein Zeitstempel, der angibt, wann der Kunde erstellt wurde. |
| `changedAt` | Ein Zeitstempel, der angibt, wann der Kunde zuletzt aktualisiert wurde. |
| `markets[*].country` | Die Kunden vermarkten als Array-Objekt abgerufen. |
| `addresses[*].email` | E-Mails, die mit den mehreren Adressen des Kunden verknüpft sind und als Array-Objekt abgerufen werden. |
| `addresses[*].city` | Städte, die mit den mehreren Adressen des Kunden verknüpft sind und als Array-Objekt abgerufen werden. |
| `addresses[*].addressUUID` | IDs, die mit den mehreren Adressen des Kunden verknüpft sind und als Array-Objekt abgerufen werden. |
| `externalObjectReferences[*].externalSystemId` | Zusätzliche Daten, als Array-Objekt abgerufen. |
| `externalObjectReferences[*].externalId` | Zusätzliche Daten, als Array-Objekt abgerufen. |
| `customReferences[*].id` | Zusätzliche Daten, als Array-Objekt abgerufen. |
| `customReferences[*].typeCode` | Zusätzliche Daten, als Array-Objekt abgerufen. |

![Der Zuordnungsschritt des Quell-Workflows.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-customers.png)

>[!TAB Kontakte]

Für Kontaktdaten verwendet [!DNL SAP Commerce] den Endpunkt [Kontakte](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts) der [!DNL SAP Business Partners]-API, um die Daten abzurufen.

Im Folgenden finden Sie ein Beispiel für Zuordnungskonfigurationen für [!DNL SAP Commerce] Datenfluss für Kontaktdaten:

| Zielfeld | Beschreibung |
| --- | --- |
| `contactNumber` | Die Nummer des Kontakts. |
| `createdAt` | Ein Zeitstempel, der angibt, wann der Kontakt erstellt wurde. |
| `changedAt` | Ein Zeitstempel, der angibt, wann der Kontakt zuletzt aktualisiert wurde. |
| `personalInfo.lastName` | Der Nachname des Kontakts. |
| `personalInfo.firstName` | Der Vorname des Kontakts. |
| `externalObjectReferences[*].externalSystemId` | Zusätzliche Daten, als Array-Objekt abgerufen. |
| `externalObjectReferences[*].externalId` | Zusätzliche Daten, als Array-Objekt abgerufen. |
| `externalObjectReferences[*].externalIdTypeCode` | Zusätzliche Daten, als Array-Objekt abgerufen. |

![Der Zuordnungsschritt des Quell-Workflows.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-contacts.png)

>[!ENDTABS]
