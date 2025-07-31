---
title: API-Endpunkt für externe Zielgruppen
description: Erfahren Sie, wie Sie mit der API für externe Zielgruppen Ihre externen Zielgruppen aus Adobe Experience Platform erstellen, aktualisieren, aktivieren und löschen können.
exl-id: eaa83933-d301-48cb-8a4d-dfeba059bae1
source-git-commit: 3e1eb697569d75d0ef3af53be1a556bdcd8a293b
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 9%

---

# Endpunkt für externe Zielgruppen

Mit externen Zielgruppen können Sie Profildaten aus Ihren externen Quellen in Adobe Experience Platform hochladen. Sie können den `/external-audience`-Endpunkt in der Segmentierungs-Service-API verwenden, um eine externe Zielgruppe in Experience Platform aufzunehmen, Details anzuzeigen und Ihre externen Zielgruppen zu aktualisieren sowie Ihre externen Zielgruppen zu löschen.

## Erste Schritte

>[!IMPORTANT]
>
>Den Endpunkten in diesem Handbuch wird im Gegensatz zu `/core/ais` das Präfix `/core/ups` vorangestellt.

Um Experience Platform-APIs verwenden zu können, müssen Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle an [!DNL Experience Platform]-APIs gerichtete Anfragen müssen über eine Kopfzeile verfügen, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Externe Zielgruppe erstellen {#create-audience}

Sie können eine externe Zielgruppe erstellen, indem Sie eine POST-Anfrage an den `/external-audience/`-Endpunkt senden.

**API-Format**

```http
POST /external-audience/
```

**Anfrage**

+++ Beispielanfrage zum Erstellen einer externen Zielgruppe.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `name` | Zeichenfolge | Der Name für die externe Zielgruppe. |
| `description` | String | Eine optionale Beschreibung für die externe Zielgruppe. |
| `customAudienceId` | String | Eine optionale Kennung für Ihre externe Zielgruppe. |
| `fields` | Array von Objekten | Liste der Felder und ihrer Datentypen Beim Erstellen der Feldliste können Sie die folgenden Elemente hinzufügen: <ul><li>`name`: **Erforderlich** Der Name des Felds, das Teil der Spezifikation der externen Zielgruppe ist.</li><li>`type`: **Erforderlich** Der Datentyp, der in das Feld aufgenommen wird. Unterstützte Werte sind `string`, `number`, `long`, `integer`, `date` (`2025-05-13`), `datetime` (`2025-05-23T20:19:00+00:00`) und `boolean`.</li>`identityNs`: **Erforderlich für Identitätsfeld** Der Namespace, der vom Identitätsfeld verwendet wird. Unterstützte Werte umfassen alle gültigen Namespaces, z. B. `ECID` oder `email`.li><li>`labels`: *Optional* Ein Array von Zugriffssteuerungsbeschriftungen für das Feld. Weitere Informationen zu den verfügbaren Zugriffssteuerungsbeschriftungen finden Sie im [Glossar zu Datennutzungsbeschriftungen](/help/data-governance/labels/reference.md). </li></ul> |
| `sourceSpec` | Objekt | Ein Objekt, das die Informationen enthält, wo sich die externe Zielgruppe befindet. Wenn Sie dieses Objekt verwenden **müssen** die folgenden Informationen einschließen: <ul><li>`path`: **Erforderlich**: Der Speicherort der externen Zielgruppe oder des Ordners, der die externe Zielgruppe in der Quelle enthält.</li><li>`type`: **Erforderlich** Der Typ des Objekts, das Sie aus der Quelle abrufen. Dieser Wert kann entweder `file` oder `folder` sein.</li><li>`sourceType`: *Optional* Der Typ der Quelle, von der Sie abrufen. Derzeit wird nur der Wert `Cloud Storage` unterstützt.</li><li>`cloudType`: *Optional* Der Typ des Cloud-Speichers, basierend auf dem Quelltyp. Zu den unterstützten Werten gehören `S3`, `DLZ`, `GCS` und `SFTP`.</li><li>`baseConnectionId`: Die ID der Basisverbindung und wird von Ihrem Quellanbieter bereitgestellt. Dieser Wert ist **erforderlich** wenn ein `cloudType` Wert von `S3`, `GCS` oder `SFTP` verwendet wird. Weitere Informationen finden Sie im Abschnitt [Übersicht über Quell-Connectoren](../../sources/home.md)li></ul> |
| `ttlInDays` | Ganzzahl | Die Datengültigkeit für die externe Zielgruppe in Tagen. Dieser Wert kann zwischen 1 und 90 eingestellt werden. Standardmäßig ist der Ablauf der Daten auf 30 Tage festgelegt. |
| `audienceType` | String | Der Zielgruppentyp für die externe Zielgruppe. Derzeit wird nur `people` unterstützt. |
| `originName` | String | **Erforderlich** Die Herkunft der Zielgruppe. Hier wird angegeben, woher die Zielgruppe stammt. Für externe Zielgruppen sollten Sie `CUSTOM_UPLOAD` verwenden. |
| `namespace` | String | Der Namespace für die Zielgruppe. Standardmäßig ist dieser Wert auf `CustomerAudienceUpload` gesetzt. |
| `labels` | Zeichenfolgen-Array | Die für die externe Zielgruppe geltenden Zugriffssteuerungsbeschriftungen. Weitere Informationen zu den verfügbaren Zugriffssteuerungsbeschriftungen finden Sie im [Glossar zu Datennutzungsbeschriftungen](/help/data-governance/labels/reference.md). |
| `tags` | Zeichenfolgen-Array | Die Tags, die Sie auf die externe Zielgruppe anwenden möchten. Weitere Informationen zu Tags finden Sie im [Handbuch zum Verwalten von Tags](/help/administrative-tags/ui/managing-tags.md). |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 202 mit Details zur neu erstellten externen Zielgruppe zurückgegeben.

+++ Beispielantwort beim Erstellen einer externen Zielgruppe.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `operationId` | Zeichenfolge | Die ID des Vorgangs. Anschließend können Sie diese ID verwenden, um den Status der Erstellung Ihrer Zielgruppe abzurufen. |
| `operationDetails` | Objekt | Ein -Objekt, das die Details der Anfrage enthält, die Sie zum Erstellen der externen Zielgruppe übermittelt haben. |
| `name` | String | Der Name für die externe Zielgruppe. |
| `description` | String | Die Beschreibung für die externe Zielgruppe. |
| `fields` | Array von Objekten | Liste der Felder und ihrer Datentypen Dieses Array bestimmt, welche Felder Sie in Ihrer externen Zielgruppe benötigen. |
| `sourceSpec` | Objekt | Ein Objekt, das die Informationen enthält, wo sich die externe Zielgruppe befindet. |
| `ttlInDays` | Ganzzahl | Die Datengültigkeit für die externe Zielgruppe in Tagen. Dieser Wert kann zwischen 1 und 90 eingestellt werden. Standardmäßig ist der Ablauf der Daten auf 30 Tage festgelegt. |
| `audienceType` | String | Der Zielgruppentyp für die externe Zielgruppe. |
| `originName` | String | **Erforderlich** Die Herkunft der Zielgruppe. Dies gibt an, woher die Zielgruppe kommt. |
| `namespace` | String | Der Namespace für die Zielgruppe. |
| `labels` | Zeichenfolgen-Array | Die für die externe Zielgruppe geltenden Zugriffssteuerungsbeschriftungen. Weitere Informationen zu den verfügbaren Zugriffssteuerungsbeschriftungen finden Sie im [Glossar zu Datennutzungsbeschriftungen](/help/data-governance/labels/reference.md). |


+++

## Abrufen des Erstellungsstatus der Zielgruppe {#retrieve-status}

Sie können den Status der Übermittlung Ihrer externen Zielgruppe abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/external-audiences/operations` stellen und die ID des Vorgangs angeben, den Sie in der Antwort „Externe Zielgruppe erstellen“ erhalten haben.

**API-Format**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{OPERATION_ID}` | Der `id` des Vorgangs, den Sie abrufen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Abrufen des Vorgangsstatus einer externen Zielgruppe.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zum Aufgabenstatus der externen Zielgruppe zurückgegeben.

+++ Eine Beispielantwort, wenn Sie den Aufgabenstatus einer externen Zielgruppe abrufen.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `operationId` | Zeichenfolge | Die ID des Vorgangs, den Sie abrufen. |
| `status` | String | Der Status des Vorgangs. Dies kann einer der folgenden Werte sein: `SUCCESS`, `FAILED`, `PROCESSING`. |
| `operationDetails` | Objekt | Ein Objekt, das Details zur Zielgruppe enthält. |
| `audienceId` | String | Die ID der externen Zielgruppe, die vom Vorgang gesendet wird. |
| `createdBy` | String | Die ID des Benutzers, der die externe Zielgruppe erstellt hat. |
| `createdAt` | Zeitstempel für lange Epochen | Der Zeitstempel in Sekunden, wann die Anfrage zur Erstellung der externen Zielgruppe gesendet wurde. |
| `updatedBy` | String | Die ID des Benutzers, der die Zielgruppe zuletzt aktualisiert hat. |
| `updatedAt` | Zeitstempel für lange Epochen | Der Zeitstempel in Sekunden, wann die Zielgruppe zuletzt aktualisiert wurde. |

+++

## Aktualisieren einer externen Zielgruppe {#update-audience}

>[!NOTE]
>
>Um den folgenden Endpunkt verwenden zu können, benötigen Sie die `audienceId` Ihrer externen Zielgruppe. Sie können Ihre `audienceId` von einem erfolgreichen Aufruf an den `GET /external-audiences/operations/{OPERATION_ID}`-Endpunkt abrufen.

Sie können Felder Ihrer externen Zielgruppe aktualisieren, indem Sie eine PATCH-Anfrage an den `/external-audience`-Endpunkt senden und im Anfragepfad die ID der Zielgruppe angeben.

Bei Verwendung dieses Endpunkts können Sie die folgenden Felder aktualisieren:

- Zielgruppen-Beschreibung
- Kennzeichnungen für die Zugriffssteuerung auf Feldebene
- Zugriffssteuerungsbeschriftungen auf Zielgruppenebene

Durch Aktualisieren des Felds mit diesem Endpunkt **ersetzt** der Inhalt des angeforderten Felds.

**API-Format**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**Anfrage**

+++ Eine Beispielanfrage zum Aktualisieren der Beschreibung der externen Zielgruppe.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `description` | Zeichenfolge | Die aktualisierte Beschreibung für die externe Zielgruppe. |

Darüber hinaus können Sie die folgenden Parameter aktualisieren:

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `labels` | Array | Ein Array, das die aktualisierte Liste der Zugriffsbeschriftungen für die Zielgruppe enthält. Weitere Informationen zu den verfügbaren Zugriffssteuerungsbeschriftungen finden Sie im [Glossar zu Datennutzungsbeschriftungen](/help/data-governance/labels/reference.md). |
| `fields` | Array von Objekten | Ein Array mit den Feldern und den zugehörigen Kennzeichnungen für die externe Zielgruppe. Nur die Felder, die in der PATCH-Anfrage aufgeführt sind, werden aktualisiert. Weitere Informationen zu den verfügbaren Zugriffssteuerungsbeschriftungen finden Sie im [Glossar zu Datennutzungsbeschriftungen](/help/data-governance/labels/reference.md). |
| `ttlInDays` | Ganzzahl | Die Datengültigkeit für die externe Zielgruppe in Tagen. Dieser Wert kann zwischen 1 und 90 eingestellt werden. |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zur aktualisierten externen Zielgruppe zurückgegeben.

+++ Eine Beispielantwort beim Aktualisieren der Beschreibung der externen Zielgruppe.

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## Zielgruppenerfassung starten {#start-audience-ingestion}

>[!IMPORTANT]
>
>Sie **eine** Aufnahme für die externe Zielgruppe starten, wenn bereits eine vorherige Zielgruppenaufnahme in Bearbeitung ist.

>[!NOTE]
>
>Um den folgenden Endpunkt verwenden zu können, benötigen Sie die `audienceId` Ihrer externen Zielgruppe. Sie können Ihre `audienceId` von einem erfolgreichen Aufruf an den `GET /external-audiences/operations/{OPERATION_ID}`-Endpunkt abrufen.

Sie können eine Zielgruppenaufnahme starten, indem Sie eine POST-Anfrage an den folgenden Endpunkt senden und dabei die Zielgruppen-ID angeben.

**API-Format**

```http
POST /external-audience/{AUDIENCE_ID}/runs
```

**Anfrage**

Mit der folgenden Anfrage wird ein Aufnahmevorgang für die externe Zielgruppe Trigger.

+++ Eine Beispielanfrage zum Starten einer Zielgruppen-Aufnahme.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | Zeitstempel der Epoche | **Erforderlich** Der Bereich, der die Startzeit angibt, zu der der Fluss ausgeführt wird, um die zu verarbeitenden Dateien auszuwählen. |
| `dataFilterEndTime` | Zeitstempel der Epoche | Der Bereich, der die Endzeit angibt, zu der der Fluss ausgeführt wird, um die zu verarbeitenden Dateien auszuwählen. |
| `differentialIngestion` | Boolesch | Ein Feld, das bestimmt, ob es sich bei der Aufnahme um eine partielle Aufnahme handelt, basierend auf der Differenz seit der letzten Aufnahme oder einer vollständigen Zielgruppenaufnahme. Standardmäßig ist dieser Wert `true`. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zur Aufnahmeausführung zurück.

+++ Eine Beispielantwort beim Starten der Zielgruppen-Aufnahme.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `audienceName` | Zeichenfolge | Der Name der Zielgruppe, für die Sie einen Aufnahmevorgang starten. |
| `audienceId` | String | Die ID der Zielgruppe. |
| `runId` | String | Die ID des von Ihnen gestarteten Aufnahmevorgangs. |
| `differentialIngestion` | Boolesch | Ein Feld, das bestimmt, ob es sich bei der Aufnahme um eine partielle Aufnahme handelt, basierend auf der Differenz seit der letzten Aufnahme oder einer vollständigen Zielgruppenaufnahme. |
| `dataFilterStartTime` | Zeitstempel der Epoche | Der Bereich, der die Startzeit angibt, zu der der Fluss ausgeführt wird, um auszuwählen, welche Dateien verarbeitet wurden. |
| `dataFilterEndTime` | Zeitstempel der Epoche | Der Bereich, der die Endzeit angibt, zu der der Fluss ausgeführt wird, um auszuwählen, welche Dateien verarbeitet wurden. |
| `createdAt` | Zeitstempel für lange Epochen | Der Zeitstempel in Sekunden, wann die Anfrage zur Erstellung der externen Zielgruppe gesendet wurde. |
| `createdBy` | String | Die ID des Benutzers, der die externe Zielgruppe erstellt hat. |

+++

## Abrufen eines bestimmten Status der Zielgruppenaufnahme {#retrieve-ingestion-status}

>[!NOTE]
>
>Um den folgenden Endpunkt verwenden zu können, müssen Sie sowohl die `audienceId` Ihrer externen Zielgruppe als auch die `runId` Ihrer Aufnahme-Ausführungs-ID haben. Sie können Ihre `audienceId` von einem erfolgreichen Aufruf an den `GET /external-audiences/operations/{OPERATION_ID}`-Endpunkt und Ihre `runId` von einem vorherigen erfolgreichen Aufruf des `POST /external-audience/{AUDIENCE_ID}/runs`-Endpunkts abrufen.

Sie können den Status einer Zielgruppenaufnahme abrufen, indem Sie eine GET-Anfrage an den folgenden Endpunkt senden und dabei sowohl die Zielgruppen- als auch die Ausführungs-IDs angeben.

**API-Format**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**Anfrage**

Die folgende Anfrage ruft den Aufnahmestatus für die externe Zielgruppe ab.

+++ Eine Beispielanfrage zum Abrufen des Aufnahmestatus der externen Zielgruppe.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zur Aufnahme externer Zielgruppen zurück.

+++ Eine Beispielantwort beim Abrufen der Aufnahme der externen Zielgruppe.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `audienceName` | Zeichenfolge | Der Name der Zielgruppe. |
| `audienceId` | String | Die ID der Zielgruppe. |
| `runId` | String | Die ID des Aufnahmedurchgangs. |
| `status` | String | Der Status des Aufnahmedurchgangs. Mögliche Status sind `SUCCESS` und `FAILED`. |
| `differentialIngestion` | Boolesch | Ein Feld, das bestimmt, ob es sich bei der Aufnahme um eine partielle Aufnahme handelt, basierend auf der Differenz seit der letzten Aufnahme oder einer vollständigen Zielgruppenaufnahme. |
| `dataFilterStartTime` | Zeitstempel der Epoche | Der Bereich, der die Startzeit angibt, zu der der Fluss ausgeführt wird, um auszuwählen, welche Dateien verarbeitet wurden. |
| `dataFilterEndTime` | Zeitstempel der Epoche | Der Bereich, der die Endzeit angibt, zu der der Fluss ausgeführt wird, um auszuwählen, welche Dateien verarbeitet wurden. |
| `createdAt` | Zeitstempel für lange Epochen | Der Zeitstempel in Sekunden, wann die Anfrage zur Erstellung der externen Zielgruppe gesendet wurde. |
| `createdBy` | String | Die ID des Benutzers, der die externe Zielgruppe erstellt hat. |
| `details` | Array von Objekten | Ein Objekt, das die Details des Aufnahmevorgangs enthält. <ul><li>`stage`: Das Stadium des Aufnahmevorgangs. Dies kann entweder `DATASET_INGEST` oder `PROFILE_STORE_INGEST` sein, die die Data-Lake-Aufnahme und die Profilaufnahme darstellen.</li><li>`status`: Der Status der Aufnahme auf dem Staging. Mögliche Status sind `SUCCESS` und `FAILED`.</li><li>`flowRunId`: Die ID der Aufnahme-Flussausführung des Schritts.</li></ul> |

+++

## Auflisten der Aufnahmedurchgänge von Zielgruppen {#list-ingestion-runs}

>[!NOTE]
>
>Um den folgenden Endpunkt verwenden zu können, benötigen Sie die `audienceId` Ihrer externen Zielgruppe. Sie können Ihre `audienceId` von einem erfolgreichen Aufruf an den `GET /external-audiences/operations/{OPERATION_ID}`-Endpunkt abrufen.

Sie können alle Aufnahmedurchgänge für die ausgewählte externe Zielgruppe abrufen, indem Sie eine GET-Anfrage an den folgenden Endpunkt senden und dabei die Zielgruppen-ID angeben. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

**API-Format**

<!-- The following endpoint supports several query parameters to help filter your results. While these parameters are optional, their use is strongly recommended to help focus your results. -->

```http
GET /external-audience/{AUDIENCE_ID}/runs
```

<!-- **Query parameters**

+++ A list of available query parameters. 

| Parameter | Description | Example |
| --------- | ----------- | ------- |
| `limit` | The maximum number of items returned in the response. This value can range from 1 to 40. By default, the limit is set to 20. | `limit=30` |
| `sortBy` | The order in which the returned items are sorted. You can sort by either `name` or by `createdAt`. Additionally, you can add a `-` sign to sort by **descending** order instead of **ascending** order. By default, the items are sorted by `createdAt` in descending order. | `sortBy=name` |
| `property` | A filter to determine which audience ingestion runs are displayed. You can filter on the following properties: <ul><li>`name`: Lets you filter by the audience name. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li><li>`createdAt`: Lets you filter by the ingestion time. If using this property, you can compare by using `>=` or `<=`.</li><li>`status`: Lets you filter by the ingestion run's status. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li></ul>  | `property=createdAt<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++ -->

**Anfrage**

Die folgende Anfrage ruft alle Aufnahmedurchgänge für die externe Zielgruppe ab.

+++ Eine Beispielanfrage zum Abrufen einer Liste von Zielgruppen-Erfassungsdurchgängen.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Liste von Aufnahmedurchgängen für die angegebene externe Zielgruppe zurückgegeben.

+++ Eine Beispielantwort, wenn Sie eine Liste der Audience-Aufnahmedurchgänge abrufen.

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}"
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}"
        }
    ]
}
```

<!-- ,
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
    
| `_page` | Object | An object that contains the pagination information about the list of results. |
     -->

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `runs` | Objekt | Ein -Objekt, das die Liste der Aufnahmedurchgänge enthält, die zur Audience gehören. Weitere Informationen zu diesem Objekt finden Sie im Abschnitt [Abrufen des ](#retrieve-ingestion-status)&quot;. |

+++

## Löschen einer externen Zielgruppe {#delete-audience}

>[!NOTE]
>
>Um den folgenden Endpunkt verwenden zu können, benötigen Sie die `audienceId` Ihrer externen Zielgruppe. Sie können Ihre `audienceId` von einem erfolgreichen Aufruf an den `GET /external-audiences/operations/{OPERATION_ID}`-Endpunkt abrufen.

Sie können eine externe Zielgruppe löschen, indem Sie eine DELETE-Anfrage an den folgenden Endpunkt stellen und dabei die Zielgruppen-ID angeben.

**API-Format**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**Anfrage**

Die folgende Anfrage löscht die angegebene externe Zielgruppe.

+++ Eine Beispielanfrage zum Löschen der externen Zielgruppe.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 mit einem leeren Antworttext zurück.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis davon, wie Sie Ihre externen Zielgruppen mithilfe der Experience Platform-APIs erstellen, verwalten und löschen können. Informationen zur Verwendung externer Zielgruppen mit der Experience Platform-Benutzeroberfläche finden Sie in der [Dokumentation zum Zielgruppenportal](../ui/audience-portal.md).

## Anhang {#appendix}

Im folgenden Abschnitt sind die verfügbaren Fehler-Codes bei Verwendung der API für externe Zielgruppen aufgeführt.

| Plattform-Fehlercode | Status-Code | Nachricht | Beschreibung |
| ------------------- | ----------- | ------- | ----------- |
| 100910-400 | 400 | `BAD_REQUEST` | Aufgrund eines Fehlers bei der Validierung der Anfragen ist eine ungültige Anfrage aufgetreten. |
| 100911-400 | 400 | `BAD_REQUEST` | Ein ungültiges Token wird angegeben. |
| 100920-401 | 401 | `UNAUTHORIZED` | Eine Kopfzeile fehlt. |
| 100921-401 | 401 | `UNAUTHORIZED` | Ein ungültiger `imsOrgId` wurde angegeben. |
| 100922-401 | 401 | `UNAUTHORIZED` | Sie sind nicht berechtigt, die APIs für externe Zielgruppen zu verwenden. |
| 100940-404 | 404 | `NOT_FOUND` | Die angeforderte Zielgruppe wurde nicht gefunden. |
| 100950-409 | 409 | `DUPLICATE_RESOURCE` | Die Zielgruppe existiert bereits. |
| 100960-422 | 422 | `UNPROCESSABLE_ENTITY` | Die Anfragestruktur ist gültig, kann jedoch aufgrund logischer oder semantischer Fehler nicht verarbeitet werden. |
| 100970-500 | 500 | `INTERNAL_SERVER_ERROR` | Bei der Verarbeitung der Anfrage im System ist ein Problem aufgetreten. |
| 100970-502 | 502 | `BAD_GATEWAY` | Es gibt Abhängigkeitsprobleme im nachgelagerten Bereich. |
