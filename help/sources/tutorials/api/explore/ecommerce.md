---
keywords: Experience Platform; Startseite; beliebte Themen; E-Commerce; eCommerce
solution: Experience Platform
title: Erkunden einer eCommerce-Verbindung mithilfe der Flow Service-API
topic-legacy: overview
description: In diesem Tutorial wird die Flow Service-API verwendet, um E-Commerce-Verbindungen zu untersuchen.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 35%

---

# Erkunden Sie eine eCommerce-Verbindung mit der [!DNL Flow Service]-API.

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform zu sammeln und zu zentralisieren. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen verbunden werden können.

In diesem Tutorial wird die [!DNL Flow Service]-API verwendet, um eine Drittanbieter-Verbindung zu untersuchen **[!UICONTROL eCommerce]**.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Sources]](../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu einer **[!UICONTROL eCommerce]**-Verbindung herstellen zu können.

### Verbindung-ID abrufen

Um Ihre **[!UICONTROL eCommerce]**-Verbindung mit [!DNL Platform]-APIs zu untersuchen, müssen Sie über eine gültige Verbindungs-ID verfügen. Wenn Sie noch keine Verbindung für die **[!UICONTROL eCommerce]**-Verbindung haben, mit der Sie arbeiten möchten, können Sie eine über das folgende Tutorial erstellen:

* [Shopify](../create/ecommerce/shopify.md)

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Datentabellen durchsuchen

Mithilfe Ihrer Verbindungs-ID **[!UICONTROL eCommerce]** können Sie Ihre Datentabellen durch Ausführen von GET-Anfragen untersuchen. Verwenden Sie den folgenden Aufruf, um den Pfad der Tabelle zu finden, die Sie untersuchen oder in [!DNL Platform] aufnehmen möchten.

**API-Format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONNECTION_ID}` | Ihre **[!UICONTROL eCommerce]**-Verbindungs-ID. |

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

Eine erfolgreiche Antwort gibt ein Array von Tabellen aus Ihrer **[!UICONTROL eCommerce]**-Verbindung zurück. Suchen Sie die Tabelle, die Sie in [!DNL Platform] einbinden möchten, und notieren Sie sich deren `path`-Eigenschaft, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

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

## Tabellenstruktur Inspect

Um die Tabellenstruktur über Ihre **[!UICONTROL eCommerce]**-Verbindung zu überprüfen, führen Sie eine GET-Anfrage aus und geben Sie dabei den Pfad einer Tabelle innerhalb eines `object`-Abfrageparameters an.

**API-Format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die Verbindungs-ID Ihrer **[!UICONTROL eCommerce]**-Verbindung. |
| `{TABLE_PATH}` | Der Pfad einer Tabelle innerhalb Ihrer **[!UICONTROL eCommerce]**-Verbindung. |

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

Eine erfolgreiche Antwort gibt die Struktur der angegebenen Tabelle zurück. Details zu den einzelnen Spalten der Tabelle befinden sich in Elementen des `columns`-Arrays.

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

In diesem Tutorial haben Sie Ihre **[!UICONTROL eCommerce]**-Verbindung untersucht, den Pfad der Tabelle gefunden, die Sie in [!DNL Platform] aufnehmen möchten, und Informationen zur Struktur erhalten. Sie können diese Informationen im nächsten Tutorial zu [erfassen und in Platform](../collect/ecommerce.md) importieren.
