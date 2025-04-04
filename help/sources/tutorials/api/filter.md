---
title: Filtern von Daten auf Zeilenebene für eine Source mithilfe der Flow Service-API
description: In diesem Tutorial werden die Schritte zum Filtern von Daten auf Quellebene mithilfe der Flow Service-API beschrieben
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1823'
ht-degree: 15%

---

# Filtern von Daten auf Zeilenebene für eine Quelle mithilfe der [!DNL Flow Service]-API

>[!AVAILABILITY]
>
>Die Unterstützung für das Filtern von Daten auf Zeilenebene ist derzeit nur für die folgenden Quellen verfügbar:
>
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)
>* [[!DNL Marketo Engage] Standardaktivitäten](../../connectors/adobe-applications/marketo/marketo.md)

Lesen Sie dieses Handbuch für Anweisungen zum Filtern von Daten auf Zeilenebene für eine Quelle mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../landing/api-guide.md).

## Filtern von Quelldaten {#filter-source-data}

Im Folgenden werden die Schritte beschrieben, die zum Filtern von Daten auf Zeilenebene für Ihre Quelle unternommen werden müssen.

### Abrufen der Verbindungsspezifikationen {#retrieve-your-connection-specs}

Der erste Schritt beim Filtern von Daten auf Zeilenebene für Ihre Quelle besteht darin, die Verbindungsspezifikationen Ihrer Quelle abzurufen und die Operatoren und die Sprache zu bestimmen, die Ihre Quelle unterstützt.

Um die Verbindungsspezifikation einer bestimmten Quelle abzurufen, stellen Sie eine GET-Anfrage an den `/connectionSpecs`-Endpunkt der [!DNL Flow Service]-API und geben Sie den Eigenschaftsnamen Ihrer Quelle als Teil Ihrer Abfrageparameter an.

