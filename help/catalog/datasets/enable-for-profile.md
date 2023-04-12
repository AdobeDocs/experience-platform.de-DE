---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Datensatz aktivieren
title: Aktivieren eines Datensatzes für Profil und Identity Service mithilfe von APIs
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie einen Datensatz für die Verwendung mit Echtzeit-Kundenprofil und Identity Service mithilfe von Adobe Experience Platform-APIs aktivieren.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 94%

---

# Aktivieren eines Datensatzes für [!DNL Profile] und [!DNL Identity Service] mithilfe von APIs

In diesem Tutorial wird der Prozess zum Aktivieren eines Datensatzes für die Verwendung in [!DNL Real-Time Customer Profile] und [!DNL Identity Service] beschrieben, der in die folgenden Schritte unterteilt ist:

1. Aktivieren eines Datensatzes für die Verwendung in [!DNL Real-Time Customer Profile] mit einer von zwei Optionen:
   - [Erstellen eines neuen Datensatzes](#create-a-dataset-enabled-for-profile-and-identity)
   - [Konfigurieren eines vorhandenen Datensatzes](#configure-an-existing-dataset)
1. [Aufnehmen von Daten in den Datensatz](#ingest-data-into-the-dataset)
1. [Datenaufnahme nach Echtzeit-Kundenprofil bestätigen](#confirm-data-ingest-by-real-time-customer-profile)
1. [Bestätigen der Datenaufnahme durch Identity Service](#confirm-data-ingest-by-identity-service)

## Erste Schritte

Dieses Tutorial setzt Grundkenntnisse verschiedener Adobe Experience Platform-Services voraus, die mit der Verwaltung von profilaktivierten Datensätzen verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden [!DNL Platform]-Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Identity Service]](../../identity-service/home.md): Aktiviert das [!DNL Real-Time Customer Profile] durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in [!DNL Platform] aufgenommen werden.
- [[!DNL Catalog Service]](../../catalog/home.md): Eine RESTful-API, mit der Sie Datensätze für das [!DNL Real-Time Customer Profile] und [!DNL Identity Service] erstellen und konfigurieren können.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche `Content-Type`-Kopfzeile erforderlich. Der richtige Wert für diese Kopfzeile wird bei Bedarf in den Beispielanfragen angezeigt.

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine `x-sandbox-name`-Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll. Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Konfigurieren eines für Profil und Identität aktivierten Datensatzes {#create-a-dataset-enabled-for-profile-and-identity}

Sie können einen Datensatz für Echtzeit-Kundenprofil und Identity Service sofort nach der Erstellung oder zu einem beliebigen Zeitpunkt nach der Erstellung des Datensatzes aktivieren. Wenn Sie einen bereits erstellten Datensatz aktivieren möchten, folgen Sie den weiter unten in diesem Dokument beschriebenen Schritten zum [Konfigurieren eines vorhandenen Datensatzes](#configure-an-existing-dataset).

>[!NOTE]
>
>Um einen neuen profilaktivierten Datensatz zu erstellen, müssen Sie die ID eines vorhandenen XDM-Schemas kennen, das für Profil aktiviert ist. Informationen zum Nachschlagen oder Erstellen eines profilaktivierten Schemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der Schema Registry-API](../../xdm/tutorials/create-schema-api.md).

Um einen Datensatz zu erstellen, der für Profil aktiviert ist, können Sie eine POST-Anfrage an den `/dataSets`-Endpunkt verwenden.

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Durch Einbeziehung von `unifiedProfile` und `unifiedIdentity` unter `tags` im Anfragetext wird der Datensatz sofort für [!DNL Profile] bzw. [!DNL Identity Service] aktiviert. Die Werte dieser Tags müssen ein Array sein, das die Zeichenfolge `"enabled:true"` enthält.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schemaRef.id` | Die ID des [!DNL Profile]-aktivierten Schemas, auf dem der Datensatz basieren soll. |
| `{TENANT_ID}` | Der Namespace innerhalb der [!DNL Schema Registry], der Ressourcen enthält, die zu Ihrer Organisation gehören. Weitere Informationen finden Sie im Abschnitt [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) des [!DNL Schema Registry]-Entwicklerhandbuchs. |

**Antwort**

Eine erfolgreiche Antwort zeigt ein Array mit der ID des neu erstellten Datensatzes in der Form `"@/dataSets/{DATASET_ID}"`. Nachdem Sie einen Datensatz erfolgreich erstellt und aktiviert haben, fahren Sie mit den Schritten zum [Hochladen von Daten](#upload-data-to-the-dataset) fort.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Konfigurieren eines vorhandenen Datensatzes {#configure-an-existing-dataset}

In den folgenden Schritten wird beschrieben, wie Sie einen zuvor erstellten Datensatz für [!DNL Real-Time Customer Profile] und [!DNL Identity Service] aktivieren. Wenn Sie bereits einen profilaktivierten Datensatz erstellt haben, fahren Sie mit den Schritten für die [Datenaufnahme](#ingest-data-into-the-dataset) fort.

### Überprüfen auf eine Aktivierung des Datensatzes {#check-if-the-dataset-is-enabled}

Mithilfe der [!DNL Catalog]-API können Sie einen vorhandenen Datensatz untersuchen, um festzustellen, ob er für die Verwendung in [!DNL Real-Time Customer Profile] und [!DNL Identity Service] aktiviert ist. Der folgende Aufruf ruft die Details eines Datensatzes nach ID ab.

**API-Format**

```http
GET /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DATASET_ID}` | Die ID des Datensatzes, den Sie untersuchen möchten. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
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
            "dule": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Unter der `tags`-Eigenschaft ist zu sehen, dass sowohl `unifiedProfile` als auch `unifiedIdentity` mit dem Wert `enabled:true` vorliegen. Daher sind [!DNL Real-Time Customer Profile] bzw. [!DNL Identity Service] für diesen Datensatz aktiviert.

### Aktivieren des Datensatzes {#enable-the-dataset}

Wenn der vorhandene Datensatz nicht für [!DNL Profile] oder [!DNL Identity Service] aktiviert ist, können Sie ihn aktivieren, indem Sie eine PATCH-Anfrage mit der Datensatz-ID stellen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

Der Anfragetext enthält einen `path` zu zwei Arten von Tags, `unifiedProfile` und `unifiedIdentity`. Als `value` sind jeweils Arrays mit der Zeichenfolge `enabled:true` angegeben.

**Antwort**

Bei einer erfolgreichen PATCH-Anfrage wird der HTTP-Status 200 (OK) sowie ein Array mit der ID des gelöschten Datensatzes zurückgegeben. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die Tags `unifiedProfile` und `unifiedIdentity` wurden hinzugefügt und der Datensatz ist für Profil und Identity Service aktiviert.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Aufnehmen von Daten in den Datensatz {#ingest-data-into-the-dataset}

Sowohl [!DNL Real-Time Customer Profile] als auch [!DNL Identity Service] verwenden XDM-Daten, wenn sie in einen Datensatz aufgenommen werden. Anweisungen zum Hochladen von Daten in einen Datensatz finden Sie im Tutorial zum [Erstellen eines Datensatzes mithilfe von APIs](../../catalog/datasets/create.md). Bei der Planung, welche Daten an Ihren [!DNL Profile]-aktivierten Datensatz gesendet werden, sollten die folgenden Best Practices berücksichtigt werden:

- Schließen Sie alle Daten ein, die Sie als Segmentierungskriterien verwenden möchten.
- Schließen Sie so viele IDs ein, wie Sie über Ihre Profildaten ermitteln können, um Ihr Identitätsdiagramm zu maximieren. So kann [!DNL Identity Service] Identitäten effektiver über Datensätze hinweg zusammenfügen.

## Bestätigen der Datenaufnahme durch das [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einer neuen ETL oder Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie wie erwartet hochgeladen wurden. Mit der Zugriffs-API des [!DNL Real-Time Customer Profile] können Sie Batch-Daten abrufen, sobald sie in einen Datensatz geladen werden. Wenn Sie keine der erwarteten Entitäten abrufen können, ist Ihr Datensatz möglicherweise nicht für [!DNL Real-Time Customer Profile] aktiviert. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihren Erwartungen entsprechen. Ausführliche Anweisungen zur Verwendung der [!DNL Real-Time Customer Profile]-API für den Zugriff auf [!DNL Profile]-Daten finden Sie im [Handbuch für Entitäten-Endpunkte](../../profile/api/entities.md), auch bekannt als „[!DNL Profile Access]“-API.

## Bestätigen der Datenaufnahme durch Identity Service {#confirm-data-ingest-by-identity-service}

Jedes erfasste Datenfragment, das mehr als eine Identität enthält, erstellt einen Link in Ihrem privaten Identitätsdiagramm. Um weitere Informationen zu Identitätsdiagrammen und zum Zugriff auf Identitätsdaten zu erhalten, lesen Sie zunächst die Seite [Identity Service – Übersicht](../../identity-service/home.md).
