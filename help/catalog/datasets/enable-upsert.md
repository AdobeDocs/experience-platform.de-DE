---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Datensatz aktivieren
title: Aktivieren eines Datensatzes für Profilaktualisierungen mithilfe von APIs
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie mit Adobe Experience Platform-APIs einen Datensatz mit "upsert"-Funktionen aktivieren können, um Aktualisierungen an den Echtzeit-Kundenprofildaten vorzunehmen.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 87%

---

# Aktivieren eines Datensatzes für Profilaktualisierungen mithilfe von APIs

In diesem Tutorial wird die Aktivierung eines Datensatzes mit &quot;upsert&quot;-Funktionen beschrieben, um Aktualisierungen an den Echtzeit-Kundenprofildaten vorzunehmen. Dazu gehören die Schritte zum Erstellen eines neuen Datensatzes und zum Konfigurieren eines vorhandenen Datensatzes.

>[!NOTE]
>
>Der in diesem Tutorial beschriebene Workflow funktioniert nur bei der Batch-Erfassung. Informationen zur Aktualisierung der Streaming-Erfassung finden Sie im Handbuch zu [Senden partieller Zeilenaktualisierungen an das Echtzeit-Kundenprofil mithilfe der Datenvorbereitung](../../data-prep/upserts.md).

## Erste Schritte

Dieses Tutorial setzt Grundkenntnisse verschiedener Adobe Experience Platform-Services voraus, die mit der Verwaltung von profilaktivierten Datensätzen verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden [!DNL Platform]-Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Catalog Service]](../../catalog/home.md): Eine RESTful-API, mit der Sie Datensätze erstellen und für [!DNL Real-Time Customer Profile] und [!DNL Identity Service] konfigurieren können.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.
- [Batch-Aufnahme](../../ingestion/batch-ingestion/overview.md): Mit der Batch-Aufnahme-API können Sie Daten als Batch-Dateien in Experience Platform aufnehmen.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um Aufrufe an [!DNL Platform] APIs verwenden, müssen Sie zunächst die [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de). Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufe, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche `Content-Type`-Kopfzeile erforderlich. Der richtige Wert für diese Kopfzeile wird bei Bedarf in den Beispielanfragen angezeigt.

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine `x-sandbox-name`-Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll. Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Erstellen eines Datensatzes, der für Profilaktualisierungen aktiviert ist

Beim Erstellen eines neuen Datensatzes können Sie diesen Datensatz für das Profil aktivieren und zum Zeitpunkt der Erstellung Aktualisierungsfunktionen aktivieren.

>[!NOTE]
>
>Um einen neuen profilaktivierten Datensatz zu erstellen, müssen Sie die ID eines vorhandenen XDM-Schemas kennen, das für Profil aktiviert ist. Informationen zum Nachschlagen oder Erstellen eines profilaktivierten Schemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der Schemaregistrierungs-API](../../xdm/tutorials/create-schema-api.md).

