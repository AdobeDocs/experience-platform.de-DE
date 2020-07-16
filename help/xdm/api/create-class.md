---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Klasse erstellen
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 89%

---


# Klasse erstellen

Der Hauptbaustein eines Schemas ist eine Klasse. Die Klasse enthält den Mindestsatz an Feldern, die definiert sein müssen, damit die Kerndaten eines Schemas erfasst werden. Wenn Sie beispielsweise ein Schema für Autos und LKWs entwerfen, würden sie wahrscheinlich eine Klasse namens „Fahrzeug“ nutzen, um die grundlegenden allgemeinen Eigenschaften aller Fahrzeuge zu beschreiben.

There are several standard classes provided by Adobe and other [!DNL Experience Platform] partners, but you may also define your own classes and save them to the [!DNL Schema Registry]. Anschließend können Sie ein Schema komponieren, das die von Ihnen erstellte Klasse implementiert, und Mixins definieren, die mit Ihrer neu definierten Klasse kompatibel sind.

>[!NOTE]
>
>Beim Erstellen eines Schemas, das auf einer von Ihnen definierten Klasse basiert, können Sie keine standardmäßigen Mixins verwenden. Jedes Mixin definiert die Klassen, mit denen es kompatibel ist, in seinem `meta:intendedToExtend`-Attribut. Sobald Sie Mixins definiert haben, die mit Ihrer neuen Klasse kompatibel sind (durch Verwendung der `$id` Ihrer neuen Klasse im `meta:intendedToExtend`-Feld des Mixins), können Sie die Mixins jedes Mal wiederverwenden, wenn Sie ein Schema definieren, das die von Ihnen definierte Klasse implementiert. Weiterführende Informationen finden Sie in den Abschnitten zum [Erstellen von Mixins](create-mixin.md) und [Erstellen von Schemas](create-schema.md).

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die Anfrage zum Erstellen einer Klasse (POST) muss ein `allOf`-Attribut enthalten, das eine `$ref` zu einem von zwei Werten enthält: `https://ns.adobe.com/xdm/data/record` oder `https://ns.adobe.com/xdm/data/time-series`. Diese Werte stellen das Verhalten dar, auf dem die Klasse basiert (Datensatz oder Zeitreihe). Weiterführende Informationen zu Unterschieden zwischen Datensatzdaten und Zeitreihendaten finden Sie im Abschnitt zu Verhaltenstypen in den [Grundlagen der Schemakomposition](../schema/composition.md).

Beim Definieren einer Klasse können Sie auch Mixins oder benutzerdefinierte Felder in die Klassendefinition einschließen. Das würde dazu führen, dass die hinzugefügten Mixins und Felder in allen Schemas enthalten sind, die die Klasse implementieren. Folgende Beispielanfrage definiert eine Klasse namens „Eigenschaft“, die Daten zu verschiedenen Eigenschaften erfasst, die von einer Firma besessen und genutzt werden. Sie enthält ein `propertyId`-Feld, das bei jeder Verwendung der Klasse eingeschlossen wird.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `_{TENANT_ID}` | Der `TENANT_ID`-Namespace für Ihre Organisation. All resources created by your organization must include this property to avoid collisions with other resources in the [!DNL Schema Registry]. |
| `allOf` | Eine Liste mit Ressourcen, deren Eigenschaften von der neuen Klasse geerbt werden sollen. Eines der `$ref`-Objekte im Array definiert das Verhalten der Klasse. In diesem Beispiel übernimmt die Klasse das Verhalten „record“. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details der neu erstellten Klasse zurück, einschließlich `$id`, `meta:altId` und `version`. These three values are read-only and are assigned by the [!DNL Schema Registry].

```JSON
{
    "title": "Property",
    "description": "Properties owned and operated by the company.",
    "type": "object",
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "property": {
                            "title": "Property Information",
                            "type": "object",
                            "description": "Information about different owned and operated properties.",
                            "properties": {
                                "propertyId": {
                                    "title": "Property Identification Number",
                                    "type": "string",
                                    "description": "Unique Property identification number",
                                    "meta:xdmType": "string"
                                }
                            },
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/record"
        },
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "version": "1.0",
    "meta:resourceType": "classes",
    "meta:registryMetadata": {
        "repo:createDate": 1552086405448,
        "repo:lastModifiedDate": 1552086405448,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Wenn Sie eine GET-Anfrage zum Auflisten aller Klassen im Mandanten-Container ausführen, würde jetzt die Klasse „Eigenschaft“ einbezogen. Sie können mit dem URL-kodierten `$id`-URI auch eine Anfrage zum Nachschlagen (GET) ausführen, um die neue Klasse direkt anzuzeigen. Stellen Sie sicher, dass Sie die `version` in die Accept-Kopfzeile aufnehmen, wenn Sie eine Anfrage zum Nachschlagen ausführen.
