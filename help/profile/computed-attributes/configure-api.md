---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API
title: Konfigurieren eines berechneten Attributfelds
type: Documentation
description: Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Um ein berechnetes Attribut zu konfigurieren, müssen Sie zunächst das Feld ermitteln, das den berechneten Attributwert enthält. Dieses Feld kann mithilfe der Schema Registry-API erstellt werden, um ein Schema und eine benutzerdefinierte Feldergruppe zu definieren, die das berechnete Attributfeld enthalten.
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 16%

---

# (Alpha) Konfigurieren Sie ein berechnetes Attributfeld mithilfe der Schema Registry-API.

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalitäten können sich ändern.

Um ein berechnetes Attribut zu konfigurieren, müssen Sie zunächst das Feld ermitteln, das den berechneten Attributwert enthält. Dieses Feld kann mithilfe der Schema Registry-API erstellt werden, um ein Schema und eine benutzerdefinierte Schemafeldergruppe zu definieren, die das berechnete Attributfeld enthalten. Es wird empfohlen, ein eigenes Schema und eine separate Feldergruppe &quot;Berechnete Attribute&quot;zu erstellen, in die Ihre Organisation alle Attribute einfügen kann, die als berechnete Attribute verwendet werden sollen. Dadurch kann Ihr Unternehmen das berechnete Attributschema sauber von anderen Schemata trennen, die für die Datenerfassung verwendet werden.

Der Workflow in diesem Dokument beschreibt, wie Sie mit der Schema Registry-API ein Profil-aktiviertes Schema &quot;Berechnetes Attribut&quot;erstellen, das auf eine benutzerdefinierte Feldergruppe verweist. Dieses Dokument enthält Beispielcode speziell für berechnete Attribute. Weitere Informationen finden Sie jedoch im Abschnitt [Handbuch zur Schema Registry-API](../../xdm/api/overview.md) für detaillierte Informationen zum Definieren von Feldergruppen und Schemas mithilfe der API.

## Erstellen einer Feldergruppe mit berechneten Attributen

Um eine Feldergruppe mithilfe der Schema Registry-API zu erstellen, stellen Sie zunächst eine POST-Anfrage an die `/tenant/fieldgroups` -Endpunkt und geben Sie die Details der Feldergruppe im Anfrageinhalt an. Weitere Informationen zum Arbeiten mit Feldergruppen mithilfe der Schema Registry-API finden Sie im Abschnitt [Handbuch für Feldergruppen-API-Endpunkte](../../xdm/api/field-groups.md).

**API-Format**

