---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Klasse erstellen
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# Klasse erstellen

Der Hauptbaustein eines Schemas ist eine Klasse. Die Klasse enthält den Mindestfeldsatz, der definiert werden muss, um die Kerndaten eines Schemas zu erfassen. Wenn Sie beispielsweise ein Schema für Pkw und Lkw entwerfen, würden sie höchstwahrscheinlich eine Klasse namens &quot;Vehicle&quot;verwenden, die die grundlegenden gemeinsamen Eigenschaften aller Fahrzeuge beschreibt.

Es gibt mehrere Standardklassen, die von Adobe und anderen Experience Platformen-Partnern bereitgestellt werden. Sie können jedoch auch eigene Klassen definieren und diese in der Schema-Registrierung speichern. Anschließend können Sie ein Schema zusammenstellen, das die von Ihnen erstellte Klasse implementiert, und Mixins definieren, die mit Ihrer neu definierten Klasse kompatibel sind.

>[!NOTE]
>
>Beim Erstellen eines Schemas, das auf einer von Ihnen definierten Klasse basiert, können Sie keine standardmäßigen Mixins verwenden. Jede Mixin definiert die Klassen, mit denen sie in ihrem `meta:intendedToExtend` Attribut kompatibel sind. Sobald Sie beginnen, Mixins zu definieren, die mit Ihrer neuen Klasse kompatibel sind (durch Verwendung `$id` der neuen Klasse im `meta:intendedToExtend` Bereich des mixins), können Sie diese Mixins jedes Mal wiederverwenden, wenn Sie ein Schema definieren, das die von Ihnen definierte Klasse implementiert. Weitere Informationen finden Sie in den Abschnitten zum [Erstellen von Mixins](create-mixin.md) und [Erstellen von Schemas](create-schema.md) .

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die Anforderung zum Erstellen (POST) einer Klasse muss ein `allOf` Attribut enthalten, das einen `$ref` von zwei Werten enthält: `https://ns.adobe.com/xdm/data/record` oder `https://ns.adobe.com/xdm/data/time-series`. Diese Werte stellen das Verhalten dar, auf dem die Klasse basiert (Datensatz oder Zeitreihen). Weitere Informationen zu den Unterschieden zwischen Datensatzdaten und Zeitreihendaten finden Sie im Abschnitt zu Verhaltenstypen innerhalb der [Grundlagen der Schema-Komposition](../schema/composition.md).

Wenn Sie eine Klasse definieren, können Sie auch Mixins oder benutzerdefinierte Felder in die Klassendefinition einschließen. Dies würde dazu führen, dass die hinzugefügten mixins und Felder in allen Schemas enthalten sind, die die Klasse implementieren. Die folgende Beispielanforderung definiert eine Klasse mit der Bezeichnung &quot;Eigenschaft&quot;, die Informationen zu verschiedenen Eigenschaften erfasst, die Eigentum und Betreiber einer Firma sind. Es enthält ein `propertyId` Feld, das bei jeder Verwendung der Klasse eingeschlossen wird.

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
| `_{TENANT_ID}` | Der `TENANT_ID` Namensraum für Ihre Organisation. Alle von Ihrer Organisation erstellten Ressourcen müssen diese Eigenschaft enthalten, um Kollisionen mit anderen Ressourcen in der Schema-Registrierung zu vermeiden. |
| `allOf` | Eine Liste von Ressourcen, deren Eigenschaften von der neuen Klasse geerbt werden sollen. Eines der `$ref` Objekte im Array definiert das Verhalten der Klasse. In diesem Beispiel übernimmt die Klasse das Verhalten &quot;record&quot;. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und eine Nutzlast mit den Details der neu erstellten Klasse zurück, einschließlich der Klassen `$id`, `meta:altId`und `version`. Diese drei Werte sind schreibgeschützt und werden von der Schema Registry zugewiesen.

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

Wenn Sie eine GET-Anforderung zur Liste aller Klassen im Mieter-Container ausführen, wird jetzt die Property-Klasse einbezogen. Sie können auch eine GET-Anfrage (Lookup) mit dem URL-kodierten `$id` URI ausführen, um die neue Klasse direkt Ansicht. Stellen Sie sicher, dass Sie die `version` in den Accept-Header aufnehmen, wenn Sie eine Suchanfrage ausführen.
