---
title: Rules-Endpunkt
description: Erfahren Sie, wie Sie den /rules-Endpunkt in der Reactor-API aufrufen.
exl-id: 79ef4389-e4b7-461e-8579-16a1a78cdd43
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 98%

---

# Rules-Endpunkt

Im Kontext von Datenerfassungs-Tags steuern Regeln das Verhalten der Ressourcen in einer bereitgestellten Bibliothek. Eine Regel besteht aus einer oder mehreren [Regelkomponenten](./rule-components.md), die dazu dienen, die Regelkomponenten logisch miteinander zu verknüpfen. Mit dem `/rules`-Endpunkt in der Reactor-API können Sie Tag-Regeln programmgesteuert verwalten.

>[!NOTE]
>
>In diesem Dokument wird beschrieben, wie Sie Regeln in der Reactor-API verwalten. Informationen zur Interaktion mit Regeln in der Benutzeroberfläche finden Sie im Abschnitt [UI-Handbuch](../../ui/managing-resources/rules.md).

Eine Regel gehört zu genau einer [Eigenschaft](./properties.md). Eine Eigenschaft kann über viele Regeln verfügen.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen einer Liste von Regeln {#list}

Sie können eine Liste von Regeln abrufen, die zu einer Eigenschaft gehören, indem Sie eine GET-Anfrage ausführen.

**API-Format**

```http
GET /properties/{PROPERTY_ID}/rules
```

| Parameter | Beschreibung |
| --- | --- |
| `PROPERTY_ID` | Die `id` der Eigenschaft, deren Komponenten Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Mithilfe von Abfrageparametern können aufgelistete Regeln anhand der folgenden Attribute gefiltert werden:<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>Weitere Informationen finden Sie in der Anleitung zum [Filtern von Antworten](../guides/filtering.md).

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

Eine erfolgreiche Antwort gibt eine Liste von Regeln für die angegebene Eigenschaft zurück.

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

## Suchen einer Entscheidungsregel {#lookup}

Sie können eine Regel suchen, indem Sie ihre ID im Pfad einer GET-Anfrage angeben.

>[!NOTE]
>
>Wenn Regeln gelöscht werden, werden sie als gelöscht markiert, aber nicht tatsächlich aus dem System entfernt. Daher ist es möglich, eine gelöschte Regel abzurufen. Gelöschte Regeln können durch das Vorhandensein einer `meta.deleted_at`-Eigenschaft identifiziert werden.

**API-Format**

```http
GET /rules/{RULE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `RULE_ID` | Die `id` der Regel, die Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Regel zurück.

```json
{
  "data": {
    "id": "RL14dc6a8c37b14b619ddb2b3ba489a1f5",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:56:33.188Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:56:33.188Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/property"
        },
        "data": {
          "id": "PRfa164e39b0d74eb5b093ab963b1f1200",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/origin"
        },
        "data": {
          "id": "RL14dc6a8c37b14b619ddb2b3ba489a1f5",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRfa164e39b0d74eb5b093ab963b1f1200",
      "origin": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5",
      "self": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5",
      "rule_components": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Erstellen einer Regel {#create}

Sie können eine neue Regel erstellen, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /properties/{PROPERTY_ID}/rules
```

| Parameter | Beschreibung |
| --- | --- |
| `PROPERTY_ID` | Die `id` der Eigenschaft, unter der Sie eine Regel definieren. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example Rule",
            "enabled": true,
          },
          "type": "rules"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes.name` | **(Erforderlich)** Ein für Menschen lesbarer Name für die Regel. |
| `attributes.enabled` | Ein boolescher Wert, der angibt, ob die Regel aktiviert ist. |
| `type` | Der Typ der zu erstellenden Ressource. Für diesen Endpunkt muss der Wert `rules` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Regel zurück.

```json
{
  "data": {
    "id": "RL52d156a9074844b89ca20c987dbafd3b",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:31:46.883Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:31:46.883Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/property"
        },
        "data": {
          "id": "PR03cc61073ef74fd2af21e4cfb6ed97a7",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/origin"
        },
        "data": {
          "id": "RL52d156a9074844b89ca20c987dbafd3b",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7",
      "origin": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "self": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "rule_components": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Hinzufügen von Ereignissen, Bedingungen und Aktionen zu einer Regel {#components}

Nachdem Sie [eine Regel erstellt](#create) haben, können Sie mit der Erstellung der Logik beginnen, indem Sie Ereignisse, Bedingungen und Aktionen hinzufügen (zusammen als Regelkomponenten bezeichnet). Weitere Informationen dazu finden Sie im Abschnitt [Erstellen einer Regelkomponente](./rule-components.md#create) im Handbuch zum `/rule_components`-Endpunkt.

## Aktualisieren einer Regel {#update}

Sie können die Attribute einer Regel aktualisieren, indem Sie deren ID im Pfad einer PATCH-Anfrage angeben.

**API-Format**

```http
PATCH /rules/{RULE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `RULE_ID` | Die `id` der Regel, die Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert den `name` einer vorhandenen Regel.

```shell
curl -X PATCH \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
  "data": {
    "attributes": {
      "name": "Test Rule"
    },
    "id": "RLd2528a53c21a468f93cfd85244f16fdd",
    "type": "rules"
  }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes` | Ein Objekt, dessen Regeln die Attribute darstellen, die für die Regel aktualisiert werden sollen. Die folgenden Attribute können für eine Regel aktualisiert werden: <ul><li>`name`</li><li>`enabled`</li></ul> |
| `id` | Die `id` der Regel, die Sie aktualisieren möchten. Diese sollte mit dem `{RULE_ID}`-Wert übereinstimmen, der im Anfragepfad angegeben ist. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `rules` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Regel zurück.

```json
{
  "data": {
    "id": "RLd2528a53c21a468f93cfd85244f16fdd",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:56:55.026Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Test Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:56:55.717Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/property"
        },
        "data": {
          "id": "PR7e37a33354cc4aa7880f2a550c4f844f",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/origin"
        },
        "data": {
          "id": "RLd2528a53c21a468f93cfd85244f16fdd",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR7e37a33354cc4aa7880f2a550c4f844f",
      "origin": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd",
      "self": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd",
      "rule_components": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Löschen einer Regel

Sie können eine Regel löschen, indem Sie deren ID im Pfad einer DELETE-Anfrage angeben.

**API-Format**

```http
DELETE /rules/{RULE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `RULE_ID` | Die `id` der Regel, die Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück und zeigt an, dass die Regel gelöscht wurde.

## Verwalten von Anmerkungen für eine Regel {#notes}

Sie können für jede einzelne Regel textbasierte Anmerkungen erstellen und abrufen. Weitere Informationen zum Verwalten von Anmerkungen für Regeln und andere kompatible Ressourcen finden Sie im [Handbuch zum notes-Endpunkt](./notes.md).

## Abrufen verwandter Ressourcen für eine Regel {#related}

Die folgenden Aufrufe zeigen, wie Sie die zugehörigen Ressourcen für eine Regel abrufen. Beim [Suchen nach einer Regel](#lookup) werden diese Beziehungen unter der Regel `relationships` aufgeführt.

Weitere Informationen zu Beziehungen in der Reactor-API finden Sie im [Handbuch zu Beziehungen](../guides/relationships.md).

### Auflisten der zugehörigen Bibliotheken für eine Regel {#libraries}

Sie können die Bibliotheken auflisten, die eine bestimmte Regel verwenden, indem Sie `/libraries` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET  /rules/{RULE_ID}/libraries
```

| Parameter | Beschreibung |
| --- | --- |
| `{RULE_ID}` | Die `id` der Regel, deren Bibliotheken Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Bibliotheken zurück, die die angegebene Regel verwenden.

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
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

### Auflisten der zugehörigen Revisionen für eine Regel {#revisions}

Sie können die Revisionen für eine Regel auflisten, indem Sie `/revisions` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET  /rules/{RULE_ID}/revisions
```

| Parameter | Beschreibung |
| --- | --- |
| `{RULE_ID}` | Die `id` der Regel, deren Revisionen Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Revisionen zurück, die die angegebene Regel verwenden.

```json
{
  "data": [
    {
      "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:57:29.835Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:57:29.835Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/property"
          },
          "data": {
            "id": "PR391208e5ea96442ea7903fe3f33f50e7",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/origin"
          },
          "data": {
            "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR391208e5ea96442ea7903fe3f33f50e7",
        "origin": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "self": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "rule_components": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/rule_components"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "RL6e5cb0d1c74542d6a3d04d08c6bb97ae",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:57:30.528Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:57:30.528Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/property"
          },
          "data": {
            "id": "PR391208e5ea96442ea7903fe3f33f50e7",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/origin"
          },
          "data": {
            "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR391208e5ea96442ea7903fe3f33f50e7",
        "origin": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "self": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae",
        "rule_components": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/rule_components"
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
      "total_count": 2
    }
  }
}
```

### Suchen des zugehörigen Ursprungs für eine Regel {#origin}

Sie können den Ursprung (frühere Version) einer Regel suchen, indem Sie `/origin` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET /rules/{RULE_ID}/origin
```

| Parameter | Beschreibung |
| --- | --- |
| `{RULE_ID}` | Die `id` der Regel, deren Ursprung Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Erweiterung der angegebenen Regel zurück.

```json
{
  "data": {
    "id": "RLb83ed2278dc045628c069ab7eb9bb866",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:57:41.517Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:57:41.517Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/property"
        },
        "data": {
          "id": "PR169d832d20ea4243b5a5db0ccc5aae9c",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/origin"
        },
        "data": {
          "id": "RLb83ed2278dc045628c069ab7eb9bb866",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR169d832d20ea4243b5a5db0ccc5aae9c",
      "origin": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866",
      "self": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866",
      "rule_components": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/rule_components"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### Suchen der zugehörigen Eigenschaft für eine Regel {#property}

Sie können die Eigenschaft suchen, der eine Regel gehört, indem Sie `/property` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET /rules/{RULE_ID}/property
```

| Parameter | Beschreibung |
| --- | --- |
| `{RULE_ID}` | Die `id` der Regel, deren Eigenschaft Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RC3d0805fde85d42db8988090bc074bb44/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Eigenschaft der angegebenen Regel zurück.

```json
{
  "data": {
    "id": "PR8ac25b57d5c24ebab68ffe5c630fc690",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:53:19.088Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:53:19.088Z",
      "platform": "web",
      "development": false,
      "token": "97b2cb1177df",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/environments",
      "extensions": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/extensions",
      "rules": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/rules",
      "self": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690"
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
