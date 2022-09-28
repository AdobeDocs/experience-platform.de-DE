---
keywords: Experience Platform; Startseite; beliebte Themen; Flussdienst; Flow Service-API; Quellen; Quellen
title: Filtern von Daten auf Zeilenebene für eine Quelle mithilfe der Flow Service-API
description: In diesem Tutorial werden die Schritte zum Filtern von Daten auf Quellebene mithilfe der Flow Service-API beschrieben.
source-git-commit: 122f6bda2fbcf72bf098b972ff7b081f4c5e3388
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 17%

---

# Filtern von Daten auf Zeilenebene für eine Quelle mithilfe der [!DNL Flow Service] API

>[!IMPORTANT]
>
>Unterstützung für das Filtern von Daten auf Zeilenebene für eine Quelle ist derzeit nur für die [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md) und [[!DNL Snowflake]](../../connectors/databases/snowflake.md) Quellen.

Dieses Tutorial enthält Schritte zum Filtern von Daten auf Zeilenebene für eine Quelle mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Filtern von Quelldaten

Im Folgenden werden die Schritte beschrieben, die zum Filtern von Daten auf Zeilenebene für Ihre Quelle durchgeführt werden müssen.

### Verbindungsspezifikationen nachschlagen

Bevor Sie die API zum Filtern von Daten auf Zeilenebene für eine Quelle verwenden können, müssen Sie zunächst die Verbindungsspezifikationsdetails Ihrer Quelle abrufen, um die von einer bestimmten Quelle unterstützten Operatoren und Sprachen zu bestimmen.

Um die Verbindungsspezifikation einer bestimmten Quelle abzurufen, stellen Sie eine GET-Anfrage an die `/connectionSpecs` Endpunkt der [!DNL Flow Service] API bei Angabe des Eigenschaftsnamens Ihrer Quelle als Teil Ihrer Abfrageparameter.

**API-Format**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMS}` | Die optionalen Abfrageparameter, nach denen Ergebnisse gefiltert werden sollen. Sie können die [!DNL Google BigQuery] Verbindungsspezifikation durch Anwendung der `name` Eigenschaft und Festlegen `"google-big-query"` in Ihrer Suche. |

**Anfrage**

Die folgende Anfrage ruft Verbindungsspezifikationen für ab [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Verbindungsspezifikationen für [!DNL Google BigQuery], einschließlich Informationen zur unterstützten Abfragesprache und logischen Operatoren.

>[!NOTE]
>
>Die nachstehende API-Antwort wird aus Gründen der Kürze abgeschnitten.

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes.filterAtSource.enabled` | Bestimmt, ob die abgefragte Quelle das Filtern von Daten auf Zeilenebene unterstützt. |
| `attributes.filterAtSource.queryLanguage` | Bestimmt die Abfragesprache, die die abgefragte Quelle unterstützt. |
| `attributes.filterAtSource.logicalOperators` | Bestimmt die logischen Operatoren, mit denen Sie Daten auf Zeilenebene für Ihre Quelle filtern können. |
| `attributes.filterAtSource.comparisonOperators` | Bestimmt Vergleichsoperatoren, mit denen Sie Daten auf Zeilenebene für Ihre Quelle filtern können. Weitere Informationen zu Vergleichsoperatoren finden Sie in der unten stehenden Tabelle. |
| `attributes.filterAtSource.columnNameEscapeChar` | Legt das Zeichen fest, das als Escape-Zeichen für Spalten verwendet werden soll. |
| `attributes.filterAtSource.valueEscapeChar` | Bestimmt, wie Werte beim Schreiben einer SQL-Abfrage eingebunden werden. |

{style=&quot;table-layout:auto&quot;}

#### Vergleichsoperatoren 

| Operator | Beschreibung |
| --- | --- |
| `==` | Filtert danach, ob die Eigenschaft dem bereitgestellten Wert entspricht. |
| `!=` | Filtert danach, ob die Eigenschaft nicht mit dem bereitgestellten Wert übereinstimmt. |
| `<` | Filtert danach, ob die Eigenschaft kleiner als der angegebene Wert ist. |
| `>` | Filtert danach, ob die Eigenschaft größer als der angegebene Wert ist. |
| `<=` | Filtert danach, ob die Eigenschaft kleiner oder gleich dem angegebenen Wert ist. |
| `>=` | Filtert danach, ob die Eigenschaft größer oder gleich dem angegebenen Wert ist. |
| `like` | Filter durch Verwendung in einer `WHERE` -Klausel, um nach einem angegebenen Muster zu suchen. |
| `in` | Filtert nach, ob sich die Eigenschaft innerhalb eines angegebenen Bereichs befindet. |

{style=&quot;table-layout:auto&quot;}

### Filterbedingungen für die Aufnahme festlegen

Nachdem Sie die von Ihrer Quelle unterstützten logischen Operatoren und Abfragesprachen identifiziert haben, können Sie mithilfe der Profile Query Language (PQL) die Filterbedingungen festlegen, die auf Ihre Quelldaten angewendet werden sollen.

Im folgenden Beispiel werden Bedingungen nur auf ausgewählte Daten angewendet, die den bereitgestellten Werten für die Knotentypen entsprechen, die als Parameter aufgeführt sind.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### Datenvorschau

Sie können eine Vorschau Ihrer Daten anzeigen, indem Sie eine GET an die `/explore` Endpunkt der [!DNL Flow Service] API bei Bereitstellung `filters` als Teil Ihrer Abfrageparameter verwenden und Ihre PQL-Eingabebedingungen in [!DNL Base64].

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Kennung der Basisverbindung Ihrer Quelle. |
| `{TABLE_PATH}` | Die Pfadeigenschaft der Tabelle, die Sie überprüfen möchten. |
| `{FILTERS}` | Ihre PQL-Filterbedingungen, die in [!DNL Base64]. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Anfrage gibt die folgende Antwort zurück.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### Quellverbindung für gefilterte Daten erstellen

Um eine Quellverbindung zu erstellen und gefilterte Daten zu erfassen, stellen Sie eine POST-Anfrage an die `/sourceConnections` -Endpunkt hinzugefügt werden, während Sie Ihre Filterbedingungen als Teil Ihrer Hauptteilparameter angeben.

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Quellverbindung zum Erfassen von Daten aus `test1.fasTestTable` where `city` = `DDN`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Anhang

Dieser Abschnitt enthält weitere Beispiele für verschiedene Payloads zum Filtern.

### Besondere Bedingungen

Sie können die anfängliche `fnApply` für Szenarien, die nur eine Bedingung erfordern.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### Verwenden der `in` operator

Ein Beispiel für den Operator finden Sie unten in der Beispiel-Payload . `in`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### Verwenden der `isNull` operator

Ein Beispiel für den Operator finden Sie unten in der Beispiel-Payload . `isNull`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### Verwenden der `NOT` operator

Ein Beispiel für den Operator finden Sie unten in der Beispiel-Payload . `NOT`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### Beispiel mit verschachtelten Bedingungen

Ein Beispiel für komplexe verschachtelte Bedingungen finden Sie unten in der Beispiel-Payload .

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