**API-Format**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMS}` | Die optionalen Abfrageparameter zum Filtern der Ergebnisse nach . Sie können die [!DNL Google BigQuery] Verbindungsspezifikation abrufen, indem Sie die `name`-Eigenschaft anwenden und bei der Suche `"google-big-query"` angeben. |

+++Anfrage

Die folgende Anfrage ruft die Verbindungsspezifikationen für [!DNL Google BigQuery] ab.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Antwort

Bei einer erfolgreichen Antwort werden der Status-Code 200 und die Verbindungsspezifikationen für [!DNL Google BigQuery] zurückgegeben, einschließlich Informationen zu der unterstützten Abfragesprache und den logischen Operatoren.

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
| `attributes.filterAtSource.enabled` | Legt fest, ob die abgefragte Quelle das Filtern nach Daten auf Zeilenebene unterstützt. |
| `attributes.filterAtSource.queryLanguage` | Bestimmt die Abfragesprache, die die abgefragte Quelle unterstützt. |
| `attributes.filterAtSource.logicalOperators` | Bestimmt die logischen Operatoren, mit denen Sie Daten auf Zeilenebene für Ihre Quelle filtern können. |
| `attributes.filterAtSource.comparisonOperators` | Bestimmt Vergleichsoperatoren, mit denen Sie Daten auf Zeilenebene für Ihre Quelle filtern können. Weitere Informationen zu Vergleichsoperatoren finden Sie in der folgenden Tabelle. |
| `attributes.filterAtSource.columnNameEscapeChar` | Bestimmt das Zeichen, das zum Maskieren von Spalten verwendet werden soll. |
| `attributes.filterAtSource.valueEscapeChar` | Bestimmt, wie Werte beim Schreiben einer SQL-Abfrage eingeschlossen werden. |

{style="table-layout:auto"}

+++

#### Vergleichsoperatoren  {#comparison-operators}

| Operator | Beschreibung |
| --- | --- |
| `==` | Filtert, ob die Eigenschaft dem angegebenen Wert entspricht. |
| `!=` | Filtert danach, ob die Eigenschaft dem angegebenen Wert nicht entspricht. |
| `<` | Filtert nach dem Wert, ob die Eigenschaft kleiner als der angegebene Wert ist. |
| `>` | Filtert danach, ob die Eigenschaft größer als der angegebene Wert ist. |
| `<=` | Filtert danach, ob die Eigenschaft kleiner oder gleich dem angegebenen Wert ist. |
| `>=` | Filtert danach, ob die Eigenschaft größer oder gleich dem angegebenen Wert ist. |
| `like` | Filtert, indem sie in einer `WHERE` verwendet wird, um nach einem angegebenen Muster zu suchen. |
| `in` | Filtert nach dem Wert, ob sich die Eigenschaft innerhalb eines angegebenen Bereichs befindet. |

{style="table-layout:auto"}

### Filterbedingungen für die Aufnahme angeben {#specify-filtering-conditions-for-ingestion}

Nachdem Sie die logischen Operatoren und die Abfragesprache identifiziert haben, die Ihre Quelle unterstützt, können Sie mit Profile Query Language (PQL) die Filterbedingungen angeben, die Sie auf Ihre Quelldaten anwenden möchten.

Im folgenden Beispiel werden Bedingungen angewendet, um nur Daten auszuwählen, die den bereitgestellten Werten für die als Parameter aufgelisteten Knotentypen entsprechen.

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

### Vorschau der Daten {#preview-your-data}

Sie können eine Vorschau Ihrer Daten anzeigen, indem Sie eine GET-Anfrage an den `/explore`-Endpunkt der [!DNL Flow Service]-API stellen, während Sie `filters` als Teil Ihrer Abfrageparameter angeben und Ihre PQL-Eingabebedingungen in [!DNL Base64] angeben.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindung Ihrer Quelle. |
| `{TABLE_PATH}` | Die Pfadeigenschaft der Tabelle, die Sie überprüfen möchten. |
| `{FILTERS}` | Ihre in [!DNL Base64] kodierten PQL-Filterbedingungen |

+++Anfrage

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Antwort

Eine erfolgreiche Antwort gibt den Inhalt und die Struktur Ihrer Daten zurück.

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

+++

### Erstellen einer Quellverbindung für gefilterte Daten

Um eine Quellverbindung zu erstellen und gefilterte Daten aufzunehmen, stellen Sie eine POST-Anfrage an den `/sourceConnections`-Endpunkt und geben Sie Ihre Filterbedingungen in den Parametern des Anfragetexts an.

**API-Format**

```http
POST /sourceConnections
```

+++Anfrage

Die folgende Anfrage erstellt eine Quellverbindung zum Aufnehmen von Daten aus `test1.fasTestTable`, wobei `city` = `DDN` ist.

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

+++

+++Antwort

Bei einer erfolgreichen Antwort wird die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurückgegeben.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## Aktivitätsentitäten für [!DNL Marketo Engage] filtern {#filter-for-marketo}

Bei Verwendung des Quell-Connectors können Sie die Filterung auf Zeilenebene verwenden, um nach Aktivitätsentitäten [[!DNL Marketo Engage]  filtern](../../connectors/adobe-applications/marketo/marketo.md). Derzeit können Sie nur nach Aktivitätsentitäten und standardmäßigen Aktivitätstypen filtern. Benutzerdefinierte Aktivitäten werden weiterhin unter [[!DNL Marketo] Feldzuordnungen“ ](../../connectors/adobe-applications/mapping/marketo.md).

### Standard-Aktivitätstypen [!DNL Marketo] {#marketo-standard-activity-types}

In der folgenden Tabelle sind die standardmäßigen Aktivitätstypen für [!DNL Marketo] aufgeführt. Verwenden Sie diese Tabelle als Referenz für Ihre Filterkriterien.

| Aktivitätstyp-ID | Aktivitätstyp-Name |
| --- | --- |
| 1 | Web-Seite besuchen |
| 2 | Formular ausfüllen |
| 3 | Link anklicken |
| 6 | E-Mail senden |
| 7 | E-Mail zugestellt |
| 8 | E-Mail gebounct |
| 9 | E-Mail abmelden |
| 10 | E-Mail öffnen |
| 11 | Click Email |
| 12 | Neuer Lead |
| 21 | Lead konvertieren |
| 22 | Score ändern |
| 24 | Zur Liste hinzufügen |
| 25 | Aus Liste entfernen |
| 27 | E-Mail nicht zugestellt (Soft-Bounce) |
| 32 | Leads zusammenführen |
| 34 | Zur Opportunity hinzufügen |
| 35 | Aus Opportunity entfernen |
| 36 | Opportunity aktualisieren |
| 46 | Interessanter Moment |
| 101 | Umsatzschritt ändern |
| 104 | Statusänderung in Bearbeitung |
| 110 | Webhook aufrufen |
| 113 | Add to Nurture |
| 114 | Pflegespur ändern |
| 115 | Nurture-Kadenz ändern |

{style="table-layout:auto"}

Gehen Sie wie folgt vor, um Ihre standardmäßigen Aktivitätsentitäten bei Verwendung des [!DNL Marketo]-Quell-Connectors zu filtern.

### Erstellen eines Entwurfsdatenflusses

Erstellen Sie zunächst einen [[!DNL Marketo] Datenfluss](../ui/create/adobe-applications/marketo.md) und speichern Sie ihn als Entwurf. Detaillierte Anweisungen zum Erstellen eines Datenflussentwurfs finden Sie in der folgenden Dokumentation:

* [Speichern eines Datenflusses als Entwurf mithilfe der Benutzeroberfläche](../ui/draft.md)
* [Speichern eines Datenflusses als Entwurf mithilfe der API](../api/draft.md)

### Abrufen Ihrer Datenfluss-ID

Nachdem Sie einen Datenfluss-Entwurf erstellt haben, müssen Sie die entsprechende ID abrufen.

Navigieren Sie in der Benutzeroberfläche zum Quellkatalog und wählen Sie **[!UICONTROL Datenflüsse]** in der oberen Kopfzeile aus. Verwenden Sie die Spalte Status , um alle Datenflüsse zu identifizieren, die im Entwurfsmodus gespeichert wurden, und wählen Sie dann den Namen Ihres Datenflusses aus. Verwenden Sie anschließend das Bedienfeld **[!UICONTROL Eigenschaften]** auf der rechten Seite, um Ihre Datenfluss-ID zu finden.

### Abrufen von Datenflussdetails

Als Nächstes müssen Sie Ihre Datenflussdetails abrufen, insbesondere die mit Ihrem Datenfluss verknüpfte Quellverbindungs-ID. Um Ihre Datenflussdetails abzurufen, stellen Sie eine GET-Anfrage an den `/flows`-Endpunkt und geben Sie Ihre Datenfluss-ID als Pfadparameter an.

**API-Format**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{FLOW_ID}` | Die ID des Datenflusses, den Sie abrufen möchten. |

