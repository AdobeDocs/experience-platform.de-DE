---
title: Suchen von Ressourcen in der Reactor-API
description: Hier erfahren Sie, wie Sie in der Reactor-API nach Ressourcen suchen.
exl-id: cb594e60-3e24-457e-bfb3-78ec84d3e39a
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: ht
source-wordcount: '260'
ht-degree: 100%

---

# Suchen von Ressourcen in der Reactor-API

Mit dem `/search`-Endpunkt in der Reactor-API können Sie strukturierte Abfragen zu gespeicherten Ressourcen durchführen. Dieses Dokument enthält Beispiele für verschiedene Suchanfragen für diverse gängige Anwendungsfälle.

>[!NOTE]
>
>Bevor Sie dieses Handbuch lesen, lesen Sie das [Handbuch zum Suchen von Endpunkten](../endpoints/search.md), um Informationen zur akzeptierten Abfragesyntax und anderen Nutzungsrichtlinien zu erhalten.

## Grundlegende Abfragestrategien

Die folgenden Beispiele zeigen einige grundlegende Konzepte für die Verwendung der Suchfunktion der API.

### Durchsuchen mehrerer Felder

Eine Suche kann über mehrere Felder hinweg mithilfe von Platzhaltern im Feldnamen durchgeführt werden. Um beispielsweise mehrere Attributfelder zu durchsuchen, verwenden Sie `attributes.*` als Feldnamen.

```json
{
  "data": {
    "query": {
      "attributes.*": {
        "value": "evar7"
      }
    }
  }
}
```

>[!IMPORTANT]
>
>Normalerweise müssen die Suchwerte mit dem Typ der gesuchten Daten übereinstimmen. Beispielsweise würde ein Abfragewert `evar7` für ein ganzzahliges Feld fehlschlagen. Bei der Suche über mehrere Felder wird die Anforderung an den Abfragetyp gelockert, um Fehler zu vermeiden, was jedoch zu unerwünschten Ergebnissen führen kann.

### Beschränken von Abfragen auf bestimmte Ressourcentypen

Sie können eine Suche auf einen bestimmten Ressourcentyp beschränken, indem Sie in der Anfrage `resource_types` angeben. So suchen Sie beispielsweise nach `data_elements` und `rule_components`:

```json
{
  "data": {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

### Sortieren von Antworten

Die Eigenschaft `sort` kann zum Sortieren von Antworten verwendet werden. Beispiel: Sortieren nach `created_at` mit dem neuesten zuerst:

```json
{
  "data": {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "sort": [
      {
        "attributes.created_at": "desc"
      }
    ],
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

## Gängige Suchbeispiele

Im folgenden Beispiel werden zusätzliche gängige Suchmuster veranschaulicht.

### Jede Ressource mit einem bestimmten Namen

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.name": {
              "value": "Adobe"
            }
          }
        }
      }'
```

### Jede Ressource mit Verweis auf „evar7“

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.*": {
              "value": "evar7"
            }
          }
        }
      }'
```

### Datenelemente eines Delegatentyps „benutzerspezifischer Code“

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.delegate_descriptor_id": {
              "value": "custom-code"
            }
          },
          "resource_types": ["data_elements"]
        }
      }'
```

### Regelkomponenten, die auf ein bestimmtes Datenelement verweisen

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.settings": {
              "value": "myDataElement8"
            }
          },
          "resource_types": ["rule_components"]
        }
      }'
```

### Regeln in einer bestimmten Eigenschaft

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "relationships.property.data.id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          },
          "resource_types": ["rules"]
        }
      }'
```

### Suchen einer Ressource nach ID

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          }
        }
      }'
```

### Durchführen einer Suche mit „OR“-Begriffslogik

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.display_name": {
              "value": "My Rule Holiday Sale",
              "value_operator: "OR"
            }
          }
        }
      }'
```
