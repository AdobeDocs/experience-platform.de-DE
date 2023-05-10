---
title: CSV-Vorlage zum Schema Conversion API-Endpunkt
description: Mit dem Endpunkt /rpc/csv2schema in der Schema Registry-API können Sie CSV-Vorlagen verwenden, um automatisch Experience-Datenmodell (XDM)-Schemas zu erstellen.
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: b4c186c8c40d1372fb5011f49979523e1201fb0b
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 6%

---

# CSV-Vorlage zum Schema-Konversions-API-Endpunkt

Die `/rpc/csv2schema` -Endpunkt im [!DNL Schema Registry] Mit der API können Sie automatisch ein Experience-Datenmodell (XDM)-Schema mithilfe einer CSV-Datei als Vorlage erstellen. Mithilfe dieses Endpunkts können Sie Vorlagen erstellen, um Schemafelder per Massenimport zu importieren und die manuelle API- oder UI-Arbeit zu reduzieren.

## Erste Schritte

Die `/rpc/csv2schema` Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Adobe Experience Platform-APIs benötigt werden.

Die `/rpc/csv2schema` Endpunkt ist Teil der Remote-Prozeduraufrufe (RPCs), die von der [!DNL Schema Registry]. Im Gegensatz zu anderen Endpunkten im [!DNL Schema Registry] API-, RPC-Endpunkte erfordern keine zusätzlichen Kopfzeilen wie `Accept` oder `Content-Type`und verwenden Sie keine `CONTAINER_ID`. Stattdessen müssen sie die `/rpc` -Namespace, wie in den API-Aufrufen unten dargestellt.

## CSV-Dateianforderungen

Um diesen Endpunkt zu nutzen, müssen Sie zunächst eine CSV-Datei mit entsprechenden Spaltenüberschriften und entsprechenden Werten erstellen. Einige Spalten sind erforderlich, während der Rest optional ist. In der folgenden Tabelle werden diese Spalten und ihre Rolle bei der Schemaerstellung beschrieben.

