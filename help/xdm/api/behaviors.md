---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schemaregistrierung; Schema Registry; Verhalten; Verhalten; Verhalten; Verhalten; Verhalten;
solution: Experience Platform
title: Verhalten-API-Endpunkt
description: Mit dem Endpunkt /verhaltenors in der Schema Registry-API können Sie alle verfügbaren Verhaltensweisen im globalen Container abrufen.
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 23%

---

# Verhaltensendpunkt

Im Experience-Datenmodell (XDM) definieren Verhaltensweisen die Art der Daten, die ein Schema beschreibt. Jede XDM-Klasse muss auf ein bestimmtes Verhalten verweisen, das von allen Schemas übernommen wird, die diese Klasse verwenden. Für fast alle Anwendungsfälle in Platform gibt es zwei verfügbare Verhaltensweisen:

* **[!UICONTROL Datensatz]**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt kann ein Unternehmen oder eine Person sein.
* **[!UICONTROL Zeitreihe]**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

>[!NOTE]
>
>Es gibt einige Anwendungsfälle in Platform, bei denen die Verwendung eines Schemas erforderlich ist, das keines der oben genannten Verhaltensweisen anwendet. Für diese Fälle ist ein drittes &quot;Ad-hoc&quot;-Verhalten verfügbar. Siehe Tutorial zu [Erstellen eines Ad-hoc-Schemas](../tutorials/ad-hoc.md) für weitere Informationen.
>
>Allgemeine Informationen zu Datenverhalten in Bezug auf die Schemakomposition finden Sie im Handbuch zu [Grundlagen der Schemakomposition](../schema/composition.md).

Die `/behaviors` -Endpunkt im [!DNL Schema Registry] Mit der API können Sie verfügbare Verhaltensweisen im `global` Container.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Liste von Verhaltensweisen abrufen {#list}

Sie können eine Liste aller verfügbaren Verhaltensweisen abrufen, indem Sie eine GET-Anfrage an die `/behaviors` -Endpunkt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Verhalten nachschlagen {#lookup}

Sie können ein bestimmtes Verhalten nachschlagen, indem Sie dessen Kennung im Pfad einer GET-Anfrage an die `/behaviors` -Endpunkt.

**API-Format**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BEHAVIOR_ID}` | Die `meta:altId` oder URL-kodiert `$id` des Verhaltens, das Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage ruft die Details des Datensatzverhaltens ab, indem sie dessen `meta:altId` im Anfragepfad.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Verhaltens zurück, einschließlich der Version, Beschreibung und der Attribute, die das Verhalten den Klassen bereitstellt, die es anwenden.

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

In diesem Handbuch wurde die Verwendung der `/behaviors` -Endpunkt im [!DNL Schema Registry] API. Informationen zum Zuweisen eines Verhaltens zu einer Klasse mithilfe der API finden Sie unter [Endpunktleitfaden für Klassen](./classes.md).
