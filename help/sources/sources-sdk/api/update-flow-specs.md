---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Aktualisieren von Flussspezifikationen mithilfe der Flow Service-API
description: Das folgende Dokument beschreibt die Schritte zum Abrufen und Aktualisieren von Flussspezifikationen mithilfe der Flow Service-API für Selbstbedienungsquellen (Batch-SDK).
exl-id: 67a0cd3e-ac18-43a4-aa22-8f6376d5cc3f
source-git-commit: 21bccacf3555881ae731d0e60ff7d7677f18732d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 17%

---

# Aktualisieren von Flussspezifikationen mithilfe der [!DNL Flow Service]-API

Nachdem Sie eine neue Verbindungsspezifikations-ID generiert haben, müssen Sie diese ID zu einer Flussspezifikation hinzufügen, um einen Datenfluss zu erstellen.

Flussspezifikationen enthalten Informationen, die einen Fluss definieren, darunter die unterstützten Quell- und Zielverbindungs-IDs, Transformationsspezifikationen, die auf die Daten angewendet werden müssen, und Zeitplanparameter, die zum Generieren eines Flusses erforderlich sind. Sie können Flussspezifikationen mithilfe des `/flowSpecs`-Endpunkts bearbeiten.

Das folgende Dokument beschreibt die Schritte zum Abrufen und Aktualisieren von Flussspezifikationen mithilfe der [!DNL Flow Service]-API für Selbstbedienungsquellen (Batch-SDK).

## Erste Schritte

Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Flussspezifikation nachschlagen {#lookup}

Mit der `generic-rest-extension` erstellte Quellen verwenden alle die `RestStorageToAEP` Flussspezifikation. Diese Flussspezifikation kann abgerufen werden, indem eine GET-Anfrage an den `/flowSpecs/`-Endpunkt gesendet und die `flowSpec.id` der `6499120c-0b15-42dc-936e-847ea3c24d72` angegeben wird.

**API-Format**

```http
GET /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**Anfrage**

Die folgende Anfrage ruft die `6499120c-0b15-42dc-936e-847ea3c24d72` Verbindungsspezifikation ab.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der abgefragten Flussspezifikation zurück.

```json
{
  "items": [
      {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "createdAt": 1633080822911,
          "updatedAt": 1633080822911,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "{SANDBOX_ID}",
          "sandboxName": "{SANDBOX_NAME}",
          "imsOrgId": "{ORG_ID}",
          "name": "RestStorageToAEP",
          "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
          "version": "1.0",
          "sourceConnectionSpecIds": [
              "2d46966e-4fcc-4015-9f9e-a67594e395a3"
          ],
          "targetConnectionSpecIds": [
              "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
          ],
          "optionSpec": {
              "name": "OptionSpec",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "properties": {
                      "errorDiagnosticsEnabled": {
                          "title": "Error diagnostics.",
                          "description": "Flag to enable detailed and sample error diagnostics summary.",
                          "type": "boolean",
                          "default": false
                      },
                      "partialIngestionPercent": {
                          "title": "Partial ingestion threshold.",
                          "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                          "type": "number",
                          "exclusiveMinimum": 0
                      }
                  }
              }
          },
          "transformationSpecs": [
              {
                  "name": "Mapping",
                  "spec": {
                      "$schema": "http://json-schema.org/draft-07/schema#",
                      "type": "object",
                      "description": "defines various params required for different mapping from source to target",
                      "properties": {
                          "mappingId": {
                              "type": "string"
                          },
                          "mappingVersion": {
                              "type": "string"
                          }
                      }
                  }
              }
          ],
          "scheduleSpec": {
              "name": "PeriodicSchedule",
              "type": "Periodic",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "properties": {
                      "startTime": {
                          "description": "epoch time",
                          "type": "integer"
                      },
                      "frequency": {
                          "type": "string",
                          "enum": [
                              "once",
                              "minute",
                              "hour",
                              "day",
                              "week"
                          ]
                      },
                      "interval": {
                          "type": "integer"
                      },
                      "backfill": {
                          "type": "boolean",
                          "default": true
                      }
                  },
                  "required": [
                      "startTime",
                      "frequency"
                  ],
                  "if": {
                      "properties": {
                          "frequency": {
                              "const": "once"
                          }
                      }
                  },
                  "then": {
                      "allOf": [
                          {
                              "not": {
                                  "required": [
                                      "interval"
                                  ]
                              }
                          },
                          {
                              "not": {
                                  "required": [
                                      "backfill"
                                  ]
                              }
                          }
                      ]
                  },
                  "else": {
                      "required": [
                          "interval"
                      ],
                      "if": {
                          "properties": {
                              "frequency": {
                                  "const": "minute"
                              }
                          }
                      },
                      "then": {
                          "properties": {
                              "interval": {
                                  "minimum": 15
                              }
                          }
                      },
                      "else": {
                          "properties": {
                              "interval": {
                                  "minimum": 1
                              }
                          }
                      }
                  }
              }
          },
          "attributes": {
              "notification": {
                  "category": "sources",
                  "flowRun": {
                      "enabled": true
                  }
              }
          },
          "permissionsInfo": {
              "manage": [
                  {
                      "@type": "lowLevel",
                      "name": "EnterpriseSource",
                      "permissions": [
                          "write"
                      ]
                  }
              ],
              "view": [
                  {
                      "@type": "lowLevel",
                      "name": "EnterpriseSource",
                      "permissions": [
                          "read"
                      ]
                  }
              ]
          }
      },
  ]
}
```

## Aktualisieren einer Flussspezifikation {#update}

Sie können die Felder einer Verbindungsspezifikation durch einen PUT-Vorgang aktualisieren. Beim Aktualisieren einer Verbindungsspezifikation über eine PUT-Anfrage muss der Hauptteil alle Felder enthalten, die beim Erstellen einer neuen Verbindungsspezifikation in einer POST-Anfrage erforderlich wären.

>[!IMPORTANT]
>
>Sie müssen die Liste der `sourceConnectionSpecIds` der Flussspezifikation, die einer neuen Quelle entspricht, jedes Mal aktualisieren, wenn eine neue Quelle erstellt wird. Dadurch wird sichergestellt, dass Ihre neue Quelle von einer vorhandenen Flussspezifikation unterstützt wird, sodass Sie den Datenfluss-Erstellungsprozess mit Ihrer neuen Quelle abschließen können.

**API-Format**

```http
PUT /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**Anfrage**

