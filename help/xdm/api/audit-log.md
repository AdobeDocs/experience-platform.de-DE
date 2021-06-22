---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Audit; Audit-Protokoll; Änderungsprotokoll; rpc
solution: Experience Platform
title: Auditprotokoll-API-Endpunkt
description: Mit dem /auditlog-Endpunkt in der Schema Registry-API können Sie eine chronologische Liste der Änderungen abrufen, die an einer vorhandenen XDM-Ressource vorgenommen wurden.
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 8%

---

# Endpunkt des Auditprotokolls

Für jede Experience-Datenmodell (XDM)-Ressource verwaltet das [!DNL Schema Registry] ein Protokoll aller Änderungen, die zwischen verschiedenen Aktualisierungen aufgetreten sind. Mit dem Endpunkt `/auditlog` in der API [!DNL Schema Registry] können Sie ein Auditprotokoll für jede Klasse, Schemafeldgruppe, jeden Datentyp oder jedes Schema abrufen, die durch eine ID angegeben wurde.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Schema Registry] ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um Links zur zugehörigen Dokumentation zu erhalten, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

Der Endpunkt `/auditlog` ist Teil der Remote-Prozeduraufrufe (RPCs), die von [!DNL Schema Registry] unterstützt werden. Im Gegensatz zu anderen Endpunkten in der [!DNL Schema Registry]-API erfordern RPC-Endpunkte keine zusätzlichen Kopfzeilen wie `Accept` oder `Content-Type` und verwenden keine `CONTAINER_ID`. Stattdessen müssen sie den Namespace `/rpc` verwenden, wie im API-Aufruf unten dargestellt.

## Abrufen eines Auditprotokolls für eine Ressource

Sie können ein Prüfprotokoll für jede Klasse, Feldergruppe, jeden Datentyp oder jedes Schema in der Schemabibliothek abrufen, indem Sie die Kennung der Ressource im Pfad einer GET-Anfrage an den Endpunkt `/auditlog` angeben.

**API-Format**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_ID}` | Die `meta:altId` oder URL-kodierte `$id` der Ressource, deren Auditprotokoll Sie abrufen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Mit der folgenden Anfrage wird das Auditprotokoll für eine Feldergruppe `Restaurant` abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine chronologische Liste der Änderungen zurück, die von der letzten zur letzten vorgenommen wurden.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auditTrails` | Ein Array von Objekten, wobei jedes Objekt eine Änderung an der angegebenen Ressource oder an einer der abhängigen Ressourcen darstellt. |
| `id` | Die `$id` der Ressource, die geändert wurde. Dieser Wert stellt normalerweise die im Anfragepfad angegebene Ressource dar, kann jedoch eine abhängige Ressource darstellen, wenn dies die Quelle der Änderung ist. |
| `action` | Die Art der Änderung, die vorgenommen wurde. |
| `path` | Eine [JSON Pointer](../../landing/api-fundamentals.md#json-pointer)-Zeichenfolge, die den Pfad zum spezifischen Feld angibt, das geändert oder hinzugefügt wurde. |
| `value` | Der Wert, der dem neuen oder aktualisierten Feld zugewiesen wurde. |

{style=&quot;table-layout:auto&quot;}
