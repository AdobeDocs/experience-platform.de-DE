---
keywords: Experience Platform;home;popular topics;ecommerce;eCommerce
solution: Experience Platform
title: Durchsuchen einer E-Commerce-Verbindung mit der Flow Service API
topic: overview
description: In diesem Lernprogramm wird die Flow Service API verwendet, um E-Commerce-Verbindungen zu untersuchen.
translation-type: tm+mt
source-git-commit: 4696bcb17427bb50549a315294baf7fbd87ac01d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 25%

---


# Durchsuchen einer E-Commerce-Verbindung mit der [!DNL Flow Service] API

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um eine **[!UICONTROL E-Commerce]** -Verbindung eines Drittanbieters zu untersuchen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect to an **[!UICONTROL eCommerce]** connection using the [!DNL Flow Service] API.

### Verbindungs-ID abrufen

Um Ihre **[!UICONTROL eCommerce]** -Verbindung mit [!DNL Platform] APIs zu untersuchen, müssen Sie über eine gültige Verbindungs-ID verfügen. Wenn Sie noch keine Verbindung für die **[!UICONTROL eCommerce]** -Verbindung haben, mit der Sie arbeiten möchten, können Sie eine Verbindung über das folgende Lernprogramm erstellen:

* [Shopify](../create/ecommerce/shopify.md)

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Ihre Datentabellen

Mithilfe Ihrer **[!UICONTROL eCommerce]** -Verbindungs-ID können Sie Ihre Datentabellen untersuchen, indem Sie GET anfordern. Verwenden Sie den folgenden Aufruf, um den Pfad der Tabelle zu finden, die Sie überprüfen oder in die Sie eingehen möchten [!DNL Platform].

**API-Format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONNECTION_ID}` | Ihre **[!UICONTROL eCommerce]** -Verbindungs-ID. |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Tabellenarray aus Ihrer **[!UICONTROL eCommerce]** -Verbindung zurück. Suchen Sie nach der Tabelle, die Sie in Ihre [!DNL Platform] Eigenschaft aufnehmen möchten, `path` und notieren Sie sich diese, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect der Tabellenstruktur

Um die Tabellenstruktur über Ihre **[!UICONTROL eCommerce]** -Verbindung zu überprüfen, führen Sie eine GET durch und geben Sie dabei den Tabellenpfad innerhalb eines `object` Abfrage-Parameters an.

**API-Format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die Verbindungs-ID Ihrer **[!UICONTROL eCommerce]** -Verbindung. |
| `{TABLE_PATH}` | Der Pfad einer Tabelle in Ihrer **[!UICONTROL E-Commerce]** -Verbindung. |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der angegebenen Tabelle zurück. Details zu den einzelnen Tabellenspalten befinden sich innerhalb der Elemente des `columns` Arrays.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## Nächste Schritte

Indem Sie diesem Tutorial folgen, haben Sie Ihre **[!UICONTROL eCommerce]** -Verbindung erkundet, den Pfad der Tabelle gefunden, in die Sie eingehen möchten, [!DNL Platform]und Informationen zu ihrer Struktur erhalten. Sie können diese Informationen im nächsten Lernprogramm verwenden, um E-Commerce-Daten zu [sammeln und in Plattform](../collect/ecommerce.md)zu übertragen.
