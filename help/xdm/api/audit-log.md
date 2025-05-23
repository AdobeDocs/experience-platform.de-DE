---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Audit;Audit;Audit-Protokoll;Änderungsprotokoll;Änderungsprotokoll;rpc;
solution: Experience Platform
title: Auditprotokoll-API-Endpunkt
description: Mit dem Endpunkt /auditlog in der Schema Registry-API können Sie eine chronologische Liste der Änderungen abrufen, die an einer vorhandenen XDM-Ressource vorgenommen wurden.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 13%

---

# Auditprotokoll-Endpunkt

Für jede Experience-Datenmodell (XDM)-Ressource führt der [!DNL Schema Registry] ein Protokoll über alle Änderungen, die zwischen verschiedenen Aktualisierungen aufgetreten sind. Mit dem `/auditlog`-Endpunkt in der [!DNL Schema Registry]-API können Sie ein Administratorprotokoll für eine beliebige Klasse, Schemafeldgruppe, einen beliebigen Datentyp oder ein beliebiges Schema abrufen, das durch eine ID angegeben wird.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

Der `/auditlog`-Endpunkt ist Teil der Remote Procedure Calls (RPCs), die vom [!DNL Schema Registry] unterstützt werden. Im Gegensatz zu anderen Endpunkten in der [!DNL Schema Registry]-API benötigen RPC-Endpunkte keine zusätzlichen Kopfzeilen wie `Accept` oder `Content-Type` und verwenden keine `CONTAINER_ID`. Stattdessen müssen sie den `/rpc`-Namespace verwenden, wie im folgenden API-Aufruf veranschaulicht.

## Abrufen eines Auditprotokolls für eine Ressource

Sie können ein Auditprotokoll für eine beliebige Klasse, Feldergruppe, einen beliebigen Datentyp oder ein beliebiges Schema in der Schemabibliothek abrufen, indem Sie die ID der Ressource im Pfad einer GET-Anfrage an den `/auditlog`-Endpunkt angeben.

**API-Format**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_ID}` | Die `meta:altId` oder URL-codierte `$id` der Ressource, deren Administratorprotokoll Sie abrufen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft das Administratorprotokoll für ein Schema ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine chronologische Liste der an der Ressource vorgenommenen Änderungen zurück, von den letzten bis zu den letzten.

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
| `updates` | Ein Array von Objekten, wobei jedes Objekt eine Änderung darstellt, die an der angegebenen Ressource oder einer ihrer abhängigen Ressourcen vorgenommen wurde. |
| `id` | Die `$id` der Ressource, die geändert wurde. Dieser Wert stellt normalerweise die im Anfragepfad angegebene Ressource dar, kann jedoch eine abhängige Ressource darstellen, wenn dies die Quelle der Änderung ist. |
| `xdmType` | Der Typ der Ressource, die geändert wurde. |
| `action` | Die Art der vorgenommenen Änderung. |
| `path` | Eine [JSON Pointer](../../landing/api-fundamentals.md#json-pointer)-Zeichenfolge, die den Pfad zu dem spezifischen Feld angibt, das geändert oder hinzugefügt wurde. |
| `value` | Der Wert, der dem neuen oder aktualisierten Feld zugewiesen wurde. |

{style="table-layout:auto"}
