---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Daten für die Verwendung in Intelligent Services vorbereiten
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 9905f0248fe88bac5194560318cf8eced32ba93c
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 1%

---


# Daten für die Verwendung in Intelligent Services vorbereiten

Damit Intelligent Services Einblicke aus den Daten Ihrer Marketing-Ereignis erhalten kann, müssen die Daten semantisch erweitert und in einer Standardstruktur gepflegt werden. Intelligente Dienste nutzen Experience Data Model-(XDM-)Schema, um dies zu erreichen. Insbesondere müssen alle in Intelligent Services verwendeten Datensätze mit dem XDM-Schema von **Consumer ExperienceEvent (CEE)** übereinstimmen.

In diesem Dokument erhalten Sie allgemeine Anleitungen zur Zuordnung Ihrer Marketing-Ereignis-Daten aus mehreren Kanälen zu diesem Schema. In diesen Anleitungen werden Informationen zu wichtigen Feldern im Schema zusammengefasst, die Ihnen bei der Bestimmung helfen, wie Sie Ihre Daten effektiv der Struktur zuordnen können.

## Workflow-Übersicht

Der Vorbereitungsprozess hängt davon ab, ob Ihre Daten in der Adobe Experience Platform oder extern gespeichert werden. In diesem Abschnitt werden die notwendigen Schritte zusammengefasst, die Sie in beiden Szenarien unternehmen müssen.

### Vorbereitung externer Daten

Wenn Ihre Daten außerhalb von gespeichert werden, führen Sie die folgenden Schritte aus [!DNL Experience Platform]:

