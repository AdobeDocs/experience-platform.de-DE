---
title: Endpunkt für Autorisierungen der Verwendung von Erweiterungspaketen
description: Erfahren Sie, wie Sie den /extension_package_usage-Autorisierungs-Endpunkt in der Reactor-API aufrufen.
exl-id: ad3fb704-7d2f-45ec-b80b-ea4d327f2205
source-git-commit: 9cdd349e0eccb4498d88f24a84b0f1c116b0adfe
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 16%

---

# Endpunkt für Autorisierungen der Verwendung von Erweiterungspaketen

Ein Erweiterungspaket stellt eine [Erweiterung](./extensions.md) dar, die von einem Erweiterungsentwickler verfasst wurde. Zusätzliche Funktionen, die Tag-Benutzern zur Verfügung gestellt werden können, werden durch ein Erweiterungspaket definiert. Diese Funktionen können Hauptmodule und freigegebene Module enthalten, obwohl sie meist als [Regelkomponenten“ (](./rule-components.md), Bedingungen und Aktionen) und [Datenelemente](./data-elements.md) bereitgestellt werden.

Ein Erweiterungspaket ist im Besitz des ([) &#x200B;](./companies.md). Besitzer von Erweiterungspaketen können andere Unternehmen autorisieren, ihre privaten Versionen der Pakete zu verwenden. Jedes autorisierte Unternehmen erhält eine Nutzungsautorisierung für ein einzelnes Erweiterungspaket, das für alle zukünftigen und aktuellen privaten Versionen des Pakets gültig ist.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen von Berechtigungen zur Verwendung von Erweiterungspaketen für ein Erweiterungspaket {#list}

Um eine Liste von Nutzungsberechtigungen für ein Erweiterungspaket abzurufen, stellen Sie eine GET-Anfrage an den folgenden Endpunkt.

**API-Format**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `ID` der Eigenschaft, deren Autorisierung zur Verwendung des Erweiterungspakets Sie auflisten möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Erweiterungspaketen zurück.

```json
{
  "data": [
    {
      "id": "EA722482c30fe44b54aa6a7317890b3bdb",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:35.776Z",
        "updated_at": "2024-06-05T23:17:35.776Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "example@adobe.com",
        "created_by_display_name": "john snow",
        "updated_by_email": "Restricted",
        "updated_by_display_name": "Restricted"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb/extension_package"
          },
          "data": {
            "id": "EPecefc8291ae346c3b3887d5b2da533b8",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb"
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

## Erstellen einer Autorisierung für die Verwendung von Erweiterungspaketen {#create}

Erstellen Sie für jedes Erweiterungspaket (Erweiterungspaket[&#x200B; und `{ORG_ID}` der Organisation](./extension-packages.md) die Sie autorisieren möchten, eine Autorisierung für die Verwendung des Erweiterungspakets. Um eine neue Autorisierung für die Verwendung von Erweiterungspaketen zu erstellen, stellen Sie eine POST-Anfrage an den folgenden Endpunkt.

**API-Format**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Die `ID` des Erweiterungspakets, für das Sie eine Autorisierung erstellen möchten.“ |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes.authorized_org_id` | Die `ID` der Organisation, die Sie autorisieren möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Autorisierung zur Verwendung des Erweiterungspakets zurück.

```json
{
  "data": {
    "id": "EA35d0e731f73645e6972df9fcac101434",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:30.308Z",
      "updated_at": "2024-06-05T23:17:30.308Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "pending_approval",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "Restricted",
      "updated_by_display_name": "Restricted"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
        },
        "data": {
          "id": "EP43649cc8856d4f09a7c2a21a4b1e449d",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
    }
  }
}
```

>[!NOTE]
>
>In der obigen Beispielantwort befindet sich die Autorisierung derzeit in der `pending_approval`. Vor Verwendung des Erweiterungspakets muss die Organisation die Autorisierung genehmigen. Benutzer der Organisation können das private Erweiterungspaket durchsuchen, während die Autorisierung noch nicht genehmigt ist, sie können es jedoch nicht installieren und nicht in ihrem Erweiterungskatalog finden.

## Abrufen einer Liste von Berechtigungen zur Verwendung von Erweiterungspaketen {#list-authorizations}

Sie können eine Liste der Autorisierungen zur Verwendung von Erweiterungspaketen abrufen, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /extension_package_usage_authorizations
```

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Erweiterungspaketen zurück.

```json
{
  "data": [
    {
      "id": "EA35d0e731f73645e6972df9fcac101434",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:30.308Z",
        "updated_at": "2024-06-05T23:17:30.308Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "Restricted",
        "created_by_display_name": "Restricted",
        "updated_by_email": "example@adobe.com",
        "updated_by_display_name": "john snow"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
          },
          "data": null
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=3&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 3,
      "total_count": 57
    }
  }
}
```

## Löschen einer Autorisierung zur Verwendung von Erweiterungspaketen {#delete}

Um eine Autorisierung zur Nutzung eines Erweiterungspakets zu löschen, schließen Sie dessen `ID` in den Pfad einer DELETE-Anfrage ein. Dadurch wird verhindert, dass autorisierte Organisationen die privaten Versionen des Erweiterungspakets im Katalog anzeigen und in ihren Eigenschaften installieren können.

>[!NOTE]
>
>Alle zuvor installierten privaten Versionen funktionieren weiterhin erwartungsgemäß.

**API-Format**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `ID` | Die `ID` der Autorisierung zur Verwendung des Erweiterungspakets, die Sie löschen möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück. Dies bedeutet, dass die Erweiterung gelöscht wurde.

## Aktualisieren der Autorisierung zur Verwendung von Erweiterungspaketen {#update}

Um eine Autorisierung zur Verwendung eines Erweiterungspakets zu genehmigen oder abzulehnen, fügen Sie dessen `ID` in den Pfad einer PATCH-Anfrage ein.

>[!NOTE]
>
>Um eine Autorisierung zur Verwendung von Erweiterungspaketen für Ihr Unternehmen zu genehmigen oder abzulehnen, müssen Sie über `manage_properties` verfügen.

**API-Format**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `ID` | Die `ID` der Autorisierung zur Verwendung des Erweiterungspakets, die Sie löschen möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
          },
          "type": "extension_package_usage_authorizations",
          "id": "EA86f54b48dd7042a68686508e03be8ba9"
        }
      } 
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes` | Die Attribute, die Sie überarbeiten möchten. Für Berechtigungen zur Verwendung von Erweiterungspaketen können Sie deren `state` überarbeiten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der überarbeiteten Autorisierung zur Verwendung von Erweiterungspaketen zurück.

