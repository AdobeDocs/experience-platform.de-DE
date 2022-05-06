---
title: Notes-Endpunkt
description: Erfahren Sie, wie Sie den /notes-Endpunkt in der Reactor-API abrufen.
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 100%

---

# Notes-Endpunkt

In der Reactor-API sind Anmerkungen textuelle Kommentare, die Sie zu bestimmten Ressourcen hinzufügen können. Anmerkungen sind im Wesentlichen Kommentare zu ihren jeweiligen Ressourcen. Der Inhalt von Anmerkungen hat keinen Einfluss auf das Verhalten von Ressourcen und kann für eine Vielzahl von Anwendungsfällen verwendet werden, z. B. für die folgenden:

* Bereitstellung von Hintergrundinformationen
* Funktion als To-Do-Listen
* Weitergabe von Hinweisen zur Ressourcenverwendung
* Erteilen von Anweisungen an andere Team-Mitglieder
* Aufzeichnung von historischem Kontext

Der `/notes`-Endpunkt in der Reactor-API erlaubt es Ihnen, diese Notizen programmgesteuert zu verwalten.

Anmerkungen können auf die folgenden Ressourcen angewendet werden:

* [Datenelemente](./data-elements.md)
* [Erweiterungen](./extensions.md)
* [Bibliotheken](./libraries.md)
* [Eigenschaften](./properties.md)
* [Regel Komponenten](./rule-components.md)
* [Regeln](./rules.md)
* [Geheime Daten](./secrets.md)

Diese sechs Typen sind Ressourcen, die mit Anmerkungen versehen werden können. Wenn Ressource, die mit Anmerkungen versehen werden kann, gelöscht wird, werden auch die zugehörigen Anmerkungen gelöscht.

>[!NOTE]
>
>Bei Ressourcen, die mehrere Revisionen haben können, müssen alle Anmerkungen in der aktuellen (Haupt-)Revision erstellt werden. Sie dürfen nicht an andere Revisionen angehängt werden.
>
>Anmerkungen können jedoch weiterhin aus Revisionen gelesen werden. In solchen Fällen gibt die API nur die Notizen zurück, die vor der Erstellung der Revision existierten. Sie bieten eine Momentaufnahme der Anmerkungen, wie sie zum Zeitpunkt der Kürzung der Revision aussahen. Im Gegensatz dazu werden beim Lesen von Anmerkungen aus der aktuellen (Haupt-)Revision alle Anmerkungen zurückgegeben.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen einer Liste von Anmerkungen {#list}

Sie können eine Liste mit Anmerkungen für eine Ressource abrufen, indem Sie `/notes` an den Pfad einer GET-Anfrage für die betreffende Ressource anhängen.

**API-Format**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parameter | Beschreibung |
| --- | --- |
| `RESOURCE_TYPE` | Der Typ der Ressource, für die Sie Anmerkungen abrufen. Muss einer der folgenden Werte sein: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | Die `id` der spezifischen Ressource, deren Anmerkungen Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Abfrage listet die Anmerkungen auf, die an eine Bibliothek angehängt sind.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Anmerkungen zurück, die an die angegebene Ressource angehängt sind.

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
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

## Suchen einer Anmerkung {#lookup}

Sie können eine Anmerkung nachschlagen, indem Sie ihre ID im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /notes/{NOTE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `NOTE_ID` | Die `id` der Anmerkung, die Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Anmerkung zurück.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## Anmerkungen erstellen {#create}

>[!WARNING]
>
>Bevor Sie eine neue Anmerkung erstellen, bedenken Sie, dass Anmerkungen nicht bearbeitet werden können und die einzige Möglichkeit, sie zu löschen, darin besteht, die zugehörige Ressource zu löschen.

Sie können eine neue Anmerkung anlegen, indem Sie `/notes` an den Pfad einer POST-Anfrage für die betreffende Ressource anhängen.

**API-Format**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parameter | Beschreibung |
| --- | --- |
| `RESOURCE_TYPE` | Der Typ der Ressource, für die Sie eine Anmerkung erstellen. Muss einer der folgenden Werte sein: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | Die `id` der spezifischen Ressource, für die Sie eine Anmerkung erstellen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage erstellt eine neue Anmerkung für eine Eigenschaft.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `type` | **(Erforderlich)** Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `notes` lauten. |
| `attributes.text` | **(Erforderlich)** Der Text, aus dem die Anmerkung besteht. Jede Anmerkung ist auf 512 Unicode-Zeichen begrenzt. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Anmerkung zurück.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