```http
POST /tenant/fieldgroups
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Field Group",
        "description":"Description of the field group.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `title` | Der Name der Feldergruppe, die Sie erstellen. |
| `meta:intendedToExtend` | Die XDM-Klasse, mit der die Feldergruppe verwendet werden kann. |

**Antwort**

Bei erfolgreicher Anfrage wird der HTTP-Status-Code 201 (Erstellt) mit einem Antworttext zurückgegeben, der die Details der neu erstellten Feldergruppe einschließlich der `$id`, `meta:altIt`und `version`. Diese Werte sind schreibgeschützt und werden von der Schema Registry zugewiesen.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of the field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Aktualisieren der Feldergruppe mit zusätzlichen berechneten Attributen

Da mehr berechnete Attribute erforderlich sind, können Sie die Feldergruppe mit berechneten Attributen mit zusätzlichen Attributen aktualisieren, indem Sie eine PUT-Anfrage an die `/tenant/fieldgroups` -Endpunkt. Für diese Anforderung müssen Sie die eindeutige ID der Feldergruppe, die Sie im Pfad erstellt haben, sowie alle neuen Felder, die Sie im Text hinzufügen möchten, einschließen.

Weiterführende Informationen zum Aktualisieren einer Feldergruppe mithilfe der Schema Registry-API finden Sie im Abschnitt [Handbuch für Feldergruppen-API-Endpunkte](../../xdm/api/field-groups.md).

**API-Format**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

**Anfrage**

Diese Anfrage fügt neue Felder hinzu, die sich auf `purchaseSummary` Informationen.

>[!NOTE]
>
>Beim Aktualisieren einer Feldergruppe über eine PUT-Anfrage muss der Hauptteil alle Felder enthalten, die beim Erstellen einer neuen Feldergruppe in einer POST-Anfrage erforderlich sind.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Field Group",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of field group.",
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  },
                  "purchaseSummary": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                      "totalSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      },
                      "countPurchases": {
                        "meta:xdmType": "int",
                        "type": "integer",
                        "minimum": -2147483648,
                        "maximum": 2147483647
                      },
                      "averageSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Feldergruppe zurück.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            },
            "purchaseSummary": {
              "type": "object",
              "meta:xdmType": "object",
              "properties": {
                "totalSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                },
                "countPurchases": {
                  "meta:xdmType": "int",
                  "type": "integer",
                  "minimum": -2147483648,
                  "maximum": 2147483647
                },
                "averageSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                }
              }
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Erstellen eines Profilaktivierten Schemas

Um ein Schema mit der Schema Registry-API zu erstellen, stellen Sie zunächst eine POST-Anfrage an die `/tenant/schemas` -Endpunkt hinzu und geben die Details des Schemas im Anfragetext an. Das Schema muss auch für [!DNL Profile] und werden als Teil des Vereinigungsschemas für die Schemaklasse angezeigt.

Weitere Informationen finden Sie unter [!DNL Profile]-aktivierte Schemas und Vereinigungsschemas, lesen Sie bitte die [[!DNL Schema Registry] API-Handbuch](../../xdm/api/overview.md) und [Dokumentation zu Grundlagen der Schemakomposition](../../xdm/schema/composition.md).

**API-Format**

```http
POST /tenants/schemas
```

**Anfrage**

Die folgende Anfrage erstellt ein neues Schema, das auf die `computedAttributesFieldGroup` wurde zuvor in diesem Dokument erstellt (mithilfe der eindeutigen ID) und ist für das Schema der Profilunion aktiviert (mithilfe der `meta:immutableTags` Array). Detaillierte Anweisungen zum Erstellen eines Schemas mithilfe der Schema Registry-API finden Sie im Abschnitt [Handbuch zu Schemas-API-Endpunkten](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Schema",
        "meta:extensible": false,
        "meta:abstract": false,
        "meta:immutableTags": [
          "union"
        ],
        "meta:extends": [
          "https://ns.adobe.com/xdm/context/profile",
          "https://ns.adobe.com/xdm/context/identitymap",
          "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
        ],
        "description": "Description of schema.",
        "definitions": {
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
          },
          {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
          },
          {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
          }
        ],
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
      }' 
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details zum neu erstellten Schema zurück, einschließlich `$id`, `meta:altId` und `version`. Diese Werte sind schreibgeschützt und werden von der Schema Registry zugewiesen.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:altId": "_{TENANT}.schemas.699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Computed Attributes Schema",
  "type": "object",
  "description": "Description of schema.",
  "definitions": {},
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/identitymap",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612385766411,
    "repo:lastModifiedDate": 1612385766411,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "a9c6b5c25c109970ffa5eaeb3db2b47b59c696e1d9407fb39ccf7e48b74b558e",
    "meta:globalLibVersion": "1.18.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT}",
  "meta:immutableTags": [
    "union"
  ]
}
```

## Nächste Schritte

Nachdem Sie ein Schema und eine Feldergruppe erstellt haben, in denen Ihre berechneten Attribute gespeichert werden, können Sie das berechnete Attribut mit dem `/computedattributes` API-Endpunkt. Ausführliche Anweisungen zum Erstellen eines berechneten Attributs in der API finden Sie in den Schritten unter [Handbuch zum API-Endpunkt für berechnete Attribute](ca-api.md).
