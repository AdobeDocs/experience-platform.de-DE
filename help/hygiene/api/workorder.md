---
title: Work Order API Endpoint
description: Mit dem /workorder -Endpunkt in der Data Hygiene API können Sie Löschaufgaben für Identitäten programmgesteuert verwalten.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 56%

---

# [!BADGE Beta]{type=Informative} Arbeitserstellungsendpunkt {#work-order-endpoint}

Die `/workorder` -Endpunkt in der Data Hygiene-API ermöglicht es Ihnen, Löschanfragen von Datensätzen in Adobe Experience Platform programmgesteuert zu verwalten.

>[!IMPORTANT]
> 
Die Funktion zum Löschen von Datensätzen ist derzeit als Beta-Version verfügbar und ist nur in einer **limitierte Version**. Sie steht nicht allen Kunden zur Verfügung. Löschanfragen von Datensätzen sind nur für Organisationen in der eingeschränkten Version verfügbar.
>
Löschvorgänge von Datensätzen dienen zur Datenbereinigung, zum Entfernen anonymer Daten oder zur Datenminimierung. Sie dürfen **nicht** für Anfragen zu den Rechten der betroffenen Personen (Compliance) verwendet werden, da sie sich auf Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) beziehen. Verwenden Sie stattdessen [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) für alle Compliance-Anwendungsfälle.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie die [Übersicht](./overview.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Datensatzlöschanfrage erstellen {#create}

Sie können eine oder mehrere Identitäten aus einem Datensatz oder allen Datensätzen löschen, indem Sie eine POST-Anfrage an die `/workorder` -Endpunkt.

>[!IMPORTANT]
> 
Es gibt unterschiedliche Beschränkungen für die Gesamtzahl der eindeutigen Identitätsdatensätze, die jeden Monat gesendet werden können. Diese Beschränkungen basieren auf Ihrem Lizenzvertrag. Organisationen, die alle Editionen von Adobe Real-time Customer Data Platform und Adobe Journey Optimizer erworben haben, können jeden Monat bis zu 100.000 Identitätsdatensätze löschen. Organisationen, die gekauft haben **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** kann jeden Monat bis zu 600.000 Identitätsdatensätze löschen.<br>Ein [Löschanfrage über die Benutzeroberfläche aufzeichnen](../ui/record-delete.md) ermöglicht die gleichzeitige Übermittlung von 10.000 IDs. Die API-Methode zum Löschen von Datensätzen ermöglicht die gleichzeitige Übermittlung von 100.000 IDs.<br>Es empfiehlt sich, bis zu Ihrer ID-Grenze so viele IDs pro Anfrage wie möglich zu senden. Wenn Sie eine große Anzahl von IDs löschen möchten, sollte vermieden werden, ein geringes Volumen oder eine einzelne ID pro Datensatz-Löschanfrage zu senden.

**API-Format**

```http
POST /workorder
```

>[!NOTE]
>
Datenlebenszyklusanfragen können Datensätze nur basierend auf primären Identitäten oder einer Identitätszuordnung ändern. Eine Anfrage muss entweder die primäre Identität angeben oder eine Identitätszuordnung bereitstellen.

**Anfrage**

Abhängig vom Wert der Variablen `datasetId` in der Anfrage-Payload angegeben wird, löscht der API-Aufruf Identitäten aus allen Datensätzen oder einem einzelnen Datensatz, den Sie angeben. Die folgende Anfrage löscht drei Identitäten aus einem bestimmten Datensatz.

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
        "displayName": "Example Record Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
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
| `action` | Die auszuführende Aktion. Der Wert muss auf `delete_identity` zum Löschen von Datensätzen. |
| `datasetId` | Wenn Sie Identitäten aus einem einzelnen Datensatz löschen, muss dieser Wert die Kennung des betreffenden Datensatzes sein. Wenn Sie Identitäten aus allen Datensätzen löschen, setzen Sie den Wert auf `ALL`.<br><br>Wenn Sie einen einzelnen Datensatz angeben, muss das zugeordnete Experience-Datenmodell (XDM)-Schema des Datensatzes über eine primäre Identität verfügen. Wenn der Datensatz keine primäre Identität hat, muss er über eine Identitätszuordnung verfügen, damit er durch eine Data Lifecycle-Anfrage geändert werden kann.<br>Wenn eine Identitätszuordnung vorhanden ist, wird sie als Feld der obersten Ebene mit dem Namen `identityMap`.<br>Beachten Sie, dass eine Datensatzzeile in ihrer Identitätszuordnung zwar viele Identitäten aufweisen kann, jedoch nur eine als primär markiert werden kann. `"primary": true` muss enthalten sein, um die `id` , um eine primäre Identität zuzuordnen. |
| `displayName` | Der Anzeigename für die Löschanfrage zum Datensatz. |
| `description` | Eine Beschreibung für die Anfrage zum Löschen von Datensätzen. |
| `identities` | Ein Array mit den Identitäten von mindestens einem Benutzer, dessen Informationen Sie löschen möchten. Jede Identität besteht aus einem [Identity-Namespace](../../identity-service/features/namespaces.md) und einem Wert:<ul><li>`namespace`: enthält die einzige Zeichenfolgen-Eigenschaft `code`, die den Identity-Namespace darstellt. </li><li>`id`: der Identitätswert.</ul>Wenn `datasetId` einen einzelnen Datensatz spezifiziert, muss jede Entität unter `identities` denselben Identity-Namespace wie die primäre Identität des Schemas verwenden.<br><br>Wenn `datasetId` auf `ALL` festgelegt ist, ist das `identities`-Array nicht auf einen einzigen Namespace beschränkt, da jeder Datensatz anders sein kann. Ihre Anfragen sind aber auf die Namespaces beschränkt, die Ihrer Organisation zur Verfügung stehen, wie von [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces) spezifiziert. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Löschvorgangs des Datensatzes zurück.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die ID des Löschauftrags. Diese kann verwendet werden, um den Status des Löschvorgangs später anzuzeigen. |
| `orgId` | Ihre Organisations-ID. |
| `bundleId` | ID des Pakets, dem dieser Löschauftrag zugeordnet ist. Sie wird zur Fehlerbehebung verwendet. Mehrere Löschaufträge werden zu einem Paket zusammengefasst, das von nachgelagerten Services verarbeitet wird. |
| `action` | Aktion, die bei dem Arbeitsauftrag ausgeführt wird. Bei Datensatzlöschungen lautet der Wert `identity-delete`. |
| `createdAt` | Zeitstempel, der angibt, wann der Löschauftrag erstellt wurde. |
| `updatedAt` | Zeitstempel, der angibt, wann der Löschauftrag zuletzt aktualisiert wurde. |
| `status` | Der aktuelle Status des Löschauftrags. |
| `createdBy` | Der Benutzer, der den Löschauftrag erstellt hat. |
| `datasetId` | ID des Datensatzes, der Gegenstand der Anfrage ist. Wenn die Anfrage alle Datensätze betrifft, wird der Wert auf `ALL` gesetzt |

{style="table-layout:auto"}

## Abrufen des Status eines Datensatzlöschens (#lookup)

Nachher [Erstellen einer Löschanfrage für Datensätze](#create)können Sie den Status mit einer GET-Anfrage überprüfen.

**API-Format**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{WORK_ORDER_ID}` | Die `workorderId` des Datensatzes löschen, den Sie nachschlagen. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Löschvorgangs zurück, einschließlich des aktuellen Status.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die ID des Löschauftrags. Diese kann verwendet werden, um den Status des Löschvorgangs später anzuzeigen. |
| `orgId` | Ihre Organisations-ID. |
| `bundleId` | ID des Pakets, dem dieser Löschauftrag zugeordnet ist. Sie wird zur Fehlerbehebung verwendet. Mehrere Löschaufträge werden zu einem Paket zusammengefasst, das von nachgelagerten Services verarbeitet wird. |
| `action` | Aktion, die bei dem Arbeitsauftrag ausgeführt wird. Bei Datensatzlöschungen lautet der Wert `identity-delete`. |
| `createdAt` | Zeitstempel, der angibt, wann der Löschauftrag erstellt wurde. |
| `updatedAt` | Zeitstempel, der angibt, wann der Löschauftrag zuletzt aktualisiert wurde. |
| `status` | Der aktuelle Status des Löschauftrags. |
| `createdBy` | Der Benutzer, der den Löschauftrag erstellt hat. |
| `datasetId` | ID des Datensatzes, der Gegenstand der Anfrage ist. Wenn die Anfrage alle Datensätze betrifft, wird der Wert auf `ALL` gesetzt |
| `productStatusDetails` | Array, das den aktuellen Status der nachgelagerten Prozesse im Zusammenhang mit der Anfrage auflistet. Jedes Array-Objekt enthält die folgenden Eigenschaften:<ul><li>`productName`: Name des nachgelagerten Services.</li><li>`productStatus`: Aktueller Verarbeitungsstatus der Anfrage von dem nachgelagerten Service.</li><li>`createdAt`: Zeitstempel, der angibt, wann der letzte Status von dem Service veröffentlicht wurde.</li></ul> |

## Aktualisieren von Löschanfragen für Datensätze

Sie können die `displayName` und `description` für einen Datensatz löschen, indem Sie eine PUT-Anfrage stellen.

**API-Format**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{WORK_ORDER_ID}` | Die `workorderId` des Datensatzes löschen, den Sie nachschlagen. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `displayName` | Ein aktualisierter Anzeigename für die Löschanfrage zum Datensatz. |
| `description` | Eine aktualisierte Beschreibung für die Anfrage zum Löschen von Datensätzen. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Löschvorgangs des Datensatzes zurück.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName" : "Update - displayName",
  "description" : "Update - description",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die ID des Löschauftrags. Diese kann verwendet werden, um den Status des Löschvorgangs später anzuzeigen. |
| `orgId` | Ihre Organisations-ID. |
| `bundleId` | ID des Pakets, dem dieser Löschauftrag zugeordnet ist. Sie wird zur Fehlerbehebung verwendet. Mehrere Löschaufträge werden zu einem Paket zusammengefasst, das von nachgelagerten Services verarbeitet wird. |
| `action` | Aktion, die bei dem Arbeitsauftrag ausgeführt wird. Bei Datensatzlöschungen lautet der Wert `identity-delete`. |
| `createdAt` | Zeitstempel, der angibt, wann der Löschauftrag erstellt wurde. |
| `updatedAt` | Zeitstempel, der angibt, wann der Löschauftrag zuletzt aktualisiert wurde. |
| `status` | Der aktuelle Status des Löschauftrags. |
| `createdBy` | Der Benutzer, der den Löschauftrag erstellt hat. |
| `datasetId` | ID des Datensatzes, der Gegenstand der Anfrage ist. Wenn die Anfrage alle Datensätze betrifft, wird der Wert auf `ALL` gesetzt |
| `productStatusDetails` | Array, das den aktuellen Status der nachgelagerten Prozesse im Zusammenhang mit der Anfrage auflistet. Jedes Array-Objekt enthält die folgenden Eigenschaften:<ul><li>`productName`: Name des nachgelagerten Services.</li><li>`productStatus`: Aktueller Verarbeitungsstatus der Anfrage von dem nachgelagerten Service.</li><li>`createdAt`: Zeitstempel, der angibt, wann der letzte Status von dem Service veröffentlicht wurde.</li></ul> |

{style="table-layout:auto"}
