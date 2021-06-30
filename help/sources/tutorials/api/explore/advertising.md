---
keywords: Experience Platform; Startseite; beliebte Themen; Werbesystem; Werbesystem
solution: Experience Platform
title: Erkunden eines Werbesystems mithilfe der Flow Service-API
topic-legacy: overview
description: Mit Flow Service werden Kundendaten aus verschiedenen Quellen in Adobe Experience Platform erfasst und zentralisiert. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen verbunden werden können. In diesem Tutorial wird die Flow Service-API verwendet, um Werbetechnologien zu untersuchen.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 8aa8dfcc4f8a36d0898a9cc079bd98b89e3589a1
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 11%

---

# Erkunden Sie ein Werbesystem mit der [!DNL Flow Service]-API.

Nachdem eine Basisverbindung erstellt wurde, können Sie jetzt die eindeutige Kennung der Basisverbindung verwenden, um die Datenstruktur und den Inhalt Ihrer Quelle zu navigieren und zu untersuchen. Auf diese Weise können Sie bestimmte Elemente sowie ihre jeweiligen Datentypen und Formate identifizieren, bevor Sie einen Datenfluss erstellen und ihn an Adobe Experience Platform übermitteln.

In diesem Tutorial wird die [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) verwendet. Erkundung von Werbesystemen.

## Erste Schritte

>[!IMPORTANT]

Für dieses Tutorial benötigen Sie die eindeutige Basis-Verbindungs-ID für Ihre Werbequelle. Wenn Sie diese ID nicht haben, lesen Sie das Tutorial zum Verbinden einer Werbequelle mit Platform](../../api/create/advertising/ads.md) .[

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu einem Werbesystem herstellen zu können.

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../landing/api-guide.md).

## Datentabellen durchsuchen

Mithilfe der Basisverbindung für Ihr Werbesystem können Sie Ihre Datentabellen durch Ausführung von GET-Anfragen untersuchen. Verwenden Sie den folgenden Aufruf, um den Pfad der Tabelle zu finden, die Sie untersuchen oder in [!DNL Platform] aufnehmen möchten.

**API-Format**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Kennung der Basisverbindung für Ihr Werbesystem. |

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort ist eine Reihe von Tabellen von zu Ihrem Werbesystem. Suchen Sie die Tabelle, die Sie in [!DNL Platform] einbinden möchten, und notieren Sie sich deren `path`-Eigenschaft, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Tabellenstruktur Inspect

Um die Tabellenstruktur in Ihrem Werbesystem zu überprüfen, führen Sie eine GET-Anfrage aus und geben Sie dabei den Pfad einer Tabelle als Abfrageparameter an.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Verbindungs-ID für Ihr Werbesystem. |
| `{TABLE_PATH}` | Der Pfad einer Tabelle in Ihrem Werbesystem. |

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur einer Tabelle zurück. Details zu den einzelnen Spalten der Tabelle befinden sich in Elementen des `columns`-Arrays.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## Nächste Schritte

In diesem Tutorial haben Sie Ihr Werbesystem durchsucht, den Pfad der Tabelle gefunden, die Sie in [!DNL Platform] einbringen möchten, und Informationen zu ihrer Struktur erhalten. Sie können diese Informationen im nächsten Tutorial zu [erfassen von Daten aus Ihrem Werbesystem und bringen sie in Platform](../collect/advertising.md).
