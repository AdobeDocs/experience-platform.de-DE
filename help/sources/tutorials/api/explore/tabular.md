---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; API; Erkunden; Flussdienst
title: Eine Tabellenquelle mithilfe der Flow Service-API durchsuchen
description: In diesem Tutorial wird die Flow Service-API verwendet, um den Inhalt und die Struktur einer tabellenbasierten Quelle zu untersuchen.
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: 3bdeec8284873b8d9368f833b24e9922ed489019
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 23%

---

# Datentabellen mithilfe der [!DNL Flow Service] API

In diesem Tutorial erfahren Sie, wie Sie die Struktur und den Inhalt Ihrer Datentabellen mithilfe des [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
> Um Ihre Datentabellen zu untersuchen, müssen Sie bereits über eine gültige Basis-Verbindungs-ID für eine tabellarische Quelle verfügen. Wenn Sie diese ID nicht haben, finden Sie in den folgenden Tutorials Schritte zum Erstellen einer Basis-Verbindungs-ID für eine tabellarische Quelle: <ul><li>[Werbung](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[Customer Success](../../../home.md#customer-success)</li><li>[Datenbank](../../../home.md#database)</li><li>[E-Commerce](../../../home.md#ecommerce)</li><li>[Marketing-Automatisierung](../../../home.md#marketing-automation)</li><li>[Zahlungen](../../../home.md#payments)</li><li>[Protokolle](../../../home.md#protocols)</li></ul>

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../landing/api-guide.md).

## Datentabellen durchsuchen

Sie können Informationen zur Struktur Ihrer Datentabellen abrufen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] API bei gleichzeitiger Angabe der grundlegenden Verbindungs-ID Ihrer Quelle.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Kennung der Basisverbindung Ihrer Quelle. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Reihe von Tabellen aus Ihrer Quelle zurück. Suchen Sie die Tabelle, die Sie in Platform einführen möchten, und notieren Sie sich deren `path` -Eigenschaft, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Tabellenstruktur Inspect

Um den Inhalt Ihrer Datentabellen zu überprüfen, stellen Sie eine GET-Anfrage an die [!DNL Flow Service] API beim Angeben des Pfads einer Tabelle als Abfrageparameter.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Kennung der Basisverbindung Ihrer Quelle. |
| `{TABLE_PATH}` | Die Pfadeigenschaft der Tabelle, die Sie überprüfen möchten. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt Informationen zu Inhalt und Struktur der angegebenen Tabelle zurück. Details zu den einzelnen Spalten der Tabelle befinden sich in Elementen der `columns` Array.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "TestID",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Name",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## Nächste Schritte

In diesem Tutorial haben Sie Informationen zur Struktur und zum Inhalt Ihrer Datentabellen gesammelt. Außerdem haben Sie den Pfad zur Tabelle abgerufen, die Sie in Platform erfassen möchten. Sie können diese Informationen verwenden, um eine Quellverbindung und einen Datenfluss zu erstellen und Ihre Daten an Platform zu übertragen. Spezifische Schritte zum Erstellen einer Quellverbindung und eines Datenflusses mithilfe der [!DNL Flow Service] API:

* [Werbequellen](../collect/advertising.md)
* [CRM-Quellen](../collect/crm.md)
* [Kundenerfolgsquellen](../collect/customer-success.md)
* [Datenbankquellen](../collect/database-nosql.md)
* [E-Commerce-Quellen](../collect/ecommerce.md)
* [Marketing-Automatisierungsquellen](../collect/marketing-automation.md)
* [Zahlungsquellen](../collect/payments.md)
* [Protokollquellen](../collect/protocols.md)