+++Anfrage

Mit der folgenden Anfrage werden Informationen zur Datenfluss-ID abgerufen: `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Antwort

Bei einer erfolgreichen Antwort werden Ihre Datenflussdetails zurückgegeben, einschließlich Informationen zu den entsprechenden Quell- und Zielverbindungen. Sie müssen Ihre Quell- und Zielverbindungs-IDs beachten, da diese Werte später erforderlich sind, um Ihren Datenfluss veröffentlichen zu können.

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### Abrufen von Details zur Quellverbindung

Verwenden Sie anschließend Ihre Quellverbindungs-ID und stellen Sie eine GET-Anfrage an den `/sourceConnections`-Endpunkt, um Ihre Details zur Quellverbindung abzurufen.

**API-Format**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | Die ID der Quellverbindung, die Sie abrufen möchten. |

+++Anfrage

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Antwort

Eine erfolgreiche Antwort gibt die Details Ihrer Quellverbindung zurück. Notieren Sie sich die Version, da Sie diesen Wert im nächsten Schritt benötigen werden, um Ihre Quellverbindung zu aktualisieren.

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### Aktualisieren der Quellverbindung mit Filterbedingungen

Nachdem Sie nun über Ihre Quellverbindungs-ID und die zugehörige Version verfügen, können Sie jetzt eine PATCH-Anfrage mit den Filterbedingungen stellen, die Ihre standardmäßigen Aktivitätstypen angeben.

Um Ihre Quellverbindung zu aktualisieren, stellen Sie eine PATCH-Anfrage an den `/sourceConnections`-Endpunkt und geben Sie Ihre Quellverbindungs-ID als Abfrageparameter an. Darüber hinaus müssen Sie einen `If-Match` Kopfzeilenparameter mit der entsprechenden Version Ihrer Quellverbindung angeben.

>[!TIP]
>
>Die Kopfzeile `If-Match` ist bei einer PATCH-Anfrage erforderlich. Der Wert für diese Kopfzeile ist die eindeutige Version/eTag des Datenflusses, den Sie aktualisieren möchten. Der Versions-/eTag-Wert wird bei jeder erfolgreichen Aktualisierung eines Datenflusses aktualisiert.

**API-Format**

```http
PATCH /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | Die ID der Quellverbindung, die Sie aktualisieren möchten |

+++Anfrage

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++Antwort

Bei einer erfolgreichen Antwort werden Ihre Quellverbindungs-ID und das eTag (Version) zurückgegeben.

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### Veröffentlichen der Quellverbindung

Nachdem Ihre Quellverbindung mit Ihren Filterbedingungen aktualisiert wurde, können Sie jetzt mit dem Status Entwurf fortfahren und Ihre Quellverbindung veröffentlichen. Stellen Sie dazu eine POST-Anfrage an den `/sourceConnections`-Endpunkt und geben Sie die ID Ihrer Entwurfsquellverbindung sowie einen Aktionsvorgang für die Veröffentlichung an.

**API-Format**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschreibung |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | Die ID der Quellverbindung, die Sie veröffentlichen möchten. |
| `op` | Ein Aktionsvorgang, mit dem der Status der abgefragten Quellverbindung aktualisiert wird. Um eine Entwurfsquellverbindung zu veröffentlichen, legen Sie für `op` den Wert `publish` fest. |

+++Anfrage

Die folgende Anfrage veröffentlicht einen Entwurf einer Quellverbindung.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Antwort

