---
title: Endpunkt für beschleunigte Abfragen
description: Erfahren Sie, wie Sie statuslos auf den abfragebeschleunigten Speicher zugreifen können, um schnell Ergebnisse basierend auf aggregierten Daten zurückzugeben. Dieses Dokument enthält eine beispielhafte HTTP-Anfrage und -Antwort für den Endpunkt für beschleunigte Abfragen des Abfrage-Service.
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: aa209dce9268a15a91db6e3afa7b6066683d76ea
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 97%

---

# Endpunkt für beschleunigte Abfragen

Im Rahmen der Data Distiller SKU ermöglicht Ihnen die [Abfrage-Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/), statuslose Abfragen an den beschleunigten Speicher zu stellen. Die zurückgegebenen Ergebnisse basieren auf aggregierten Daten. Die geringere Latenz der Ergebnisse ermöglicht einen interaktiveren Informationsaustausch. Die APIs für beschleunigte Abfragen werden auch für [benutzerdefinierte Dashboards](../../dashboards/user-defined-dashboards.md) verwendet.

Bevor Sie mit diesem Handbuch fortfahren, stellen Sie sicher, dass Sie das [Handbuch zur Abfrage-Service-API](./getting-started.md) gelesen und verstanden haben, um die Abfrage-Service-API erfolgreich verwenden zu können.

## Erste Schritte

Die Data Distiller SKU ist erforderlich, um den abfragebeschleunigten Speicher zu verwenden. Siehe [Verpackung](../packages.md) und [Limits](../guardrails.md#query-accelerated-store) Dokumentation, die sich auf die Data Distiller SKU bezieht. Wenn Sie nicht über die Data Distiller SKU verfügen, wenden Sie sich bitte an den Adobe-Support, um weitere Informationen zu erhalten.

<!-- Document is hidden temporarily
Please see the [packaging](../packages.md), [guardrails](../guardrails.md#query-accelerated-store), and [licensing](../data-distiller/license-usage.md) documentation that relates to the Data Distiller SKU. 
-->

In den folgenden Abschnitten werden die API-Aufrufe beschrieben, die für den statuslosen Zugriff auf den abfragebeschleunigten Speicher über die Abfrage-Service-API erforderlich sind. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

## Ausführen einer beschleunigten Abfrage {#run-accelerated-query}

Stellen Sie eine POST-Anfrage an den `/accelerated-queries`-Endpunkt, um eine beschleunigte Abfrage auszuführen. Die Abfrage ist entweder direkt in der Payload der Anfrage enthalten oder wird mit einer Vorlagen-ID referenziert.

**API-Format**

```shell
POST /accelerated-queries
```

### Anfrage

>[!IMPORTANT]
>
>Anfragen an den `/accelerated-queries`-Endpunkt erfordern entweder eine SQL-Anweisung ODER eine Vorlagen-ID, aber nicht beides. Die Übermittlung beider Elemente in einer Anfrage führt zu einem Fehler.

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

Diese alternative Anfrage sendet eine Vorlagen-ID im Anfragetext an den beschleunigten Speicher. Die SQL aus der entsprechenden Vorlage wird zum Abfragen des beschleunigten Speichers verwendet.

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
| `dbName` | Der Name der Datenbank, für die Sie eine beschleunigte Abfrage stellen. Der Wert für `dbName` sollte das Format `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}` haben. Die angegebene Datenbank muss im beschleunigten Speicher vorhanden sein. Andernfalls führt die Anfrage zu einem Fehler. Sie müssen zudem sicherstellen, dass die Kopfzeile `x-sandbox-name` und der Sandbox-Name in `dbName` auf dieselbe Sandbox verweisen. |
| `sql` | Eine SQL-Anweisungszeichenfolge. Die maximal zulässige Größe beträgt 1.000.000 Zeichen. |
| `templateId` | Die eindeutige Kennung einer Abfrage, die bei einer POST-Anfrage an den `/templates`-Endpunkt erstellt und als Vorlage gespeichert wird. |
| `name` | Ein optionaler benutzerfreundlicher, beschreibender Name für die beschleunigte Abfrage. |
| `description` | Ein optionaler Kommentar zur Zielsetzung der Abfrage, der anderen Benutzenden hilft, den Zweck zu verstehen. Die maximal zulässige Größe beträgt 1.000 Byte. |

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit dem von der Abfrage erstellten Ad-hoc-Schema zurückgegeben.

>[!NOTE]
>
>Die folgende Antwort wurde zur Vereinfachung gekürzt.

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
| `resultsMeta` | Dieses Objekt enthält die Metadaten für jede Spalte, die in den Ergebnissen zurückgegeben wird, damit Benutzende den Namen und den Typ jeder Spalte kennen. |
| `resultsMeta._adhoc` | Ein Ad-hoc-Schema des Experience-Datenmodells (XDM) mit Feldern, die für die Verwendung durch nur einen einzigen Datensatz mit einem Namespace versehen wurden. |
| `resultsMeta._adhoc.type` | Der Datentyp des Ad-hoc-Schemas. |
| `resultsMeta._adhoc.meta:xdmType` | Dies ist ein systemgenerierter Wert für den XDM-Feldtyp. Weitere Informationen zu den verfügbaren Typen finden Sie in der Dokumentation zu den [verfügbaren XDM-Typen](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/custom-fields-api.html?lang=de). |
| `resultsMeta._adhoc.properties` | Dies sind die Spaltennamen des abgefragten Datensatzes. |
| `resultsMeta._adhoc.results` | Dies sind die Zeilennamen des abgefragten Datensatzes. Sie spiegeln jede der zurückgegebenen Spalten wider. |