Um einen Datensatz zu erstellen, der für Profil und Aktualisierungen aktiviert ist, verwenden Sie eine POST-Anfrage an den `/dataSets`-Endpunkt.

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Indem Sie `unifiedIdentity` und `unifiedProfile` unter `tags` im Anfrageinhalt aufnehmen, wird der Datensatz bei der Erstellung für [!DNL Profile] aktiviert. Innerhalb des `unifiedProfile`-Arrays wird durch Hinzufügen von `isUpsert:true` zum Datensatz die Möglichkeit hinzugefügt, Aktualisierungen zu unterstützen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schemaRef.id` | Die ID des [!DNL Profile]-aktivierten Schemas, auf dem der Datensatz basieren soll. |
| `{TENANT_ID}` | Der Namespace innerhalb der [!DNL Schema Registry], der Ressourcen enthält, die zu Ihrer Organisation gehören. Weitere Informationen finden Sie im Abschnitt [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) des [!DNL Schema Registry]-Entwicklerhandbuchs. |

**Antwort**

Eine erfolgreiche Antwort zeigt ein Array mit der ID des neu erstellten Datensatzes in der Form `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Konfigurieren eines vorhandenen Datensatzes {#configure-an-existing-dataset}

Die folgenden Schritte beschreiben, wie Sie einen vorhandenen, für Profil aktivierten Datensatz für die Aktualisierung (upsert) konfigurieren.

>[!NOTE]
>
>Um einen vorhandenen profilaktivierten Datensatz für upsert zu konfigurieren, müssen Sie zunächst den Datensatz für Profil deaktivieren und ihn dann zusammen mit dem Tag `isUpsert` wieder aktivieren. Wenn der vorhandene Datensatz nicht für Profil aktiviert ist, können Sie direkt mit den Schritten für das [Aktivieren des Datensatzes für Profil und upsert](#enable-the-dataset) fortfahren. Wenn Sie sich nicht sicher sind, zeigen Ihnen die folgenden Schritte, wie Sie überprüfen können, ob der Datensatz bereits aktiviert ist.

### Überprüfen, ob der Datensatz für Profil aktiviert ist

Mithilfe der [!DNL Catalog]-API können Sie einen vorhandenen Datensatz untersuchen, um festzustellen, ob er für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert ist. Der folgende Aufruf ruft die Details eines Datensatzes nach ID ab.

**API-Format**

```http
GET /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATASET_ID}` | Die ID des Datensatzes, den Sie untersuchen möchten. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Unter der `tags`-Eigenschaft ist zu sehen, dass `unifiedProfile` mit dem Wert `enabled:true` vorliegt. Daher ist [!DNL Real-Time Customer Profile] für diesen Datensatz aktiviert.

### Deaktivieren des Datensatzes für Profil

Um einen Profil-aktivierten Datensatz für Aktualisierungen zu konfigurieren, müssen Sie zunächst die Tags `unifiedProfile` und `unifiedIdentity` deaktivieren und sie dann zusammen mit dem Tag `isUpsert` erneut aktivieren. Dies erfolgt über zwei PATCH-Anfragen: die eine zur Deaktivierung und die andere zur erneuten Aktivierung.

>[!WARNING]
>
>Daten, die während der Deaktivierung in den Datensatz aufgenommen werden, werden nicht in den Profilspeicher aufgenommen. Sie sollten die Aufnahme von Daten in den Datensatz vermeiden, bis er erneut für Profil aktiviert wurde.

**API-Format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATASET_ID}` | Die ID des Datensatzes, den Sie aktualisieren möchten. |

**Anfrage**

Der erste PATCH-Anfragetext enthält einen `path`-Verweis zu `unifiedProfile` und einen `path`-Verweis zu `unifiedIdentity`. Wird `value` für beide Pfade auf `enabled:false` festgelegt, werden die Tags deaktiviert.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**Antwort**

Bei einer erfolgreichen PATCH-Anfrage wird der HTTP-Status 200 (OK) sowie ein Array mit der ID des gelöschten Datensatzes zurückgegeben. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die Tags `unifiedProfile` und `unifiedIdentity` sind nun deaktiviert.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Aktivieren des Datensatzes für Profil und upsert {#enable-the-dataset}

Ein vorhandener Datensatz kann mit einer einzigen PATCH-Anfrage für Profil- und Attributaktualisierungen aktiviert werden.

>[!IMPORTANT]
>
>Stellen Sie beim Aktivieren Ihres Datensatzes für Profil sicher, dass das Schema, mit dem der Datensatz verknüpft ist, **ebenfalls** Profil-aktiviert ist. Wenn das Schema nicht Profil-aktiviert ist, wird der Datensatz in der Platform-Benutzeroberfläche **nicht** als Profil-aktiviert angezeigt.

**API-Format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATASET_ID}` | Die ID eines Datensatzes, den Sie aktualisieren möchten. |

**Anfrage**

Der Anfragetext enthält einen `path`-Verweis zu `unifiedProfile`. `value` umfasst dabei die Tags `enabled` und `isUpsert`, die beide auf `true` eingestellt sind. Der Anfragetext enthält auch einen `path`-Verweis zu `unifiedIdentity`, wobei `value` das Tag `enabled` mit der Einstellung `true` umfasst.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**Antwort**

Bei einer erfolgreichen PATCH-Anfrage wird der HTTP-Status 200 (OK) sowie ein Array mit der ID des gelöschten Datensatzes zurückgegeben. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die Tags `unifiedProfile` und `unifiedIdentity` sind nun für Attributaktualisierungen aktiviert und konfiguriert.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Nächste Schritte

Ihr Profil- und upsert-aktivierter Datensatz kann nun von Batch-Aufnahme-Workflows verwendet werden, um Aktualisierungen an Profildaten vorzunehmen. Um mehr über die Aufnahme von Daten in Adobe Experience Platform zu erfahren, lesen Sie bitte zunächst die [Übersicht zur Datenaufnahme](../../ingestion/home.md).
