---
keywords: Experience Platform;Startseite;beliebte Themen;Zahlung
solution: Experience Platform
title: Erkunden eines Zahlungssystems mithilfe der Flow Service-API
description: In diesem Tutorial wird die Flow Service-API verwendet, um Zahlungsanwendungen zu untersuchen.
exl-id: 7d0231de-46c0-49df-8a10-aeb42a2c8822
source-git-commit: 104db777446b19fa9e3ea7538ae1dda6f51a00b1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 41%

---

# Erkunden eines Zahlungssystems mit der [!DNL Flow Service]-API

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform zu sammeln und zu zentralisieren. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Tutorial wird die [!DNL Flow Service]-API verwendet, um Zahlungsanwendungen zu untersuchen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um sich mithilfe der [!DNL Flow Service]-API erfolgreich mit einem Zahlungsprogramm verbinden zu können.

### Sammeln erforderlicher Anmeldedaten

Sie müssen über eine aktive Verbindung mit einem Zahlungsprogramm verfügen, um die Dateien und Dateistruktur Ihrer Quelle zu untersuchen. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Square]](../create/payments/square.md)
* [[!DNL Stripe]](../create/payments/stripe.md)

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* x-sandbox-name: `{SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Erkunden von Datentabellen

Mit der Verbindungs-ID für Ihr Zahlungssystem können Sie Ihre Datentabellen untersuchen, indem Sie GET-Anfragen ausführen. Verwenden Sie den folgenden Aufruf, um den Pfad der Tabelle zu finden, die Sie untersuchen oder in [!DNL Experience Platform] aufnehmen möchten.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID einer Verbindung der Zahlungsbasis. |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array von Tabellen aus Ihrem Zahlungssystem zurück. Suchen Sie die Tabelle, die Sie in [!DNL Experience Platform] importieren möchten, und notieren Sie sich ihre `path` Eigenschaft, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

```json
[
    {
        "type": "table",
        "name": "Stripe.Billing_Plans",
        "path": "Stripe.Billing_Plans",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Billing_Plans_Payment_Definition",
        "path": "Stripe.Billing_Plans_Payment_Definition",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Billing_Plans_Payment_Definition_Charge_Models",
        "path": "Stripe.Billing_Plans_Payment_Definition_Charge_Models",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Catalog_Products",
        "path": "Stripe.Catalog_Products",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Überprüfen der Tabellenstruktur

Um die Tabellenstruktur aus Ihrem Zahlungssystem zu überprüfen, führen Sie eine GET-Anfrage aus und geben Sie dabei den Tabellenpfad als Abfrageparameter an.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Die Verbindungs-ID Ihres Zahlungssystems. |
| `{TABLE_PATH}` | Der Pfad einer Tabelle innerhalb Ihres Zahlungssystems. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
                "name": "Product_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Product_Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Description",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Type",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## Nächste Schritte

In diesem Tutorial haben Sie Ihr Zahlungssystem erkundet, den Pfad der Tabelle gefunden, die Sie in [!DNL Experience Platform] aufnehmen möchten, und Informationen über dessen Struktur erhalten. Sie können diese Informationen im nächsten Tutorial verwenden[ um Daten aus Ihrem Zahlungssystem zu erfassen und in Experience Platform zu ](../collect/payments.md).
