---
title: Endpunkt der Regelkomponenten
description: Erfahren Sie, wie Sie den Endpunkt /rule_components in der Reactor-API aufrufen.
source-git-commit: 53612919dc040a8a3ad35a3c5c0991554ffbea7c
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 7%

---

# Endpunkt der Regelkomponenten

In Datenerfassungs-Tags steuern [rules](./rules.md) das Verhalten der Ressourcen in einer bereitgestellten [Bibliothek](./libraries.md). **Regelkomponenten** sind die einzelnen Teile, aus denen eine Regel besteht. Wenn eine Regel ein Rezept ist, ist eine Regelkomponente eine der Inhaltskomponenten. Mit dem Endpunkt `/rule_components` in der Reactor-API können Sie Regelkomponenten programmgesteuert verwalten.

>[!NOTE]
>
>In diesem Dokument wird beschrieben, wie Sie Regelkomponenten in der Reactor-API verwalten. Weitere Informationen zur Interaktion mit Regeln und Regelkomponenten in der Datenerfassungs-Benutzeroberfläche finden Sie im [UI-Handbuch](../../ui/managing-resources/rules.md).

Regelkomponenten haben drei grundlegende Typen:

| Komponententyp Regel | Beschreibung |
| --- | --- |
| Ereignisse | Ein Ereignis ist der Trigger für eine Regel. Die Regel beginnt, wenn das Ereignis zur Laufzeit auf dem Client-Gerät auftritt. Beispiele für Ereignisse sind &quot;[!UICONTROL Library Load]&quot;, &quot;[!UICONTROL Page Top]&quot;und &quot;[!UICONTROL Click]&quot;. |
| Bedingungen | Eine Bedingung ist eine Bewertung, ob bestimmte Kriterien erfüllt sind, bevor Aktionen ausgeführt werden. Sobald ein Ereignis eintritt, werden die Bedingungen ausgewertet. Die Aktionen der Regel werden nur ausgeführt, wenn alle Bedingungen erfüllt sind. |
| Aktionen | Dies sind die Aktionen, die die Regel tatsächlich durchführen soll, z. B. das Senden eines Adobe Analytics-Beacons, das Abrufen einer benutzerdefinierten Besucher-ID oder das Auslösen einer bestimmten Mbox. |

{style=&quot;table-layout:auto&quot;}

Eine Regelkomponente gehört genau zu einer Regel. Eine Regel kann (und sollte) viele Regelkomponenten enthalten.

Eine Regelkomponente wird von genau einer [Erweiterung](./extensions.md) bereitgestellt. Erweiterungen können viele Regelkomponenten bereitstellen.