```json
{
  "data": {
    "id": "EA86f54b48dd7042a68686508e03be8ba9",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:59.480Z",
      "updated_at": "2024-06-05T23:18:00.115Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "approved",
      "created_by_email": "Restricted",
      "created_by_display_name": "Restricted",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9/extension_package"
        },
        "data": {
          "id": "EPb91d54cad9f749dba4e5566459f84c9c",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9"
    }
  }
}
```

>[!NOTE]
>
>Sobald die Autorisierung genehmigt wurde, kann Ihr Unternehmen das Erweiterungspaket in Ihren Eigenschaften installieren.

## Abrufen von Daten für das Erweiterungspaket für eine Autorisierung der Verwendung von Erweiterungspaketen {#retrieve-data}

Sie können Daten für das Erweiterungspaket für eine Autorisierung zur Nutzung eines Erweiterungspakets abrufen, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| Parameter | Beschreibung |
| --- | --- |
| `ID` | Die `ID` der Autorisierung für die Verwendung des Erweiterungspakets, die Sie abrufen möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID}/extension_package \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt Daten für das Erweiterungspaket für eine Autorisierung des Erweiterungspakets zurück.

```json
{
  "data": {
    "id": "EP45ae063fd75c4c22936d3d456c858cfa",
    "type": "extension_packages",
    "attributes": {
      "actions": [],
      "author": {
        "url": "http://adobe.com",
        "name": "Acme",
        "email": "acme@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP45ae063fd75c4c22936d3d456c858cfa",
      "conditions": [],
      "configuration": null,
      "created_at": "2024-06-05T23:17:48.607Z",
      "data_elements": [],
      "description": "Provides nothing.",
      "discontinued": false,
      "display_name": "Acme Template Test",
      "ecma_version": null,
      "events": [],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": "null",
      "name": "Acme",
      "owner_org_id": "{ORG_ID}",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2024-06-05T23:17:53.806Z",
      "version": "1.0.0",
      "view_base_path": "dist/",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa/extension_package_usage_authorizations"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa"
    }
  }
}
```
