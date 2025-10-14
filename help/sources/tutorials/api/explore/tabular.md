---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;API;erkunden;Flow Service
title: Erkunden einer tabellarischen Source mithilfe der Flow Service-API
description: In diesem Tutorial wird die Flow Service-API verwendet, um den Inhalt und die Struktur einer tabellenbasierten Quelle zu untersuchen.
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 16%

---

# Erkunden von Datentabellen mithilfe der [!DNL Flow Service]-API

In diesem Tutorial erfahren Sie, wie Sie die Struktur und den Inhalt Ihrer Datentabellen mithilfe der [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/)-API untersuchen und in der Vorschau anzeigen können.

>[!NOTE]
>
> Um Ihre Datentabellen zu untersuchen, müssen Sie bereits über eine gültige Basisverbindungs-ID für eine tabellarische Quelle verfügen. Wenn Sie diese ID nicht haben, finden Sie in den folgenden Tutorials Anweisungen zum Erstellen einer Basisverbindungs-ID für eine tabellarische Quelle: <ul><li>[Werbung](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[Customer Success](../../../home.md#customer-success)</li><li>[Datenbank](../../../home.md#database)</li><li>[E-Commerce](../../../home.md#ecommerce)</li><li>[Marketing-Automatisierung](../../../home.md#marketing-automation)</li><li>[Zahlungen](../../../home.md#payments)</li><li>[Protokolle](../../../home.md#protocols)</li></ul>

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [&#x200B; mit Experience Platform-APIs](../../../../landing/api-guide.md).

## Erkunden von Datentabellen

Sie können Informationen zur Struktur Ihrer Datentabellen abrufen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API richten und dabei die Basisverbindungs-ID Ihrer Quelle angeben.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindung Ihrer Quelle. |

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

Eine erfolgreiche Antwort gibt ein Array von Tabellen aus Ihrer Quelle zurück. Suchen Sie die Tabelle, die Sie in Experience Platform importieren möchten, und notieren Sie sich die `path` Eigenschaft, da Sie sie im nächsten Schritt bereitstellen müssen, um die Struktur zu überprüfen.

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

## Überprüfen der Tabellenstruktur

Um den Inhalt Ihrer Datentabellen zu überprüfen, führen Sie eine GET-Anfrage an die [!DNL Flow Service]-API aus und geben Sie dabei den Pfad einer Tabelle als Abfrageparameter an.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindung Ihrer Quelle. |
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

Eine erfolgreiche Antwort gibt Informationen über den Inhalt und die Struktur der angegebenen Tabelle zurück. Details zu den einzelnen Spalten der Tabelle befinden sich in Elementen des `columns`-Arrays.

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

In diesem Tutorial haben Sie Informationen über die Struktur und den Inhalt Ihrer Datentabellen gesammelt. Darüber hinaus haben Sie den Pfad zu der Tabelle abgerufen, die Sie in Experience Platform aufnehmen möchten. Mithilfe dieser Informationen können Sie eine Quellverbindung und einen Datenfluss erstellen, um Ihre Daten an Experience Platform zu übertragen. In den folgenden Tutorials finden Sie spezifische Schritte zum Erstellen einer Quellverbindung und eines Datenflusses mithilfe der [!DNL Flow Service]-API:

* [Advertising-Quellen](../collect/advertising.md)
* [CRM-Quellen](../collect/crm.md)
* [Customer Success Sources](../collect/customer-success.md)
* [Datenbankquellen](../collect/database-nosql.md)
* [E-Commerce-Quellen](../collect/ecommerce.md)
* [Quellen der Marketing-Automatisierung](../collect/marketing-automation.md)
* [Zahlungsquellen](../collect/payments.md)
* [Protokollquellen](../collect/protocols.md)
