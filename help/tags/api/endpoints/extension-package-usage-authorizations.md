---
title: Autorisierungs-Endpunkt für Erweiterungspaketverwendung
description: Erfahren Sie, wie Sie den Endpunkt /extension_package_usage authorizations in der Reactor-API aufrufen.
source-git-commit: fdf01451527e2fab8eb6e6f9d7b4901a85381450
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 16%

---


# Endpunkt für Nutzungsberechtigungen für Erweiterungspakete

Ein Erweiterungspaket stellt eine [Erweiterung](./extensions.md) dar, die von einem Erweiterungsentwickler verfasst wurde. Zusätzliche Funktionen, die Tag-Benutzern zur Verfügung gestellt werden können, werden durch ein Erweiterungspaket definiert. Diese Funktionen können Hauptmodule und gemeinsame Module enthalten, die jedoch am häufigsten als [Regelkomponenten](./rule-components.md) (Ereignisse, Bedingungen und Aktionen) und [Datenelemente](./data-elements.md).

Ein Erweiterungspaket gehört dem [Firma](./companies.md). Inhaber von Erweiterungspaketen können anderen Unternehmen die Verwendung ihrer privaten Versionen der Pakete gestatten. Jedes autorisierte Unternehmen erhält eine Nutzungsgenehmigung für ein einzelnes Erweiterungspaket, das für alle zukünftigen und aktuellen privaten Versionen des Pakets gültig ist.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen von Nutzungsberechtigungen für Erweiterungspakete für ein Erweiterungspaket {#list}

Um eine Liste von Nutzungsberechtigungen für ein Erweiterungspaket abzurufen, stellen Sie eine GET-Anfrage an den folgenden Endpunkt.

**API-Format**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `ID` der Eigenschaft, deren Erweiterungspaketverwendungsautorisierung Sie auflisten möchten. |

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

## Erstellen einer Nutzungsautorisierung für ein Erweiterungspaket {#create}

Erstellen Sie für jede [Erweiterungspaket](./extension-packages.md) und `{ORG_ID}` der Organisation, die Sie autorisieren möchten. Um eine neue Autorisierung zur Verwendung von Erweiterungspaketen zu erstellen, stellen Sie eine POST-Anfrage an den unten stehenden Endpunkt.

**API-Format**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Die `ID` des Erweiterungspakets, für das Sie eine Autorisierung erstellen möchten.&quot; |

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
>In der obigen Beispielantwort befindet sich die Autorisierung derzeit im `pending_approval` Bühne. Vor Verwendung des Erweiterungspakets muss die Organisation die Autorisierung genehmigen. Benutzer der Organisation können das private Erweiterungspaket durchsuchen, während die Autorisierung aussteht, es jedoch nicht installieren kann und nicht in ihrem Erweiterungskatalog finden.

## Abrufen einer Liste der Nutzungsberechtigungen für Erweiterungspakete {#list_authorizations}

Sie können eine Liste der Nutzungsberechtigungen für Erweiterungspakete abrufen, indem Sie eine GET-Anfrage stellen.

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

## Nutzungsautorisierung eines Erweiterungspakets löschen {#delete}

Um eine Nutzungsautorisierung für ein Erweiterungspaket zu löschen, fügen Sie dessen `ID` im Pfad einer DELETE-Anfrage. Dadurch wird verhindert, dass die autorisierte Organisation die privaten Versionen des Erweiterungspakets im Katalog anzeigt und in ihren Eigenschaften installiert.

>[!NOTE]
>
>Alle zuvor installierten privaten Versionen funktionieren weiterhin erwartungsgemäß.

**API-Format**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `ID` | Die `ID` der Nutzungsberechtigung für das Erweiterungspaket, die Sie löschen möchten. |

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

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück. Dies zeigt an, dass die Erweiterung gelöscht wurde.

## Aktualisieren der Autorisierung zur Verwendung eines Erweiterungspakets {#update}

Um eine Nutzungsgenehmigung für ein Erweiterungspaket zu genehmigen oder abzulehnen, fügen Sie dessen `ID` im Pfad einer PATCH-Anfrage.

>[!NOTE]
>
>Um eine Genehmigung zur Verwendung eines Erweiterungspakets für Ihr Unternehmen zu genehmigen oder abzulehnen, müssen Sie über `manage_properties` Rechte.

**API-Format**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `ID` | Die `ID` der Nutzungsberechtigung für das Erweiterungspaket, die Sie löschen möchten. |

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
| `attributes` | Die Attribute, die Sie überarbeiten möchten. Für die Nutzungsberechtigungen von Erweiterungspaketen können Sie deren `state`. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der überarbeiteten Autorisierung zur Verwendung des Erweiterungspakets zurück.

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
>Nachdem die Autorisierung genehmigt wurde, kann Ihr Unternehmen das Erweiterungspaket in Ihren Eigenschaften installieren.

## Abrufen von Daten für das Erweiterungspaket für die Autorisierung der Verwendung eines Erweiterungspakets {#retrieve_data}

Sie können Daten für das Erweiterungspaket für die Autorisierung der Verwendung eines Erweiterungspakets abrufen, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| Parameter | Beschreibung |
| --- | --- |
| `ID` | Die `ID` der Nutzungsautorisierung des Erweiterungspakets, die Sie abrufen möchten. |

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