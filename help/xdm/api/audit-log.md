---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Audit; Audit-Protokoll; Änderungsprotokoll; rpc
solution: Experience Platform
title: Auditprotokoll-API-Endpunkt
description: Mit dem /auditlog-Endpunkt in der Schema Registry-API können Sie eine chronologische Liste der Änderungen abrufen, die an einer vorhandenen XDM-Ressource vorgenommen wurden.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 15%

---

# Endpunkt des Auditprotokolls

Für jede Experience-Datenmodell (XDM)-Ressource muss die [!DNL Schema Registry] verwaltet ein Protokoll aller Änderungen, die zwischen verschiedenen Aktualisierungen aufgetreten sind. Die `/auditlog` -Endpunkt im [!DNL Schema Registry] Mit der API können Sie ein Prüfprotokoll für jede Klasse, Schemafeldgruppe, jeden Datentyp oder jedes Schema abrufen, die bzw. das durch die ID angegeben ist.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

Die `/auditlog` Endpunkt ist Teil der Remote-Prozeduraufrufe (RPCs), die von der [!DNL Schema Registry]. Im Gegensatz zu anderen Endpunkten im [!DNL Schema Registry] API-, RPC-Endpunkte erfordern keine zusätzlichen Kopfzeilen wie `Accept` oder `Content-Type`und verwenden Sie keine `CONTAINER_ID`. Stattdessen müssen sie die `/rpc` -Namespace, wie im API-Aufruf unten dargestellt.

## Abrufen eines Auditprotokolls für eine Ressource

Sie können ein Prüfprotokoll für jede Klasse, Feldergruppe, jeden Datentyp oder jedes Schema in der Schemabibliothek abrufen, indem Sie die Kennung der Ressource im Pfad einer GET-Anfrage an die `/auditlog` -Endpunkt.

**API-Format**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_ID}` | Die `meta:altId` oder URL-kodiert `$id` der Ressource, deren Auditprotokoll Sie abrufen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Mit der folgenden Anfrage wird das Auditprotokoll für ein Schema abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine chronologische Liste der Änderungen zurück, die von der letzten zur letzten vorgenommen wurden.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `updates` | Ein Array von Objekten, wobei jedes Objekt eine Änderung an der angegebenen Ressource oder an einer der abhängigen Ressourcen darstellt. |
| `id` | Die `$id` der Ressource, die geändert wurde. Dieser Wert stellt normalerweise die im Anfragepfad angegebene Ressource dar, kann jedoch eine abhängige Ressource darstellen, wenn dies die Quelle der Änderung ist. |
| `xdmType` | Der Typ der Ressource, die geändert wurde. |
| `action` | Die Art der Änderung, die vorgenommen wurde. |
| `path` | A [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) Zeichenfolge, die den Pfad zum spezifischen Feld angibt, das geändert oder hinzugefügt wurde. |
| `value` | Der Wert, der dem neuen oder aktualisierten Feld zugewiesen wurde. |

{style=&quot;table-layout:auto&quot;}
