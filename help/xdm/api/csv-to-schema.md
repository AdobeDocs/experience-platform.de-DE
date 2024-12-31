---
title: Endpunkt der CSV-Vorlage für die Schemakonvertierungs-API
description: Mit dem Endpunkt /rpc/csv2schema in der Schema Registry-API können Sie CSV-Vorlagen verwenden, um automatisch Experience-Datenmodell (XDM)-Schemas zu erstellen.
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 6%

---

# Endpunkt der Konvertierungs-API für CSV-Vorlage in Schema

Der `/rpc/csv2schema`-Endpunkt in der [!DNL Schema Registry]-API ermöglicht Ihnen die automatische Erstellung eines Experience-Datenmodell (XDM)-Schemas mithilfe einer CSV-Datei als Vorlage. Mit diesem Endpunkt können Sie Vorlagen erstellen, um Schemafelder per Massenimport zu importieren und den manuellen API- oder UI-Arbeitsaufwand zu reduzieren.

## Erste Schritte

Der `/rpc/csv2schema`-Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen [ im Handbuch „Erste Schritte](./getting-started.md) Links zu entsprechenden Dokumentationen, einen Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer Adobe Experience Platform-API erforderlich sind.

Der `/rpc/csv2schema`-Endpunkt ist Teil der Remote Procedure Calls (RPCs), die vom [!DNL Schema Registry] unterstützt werden. Im Gegensatz zu anderen Endpunkten in der [!DNL Schema Registry]-API benötigen RPC-Endpunkte keine zusätzlichen Kopfzeilen wie `Accept` oder `Content-Type` und verwenden keine `CONTAINER_ID`. Stattdessen müssen sie den `/rpc` Namespace verwenden, wie in den folgenden API-Aufrufen veranschaulicht.

## CSV-Dateianforderungen

Um diesen Endpunkt zu verwenden, müssen Sie zunächst eine CSV-Datei mit entsprechenden Spaltenüberschriften und entsprechenden Werten erstellen. Einige Spalten sind erforderlich, der Rest ist optional. In der folgenden Tabelle werden diese Spalten und ihre Rolle bei der Schemaerstellung beschrieben.

