---
keywords: Experience Platform;home;Intelligent Services;popular topics
solution: Experience Platform
title: Prepare data for use in Intelligent Services
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 88e4a183422dd1bc625fd842e24c2604fb249c91
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 3%

---


# Prepare data for use in [!DNL Intelligent Services]

In order for [!DNL Intelligent Services] to discover insights from your marketing events data, the data must be semantically enriched and maintained in a standard structure. [!DNL Intelligent Services] leverage [!DNL Experience Data Model] (XDM) schemas in order to achieve this. Specifically, all datasets that are used in [!DNL Intelligent Services] must conform to the **Consumer ExperienceEvent (CEE)** XDM schema.

This document provides general guidance on mapping your marketing events data from multiple channels to this schema, outlining information on important fields within the schema to help you determine how to effectively map your data to its structure.

## Workflow summary

The preparation process varies depending on whether your data is stored in Adobe Experience Platform or externally. In diesem Abschnitt werden die notwendigen Schritte zusammengefasst, die Sie in beiden Szenarien unternehmen müssen.

### Vorbereitung externer Daten

Wenn Ihre Daten außerhalb von gespeichert werden, führen Sie die folgenden Schritte aus [!DNL Experience Platform]:

1. Wenden Sie sich an Adobe Consulting Services, um Zugangsdaten für einen dedizierten Azurblase Datenspeicherung Container anzufordern.
1. Laden Sie Ihre Daten mit Ihren Zugriffsberechtigungen in den Blob-Container hoch.
1. Arbeiten Sie mit Adobe Consulting Services, um Ihre Daten dem [Consumer ExperienceEvent-Schema](#cee-schema) zuzuordnen und in [!DNL Intelligent Services]einzubinden.

### [!DNL Experience Platform] Datenaufbereitung

Wenn Ihre Daten bereits in gespeichert sind, führen Sie [!DNL Platform]die folgenden Schritte aus:

1. Überprüfen Sie die Struktur des [Consumer ExperienceEvent-Schemas](#cee-schema) und stellen Sie fest, ob Ihre Daten Feldern zugeordnet werden können.
1. Wenden Sie sich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und sie zu erfassen, oder [!DNL Intelligent Services]befolgen Sie die Schritte in diesem Handbuch [](#mapping) , wenn Sie die Daten selbst zuordnen möchten.

## Das CEE-Schema {#cee-schema}

Das Consumer ExperienceEvent-Schema beschreibt das Verhalten eines Individuums in Bezug auf digitale Marketing-Ereignis (Web oder Mobil) sowie Online- oder Offline-Commerce-Aktivitäten. Die Verwendung dieses Schemas ist [!DNL Intelligent Services] aufgrund seiner semantisch definierten Felder (Spalten) erforderlich, wobei unbekannte Namen vermieden werden, die sonst die Daten weniger eindeutig machen würden.

Das CEE-Schema erfasst wie alle XDM ExperienceEvent-Schema den zeitreihenbasierten Systemzustand, in dem ein Ereignis (oder eine Reihe von Ereignissen) aufgetreten ist, einschließlich des Zeitpunkts und der Identität des jeweiligen Objekts. Erfahrungs-Ereignisse sind Faktenberichte über das, was geschehen ist, und somit sind sie unveränderlich und stellen dar, was ohne Aggregation oder Interpretation passiert ist.

[!DNL Intelligent Services] Verwenden Sie mehrere Schlüsselfelder in diesem Schema, um Einblicke aus Ihren Marketing-Ereignissen-Daten zu generieren, die sich alle auf der Stammebene befinden und erweitert werden, um die erforderlichen Unterfelder anzuzeigen.

![](./images/data-preparation/schema-expansion.gif)

Wie alle XDM-Schema ist auch das CEE-Mixin erweiterbar. Mit anderen Worten, dem CEE-Mixin können zusätzliche Felder hinzugefügt werden, und bei Bedarf können verschiedene Varianten in mehreren Schemas enthalten sein.

Ein vollständiges Beispiel des Mixins finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Darüber hinaus können Sie die folgende [JSON-Datei](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) als Beispiel für die Strukturierung von Daten entsprechend dem CEE-Schema Ansicht und kopieren. In beiden Beispielen erfahren Sie mehr über die im folgenden Abschnitt beschriebenen Schlüsselfelder, um zu ermitteln, wie Sie dem Schema Ihre eigenen Daten zuordnen können.

## Schlüsselfelder

Es gibt mehrere Schlüsselfelder innerhalb des CEE-Mixins, die genutzt werden sollten, um nützliche Einblicke [!DNL Intelligent Services] zu generieren. In diesem Abschnitt werden der Verwendungsfall und die erwarteten Daten für diese Felder beschrieben und Links zur Referenzdokumentation für weitere Beispiele bereitgestellt.

### Obligatorische Felder

Die Verwendung aller Schlüsselfelder wird dringend empfohlen, es gibt jedoch zwei Felder, die **erforderlich** sind, [!DNL Intelligent Services] um zu funktionieren:

* [Ein primäres Identitätsfeld](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:Kanal](#channel) (nur für Attribution AIS obligatorisch)

#### Primär {#identity}

Eines der Felder in Ihrem Schema muss als primäres Identitätsfeld festgelegt werden, mit dem jede Instanz von Zeitreihendaten mit einer Einzelperson verknüpft werden [!DNL Intelligent Services] kann.

Sie müssen das beste Feld als primäre Identität basierend auf der Quelle und der Art Ihrer Daten festlegen. Ein Identitätsfeld muss einen **Identitäts-Namensraum** enthalten, der den Typ der Identitätsdaten angibt, den das Feld als Wert erwartet. Zu den gültigen Namensräumen gehören:

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(für Adobe Audience Manager-IDs)
* &quot;aaid&quot;(für Adobe Analytics-IDs)

Wenn Sie sich nicht sicher sind, welches Feld Sie als primäre Identität verwenden sollten, wenden Sie sich an Adobe Consulting Services, um die beste Lösung zu finden.

#### xdm:timestamp {#timestamp}

Dieses Feld gibt den Zeitpunkt an, zu dem das Ereignis aufgetreten ist. Dieser Wert muss als Zeichenfolge gemäß ISO 8601 angegeben werden.

#### xdm:channel {#channel}

>[!NOTE]
>
>Dieses Feld ist nur bei Verwendung von Attribution AI obligatorisch.

Dieses Feld stellt den Marketing-Kanal im Zusammenhang mit dem ExperienceEvent dar. Das Feld enthält Informationen zum Typ des Kanals, Medientyp und Standort.

![](./images/data-preparation/channel.png)

**Beispiel-Schema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern `xdm:channel`finden Sie in der [Experience Kanal Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) -Spezifikation. Beispielzuordnungen finden Sie in der [Tabelle unten](#example-channels).

##### Example channel mappings {#example-channels}

The following table provides some examples of marketing channels mapped to the `xdm:channel` schema:

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Paid Search | https:/<span>/ns.adobe.com/xdm/Kanal-types/search | paid | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | earned | clicks |
| Anzeigen | https:/<span>/ns.adobe.com/xdm/channel-types/display | paid | clicks |
| E-Mail  | https:/<span>/ns.adobe.com/xdm/channel-types/email | paid | clicks |
| Internal Referrer | https:/<span>/ns.adobe.com/xdm/channel-types/direct | owned | clicks |
| Display ViewThrough | https:/<span>/ns.adobe.com/xdm/channel-types/display | paid | impressions |
| QR-Codeumleitung | https:/<span>/ns.adobe.com/xdm/Kanal-types/direct | besetzt | clicks |
| Mobile | https:/<span>/ns.adobe.com/xdm/Kanal-types/mobile | besetzt | clicks |

### Empfohlene Felder

Die übrigen Schlüsselfelder werden in diesem Abschnitt beschrieben. Diese Felder sind zwar nicht unbedingt erforderlich, um zu funktionieren, es wird jedoch dringend empfohlen, möglichst viele davon zu verwenden, um tiefer gehende Einblicke zu erhalten. [!DNL Intelligent Services]

#### xdm:productListItems

Dieses Feld enthält eine Reihe von Artikeln, die die von einem Kunden ausgewählten Produkte darstellen, einschließlich der Produkt-SKU, des Namens, des Preises und der Menge.

![](./images/data-preparation/productListItems.png)

**Beispiel-Schema**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern `xdm:productListItems`finden Sie in der [Commerce-Details-Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) -Spezifikation.

#### xdm:commerce

Dieses Feld enthält handelsspezifische Informationen zum ExperienceEvent, einschließlich Bestellnummer und Zahlungsinformationen.

![](./images/data-preparation/commerce.png)

**Beispiel-Schema**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern `xdm:commerce`finden Sie in der [Commerce-Details-Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) -Spezifikation.

#### xdm:web

Dieses Feld enthält Webdetails zum ExperienceEvent, wie Interaktion, Seitendetails und Werber.

![](./images/data-preparation/web.png)

**Beispiel-Schema**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern `xdm:productListItems`finden Sie in der Spezifikation des [ExperienceEvent-Webdetails-Schemas](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) .

#### xdm:marketing

Dieses Feld enthält Informationen zu Marketing-Aktivitäten, die mit dem Touchpoint aktiv sind.

![](./images/data-preparation/marketing.png)

**Beispiel-Schema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Vollständige Informationen zu jedem der erforderlichen Unterfelder finden Sie `xdm:productListItems`in der [Marketing-Sechsfachspezifikation](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) .

## Zuordnung und Erfassung von Daten (#mapping)

Sobald Sie festgestellt haben, ob Ihre Marketing-Ereignis-Daten dem CEE-Schema zugeordnet werden können, müssen Sie als Nächstes ermitteln, welche Daten Sie in dieses  einbeziehen [!DNL Intelligent Services]. Alle in verwendeten Verlaufsdaten [!DNL Intelligent Services] müssen innerhalb des Mindestzeitraums von vier Monaten an Daten liegen, zuzüglich der Anzahl der Tage, die als Lookback-Zeitraum gedacht sind.

Wenden Sie sich nach der Entscheidung über den zu sendenden Datenbereich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und sie in den Dienst zu integrieren.

Wenn Sie ein [!DNL Adobe Experience Platform] Abonnement haben und die Daten selbst zuordnen und erfassen möchten, führen Sie die im folgenden Abschnitt beschriebenen Schritte aus.

### Verwenden von Adobe Experience Platform

>[!NOTE]
>
>Die folgenden Schritte erfordern ein Abonnement zur Experience Platform. Wenn Sie keinen Zugriff auf die Plattform haben, fahren Sie mit dem Abschnitt [Nächste Schritte](#next-steps) fort.

In diesem Abschnitt wird der Arbeitsablauf für die Zuordnung und Einbindung von Daten in die Experience Platform zur Verwendung in [!DNL Intelligent Services]erläutert, einschließlich Links zu Schulungen für detaillierte Schritte.

#### Erstellen eines CEE-Schemas und eines Datasets

Wenn Sie bereit sind, Ihre Daten für die Erfassung vorzubereiten, müssen Sie zunächst ein neues XDM-Schema erstellen, das das CEE-Mixin verwendet. Die folgenden Lernprogramme erläutern die Erstellung eines neuen Schemas in der Benutzeroberfläche oder API:

* [Erstellen eines Schemas in der Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md)
* [Erstellen eines Schemas in der API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Die oben stehenden Lernprogramme folgen einem allgemeinen Arbeitsablauf zum Erstellen eines Schemas. Bei der Auswahl einer Klasse für das Schema müssen Sie die **XDM ExperienceEvent-Klasse** verwenden. Nachdem diese Klasse ausgewählt wurde, können Sie das CEE-Mixin dem Schema hinzufügen.

Nachdem Sie das CEE-Mixin zum Schema hinzugefügt haben, können Sie je nach Bedarf weitere Mixins in Ihre Daten einfügen.

Nachdem Sie das Schema erstellt und gespeichert haben, können Sie auf der Grundlage dieses Schemas einen neuen Datensatz erstellen. Die folgenden Lernprogramme erläutern den Vorgang zum Erstellen eines neuen Datensatzes in der Benutzeroberfläche oder API:

* [Erstellen Sie ein Dataset in der Benutzeroberfläche](../catalog/datasets/user-guide.md#create) (zum Verwenden eines vorhandenen Schemas im Workflow)
* [Erstellen eines Datensatzes in der API](../catalog/datasets/create.md)

Nachdem der Datensatz erstellt wurde, können Sie ihn in der Benutzeroberfläche &quot;Plattform&quot;im Arbeitsbereich &quot; *[!UICONTROL Datensätze]* &quot;finden.

![](images/data-preparation/dataset-location.png)

#### hinzufügen eines primären Identitäts-Namensraum-Tags zum Dataset

>[!NOTE]
>
>In zukünftigen Versionen von [!DNL Intelligent Services] wird der [Adobe Experience Platform Identity Service](../identity-service/home.md) in die Kundenidentifizierungsfunktionen integriert. Die unten aufgeführten Schritte können sich daher ändern.

If you are bringing in data from [!DNL Adobe Audience Manager], [!DNL Adobe Analytics], or another external source, then you must add a `primaryIdentityNameSpace` tag to the dataset. This can be done by making a PATCH request to the Catalog Service API.

Wenn Sie Daten aus einer lokalen CSV-Datei aufnehmen, können Sie den nächsten Abschnitt über die [Zuordnung und Erfassung von Daten](#ingest)überspringen.

Before following along with the example API call below, see the [getting started section](../catalog/api/getting-started.md) in the Catalog developer guide for important information regarding required headers.

**API-Format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | The ID of the dataset you created previously. |

**Anfrage**

Depending on which source you are ingesting data from, you must provide appropriate `primaryIdentityNamespace` and `sourceConnectorId` tag values in the request payload.

The following request adds the appropriate tag values for Audience Manager:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["mcid"],
          "sourceConnectorId": ["audiencemanager"],
        }
      }'
```

The following request adds the appropriate tag values for Analytics:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["aaid"],
          "sourceConnectorId": ["analytics"],
        }
      }'
```

>[!NOTE]
>
>For more information on working with identity namespaces in Platform, see the [identity namespace overview](../identity-service/namespaces.md).

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des aktualisierten Datensatzes enthält. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

#### Map and ingest data {#ingest}

After creating a CEE schema and dataset, you can start mapping your data tables to the schema and ingest that data into Platform. See the tutorial on [mapping a CSV file to an XDM schema](../ingestion/tutorials/map-a-csv-file.md) for steps on how to perform this in the UI. You can use the following [sample JSON file](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) to test the ingestion process before using your own data.

Once a dataset has been populated, the same dataset can be used to ingest additional data files.

If your data is stored in a supported third-party application, you can also choose to create a [source connector](../sources/home.md) to ingest your marketing events data into [!DNL Platform] in real time.

## Nächste Schritte {#next-steps}

This document provided general guidance on preparing your data for use in [!DNL Intelligent Services]. Wenn Sie je nach Anwendungsfall weitere Beratung benötigen, wenden Sie sich bitte an den Adobe Consulting Support.

Nachdem Sie einen Datensatz mit Ihren Kundenerlebnisdaten ausgefüllt haben, können Sie [!DNL Intelligent Services] Einblicke generieren. Die ersten Schritte finden Sie in den folgenden Dokumenten:

* [Übersicht über Attribution AIS](./attribution-ai/overview.md)
* [Customer AI – Übersicht](./customer-ai/overview.md)
