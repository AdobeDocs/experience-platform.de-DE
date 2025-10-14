---
title: Shopify Streaming Source
description: Erfahren Sie, wie Sie eine Quellverbindung und einen Datenfluss erstellen, um Streaming-Daten von Ihrer Shopify-Instanz in Adobe Experience Platform aufzunehmen
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 3%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>Die [!DNL Shopify Streaming]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie &#x200B;](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Adobe Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Anwendungen. Unterstützung für Streaming-Anbieter umfasst [!DNL Shopify].

## Voraussetzungen {#prerequisites}

Im folgenden Abschnitt werden die Schritte beschrieben, die vor der Verwendung der [!DNL Shopify Streaming] ausgeführt werden müssen.

Sie müssen über ein gültiges [!DNL Shopify]-Partnerkonto verfügen, um eine Verbindung zu den [!DNL Shopify]-APIs herstellen zu können. Wenn Sie noch kein Partnerkonto haben, registrieren Sie sich bitte über das [[!DNL Shopify] Partner-Dashboard](https://www.shopify.com/partners).

### Erstellen des Programms

Mit einem gültigen [!DNL Shopify]-Partnerkonto können Sie jetzt fortfahren und Ihre App mithilfe des Partner-Dashboards erstellen. Eine ausführliche Anleitung zum Erstellen Ihres Programms in [!DNL Shopify] finden Sie im [[!DNL Shopify] Handbuch zu den ersten Schritten](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Rufen Sie nach der Erstellung Ihrer App Ihre **Client-ID** und **Client-**) auf der Registerkarte **Client-Anmeldeinformationen** des Dashboards [!DNL Shopify] Partner ab. Die Client-ID und das Client-Geheimnis werden in den nächsten Schritten zum Abrufen Ihres Autorisierungs-Codes und Zugriffs-Tokens verwendet.

### Abrufen des Autorisierungs-Codes

Rufen Sie anschließend Ihren Autorisierungs-Code ab, indem Sie die `myshopify.com`-URL Ihrer Domain in Ihren Browser eingeben und Abfragezeichenfolgen hinzufügen, die Ihren API-Schlüssel, die Bereiche und den Weiterleitungs-URI definieren.

Die URL hat folgendes Format:

**API-Format**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parameter | Beschreibung |
| --- | --- |
| `shop` | Ihre Subdomain `myshopify.com` URL. |
| `api_key` | Ihre [!DNL Shopify]-Client-ID. Sie können Ihre Client-ID über die Registerkarte **Client-Anmeldeinformationen** im Dashboard der [!DNL Shopify] abrufen. |
| `scopes` | Die Art des Zugriffs, den Sie definieren möchten. Sie können beispielsweise Bereiche als `scope=write_orders,read_customers` festlegen, um Berechtigungen zum Ändern von Bestellungen und zum Lesen von Kunden zuzulassen. |
| `redirect_uri` | Die URL für das Skript, das das Zugriffstoken generiert. |

**Anfrage**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Antwort**

Bei einer erfolgreichen Antwort wird Ihre Umleitungs-URL zurückgegeben, einschließlich des Autorisierungs-Codes, der zum Generieren Ihres Zugriffs-Tokens erforderlich ist.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Abrufen Ihres Zugriffs-Tokens

Nachdem Sie nun über Ihre Client-ID, Ihr Client-Geheimnis und Ihren Autorisierungs-Code verfügen, können Sie Ihr Zugriffs-Token abrufen. Um Ihr Zugriffs-Token abzurufen, stellen Sie eine POST-Anfrage an die `myshopify.com`-URL Ihrer Domain, während Sie diese URL an [!DNL Shopify's] API-Endpunkt anhängen: `/admin/oauth/access_token`.

**API-Format**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Anfrage**

Die folgende Anfrage generiert ein Zugriffstoken für Ihre [!DNL Shopify].

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

Bei einer erfolgreichen Antwort werden Ihr Zugriffstoken und Ihre Berechtigungsbereiche zurückgegeben.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Erstellen eines Webhooks für das Streaming von [!DNL Shopify] {#webhook}

Webhooks ermöglichen es Anwendungen, mit Ihren [!DNL Shopify]-Daten synchronisiert zu bleiben oder eine Aktion auszuführen, nachdem ein bestimmtes Ereignis in einem Shop stattgefunden hat. Für das Streaming von [!DNL Shopify] auf Experience Platform können Webhooks verwendet werden, um den HTTP-Endpunkt und die Themen für das Abonnement zu definieren.

**Anfrage**

Die folgende Anfrage erstellt einen Webhook für Ihre [!DNL Shopify Streaming].

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
| `webhook.topic` | Das Thema Ihres Webhook-Abonnements. Weitere Informationen finden Sie im [[!DNL Shopify] Handbuch zu Webhook-](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | Das Format Ihrer Daten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Informationen zu Ihrem Webhook zurückgegeben, einschließlich der entsprechenden `id`, Adresse und anderer Metadateninformationen.

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

Im Folgenden finden Sie eine Liste bekannter Einschränkungen, auf die Sie bei der Verwendung von Webhooks mit der [!DNL Shopify Streaming] stoßen können.

* Es ist nicht garantiert, dass Sie die Reihenfolge der Bereitstellung verschiedener Themen für dieselbe Ressource arrangieren können. Beispielsweise ist es möglich, dass ein `products/update` Webhook vor einem `products/create` Webhook bereitgestellt wird.
* Sie können Ihren Webhook so einstellen, dass Webhook-Ereignisse mindestens einmal an einen Endpunkt gesendet werden. Dies bedeutet, dass ein Endpunkt dasselbe Ereignis mehrmals erhalten kann. Sie können nach doppelten Webhook-Ereignissen suchen, indem Sie den `X-Shopify-Webhook-Id`-Header mit vorherigen Ereignissen vergleichen.
* [!DNL Shopify] behandelt HTTP-2xx-Statusantworten als erfolgreiche Benachrichtigungen. Alle anderen Status-Code-Antworten werden als Fehler betrachtet. [!DNL Shopify] bietet einen Mechanismus zum Wiederholen fehlgeschlagener Webhook-Benachrichtigungen. Wenn es **keine Antwort nach fünf Sekunden warten** versucht [!DNL Shopify] die Verbindung **19-mal** im Laufe der nächsten **48 Stunden**. Wenn bis zum Ende des Wiederholungszeitraums immer noch keine Antworten vorhanden sind, löscht [!DNL Shopify] den Webhook.

## Nächste Schritte

In den folgenden Tutorials wird beschrieben, wie Sie Ihre [!DNL Shopify Streaming] mithilfe der -API und der Benutzeroberfläche mit dem Experience Platform verbinden:

* [Erstellen einer Shopify Streaming-Quellverbindung und eines Datenflusses mithilfe der Flow Service-API](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Erstellen einer Shopify Streaming-Quellverbindung und eines Datenflusses in der Benutzeroberfläche](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