| CSV-Kopfzeilenposition | CSV-Kopfzeilenname | Erforderlich/Optional | Beschreibung |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Optional | Wenn enthalten und auf `true` gesetzt, bedeutet dies, dass das Feld nicht für den API-Upload bereit ist und ignoriert werden sollte. |
| 2 | `isCustom` | Erforderlich | Gibt an, ob das Feld ein benutzerdefiniertes Feld ist oder nicht. |
| 3 | `fieldGroupId` | Optional | Die ID der Feldergruppe, mit der ein benutzerdefiniertes Feld verknüpft werden soll. |
| 4 | `fieldGroupName` | (Siehe Beschreibung) | Der Name der Feldergruppe, mit der dieses Feld verknüpft werden soll.<br><br>Optional für benutzerdefinierte Felder, die vorhandene Standardfelder nicht erweitern. Wenn Sie das Feld leer lassen, weist das System den Namen automatisch zu.<br><br>Erforderlich für Standardfelder oder benutzerdefinierte Felder, die Standardfeldgruppen erweitern und zur Abfrage des `fieldGroupId` verwendet werden. |
| 5 | `fieldPath` | Erforderlich | Der vollständige XED-Punktnotation-Pfad für das Feld. Um alle Felder aus einer Standardfeldgruppe einzubeziehen (wie unter `fieldGroupName` angegeben), setzen Sie den Wert auf `ALL`. |
| 6 | `displayName` | Optional | Der Titel oder Anzeigename für das Feld. Kann auch ein Alias für den Titel sein, sofern vorhanden. |
| 7 | `fieldDescription` | Optional | Eine Beschreibung für das Feld. Kann auch ein Alias für die Beschreibung sein, sofern vorhanden. |
| 8 | `dataType` | (Siehe Beschreibung) | Gibt den [einfachen Datentyp](../schema/field-constraints.md#basic-types) für das Feld an. Erforderlich für alle benutzerdefinierten Felder.<br><br>Wenn `dataType` auf `object` gesetzt ist, müssen entweder `properties` oder `$ref` ebenfalls für dieselbe Zeile definiert werden, jedoch nicht für beide. |
| 9 | `isRequired` | Optional | Gibt an, ob das Feld für die Datenaufnahme erforderlich ist. |
| 10 | `isArray` | Optional | Gibt an, ob das Feld ein Array seiner angegebenen `dataType` ist. |
| 11 | `isIdentity` | Optional | Gibt an, ob das Feld ein Identitätsfeld ist. |
| 12 | `identityNamespace` | Erforderlich, wenn `isIdentity` wahr ist | Der [Identity-Namespace](../../identity-service/features/namespaces.md) für das Identitätsfeld. |
| 13 | `isPrimaryIdentity` | Optional | Gibt an, ob das Feld die primäre Identität für das Schema ist. |
| 14 | `minimum` | Optional | (Nur für numerische Felder) Der Mindestwert für das Feld. |
| 15 | `maximum` | Optional | (Nur für numerische Felder) Der maximale Wert für das Feld. |
| 16 | `enum` | Optional | Eine Liste von Aufzählungswerten für das Feld, ausgedrückt als Array (z. B. `[value1,value2,value3]`). |
| 17 | `stringPattern` | Optional | (Nur für Zeichenfolgenfelder) Ein Regex-Muster, mit dem der Zeichenfolgenwert übereinstimmen muss, damit die Validierung während der Datenaufnahme erfolgreich ist. |
| 18 | `format` | Optional | (Nur für Zeichenfolgenfelder) Das Format für das Zeichenfolgenfeld. |
| 19 | `minLength` | Optional | (Nur für Zeichenfolgenfelder) Die Mindestlänge des Zeichenfolgenfelds. |
| 20 | `maxLength` | Optional | (Nur für Zeichenfolgenfelder) Die maximale Länge des Zeichenfolgenfelds. |
| 21 | `properties` | (Siehe Beschreibung) | Erforderlich, wenn `dataType` auf `object` gesetzt und `$ref` nicht definiert ist. Dadurch wird der Objekttext als JSON-String definiert (z. B. `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (Siehe Beschreibung) | Erforderlich, wenn `dataType` auf `object` gesetzt und `properties` nicht definiert ist. Dadurch wird die `$id` des referenzierten Objekts für den Objekttyp definiert (z. B. `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | Optional | Wenn `isIgnored` auf `true` gesetzt ist, wird diese Spalte verwendet, um die Kopfzeileninformationen des Schemas bereitzustellen. |

{style="table-layout:auto"}

Anhand der folgenden [CSV-Vorlage](../assets/sample-csv-template.csv) können Sie bestimmen, wie Ihre CSV-Datei formatiert werden soll.

## Erstellen einer Export-Payload aus einer CSV-Datei

Nachdem Sie Ihre CSV-Vorlage eingerichtet haben, können Sie die Datei an den `/rpc/csv2schema`-Endpunkt senden und in eine Export-Payload konvertieren.

**API-Format**

```http
POST /rpc/csv2schema
```

**Anfrage**

Die Anfrage-Payload muss Formulardaten als Format verwenden. Die erforderlichen Formularfelder werden unten angezeigt.

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
| `csv-file` | Der Pfad zur auf Ihrem lokalen Computer gespeicherten CSV-Vorlage. |
| `schema-class-id` | Die `$id` der XDM-Klasse [Klasse](../schema/composition.md#class) die dieses Schema verwenden wird. |
| `schema-name` | Ein Anzeigename für das Schema. |
| `schema-description` | Eine Beschreibung für das Schema. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Export-Payload zurück, die aus der CSV-Datei generiert wurde. Die Payload hat die Form eines Arrays und jedes Array-Element ist ein Objekt, das eine abhängige XDM-Komponente für das Schema darstellt. Wählen Sie den folgenden Abschnitt aus, um ein vollständiges Beispiel einer Export-Payload anzuzeigen, die aus einer CSV-Datei generiert wurde.

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

## Schema-Payload importieren

Nachdem Sie die Export-Payload aus der CSV-Datei generiert haben, können Sie diese Payload an den `/rpc/import`-Endpunkt senden, um das Schema zu generieren.

Weitere Informationen [ Generieren von Schemata aus Export](./import.md)Payloads finden Sie im Handbuch zum Import-Endpunkt .
