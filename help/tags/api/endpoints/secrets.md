---
title: Secrets-Endpunkt
description: Hier erfahren Sie, wie Sie den Endpunkt /secrets in der Reactor-API aufrufen.
exl-id: 76875a28-5d13-402d-8543-24db7e2bee8e
source-git-commit: 4f3c97e2cad6160481adb8b3dab3d0c8b23717cc
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 92%

---

# Secrets-Endpunkt

Geheime Daten sind Ressourcen, die nur in den Eigenschaften der Ereignisweiterleitung (Eigenschaften mit einem `platform`-Attribut, das auf `edge` gesetzt wurde) existieren. Sie ermöglichen die Authentifizierung der Ereignisweiterleitung an ein anderes System für den sicheren Datenaustausch.

In diesem Handbuch erfahren Sie, wie Sie Aufrufe an den Endpunkt `/secrets` in der Reactor-API durchführen. Lesen Sie eine ausführliche Erläuterung der verschiedenen Typen von geheimen Daten und deren Verwendung in der allgemeinen Übersicht zu [geheimen Daten](../guides/secrets.md), bevor Sie zu diesem Handbuch zurückkehren.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen einer Liste von geheimen Daten für eine Eigenschaft {#list-property}

Sie können die geheimen Daten auflisten, die zu einer Eigenschaft gehören, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /properties/{PROPERTY_ID}/secrets
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die ID der Eigenschaft, deren geheime Daten Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRe005d921bb724bc88c3ff28e3e916f04/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von geheimen Daten zurück, die zur Eigenschaft gehören.

```json
{
  "data": [
    {
      "id": "SE8bd20bd5d16b49ee9d925929e292526c",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:29.777Z",
        "updated_at": "2021-07-16T22:29:29.777Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
          },
          "data": {
            "id": "PRe005d921bb724bc88c3ff28e3e916f04",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/environment"
          },
          "data": {
            "id": "EN80ad9efbf4ff4f15bebd770613378a75",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c",
        "property": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
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

## Abrufen einer Liste von geheimen Daten für eine Umgebung {#list-environment}

Sie können die geheimen Daten auflisten, die zu einer Umgebung gehören, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /environments/{ENVIRONMENT_ID}/secrets
```

| Parameter | Beschreibung |
| --- | --- |
| `{ENVIRONMENT_ID}` | Die ID der Umgebung, deren geheimen Daten Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/EN0a1b00749daf4ff48a34d2ec37286aa7/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von geheimen Daten zurück, die zu der Umgebung gehören.

```json
{
  "data": [
    {
      "id": "SE57b5ea69acde4595825b85befd1675b3",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:35.447Z",
        "updated_at": "2021-07-16T22:29:35.447Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
          },
          "data": {
            "id": "PRb302ca3557334c13b130da719222ec97",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/environment"
          },
          "data": {
            "id": "EN0a1b00749daf4ff48a34d2ec37286aa7",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3",
        "property": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
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

## Nachschlagen geheimer Daten {#lookup}

Sie können geheime Daten nachschlagen, indem Sie ihre ID im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /secrets/{SECRET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID der geheimen Daten, die Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der geheimen Daten zurück.

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## Erstellen geheimer Daten {#create}

Sie können neue geheime Daten erstellen, indem Sie eine POST-Anfrage ausführen.

>[!NOTE]
>
>Wenn Sie neue geheime Daten erstellen, gibt die API eine sofortige Antwort zurück, die Informationen zu dieser Ressource enthält. Gleichzeitig wird eine Aufgabe für den Austausch geheimer Daten ausgelöst, um zu testen, ob der Austausch von Anmeldedaten funktioniert. Diese Aufgabe wird asynchron verarbeitet und aktualisiert das Statusattribut der geheimen Daten je nach Ergebnis auf `succeeded` oder `failed`.

**API-Format**

```http
POST /properties/{PROPERTY_ID}/secrets
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die ID der Eigenschaft, unter der Sie die geheimen Daten definieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR9eff664dc6014217b76939bb78b83976/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example Secret",
            "type_of": "simple-http",
            "credentials": {
              "username": "example_username",
              "password": "pass12345"
            }
          },
          "relationships": {
            "environment": {
              "data": {
                "id": "EN04cdddbdb6574170bcac9f470f3b8087",
                "type": "environments"
              }
            }
          },
          "type": "secrets"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Ein eindeutiger, beschreibender Name für die geheimen Daten. |
