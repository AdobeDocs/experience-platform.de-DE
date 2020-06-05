---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Daten für die Verwendung in Intelligent Services vorbereiten
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 1%

---


# Daten für die Verwendung in Intelligent Services vorbereiten

Damit Intelligent Services Einblicke aus den Daten Ihrer Marketing-Ereignis erhalten kann, müssen die Daten semantisch erweitert und in einer Standardstruktur gepflegt werden. Intelligente Dienste nutzen Experience Data Model-(XDM-)Schema, um dies zu erreichen. Insbesondere müssen alle in Intelligent Services verwendeten Datensätze mit dem XDM-Schema von **Consumer ExperienceEvent (CEE)** übereinstimmen.

In diesem Dokument erhalten Sie allgemeine Anleitungen zur Zuordnung Ihrer Marketing-Ereignis-Daten aus mehreren Kanälen zu diesem Schema. In diesen Anleitungen werden Informationen zu wichtigen Feldern im Schema zusammengefasst, die Ihnen bei der Bestimmung helfen, wie Sie Ihre Daten effektiv der Struktur zuordnen können.

## Das CEE-Schema

Das Consumer ExperienceEvent-Schema beschreibt das Verhalten eines Individuums in Bezug auf digitale Marketing-Ereignis (Web oder Mobil) sowie Online- oder Offline-Commerce-Aktivitäten. Die Verwendung dieses Schemas ist für Intelligent Services aufgrund seiner semantisch definierten Felder (Spalten) erforderlich, wodurch unbekannte Namen vermieden werden, die sonst die Daten weniger eindeutig machen würden.

Intelligent Services nutzt mehrere Schlüsselfelder in diesem Schema, um Erkenntnisse aus Ihren Marketing-Ereignissen-Daten zu generieren. Diese können alle auf der Stammebene gefunden und erweitert werden, um die erforderlichen Unterfelder anzuzeigen.

![](./images/data-preparation/schema-expansion.gif)

Wie alle XDM-Schema ist auch das CEE-Mixin erweiterbar. Mit anderen Worten, dem CEE-Mixin können zusätzliche Felder hinzugefügt werden, und bei Bedarf können verschiedene Varianten in mehreren Schemas enthalten sein.

Ein vollständiges Beispiel des Mixins finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)und sollten als Referenz für die Schlüsselfelder verwendet werden, die im folgenden Abschnitt beschrieben werden.

## Schlüsselfelder

In den folgenden Abschnitten werden die Schlüsselfelder im CEE-Mixin hervorgehoben, die genutzt werden sollten, damit Intelligent Services nützliche Einblicke generieren kann, einschließlich Beschreibungen und Links zur Referenzdokumentation für weitere Beispiele.

>[!IMPORTANT] Das `xdm:channel` Feld (im ersten Abschnitt unten erläutert) ist **erforderlich** , damit Attribution AI mit Ihren Daten arbeiten kann, während Customer AI keine Pflichtfelder hat. Alle anderen Schlüsselfelder werden dringend empfohlen, jedoch nicht obligatorisch.

### xdm:Kanal

Dieses Feld stellt den Marketing-Kanal im Zusammenhang mit dem ExperienceEvent dar. Das Feld enthält Informationen zum Typ des Kanals, Medientyp und Standort. **Dieses Feld _muss_bereitgestellt werden, damit Attribution AI mit Ihren Daten** arbeiten kann.

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

#### Beispielzuordnungen für Kanal {#example-channels}

Die folgende Tabelle enthält einige Beispiele für Marketing-Kanal, die dem `xdm:channel` Schema zugeordnet sind:

| Kanal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Paid Search | https:/<span>/ns.adobe.com/xdm/Kanal-types/search | bezahlt | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/Kanal-types/social | verdient | clicks |
| Anzeigen | https:/<span>/ns.adobe.com/xdm/Kanal-types/display | bezahlt | clicks |
| E-Mail  | https:/<span>/ns.adobe.com/xdm/Kanal-types/email | bezahlt | clicks |
| Interner Werber | https:/<span>/ns.adobe.com/xdm/Kanal-types/direct | besetzt | clicks |
| Display ViewThrough | https:/<span>/ns.adobe.com/xdm/Kanal-types/display | bezahlt | impressions |
| QR-Codeumleitung | https:/<span>/ns.adobe.com/xdm/Kanal-types/direct | besetzt | clicks |
| Mobil | https:/<span>/ns.adobe.com/xdm/Kanal-types/mobile | besetzt | clicks |

### xdm:productListItems

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

### xdm:commerce

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

### xdm:web

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

### xdm:marketing

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

## Zuordnung und Erfassung von Daten

Sobald Sie festgestellt haben, ob Ihre Marketing-Ereignis-Daten dem CEE-Schema zugeordnet werden können, müssen Sie als Nächstes ermitteln, welche Daten Sie in Intelligent Services einführen möchten. Alle in Intelligent Services verwendeten Verlaufsdaten müssen innerhalb des Mindestzeitraums von vier Monaten an Daten liegen, zuzüglich der Anzahl der Tage, die als Lookback-Zeitraum gedacht sind.

Nachdem Sie den zu sendenden Datenbereich festgelegt haben, wenden Sie sich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und sie in den Dienst zu integrieren.

Wenn Sie ein [!DNL Adobe Experience Platform] Abonnement haben und die Daten selbst zuordnen und erfassen möchten, führen Sie die im folgenden Abschnitt beschriebenen Schritte aus.

