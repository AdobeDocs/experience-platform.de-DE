---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: Konfigurieren eines Felds für berechnete Attribute
topic-legacy: guide
type: Documentation
description: Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene Aggregat werden. Um ein berechnetes Attribut zu konfigurieren, müssen Sie zunächst das Feld ermitteln, das den berechneten Attributwert enthält. Dieses Feld kann mithilfe der Schema Registry API erstellt werden, um ein Schema und eine benutzerspezifische Feldgruppe zu definieren, die das berechnete Attributfeld enthalten.
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 14%

---

# (Alpha) Konfigurieren Sie ein berechnetes Attributfeld mithilfe der Schema Registry API

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Um ein berechnetes Attribut zu konfigurieren, müssen Sie zunächst das Feld ermitteln, das den berechneten Attributwert enthält. Dieses Feld kann mithilfe der Schema Registry API erstellt werden, um ein Schema und eine benutzerspezifische Schema-Feldgruppe zu definieren, die das berechnete Attributfeld enthalten. Es empfiehlt sich, ein separates Schema und eine Feldgruppe für &quot;Berechnete Attribute&quot;zu erstellen, in die Ihr Unternehmen alle Attribute einfügen kann, die als berechnete Attribute verwendet werden sollen. Dadurch kann Ihr Unternehmen das Schema des berechneten Attributs sauber von anderen Schemas trennen, die zur Datenerfassung verwendet werden.

Der Arbeitsablauf in diesem Dokument beschreibt, wie Sie mit der Schema-Registrierungs-API ein Profil-aktiviertes &quot;Berechnetes Attribut&quot;-Schema erstellen, das auf eine benutzerspezifische Feldgruppe verweist. Dieses Dokument enthält Beispielcode, der spezifisch für berechnete Attribute ist. Detaillierte Informationen zum Definieren von Feldgruppen und Schemas mithilfe der API finden Sie jedoch im Handbuch [Schema Registry API guide](../../xdm/api/overview.md).

## Erstellen einer Feldgruppe für berechnete Attribute

Um eine Feldgruppe mithilfe der Schema Registry API zu erstellen, müssen Sie zunächst eine POST an den `/tenant/fieldgroups`-Endpunkt anfordern und die Details der Feldgruppe im Anforderungstext angeben. Weitere Informationen zum Arbeiten mit Feldgruppen mithilfe der Schema Registry API finden Sie im [API-Endpunktleitfaden ](../../xdm/api/field-groups.md) für Feldgruppen.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `title` | Der Name der Feldgruppe, die Sie erstellen. |
| `meta:intendedToExtend` | Die XDM-Klasse, mit der die Feldgruppe verwendet werden kann. |

**Antwort**

Bei einer erfolgreichen Anforderung wird HTTP Response Status 201 (Erstellt) mit einem Antworttext zurückgegeben, der die Details der neu erstellten Feldgruppe enthält, einschließlich `$id`, `meta:altIt` und `version`. Diese Werte sind schreibgeschützt und werden von der Schema Registry zugewiesen.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.fieldgroups.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "fieldgroups",
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
  "imsOrg": "{IMS_ORG}",
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

## Feldgruppe mit zusätzlichen berechneten Attributen aktualisieren

Da mehr berechnete Attribute benötigt werden, können Sie die Feldgruppe für berechnete Attribute mit zusätzlichen Attributen aktualisieren, indem Sie eine PUT an den `/tenant/fieldgroups`-Endpunkt anfordern. Für diese Anforderung müssen Sie die eindeutige ID der Feldgruppe, die Sie im Pfad erstellt haben, sowie alle neuen Felder, die Sie im Textkörper hinzufügen möchten, einschließen.

Weitere Informationen zum Aktualisieren einer Feldgruppe mit der Schema Registry API finden Sie im [API-Endpunktleitfaden ](../../xdm/api/field-groups.md) für Feldgruppen.

**API-Format**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

**Anfrage**

Mit dieser Anforderung werden neue Felder zu `purchaseSummary`-Informationen hinzugefügt.

>[!NOTE]
>
>Beim Aktualisieren einer Feldgruppe über eine PUT-Anforderung muss der Textkörper alle Felder enthalten, die beim Erstellen einer neuen Feldgruppe in einer POST-Anforderung erforderlich sind.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Eine erfolgreiche Antwort gibt die Details der aktualisierten Feldgruppe zurück.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.fieldgroups.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "fieldgroups",
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
  "imsOrg": "{IMS_ORG}",
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

## Erstellen eines Profil-aktivierten Schemas

Um ein Schema mithilfe der Schema Registry API zu erstellen, stellen Sie zunächst eine Anfrage an den `/tenant/schemas`-Endpunkt und geben Sie die Details des Schemas im Anforderungstext ein. Das Schema muss auch für [!DNL Profile] aktiviert sein und als Teil des Vereinigung-Schemas für die Schema-Klasse angezeigt werden.

Weitere Informationen zu [!DNL Profile]-aktivierten Schemas und Vereinigung-Schemas finden Sie im [[!DNL Schema Registry] API-Handbuch](../../xdm/api/overview.md) und in der [Schema-Komposition - Dokumentation](../../xdm/schema/composition.md).

**API-Format**

```http
POST /tenants/schemas
```

**Anfrage**

Die folgende Anforderung erstellt ein neues Schema, das auf das zuvor in diesem Dokument erstellte `computedAttributesFieldGroup` verweist (unter Verwendung seiner eindeutigen ID) und für das Profil-Vereinigung-Schema aktiviert ist (unter Verwendung des Arrays `meta:immutableTags`). Detaillierte Anweisungen zum Erstellen eines Schemas mit der Schema Registry-API finden Sie im [Schemas API-Endpunkt-Handbuch](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
          "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
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
      "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
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

Nachdem Sie eine Schema- und Feldgruppe erstellt haben, in der die berechneten Attribute gespeichert werden, können Sie das berechnete Attribut mit dem API-Endpunkt `/computedattributes` erstellen. Ausführliche Anweisungen zum Erstellen eines berechneten Attributs in der API finden Sie in der Anleitung [API-Endpunkt für berechnete Attribute](ca-api.md).