Bei einer erfolgreichen Antwort werden Ihre Quellverbindungs-ID und das eTag (Version) zurückgegeben.

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### Veröffentlichen der Zielverbindung

Ähnlich wie im vorherigen Schritt müssen Sie auch Ihre Zielverbindung veröffentlichen, um fortfahren und Ihren Datenflussentwurf veröffentlichen zu können. Stellen Sie eine POST-Anfrage an den `/targetConnections`-Endpunkt und geben Sie die ID der Entwurfs-Zielverbindung an, die Sie veröffentlichen möchten, sowie einen Aktionsvorgang für die Veröffentlichung.

**API-Format**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschreibung |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | Die ID der Zielverbindung, die Sie veröffentlichen möchten. |
| `op` | Ein Aktionsvorgang, mit dem der Status der abgefragten Zielverbindung aktualisiert wird. Um eine Entwurfszielverbindung zu veröffentlichen, legen Sie für `op` den Wert `publish` fest. |

+++Anfrage

Die folgende Anfrage veröffentlicht die Zielverbindung mit der ID: `7e53e6e8-b432-4134-bb29-21fc6e8532e5`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Antwort

Bei einer erfolgreichen Antwort werden die ID und das entsprechende eTag für Ihre veröffentlichte Zielverbindung zurückgegeben.

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### Veröffentlichen des Datenflusses

Nachdem sowohl Ihre Quell- als auch Ihre Zielverbindung veröffentlicht wurden, können Sie jetzt mit dem letzten Schritt fortfahren und Ihren Datenfluss veröffentlichen. Um Ihren Datenfluss zu veröffentlichen, stellen Sie eine POST-Anfrage an den `/flows`-Endpunkt und geben Sie Ihre Datenfluss-ID und einen Aktionsvorgang für die Veröffentlichung an.

**API-Format**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parameter | Beschreibung |
| --- | --- |
| `{FLOW_ID}` | Die ID des Datenflusses, den Sie veröffentlichen möchten. |
| `op` | Ein Aktionsvorgang, der den Status des abgefragten Datenflusses aktualisiert. Um einen Datenfluss-Entwurf zu veröffentlichen, legen Sie `op` auf `publish` fest. |

+++Anfrage

Mit der folgenden Anfrage wird Ihr Datenfluss-Entwurf veröffentlicht.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Antwort

Bei einer erfolgreichen Antwort werden die ID und das entsprechende `etag` Ihres Datenflusses zurückgegeben.

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

Sie können die Experience Platform-Benutzeroberfläche verwenden, um zu überprüfen, ob Ihr Datenflussentwurf veröffentlicht wurde. Navigieren Sie im Quellkatalog zur Seite „Datenflüsse“ und verweisen Sie auf **[!UICONTROL Status]** Ihres Datenflusses. Bei Erfolg sollte der Status jetzt auf „Aktiviert **gesetzt**.

>[!TIP]
>
>* Ein Datenfluss mit aktivierter Filterung wird nur einmal aufgestockt. Alle Änderungen an den Filterkriterien (Hinzufügen oder Entfernen) können nur für inkrementelle Daten wirksam werden.
>* Wenn Sie historische Daten für einen neuen Aktivitätstyp bzw. neue Aktivitätstypen aufnehmen müssen, wird empfohlen, einen neuen Datenfluss zu erstellen und die Filterkriterien mit den entsprechenden Aktivitätstypen in der Filterbedingung zu definieren.
>* Benutzerdefinierte Aktivitäten können nicht gefiltert werden.
>* Sie können keine Vorschau von gefilterten Daten anzeigen.

## Anhang

In diesem Abschnitt finden Sie weitere Beispiele für verschiedene Payloads zum Filtern.

### Singular-Bedingungen

Sie können die anfängliche `fnApply` für Szenarien auslassen, für die nur eine Bedingung erforderlich ist.

+++Beispiel auswählen, um es anzuzeigen

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

+++

### Verwenden des `in` Operators

Ein Beispiel für den `in` finden Sie unten in der Beispiel-Payload .

+++Beispiel auswählen, um es anzuzeigen

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

+++

### Verwenden des `isNull` Operators

+++Beispiel auswählen, um es anzuzeigen

Ein Beispiel für den `isNull` finden Sie unten in der Beispiel-Payload .

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

+++

### Verwenden des `NOT` Operators

Ein Beispiel für den `NOT` finden Sie unten in der Beispiel-Payload .


+++Beispiel auswählen, um es anzuzeigen

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

+++

### Beispiel mit verschachtelten Bedingungen

Ein Beispiel für komplexe verschachtelte Bedingungen finden Sie unten in der Beispiel-Payload .

+++Beispiel auswählen, um es anzuzeigen

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

+++