### Verwenden der Adobe Experience Platform

>[!NOTE] Die folgenden Schritte erfordern ein Abonnement zu Experience Platform. Wenn Sie keinen Zugriff auf die Plattform haben, fahren Sie mit dem Abschnitt [Nächste Schritte](#next-steps) fort.

In diesem Abschnitt wird der Arbeitsablauf für die Zuordnung und Erfassung von Daten zur Experience Platform zur Verwendung in Intelligent Services beschrieben, einschließlich Links zu Schulungen für detaillierte Schritte.

#### Erstellen eines CEE-Schemas und eines Datasets

Wenn Sie bereit sind, Ihre Daten für die Erfassung vorzubereiten, müssen Sie zunächst ein neues XDM-Schema erstellen, das das CEE-Mixin verwendet. Die folgenden Lernprogramme erläutern die Erstellung eines neuen Schemas in der Benutzeroberfläche oder API:

* [Erstellen eines Schemas in der Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md)
* [Erstellen eines Schemas in der API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Die oben stehenden Lernprogramme folgen einem allgemeinen Arbeitsablauf zum Erstellen eines Schemas. Bei der Auswahl einer Klasse für das Schema müssen Sie die **XDM ExperienceEvent-Klasse** verwenden. Nachdem diese Klasse ausgewählt wurde, können Sie das CEE-Mixin dem Schema hinzufügen.

Nachdem Sie das CEE-Mixin zum Schema hinzugefügt haben, können Sie je nach Bedarf weitere Mixins in Ihre Daten einfügen.

Nachdem Sie das Schema erstellt und gespeichert haben, können Sie auf der Grundlage dieses Schemas einen neuen Datensatz erstellen. Die folgenden Lernprogramme erläutern den Vorgang zum Erstellen eines neuen Datensatzes in der Benutzeroberfläche oder API:

* [Erstellen Sie ein Dataset in der Benutzeroberfläche](../catalog/datasets/user-guide.md#create) (zum Verwenden eines vorhandenen Schemas im Workflow)
* [Erstellen eines Datensatzes in der API](../catalog/datasets/create.md)

#### Hinzufügen eines primären Identitäts-Namensraum-Tags zum Dataset

Wenn Sie Daten aus [!DNL Adobe Audience Manager], [!DNL Adobe Analytics]oder einer anderen externen Quelle einreichen, müssen Sie dem Datensatz ein `primaryIdentityNameSpace` -Tag hinzufügen. Dies kann durch eine PATCH-Anforderung an die Katalogdienst-API erfolgen.

Wenn Sie Daten aus einer lokalen CSV-Datei aufnehmen, können Sie den nächsten Abschnitt über die [Zuordnung und Erfassung von Daten](#ingest)überspringen.

Bevor Sie dem Beispiel-API-Aufruf unten folgen, finden Sie im Abschnitt [&quot;](../catalog/api/getting-started.md) Erste Schritte&quot;im Katalog-Entwicklerhandbuch wichtige Informationen zu den erforderlichen Kopfzeilen.

**API-Format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Die ID des zuvor erstellten Datensatzes. |

**Anfrage**

Je nachdem, aus welcher Quelle Sie Daten abrufen, müssen Sie entsprechende `primaryIdentityNamespace` und `sourceConnectorId` Tag-Werte in der Anforderungsnutzlast angeben.

Mit der folgenden Anforderung werden die entsprechenden Tag-Werte für Audience Manager hinzugefügt:

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

Die folgende Anforderung fügt die entsprechenden Tag-Werte für Analytics hinzu:

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

>[!NOTE] Weitere Informationen zum Arbeiten mit Identitäts-Namensräumen in Platform finden Sie in der Übersicht über den [Identitäts-Namensraum](../identity-service/namespaces.md).

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des aktualisierten Datensatzes enthält. Diese ID sollte mit der in der PATCH-Anforderung gesendeten ID übereinstimmen.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

#### Daten zuordnen und erfassen {#ingest}

Nachdem Sie ein CEE-Schema und einen Dataset erstellt haben, können Sie Ihre Datentabellen dem Schema zuordnen und diese Daten in Platform erfassen. Anweisungen dazu, wie Sie dies in der Benutzeroberfläche durchführen, finden Sie im Lernprogramm zum [Zuordnen einer CSV-Datei zu einem XDM-Schema](../ingestion/tutorials/map-a-csv-file.md) . Nachdem ein Datensatz gefüllt wurde, kann derselbe Datensatz zum Erfassen zusätzlicher Datendateien verwendet werden.

Wenn Ihre Daten in einer unterstützten Drittanbieteranwendung gespeichert werden, können Sie auch einen [Quellanschluss](../sources/home.md) erstellen, um Ihre Marketing-Ereignis-Daten in Echtzeit in Platform zu erfassen.

## Nächste Schritte {#next-steps}

Dieses Dokument enthält allgemeine Anleitungen zum Vorbereiten Ihrer Daten für die Verwendung in Intelligent Services. Wenn Sie je nach Anwendungsfall weitere Beratung benötigen, wenden Sie sich bitte an den Adobe Consulting Support.

Nachdem Sie einen Datensatz mit Ihren Kundenerlebnisdaten gefüllt haben, können Sie mithilfe von Intelligent Services Erkenntnisse generieren. Die ersten Schritte finden Sie in den folgenden Dokumenten:

* [Übersicht über die Zuordnungs-AI](./attribution-ai/overview.md)
* [Customer AI – Übersicht](./customer-ai/overview.md)
