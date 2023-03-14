---
title: App configurations-Endpunkt
description: Lernen Sie, wie Sie den /app_configurations-Endpunkt in der Reactor-API aufrufen.
exl-id: 88a1ec36-b4d2-4fb6-92cb-1da04268492a
source-git-commit: 36320addc790e844a1102314890e8692841dc5d0
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 96%

---

# App configurations-Endpunkt

>[!WARNING]
>
>Die Implementierung des `/app_configurations`-Endpunkts ist im Fluss, da Funktionen hinzugefügt, entfernt und überarbeitet werden.

App-Konfigurationen ermöglichen das Speichern und Abrufen von Anmeldeinformationen zur späteren Verwendung. Mit dem `/app_configurations`-Endpunkt in der Reactor-API können Sie App-Konfigurationen in Ihrer Erlebnisanwendung programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen einer Liste von App-Konfigurationen {#list}

**API-Format**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Parameter | Beschreibung |
| --- | --- |
| `COMPANY_ID` | Die `id` des [Unternehmens](./companies.md), dem die App-Konfigurationen gehören. |

{style="table-layout:auto"}

>[!NOTE]
>
>Mit Hilfe von Abfrageparametern können die aufgelisteten App-Konfigurationen anhand der folgenden Attribute gefiltert werden:<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Weiterführende Informationen finden Sie im Handbuch zum [Filtern von Antworten](../guides/filtering.md).

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
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

## Suchen einer App-Konfiguration {#lookup}

Sie können eine App-Konfiguration suchen, indem Sie ihre ID im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `APP_CONFIGURATION_ID` | Die `id` der App-Konfiguration, die Sie suchen möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
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

## Erstellen einer App-Konfiguration  {#create}

Sie können eine neue App-Konfiguration erstellen, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| Parameter | Beschreibung |
| --- | --- |
| `COMPANY_ID` | Die `id` des [Unternehmens](./companies.md), unter dem Sie die App-Konfiguration definieren. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
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
| `platform` | Die Plattform, auf der die Anwendung läuft (Web oder Mobile). Damit wird festgelegt, welche Messaging-Services verfügbar sind. |
| `messaging_service` | Der mit der Anwendung verknüpfte Messaging-Service, z. B. [Apple Push Notification Service (APNs)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) und [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). Damit wird festgelegt, welche Tastentypen verwendet werden können. |
| `key_type` | Stellt das Protokoll dar, das ein Push-Service-Anbieter unterstützt, und bestimmt das Format des Objekts `push_credential`. Bei der Weiterentwicklung der Protokolle für Messaging-Services werden neue `key_type`-Werte erstellt, die die aktualisierten Protokolle unterstützen. |
| `push_credential` | Der eigentliche Anmeldeinformationswert, der im Ruhezustand verschlüsselt wird. Dieses Feld wird normalerweise nicht entschlüsselt oder in API-Antworten aufgenommen. Nur bestimmte Adobe-Services können eine Antwort erhalten, die eine entschlüsselte Push-Anmeldeinformation enthält. |

{style="table-layout:auto"}

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

## Aktualisieren einer App-Konfiguration

Sie können eine App-Konfiguration aktualisieren, indem Sie ihre ID in den Pfad einer PATCH-Anfrage einschließen.

**API-Format**

```http
PATCH /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `APP_CONFIGURATION_ID` | Die `id` der App-Konfiguration, die Sie aktualisieren möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage aktualisiert die `app_id` für eine vorhandene Mobile-App-Konfiguration.

```shell
curl -X PATCH \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
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
| `attributes` | Ein Objekt, dessen Eigenschaften die zu aktualisierenden Attribute für die App-Konfiguration darstellen. Jeder Schlüssel steht für ein bestimmtes App-Konfigurationsattribut, das aktualisiert werden soll, zusammen mit dem entsprechenden Wert, auf den es aktualisiert werden soll.<br><br>Die folgenden Attribute können für App-Konfigurationen aktualisiert werden:<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | Die `id` der App-Konfiguration, die Sie aktualisieren möchten. Diese sollte mit dem `{APP_CONFIGURATION_ID}`-Wert übereinstimmen, der im Anfragepfad angegeben ist. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `app_configurations` lauten. |

{style="table-layout:auto"}

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

## Löschen einer App-Konfiguration

Sie können eine App-Konfiguration löschen, indem Sie ihre ID im Pfad einer DELETE-Anfrage angeben.

**API-Format**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `APP_CONFIGURATION_ID` | Die `id` der App-Konfiguration, die Sie löschen möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück und zeigt damit an, dass die App-Konfiguration gelöscht wurde.