1. Wenden Sie sich an Adobe Consulting Services, um Zugangsdaten für einen dedizierten Container der Azurblase-Datenspeicherung anzufordern.
1. Laden Sie Ihre Daten mit Ihren Zugriffsberechtigungen in den Blob-Container hoch.
1. Arbeiten Sie mit Adobe Consulting Services, um Ihre Daten dem [Consumer ExperienceEvent-Schema](#cee-schema) zuzuordnen und in Intelligent Services zu integrieren.

### [!DNL Experience Platform] Datenaufbereitung

Wenn Ihre Daten bereits in gespeichert sind, führen Sie [!DNL Platform]die folgenden Schritte aus:

1. Überprüfen Sie die Struktur des [Consumer ExperienceEvent-Schemas](#cee-schema) und stellen Sie fest, ob Ihre Daten Feldern zugeordnet werden können.
1. Wenden Sie sich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und sie in Intelligent Services zu erfassen, oder [befolgen Sie die Schritte in diesem Handbuch](#mapping) , wenn Sie die Daten selbst zuordnen möchten.

## Das CEE-Schema {#cee-schema}

Das Consumer ExperienceEvent-Schema beschreibt das Verhalten eines Individuums in Bezug auf digitale Marketing-Ereignis (Web oder Mobil) sowie Online- oder Offline-Commerce-Aktivitäten. Die Verwendung dieses Schemas ist für Intelligent Services aufgrund seiner semantisch definierten Felder (Spalten) erforderlich, wodurch unbekannte Namen vermieden werden, die sonst die Daten weniger eindeutig machen würden.

Das CEE-Schema erfasst wie alle XDM ExperienceEvent-Schema den zeitreihenbasierten Systemzustand, in dem ein Ereignis (oder eine Reihe von Ereignissen) aufgetreten ist, einschließlich des Zeitpunkts und der Identität des jeweiligen Objekts. Erfahrungs-Ereignisse sind Faktenberichte über das, was geschehen ist, und somit sind sie unveränderlich und stellen dar, was ohne Aggregation oder Interpretation passiert ist.

Intelligent Services nutzt mehrere Schlüsselfelder in diesem Schema, um Erkenntnisse aus Ihren Marketing-Ereignissen-Daten zu generieren. Diese können alle auf der Stammebene gefunden und erweitert werden, um die erforderlichen Unterfelder anzuzeigen.

![](./images/data-preparation/schema-expansion.gif)

Wie alle XDM-Schema ist auch das CEE-Mixin erweiterbar. Mit anderen Worten, dem CEE-Mixin können zusätzliche Felder hinzugefügt werden, und bei Bedarf können verschiedene Varianten in mehreren Schemas enthalten sein.

Ein vollständiges Beispiel des Mixins finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)und sollten als Referenz für die Schlüsselfelder verwendet werden, die im folgenden Abschnitt beschrieben werden.

## Schlüsselfelder

Es gibt mehrere Schlüsselfelder im CEE-Mixin, die genutzt werden sollten, damit Intelligent Services nützliche Einblicke generieren kann. In diesem Abschnitt werden der Verwendungsfall und die erwarteten Daten für diese Felder beschrieben und Links zur Referenzdokumentation für weitere Beispiele bereitgestellt.

### Obligatorische Felder

Die Verwendung aller Schlüsselfelder wird dringend empfohlen, es gibt jedoch zwei Felder, die **erforderlich** sind, damit Intelligent Services funktioniert:

* [Ein primäres Identitätsfeld](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:Kanal](#channel) (nur obligatorisch für Attribution AI)

#### Primär {#identity}

Eines der Felder in Ihrem Schema muss als primäres Identitätsfeld festgelegt werden, das es Intelligent Services ermöglicht, jede Instanz von Zeitreihendaten mit einer Person zu verknüpfen.

Sie müssen das beste Feld als primäre Identität basierend auf der Quelle und der Art Ihrer Daten festlegen. Ein Identitätsfeld muss einen **Identitäts-Namensraum** enthalten, der den Typ der Identitätsdaten angibt, den das Feld als Wert erwartet. Zu den gültigen Namensräumen gehören:

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(für Adobe Audience Manager-IDs)
* &quot;aaid&quot;(für Adobe Analytics IDs)

Wenn Sie sich nicht sicher sind, welches Feld Sie als primäre Identität verwenden sollten, wenden Sie sich an Adobe Consulting Services, um die beste Lösung zu finden.

#### xdm:timestamp {#timestamp}

Dieses Feld gibt den Zeitpunkt an, zu dem das Ereignis aufgetreten ist. Dieser Wert muss als Zeichenfolge gemäß ISO 8601 angegeben werden.

#### xdm:Kanal {#channel}

>[!NOTE] Dieses Feld ist nur bei Verwendung von Attribution AI obligatorisch.

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

##### Beispielzuordnungen für Kanal {#example-channels}

Die folgende Tabelle enthält einige Beispiele für Marketing-Kanal, die dem `xdm:channel` Schema zugeordnet sind:

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Paid Search | https:/<span>/ns.adobe.com/xdm/Kanal-types/search | bezahlt | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/Kanal-types/social | verdient | clicks |
| Anzeigen | https:/<span>/ns.adobe.com/xdm/Kanal-types/display | bezahlt | clicks |
| E-Mail  | https:/<span>/ns.adobe.com/xdm/Kanal-types/email | bezahlt | clicks |
| Interner Werber | https:/<span>/ns.adobe.com/xdm/Kanal-types/direct | besetzt | clicks |
| Display ViewThrough | https:/<span>/ns.adobe.com/xdm/Kanal-types/display | bezahlt | impressions |
| QR-Codeumleitung | https:/<span>/ns.adobe.com/xdm/Kanal-types/direct | besetzt | clicks |
| Mobil | https:/<span>/ns.adobe.com/xdm/Kanal-types/mobile | besetzt | clicks |

### Empfohlene Felder

Die übrigen Schlüsselfelder werden in diesem Abschnitt beschrieben. Diese Felder sind zwar nicht unbedingt erforderlich, damit Intelligent Services funktionieren kann, es wird jedoch dringend empfohlen, möglichst viele davon zu verwenden, um umfassendere Einblicke zu erhalten.

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

Sobald Sie festgestellt haben, ob Ihre Marketing-Ereignis-Daten dem CEE-Schema zugeordnet werden können, müssen Sie als Nächstes ermitteln, welche Daten Sie in Intelligent Services einführen möchten. Alle in Intelligent Services verwendeten Verlaufsdaten müssen innerhalb des Mindestzeitraums von vier Monaten an Daten liegen, zuzüglich der Anzahl der Tage, die als Lookback-Zeitraum gedacht sind.

Nachdem Sie den zu sendenden Datenbereich festgelegt haben, wenden Sie sich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und sie in den Dienst zu integrieren.

Wenn Sie ein [!DNL Adobe Experience Platform] Abonnement haben und die Daten selbst zuordnen und erfassen möchten, führen Sie die im folgenden Abschnitt beschriebenen Schritte aus.

### Adobe Experience Platform verwenden

>[!NOTE] Die folgenden Schritte erfordern ein Abonnement zur Experience Platform. Wenn Sie keinen Zugriff auf die Platform haben, fahren Sie mit den [nächsten Schritten](#next-steps) fort.

In diesem Abschnitt wird der Arbeitsablauf für die Zuordnung und Erfassung von Daten zur Experience Platform für die Verwendung in Intelligent Services beschrieben, einschließlich Links zu Schulungen für detaillierte Schritte.

#### Erstellen eines CEE-Schemas und eines Datasets

Wenn Sie bereit sind, Ihre Daten für die Erfassung vorzubereiten, müssen Sie zunächst ein neues XDM-Schema erstellen, das das CEE-Mixin verwendet. Die folgenden Lernprogramme erläutern die Erstellung eines neuen Schemas in der Benutzeroberfläche oder API:

* [Erstellen eines Schemas in der Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md)
* [Erstellen eines Schemas in der API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Die oben stehenden Lernprogramme folgen einem allgemeinen Arbeitsablauf zum Erstellen eines Schemas. Bei der Auswahl einer Klasse für das Schema müssen Sie die **XDM ExperienceEvent-Klasse** verwenden. Nachdem diese Klasse ausgewählt wurde, können Sie das CEE-Mixin dem Schema hinzufügen.

Nachdem Sie das CEE-Mixin zum Schema hinzugefügt haben, können Sie je nach Bedarf weitere Mixins in Ihre Daten einfügen.

Nachdem Sie das Schema erstellt und gespeichert haben, können Sie auf der Grundlage dieses Schemas einen neuen Datensatz erstellen. Die folgenden Lernprogramme erläutern den Vorgang zum Erstellen eines neuen Datensatzes in der Benutzeroberfläche oder API:

* [Erstellen Sie ein Dataset in der Benutzeroberfläche](../catalog/datasets/user-guide.md#create) (zum Verwenden eines vorhandenen Schemas im Workflow)
* [Erstellen eines Datensatzes in der API](../catalog/datasets/create.md)

Nachdem der Datensatz erstellt wurde, können Sie ihn in der Benutzeroberfläche &quot;Platform&quot;im Arbeitsbereich &quot; *[!UICONTROL Datensätze]* &quot;finden.

![](images/data-preparation/dataset-location.png)

#### Hinzufügen eines primären Identitäts-Namensraum-Tags zum Dataset

>[!NOTE] In zukünftigen Versionen von Intelligent Services wird der Identitätsdienst für [Adobe Experience Platformen](../identity-service/home.md) in die Kundenidentifizierungsfunktionen integriert. Die unten aufgeführten Schritte können sich daher ändern.

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

Die folgende Anforderung fügt die entsprechenden Tag-Werte für Audience Manager hinzu:

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

>[!NOTE] Weitere Informationen zum Arbeiten mit Identitäts-Namensräumen in der Platform finden Sie in der Übersicht über den [Identitäts-Namensraum](../identity-service/namespaces.md).

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des aktualisierten Datensatzes enthält. Diese ID sollte mit der in der PATCH-Anforderung gesendeten ID übereinstimmen.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

#### Daten zuordnen und erfassen {#ingest}

Nachdem Sie ein CEE-Schema und einen Dataset erstellt haben, können Sie Ihre Datentabellen dem Schema zuordnen und diese Daten in Platform erfassen. Anweisungen dazu, wie Sie dies in der Benutzeroberfläche durchführen, finden Sie im Lernprogramm zum [Zuordnen einer CSV-Datei zu einem XDM-Schema](../ingestion/tutorials/map-a-csv-file.md) . Nachdem ein Datensatz gefüllt wurde, kann derselbe Datensatz zum Erfassen zusätzlicher Datendateien verwendet werden.

Wenn Ihre Daten in einer unterstützten Drittanbieteranwendung gespeichert werden, können Sie auch einen [Quellanschluss](../sources/home.md) erstellen, um Ihre Marketing-Ereignis-Daten in Echtzeit in die Platform zu übernehmen.

## Nächste Schritte {#next-steps}

Dieses Dokument enthält allgemeine Anleitungen zum Vorbereiten Ihrer Daten für die Verwendung in Intelligent Services. Wenn Sie je nach Anwendungsfall weitere Beratung benötigen, wenden Sie sich bitte an den Adobe Consulting Support.

Nachdem Sie einen Datensatz mit Ihren Kundenerlebnisdaten gefüllt haben, können Sie mithilfe von Intelligent Services Erkenntnisse generieren. Die ersten Schritte finden Sie in den folgenden Dokumenten:

* [Übersicht über die Zuordnungs-AI](./attribution-ai/overview.md)
* [Customer AI – Übersicht](./customer-ai/overview.md)
