---
keywords: Experience Platform; Startseite; beliebte Themen; Werbesystem; Werbesystem
solution: Experience Platform
title: Erkunden eines Werbesystems mithilfe der Flow Service-API
description: Mit Flow Service werden Kundendaten aus verschiedenen Quellen in Adobe Experience Platform erfasst und zentralisiert. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen verbunden werden können. In diesem Tutorial wird die Flow Service-API verwendet, um Werbetechnologien zu untersuchen.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 20%

---

# Erkunden Sie ein Werbesystem mit dem [!DNL Flow Service] API

Nachdem eine Basisverbindung erstellt wurde, können Sie jetzt die eindeutige Kennung der Basisverbindung verwenden, um die Datenstruktur und den Inhalt Ihrer Quelle zu navigieren und zu untersuchen. Auf diese Weise können Sie bestimmte Elemente sowie ihre jeweiligen Datentypen und Formate identifizieren, bevor Sie einen Datenfluss erstellen und ihn an Adobe Experience Platform übermitteln.

In diesem Tutorial wird die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) Erkundung von Werbesystemen.

## Erste Schritte

>[!IMPORTANT]
>
>Für dieses Tutorial benötigen Sie die eindeutige Basis-Verbindungs-ID für Ihre Werbequelle. Wenn Sie diese ID nicht haben, lesen Sie das Tutorial zu [Werbequelle mit Platform verbinden](../../api/create/advertising/ads.md) Tutorial.

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] API.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../landing/api-guide.md).

## Datentabellen durchsuchen

Mithilfe der Basisverbindung für Ihr Werbesystem können Sie Ihre Datentabellen durch Ausführung von GET-Anfragen untersuchen. Verwenden Sie den folgenden Aufruf, um den Pfad der Tabelle zu finden, die Sie untersuchen oder in die Sie aufnehmen möchten [!DNL Platform].

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort ist eine Reihe von Tabellen von zu Ihrem Werbesystem. Finden Sie den Tisch, den Sie mitbringen möchten [!DNL Platform] und nimmt Kenntnis von `path` -Eigenschaft, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur einer Tabelle zurück. Details zu den einzelnen Spalten der Tabelle befinden sich in Elementen der `columns` Array.

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

In diesem Tutorial haben Sie Ihr Werbesystem durchsucht und den Pfad der Tabelle gefunden, die Sie einführen möchten [!DNL Platform]und Informationen über seine Struktur erhalten. Sie können diese Informationen im nächsten Tutorial zu [Daten aus Ihrem Werbesystem erfassen und in Platform einbringen](../collect/advertising.md).
