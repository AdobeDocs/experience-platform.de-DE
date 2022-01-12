---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; Zeitpläne; Zeitplan; API; API
solution: Experience Platform
title: Zeitplan-API-Endpunkt
topic-legacy: developer guide
description: Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsaufträge einmal täglich automatisch ausgeführt werden können.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 49%

---

# Endpunkt &quot;Zeitpläne&quot;

Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsaufträge einmal täglich automatisch ausgeführt werden können. Sie können die `/config/schedules` Endpunkt zum Abrufen einer Liste von Zeitplänen, Erstellen eines neuen Zeitplans, Abrufen von Details eines bestimmten Zeitplans, Aktualisieren eines bestimmten Zeitplans oder Löschen eines bestimmten Zeitplans.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-. Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Informationen zum Lesen von Beispiel-API-Aufrufen.

## Abrufen einer Liste von Zeitplänen {#retrieve-list}

Sie können eine Liste aller Zeitpläne Ihrer IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/config/schedules` stellen.

**API-Format**

Der `/config/schedules`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Diese Parameter sind zwar optional, doch wird ihre Verwendung dringend empfohlen, um den teuren Verwaltungsaufwand zu reduzieren. Beim Aufruf dieses Endpunkts ohne Angabe von Parametern werden alle für Ihr Unternehmen verfügbaren Zeitpläne abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{START}` | Gibt an, von welcher Seite der Offset beginnt. Der Standardwert ist 0. |
| `{LIMIT}` | Gibt die Anzahl der Zeitpläne an, die zurückgegeben werden. Der Standardwert ist 100. |

**Anfrage**

Mit der folgenden Anfrage werden die letzten zehn Zeitpläne abgerufen, die innerhalb Ihrer IMS-Organisation veröffentlicht wurden.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 200 mit einer Liste der für die angegebene IMS-Organisation abgerufenen Zeitpläne als JSON zurückgegeben.

>[!NOTE]
>
>Die folgende Antwort wurde aus Platzgründen abgeschnitten und zeigt nur den ersten zurückgegebenen Zeitplan an.

