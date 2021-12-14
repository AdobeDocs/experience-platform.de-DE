---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; Datensatz aktivieren
title: Datensatz für Profil-Updates mithilfe von APIs aktivieren
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie mit Adobe Experience Platform-APIs einen Datensatz mit "upsert"-Funktionen aktivieren können, um Aktualisierungen an Echtzeit-Kundenprofildaten vorzunehmen.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 22%

---

# Datensatz für Profilaktualisierungen mithilfe von APIs aktivieren

In diesem Tutorial wird die Aktivierung eines Datensatzes mit &quot;upsert&quot;-Funktionen beschrieben, um Aktualisierungen an Echtzeit-Kundenprofildaten vorzunehmen. Dies umfasst die Schritte zum Erstellen eines neuen Datensatzes und zum Konfigurieren eines vorhandenen Datensatzes.

## Erste Schritte

Dieses Tutorial setzt Grundkenntnisse verschiedener Adobe Experience Platform-Dienste voraus, die mit der Verwaltung von profilaktivierten Datensätzen verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für diese zugehörigen DNL Platform-Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Catalog Service]](../../catalog/home.md): Eine RESTful-API, mit der Sie Datensätze erstellen und konfigurieren können für [!DNL Real-time Customer Profile] und [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.
- [Batch-Erfassung](../../ingestion/batch-ingestion/overview.md)

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Für alle Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche `Content-Type` -Kopfzeile. Der richtige Wert für diese Kopfzeile wird bei Bedarf in den Beispielanfragen angezeigt.

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle Anfragen an [!DNL Platform] APIs erfordern eine `x-sandbox-name` -Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll. Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Erstellen eines Datensatzes, der für Profilaktualisierungen aktiviert ist

Beim Erstellen eines neuen Datensatzes können Sie diesen Datensatz für Profil aktivieren und zum Zeitpunkt der Erstellung Aktualisierungsfunktionen aktivieren.

>[!NOTE]
>
>Um einen neuen Datensatz mit aktiviertem Profil zu erstellen, müssen Sie die ID eines vorhandenen XDM-Schemas kennen, das für Profil aktiviert ist. Informationen zum Nachschlagen oder Erstellen eines Profilaktivierten Schemas finden Sie in der Anleitung zu [Erstellen eines Schemas mithilfe der Schema Registry-API](../../xdm/tutorials/create-schema-api.md).

Um einen Datensatz zu erstellen, der für Profil und Updates aktiviert ist, verwenden Sie eine POST-Anfrage an die `/dataSets` -Endpunkt.

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Durch Einbeziehung von `unifiedProfile` under `tags` im Anfrageinhalt wird der Datensatz für [!DNL Profile] bei der Erstellung. Innerhalb der `unifiedProfile` Array hinzufügen `isUpsert:true` fügt dem Datensatz die Möglichkeit hinzu, Aktualisierungen zu unterstützen.

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
          "unifiedProfile": [
            "enabled:true",
            "isUpsert:true"
          ]
        }
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `schemaRef.id` | Die ID der [!DNL Profile]-aktiviertes Schema, auf dem der Datensatz basieren soll. |
| `{TENANT_ID}` | Der Namespace innerhalb der [!DNL Schema Registry] , die Ressourcen Ihrer IMS-Organisation enthält. Siehe [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) Abschnitt [!DNL Schema Registry] Entwicklerhandbuch für weitere Informationen. |

**Antwort**

