---
title: Accelerated Queries Endpoint
description: Erfahren Sie, wie Sie statuslos auf den Abfrage-beschleunigten Speicher zugreifen können, um schnell Ergebnisse basierend auf aggregierten Daten zurückzugeben. Dieses Dokument enthält eine Beispiel-HTTP-Anforderung und -Antwort für den Endpunkt "Schnellabfragen"in Query Service.
source-git-commit: 2a9d40fc783feb78a1d5ad7eb615ceb40097eb89
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 11%

---

# Accelerated Query Endpoint

Im Rahmen der Data Distiller-SKU muss die [Query Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/) ermöglicht es Ihnen, stateless-Abfragen an den beschleunigten Speicher zu senden. Die zurückgegebenen Ergebnisse basieren auf aggregierten Daten. Die geringere Latenz der Ergebnisse ermöglicht einen interaktiveren Informationsaustausch. Die APIs für beschleunigte Abfragen werden auch verwendet, um [Benutzerdefinierte Dashboards](../../dashboards/user-defined-dashboards.md).

Bevor Sie mit diesem Handbuch fortfahren, stellen Sie sicher, dass Sie die [Handbuch zur Query Service-API](./getting-started.md) , um die Query Service-API erfolgreich zu verwenden.

## Erste Schritte

Die Data Distiller-SKU ist erforderlich, um den Abfrage-beschleunigten Store zu verwenden. Bitte beachten Sie die Dokumentation zu [Packaging](../packages.md), [Leitlinien](../guardrails.md#query-accelerated-store) und [Lizenzierung](../data-distiller/licence-usage.md), die sich auf die Data Distiller SKU bezieht. Wenn Sie nicht über die Data Distiller SKU verfügen, wenden Sie sich bitte an den Adobe-Support, um weitere Informationen zu erhalten.

In den folgenden Abschnitten werden die API-Aufrufe beschrieben, die für den statuslosen Zugriff auf den Abfrage-beschleunigten Speicher über die Query Service-API erforderlich sind. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

## Beschleunigte Abfrage ausführen {#run-accelerated-query}

Stellen Sie eine POST-Anfrage an die `/accelerated-queries` Endpunkt zum Ausführen einer beschleunigten Abfrage. Die Abfrage ist entweder direkt in der Anfrage-Payload enthalten oder wird mit einer Vorlagen-ID referenziert.

**API-Format**

```shell
POST /accelerated-queries
```

### Anfrage

>[!IMPORTANT]
>
>Anforderungen an `/accelerated-queries` -Endpunkt erfordert entweder eine SQL-Anweisung ODER eine Vorlagen-ID, aber nicht beide. Die Übermittlung beider Elemente in einer Anfrage führt zu einem Fehler.

Mit der folgenden Anfrage wird eine SQL-Abfrage im Anfragetext an den beschleunigten Speicher gesendet.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

Diese alternative Anfrage sendet eine Vorlagen-ID im Anfrageinhalt an den beschleunigten Speicher. Die SQL aus der entsprechenden Vorlage wird zum Abfragen des beschleunigten Stores verwendet.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| Eigenschaft | Beschreibung |
|---|---|
| `dbName` | Der Name der Datenbank, an die Sie eine beschleunigte Abfrage durchführen. Der Wert für `dbName` sollte das Format `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. Die bereitgestellte Datenbank muss im beschleunigten Speicher vorhanden sein. Andernfalls wird die Anfrage zu einem Fehler führen. Sie müssen auch sicherstellen, dass die Variable `x-sandbox-name` Kopfzeile und Sandbox-Name in `dbName` auf dieselbe Sandbox verweisen. |
| `sql` | Eine SQL-Anweisungszeichenfolge. Die maximal zulässige Größe beträgt 1000000 Zeichen. |
| `templateId` | Die eindeutige Kennung einer Abfrage, die bei einer POST-Anfrage an die `/templates` -Endpunkt. |
| `name` | Ein optionaler benutzerfreundlicher, beschreibender Name für die beschleunigte Abfrage. |
| `description` | Ein optionaler Kommentar zum Zweck der Abfrage, der anderen Benutzern beim Verständnis des Zwecks hilft. Die maximal zulässige Größe beträgt 1.000 Byte. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit dem von der Abfrage erstellten Ad-hoc-Schema zurück.

>[!NOTE]
>
>Die folgende Antwort wurde aus Gründen der Kürze abgeschnitten.

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `queryId` | Der ID-Wert der erstellten Abfrage. |
| `resultsMeta` | Dieses Objekt enthält die Metadaten für jede Spalte, die in den Ergebnissen zurückgegeben wird, damit Benutzer den Namen und den Typ jeder Spalte kennen. |
| `resultsMeta._adhoc` | Ein Ad-hoc-Experience-Datenmodell (XDM)-Schema mit Feldern, die nur für die Verwendung durch einen einzigen Datensatz benannt wurden. |
| `resultsMeta._adhoc.type` | Der Datentyp des Ad-hoc-Schemas. |
| `resultsMeta._adhoc.meta:xdmType` | Dies ist ein systemgenerierter Wert für den XDM-Feldtyp. Weitere Informationen zu den verfügbaren Typen finden Sie in der Dokumentation unter [Verfügbare XDM-Typen](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/custom-fields-api.html). |
| `resultsMeta._adhoc.properties` | Dies sind die Spaltennamen des abgefragten Datensatzes. |
| `resultsMeta._adhoc.results` | Dies sind die Zeilennamen des abgefragten Datensatzes. Sie spiegeln jede der zurückgegebenen Spalten wider. |