| CSV-Kopfzeilenposition | CSV-Headername | Erforderlich/Optional | Beschreibung |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Optional | Wenn eingeschlossen, setzen Sie auf `true`gibt an, dass das Feld nicht bereit für den API-Upload ist und ignoriert werden sollte. |
| 2 | `isCustom` | Erforderlich | Gibt an, ob das Feld ein benutzerdefiniertes Feld ist oder nicht. |
| 3 | `fieldGroupId` | Optional | Die ID der Feldergruppe, der ein benutzerdefiniertes Feld zugeordnet werden soll. |
| 4 | `fieldGroupName` | (Siehe Beschreibung) | Der Name der Feldergruppe, mit der dieses Feld verknüpft werden soll.<br><br>Optional für benutzerdefinierte Felder, die keine vorhandenen Standardfelder erweitern. Wenn das Feld leer gelassen wird, weist das System automatisch einen Namen zu.<br><br>Erforderlich für Standardfelder oder benutzerdefinierte Felder, die Standardfeldgruppen erweitern, die zum Abfragen der `fieldGroupId`. |
| 5 | `fieldPath` | Erforderlich | Der vollständige Pfad für die XED-Punktnotation für das Feld. So schließen Sie alle Felder aus einer Standardfeldgruppe ein (wie unter `fieldGroupName`), setzen Sie den Wert auf `ALL`. |
| 6 | `displayName` | Optional | Der Titel oder Anzeigename für das Feld. Kann auch ein Alias für den Titel sein, sofern vorhanden. |
| 7 | `fieldDescription` | Optional | Eine Beschreibung für das Feld. Kann auch ein Alias für die Beschreibung sein, sofern vorhanden. |
| 8 | `dataType` | (Siehe Beschreibung) | Gibt die [Basistyp](../schema/field-constraints.md#basic-types) für das Feld. Erforderlich für alle benutzerdefinierten Felder.<br><br>Wenn `dataType` auf `object`, entweder `properties` oder `$ref` muss auch für dieselbe Zeile definiert werden, aber nicht für beide. |
| 9 | `isRequired` | Optional | Gibt an, ob das Feld für die Datenerfassung erforderlich ist. |
| 10 | `isArray` | Optional | Gibt an, ob das Feld ein Array von `dataType`. |
| 11 | `isIdentity` | Optional | Gibt an, ob das Feld ein Identitätsfeld ist. |
| 12 | `identityNamespace` | Erforderlich, wenn `isIdentity` ist wahr | Die [Identitäts-Namespace](../../identity-service/namespaces.md) für das Identitätsfeld. |
| 13 | `isPrimaryIdentity` | Optional | Gibt an, ob das Feld die primäre Identität für das Schema ist. |
| 14 | `minimum` | Optional | (Nur für numerische Felder) Der Mindestwert für das Feld. |
| 15 | `maximum` | Optional | (Nur für numerische Felder) Der Maximalwert für das Feld. |
| 16 | `enum` | Optional | Eine Liste von Enum-Werten für das Feld, ausgedrückt als Array (z. B. `[value1,value2,value3]`). |
| 17 | `stringPattern` | Optional | (Nur für Zeichenfolgenfelder) Ein Regex-Muster, mit dem der Zeichenfolgenwert übereinstimmen muss, um die Validierung während der Datenerfassung zu bestehen. |
| 18 | `format` | Optional | (Nur für Zeichenfolgenfelder) Das Format für das Zeichenfolgenfeld. |
| 19 | `minLength` | Optional | (Nur für Zeichenfolgenfelder) Die Mindestlänge des Zeichenfolgenfelds. |
| 20 | `maxLength` | Optional | (Nur für Zeichenfolgenfelder) Die maximale Länge des Zeichenfolgenfelds. |
| 21 | `properties` | (Siehe Beschreibung) | Erforderlich, wenn `dataType` auf `object` und `$ref` nicht definiert ist. Dadurch wird der Objekttext als JSON-Zeichenfolge definiert (z. B. `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (Siehe Beschreibung) | Erforderlich, wenn `dataType` auf `object` und `properties` nicht definiert ist. Dadurch wird die `$id` des referenzierten Objekts für den Objekttyp (z. B. `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | Optional | Wann `isIgnored` auf `true`, wird diese Spalte verwendet, um die Kopfzeileninformationen des Schemas anzugeben. |

{style="table-layout:auto"}

Siehe Folgendes [CSV-Vorlage](../assets/sample-csv-template.csv) , um zu bestimmen, wie Ihre CSV-Datei formatiert werden soll.

## Export-Payload aus einer CSV-Datei erstellen

Nachdem Sie Ihre CSV-Vorlage eingerichtet haben, können Sie die Datei an die `/rpc/csv2schema` -Endpunkt und konvertieren Sie ihn in eine Export-Payload.

**API-Format**

```http
POST /rpc/csv2schema
```

**Anfrage**

Die Anfrage-Payload muss Formulardaten als Format verwenden. Die erforderlichen Formularfelder sind unten dargestellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `csv-file` | Der Pfad zur CSV-Vorlage, die auf Ihrem lokalen Computer gespeichert ist. |
| `schema-class-id` | Die `$id` des XDM [class](../schema/composition.md#class) dass dieses Schema verwendet. |
| `schema-name` | Ein Anzeigename für das Schema. |
| `schema-description` | Eine Beschreibung für das Schema. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Export-Payload zurück, die aus der CSV-Datei generiert wurde. Die Payload hat die Form eines Arrays, und jedes Array-Element ist ein Objekt, das eine abhängige XDM-Komponente für das Schema darstellt. Wählen Sie den folgenden Abschnitt aus, um ein vollständiges Beispiel einer Export-Payload anzuzeigen, die aus einer CSV-Datei generiert wurde.

+++ Beispiel für Antwort-Payload

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## Importieren der Schema-Payload

Nachdem Sie die Export-Payload aus der CSV-Datei generiert haben, können Sie diese Payload an die `/rpc/import` -Endpunkt zum Generieren des Schemas.

Siehe [Import-Endpunkthandbuch](./import.md) für Details zum Generieren von Schemas aus Export-Payloads.
