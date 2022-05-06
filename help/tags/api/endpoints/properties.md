---
title: Properties-Endpunkt
description: Erfahren Sie, wie Sie den /properties-Endpunkt in der Reactor-API aufrufen.
exl-id: 7830c519-312f-4f73-b3f5-64ab0420d902
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 100%

---

# Properties-Endpunkt

Eine Eigenschaft ist ein Container-Konstrukt, das die meisten anderen Ressourcen enthält, die in der Reactor-API verfügbar sind. Sie verwalten Eigenschaften programmgesteuert mithilfe des `/properties`-Endpunkts.

In der Ressourcenhierarchie ist eine Eigenschaft der Eigentümer der folgenden Elemente:

* [Builds](./builds.md)
* [Callbacks](./callbacks.md)
* [Datenelemente](./data-elements.md)
* [Umgebungen](./environments.md)
* [Erweiterungen](./extensions.md)
* [Hosts](./properties.md)
* [Bibliotheken](./libraries.md)
* [Regel  Komponenten](./rule-components.md)
* [Regeln](./rules.md)

Eine Eigenschaft gehört zu genau einem [Unternehmen](./companies.md). Ein Unternehmen kann über viele Eigenschaften verfügen.

Weitere allgemeine Informationen zu Eigenschaften und ihrer Rolle im Tag-Management finden Sie in der Übersicht zu [Unternehmen und Eigenschaften](../../ui/administration/companies-and-properties.md).

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen einer Liste von Eigenschaften {#list}

Sie können eine Liste von Eigenschaften abrufen, die zu einem Unternehmen gehören, indem Sie die ID des Unternehmens im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /companies/{COMPANY_ID}/properties
```

| Parameter | Beschreibung |
| --- | --- |
| `COMPANY_ID` | Die `id` des Unternehmens, dem die Eigenschaften gehören, die Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Mithilfe von Abfrageparametern können aufgelistete Eigenschaften anhand der folgenden Attribute gefiltert werden:<ul><li>`copying`</li><li>`created_at`</li><li>`enabled`</li><li>`name`</li><li>`platform`</li><li>`token`</li><li>`updated_at`</li></ul>Weiterführende Informationen finden Sie im Handbuch zum [Filtern von Antworten](../guides/filtering.md).

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Eigenschaften für das angegebene Unternehmen zurück.

```json
{
  "data": [
    {
      "id": "PR29e066628dcf4ba0a16780b2e339821c",
      "type": "properties",
      "attributes": {
        "created_at": "2020-12-14T17:51:28.215Z",
        "enabled": true,
        "name": "Kessel Example Property",
        "updated_at": "2020-12-14T17:51:28.215Z",
        "platform": "web",
        "development": false,
        "token": "30a138ca7f5b",
        "domains": [
          "example.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments",
        "extensions": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions",
        "rules": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules",
        "self": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c"
      },
      "meta": {
        "rights": [
          "approve",
          "develop",
          "manage_environments",
          "manage_extensions",
          "publish"
        ]
      }
    },
    {
      "id": "PR0c559a62480142a7b9be4a118d1a0448",
      "type": "properties",
      "attributes": {
        "created_at": "2020-08-14T15:29:34.241Z",
        "enabled": true,
        "name": "new prop",
        "updated_at": "2020-08-14T15:29:34.241Z",
        "platform": "web",
        "development": true,
        "token": "b6cee01dedb7",
        "domains": [
          "google.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments",
        "extensions": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions",
        "rules": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules",
        "self": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448"
      },
      "meta": {
        "rights": [
          "approve",
          "develop",
          "manage_environments",
          "manage_extensions",
          "publish"
        ]
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

## Suchen einer Eigenschaft {#lookup}

Sie können eine Eigenschaft suchen, indem Sie ihre ID im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /properties/{PROPERTY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `PROPERTY_ID` | Die `id` der Eigenschaft, die Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Eigenschaft zurück.

```json
{
  "data": {
    "id": "PR48ade10e6acf4385ba96214e9f5d31e1",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:18.725Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:18.725Z",
      "platform": "web",
      "development": false,
      "token": "c54ba5e843e6",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments",
      "extensions": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions",
      "rules": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules",
      "self": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## Erstellen einer Eigenschaft {#create}

Sie können eine neue Eigenschaft erstellen, indem Sie eine POST-Anfrage ausführen.

**API-Format**

```http
POST /company/{COMPANY_ID}/properties
```

| Parameter | Beschreibung |
| --- | --- |
| `COMPANY_ID` | Die `id` des Unternehmens, unter dem Sie die Eigenschaft definieren. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage erstellt eine neue Eigenschaft für die angegebene Eigenschaft. Der Aufruf verknüpft die Eigenschaft auch mit einer vorhandenen Erweiterung über die Eigenschaft `relationships`. Weitere Informationen finden Sie im Handbuch zu [Beziehungen](../guides/relationships.md).

```shell
curl -X POST \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Example Property",
            "platform": "web"
            "domains": [
              "example.com"
            ],
            "privacy": "gdpr",
            "rule_component_sequencing_enabled": false,
            "ssl_enabled": false,
            "undefined_vars_return_empty": true
          },
          "type": "properties"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes.name` | **(Erforderlich)** Ein für Menschen lesbarer Name für die Eigenschaft. |
| `attributes.platform` | **(Erforderlich)** Die Plattform für die Eigenschaft. Kann entweder `web` für Web-Eigenschaften sein oder `mobile` oder `edge` für Mobile-Eigenschaften. |
| `attributes.domains` | **(Erforderlich für Web-Eigenschaften)** Ein Array von URL-Domains für die Eigenschaft. |
| `attributes.development` | Ein boolescher Wert, der anzeigt, ob es sich um eine Entwicklungseigenschaft handelt. |
| `attributes.privacy` | Eine Zeichenfolge, die verwendet werden kann, um datenschutzbezogene Überlegungen für die Eigenschaft zu referenzieren. |
| `attributes.rule_component_sequencing_enabled` | Ein boolescher Wert, der angibt, ob die Sequenzierung von Regelkomponenten für diese Eigenschaft aktiviert werden soll. |
| `attributes.ssl_enabled` | Ein boolescher Wert, der angibt, ob SSL (Secure Sockets Layer) für diese Eigenschaft aktiviert werden soll. |
| `attributes.undefined_vars_return_empty` | Ein boolescher Wert dafür, ob nicht definierte Variablen für diese Eigenschaft als leer zurückgegeben werden sollen. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `properties` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Eigenschaft zurück.

```json
{
  "data": {
    "id": "PR505e39de0d0042d1b22321e7767edb4d",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:31:31.579Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:31:31.579Z",
      "platform": "web",
      "development": false,
      "token": "a969ffc6f872",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments",
      "extensions": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions",
      "rules": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules",
      "self": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## Aktualisieren einer Eigenschaft {#update}

Sie können eine Eigenschaft aktualisieren, indem Sie deren ID im Pfad einer PATCH-Anfrage angeben.

**API-Format**

```http
PATCH /properties/{PROPERTY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `PROPERTY_ID` | Die `id` der Eigenschaft, die Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert den `name` und die `domains` für eine vorhandene Eigenschaft.

```shell
curl -X PATCH \
  https://reactor.adobe.io/properties/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Property B",
            "domains": [
              "example.com"
            ]
          },
          "id": "PR541dbb24bad54dceb04710d7a9e7a740",
          "type": "properties"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes` | Ein Objekt, dessen Eigenschaften die Attribute darstellen, die für die Eigenschaft aktualisiert werden sollen. Die folgenden Attribute können für eine Eigenschaft aktualisiert werden: <ul><li>`development`</li><li>`domains`</li><li>`name`</li><li>`platform`</li><li>`privacy`</li><li>`rule_component_sequencing_enabled`</li><li>`ssl_enabled`</li><li>`undefined_vars_return_empty`</li></ul> |
| `id` | Die `id` der Eigenschaft, die Sie aktualisieren möchten. Diese sollte mit dem `{PROPERTY_ID}`-Wert übereinstimmen, der im Anfragepfad angegeben ist. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `properties` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Eigenschaft zurück.

```json
{
  "data": {
    "id": "PR541dbb24bad54dceb04710d7a9e7a740",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:37.386Z",
      "enabled": true,
      "name": "Kessel Property B",
      "updated_at": "2020-12-14T17:51:43.062Z",
      "platform": "web",
      "development": false,
      "token": "3f2d8630a8d3",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments",
      "extensions": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions",
      "rules": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules",
      "self": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## Löschen von Properties

Sie können eine Eigenschaft löschen, indem Sie deren ID im Pfad einer DELETE-Anfrage angeben.

**API-Format**

```http
DELETE /properties/{PROPERTY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `PROPERTY_ID` | Die `id` der Eigenschaft, die Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück und zeigt an, dass die Eigenschaft gelöscht wurde.

## Verwalten von Hinweisen für eine Eigenschaft {#notes}

Sie können für jede einzelne Eigenschaft textbasierte Anmerkungen erstellen und abrufen. Weitere Informationen zum Verwalten von Notizen für Eigenschaften und andere kompatible Ressourcen finden Sie im [Handbuch zum notes-Endpunkt](./notes.md).

## Abrufen verwandter Ressourcen für eine Eigenschaft {#related}

Die folgenden Aufrufe zeigen, wie Sie die zugehörigen Ressourcen für eine Eigenschaft abrufen. Beim [Suchen nach einer Eigenschaft](#lookup) werden diese Beziehungen unter der Eigenschaft `relationships` aufgeführt.

Weitere Informationen zu Beziehungen in der Reactor-API finden Sie im [Handbuch zu Beziehungen](../guides/relationships.md).

### Auflisten der zugehörigen Callbacks für eine Eigenschaft {#callbacks}

Sie können die in einer Eigenschaft registrierten [Callbacks](./callbacks.md) auflisten, indem Sie `/callbacks` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `id` der Eigenschaft, deren Callbacks Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Callbacks zurück, die der angegebenen Eigenschaft gehören.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Auflisten der zugehörigen Datenelemente für eine Eigenschaft {#data-elements}

Sie können die [Datenelemente](./data-elements.md), die einer Eigenschaft gehören, auflisten, indem Sie `/data_elements` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET  /properties/{PROPERTY_ID}/data_elements
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `id` der Eigenschaft, deren Datenelemente Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Datenelementen zurück, die der angegebenen Eigenschaft gehören.

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:36:08 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Auflisten der zugehörigen Umgebungen für eine Eigenschaft {#environments}

Sie können die [Umgebungen](./environments.md) auflisten, die einer Eigenschaft gehören, indem Sie `/environments` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET  /properties/{PROPERTY_ID}/environments
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `id` der Eigenschaft, deren Umgebungen Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Umgebungen zurück, die der angegebenen Eigenschaft gehören.

```json
{
  "data": [
    {
      "id": "ENbe322acb4fc64dfdb603254ffe98b5d3",
      "type": "environments",
      "attributes": {
        "archive": false,
        "created_at": "2020-12-14T17:38:51.047Z",
        "library_path": "f9fd106ab399/cb29d726b35e",
        "library_name": "launch-c0331746ae03-development.min.js",
        "library_entry_points": [
          {
            "library_name": "launch-c0331746ae03-development.min.js",
            "minified": true,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.min.js"
            ],
            "license_path": "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
          },
          {
            "library_name": "launch-c0331746ae03-development.js",
            "minified": false,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
            ]
          }
        ],
        "name": "Development Environment A",
        "path": "https://assets.adobedtm.com/staging",
        "stage": "development",
        "updated_at": "2020-12-14T17:38:51.047Z",
        "status": "succeeded",
        "token": "c0331746ae03"
      },
      "relationships": {
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/library"
          },
          "data": null
        },
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/builds"
          }
        },
        "host": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/host",
            "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/relationships/host"
          },
          "data": {
            "id": "HTc5cae9ce1e3943aab185bdba939f98bd",
            "type": "hosts"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/property"
          },
          "data": {
            "id": "PR06c9196bc57048dd8ff169c27baeeca8",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8",
        "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3"
      },
      "meta": {
        "archive_encrypted": false
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Auflisten der zugehörigen Erweiterungen für eine Eigenschaft {#extensions}

Sie können die [Erweiterungen](./extensions.md) auflisten, die einer Eigenschaft gehören, indem Sie `/extensions` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET  /properties/{PROPERTY_ID}/extensions
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `id` der Eigenschaft, deren Erweiterungen Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Erweiterungen zurück, die der angegebenen Eigenschaft gehören.

```json
{
  "data": [
    {
      "id": "EXd9d80c87afb6432ba823a58d3e78299b",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:40:21.000Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:40:21.000Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/property"
          },
          "data": {
            "id": "PRee071cb5b7794f42b74c913e1ad2e325",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/origin"
          },
          "data": {
            "id": "EXd9d80c87afb6432ba823a58d3e78299b",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325",
        "origin": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "self": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Auflisten der zugehörigen Hosts für eine Eigenschaft {#hosts}

Sie können die von einer Eigenschaft verwendeten [Hosts](./hosts.md) auflisten, indem Sie `/hosts` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET  /properties/{PROPERTY_ID}/hosts
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `id` der Eigenschaft, deren Hosts Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Hosts zurück, die von einer angegebenen Eigenschaft verwendet werden.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Auflisten der zugehörigen Regeln für eine Eigenschaft {#rules}

Sie können die von einer Eigenschaft verwendeten [Regeln](./rules.md) auflisten, indem Sie `/rules` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET  /properties/{PROPERTY_ID}/rules
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `id` der Eigenschaft, deren Regeln Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Regeln zurück, die von einer angegebenen Eigenschaft verwendet werden.

```json
{
  "data": [
    {
      "id": "RL8429f3fee98b44c68f7a538e68e21747",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:56:44.109Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:56:44.109Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/property"
          },
          "data": {
            "id": "PR41f64d2a9d9b4862b0582c5ff6a07504",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/origin"
          },
          "data": {
            "id": "RL8429f3fee98b44c68f7a538e68e21747",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504",
        "origin": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "self": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "rule_components": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Suchen des verbundenen Unternehmens für eine Eigenschaft {#company}

Sie können das Unternehmen suchen, dem eine Eigenschaft gehört, indem Sie `/company` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET /properties/{PROPERTY_ID}/company
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `id` der Eigenschaft, deren Unternehmen Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/HT5d90148e72224224aac9bc0b01498b84/company \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Unternehmens der angegebenen Eigenschaft zurück.

```json
{
  "data": {
    "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.711Z",
      "name": "Reactor QE",
      "org_id": "08364A825824E04F0A494115@AdobeOrg",
      "updated_at": "2020-08-13T17:13:30.711Z",
      "token": "f9fd106ab399",
      "cjm_enabled": true,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "properties": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties",
        "manage_app_configurations"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ]
      }
    }
  }
}
```
