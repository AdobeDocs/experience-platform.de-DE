---
title: Hosts-Endpunkt
description: Erfahren Sie, wie Sie den /hosts-Endpunkt in der Reactor-API aufrufen.
exl-id: 9d0d2a65-49e9-429c-a665-754b59a11cf1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 100%

---

# Hosts-Endpunkt

>[!NOTE]
>
>Dieses Dokument beschreibt, wie Hosts in der Reactor-API verwaltet werden. Weitere allgemeine Informationen zu Hosts für Tags finden Sie im Handbuch [Hosts – Übersicht](../../ui/publishing/hosts/hosts-overview.md) in der Publishing-Dokumentation.

In der Reactor-API definiert ein Host ein Ziel, an dem ein [Build](./builds.md) bereitgestellt werden kann.

Wenn ein Build von einem Tags-Benutzer in Adobe Experience Platform angefordert wird, überprüft das System die Bibliothek, um zu bestimmen, in welcher [Umgebung](./environments.md) die Bibliothek erstellt werden soll. Jede Umgebung hat eine Beziehung zu einem Host, die angibt, wo der Build bereitgestellt werden soll.

Ein Host gehört genau zu einer [Eigenschaft](./properties.md), während eine Eigenschaft über viele Hosts verfügen kann. Eine Eigenschaft muss über mindestens einen Host verfügen, damit Sie veröffentlichen können.

Ein Host kann von mehr als einer Umgebung innerhalb einer Eigenschaft verwendet werden. Es ist üblich, nur einen einzelnen Host in einer Eigenschaft zu haben, und alle Umgebungen in dieser Eigenschaft verwenden denselben Host.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen einer Liste von Hosts {#list}

Sie können eine Liste von Hosts für eine Eigenschaft abrufen, indem Sie die ID der Eigenschaft im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| Parameter | Beschreibung |
| --- | --- |
| `PROPERTY_ID` | Die `id` der Eigenschaft, zu der die Hosts gehören. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Mithilfe von Abfrageparametern können die aufgelisteten Hosts anhand der folgenden Attribute gefiltert werden:<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>Weiterführende Informationen finden Sie im Handbuch zum [Filtern von Antworten](../guides/filtering.md).

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

Eine erfolgreiche Antwort gibt eine Liste von Hosts für die angegebene Eigenschaft zurück.

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

## Suchen eines Hosts {#lookup}

Sie können einen Host suchen, indem Sie dessen ID im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /hosts/{HOST_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `HOST_ID` | Die `id` des Hosts, den Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Hosts zurück.

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## Erstellen eines Hosts {#create}

Sie können einen neuen Host erstellen, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| Parameter | Beschreibung |
| --- | --- |
| `PROPERTY_ID` | Die `id` der [Eigenschaft](./properties.md), unter der Sie den Host definieren. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage erstellt einen neuen Host für die angegebene Eigenschaft. Der Aufruf verknüpft den Host auch mit einer vorhandenen Erweiterung über die Eigenschaft `relationships`. Weitere Informationen finden Sie im Handbuch zu [Beziehungen](../guides/relationships.md).

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes.name` | **(Erforderlich)** Ein für Menschen lesbarer Name für den Host. |
| `attributes.type_of` | **(Erforderlich)** Der Host-Typ. Kann eine von zwei Optionen sein: <ul><li>`akamai` für [von Adobe verwaltete Hosts](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` für [SFTP-Hosts](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | Ein optionaler privater Schlüssel, der für die Host-Authentifizierung verwendet werden soll. |
| `attributes.path` | Der Pfad, der an die URL `server` angehängt werden soll. |
| `attributes.port` | Eine Ganzzahl, die den zu verwendenden Serverport angibt. |
| `attributes.server` | Die Host-URL für den Server. |
| `attributes.username` | Ein optionaler Benutzername für die Authentifizierung. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `hosts` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Hosts zurück.

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## Aktualisieren eines Hosts {#update}

>[!NOTE]
>
>Nur SFTP-Hosts können aktualisiert werden.

Sie können einen Host aktualisieren, indem Sie dessen ID im Pfad einer PATCH-Anfrage angeben.

**API-Format**

```http
PATCH /hosts/{HOST_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `HOST_ID` | Die `id` des Hosts, den Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert den `name` für einen vorhandenen Host.

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes` | Ein Objekt, dessen Eigenschaften die Attribute darstellen, die für den Host aktualisiert werden sollen. Die folgenden Attribute können für einen Host aktualisiert werden: <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | Die `id` des Hosts, den Sie aktualisieren möchten. Diese sollte mit dem `{HOST_ID}`-Wert übereinstimmen, der im Anfragepfad angegeben ist. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `hosts` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Hosts zurück.

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## Löschen eines Hosts

Sie können einen Host löschen, indem Sie dessen ID im Pfad einer DELETE-Anfrage angeben.

**API-Format**

```http
DELETE /hosts/{HOST_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `HOST_ID` | Die `id` des Hosts, den Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück und zeigt an, dass der Host gelöscht wurde.

## Abrufen verwandter Ressourcen für einen Host {#related}

Die folgenden Aufrufe zeigen, wie Sie die zugehörigen Ressourcen für einen Host abrufen. Bei der [Suche nach einem Host](#lookup) werden diese Beziehungen unter der Eigenschaft `relationships` aufgeführt.

Weitere Informationen zu Beziehungen in der Reactor-API finden Sie im [Handbuch zu Beziehungen](../guides/relationships.md).

### Suchen der zugehörigen Eigenschaft für einen Host {#property}

Sie können die Eigenschaft suchen, der ein Host gehört, indem Sie `/property` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET /hosts/{HOST_ID}/property
```

| Parameter | Beschreibung |
| --- | --- |
| `{HOST_ID}` | Die `id` des Hosts, dessen Eigenschaft Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Eigenschaft des angegebenen Hosts zurück.

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
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
