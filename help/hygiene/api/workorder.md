---
title: API-Endpunkt für Arbeitsauftrag
description: Mit dem /workorder -Endpunkt in der Data Hygiene API können Sie Löschaufgaben für Verbraucheridentitäten programmgesteuert verwalten.
source-git-commit: 931b847761e649696aa8433d53233593efd4d1ee
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 5%

---

# Arbeitserstellungsendpunkt

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Adobe Shield für das Gesundheitswesen erworben haben.

Die `/workorder` -Endpunkt in der Data Hygiene API ermöglicht Ihnen die programmgesteuerte Verwaltung von Löschaufgaben für Verbraucheridentitäten in Adobe Experience Platform.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie bitte die [Übersicht](./overview.md) für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Identitäten löschen {#delete-identities}

Sie können eine oder mehrere Verbraucheridentitäten aus einem Datensatz oder allen Datensätzen löschen, indem Sie eine POST-Anfrage an die `/workorder` -Endpunkt.

**API-Format**

```http
POST /workorder
```

**Anfrage**

Abhängig vom Wert der Variablen `datasetId` in der Anfrage-Payload angegeben wird, löscht der API-Aufruf Verbraucheridentitäten aus allen Datensätzen oder einem einzelnen Datensatz, den Sie angeben. Mit der folgenden Anfrage werden drei Verbraucheridentitäten aus einem bestimmten Datensatz gelöscht.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `action` | Die auszuführende Aktion. Der Wert muss auf `delete_identity` beim Löschen von Identitäten. |
| `datasetId` | Wenn Sie aus einem Datensatz löschen, muss dieser Wert die Kennung des betreffenden Datensatzes sein. Wenn Sie aus allen Datensätzen löschen, setzen Sie den Wert auf `ALL`.<br><br>Wenn Sie einen einzelnen Datensatz angeben, muss das zugeordnete Experience-Datenmodell (XDM)-Schema des Datensatzes über eine primäre Identität verfügen. |
| `identities` | Ein Array, das die Identitäten von mindestens einem Benutzer enthält, dessen Informationen Sie löschen möchten. Jede Identität besteht aus einer [Identitäts-Namespace](../../identity-service/namespaces.md) und einen Wert:<ul><li>`namespace`: Enthält eine einzelne String-Eigenschaft, `code`, der den Identitäts-Namespace darstellt. </li><li>`id`: Der Identitätswert.</ul>Wenn `datasetId` gibt einen einzelnen Datensatz an, wobei jede Entität unter `identities` muss denselben Identitäts-Namespace wie die primäre Identität des Schemas verwenden.<br><br>Wenn `datasetId` auf `ALL`, die `identities` -Array ist nicht auf einen einzelnen Namespace beschränkt, da jeder Datensatz anders sein kann. Ihre Anforderungen sind jedoch weiterhin auf die Namespaces beschränkt, die Ihrer Organisation zur Verfügung stehen, wie von [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Identitätslöschens zurück.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die ID der Löschreihenfolge. Dies kann verwendet werden, um den Status des Löschvorgangs später nachzuschlagen. |
| `orgId` | Die Kennung Ihres Unternehmens. |
| `batchId` | Die Kennung des Batches, mit dem diese Löschreihenfolge verknüpft ist und der zum Debugging verwendet wird. Mehrere Löschaufträge werden zu einem Batch gebündelt, der von nachgelagerten Diensten verarbeitet werden soll. |
| `bundleOrdinal` | Die Reihenfolge, in der diese Löschreihenfolge empfangen wurde, als sie in einem Batch zur nachgelagerten Verarbeitung gebündelt wurde. Dient zum Debugging. |
| `payloadByteSize` | Die Größe der Liste der Identitäten in Byte, die in der Anfrage-Payload bereitgestellt wurden, die diese Löschreihenfolge erstellt hat. |
| `operationCount` | Die Anzahl der Identitäten, für die diese Löschreihenfolge gilt. |
| `createdAt` | Ein Zeitstempel, der angibt, wann die Löschreihenfolge erstellt wurde. |
| `responseMessage` | Die neueste vom System zurückgegebene Antwort. Tritt bei der Verarbeitung ein Fehler auf, ist dieser Wert eine JSON-Zeichenfolge mit detaillierten Fehlerinformationen, die Ihnen dabei helfen, mögliche Fehler zu verstehen. |
| `status` | Der aktuelle Status der Löschreihenfolge. |
| `createdBy` | Der Benutzer, der die Löschreihenfolge erstellt hat. |

{style=&quot;table-layout:auto&quot;}

## Status aller Identitätslöschungen auflisten {#list}

Sie können die Status aller Identitätslöschungen auflisten, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /workorder?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMS}` | Eine Liste optionaler Abfrageparameter für den Auflistungsaufruf mit mehreren Parametern, getrennt durch `&` Zeichen. Folgende Abfrageparameter werden akzeptiert:<ul><li>`data` - Ein boolescher Wert, der bei Festlegung auf `true`enthält alle zusätzlichen Anfrage- und Antwortdaten, die für die Löschreihenfolge empfangen wurden. Die Standardeinstellung ist `false`.</li><li>`start` - Ein Zeitstempel für den Anfang des Zeitrahmens, um nach Löschanweisungen zu suchen.</li><li>`end` - Ein Zeitstempel für das Ende des Zeitrahmens für die Suche nach Löschanweisungen.</li><li>`page` - Die spezifische Antwortseite, die zurückgegeben werden soll.</li><li>`limit` - Die Anzahl der pro Seite anzuzeigenden Datensätze.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details aller Löschvorgänge zurück, einschließlich des aktuellen Status. Die folgende Beispielantwort wurde aus Platzgründen gekürzt.

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `results` | Enthält die Liste der Löschaufträge und deren Details. Weitere Informationen zu den Eigenschaften einer Löschreihenfolge finden Sie in der Beispielantwort im Abschnitt [Nachschlagen einer Löschreihenfolge](#lookup). |
| `total` | Die Gesamtzahl der gefundenen Löschaufträge basierend auf aktuellen Filtern. |
| `count` | Die Gesamtzahl der Löschaufträge, die auf jeder Seite der Antwort gefunden wurden. |
| `_links` | Enthält Paginierungsinformationen, mit denen Sie die restliche Antwort untersuchen können:<ul><li>`next`: Enthält eine URL für die nächste Seite in der Antwort.</li><li>`page`: Enthält eine URL-Vorlage für den Zugriff auf eine andere Seite in der Antwort oder zur Anpassung der Anzahl der auf jeder Seite zurückgegebenen Elemente.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Abrufen des Status eines Identitätslöschens (#lookup)

Nach dem Senden einer Anfrage an [Identität löschen](#delete-identities)können Sie den Status mit einer GET-Anfrage überprüfen.

**API-Format**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{WORK_ORDER_ID}` | Die `workorderId` der Identitätslöschung, die Sie nachschlagen. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Löschvorgangs zurück, einschließlich des aktuellen Status.

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die ID der Löschreihenfolge. Dies kann verwendet werden, um den Status des Löschvorgangs später nachzuschlagen. |
| `orgId` | Die Kennung Ihres Unternehmens. |
| `batchId` | Die Kennung des Batches, mit dem diese Löschreihenfolge verknüpft ist und der zum Debugging verwendet wird. Mehrere Löschaufträge werden zu einem Batch gebündelt, der von nachgelagerten Diensten verarbeitet werden soll. |
| `bundleOrdinal` | Die Reihenfolge, in der diese Löschreihenfolge empfangen wurde, als sie in einem Batch zur nachgelagerten Verarbeitung gebündelt wurde. Dient zum Debugging. |
| `payloadByteSize` | Die Größe der Liste der Identitäten in Byte, die in der Anfrage-Payload bereitgestellt wurden, die diese Löschreihenfolge erstellt hat. |
| `operationCount` | Die Anzahl der Identitäten, für die diese Löschreihenfolge gilt. |
| `createdAt` | Ein Zeitstempel, der angibt, wann die Löschreihenfolge erstellt wurde. |
| `responseMessage` | Die neueste vom System zurückgegebene Antwort. Tritt bei der Verarbeitung ein Fehler auf, ist dieser Wert eine JSON-Zeichenfolge mit detaillierten Fehlerinformationen, die Ihnen dabei helfen, mögliche Fehler zu verstehen. |
| `status` | Der aktuelle Status der Löschreihenfolge. |
| `createdBy` | Der Benutzer, der die Löschreihenfolge erstellt hat. |
