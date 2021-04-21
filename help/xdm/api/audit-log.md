---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Audit;Audit-Protokoll;Änderungsprotokoll;rpc
solution: Experience Platform
title: Auditprotokoll-API-Endpunkt
description: Der /auditlog-Endpunkt in der Schema Registry-API ermöglicht es Ihnen, eine chronologische Liste der Änderungen abzurufen, die an einer vorhandenen XDM-Ressource vorgenommen wurden.
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 4%

---

# Endpunkt des Prüfprotokolls

Für jede Experience Data Model-(XDM-)Ressource verwaltet das [!DNL Schema Registry] ein Protokoll aller Änderungen, die zwischen verschiedenen Aktualisierungen vorgenommen wurden. Mit dem `/auditlog`-Endpunkt in der [!DNL Schema Registry]-API können Sie ein Prüfprotokoll für alle Klassen, Mixins, Datentypen oder Schema abrufen, die von der ID angegeben wurden.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer Experience Platformen-API benötigt werden.

Der Endpunkt `/auditlog` ist Teil der Remote-Prozeduraufrufe (RPCs), die von [!DNL Schema Registry] unterstützt werden. Im Gegensatz zu anderen Endpunkten in der API sind für RPC-Endpunkte keine zusätzlichen Kopfzeilen wie `Accept` oder `Content-Type` erforderlich und es wird kein `CONTAINER_ID` verwendet. [!DNL Schema Registry] Stattdessen müssen sie den Namensraum `/rpc` verwenden, wie im API-Aufruf unten gezeigt.

## Abrufen eines Prüfprotokolls für eine Ressource

Sie können ein Prüfprotokoll für alle Klassen, Mixins, Datentypen oder Schema in der Schema-Bibliothek abrufen, indem Sie die Ressourcenkennung im Pfad einer GET zum Endpunkt `/auditlog` angeben.

**API-Format**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_ID}` | Die `meta:altId`- oder URL-kodierte `$id` der Ressource, deren Prüfprotokoll Sie abrufen möchten. |

**Anfrage**

Die folgende Anforderung ruft das Prüfprotokoll für ein `Restaurant`-Mixin ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine chronologische Liste der Änderungen zurück, die an der Ressource vorgenommen wurden, von der letzten bis zur letzten.

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
| `auditTrails` | Ein Array von Objekten, wobei jedes Objekt eine Änderung darstellt, die an der angegebenen Ressource oder einer der abhängigen Ressourcen vorgenommen wurde. |
| `id` | Die `$id` der Ressource, die geändert wurde. Dieser Wert stellt in der Regel die im Anforderungspfad angegebene Ressource dar, kann jedoch eine abhängige Ressource darstellen, wenn dies die Quelle der Änderung ist. |
| `action` | Die Art der vorgenommenen Änderung. |
| `path` | Eine [JSON-Zeiger](../../landing/api-fundamentals.md#json-pointer)-Zeichenfolge, die den Pfad zum jeweiligen Feld angibt, das geändert oder hinzugefügt wurde. |
| `value` | Der Wert, der dem neuen oder aktualisierten Feld zugewiesen wurde. |
