---
title: Anmerkungen-Endpunkt
description: Erfahren Sie, wie Sie Aufrufe an den Endpunkt /notes in der Reactor-API durchführen.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 8%

---

# Anmerkungen-Endpunkt

In der Reactor-API sind Notizen Kommentare in Textform, die Sie bestimmten Ressourcen hinzufügen können. Anmerkungen sind im Wesentlichen Kommentare zu ihren jeweiligen Ressourcen. Der Inhalt von Notizen hat keine Auswirkungen auf das Ressourcenverhalten und kann für verschiedene Anwendungsfälle verwendet werden, darunter die folgenden:

* Bereitstellung von Hintergrundinformationen
* Funktionsweise von Aufgabenlisten
* Weitergeben von Ratschlägen zur Ressourcennutzung
* Anweisungen für andere Teammitglieder geben
* Verlaufskontext aufzeichnen

Mit dem Endpunkt `/notes` in der Reactor-API können Sie diese Notizen programmgesteuert verwalten.

Anmerkungen können auf die folgenden Ressourcen angewendet werden:

* [Datenelemente](./data-elements.md)
* [Erweiterungen](./extensions.md)
* [Bibliotheken](./libraries.md)
* [Eigenschaften](./properties.md)
* [Regel Komponenten](./rule-components.md)
* [Regeln](./rules.md)

Diese sechs Typen werden zusammen als &quot;bemerkenswerte&quot;Ressourcen bezeichnet. Wenn eine wichtige Ressource gelöscht wird, werden auch die zugehörigen Hinweise gelöscht.

>[!NOTE]
>
>Für Ressourcen, die mehrere Revisionen aufweisen können, müssen alle Notizen für die aktuelle (head) Revision erstellt werden. Sie dürfen nicht an andere Revisionen angehängt werden.
>
>Anmerkungen können jedoch weiterhin aus Revisionen gelesen werden. In solchen Fällen gibt die API nur die Hinweise zurück, die vor der Erstellung der Revision existierten. Sie zeigen eine Momentaufnahme der Anmerkungen an, die zum Zeitpunkt der Kürzung der Revision vorgenommen wurden. Im Gegensatz dazu werden beim Lesen von Notizen aus der aktuellen (head-)Revision alle zugehörigen Anmerkungen zurückgegeben.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md) , um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Liste mit Anmerkungen abrufen {#list}

Sie können eine Liste mit Hinweisen für eine Ressource abrufen, indem Sie `/notes` an den Pfad einer Ressourcenanforderung für die betreffende GET anhängen.

**API-Format**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parameter | Beschreibung |
| --- | --- |
| `RESOURCE_TYPE` | Der Ressourcentyp, für den Sie Notizen abrufen. Muss einer der folgenden Werte sein: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | Die `id` der spezifischen Ressource, deren Anmerkungen Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage listet die Anmerkungen auf, die an eine Bibliothek angehängt sind.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste mit Anmerkungen zurück, die an die angegebene Ressource angehängt sind.

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

## Notiz nachschlagen {#lookup}

Sie können eine Notiz nachschlagen, indem Sie ihre ID im Pfad einer GET-Anfrage angeben.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Notiz zurück.

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
>Beachten Sie vor der Erstellung einer neuen Notiz, dass Notizen nicht bearbeitbar sind. Sie können sie nur löschen, indem Sie die entsprechende Ressource löschen.

Sie können eine neue Anmerkung erstellen, indem Sie `/notes` an den Pfad einer Ressourcenanforderung für die betreffende POST anhängen.

**API-Format**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parameter | Beschreibung |
| --- | --- |
| `RESOURCE_TYPE` | Der Ressourcentyp, für den Sie eine Notiz erstellen. Muss einer der folgenden Werte sein: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | Die `id` der spezifischen Ressource, für die Sie eine Notiz erstellen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage erstellt eine neue Notiz für eine Eigenschaft.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `attributes.text` | **(Erforderlich)** Der Text, der die Notiz enthält. Jeder Hinweis ist auf 512 Unicode-Zeichen begrenzt. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Notiz zurück.

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
