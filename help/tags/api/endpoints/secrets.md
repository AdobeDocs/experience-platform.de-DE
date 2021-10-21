---
title: Geheimer Endpunkt
description: Erfahren Sie, wie Sie Aufrufe des Endpunkts /geheimnisse in der Reactor-API durchführen.
source-git-commit: 103ba74646a42fd62007f47df4d1a46caf25e3e6
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 16%

---

# Geheimer Endpunkt

Ein Geheimnis ist eine Ressource, die nur in den Eigenschaften der Ereignis-Weiterleitung vorhanden ist (Eigenschaften mit `platform` Attribut festgelegt auf `edge`). Sie ermöglichen es der Ereignis-Weiterleitung, sich für einen sicheren Datenaustausch an ein anderes System zu authentifizieren.

Dieses Handbuch zeigt Ihnen, wie Sie Aufrufe an die `/secrets` Endpunkt in der Reaktor-API. Eine detaillierte Erläuterung der verschiedenen geheimen Typen und ihre Verwendung finden Sie in der hochrangigen Übersicht unter [Geheimnisse](../guides/secrets.md) bevor Sie zu diesem Handbuch zurückkehren.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Liste von Geheimnissen für eine Eigenschaft abrufen {#list-property}

Sie können die Geheimnisse einer Immobilie durch eine GET anfordern.

**API-Format**

```http
GET /properties/{PROPERTY_ID}/secrets
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die ID der Eigenschaft, deren Geheimnisse Liste werden sollen. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRe005d921bb724bc88c3ff28e3e916f04/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Geheimnissen der Immobilie zurück.

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

## Liste von Geheimnissen für eine Umgebung abrufen {#list-environment}

Sie können die Geheimnisse einer Umgebung Liste haben, indem Sie eine GET anfordern.

**API-Format**

```http
GET /environments/{ENVIRONMENT_ID}/secrets
```

| Parameter | Beschreibung |
| --- | --- |
| `{ENVIRONMENT_ID}` | Die ID der Umgebung, deren Geheimnisse Sie Liste haben möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/EN0a1b00749daf4ff48a34d2ec37286aa7/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Geheimnissen der Umgebung zurück.

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

## Schlag ein Geheimnis auf {#lookup}

Sie können ein Geheimnis nachschlagen, indem Sie dessen ID in den Pfad einer GET-Anfrage einschließen.

**API-Format**

```http
GET /secrets/{SECRET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID des Geheimnisses, das Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Geheimnisses zurück.

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

## Geheimnis erstellen {#create}

Sie können ein Geheimnis erstellen, indem Sie eine POST anfordern.

>[!NOTE]
>
>Wenn Sie ein neues Geheimnis erstellen, gibt die API eine sofortige Antwort zurück, die Informationen zu dieser Ressource enthält. Gleichzeitig wird eine Aufgabe des geheimen Austausches ausgelöst, um zu testen, ob der Austausch von Anmeldeinformationen funktionsfähig ist. Diese Aufgabe wird asynchron verarbeitet und aktualisiert das Statusattribut des geheimen Elements auf `succeeded` oder `failed` je nach Ergebnis.

**API-Format**

```http
POST /properties/{PROPERTY_ID}/secrets
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die ID der Eigenschaft, unter der das Geheimnis definiert werden soll. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR9eff664dc6014217b76939bb78b83976/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Ein eindeutiger, beschreibender Name für das Geheimnis. |
| `type_of` | Der Typ der Authentifizierungsberechtigung, den das Geheimnis darstellt. Hat drei akzeptierte Werte:<ul><li>`token`: Eine Tokenzeichenfolge.</li><li>`simple-http`: Ein Benutzername und ein Kennwort.</li><li>`oauth2`: Anmeldedaten, die dem OAuth-Standard entsprechen.</li></ul> |
| `credentials` | Ein Objekt, das die Berechtigungswerte für das Geheimnis enthält. Je nach `type_of` -Attribut, müssen andere Eigenschaften angegeben werden. Siehe Abschnitt über [Anmeldedaten](../guides/secrets.md#credentials) im Leitfaden &quot;Geheimnisse&quot; Einzelheiten zu den Anforderungen für jeden Typ. |
| `relationships.environment` | Jedes Geheimnis muss einer Umgebung zugeordnet sein, wenn es zum ersten Mal erstellt wird. Die `data` Objekt in dieser Eigenschaft muss Folgendes enthalten: `id` der Umgebung, der das Geheimnis zugewiesen wurde, zusammen mit `type` Wert von `environments`. |
| `type` | Der Typ der zu erstellenden Ressource. Für diesen Aufruf muss der Wert `secrets`. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Geheimnisses zurück. Beachten Sie, dass je nach Geheimtyp einige Eigenschaften unter `credentials` kann ausgeblendet werden.

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

## Testen `oauth2` geheim {#test}

>[!NOTE]
>
>Dieser Vorgang kann nur für Geheimnisse durchgeführt werden mit `type_of` Wert von `oauth2`.

Sie können `oauth2` geheim, indem die ID in den Pfad einer PATCH-Anfrage aufgenommen wird. Der Testvorgang führt einen Austausch durch und beinhaltet die Antwort des Autorisierungsdienstes in `test_exchange` -Attribut im geheimen `meta` Objekt. Dieser Vorgang aktualisiert das Geheimnis selbst nicht.

**API-Format**

```http
PATCH /secrets/{SECRET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID der `oauth2` geheim, das Sie testen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SE6c15a7a64f9041b5985558ed3e19a449 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `attributes` | Muss Folgendes enthalten: `type_of` Eigenschaft mit einem Wert von `oauth2`. |
| `meta` | Muss eine `action` Eigenschaft mit einem Wert von `test`. |
| `id` | Die ID des Geheimtitels, das Sie testen. Diese muss mit der im Anfragepfad angegebenen ID übereinstimmen. |
| `type` | Die Art der Ressource, auf der gearbeitet wird. Muss auf `secrets` festgelegt werden. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Bei einer erfolgreichen Antwort werden die Details des geheimen Geheims zurückgegeben, wobei die Antwort des Autorisierungsdienstes unter `meta.test_exchange`.

```json
{ 
  "data": { 
    "id": "SE6c15a7a64f9041b5985558ed3e19a449", 
    "type": "secrets", 
    "attributes": { 
      "activated_at": null, 
      "created_at": "2021-07-14T19:33:25.628Z", 
      "credentials": { 
        "authorization_url": "https://athorization_url.test/token/authorize?required_param=value",
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

## Geheimnis erneut versuchen {#retry}

Ein Geheimnis erneut zu versuchen ist die Handauslösung des geheimen Austausches. Sie können ein Geheimnis erneut versuchen, indem Sie seine ID in den Pfad einer PATCH-Anforderung einschließen.

**API-Format**

```http
PATCH /secrets/{SECRET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID des geheimen Bereichs, das Sie erneut versuchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `attributes` | Muss Folgendes enthalten: `type_of` Eigenschaft, die mit der des zu aktualisierenden geheimen Bereichs übereinstimmt (`token`, `simple-http`oder `oauth2`). |
| `meta` | Muss eine `action` Eigenschaft mit einem Wert von `retry`. |
| `id` | Die ID des Geheimtitels, das Sie erneut versuchen. Diese muss mit der im Anfragepfad angegebenen ID übereinstimmen. |
| `type` | Die Art der Ressource, auf der gearbeitet wird. Muss auf `secrets` festgelegt werden. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des geheimen Geheims zurück, wobei der Status zurückgesetzt wird auf `pending`. Nach Abschluss des Austausches wird der geheime Status auf aktualisiert auf `succeeded` oder `failed` je nach Ergebnis.

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

## Geheimnis löschen {#delete}

Sie können ein Geheimnis löschen, indem Sie dessen ID in den Pfad einer DELETE-Anforderung einschließen. Dies ist ein schwerer Löschvorgang mit sofortiger Wirkung und erfordert keine erneute Veröffentlichung der Bibliothek.

Dieser Vorgang entfernt das Geheimnis aus der Umgebung, auf die es sich bezieht, und die zugrunde liegende Ressource wird gelöscht.

>[!WARNING]
>
>Wenn Sie über bereitgestellte Regeln verfügen, die auf ein gelöschtes Geheimnis verweisen, funktionieren diese Regeln sofort nicht mehr. Alle Datenelemente, die auf dieses Geheimnis verweisen, müssen nachträglich aktualisiert oder entfernt werden.

**API-Format**

```http
DELETE /secrets/{SECRET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID des geheimen Rahmens, den Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und einen leeren Antworttext zurück, was darauf hinweist, dass das Geheimnis aus dem System gelöscht wurde.

## Liste der geheimen Hinweise {#notes}

Die Reactor-API ermöglicht das Hinzufügen von Notizen zu bestimmten Ressourcen, einschließlich Geheimnissen. Hinweise sind Textkommentare, die sich nicht auf das Ressourcenverhalten auswirken und für eine Vielzahl von Anwendungsfällen verwendet werden können.

>[!NOTE]
>
>Siehe [Hinweis-Endpunkt-Handbuch](./notes.md) für Details zum Erstellen und Bearbeiten von Notizen für Reactor-API-Ressourcen.

Sie können alle geheimen Hinweise abrufen, indem Sie eine GET anfordern.

**API-Format**

```http
GET /secrets/{SECRET_ID}/notes
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID des Geheimtitels, dessen Notizen Sie Liste wünschen. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Notizen, die dem Geheimnis gehören.

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

## Zugehörige Ressourcen für ein Geheimnis abrufen {#related}

Die folgenden Aufrufe zeigen, wie die zugehörigen Ressourcen für ein Geheimnis abgerufen werden. Wann [Geheimnis nachschlagen](#lookup), werden diese Beziehungen unter `relationships` Eigenschaft.

Weitere Informationen zu Beziehungen in der Reactor-API finden Sie im [Handbuch zu Beziehungen](../guides/relationships.md).

### Die zugehörige Umgebung nach einem Geheimnis suchen {#environment}

Sie können die Umgebung nachschlagen, die ein Geheimnis verwendet, indem Sie anhängen `/environment` zum Pfad einer GET.

**API-Format**

```http
GET /secrets/{SECRET_ID}/environment
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID des Geheimtitels, dessen Umgebung Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

### Verwandte Eigenschaft für ein Geheimnis nachschlagen {#property}

Sie können die Eigenschaft nachschlagen, der ein Geheimnis gehört, indem Sie anhängen `/property` zum Pfad einer GET.

**API-Format**

```http
GET /secrets/{SECRET_ID}/property
```

| Parameter | Beschreibung |
| --- | --- |
| `{SECRET_ID}` | Die ID des geheimen Elements, dessen Eigenschaft Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
