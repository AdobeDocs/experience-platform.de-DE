---
title: Endpunkt "App-Konfigurationen"
description: Erfahren Sie, wie Sie den Endpunkt /app_configurations in der Reactor-API aufrufen.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 11%

---

# Endpunkt &quot;App-Konfigurationen&quot;

>[!WARNING]
>
>Die Implementierung des Endpunkts `/app_configurations` ist im Fluss, da Funktionen hinzugefügt, entfernt und überarbeitet werden.

App-Konfigurationen ermöglichen das Speichern und Abrufen von Anmeldeinformationen zur späteren Verwendung. Mit dem Endpunkt `/app_configurations` in der Reactor-API können Sie App-Konfigurationen in Ihrer Erlebnisanwendung programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md) , um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Liste von App-Konfigurationen abrufen {#list}

**API-Format**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Parameter | Beschreibung |
| --- | --- |
| `COMPANY_ID` | Die `id` der [Firma](./companies.md), der die App-Konfigurationen gehören. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Mithilfe von Abfrageparametern können aufgelistete App-Konfigurationen anhand der folgenden Attribute gefiltert werden:<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Weitere Informationen finden Sie im Handbuch zu [Filterantworten](../guides/filtering.md) .

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von App-Konfigurationen zurück.

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
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

## App-Konfiguration nachschlagen {#lookup}

Sie können nach einer App-Konfiguration suchen, indem Sie deren ID im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `APP_CONFIGURATION_ID` | Die `id` der App-Konfiguration, die Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der App-Konfiguration zurück.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## App-Konfiguration erstellen {#create}

Sie können eine neue App-Konfiguration erstellen, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| Parameter | Beschreibung |
| --- | --- |
| `COMPANY_ID` | Die `id` der [Firma](./companies.md), unter der Sie die App-Konfiguration definieren. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `platform` | Die Plattform, auf der die Anwendung ausgeführt wird (Web oder Mobil). Dadurch wird bestimmt, welche Messaging-Dienste verfügbar sind. |
| `messaging_service` | Der mit der App verknüpfte Messaging-Dienst, z. B. [Apple Push Notification Service (APNs)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) und [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). Dadurch wird bestimmt, welche Schlüsseltypen verwendet werden können. |
| `key_type` | Stellt das Protokoll dar, das ein Push-Dienst-Anbieter unterstützt, und bestimmt das Format des Objekts `push_credential`. Wenn sich Protokolle für Messaging-Dienste entwickeln, werden neue `key_type`-Werte erstellt, die die aktualisierten Protokolle unterstützen. |
| `push_credential` | Der tatsächliche Berechtigungswert, der während der Ruhezeit verschlüsselt wird. Dieses Feld ist normalerweise nicht entschlüsselt oder in API-Antworten enthalten. Nur bestimmte Adobe-Dienste können eine Antwort mit einer entschlüsselten Push-Berechtigung erhalten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten App-Konfiguration zurück.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## App-Konfiguration aktualisieren

Sie können eine App-Konfiguration aktualisieren, indem Sie ihre ID in den Pfad einer PUT-Anfrage einschließen.

**API-Format**

```http
PUT /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `APP_CONFIGURATION_ID` | Die `id` der App-Konfiguration, die Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert die `app_id` für eine vorhandene App-Konfiguration.

```shell
curl -X PUT \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes` | Ein Objekt, dessen Eigenschaften die Attribute darstellen, die für die App-Konfiguration aktualisiert werden sollen. Jeder Schlüssel stellt das jeweilige App-Konfigurationsattribut dar, das aktualisiert werden soll, sowie den entsprechenden Wert, auf den es aktualisiert werden soll.<br><br>Die folgenden Attribute können für App-Konfigurationen aktualisiert werden:<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | Die `id` der App-Konfiguration, die Sie aktualisieren möchten. Dies sollte mit dem Wert `{APP_CONFIGURATION_ID}` übereinstimmen, der im Anfragepfad bereitgestellt wird. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `app_configurations` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten App-Konfiguration zurück.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## App-Konfiguration löschen

Sie können eine App-Konfiguration löschen, indem Sie ihre ID in den Pfad einer DELETE-Anfrage einschließen.

**API-Format**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `APP_CONFIGURATION_ID` | Die `id` der App-Konfiguration, die Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück und zeigt an, dass die App-Konfiguration gelöscht wurde.
