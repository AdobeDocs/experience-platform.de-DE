---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;Verhalten;Verhalten;Verhalten;Verhalten;
solution: Experience Platform
title: Verhalten-API-Endpunkt
description: Mit dem Endpunkt "/verhaltenors"in der Schema Registry-API können Sie alle verfügbaren Verhaltensweisen im globalen Container abrufen.
topic-legacy: developer guide
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

---

# Verhaltensendpunkt

Im Erlebnis-Datenmodell (XDM) definieren Verhaltensweisen die Art der Daten, die ein Schema beschreibt. Jede XDM-Klasse muss auf ein bestimmtes Verhalten verweisen, das von allen Schemas, die diese Klasse verwenden, übernommen wird. Für nahezu alle Anwendungsfälle in Platform gibt es zwei verfügbare Verhaltensweisen:

* **[!UICONTROL Datensatz]**: Stellt Informationen zu den Attributen eines Betreffs bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **[!UICONTROL Zeitreihen]**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt dar, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

>[!NOTE]
>
>Es gibt einige Anwendungsfälle in der Plattform, die die Verwendung von Schema erfordern, das keines der oben genannten Verhalten verwendet. Für diese Fälle steht ein drittes &quot;Ad-hoc&quot;-Verhalten zur Verfügung. Weitere Informationen finden Sie im Tutorial [Erstellen eines Ad-hoc-Schemas](../tutorials/ad-hoc.md).
>
>Weitere allgemeine Informationen zu Datenverhalten in Bezug darauf, wie sie die Zusammensetzung des Schemas beeinflussen, finden Sie im Handbuch [Grundlagen der Schema-Komposition](../schema/composition.md).

Der `/behaviors`-Endpunkt in der [!DNL Schema Registry]-API ermöglicht die Ansicht der verfügbaren Verhaltensweisen im `global`-Container.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer Experience Platformen-API benötigt werden.

## Abrufen einer Liste von Verhalten {#list}

Sie können eine Liste aller verfügbaren Verhaltensweisen abrufen, indem Sie eine GET an den `/behaviors`-Endpunkt anfordern.

**API-Format**

```http
GET /global/behaviors
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Antwort**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## Nachschlagen eines Verhaltens {#lookup}

Sie können ein bestimmtes Verhalten nachschlagen, indem Sie seine ID im Pfad einer GET zum `/behaviors`-Endpunkt angeben.

**API-Format**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BEHAVIOR_ID}` | Die `meta:altId`- oder URL-kodierte `$id` des Verhaltens, das nachschlagen soll. |

**Anfrage**

Die folgende Anforderung ruft die Details des Datensatzverhaltens ab, indem sie dessen `meta:altId` im Anforderungspfad angibt.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Verhaltens zurück, einschließlich der Version, Beschreibung und der Attribute, die das Verhalten den Klassen bereitstellt, die es verwenden.

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## Nächste Schritte

In diesem Handbuch wurde die Verwendung des Endpunkts `/behaviors` in der [!DNL Schema Registry]-API behandelt. Informationen zum Zuweisen eines Verhaltens zu einer Klasse mithilfe der API finden Sie im Endpunktleitfaden [Klassen](./classes.md).
