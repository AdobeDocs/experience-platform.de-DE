---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Dataset für Profil- und Identitätsdienst mithilfe von APIs konfigurieren
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 1%

---


# Dataset für Profil- und Identitätsdienst mithilfe von APIs konfigurieren

In diesem Lernprogramm wird beschrieben, wie Sie einen Datensatz für die Verwendung im Echtzeit-Kundendienst und -Identitätsdienst aktivieren, und zwar in den folgenden Schritten:

1. Aktivieren Sie einen Datensatz zur Verwendung im Echtzeit-Kundenkonto-Profil mit einer der beiden folgenden Optionen:
   - [Erstellen eines neuen Datensatzes](#create-a-dataset-enabled-for-profile-and-identity)
   - [Vorhandenen Datensatz konfigurieren](#configure-an-existing-dataset)
1. [Daten in den Datensatz aufnehmen](#ingest-data-into-the-dataset)
1. [Datenerfassung nach Echtzeit-Kundendaten bestätigen](#confirm-data-ingest-by-real-time-customer-profile)
1. [Datenerfassung durch Identitätsdienst bestätigen](#confirm-data-ingest-by-identity-service)

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen Adobe Experience Platformen, die mit der Verwaltung von Profil-aktivierten Datensätzen verbunden sind. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation zu diesen entsprechenden Platformen-Services:

- [Echtzeit-Profil](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Identitätsdienst](../../identity-service/home.md): Ermöglicht Kunden-Profil in Echtzeit durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in die Platform aufgenommen werden.
- [Katalogdienst](../../catalog/home.md): Eine RESTful-API, mit der Sie Datasets erstellen und für den Echtzeit-Kunden- und Identitätsdienst konfigurieren können.
- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platformen-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Werte für erforderliche Kopfzeilen sammeln

Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird. Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Erstellen eines Datensatzes, der für Profil und Identität aktiviert ist {#create-a-dataset-enabled-for-profile-and-identity}

Sie können einen Datensatz für Echtzeit-Kundendienst und -Identitätsdienst unmittelbar nach der Erstellung oder jederzeit nach Erstellung des Datensatzes aktivieren. Wenn Sie einen Datensatz aktivieren möchten, der bereits erstellt wurde, führen Sie die Schritte zum [Konfigurieren eines vorhandenen Datensatzes](#configure-an-existing-dataset) weiter unten in diesem Dokument aus. Um einen neuen Datensatz zu erstellen, müssen Sie die ID eines vorhandenen XDM-Schemas kennen, das für Echtzeit-Kundendaten-Profil aktiviert ist. Informationen zum Nachschlagen oder Erstellen eines Profil-aktivierten Schemas finden Sie im Lernprogramm zum [Erstellen eines Schemas mit der Schema-Registrierungs-API](../../xdm/tutorials/create-schema-api.md). Durch den folgenden Aufruf der Katalog-API wird ein Datensatz für den Profil- und Identitätsdienst aktiviert.

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Indem der Datensatz in den Anforderungstext aufgenommen `unifiedProfile` und `unifiedIdentity` unter `tags` diesen eingefügt wird, wird er sofort für den Profil- bzw. Identitätsdienst aktiviert. Die Werte dieser Tags müssen ein Array sein, das die Zeichenfolge enthält `"enabled:true"`.

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
| `schemaRef.id` | Die ID des Profil-aktivierten Schemas, auf dem der Datensatz basiert. |
| `{TENANT_ID}` | Der Namensraum in der Schema-Registrierung, der Ressourcen Ihrer IMS-Organisation enthält. Weitere Informationen finden Sie im Abschnitt [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) des Schema Registry-Entwicklerhandbuchs. |

**Antwort**

Eine erfolgreiche Antwort zeigt ein Array mit der ID des neu erstellten Datensatzes in Form von `"@/dataSets/{DATASET_ID}"`. Nachdem Sie einen Datensatz erfolgreich erstellt und aktiviert haben, fahren Sie mit den Schritten zum [Hochladen der Daten](#upload-data-to-the-dataset)fort.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Vorhandenen Datensatz konfigurieren {#configure-an-existing-dataset}

In den folgenden Schritten wird beschrieben, wie Sie einen zuvor erstellten Datensatz für Echtzeit-Kundendienst und -Profil aktivieren. Wenn Sie bereits einen Datensatz mit aktiviertem Profil erstellt haben, fahren Sie mit den Schritten zum [Erfassen von Daten](#ingest-data-into-the-dataset)fort.

### Überprüfen, ob der Datensatz aktiviert ist {#check-if-the-dataset-is-enabled}

Mithilfe der Katalog-API können Sie einen vorhandenen Datensatz überprüfen, um festzustellen, ob er für die Verwendung im Echtzeit-Kunden- und Identitätsdienst aktiviert ist. Der folgende Aufruf ruft die Details eines Datensatzes nach ID ab.

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

Unter der `tags` Eigenschaft können Sie sehen, dass `unifiedProfile` und `unifiedIdentity` beide vorhanden sind mit dem Wert `enabled:true`. Daher sind Kundendienst und Identitätsdienst in Echtzeit für diesen Datensatz aktiviert.

### Datensatz aktivieren {#enable-the-dataset}

Wenn der vorhandene Datensatz nicht für Profil oder Identitätsdienst aktiviert wurde, können Sie ihn aktivieren, indem Sie eine PATCH-Anforderung mit der DataSet-ID durchführen.

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

**Antwort** Eine erfolgreiche PATCH-Anforderung gibt HTTP-Status 200 (OK) und ein Array mit der ID des aktualisierten Datensatzes zurück. Diese ID sollte mit der in der PATCH-Anforderung gesendeten ID übereinstimmen. Die Tags `"unifiedProfile"` und `"unifiedIdentity"` Tags wurden jetzt hinzugefügt und der Datensatz für die Verwendung durch Profil- und Identitätsdienste aktiviert.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Daten in den Datensatz aufnehmen {#ingest-data-into-the-dataset}

Sowohl Kundendaten in Echtzeit als auch der Identitätsdienst nutzen XDM-Daten, während sie in einen Datensatz aufgenommen werden. Anweisungen zum Hochladen von Daten in einen Datensatz finden Sie im Lernprogramm zum [Erstellen eines Datensatzes mit APIs](../../catalog/datasets/create.md). Berücksichtigen Sie bei der Planung, welche Daten an Ihren Profil-aktivierten Dataset gesendet werden sollen, die folgenden Best Practices:

- Schließen Sie alle Daten ein, die Sie als Segmentkriterien für Audiencen verwenden möchten.
- Schließen Sie so viele Bezeichner ein, wie Sie aus Ihren Profil-Daten erkennen können, um Ihr Identitätsdiagramm zu maximieren. Dadurch kann der Identitätsdienst Identitäten effektiver über Datensätze hinweg verbinden.

## Datenerfassung nach Echtzeit-Kundendaten bestätigen {#confirm-data-ingest-by-real-time-customer-profile}

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einer neuen ETL oder Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie erwartungsgemäß hochgeladen wurden. Mit der Echtzeit-API für den Zugriff auf Kundendaten können Sie Stapeldaten abrufen, während sie in ein Profil geladen werden. Wenn Sie keine der erwarteten Entitäten abrufen können, ist Ihr Datensatz möglicherweise nicht für Echtzeit-Kundendaten aktiviert. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen. Detaillierte Anweisungen zur Verwendung der Echtzeit-Client-Profil-API für den Zugriff auf Profil-Daten finden Sie im [Entitäts-Endpunkthandbuch](../api/entities.md), auch bekannt als &quot;Profil Access API&quot;.

## Datenerfassung durch Identitätsdienst bestätigen {#confirm-data-ingest-by-identity-service}

Jedes ingetierte Datenfragment, das mehr als eine Identität enthält, erstellt einen Link in Ihrem privaten Identitätsdiagramm. Weitere Informationen zu Identitätsdiagrammen und zum Zugriff auf Identitätsdaten erhalten Sie zunächst in der Übersicht über den [Identitätsdienst](../../identity-service/home.md).