```json
{
    "_page": {
        "totalCount": 10,
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

| Eigenschaft | Beschreibung |
| -------- | ------------ |
| `_page.totalCount` | Die Gesamtzahl der zurückgegebenen Zeitpläne. |
| `_page.pageSize` | Die Größe der Seite der Zeitpläne. |
| `children.name` | Der Name des Zeitplans als Zeichenfolge. |
| `children.type` |  Der Auftragstyp als Zeichenfolge. Die beiden unterstützten Typen sind &quot;batch_segmentation&quot;und &quot;export&quot;. |
| `children.properties` | Ein Objekt, das zusätzliche dem Zeitplan zugehörige Eigenschaften enthält. |
| `children.properties.segments` | Mit `["*"]` wird sichergestellt, dass alle Segmente einbezogen werden. |
| `children.schedule` |  Eine Zeichenfolge, die den Zeitplan für den Auftrag enthält. Aufträge können nur einmal pro Tag ausgeführt werden. Das bedeutet, dass Sie nicht planen können, dass ein Auftrag innerhalb eines Zeitraums von 24 Stunden mehrmals ausgeführt wird. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Format von Cron-Ausdrücken](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Die in diesem Bespiel verwendete Eingabe „0 0 1 * *“ legt fest, dass dieser Zeitplan am ersten jedes Monats um 0:00 Uhr ausgeführt wird. |
| `children.state` |  Eine Zeichenfolge, die den Status des Zeitplans enthält. Die beiden unterstützten Status sind &quot;aktiv&quot;und &quot;inaktiv&quot;. Standardmäßig ist der Status auf &quot;inaktiv&quot;festgelegt. |

## Erstellen neuer Zeitpläne {#create}

Sie können einen neuen Zeitplan erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/config/schedules` senden.

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
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| Eigenschaft | Beschreibung |
| -------- | ------------ |
| `name` | **Erforderlich.** Der Name des Zeitplans als Zeichenfolge. |
| `type` | **Erforderlich.** Der Auftragstyp als Zeichenfolge. Die beiden unterstützten Typen sind &quot;batch_segmentation&quot;und &quot;export&quot;. |
| `properties` | **Erforderlich.** Ein Objekt, das zusätzliche dem Zeitplan zugehörige Eigenschaften enthält. |
| `properties.segments` | **Erforderlich, wenn `type` entspricht &quot;batch_segmentation&quot;.** Mit `["*"]` wird sichergestellt, dass alle Segmente einbezogen werden. |
| `schedule` | *Optional.* Eine Zeichenfolge, die den Zeitplan für den Auftrag enthält. Aufträge können nur einmal pro Tag ausgeführt werden. Das bedeutet, dass Sie nicht planen können, dass ein Auftrag innerhalb eines Zeitraums von 24 Stunden mehrmals ausgeführt wird. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Format von Cron-Ausdrücken](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Die in diesem Bespiel verwendete Eingabe „0 0 1 * *“ legt fest, dass dieser Zeitplan am ersten jedes Monats um 0:00 Uhr ausgeführt wird. <br><br>Wenn diese Zeichenfolge nicht angegeben wird, wird automatisch ein systemgenerierter Zeitplan generiert. |
| `state` | *Optional.* Eine Zeichenfolge, die den Status des Zeitplans enthält. Die beiden unterstützten Status sind &quot;aktiv&quot;und &quot;inaktiv&quot;. Standardmäßig ist der Status auf &quot;inaktiv&quot;festgelegt. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zum von Ihnen neu erstellten Zeitplan zurück.

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

## Abrufen einzelner Zeitpläne {#get}

Sie können detaillierte Informationen zu einem bestimmten Zeitplan abrufen, indem Sie eine GET-Anfrage an die `/config/schedules` -Endpunkt und geben Sie die Kennung des Zeitplans an, den Sie im Anfragepfad abrufen möchten.

**API-Format**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id`-Wert des Zeitplans, den Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zum angegebenen Zeitplan zurück.

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

| Eigenschaft | Beschreibung |
| -------- | ------------ |
| `name` | Der Name des Zeitplans als Zeichenfolge. |
| `type` |  Der Auftragstyp als Zeichenfolge. Unterstützt werden die Typen `batch_segmentation` und `export`. |
| `properties` | Ein Objekt, das zusätzliche dem Zeitplan zugehörige Eigenschaften enthält. |
| `properties.segments` | Mit `["*"]` wird sichergestellt, dass alle Segmente einbezogen werden. |
| `schedule` |  Eine Zeichenfolge, die den Zeitplan für den Auftrag enthält. Aufträge können nur einmal pro Tag ausgeführt werden, d. h., Sie können einen Auftrag nicht so planen, dass er während eines Zeitraums von 24 Stunden mehr als einmal ausgeführt wird. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Format von Cron-Ausdrücken](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Die in diesem Bespiel verwendete Eingabe „0 0 1 * *“ legt fest, dass dieser Zeitplan am ersten jedes Monats um 0:00 Uhr ausgeführt wird. |
| `state` |  Eine Zeichenfolge, die den Status des Zeitplans enthält. Unterstützt werden die Status `active` und `inactive`. Standardmäßig lautet der Status `inactive`. |

## Aktualisieren von Details für einen bestimmten Zeitplan {#update}

Sie können einen bestimmten Zeitplan aktualisieren, indem Sie eine PATCH-Anfrage an die `/config/schedules` -Endpunkt und geben Sie die Kennung des Zeitplans an, den Sie im Anfragepfad aktualisieren möchten.

Mit der PATCH-Anfrage können Sie entweder die [state](#update-state) oder [Cron-Zeitplan](#update-schedule) für einen individuellen Zeitplan.

### Aktualisieren des Status eines Zeitplans {#update-state}

Sie können einen JSON Patch-Vorgang verwenden, um den Status des Zeitplans zu aktualisieren. Um den Status zu aktualisieren, deklarieren Sie die `path` Eigenschaft als `/state` und legen Sie die `value` entweder `active` oder `inactive`. Weitere Informationen zum JSON Patch finden Sie im [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902) Dokumentation.

**API-Format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id`-Wert des Zeitplans, den Sie aktualisieren möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
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
]'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `path` | Der Pfad des Werts, den Sie ändern möchten. Da Sie in diesem Fall den Status des Zeitplans aktualisieren, müssen Sie den Wert von `path` auf &quot;/state&quot;. |
| `value` | Der aktualisierte Wert des Status des Zeitplans. Dieser Wert kann entweder als &quot;aktiv&quot;oder &quot;inaktiv&quot;festgelegt werden, um den Zeitplan zu aktivieren oder zu deaktivieren. |

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 204 (kein Inhalt) zurückgegeben.

### Cron-Zeitplan aktualisieren {#update-schedule}

Sie können einen JSON Patch-Vorgang verwenden, um den Cron-Zeitplan zu aktualisieren. Um den Zeitplan zu aktualisieren, deklarieren Sie die `path` Eigenschaft als `/schedule` und legen Sie die `value` zu einem gültigen Cron-Zeitplan. Weitere Informationen zum JSON Patch finden Sie im [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902) Dokumentation. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Format von Cron-Ausdrücken](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**API-Format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id`-Wert des Zeitplans, den Sie aktualisieren möchten. |

**Anfrage**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `path` | Der Pfad des Werts, den Sie aktualisieren möchten. Da Sie in diesem Fall den Cron-Zeitplan aktualisieren, müssen Sie den Wert von `path` nach `/schedule`. |
| `value` | Der aktualisierte Wert des Cron-Zeitplans. Dieser Wert muss in Form eines Cron-Zeitplans angegeben werden. In diesem Beispiel wird der Zeitplan am zweiten Tag jedes Monats ausgeführt. |

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 204 (kein Inhalt) zurückgegeben.

## Löschen einzelner Zeitpläne

Sie können das Löschen eines bestimmten Zeitplans anfordern, indem Sie eine DELETE-Anfrage an die `/config/schedules` -Endpunkt und geben Sie die Kennung des Zeitplans an, den Sie im Anfragepfad löschen möchten.

**API-Format**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id`-Wert des Zeitplans, den Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 204 (kein Inhalt) zurückgegeben.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis davon, wie Zeitpläne funktionieren.