Die folgende Anfrage aktualisiert die Flussspezifikation von `6499120c-0b15-42dc-936e-847ea3c24d72`, um die Verbindungsspezifikations-ID `f6c0de0c-0a42-4cd9-9139-8768bf2f1b55` einzuschließen.

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
`     "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "name": "RestStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "attributes": {
        "notification": {
          "category": "sources",
          "flowRun": {
            "enabled": true
          }
        }
      },
      "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
      ],
      "targetConnectionSpecIds": [
        "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "write"
            ]
          }
        ]
      },
      "optionSpec": {
        "name": "OptionSpec",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "errorDiagnosticsEnabled": {
              "title": "Error diagnostics.",
              "description": "Flag to enable detailed and sample error diagnostics summary.",
              "type": "boolean",
              "default": false
            },
            "partialIngestionPercent": {
              "title": "Partial ingestion threshold.",
              "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
              "type": "number",
              "exclusiveMinimum": 0
            }
          }
        }
      },
      "scheduleSpec": {
        "name": "PeriodicSchedule",
        "type": "Periodic",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "startTime": {
              "description": "epoch time",
              "type": "integer"
            },
            "frequency": {
              "type": "string",
              "enum": [
                "once",
                "minute",
                "hour",
                "day",
                "week"
              ]
            },
            "interval": {
              "type": "integer"
            },
            "backfill": {
              "type": "boolean",
              "default": true
            }
          },
          "required": [
            "startTime",
            "frequency"
          ],
          "if": {
            "properties": {
              "frequency": {
                "const": "once"
              }
            }
          },
          "then": {
            "allOf": [
              {
                "not": {
                  "required": [
                    "interval"
                  ]
                }
              },
              {
                "not": {
                  "required": [
                    "backfill"
                  ]
                }
              }
            ]
          },
          "else": {
            "required": [
              "interval"
            ],
            "if": {
              "properties": {
                "frequency": {
                  "const": "minute"
                }
              }
            },
            "then": {
              "properties": {
                "interval": {
                  "minimum": 15
                }
              }
            },
            "else": {
              "properties": {
                "interval": {
                  "minimum": 1
                }
              }
            }
          }
        }
      },
      "transformationSpec": [
        {
          "name": "Mapping",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for different mapping from source to target",
            "properties": {
              "mappingId": {
                "type": "string"
              },
              "mappingVersion": {
                "type": "string"
              }
            }
          }
        }
      ]
    }'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Details der abgefragten Flussspezifikation zurückgegeben, einschließlich der aktualisierten Liste der `sourceConnectionSpecIds`.

```json
{
    "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
    "updatedAt": 1633393222979,
    "updatedBy": "1633393222979",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "RestStorageToAEP",
    "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
    "version": "1.0",
    "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
    ],
    "targetConnectionSpecIds": [
        "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
    ],
    "optionSpec": {
        "name": "OptionSpec",
        "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "properties": {
                "errorDiagnosticsEnabled": {
                    "title": "Error diagnostics.",
                    "description": "Flag to enable detailed and sample error diagnostics summary.",
                    "type": "boolean",
                    "default": false
                },
                "partialIngestionPercent": {
                    "title": "Partial ingestion threshold.",
                    "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                    "type": "number",
                    "exclusiveMinimum": 0
                }
            }
        }
    },
    "transformationSpecs": [
        {
            "name": "Mapping",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "description": "defines various params required for different mapping from source to target",
                "properties": {
                    "mappingId": {
                        "type": "string"
                    },
                    "mappingVersion": {
                        "type": "string"
                    }
                }
            }
        }
    ],
    "scheduleSpec": {
        "name": "PeriodicSchedule",
        "type": "Periodic",
        "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "properties": {
                "startTime": {
                    "description": "epoch time",
                    "type": "integer"
                },
                "frequency": {
                    "type": "string",
                    "enum": [
                        "once",
                        "minute",
                        "hour",
                        "day",
                        "week"
                    ]
                },
                "interval": {
                    "type": "integer"
                },
                "backfill": {
                    "type": "boolean",
                    "default": true
                }
            },
            "required": [
                "startTime",
                "frequency"
            ],
            "if": {
                "properties": {
                    "frequency": {
                        "const": "once"
                    }
                }
            },
            "then": {
                "allOf": [
                    {
                        "not": {
                            "required": [
                                "interval"
                            ]
                        }
                    },
                    {
                        "not": {
                            "required": [
                                "backfill"
                            ]
                        }
                    }
                ]
            },
            "else": {
                "required": [
                    "interval"
                ],
                "if": {
                    "properties": {
                        "frequency": {
                            "const": "minute"
                        }
                    }
                },
                "then": {
                    "properties": {
                        "interval": {
                            "minimum": 15
                        }
                    }
                },
                "else": {
                    "properties": {
                        "interval": {
                            "minimum": 1
                        }
                    }
                }
            }
        }
    },
    "attributes": {
        "notification": {
            "category": "sources",
            "flowRun": {
                "enabled": true
            }
        }
    },
    "permissionsInfo": {
        "manage": [
            {
                "@type": "lowLevel",
                "name": "EnterpriseSource",
                "permissions": [
                    "write"
                ]
            }
        ],
        "view": [
            {
                "@type": "lowLevel",
                "name": "EnterpriseSource",
                "permissions": [
                    "read"
                ]
            }
        ]
    }
}
```

## Nächste Schritte

Nachdem Ihre neue Verbindungsspezifikation zur entsprechenden Flussspezifikation hinzugefügt wurde, können Sie jetzt mit dem Testen und Senden Ihrer neuen Quelle fortfahren. Weitere Informationen finden Sie im Handbuch [Testen und Senden einer neuen ](./submit.md)&quot;.
