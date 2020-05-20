---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zeitpläne
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 4%

---


# Zeitplan-Entwicklerleitfaden

intro

- Eine Liste von Zeitplänen abrufen
- Neuen Zeitplan erstellen
- Abrufen eines bestimmten Zeitplans
- Einen bestimmten Zeitplan aktualisieren
- Einen bestimmten Zeitplan löschen

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Segmentierungs-API. Bevor Sie fortfahren, lesen Sie bitte das Entwicklerhandbuch für die [Segmentierung](./getting-started.md).

Insbesondere enthält der [Abschnitt](./getting-started.md#getting-started) &quot;Erste Schritte&quot;des Segmentierungsentwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe im Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer Experience Platform-API erforderlich sind.

## Eine Liste von Zeitplänen abrufen

Sie können eine Liste aller Zeitpläne für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anforderung an den `/config/schedules` Endpunkt senden.

**API-Format**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Optional*) Dem Anforderungspfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch das kaufmännische Und (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt.

**Abfrage**

Im Folgenden finden Sie eine Liste der verfügbaren Parameter für die Abfrage von Listen-Zeitplänen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren Zeitpläne abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `start` | Gibt an, von welcher Seite der Offset Beginn wird. Standardmäßig ist dieser Wert 0. |
| `limit` | Gibt die Anzahl der zurückgegebenen Zeitpläne an. Der Standardwert ist 100. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit einer Liste von Zeitplänen für die angegebene IMS-Organisation als JSON zurück.

```json
{
    "_page": {
        "totalCount": 1,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

## Neuen Zeitplan erstellen

Sie können einen neuen Zeitplan erstellen, indem Sie eine POST-Anforderung an den `/config/schedules` Endpunkt senden.

**API-Format**

```http
POST /config/schedules
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| Parameter | Beschreibung |
| --------- | ------------ |
| `name` | **Erforderlich.** Der Name des Zeitplans als Zeichenfolge. |
| `type` | **Erforderlich.** Der Auftragstyp als Zeichenfolge. Die beiden unterstützten Typen sind `batch_segmentation` und `export`. |
| `properties` | **Erforderlich.** Ein Objekt, das zusätzliche Eigenschaften im Zusammenhang mit dem Zeitplan enthält. |
| `properties.segments` | **Erforderlich, wenn`type`gleich`batch_segmentation`.** Durch Verwendung `["*"]` wird sichergestellt, dass alle Segmente einbezogen werden. |
| `schedule` | **Erforderlich.** Eine Zeichenfolge, die den Auftragsplan enthält. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Cron-Ausdruck](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . In diesem Beispiel bedeutet &quot;0 0 1 * *&quot;, dass dieser Zeitplan am ersten des Monats um Mitternacht ausgeführt wird. |
| `state` | *Optional.* Eine Zeichenfolge, die den Planstatus enthält. Die beiden unterstützten Status sind `active` und `inactive`. By default, the state is set to `inactive`. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zu Ihrem neu erstellten Zeitplan zurück.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## Abrufen eines bestimmten Zeitplans

Sie können detaillierte Informationen zu einem bestimmten Zeitplan abrufen, indem Sie eine GET-Anforderung an den `/config/schedules` Endpunkt senden und den `id` Wert des Zeitplans im Anforderungspfad angeben.

**API-Format**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Der `id` Wert des Zeitplans, den Sie abrufen möchten.

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zum angegebenen Zeitplan zurück.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
```

## Details zu einem bestimmten Zeitplan aktualisieren

Sie können einen festgelegten Zeitplan aktualisieren, indem Sie eine PATCH-Anforderung an den `/config/schedules` Endpunkt senden und den `id` Wert des Zeitplans im Anforderungspfad angeben.

Die PATCH-Anforderung unterstützt zwei verschiedene Pfade: `/state` und `/schedule`.

### Status des Zeitplans aktualisieren

Sie können den Status des Zeitplans `/state` aktualisieren - AKTIV oder INAKTIV. Um den Status zu aktualisieren, müssen Sie den Wert als `active` oder `inactive`festlegen.

**API-Format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Der `id` Wert des Zeitplans, den Sie aktualisieren möchten.

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/state",
    "value": "active"
  }
]
'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `path` | Der Pfad des Werts, den Sie patchen möchten. In diesem Fall müssen Sie, da Sie den Status des Zeitplans aktualisieren, den Wert `path` auf `/state`einstellen. |
| `value` | Der aktualisierte Wert der `/state`. Dieser Wert kann entweder als `active` oder `inactive` zur Aktivierung oder Deaktivierung des Zeitplans eingestellt werden. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 204 (Kein Inhalt) zurück.

### Zeitplan-Cron-Plan aktualisieren

Sie können den Cron-Zeitplan `schedule` aktualisieren. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Cron-Ausdruck](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) .

**API-Format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Der `id` Wert des Zeitplans, den Sie aktualisieren möchten.

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `path` | Der Pfad des Werts, den Sie patchen möchten. In diesem Fall müssen Sie, da Sie den Cron-Plan des Zeitplans aktualisieren, den Wert von `path` auf `/schedule`einstellen. |
| `value` | Der aktualisierte Wert der `/state`. Dieser Wert muss in Form eines Cron-Plans vorliegen. In diesem Beispiel wird der Zeitplan jeweils am zweiten Monat ausgeführt. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 204 (Kein Inhalt) zurück.

## Einen bestimmten Zeitplan löschen

Sie können einen bestimmten Zeitplan löschen, indem Sie eine DELETE-Anforderung an das Programm senden `/config/schedules` und den `id` Wert des Zeitplans im Anforderungspfad angeben.

**API-Format**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Der `id` Wert des Zeitplans, den Sie löschen möchten.

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 204 (Kein Inhalt) mit der folgenden Meldung zurückgegeben:

```json
(No Content) Schedule deleted successfully
```

## Nächste Schritte
