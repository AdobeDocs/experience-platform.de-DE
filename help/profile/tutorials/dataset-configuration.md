---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Dataset für Profil- und Identitätsdienst mithilfe von APIs konfigurieren
topic: tutorial
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 15%

---


# DataSet für [!DNL Profile] und [!DNL Identity Service] mit APIs konfigurieren

In diesem Lernprogramm wird der Prozess der Aktivierung eines Datensatzes zur Verwendung in [!DNL Real-time Customer Profile] und [!DNL Identity Service]unterteilt in die folgenden Schritte beschrieben:

1. Aktivieren Sie einen Datensatz zur Verwendung in [!DNL Real-time Customer Profile]einer der beiden Optionen:
   - [Neuen Datensatz erstellen](#create-a-dataset-enabled-for-profile-and-identity)
   - [Vorhandenen Datensatz konfigurieren](#configure-an-existing-dataset)
1. [Daten in den Datensatz aufnehmen](#ingest-data-into-the-dataset)
1. [Datenerfassung nach Echtzeit-Kundendaten bestätigen](#confirm-data-ingest-by-real-time-customer-profile)
1. [Datenerfassung durch Identitätsdienst bestätigen](#confirm-data-ingest-by-identity-service)

## Erste Schritte

This tutorial requires a working understanding of the various Adobe Experience Platform services involved in managing [!DNL Profile]-enabled datasets. Before beginning this tutorial, please review the documentation for these related [!DNL Platform] services:

- [!DNL Real-time Customer Profile](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [!DNL Identity Service](../../identity-service/home.md): Ermöglicht [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die Daten eingehen [!DNL Platform].
- [!DNL Catalog Service](../../catalog/home.md): Eine RESTful-API, mit der Sie Datasets erstellen und konfigurieren können, für [!DNL Real-time Customer Profile] und [!DNL Identity Service].
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platform-APIs erfolgreich aufrufen zu können.

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Für alle Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in. For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Erstellen Sie einen Datensatz, der für [!DNL Profile] und [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

Sie können einen Datensatz für [!DNL Real-time Customer Profile] und [!DNL Identity Service] sofort nach der Erstellung oder jederzeit nach Erstellung des Datensatzes aktivieren. Wenn Sie einen Datensatz aktivieren möchten, der bereits erstellt wurde, führen Sie die Schritte zum [Konfigurieren eines vorhandenen Datensatzes](#configure-an-existing-dataset) weiter unten in diesem Dokument aus. Um einen neuen Datensatz zu erstellen, müssen Sie die ID eines vorhandenen XDM-Schemas kennen, das für Echtzeit-Kundendaten-Profil aktiviert ist. Informationen zum Nachschlagen oder Erstellen eines Profil-aktivierten Schemas finden Sie im Lernprogramm zum [Erstellen eines Schemas mit der Schema-Registrierungs-API](../../xdm/tutorials/create-schema-api.md). Der folgende Aufruf der [!DNL Catalog] API aktiviert einen Datensatz für [!DNL Profile] und [!DNL Identity Service].

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Durch Aufnahme `unifiedProfile` und `unifiedIdentity` unter `tags` in den Anforderungstext wird der Datensatz sofort für [!DNL Profile] bzw. [!DNL Identity Service]aktiviert. Die Werte dieser Tags müssen ein Array sein, das die Zeichenfolge enthält `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fileDescription" : {
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "fields":[],
    "schemaRef" : {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags" : {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `schemaRef.id` | Die ID des [!DNL Profile]aktivierten Schemas, auf dem der Datensatz basiert. |
| `{TENANT_ID}` | Der Namensraum innerhalb der [!DNL Schema Registry] , der Ressourcen Ihrer IMS-Organisation enthält. Weitere Informationen finden Sie im Abschnitt [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) des [!DNL Schema Registry] Entwicklerhandbuchs. |

**Antwort**

Eine erfolgreiche Antwort zeigt ein Array mit der ID des neu erstellten Datensatzes in Form von `"@/dataSets/{DATASET_ID}"`. Nachdem Sie einen Datensatz erfolgreich erstellt und aktiviert haben, fahren Sie mit den Schritten zum [Hochladen der Daten](#upload-data-to-the-dataset)fort.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Vorhandenen Datensatz konfigurieren {#configure-an-existing-dataset}

In den folgenden Schritten wird beschrieben, wie Sie einen zuvor erstellten Datensatz für [!DNL Real-time Customer Profile] und aktivieren [!DNL Identity Service]. Wenn Sie bereits einen Datensatz mit aktiviertem Profil erstellt haben, fahren Sie mit den Schritten zum [Erfassen von Daten](#ingest-data-into-the-dataset)fort.

### Überprüfen, ob der Datensatz aktiviert ist {#check-if-the-dataset-is-enabled}

Mithilfe der [!DNL Catalog] API können Sie einen vorhandenen Datensatz überprüfen, um festzustellen, ob er für die Verwendung in und [!DNL Real-time Customer Profile] [!DNL Identity Service]die Verwendung aktiviert ist. Der folgende Aufruf ruft die Details eines Datensatzes nach ID ab.

**API-Format**

```http
GET /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DATASET_ID}` | Die ID eines Datensatzes, den Sie überprüfen möchten. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Unter der `tags` Eigenschaft können Sie sehen, dass `unifiedProfile` und `unifiedIdentity` beide vorhanden sind mit dem Wert `enabled:true`. Daher sind [!DNL Real-time Customer Profile] und [!DNL Identity Service] sind für diesen Datensatz aktiviert.

### Datensatz aktivieren {#enable-the-dataset}

Wenn der vorhandene Datensatz nicht aktiviert wurde [!DNL Profile] oder [!DNL Identity Service], können Sie ihn aktivieren, indem Sie eine PATCH-Anforderung mit der DataSet-ID durchführen.

**API-Format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DATASET_ID}` | Die ID eines Datensatzes, den Sie aktualisieren möchten. |

**Anfrage**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

Der Anforderungstext enthält eine `tags` Eigenschaft, die zwei Untereigenschaften enthält: `"unifiedProfile"` und `"unifiedIdentity"`. Die Werte dieser Untereigenschaften sind Arrays mit der Zeichenfolge `"enabled:true"`.

**Antwort** Eine erfolgreiche PATCH-Anforderung gibt HTTP-Status 200 (OK) und ein Array mit der ID des aktualisierten Datensatzes zurück. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die Tags `"unifiedProfile"` und `"unifiedIdentity"` Tags wurden jetzt hinzugefügt und der Datensatz für die Verwendung durch Profil- und Identitätsdienste aktiviert.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Daten in den Datensatz aufnehmen {#ingest-data-into-the-dataset}

Sowohl [!DNL Real-time Customer Profile] als auch [!DNL Identity Service] verwenden XDM-Daten, während sie in einen Datensatz aufgenommen werden. Anweisungen zum Hochladen von Daten in einen Datensatz finden Sie im Lernprogramm zum [Erstellen eines Datensatzes mit APIs](../../catalog/datasets/create.md). Berücksichtigen Sie bei der Planung, welche Daten an Ihren [!DNL Profile]aktivierten Datensatz gesendet werden sollen, die folgenden Best Practices:

- Schließen Sie alle Daten ein, die Sie als Segmentkriterien für Audiencen verwenden möchten.
- Schließen Sie so viele Bezeichner ein, wie Sie aus Ihren Profil-Daten erkennen können, um Ihr Identitätsdiagramm zu maximieren. Dadurch können Identitäten effektiver über Datensätze hinweg [!DNL Identity Service] zusammengeführt werden.

## Datenerfassung bestätigen durch [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einer neuen ETL oder Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie erwartungsgemäß hochgeladen wurden. Using the [!DNL Real-time Customer Profile] Access API, you can retrieve batch data as it gets loaded into a dataset. If you are unable to retrieve any of the entities you expect, your dataset may not be enabled for [!DNL Real-time Customer Profile]. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen. Ausführliche Anweisungen zum Verwenden der [!DNL Real-time Customer Profile] API für den Zugriff auf [!DNL Profile] Daten finden Sie im [Entitäts-Endpunkthandbuch](../api/entities.md), auch bekannt als &quot;[!DNL Profile Access] API&quot;.

## Datenerfassung durch Identitätsdienst bestätigen {#confirm-data-ingest-by-identity-service}

Jedes ingetierte Datenfragment, das mehr als eine Identität enthält, erstellt einen Link in Ihrem privaten Identitätsdiagramm. Weitere Informationen zu Identitätsdiagrammen und zum Zugriff auf Identitätsdaten erhalten Sie zunächst in der Übersicht über den [Identitätsdienst](../../identity-service/home.md).