| `type_of` | Der Typ der Authentifizierungsberechtigung, die die geheimen Daten darstellt. Hat drei akzeptierte Werte:<ul><li>`token`: Eine Token-Zeichenfolge.</li><li>`simple-http`: Ein Benutzername und ein Kennwort.</li><li>`oauth2`: Anmeldeinformationen, die dem OAuth-Standard entsprechen.</li></ul> |
| `credentials` | Ein Objekt, das die Werte der Anmeldeinformationen für die geheimen Daten enthält. Je nach `type_of`-Attribut müssen verschiedene Eigenschaften angegeben werden. Im Abschnitt zu [Anmeldeinformationen](../guides/secrets.md#credentials) des Handbuchs zu geheimen Daten finden Sie Einzelheiten zu den Anforderungen für die einzelnen Typen. |
| `relationships.environment` | Geheime Daten müssen bei der ersten Erstellung jeweils einer Umgebung zugeordnet werden. Das `data`-Objekt in dieser Eigenschaft muss die `id` der Umgebung, der die geheimen Daten zugewiesen werden, zusammen mit einem `type`-Wert von `environments` enthalten. |
| `type` | Der Typ der zu erstellenden Ressource. Für diesen Aufruf muss der Wert `secrets` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der geheimen Daten zurück. Beachten Sie, dass je nach Art der geheimen Daten einige Eigenschaften unter `credentials` ausgeblendet sein können.

```json
{
  "data": { 
    "id": "SE39fdf431f8ad4600bbc24ea73fcb1154", 
    "type": "secrets", 
    "attributes": { 
    "created_at": "2021-07-14T19:33:25.628Z", 
    "updated_at": "2021-07-14T19:33:25.628Z", 
    "name": "Example Secret", 
    "type_of": "simple-http", 
    "activated_at": null, 
    "expires_at": null, 
    "refresh_at": null, 
    "status": "pending", 
    "credentials": { 
      "username": "example_username" 
      } 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    } 
  } 
}
```

## Testen von geheimen Daten des Typs `oauth2` {#test}

>[!NOTE]
>
>Dieser Vorgang kann nur für geheime Daten mit einem `type_of`-Wert von `oauth2` ausgeführt werden.

Sie können geheime Daten vom Typ `oauth2` testen, indem Sie ihre ID(s) im Pfad einer PATCH-Anfrage angeben. Der Testvorgang führt einen Austausch durch und schließt die Antwort des Autorisierungsdienstes in das Attribut `test_exchange` im `meta`-Objekt der geheimen Daten ein. Dieser Vorgang aktualisiert nicht die geheimen Daten selbst.

**API-Format**

```http
PATCH /secrets/{SECRET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID der geheimen Daten vom Typ `oauth2`, die Sie testen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SE6c15a7a64f9041b5985558ed3e19a449 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "oauth2"
          },
          "meta": {
            "action": "test"
          },
          "id": "SE6c15a7a64f9041b5985558ed3e19a449",
          "type": "secrets"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes` | Muss eine `type_of`-Eigenschaft mit dem Wert `oauth2` enthalten. |
| `meta` | Muss eine `action`-Eigenschaft mit dem Wert `test` enthalten. |
| `id` | Die ID der geheimen Daten, die Sie testen. Diese sollte mit der ID übereinstimmen, der im Anfragepfad angegeben ist. |
| `type` | Der Typ der Ressource, für die der Vorgang ausgeführt wird. Muss auf `secrets` festgelegt werden. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der geheimen Daten zurück, wobei die Antwort des Autorisierungsdienstes unter `meta.test_exchange` enthalten ist.

```json
{ 
  "data": { 
    "id": "SE6c15a7a64f9041b5985558ed3e19a449", 
    "type": "secrets", 
    "attributes": { 
      "activated_at": null, 
      "created_at": "2021-07-14T19:33:25.628Z", 
      "credentials": { 
        "token_url": "https://token_url.test/token/authorize?required_param=value",
        "client_id": "test_client_id", 
        "client_secret": "test_client_secret", 
        "refresh_offset": 14400, 
      },
      "expires_at": null, 
      "name": "Example Secret", 
      "refresh_at": null, 
      "status": "pending", 
      "type_of": "oauth2", 
      "updated_at": "2021-07-14T19:33:25.628Z", 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    }, 
    "meta": { 
      "test_exchange": { 
        "access_token": "FpIkBn3zxW0fH6EBC4MB", 
        "expires_in": 36000, 
        "token_type": "Bearer", 
      } 
    } 
  } 
}
```

## Wiederholen von geheimen Daten {#retry}

Das Wiederholen von geheimen Daten ist die Aktion, den Austausch der geheimen Daten manuell auszulösen. Sie können geheime Daten neu testen, indem Sie ihre ID im Pfad einer PATCH-Anfrage angeben.

**API-Format**

```http
PATCH /secrets/{SECRET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID der geheimen Daten, die Sie neu testen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "token"
          },
          "meta": {
            "action": "retry"
          },
          "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
          "type": "secrets"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes` | Muss eine `type_of`-Eigenschaft enthalten, die mit der der zu aktualisierenden geheimen Daten übereinstimmt (`token`, `simple-http` oder `oauth2`). |
| `meta` | Muss eine `action`-Eigenschaft mit dem Wert `retry` enthalten. |
| `id` | Die ID der geheimen Daten, die Sie erneut testen. Diese sollte mit der ID übereinstimmen, der im Anfragepfad angegeben ist. |
| `type` | Der Typ der Ressource, für die der Vorgang ausgeführt wird. Muss auf `secrets` festgelegt werden. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der geheimen Daten zurück, wobei der Status auf `pending` zurückgesetzt wird. Nach Abschluss des Austausches wird der Status der geheimen Daten je nach Ergebnis auf `succeeded` oder `failed` gesetzt.

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## Erneutes Autorisieren eines `oauth2-google` secret {#reauthorize}

Jeder `oauth2-google` secret contains `meta.token_url_expires_at` -Eigenschaft, die angibt, wann die Autorisierungs-URL abläuft. Danach muss das Geheimnis erneut autorisiert werden, damit es den Authentifizierungsprozess verlängern kann.

So autorisieren Sie eine `oauth2-google` geheim, stellen Sie eine PATCH-Anfrage für das betreffende Geheimnis.

**API-Format**

```http
PATCH /secrets/{SECRET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die `id` des Geheimnisses, das Sie erneut autorisieren möchten. |

**Anfrage**

Die `data` -Objekt in der Anfrage-Payload muss eine `meta.action` Eigenschaft auf `reauthorize`.

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "oauth2-google"
          },
          "meta": {
            "action": "reauthorize"
          },
          "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
          "type": "secrets"
        }
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Geheimnisses zurück. Von hier aus müssen Sie die `meta.token_url` in einen Browser, um den Autorisierungsprozess abzuschließen.

```json
{
  "data": {
    "id": "SE5fdfa4c0a2d8404e8b1bc38827cc41c9",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-15T19:00:25.628Z", 
      "updated_at": "2021-07-15T19:00:25.628Z", 
      "name": "Example Secret", 
      "type_of": "oauth2-google", 
      "activated_at": null, 
      "expires_at": null, 
      "refresh_at": null, 
      "status": "pending", 
      "credentials": { 
        "scopes": [
          "https://www.googleapis.com/auth/adwords",
          "https://www.googleapis.com/auth/pubsub"
        ], 
      } 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9", 
      "property": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/property" 
    }, 
    "meta": { 
      "token_url": "https://accounts.google.com/o/oauth2/auth?access_type=offline&approval_prompt=force&client_id=434635668552-0qvlu519fdjtnkvk8hu8c8dj8rg3723r.apps.googleusercontent.com&redirect_uri=https%3A%2F%2Freactor.adobe.io%2Foauth2%2Fcallback&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fadwords&state=state", 
      "token_url_expires_at": "2021-07-15T20:00:25.628Z" 
    } 
  } 
}
```

## Löschen von geheimen Daten {#delete}

Sie können geheime Daten löschen, indem Sie ihre ID im Pfad einer DELETE-Anfrage angeben. Dies ist ein harter Löschvorgang mit sofortiger Wirkung und erfordert keine erneute Veröffentlichung der Bibliothek.

Dieser Vorgang entfernt die geheimen Daten aus der Umgebung, mit der sie verbunden sind, und die zugrunde liegende Ressource wird gelöscht.

>[!WARNING]
>
>Wenn Sie über bereitgestellte Regeln verfügen, die auf gelöschte geheime Daten verweisen, funktionieren diese Regeln ab sofort nicht mehr. Alle Datenelemente, die auf diese geheimen Daten verweisen, müssen nachträglich aktualisiert oder entfernt werden.

**API-Format**

```http
DELETE /secrets/{SECRET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID der geheimen Daten, die Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und einen leeren Antworttext zurück, was angibt, dass die geheimen Daten aus dem System gelöscht wurden.

## Auflisten der Anmerkungen für geheime Daten {#notes}

Mit der Reactor-API können Sie zu bestimmten Ressourcen Anmerkungen hinzufügen, darunter auch zu geheimen Daten. Anmerkungen sind Kommentare in Textform, die sich nicht auf das Ressourcenverhalten auswirken und für verschiedene Anwendungsfälle verwendet werden können.

>[!NOTE]
>
>Siehe das [Handbuch zum Anmerkungen-Endpunkt](./notes.md) für Details zum Erstellen und Bearbeiten von Anmerkungen für Reactor-API-Ressourcen.

Sie können alle Hinweise zu geheimen Daten abrufen, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /secrets/{SECRET_ID}/notes
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID der geheimen Daten, deren Anmerkungen Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Hinweisen zurück, die zu den geheimen Daten gehören.

```json
{
  "data": [
    {
      "id": "NTe666dbcc2f204218b6fde2fe60ab7043",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Doe",
        "author_email": "jdoe@example.com",
        "created_at": "2021-07-16T22:29:58.259Z",
        "text": "This is a secret note."
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1"
          },
          "data": {
            "id": "SE591d3b86910f4e6883f0e1c36e54bff1",
            "type": "secrets"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1",
        "self": "https://reactor.adobe.io/notes/NTe666dbcc2f204218b6fde2fe60ab7043"
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

## Abrufen zugehöriger Ressourcen für geheime Daten {#related}

Die folgenden Aufrufe zeigen, wie Sie die zugehörigen Ressourcen für geheime Daten abrufen. Beim [Nachschlagen geheimer Daten](#lookup) werden diese Beziehungen unter der `relationships`-Eigenschaft aufgeführt.

Weitere Informationen zu Beziehungen in der Reactor-API finden Sie im [Handbuch zu Beziehungen](../guides/relationships.md).

### Suchen der zugehörigen Umgebung von geheimen Daten {#environment}

Sie können die Umgebung nachschlagen, die geheime Daten verwenden, indem Sie `/environment` an den Pfad einer GET-Anfrage anhängen.

**API-Format**

```http
GET /secrets/{SECRET_ID}/environment
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID der geheimen Daten, deren Umgebung Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Umgebung zurück.

```json
{
  "data": {
    "id": "EN33e8d63ac647448da1f77ced5c3c8580",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2021-07-16T22:19:13.438Z",
      "library_path": "bc12f2b85d11/b9a3067414ff",
      "library_name": "launch-3b6c4eea15ae-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-3b6c4eea15ae-development.min.js",
          "minified": true,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.min.js"
          ],
          "license_path": "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
        },
        {
          "library_name": "launch-3b6c4eea15ae-development.js",
          "minified": false,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": null,
      "stage": "development",
      "updated_at": "2021-07-16T22:19:13.438Z",
      "status": "succeeded",
      "token": "3b6c4eea15ae"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/host",
          "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/relationships/host"
        },
        "data": {
          "id": "HT7d5cf665463e46a1968ada1ceb1b5ca7",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/property"
        },
        "data": {
          "id": "PRba81d3027db846b084212391aa5d2f1f",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRba81d3027db846b084212391aa5d2f1f",
      "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### Nachschlagen der zugehörigen Eigenschaft für geheime Daten {#property}

Sie können die Eigenschaft nachschlagen, zu der eine Bibliothek gehört, indem Sie `/property` an den Pfad einer GET-Anfrage anhängen.

**API-Format**

```http
GET /secrets/{SECRET_ID}/property
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID der geheimen Daten, deren Eigenschaft Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Eigenschaft zurück.

```json
{
  "data": {
    "id": "PR2d191feafef54c5da4ddb5ef647d4867",
    "type": "properties",
    "attributes": {
      "created_at": "2021-07-16T22:26:25.320Z",
      "enabled": true,
      "name": "Kessel Edge Example Property",
      "updated_at": "2021-07-16T22:26:25.320Z",
      "platform": "edge",
      "development": false,
      "token": "8efbe7023155"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/company"
        },
        "data": {
          "id": "COc26fb19f87d24cbe827a70ad2a672093",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/COc26fb19f87d24cbe827a70ad2a672093",
      "data_elements": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments",
      "extensions": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions",
      "rules": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules",
      "self": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "edit_property",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
