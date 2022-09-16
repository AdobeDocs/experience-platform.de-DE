---
title: API-Endpunkt für Arbeitsaufträge
description: Mit dem Endpunkt /workorder in der Data Hygiene API können Sie Löschaufgaben für Verbraucheridentitäten programmgesteuert verwalten.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 100%

---

# Arbeitsauftrags-Endpunkt

>[!IMPORTANT]
>
>Die Datenhygiene-Funktionen in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Healthcare Shield erworben haben.

Mit dem Endpunkt `/workorder` in der Data Hygiene API können Sie in Adobe Experience Platform Löschaufgaben für Verbraucheridentitäten programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie die [Übersicht](./overview.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Löschen von Identitäten {#delete-identities}

Sie können eine oder mehrere Verbraucheridentitäten aus einem einzelnen Datensatz oder allen Datensätzen löschen, indem Sie eine POST-Anfrage an den `/workorder`-Endpunkt stellen.

**API-Format**

```http
POST /workorder
```

**Anfrage**

Abhängig vom Wert der `datasetId` in der Anfrage-Payload löscht der API-Aufruf Verbraucheridentitäten aus allen Datensätzen oder einem einzelnen von Ihnen angegebenen Datensatz. Mit der folgenden Anfrage werden drei Verbraucheridentitäten aus einem Datensatz gelöscht.

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
| `action` | Die auszuführende Aktion. Zum Löschen von Identitäten muss für den Wert `delete_identity` ausgewählt werden. |
| `datasetId` | Wenn Sie Identitäten aus einem einzelnen Datensatz löschen, muss dieser Wert die Kennung des betreffenden Datensatzes sein. Wenn Sie Identitäten aus allen Datensätzen löschen, setzen Sie den Wert auf `ALL`.<br><br>Wenn Sie einen einzelnen Datensatz angeben, muss für das zugeordnete Experience-Datenmodell-Schema (XDM) des Datensatzes eine primäre Identität definiert sein. |
| `identities` | Ein Array mit den Identitäten von mindestens einem Benutzer, dessen Informationen Sie löschen möchten. Jede Identität besteht aus einem [Identity-Namespace](../../identity-service/namespaces.md) und einem Wert:<ul><li>`namespace`: enthält die einzige Zeichenfolgen-Eigenschaft `code`, die den Identity-Namespace darstellt. </li><li>`id`: der Identitätswert.</ul>Wenn `datasetId` einen einzelnen Datensatz spezifiziert, muss jede Entität unter `identities` denselben Identity-Namespace wie die primäre Identität des Schemas verwenden.<br><br>Wenn `datasetId` auf `ALL` festgelegt ist, ist das `identities`-Array nicht auf einen einzigen Namespace beschränkt, da jeder Datensatz anders sein kann. Ihre Anfragen sind aber auf die Namespaces beschränkt, die Ihrer Organisation zur Verfügung stehen, wie von [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces) spezifiziert. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Identitätslöschung zurück.

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
| `workorderId` | Die ID des Löschauftrags. Diese kann verwendet werden, um den Status des Löschvorgangs später anzuzeigen. |
| `orgId` | Die Kennung Ihres Unternehmens. |
| `batchId` | Die Kennung des Batches, mit dem dieser Löschauftrag verknüpft ist. Sie wird zur Fehlerbehebung verwendet. Mehrere Löschaufträge werden zu einem Batch zusammengefasst, der von nachgelagerten Services verarbeitet wird. |
| `bundleOrdinal` | Die Reihenfolge, in der dieser Löschauftrag empfangen wurde, als er in einem Batch zur nachgelagerten Verarbeitung zusammengefasst wurde. Dient zur Fehlerbehebung. |
| `payloadByteSize` | Die Größe (gemessen in Bytes) der Liste mit Identitäten, die in der Anfrage-Payload bereitgestellt wurden, durch die dieser Löschauftrag erstellt wurde. |
| `operationCount` | Die Anzahl der Identitäten, für die dieser Löschauftrag gilt. |
| `createdAt` | Ein Zeitstempel, der angibt, wann der Löschauftrag erstellt wurde. |
| `responseMessage` | Die jüngste vom System zurückgegebene Antwort. Tritt bei der Verarbeitung ein Fehler auf, ist dieser Wert eine JSON-Zeichenfolge mit detaillierten Fehlerinformationen, die Ihnen dabei helfen, mögliche Fehler zu verstehen. |
| `status` | Der aktuelle Status des Löschauftrags. |
| `createdBy` | Der Benutzer, der den Löschauftrag erstellt hat. |

{style=&quot;table-layout:auto&quot;}

## Auflistung der Status aller Identitätslöschungen {#list}

Sie können die Status aller Identitätslöschungen auflisten, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /workorder?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMS}` | Eine Liste optionaler Abfrageparameter für den Auflistungsaufruf mit mehreren Parametern, die durch `&`-Zeichen getrennt sind. Folgende Abfrageparameter werden akzeptiert:<ul><li>`data`: ein boolescher Wert, der bei Festlegung auf `true` alle zusätzlichen Anfrage- und Antwortdaten enthält, die für den Löschauftrag empfangen wurden. Die Standardeinstellung ist `false`.</li><li>`start`: ein Zeitstempel für den Beginn des Zeitrahmens für die Suche nach Löschaufträgen.</li><li>`end`: ein Zeitstempel für das Ende des Zeitrahmens für die Suche nach Löschaufträgen.</li><li>`page`: die spezifische Antwortseite, die zurückgegeben werden soll.</li><li>`limit`: die Anzahl der pro Seite anzuzeigenden Datensätze.</li></ul> |

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

Eine erfolgreiche Antwort gibt die Details aller Löschvorgänge zurück, einschließlich ihres aktuellen Status. Die folgende Beispielantwort wurde aus Platzgründen gekürzt.

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
| `results` | Enthält die Liste der Löschaufträge und deren Details. Weitere Informationen zu den Eigenschaften eines Löschauftrags finden Sie in der Beispielantwort im Abschnitt zur [Suche eines Löschauftrags](#lookup). |
| `total` | Die Gesamtzahl der gefundenen Löschaufträge basierend auf den aktuellen Filtern. |
| `count` | Die Gesamtzahl der Löschaufträge, die auf jeder Seite der Antwort gefunden wurden. |
| `_links` | Enthält Paginierungsinformationen, mit denen Sie die restliche Antwort untersuchen können:<ul><li>`next`: enthält eine URL für die nächste Seite in der Antwort.</li><li>`page`: enthält eine URL-Vorlage für den Zugriff auf eine weitere Seite in der Antwort oder zur Anpassung der Anzahl der auf jeder Seite zurückgegebenen Elemente.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Abrufen des Status einer Identitätslöschung (#lookup)

Nach dem Senden einer Anfrage zum [Löschen einer Identität](#delete-identities) können Sie den Status mit einer GET-Anfrage überprüfen.

**API-Format**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{WORK_ORDER_ID}` | Die `workorderId` der Identitätslöschung, nach der Sie suchen. |

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
| `workorderId` | Die ID des Löschauftrags. Diese kann verwendet werden, um den Status des Löschvorgangs später anzuzeigen. |
| `orgId` | Die Kennung Ihres Unternehmens. |
| `batchId` | Die Kennung des Batches, mit dem dieser Löschauftrag verknüpft ist. Sie wird zur Fehlerbehebung verwendet. Mehrere Löschaufträge werden zu einem Batch zusammengefasst, der von nachgelagerten Services verarbeitet wird. |
| `bundleOrdinal` | Die Reihenfolge, in der dieser Löschauftrag empfangen wurde, als er in einem Batch zur nachgelagerten Verarbeitung zusammengefasst wurde. Dient zur Fehlerbehebung. |
| `payloadByteSize` | Die Größe (gemessen in Bytes) der Liste mit Identitäten, die in der Anfrage-Payload bereitgestellt wurden, durch die dieser Löschauftrag erstellt wurde. |
| `operationCount` | Die Anzahl der Identitäten, für die dieser Löschauftrag gilt. |
| `createdAt` | Ein Zeitstempel, der angibt, wann der Löschauftrag erstellt wurde. |
| `responseMessage` | Die jüngste vom System zurückgegebene Antwort. Tritt bei der Verarbeitung ein Fehler auf, ist dieser Wert eine JSON-Zeichenfolge mit detaillierten Fehlerinformationen, die Ihnen dabei helfen, mögliche Fehler zu verstehen. |
| `status` | Der aktuelle Status des Löschauftrags. |
| `createdBy` | Der Benutzer, der den Löschauftrag erstellt hat. |
