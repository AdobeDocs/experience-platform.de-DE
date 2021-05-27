---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schemaregistrierung; Schema Registry; Verhalten; Verhalten; Verhalten; Verhalten; Verhalten;
solution: Experience Platform
title: Verhalten-API-Endpunkt
description: Mit dem Endpunkt /verhaltenors in der Schema Registry-API können Sie alle verfügbaren Verhaltensweisen im globalen Container abrufen.
topic-legacy: developer guide
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 8%

---

# Verhaltensendpunkt

Im Experience-Datenmodell (XDM) definieren Verhaltensweisen die Art der Daten, die ein Schema beschreibt. Jede XDM-Klasse muss auf ein bestimmtes Verhalten verweisen, das von allen Schemas übernommen wird, die diese Klasse verwenden. Für fast alle Anwendungsfälle in Platform gibt es zwei verfügbare Verhaltensweisen:

* **[!UICONTROL Datensatz]**: Enthält Informationen zu den Attributen eines Betreffs. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **[!UICONTROL Zeitreihen]**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

>[!NOTE]
>
>Es gibt einige Anwendungsfälle in Platform, bei denen die Verwendung eines Schemas erforderlich ist, das keines der oben genannten Verhaltensweisen anwendet. Für diese Fälle ist ein drittes &quot;Ad-hoc&quot;-Verhalten verfügbar. Weitere Informationen finden Sie im Tutorial zum Erstellen eines Ad-hoc-Schemas](../tutorials/ad-hoc.md) .[
>
>Allgemeine Informationen zu Datenverhalten in Bezug darauf, wie sie sich auf die Schemakomposition auswirken, finden Sie im Leitfaden zu den [Grundlagen der Schemakomposition](../schema/composition.md).

Mit dem Endpunkt `/behaviors` in der API [!DNL Schema Registry] können Sie verfügbare Verhaltensweisen im Container `global` anzeigen.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Schema Registry] ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um Links zur zugehörigen Dokumentation zu erhalten, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Liste von Verhaltensweisen abrufen {#list}

Sie können eine Liste aller verfügbaren Verhaltensweisen abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/behaviors` stellen.

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

## Verhalten nachschlagen {#lookup}

Sie können ein bestimmtes Verhalten nachschlagen, indem Sie dessen Kennung im Pfad einer GET-Anfrage an den Endpunkt `/behaviors` angeben.

**API-Format**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BEHAVIOR_ID}` | Die `meta:altId` oder URL-kodierte `$id` des Verhaltens, das Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage ruft die Details des Datensatzverhaltens ab, indem sie im Anfragepfad den Wert `meta:altId` angibt.

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

In diesem Handbuch wurde die Verwendung des Endpunkts `/behaviors` in der API [!DNL Schema Registry] beschrieben. Informationen zum Zuweisen eines Verhaltens zu einer Klasse mithilfe der API finden Sie im [Klassen-Endpunkthandbuch](./classes.md).