Eine erfolgreiche Antwort zeigt ein Array mit der Kennung des neu erstellten Datensatzes in der Form von `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Vorhandenen Datensatz konfigurieren {#configure-an-existing-dataset}

Die folgenden Schritte beschreiben, wie Sie einen vorhandenen Datensatz mit aktiviertem Profil für die Aktualisierungsfunktion (&quot;upsert&quot;) konfigurieren.

>[!NOTE]
>
>Um einen vorhandenen Datensatz mit aktiviertem Profil für &quot;upsert&quot;zu konfigurieren, müssen Sie zunächst den Datensatz für Profil deaktivieren und ihn dann neben der `isUpsert` -Tag. Wenn der vorhandene Datensatz nicht für Profil aktiviert ist, können Sie direkt mit den Schritten für [Aktivieren des Datensatzes für Profil und Hochladen](#enable-the-dataset). Wenn Sie sich nicht sicher sind, zeigen Ihnen die folgenden Schritte, wie Sie überprüfen können, ob der Datensatz bereits aktiviert ist.

### Überprüfen Sie, ob der Datensatz für Profil aktiviert ist.

Verwenden der [!DNL Catalog] API können Sie einen vorhandenen Datensatz überprüfen, um festzustellen, ob er zur Verwendung in [!DNL Real-time Customer Profile]. Der folgende Aufruf ruft die Details eines Datensatzes nach Kennung ab.

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
        "name": "{DATASET_NAME}",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
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
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
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

Unter dem `tags` -Eigenschaft, sehen Sie, dass `unifiedProfile` mit dem Wert vorhanden ist `enabled:true`. Daher [!DNL Real-time Customer Profile] für diesen Datensatz aktiviert ist.

### Datensatz für Profil deaktivieren

Um einen für Profile aktivierten Datensatz für Aktualisierungen zu konfigurieren, müssen Sie zunächst die `unifiedProfile` -Tag erstellen und es dann neben dem `isUpsert` -Tag. Dies geschieht mit zwei PATCH-Anfragen, einmal zur Deaktivierung und einmal zur erneuten Aktivierung.

>[!WARNING]
>
>Daten, die während der Deaktivierung in den Datensatz aufgenommen werden, werden nicht in den Profilspeicher aufgenommen. Es wird empfohlen, die Aufnahme von Daten in den Datensatz zu vermeiden, bis er für Profil wieder aktiviert wurde.

**API-Format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DATASET_ID}` | Die ID eines Datensatzes, den Sie aktualisieren möchten. |

**Anfrage**

Der erste PATCH-Anforderungstext enthält eine `path` nach `unifiedProfile` festlegen, `value` nach `enabled:false` um das Tag zu deaktivieren.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "replace", "path": "/tags/unifiedProfile", "value": ["enabled:false"] },
      ]'
```

**Reaktion**
Bei erfolgreicher PATCH-Anfrage werden der HTTP-Status-Code 200 (OK) und ein Array mit der Kennung des aktualisierten Datensatzes zurückgegeben. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die `unifiedProfile` -Tag deaktiviert wurde.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Datensatz für Profil aktivieren und aktualisieren {#enable-the-dataset}

Ein vorhandener Datensatz kann mit einer einzigen PATCH-Anfrage für Profil- und Attributaktualisierungen aktiviert werden.

**API-Format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DATASET_ID}` | Die ID eines Datensatzes, den Sie aktualisieren möchten. |

**Anfrage**

Der Anfrageinhalt enthält eine `path` nach `unifiedProfile` festlegen, `value` , um `enabled` und `isUpsert` Tags, die beide auf `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true","isUpsert:true"] },
      ]'
```

**Reaktion**
Bei erfolgreicher PATCH-Anfrage werden der HTTP-Status-Code 200 (OK) und ein Array mit der Kennung des aktualisierten Datensatzes zurückgegeben. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die `unifiedProfile` -Tag wurde nun für Attributaktualisierungen aktiviert und konfiguriert.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Nächste Schritte

Ihr Profil und Ihr hochaktivierter Datensatz können jetzt von Batch- und Streaming-Aufnahme-Workflows verwendet werden, um Aktualisierungen an Profildaten vorzunehmen. Um mehr über die Aufnahme von Daten in Adobe Experience Platform zu erfahren, lesen Sie zunächst das [Datenerfassung - Übersicht](../../ingestion/home.md).
