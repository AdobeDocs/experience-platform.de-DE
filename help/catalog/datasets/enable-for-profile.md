---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; Datensatz aktivieren
title: Datensatz für Profil- und Identitätsdienst mithilfe von APIs aktivieren
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie einen Datensatz für die Verwendung mit Echtzeit-Kundenprofil und Identity Service mithilfe von Adobe Experience Platform-APIs aktivieren.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: d463dabbb9dc099394081b803df619129c0cb416
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 20%

---

# Datensatz aktivieren für [!DNL Profile] und [!DNL Identity Service] Verwenden von APIs

In diesem Tutorial wird der Prozess zum Aktivieren eines Datensatzes zur Verwendung in [!DNL Real-time Customer Profile] und [!DNL Identity Service], unterteilt in die folgenden Schritte:

1. Datensatz zur Verwendung in aktivieren [!DNL Real-time Customer Profile], wobei eine von zwei Optionen verwendet wird:
   - [Neuen Datensatz erstellen](#create-a-dataset-enabled-for-profile-and-identity)
   - [Vorhandenen Datensatz konfigurieren](#configure-an-existing-dataset)
1. [Daten in den Datensatz aufnehmen](#ingest-data-into-the-dataset)
1. [Datenaufnahme nach Echtzeit-Kundenprofil bestätigen](#confirm-data-ingest-by-real-time-customer-profile)
1. [Datenerfassung durch Identity Service bestätigen](#confirm-data-ingest-by-identity-service)

## Erste Schritte

Dieses Tutorial setzt Grundkenntnisse verschiedener Adobe Experience Platform-Dienste voraus, die mit der Verwaltung von profilaktivierten Datensätzen verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation zu diesen verwandten Themen [!DNL Platform] Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Identity Service]](../../identity-service/home.md): Aktiviert [!DNL Real-time Customer Profile] durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die aufgenommen wird [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Eine RESTful-API, mit der Sie Datensätze erstellen und konfigurieren können für [!DNL Real-time Customer Profile] und [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Für alle Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche `Content-Type` -Kopfzeile. Der richtige Wert für diese Kopfzeile wird bei Bedarf in den Beispielanfragen angezeigt.

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle Anfragen an [!DNL Platform] APIs erfordern eine `x-sandbox-name` -Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll. Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Erstellen eines Datensatzes, der für Profil und Identität aktiviert ist {#create-a-dataset-enabled-for-profile-and-identity}

Sie können einen Datensatz für Echtzeit-Kundenprofil und Identity Service sofort nach der Erstellung oder zu einem beliebigen Zeitpunkt nach der Erstellung des Datensatzes aktivieren. Wenn Sie einen bereits erstellten Datensatz aktivieren möchten, gehen Sie wie folgt vor: [Konfigurieren eines vorhandenen Datensatzes](#configure-an-existing-dataset) finden Sie später in diesem Dokument.

>[!NOTE]
>
>Um einen neuen Datensatz mit aktiviertem Profil zu erstellen, müssen Sie die ID eines vorhandenen XDM-Schemas kennen, das für Profil aktiviert ist. Informationen zum Nachschlagen oder Erstellen eines Profilaktivierten Schemas finden Sie in der Anleitung zu [Erstellen eines Schemas mithilfe der Schema Registry-API](../../xdm/tutorials/create-schema-api.md).

Um einen Datensatz zu erstellen, der für Profile aktiviert ist, können Sie eine POST-Anfrage an die `/dataSets` -Endpunkt.

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Durch Einbeziehung von `unifiedProfile` und `unifiedIdentity` under `tags` im Anfrageinhalt wird der Datensatz sofort für [!DNL Profile] und [!DNL Identity Service]zurück. Die Werte dieser Tags müssen ein Array sein, das die Zeichenfolge enthält `"enabled:true"`.

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
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `schemaRef.id` | Die ID der [!DNL Profile]-aktiviertes Schema, auf dem der Datensatz basieren soll. |
| `{TENANT_ID}` | Der Namespace innerhalb der [!DNL Schema Registry] , die Ressourcen Ihrer IMS-Organisation enthält. Siehe [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) Abschnitt [!DNL Schema Registry] Entwicklerhandbuch für weitere Informationen. |

**Antwort**

Eine erfolgreiche Antwort zeigt ein Array mit der Kennung des neu erstellten Datensatzes in der Form von `"@/dataSets/{DATASET_ID}"`. Nachdem Sie einen Datensatz erfolgreich erstellt und aktiviert haben, fahren Sie mit den Schritten für [Hochladen von Daten](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Vorhandenen Datensatz konfigurieren {#configure-an-existing-dataset}

In den folgenden Schritten wird beschrieben, wie Sie einen zuvor erstellten Datensatz für [!DNL Real-time Customer Profile] und [!DNL Identity Service]. Wenn Sie bereits einen Datensatz mit aktiviertem Profil erstellt haben, fahren Sie mit den Schritten für [Datenerfassung](#ingest-data-into-the-dataset).

### Überprüfen, ob der Datensatz aktiviert ist {#check-if-the-dataset-is-enabled}

Verwenden der [!DNL Catalog] API können Sie einen vorhandenen Datensatz überprüfen, um festzustellen, ob er zur Verwendung in [!DNL Real-time Customer Profile] und [!DNL Identity Service]. Der folgende Aufruf ruft die Details eines Datensatzes nach Kennung ab.

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

Unter dem `tags` -Eigenschaft, sehen Sie, dass `unifiedProfile` und `unifiedIdentity` sind beide mit dem Wert vorhanden `enabled:true`. Daher [!DNL Real-time Customer Profile] und [!DNL Identity Service] für diesen Datensatz aktiviert sind.

### Datensatz aktivieren {#enable-the-dataset}

Wenn der vorhandene Datensatz nicht für [!DNL Profile] oder [!DNL Identity Service]können Sie sie aktivieren, indem Sie eine PATCH-Anfrage mit der Datensatz-ID ausführen.

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

Der Anfrageinhalt enthält eine `path` zwei Arten von Tags, `unifiedProfile` und `unifiedIdentity`. Die `value` jeweils sind Arrays, die die Zeichenfolge enthalten `enabled:true`.

**Reaktion**
Bei erfolgreicher PATCH-Anfrage werden der HTTP-Status-Code 200 (OK) und ein Array mit der Kennung des aktualisierten Datensatzes zurückgegeben. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die `unifiedProfile` und `unifiedIdentity` -Tags wurden hinzugefügt und der Datensatz ist für die Verwendung durch Profil- und Identitätsdienste aktiviert.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Daten in den Datensatz aufnehmen {#ingest-data-into-the-dataset}

Beide [!DNL Real-time Customer Profile] und [!DNL Identity Service] XDM-Daten bei der Erfassung in einen Datensatz verwenden. Anweisungen zum Hochladen von Daten in einen Datensatz finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe von APIs](../../catalog/datasets/create.md). Bei der Planung, welche Daten an Ihre [!DNL Profile]-aktivierter Datensatz. Beachten Sie die folgenden Best Practices:

- Schließen Sie alle Daten ein, die Sie als Segmentierungskriterien verwenden möchten.
- Fügen Sie so viele Identifikatoren ein, wie Sie aus Ihren Profildaten erkennen können, um Ihr Identitätsdiagramm zu maximieren. Dies ermöglicht Folgendes [!DNL Identity Service] , um Identitäten effektiver über Datensätze hinweg zuzuordnen.

## Datenaufnahme bestätigen durch [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einem neuen ETL oder einer neuen Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie erwartungsgemäß hochgeladen wurden. Verwenden der [!DNL Real-time Customer Profile] Auf API zugreifen, können Sie Batch-Daten abrufen, während sie in einen Datensatz geladen werden. Wenn Sie keine der erwarteten Entitäten abrufen können, wird Ihr Datensatz möglicherweise nicht für [!DNL Real-time Customer Profile]. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen. Detaillierte Anweisungen zur Verwendung der [!DNL Real-time Customer Profile] API für den Zugriff [!DNL Profile] Daten, siehe [Endpunktleitfaden für Entitäten](../../profile/api/entities.md), auch als bezeichnet[!DNL Profile Access]&quot;API.

## Datenerfassung durch Identity Service bestätigen {#confirm-data-ingest-by-identity-service}

Jedes erfasste Datenfragment, das mehr als eine Identität enthält, erstellt einen Link in Ihrem privaten Identitätsdiagramm. Für weitere Informationen zu Identitätsdiagrammen und zum Zugriff auf Identitätsdaten lesen Sie zunächst das [Identity Service - Übersicht](../../identity-service/home.md).