## Erste Schritte 

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md) , um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Liste von Regelkomponenten abrufen {#list}

Sie können eine Liste von Regelkomponenten abrufen, die zu einer Regel gehören, indem Sie die Kennung der Regel in den Pfad einer GET-Anfrage einschließen.

**API-Format**

```http
GET /rules/{RULE_ID}/rule_components
```

| Parameter | Beschreibung |
| --- | --- |
| `RULE_ID` | Die `id` der Regel, deren Komponenten Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Mithilfe von Abfrageparametern können aufgelistete Regelkomponenten anhand der folgenden Attribute gefiltert werden:<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`negate`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>Weitere Informationen finden Sie im Handbuch zu [Filterantworten](../guides/filtering.md) .

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f51/rule_components \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Regelkomponenten für die angegebene Regel zurück.

```json
{
  "data": [
    {
      "id": "RC45944086902c4828b6e14ffbb40017f4",
      "type": "rule_components",
      "attributes": {
        "created_at": "2020-12-14T17:54:34.976Z",
        "delegate_descriptor_id": "kessel-test::events::click",
        "deleted_at": null,
        "dirty": true,
        "name": "My Example Click Event",
        "negate": false,
        "order": 0,
        "rule_order": 50.0,
        "timeout": 2000,
        "delay_next": true,
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:54:34.976Z",
        "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
      },
      "relationships": {
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/updated_with_extension"
          },
          "data": {
            "id": "EX6312cea676de47ad9f70b42f7c0fbf02",
            "type": "extensions"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/extension"
          },
          "data": {
            "id": "EXbfd099788024423ebdd49cf06b52e50a",
            "type": "extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/notes"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/origin"
          },
          "data": {
            "id": "RC45944086902c4828b6e14ffbb40017f4",
            "type": "rule_components"
          }
        },
        "rule component": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PRb1090b7443e948ac91650964b490e622"
          },
          "data": {
            "id": "PRb1090b7443e948ac91650964b490e622",
            "type": "properties"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/rules"
          }
        }
      },
      "links": {
        "extension": "https://reactor.adobe.io/extensions/EXbfd099788024423ebdd49cf06b52e50a",
        "origin": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4",
        "rules": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/rules",
        "self": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4"
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

## Nachschlagen einer Regelkomponente {#lookup}

Sie können eine Regelkomponente nachschlagen, indem Sie ihre Kennung im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /rule_components/{RULE_COMPONENT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `RULE_COMPONENT_ID` | Die `id` der Regelkomponente, die Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Regelkomponente zurück.

```json
{
  "data": {
    "id": "RC7be169fcfd534ffc82acc7bffdc50128",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:18.551Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:18.551Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/updated_with_extension"
        },
        "data": {
          "id": "EXa11e168f2ff2485197a493095269f964",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/extension"
        },
        "data": {
          "id": "EXa76eb16dd86849318b743494e75c33a1",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/origin"
        },
        "data": {
          "id": "RC7be169fcfd534ffc82acc7bffdc50128",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR00a35a74381443dc994e6b30b7152106"
        },
        "data": {
          "id": "PR00a35a74381443dc994e6b30b7152106",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXa76eb16dd86849318b743494e75c33a1",
      "origin": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128",
      "rules": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/rules",
      "self": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Erstellen einer Regelkomponente {#create}

Sie können eine neue Regelkomponente erstellen, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /rules/{RULE_ID}/rule_components
```

| Parameter | Beschreibung |
| --- | --- |
| `RULE_ID` | Die `id` der Regel, für die Sie eine Regelkomponente definieren. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage erstellt eine neue Regelkomponente für die angegebene Regel. Der Aufruf verknüpft die Regelkomponente auch mit einer vorhandenen Erweiterung über die Eigenschaft `relationships` . Weitere Informationen finden Sie im Handbuch zu [Beziehungen](../guides/relationships.md) .

```shell
curl -X POST \
  https://reactor.adobe.io/rules/RLf7b4f416b2e04ae1ba857ae681fee5bc/rule_components \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "delay_next": true,
            "order": 0,
            "rule_order": 50.0,
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}",
            "timeout": 2000
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EX31b8c49f134b4307924d71a64204099e",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLf7b4f416b2e04ae1ba857ae681fee5bc",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes.delegate_descriptor_id` | **(Erforderlich)** Die Typen von Regelkomponenten, die Sie definieren können, werden von  [Erweiterungspaketen](./extension-packages.md) bereitgestellt. Wenn Sie eine neue Regelkomponente erstellen, müssen Sie eine Delegate-Deskriptor-ID angeben, um anzugeben, auf welchem Erweiterungspaket diese Regelkomponente basiert, den Typ der Komponente (Ereignis, Bedingung oder Aktion) und den Namen der spezifischen Komponente, wie durch die Erweiterung definiert (z. B. das &quot;Klick&quot;-Ereignis in der Haupterweiterung).<br><br>Weitere Informationen finden Sie im Handbuch zu  [Delegate-Deskriptor-](../guides/delegate-descriptor-ids.md) IDs . |
| `attributes.name` | **(Erforderlich)** Ein für Menschen lesbarer Name für die Regelkomponente. |
| `attributes.delay_next` | Ein boolescher Wert, der anzeigt, ob spätere Aktionen verzögert werden sollen. |
| `attributes.order` | Eine Ganzzahl, die die Reihenfolge angibt, in der die Komponente nach Typ geladen werden soll. |
| `attributes.rule_order` | Eine Ganzzahl, die die Priorität angibt, mit der die verknüpfte Regel ausgelöst werden soll. |
| `attributes.settings` | Ein settings-JSON-Objekt, das als Zeichenfolge dargestellt wird. |
| `attributes.timeout` | Eine Ganzzahl, die die Zeitüberschreitung der Aktion angibt, die nacheinander ausgeführt wird. |
| `relationships` | Ein Objekt, das die erforderlichen Beziehungen für die Regelkomponente herstellt. Es müssen zwei Beziehungen hergestellt werden: <ol><li>`extension`: Die Erweiterung, die diese Regelkomponente definiert. Dies muss dieselbe Erweiterung sein, deren Erweiterungspaket durch das `delegate_descriptor_id` gekennzeichnet ist.</li><li>`rules`: Die Regel, unter der diese Komponente definiert wird. Muss dieselbe Regel-ID sein wie im Anfragepfad angegeben.</li></ol>Allgemeine Informationen zu Beziehungen finden Sie im [Beziehungshandbuch](../guides/relationships.md). |
| `type` | Der Typ der zu erstellenden Ressource. Für diesen Endpunkt muss der Wert `rule_components` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Regelkomponente zurück.

```json
{
  "data": {
    "id": "RC78c44af3cf7644e5927fc0ad61e88940",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:00.232Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:00.232Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/updated_with_extension"
        },
        "data": {
          "id": "EX0019a115a74f401fa0b9bb8f57a0196b",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/extension"
        },
        "data": {
          "id": "EX31b8c49f134b4307924d71a64204099e",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/origin"
        },
        "data": {
          "id": "RC78c44af3cf7644e5927fc0ad61e88940",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR97596432a82549ceb8e2a5d9df05c0e1"
        },
        "data": {
          "id": "PR97596432a82549ceb8e2a5d9df05c0e1",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EX31b8c49f134b4307924d71a64204099e",
      "origin": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940",
      "rules": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/rules",
      "self": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Aktualisieren einer Regelkomponente {#update}

Sie können eine Regelkomponente aktualisieren, indem Sie ihre ID in den Pfad einer PATCH-Anfrage einschließen.

>[!NOTE]
>
>Beim Aktualisieren einer Regelkomponente wird auch der Zeitstempel `updated_at` der übergeordneten Regel aktualisiert.

**API-Format**

```http
PATCH /rule_components/{RULE_COMPONENT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `RULE_COMPONENT_ID` | Die `id` der Regelkomponente, die Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert die Attribute `order` und `settings` für eine vorhandene Regelkomponente.

```shell
curl -X PATCH \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "order": 1,
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":false}"
          },
          "type": "rule_components",
          "id": "RC9af052ee231346f28d1e44865ab62c04"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes` | Ein Objekt, dessen Regelkomponenten die Attribute darstellen, die für die Regelkomponente aktualisiert werden sollen. Die folgenden Attribute können für eine Regelkomponente aktualisiert werden: <ul><li>`delay_next`</li><li>`delegate_descriptor_id`</li><li>`name`</li><li>`order`</li><li>`rule_order`</li><li>`settings`</li><li>`timeout`</li></ul> |
| `id` | Die `id` der Regelkomponente, die Sie aktualisieren möchten. Dies sollte mit dem Wert `{RULE_COMPONENT_ID}` übereinstimmen, der im Anfragepfad bereitgestellt wird. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `rule_components` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Regelkomponente zurück.

```json
{
  "data": {
    "id": "RC9af052ee231346f28d1e44865ab62c04",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:50.887Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 1,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:52.553Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":false}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/updated_with_extension"
        },
        "data": {
          "id": "EX468796dd09d743858f17d4c5ca52f3e0",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/extension"
        },
        "data": {
          "id": "EXcedb08a8265c488e8bb98b46245b2486",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/origin"
        },
        "data": {
          "id": "RC9af052ee231346f28d1e44865ab62c04",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR986402dc07834fbeb4789c56060dbf41"
        },
        "data": {
          "id": "PR986402dc07834fbeb4789c56060dbf41",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXcedb08a8265c488e8bb98b46245b2486",
      "origin": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04",
      "rules": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules",
      "self": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Löschen einer Regelkomponente

Sie können eine Regelkomponente löschen, indem Sie die zugehörige ID in den Pfad einer DELETE-Anfrage einschließen.

**API-Format**

```http
DELETE /rule_components/{RULE_COMPONENT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `RULE_COMPONENT_ID` | Die `id` der Regelkomponente, die Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück und zeigt an, dass die Regelkomponente gelöscht wurde.

## Hinweise für eine Regelkomponente verwalten {#notes}

Regelkomponenten sind &quot;wichtige&quot;Ressourcen, d. h. Sie können textbasierte Notizen für jede einzelne Ressource erstellen und abrufen. Weitere Informationen zum Verwalten von Notizen für Regelkomponenten und andere kompatible Ressourcen finden Sie im [Notes-Endpunkthandbuch](./notes.md) .

## Abrufen verwandter Ressourcen für eine Regelkomponente {#related}

Die folgenden Aufrufe zeigen, wie Sie die zugehörigen Ressourcen für eine Regelkomponente abrufen. Wenn [nach einer Regelkomponente](#lookup) sucht, werden diese Beziehungen unter der Regelkomponente `relationships` aufgeführt.

Weitere Informationen zu Beziehungen in der Reactor-API finden Sie im [Beziehungshandbuch](../guides/relationships.md) .

### Zugehörige Regeln für eine Regelkomponente auflisten {#rules}

Sie können die Regeln auflisten, die eine bestimmte Regelkomponente verwenden, indem Sie `/rules` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET  /rule_components/{RULE_COMPONENT_ID}/rules
```

| Parameter | Beschreibung |
| --- | --- |
| `{RULE_COMPONENT_ID}` | Die `id` der Regelkomponente, deren Regeln Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Regeln zurück, die die angegebene Regelkomponente verwenden.

```json
{
  "data": [
    {
      "id": "RLf1baa571748941db88f54de8efd119aa",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:58:36.072Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:58:37.452Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/property"
          },
          "data": {
            "id": "PR966c4a501e1a43a48cb55e104b4de935",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/origin"
          },
          "data": {
            "id": "RLf1baa571748941db88f54de8efd119aa",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR966c4a501e1a43a48cb55e104b4de935",
        "origin": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa",
        "self": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa",
        "rule_components": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ]
}
```

### Nachschlagen der zugehörigen Erweiterung für eine Regelkomponente {#extension}

Sie können die Erweiterung nachschlagen, die eine Regelkomponente bereitstellt, indem Sie `/extension` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET /rule_components/{RULE_COMPONENT_ID}/extension
```

| Parameter | Beschreibung |
| --- | --- |
| `{RULE_COMPONENT_ID}` | Die `id` der Regelkomponente, deren Erweiterung Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Erweiterung der angegebenen Regelkomponente zurück.

```json
{
  "data": {
    "id": "EX5644c3eed97d46b39cb2279ea11dde29",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:55:22.634Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:55:22.634Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/property"
        },
        "data": {
          "id": "PRcdb3d12504ce48ecbfa4fbbe5b80b6dd",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/origin"
        },
        "data": {
          "id": "EX5644c3eed97d46b39cb2279ea11dde29",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcdb3d12504ce48ecbfa4fbbe5b80b6dd",
      "origin": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29",
      "self": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### Nachschlagen der zugehörigen Herkunft für eine Regelkomponente {#origin}

Sie können die Herkunft (vorherige Revision) einer Regelkomponente nachschlagen, indem Sie `/origin` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET /rule_components/{RULE_COMPONENT_ID}/origin
```

| Parameter | Beschreibung |
| --- | --- |
| `{RULE_COMPONENT_ID}` | Die `id` der Regelkomponente, deren Ursprung Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Herkunft der angegebenen Regelkomponente zurück.

```json
{
  "data": {
    "id": "RC3d0805fde85d42db8988090bc074bb44",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:55:40.016Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": false,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:55:40.016Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/updated_with_extension"
        },
        "data": {
          "id": "EXb713fc209ce344c996bdeb377685e2c4",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/extension"
        },
        "data": {
          "id": "EXd6e1dce006b2412f874301e24d58ce24",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/origin"
        },
        "data": {
          "id": "RC3d0805fde85d42db8988090bc074bb44",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR89c66a560ec44928889b439333255efe"
        },
        "data": {
          "id": "PR89c66a560ec44928889b439333255efe",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXd6e1dce006b2412f874301e24d58ce24",
      "origin": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44",
      "rules": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/rules",
      "self": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```
