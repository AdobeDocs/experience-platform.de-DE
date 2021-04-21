---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API;Datenbestand aktivieren
title: Dataset für Profil- und Identitätsdienst mit APIs konfigurieren
topic-legacy: tutorial
type: Tutorial
description: In diesem Lernprogramm wird gezeigt, wie Sie einen Datensatz für die Verwendung mit dem Echtzeit-Kundendienst und dem Identitätsdienst mithilfe von Adobe Experience Platform-APIs aktivieren können.
exl-id: 142cb7df-072a-4f3a-8a9c-9a78afb35312
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 19%

---

# Konfigurieren eines Datensatzes für [!DNL Profile] und [!DNL Identity Service] mithilfe von APIs

Dieses Lernprogramm beschreibt den Prozess der Aktivierung eines Datensatzes für die Verwendung in [!DNL Real-time Customer Profile] und [!DNL Identity Service] und unterteilt in die folgenden Schritte:

1. Aktivieren Sie einen Datensatz zur Verwendung in [!DNL Real-time Customer Profile], indem Sie eine der beiden Optionen verwenden:
   - [Neuen Datensatz erstellen](#create-a-dataset-enabled-for-profile-and-identity)
   - [Vorhandenen Datensatz konfigurieren](#configure-an-existing-dataset)
1. [Daten in den Datensatz aufnehmen](#ingest-data-into-the-dataset)
1. [Datenerfassung nach Echtzeit-Kundendaten bestätigen](#confirm-data-ingest-by-real-time-customer-profile)
1. [Datenerfassung durch Identitätsdienst bestätigen](#confirm-data-ingest-by-identity-service)

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die mit der Verwaltung von [!DNL Profile]-fähigen Datensätzen befasst sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation zu diesen verwandten [!DNL Platform]-Diensten:

- [[!DNL Real-time Customer Profile]](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Identity Service]](../../identity-service/home.md): Ermöglicht  [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die Daten eingehen  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Eine RESTful-API, mit der Sie Datasets erstellen und konfigurieren können, für  [!DNL Real-time Customer Profile] und  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird. Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Erstellen Sie einen Datensatz, der für [!DNL Profile] und [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity} aktiviert ist.

Sie können einen Datensatz für [!DNL Real-time Customer Profile] und [!DNL Identity Service] unmittelbar nach der Erstellung oder zu einem beliebigen Zeitpunkt nach der Erstellung des Datensatzes aktivieren. Wenn Sie einen Datensatz aktivieren möchten, der bereits erstellt wurde, führen Sie die Schritte für [Konfigurieren eines vorhandenen Datensatzes](#configure-an-existing-dataset) weiter unten in diesem Dokument aus. Um einen neuen Datensatz zu erstellen, müssen Sie die ID eines vorhandenen XDM-Schemas kennen, das für Echtzeit-Kundendaten-Profil aktiviert ist. Informationen zum Nachschlagen oder Erstellen eines Profil-aktivierten Schemas finden Sie im Lernprogramm zum Erstellen eines Schemas mit der Schema Registry API](../../xdm/tutorials/create-schema-api.md). [ Der folgende Aufruf der API [!DNL Catalog] aktiviert einen Datensatz für [!DNL Profile] und [!DNL Identity Service].

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Durch die Aufnahme von `unifiedProfile` und `unifiedIdentity` unter `tags` in den Anforderungstext wird der Datensatz sofort für [!DNL Profile] bzw. [!DNL Identity Service] aktiviert. Die Werte dieser Tags müssen ein Array sein, das die Zeichenfolge `"enabled:true"` enthält.

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
        "persisted": true
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
| `schemaRef.id` | Die ID des [!DNL Profile]-aktivierten Schemas, auf dem der Datensatz basiert. |
| `{TENANT_ID}` | Der Namensraum innerhalb von [!DNL Schema Registry], der Ressourcen enthält, die zu Ihrer IMS-Organisation gehören. Weitere Informationen finden Sie im Abschnitt [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) des [!DNL Schema Registry]-Entwicklerhandbuchs. |

**Antwort**

Eine erfolgreiche Antwort zeigt ein Array mit der ID des neu erstellten Datensatzes in Form von `"@/dataSets/{DATASET_ID}"`. Nachdem Sie einen Datensatz erfolgreich erstellt und aktiviert haben, fahren Sie mit den Schritten für [Hochladen von Daten](#upload-data-to-the-dataset) fort.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Vorhandenen Datensatz {#configure-an-existing-dataset} konfigurieren

Die folgenden Schritte beschreiben, wie Sie einen zuvor erstellten Datensatz für [!DNL Real-time Customer Profile] und [!DNL Identity Service] aktivieren. Wenn Sie bereits einen Profil-aktivierten Datensatz erstellt haben, fahren Sie mit den Schritten für [Erfassen von Daten](#ingest-data-into-the-dataset) fort.

### Überprüfen Sie, ob der Datensatz aktiviert ist. {#check-if-the-dataset-is-enabled}

Mithilfe der API [!DNL Catalog] können Sie einen vorhandenen Datensatz überprüfen, um festzustellen, ob er für die Verwendung in [!DNL Real-time Customer Profile] und [!DNL Identity Service] aktiviert ist. Der folgende Aufruf ruft die Details eines Datensatzes nach ID ab.

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
            "persisted": true
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

Unter der Eigenschaft `tags` können Sie sehen, dass `unifiedProfile` und `unifiedIdentity` beide mit dem Wert `enabled:true` vorhanden sind. Daher sind [!DNL Real-time Customer Profile] und [!DNL Identity Service] für diesen Datensatz aktiviert.

### Datensatz {#enable-the-dataset} aktivieren

Wenn der vorhandene Datensatz nicht für [!DNL Profile] oder [!DNL Identity Service] aktiviert wurde, können Sie ihn aktivieren, indem Sie eine PATCH-Anforderung mit der DataSet-ID erstellen.

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

Der Anforderungstext enthält die Eigenschaft `tags`, die zwei Untereigenschaften enthält: `"unifiedProfile"` und `"unifiedIdentity"`. Die Werte dieser Untereigenschaften sind Arrays mit der Zeichenfolge `"enabled:true"`.

**Antwort**
Eine erfolgreiche PATCH-Anforderung gibt HTTP-Status 200 (OK) und ein Array mit der ID des aktualisierten Datensatzes zurück. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die Tags `"unifiedProfile"` und `"unifiedIdentity"` wurden hinzugefügt und der Datensatz ist für die Verwendung durch Profil- und Identitätsdienste aktiviert.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Daten in Dataset {#ingest-data-into-the-dataset} aufnehmen

Sowohl [!DNL Real-time Customer Profile] als auch [!DNL Identity Service] verwenden XDM-Daten, während sie in einen Datensatz aufgenommen werden. Anweisungen zum Hochladen von Daten in einen Datensatz finden Sie im Lernprogramm [Erstellen eines Datensatzes mit APIs](../../catalog/datasets/create.md). Berücksichtigen Sie bei der Planung, welche Daten an Ihren [!DNL Profile]-aktivierten Datensatz gesendet werden sollen, die folgenden Best Practices:

- Schließen Sie alle Daten ein, die Sie als Segmentkriterien für Audiencen verwenden möchten.
- Schließen Sie so viele Bezeichner ein, wie Sie aus Ihren Profil-Daten erkennen können, um Ihr Identitätsdiagramm zu maximieren. Auf diese Weise können Identitäten zwischen Datensätzen effektiver verknüpft werden.[!DNL Identity Service]

## Datenerfassung bestätigen durch [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einer neuen ETL oder Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie erwartungsgemäß hochgeladen wurden. Mit der Zugriffs-API [!DNL Real-time Customer Profile] können Sie Stapeldaten abrufen, während sie in ein Dataset geladen werden. Wenn Sie keine der erwarteten Entitäten abrufen können, ist Ihr Datensatz möglicherweise nicht für [!DNL Real-time Customer Profile] aktiviert. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen. Ausführliche Anweisungen zum Verwenden der [!DNL Real-time Customer Profile]-API für den Zugriff auf [!DNL Profile]-Daten erhalten Sie im [Entitäts-Endpunkthandbuch](../api/entities.md), auch als &quot;[!DNL Profile Access]-API&quot;bezeichnet.

## Datenerfassung durch Identitätsdienst {#confirm-data-ingest-by-identity-service} bestätigen

Jedes ingetierte Datenfragment, das mehr als eine Identität enthält, erstellt einen Link in Ihrem privaten Identitätsdiagramm. Weitere Informationen zu Identitätsdiagrammen und zum Zugriff auf Identitätsdaten erhalten Sie zunächst im [Übersicht über den Identitätsdienst](../../identity-service/home.md).
