---
title: Streaming-Quelle kaufen
description: Erfahren Sie, wie Sie eine Quellverbindung und einen Datenfluss erstellen, um Streaming-Daten aus Ihrer Shopify-Instanz in Adobe Experience Platform zu erfassen.
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: 4c83c08d-c744-4167-9e3b-ed9a995943f4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 3%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>Die [!DNL Shopify Streaming]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Adobe Experience Platform unterstützt die Erfassung von Daten aus Streaming-Anwendungen. Unterstützung für Streaming-Anbieter umfasst [!DNL Shopify].

## Voraussetzungen {#prerequisites}

Im folgenden Abschnitt werden die erforderlichen Schritte beschrieben, die vor Verwendung der [!DNL Shopify Streaming] -Quelle.

Sie müssen über gültige [!DNL Shopify] Partnerkonto, um eine Verbindung zum [!DNL Shopify] APIs. Wenn Sie noch kein Partnerkonto haben, registrieren Sie sich bitte über das [[!DNL Shopify] Partner-Dashboard](https://www.shopify.com/partners).

### Anwendung erstellen

Mit gültigen [!DNL Shopify] Partnerkonto verwenden, können Sie jetzt mit dem Partner-Dashboard fortfahren und Ihre App erstellen. Umfassende Schritte zum Erstellen Ihrer App in [!DNL Shopify], lesen Sie die [[!DNL Shopify] Handbuch zu den ersten Schritten](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Rufen Sie nach der Erstellung Ihrer App Ihre **Client-ID** und **Client-Geheimnis** von **Client-Anmeldeinformationen** des [!DNL Shopify] Partner-Dashboard. Die Client-ID und das Client-Geheimnis werden in den nächsten Schritten verwendet, um Ihren Autorisierungscode und Ihr Zugriffstoken abzurufen.

### Abrufen des Autorisierungscodes

Rufen Sie als Nächstes Ihren Autorisierungscode ab, indem Sie die `myshopify.com` URL in Ihren Browser sowie Abfragezeichenfolgen, die Ihren API-Schlüssel, Bereiche und den Umleitungs-URI definieren.

Das Format dieser URL lautet wie folgt:

**API-Format**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parameter | Beschreibung |
| --- | --- |
| `shop` | Ihre Subdomain `myshopify.com` URL. |
| `api_key` | Ihre [!DNL Shopify] Client-ID. Sie können Ihre Client-ID aus der **Client-Anmeldeinformationen** des [!DNL Shopify] Partner-Dashboard. |
| `scopes` | Der Zugriffstyp, den Sie definieren möchten. Sie können beispielsweise Bereiche wie `scope=write_orders,read_customers` um Berechtigungen zur Änderung von Bestellungen und zum Lesen von Kunden zu gewähren. |
| `redirect_uri` | Die URL für das Skript, das das Zugriffstoken generiert. |

**Anfrage**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Antwort**

Bei einer erfolgreichen Antwort wird Ihre Umleitungs-URL zurückgegeben, einschließlich des Autorisierungscodes, der zum Generieren Ihres Zugriffstokens erforderlich ist.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Zugriffstoken abrufen

Nachdem Sie nun Ihre Client-ID, Ihr Client-Geheimnis und Ihren Autorisierungscode haben, können Sie Ihr Zugriffstoken abrufen. Um Ihr Zugriffstoken abzurufen, stellen Sie eine POST-Anfrage an die `myshopify.com` URL beim Anhängen dieser URL an [!DNL Shopify's] API-Endpunkt: `/admin/oauth/access_token`.

**API-Format**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Anfrage**

Die folgende Anfrage generiert ein Zugriffstoken für Ihre [!DNL Shopify] -Instanz.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden Ihr Zugriffstoken und die Berechtigungsbereiche zurückgegeben.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Webhook für Streaming erstellen [!DNL Shopify] data {#webhook}

Webhooks ermöglichen es Anwendungen, mit Ihrer [!DNL Shopify] Daten oder eine Aktion ausführen, nachdem ein bestimmtes Ereignis in einem Shop auftritt. Streaming [!DNL Shopify] -Daten in die Experience Platform übertragen, können Webhooks verwendet werden, um den HTTP-Endpunkt und die Themen für die Anmeldung zu definieren.

**Anfrage**

Die folgende Anfrage erstellt einen Webhook für Ihre [!DNL Shopify Streaming] Daten.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| Parameter | Beschreibung |
| --- | --- | 
| `webhook.address` | Der HTTP-Endpunkt, an den Streaming-Nachrichten gesendet werden. |
| `webhook.topic` | Das Thema Ihres Webhook-Abonnements. Weitere Informationen finden Sie im Abschnitt [[!DNL Shopify] Webhook-Ereignisthemen-Handbuch](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | Das Format Ihrer Daten. |

**Antwort**

Eine erfolgreiche Antwort gibt Informationen zu Ihrem Webhook zurück, einschließlich der zugehörigen `id`, Adresse und andere Metadateninformationen.

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### Einschränkungen {#limitations}

Im Folgenden finden Sie eine Liste bekannter Einschränkungen, auf die Sie bei der Verwendung von Webhooks mit dem [!DNL Shopify Streaming] -Quelle.

* Es ist nicht garantiert, dass Sie die Reihenfolge der verschiedenen Themen für dieselbe Ressource festlegen können. Beispielsweise ist es möglich, dass ein `products/update` Webhook wird vor einem `products/create` Webhook.
* Sie können Ihren Webhook so einrichten, dass Webhook-Ereignisse mindestens einmal an einen Endpunkt gesendet werden. Das bedeutet, dass ein Endpunkt dasselbe Ereignis mehrmals empfangen kann. Sie können nach doppelten Webhook-Ereignissen suchen, indem Sie die `X-Shopify-Webhook-Id` -Kopfzeile zu vorherigen Ereignissen.
* [!DNL Shopify] behandelt HTTP 2xx-Statusantworten als erfolgreiche Benachrichtigungen. Alle anderen Status-Code-Antworten werden als Fehler betrachtet. [!DNL Shopify] bietet einen Wiederholungsmechanismus für fehlgeschlagene Webhook-Benachrichtigungen. Wenn **keine Antwort nach fünf Sekunden Wartezeit**, [!DNL Shopify] wiederholt die Verbindung **19-mal** im Laufe der nächsten **48 Stunden**. Wenn bis zum Ende des Wiederholungszeitraums immer noch keine Antworten vorhanden sind, dann [!DNL Shopify] löscht den Webhook.

## Nächste Schritte

In den folgenden Tutorials erfahren Sie, wie Sie Ihre [!DNL Shopify Streaming] -Quelle zur Experience Platform mithilfe der API und der Benutzeroberfläche:

* [Erstellen einer Shopify Streaming-Quellverbindung und eines Datenflusses mithilfe der Flow Service-API](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Erstellen einer Shopify Streaming-Quellverbindung und eines Datenflusses in der Benutzeroberfläche](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
