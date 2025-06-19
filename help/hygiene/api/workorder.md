---
title: Löschanfragen für Datensätze (Arbeitsauftrags-Endpunkt)
description: Mit dem Endpunkt /workorder in der Data Hygiene API können Sie Löschaufgaben für Identitäten programmgesteuert verwalten.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: d569b1d04fa76e0a0e48364a586e8a1a773b9bf2
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 48%

---

# Löschanfragen für Datensätze (Arbeitsauftrags-Endpunkt) {#work-order-endpoint}

Mit dem `/workorder`-Endpunkt in der Data Hygiene API können Sie Anfragen zum Löschen von Datensätzen in Adobe Experience Platform programmgesteuert verwalten.

>[!IMPORTANT]
> 
>Löschvorgänge von Datensätzen dienen zur Datenbereinigung, zum Entfernen anonymer Daten oder zur Datenminimierung. Sie dürfen **nicht** für Anfragen zu den Rechten der betroffenen Personen (Compliance) verwendet werden, da sie sich auf Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) beziehen. Verwenden Sie stattdessen [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) für alle Compliance-Anwendungsfälle.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie die [Übersicht](./overview.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Kontingente und Verarbeitungszeitpläne {#quotas}

Anfragen zum Löschen von Datensätzen unterliegen täglichen und monatlichen Obergrenzen für die Übermittlung von Identifikatoren, die durch die Lizenzberechtigung Ihres Unternehmens bestimmt werden. Diese Einschränkungen gelten sowohl für benutzeroberflächen- als auch für API-basierte Löschanfragen.

>[!NOTE]
>
>Sie können bis zu **1.000.000 Kennungen pro Tag**, jedoch nur, wenn Ihr restliches monatliches Kontingent dies zulässt. Wenn Ihre monatliche Obergrenze weniger als 1 Million beträgt, können Ihre täglichen Einreichungen diese Obergrenze nicht überschreiten.

### Berechtigung zur monatlichen Übermittlung nach Produkt {#quota-limits}

In der folgenden Tabelle sind die Beschränkungen für die Übermittlung von Kennungen nach Produkt und Berechtigungsebene aufgeführt. Für jedes Produkt ist die monatliche Obergrenze der niedrigere von zwei Werten: eine feste Kennungsobergrenze oder ein prozentualer Schwellenwert, der an Ihr lizenziertes Datenvolumen gebunden ist.

| Produkt | Beschreibung der Berechtigung | Monatliche Obergrenze (je nachdem, welcher Wert niedriger ist) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP oder Adobe Journey Optimizer | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 5 % der adressierbaren Zielgruppe |
| Real-Time CDP oder Adobe Journey Optimizer | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 10 % der adressierbaren Zielgruppe |
| Customer Journey Analytics | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 100 Kennungen pro Million CJA-Berechtigungszeilen |
| Customer Journey Analytics | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 200 Kennungen pro Million CJA-Berechtigungszeilen |

>[!NOTE]
>
> Die meisten Unternehmen verfügen über niedrigere monatliche Limits, die auf ihren tatsächlichen adressierbaren Zielgruppen- oder CJA-Zeilenberechtigungen basieren.

Die Kontingente werden am ersten Tag jedes Kalendermonats zurückgesetzt. Nicht verwendetes Kontingent wird **nicht** übertragen.

>[!NOTE]
>
>Kontingente basieren auf der lizenzierten monatlichen Berechtigung Ihres Unternehmens für **übermittelte Kennungen**. Diese werden von den Systemschutzmechanismen nicht durchgesetzt, können jedoch überwacht und überprüft werden.
>
>Löschen eines Datensatzes ist ein **freigegebener Dienst**. Die monatliche Obergrenze spiegelt die höchsten Berechtigungen für Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics und alle anwendbaren Shield-Add-ons wider.

### Zeitleisten für die Übermittlung von Identifikatoren {#sla-processing-timelines}

Nach der Übermittlung werden Anfragen zum Löschen von Datensätzen basierend auf Ihrer Berechtigungsstufe in die Warteschlange gestellt und verarbeitet.

| Produkt- und Berechtigungsbeschreibung | Warteschlangendauer | Maximale Verarbeitungszeit (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | Bis zu 15 Tage | 30 Tage |
| Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | In der Regel 24 Stunden | 15 Tage |

Wenn für Ihr Unternehmen höhere Limits erforderlich sind, wenden Sie sich zur Überprüfung der Berechtigungen an den Adobe-Support.

>[!TIP]
>
>Informationen zur aktuellen Kontingentnutzung oder Berechtigungsstufe finden Sie im [Kontingentreferenzhandbuch](../api/quota.md).

## Erstellen einer Anfrage zum Löschen eines Datensatzes {#create}

Sie können eine oder mehrere Identitäten aus einem einzelnen Datensatz oder allen Datensätzen löschen, indem Sie eine POST-Anfrage an den `/workorder`-Endpunkt senden.

>[!TIP]
>
>Jede über die API gesendete Anfrage zum Löschen von Datensätzen kann bis zu **100.000 Identitäten**. Um die Effizienz zu maximieren, sollten Sie so viele Identitäten wie möglich pro Anfrage einreichen und volumenarme Übermittlungen wie Arbeitsaufträge mit einer einzelnen ID vermeiden.

**API-Format**

```http
POST /workorder
```

>[!NOTE]
>
>Datenlebenszyklusanfragen können nur Datensätze ändern, die auf primären Identitäten oder einer Identitätszuordnung basieren. Eine Anfrage muss entweder die primäre Identität angeben oder eine Identitätszuordnung bereitstellen.

**Anfrage**

Abhängig vom Wert der `datasetId` in der Anfrage-Payload löscht der API-Aufruf Identitäten aus allen Datensätzen oder einem einzelnen von Ihnen angegebenen Datensatz. Die folgende Anfrage löscht drei Identitäten aus einem bestimmten Datensatz.

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
| `action` | Die auszuführende Aktion. Für das Löschen von Datensätzen muss der Wert auf `delete_identity` festgelegt werden. |
| `datasetId` | Wenn Sie Identitäten aus einem einzelnen Datensatz löschen, muss dieser Wert die Kennung des betreffenden Datensatzes sein. Wenn Sie Identitäten aus allen Datensätzen löschen, setzen Sie den Wert auf `ALL`.<br><br>Wenn Sie einen einzelnen Datensatz angeben, muss für das zugeordnete Experience-Datenmodell-Schema (XDM) des Datensatzes eine primäre Identität definiert sein. Wenn der Datensatz keine primäre Identität hat, muss er über eine Identitätszuordnung verfügen, damit er durch eine Data-Lifecycle-Anfrage geändert werden kann.<br>Wenn eine Identitätszuordnung vorhanden ist, ist sie als Feld der obersten Ebene mit dem Namen `identityMap` vorhanden.<br>Beachten Sie, dass eine Datensatzzeile viele Identitäten in ihrer Identitätszuordnung haben kann, aber nur eine als primär markiert werden kann. `"primary": true` müssen eingeschlossen werden, damit der `id` mit einer primären Identität übereinstimmt. |
| `displayName` | Der Anzeigename für die Löschanfrage des Datensatzes. |
| `description` | Eine Beschreibung für den Antrag auf Löschung eines Datensatzes. |
| `identities` | Ein Array mit den Identitäten von mindestens einem Benutzer, dessen Informationen Sie löschen möchten. Jede Identität besteht aus einem [Identity-Namespace](../../identity-service/features/namespaces.md) und einem Wert:<ul><li>`namespace`: enthält die einzige Zeichenfolgen-Eigenschaft `code`, die den Identity-Namespace darstellt. </li><li>`id`: der Identitätswert.</ul>Wenn `datasetId` einen einzelnen Datensatz spezifiziert, muss jede Entität unter `identities` denselben Identity-Namespace wie die primäre Identität des Schemas verwenden.<br><br>Wenn `datasetId` auf `ALL` festgelegt ist, ist das `identities`-Array nicht auf einen einzigen Namespace beschränkt, da jeder Datensatz anders sein kann. Ihre Anfragen sind aber auf die Namespaces beschränkt, die Ihrer Organisation zur Verfügung stehen, wie von [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces) spezifiziert. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Datensatzlöschvorgangs zurück.

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
| `action` | Aktion, die bei dem Arbeitsauftrag ausgeführt wird. Beim Löschen von Datensätzen ist der Wert `identity-delete`. |
| `createdAt` | Zeitstempel, der angibt, wann der Löschauftrag erstellt wurde. |
| `updatedAt` | Zeitstempel, der angibt, wann der Löschauftrag zuletzt aktualisiert wurde. |
| `status` | Der aktuelle Status des Löschauftrags. |
| `createdBy` | Der Benutzer, der den Löschauftrag erstellt hat. |
| `datasetId` | ID des Datensatzes, der Gegenstand der Anfrage ist. Wenn die Anfrage alle Datensätze betrifft, wird der Wert auf `ALL` gesetzt |

{style="table-layout:auto"}

## Abrufen des Status einer Datensatzlöschung {#lookup}

Nachdem Sie [eine Anfrage zum Löschen eines Datensatzes erstellt](#create) können Sie den Status mit einer GET-Anfrage überprüfen.

**API-Format**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{WORK_ORDER_ID}` | Die `workorderId` des Datensatzlöschens, nach dem Sie suchen. |

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
| `action` | Aktion, die bei dem Arbeitsauftrag ausgeführt wird. Beim Löschen von Datensätzen ist der Wert `identity-delete`. |
| `createdAt` | Zeitstempel, der angibt, wann der Löschauftrag erstellt wurde. |
| `updatedAt` | Zeitstempel, der angibt, wann der Löschauftrag zuletzt aktualisiert wurde. |
| `status` | Der aktuelle Status des Löschauftrags. |
| `createdBy` | Der Benutzer, der den Löschauftrag erstellt hat. |
| `datasetId` | ID des Datensatzes, der Gegenstand der Anfrage ist. Wenn die Anfrage alle Datensätze betrifft, wird der Wert auf `ALL` gesetzt |
| `productStatusDetails` | Array, das den aktuellen Status der nachgelagerten Prozesse im Zusammenhang mit der Anfrage auflistet. Jedes Array-Objekt enthält die folgenden Eigenschaften:<ul><li>`productName`: Name des nachgelagerten Services.</li><li>`productStatus`: Aktueller Verarbeitungsstatus der Anfrage von dem nachgelagerten Service.</li><li>`createdAt`: Zeitstempel, der angibt, wann der letzte Status von dem Service veröffentlicht wurde.</li></ul> |

## Aktualisieren einer Löschanfrage für einen Datensatz

Sie können die `displayName` und `description` für eine Datensatzlöschung aktualisieren, indem Sie eine PUT-Anfrage stellen.

**API-Format**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{WORK_ORDER_ID}` | Die `workorderId` des Datensatzlöschens, nach dem Sie suchen. |

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
| `displayName` | Ein aktualisierter Anzeigename für die Löschanfrage des Datensatzes. |
| `description` | Eine aktualisierte Beschreibung für die Löschanfrage des Datensatzes. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Datensatzlöschvorgangs zurück.

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
    "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die ID des Löschauftrags. Diese kann verwendet werden, um den Status des Löschvorgangs später anzuzeigen. |
| `orgId` | Ihre Organisations-ID. |
| `bundleId` | ID des Pakets, dem dieser Löschauftrag zugeordnet ist. Sie wird zur Fehlerbehebung verwendet. Mehrere Löschaufträge werden zu einem Paket zusammengefasst, das von nachgelagerten Services verarbeitet wird. |
| `action` | Aktion, die bei dem Arbeitsauftrag ausgeführt wird. Beim Löschen von Datensätzen ist der Wert `identity-delete`. |
| `createdAt` | Zeitstempel, der angibt, wann der Löschauftrag erstellt wurde. |
| `updatedAt` | Zeitstempel, der angibt, wann der Löschauftrag zuletzt aktualisiert wurde. |
| `status` | Der aktuelle Status des Löschauftrags. |
| `createdBy` | Der Benutzer, der den Löschauftrag erstellt hat. |
| `datasetId` | ID des Datensatzes, der Gegenstand der Anfrage ist. Wenn die Anfrage alle Datensätze betrifft, wird der Wert auf `ALL` gesetzt |
| `productStatusDetails` | Array, das den aktuellen Status der nachgelagerten Prozesse im Zusammenhang mit der Anfrage auflistet. Jedes Array-Objekt enthält die folgenden Eigenschaften:<ul><li>`productName`: Name des nachgelagerten Services.</li><li>`productStatus`: Aktueller Verarbeitungsstatus der Anfrage von dem nachgelagerten Service.</li><li>`createdAt`: Zeitstempel, der angibt, wann der letzte Status von dem Service veröffentlicht wurde.</li></ul> |

{style="table-layout:auto"}
