---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; Datensatz aktivieren
title: Datensatz für Profil- und Identitätsdienst mithilfe von APIs konfigurieren
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie einen Datensatz für die Verwendung mit Echtzeit-Kundenprofil und Identity Service mithilfe von Adobe Experience Platform-APIs aktivieren.
exl-id: 142cb7df-072a-4f3a-8a9c-9a78afb35312
source-git-commit: 453e120fa20232533289ee5ff34821ce8c0c310b
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 20%

---

# Datensatz für [!DNL Profile] und [!DNL Identity Service] mithilfe von APIs konfigurieren

In diesem Tutorial wird der Prozess zum Aktivieren eines Datensatzes für die Verwendung in [!DNL Real-time Customer Profile] und [!DNL Identity Service] beschrieben, der in die folgenden Schritte unterteilt wird:

1. Aktivieren Sie einen Datensatz zur Verwendung in [!DNL Real-time Customer Profile] mithilfe einer von zwei Optionen:
   - [Neuen Datensatz erstellen](#create-a-dataset-enabled-for-profile-and-identity)
   - [Vorhandenen Datensatz konfigurieren](#configure-an-existing-dataset)
1. [Daten in den Datensatz aufnehmen](#ingest-data-into-the-dataset)
1. [Datenaufnahme nach Echtzeit-Kundenprofil bestätigen](#confirm-data-ingest-by-real-time-customer-profile)
1. [Datenerfassung durch Identity Service bestätigen](#confirm-data-ingest-by-identity-service)

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der verschiedenen Adobe Experience Platform-Dienste voraus, die mit der Verwaltung von [!DNL Profile]-aktivierten Datensätzen verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für diese zugehörigen [!DNL Platform]-Dienste:

- [[!DNL Real-time Customer Profile]](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Identity Service]](../../identity-service/home.md): Ermöglicht  [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die  [!DNL Platform]aufgenommen wird.
- [[!DNL Catalog Service]](../../catalog/home.md): Eine RESTful-API, mit der Sie Datensätze erstellen und für  [!DNL Real-time Customer Profile]   [!DNL Identity Service]und konfigurieren können.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Für alle Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche `Content-Type` -Kopfzeile erforderlich. Der richtige Wert für diese Kopfzeile wird bei Bedarf in den Beispielanfragen angezeigt.

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Für alle Anfragen an [!DNL Platform]-APIs ist eine `x-sandbox-name`-Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll. Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Erstellen Sie einen Datensatz, der für [!DNL Profile] und [!DNL Identity] aktiviert ist. {#create-a-dataset-enabled-for-profile-and-identity}

Sie können einen Datensatz für [!DNL Real-time Customer Profile] und [!DNL Identity Service] sofort nach der Erstellung oder zu einem beliebigen Zeitpunkt nach der Erstellung des Datensatzes aktivieren. Wenn Sie einen bereits erstellten Datensatz aktivieren möchten, führen Sie die Schritte für [Konfigurieren eines vorhandenen Datensatzes](#configure-an-existing-dataset) aus, die weiter unten in diesem Dokument zu finden sind. Um einen neuen Datensatz zu erstellen, müssen Sie die ID eines vorhandenen XDM-Schemas kennen, das für das Echtzeit-Kundenprofil aktiviert ist. Informationen zum Nachschlagen oder Erstellen eines Profilaktivierten Schemas finden Sie im Tutorial zum Erstellen eines Schemas mit der Schema Registry-API](../../xdm/tutorials/create-schema-api.md). [ Der folgende Aufruf der API [!DNL Catalog] aktiviert einen Datensatz für [!DNL Profile] und [!DNL Identity Service].

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Durch die Einbeziehung von `unifiedProfile` und `unifiedIdentity` unter `tags` in den Anfrageinhalt wird der Datensatz sofort für [!DNL Profile] bzw. [!DNL Identity Service] aktiviert. Die Werte dieser Tags müssen ein Array sein, das die Zeichenfolge `"enabled:true"` enthält.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
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
| `schemaRef.id` | Die ID des [!DNL Profile]-aktivierten Schemas, auf dem der Datensatz basieren soll. |
| `{TENANT_ID}` | Der Namespace innerhalb von [!DNL Schema Registry] , der Ressourcen enthält, die zu Ihrer IMS-Organisation gehören. Weitere Informationen finden Sie im Abschnitt [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) des [!DNL Schema Registry]-Entwicklerhandbuchs. |

**Antwort**

Eine erfolgreiche Antwort zeigt ein Array mit der Kennung des neu erstellten Datensatzes in der Form `"@/dataSets/{DATASET_ID}"` an. Nachdem Sie einen Datensatz erfolgreich erstellt und aktiviert haben, fahren Sie mit den Schritten für [Hochladen von Daten](#upload-data-to-the-dataset) fort.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Vorhandenen Datensatz konfigurieren {#configure-an-existing-dataset}

Die folgenden Schritte beschreiben, wie Sie einen zuvor erstellten Datensatz für [!DNL Real-time Customer Profile] und [!DNL Identity Service] aktivieren. Wenn Sie bereits einen Datensatz mit aktiviertem Profil erstellt haben, fahren Sie mit den Schritten für [Erfassen von Daten](#ingest-data-into-the-dataset) fort.

### Überprüfen, ob der Datensatz aktiviert ist {#check-if-the-dataset-is-enabled}

Mithilfe der [!DNL Catalog]-API können Sie einen vorhandenen Datensatz überprüfen, um festzustellen, ob er für die Verwendung in [!DNL Real-time Customer Profile] und [!DNL Identity Service] aktiviert ist. Der folgende Aufruf ruft die Details eines Datensatzes nach Kennung ab.

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

### Datensatz aktivieren {#enable-the-dataset}

Wenn der vorhandene Datensatz für [!DNL Profile] oder [!DNL Identity Service] nicht aktiviert wurde, können Sie ihn aktivieren, indem Sie eine PATCH-Anfrage mit der Datensatz-ID ausführen.

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
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] }	
      ]'
```

Der Anfrageinhalt enthält `path` bis zu zwei Arten von Tags, `unifiedProfile` und `unifiedIdentity`. Die `value` von jedem sind Arrays, die die Zeichenfolge `enabled:true` enthalten.

****
AntwortEine erfolgreiche PATCH-Anfrage gibt den HTTP-Status 200 (OK) und ein Array mit der ID des aktualisierten Datensatzes zurück. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die Tags `unifiedProfile` und `unifiedIdentity` wurden hinzugefügt und der Datensatz ist für die Verwendung durch Profil- und Identitätsdienste aktiviert.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Daten in den Datensatz aufnehmen {#ingest-data-into-the-dataset}

Sowohl [!DNL Real-time Customer Profile] als auch [!DNL Identity Service] verwenden XDM-Daten, während sie in einen Datensatz aufgenommen werden. Anweisungen zum Hochladen von Daten in einen Datensatz finden Sie im Tutorial zum Erstellen eines Datensatzes mithilfe von APIs](../../catalog/datasets/create.md). [ Beachten Sie bei der Planung der an Ihren [!DNL Profile]-aktivierten Datensatz zu sendenden Daten die folgenden Best Practices:

- Schließen Sie alle Daten ein, die Sie als Zielgruppensegmentkriterien verwenden möchten.
- Fügen Sie so viele Identifikatoren ein, wie Sie aus Ihren Profildaten erkennen können, um Ihr Identitätsdiagramm zu maximieren. Dadurch kann [!DNL Identity Service] Identitäten besser über Datensätze hinweg zuordnen.

## Datenerfassung bestätigen mit [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einem neuen ETL oder einer neuen Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie erwartungsgemäß hochgeladen wurden. Mit der Zugriffs-API [!DNL Real-time Customer Profile] können Sie Batch-Daten abrufen, während sie in einen Datensatz geladen werden. Wenn Sie keine der erwarteten Entitäten abrufen können, ist Ihr Datensatz möglicherweise nicht für [!DNL Real-time Customer Profile] aktiviert. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen. Ausführliche Anweisungen zur Verwendung der [!DNL Real-time Customer Profile]-API für den Zugriff auf [!DNL Profile]-Daten finden Sie im [Entitäts-Endpunkthandbuch](../api/entities.md), auch als &quot;[!DNL Profile Access]-API&quot;bezeichnet.

## Datenerfassung durch Identity Service bestätigen {#confirm-data-ingest-by-identity-service}

Jedes erfasste Datenfragment, das mehr als eine Identität enthält, erstellt einen Link in Ihrem privaten Identitätsdiagramm. Weitere Informationen zu Identitätsdiagrammen und zum Zugriff auf Identitätsdaten finden Sie in der [Übersicht über den Identitätsdienst](../../identity-service/home.md).
