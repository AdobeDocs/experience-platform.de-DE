---
title: Companies-Endpunkt
description: Erfahren Sie, wie Sie den /companies-Endpunkt in der Reactor-API aufrufen.
exl-id: ee435358-ed34-4e0c-93af-796133fb11fc
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 100%

---

# Companies-Endpunkt

Bei einem Unternehmen handelt es sich um eine Kundenorganisation, typischerweise eine Firma. In der Reactor-API stimmen diese Unternehmen 1:1 mit der IMS-Organisations-ID überein. API-Benutzer haben nur Einblick in die Unternehmen, auf die sie Zugriff haben. Ein Unternehmen kann über viele [Eigenschaften](./properties.md) verfügen. Eine Eigenschaft gehört zu genau einem Unternehmen.

Mit dem `/companies`-Endpunkt in der Reactor-API können Sie die Unternehmen programmgesteuert abrufen, auf die Sie in Ihrer Erlebnisanwendung Zugriff haben.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen einer Liste von Unternehmen {#list}

Sie können die Unternehmen, zu deren Nutzung Sie berechtigt sind, auflisten, indem Sie eine GET-Anfrage an den `/companies`-Endpunkt stellen. In den meisten Fällen gibt es genau eines.

**API-Format**

```http
GET /companies
```

>[!NOTE]
>
>Mithilfe von Abfrageparametern können gelistete Unternehmen anhand der folgenden Attribute gefiltert werden:<ul><li>`created_at`</li><li>`name`</li><li>`org_id`</li><li>`token`</li><li>`updated_at`</li></ul>Weiterführende Informationen finden Sie im Handbuch zum [Filtern von Antworten](../guides/filtering.md).

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort liefert eine Liste von Firmen, auf die Sie Zugriff haben.

```json
{
  "data": [
    {
      "id": "COdb0cd64ad4524440be94b8496416ec7d",
      "type": "companies",
      "attributes": {
        "created_at": "2020-08-13T17:13:30.667Z",
        "name": "Example Company",
        "org_id": "{ORG_ID}",
        "updated_at": "2020-08-13T17:13:30.667Z",
        "token": "d5a4f682bbae",
        "cjm_enabled": false,
        "edge_enabled": false,
        "edge_events_allotment": null,
        "edge_fanout_ratio": null
      },
      "relationships": {
        "properties": {
          "links": {
            "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
        "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
      },
      "meta": {
        "rights": [
          "develop_extensions",
          "manage_properties"
        ],
        "platform_rights": {
          "web": [
            "develop_extensions",
            "manage_properties"
          ],
          "mobile": [
            "develop_extensions",
            "manage_properties"
          ]
        }
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Suchen eines Unternehmens {#lookup}

Sie können ein bestimmtes Unternehmen suchen, indem Sie seine ID im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /companies/{COMPANY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{COMPANY_ID}` | Die `id` Wert des Unternehmens, die Sie suchen möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Firma zurück.

```json
{
  "data": {
    "id": "COdb0cd64ad4524440be94b8496416ec7d",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.667Z",
      "name": "Example Company",
      "org_id": "{ORG_ID}",
      "updated_at": "2020-08-13T17:13:30.667Z",
      "token": "d5a4f682bbae",
      "cjm_enabled": false,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
      "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties"
        ]
      }
    }
  }
}
```
