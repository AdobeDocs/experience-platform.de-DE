---
solution: Experience Platform
title: Zeitplan-API-Endpunkt
description: Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsaufträge einmal täglich automatisch ausgeführt werden können.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 16%

---

# Endpunkt &quot;Zeitpläne&quot;

Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsaufträge einmal täglich automatisch ausgeführt werden können. Sie können den Endpunkt `/config/schedules` verwenden, um eine Liste von Zeitplänen abzurufen, einen neuen Zeitplan zu erstellen, Details eines bestimmten Zeitplans abzurufen, einen bestimmten Zeitplan zu aktualisieren oder einen bestimmten Zeitplan zu löschen.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service] -API. Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Anweisungen zum Lesen von Beispiel-API-Aufrufen.

## Abrufen einer Liste von Zeitplänen {#retrieve-list}

Sie können eine Liste aller Zeitpläne für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/config/schedules` senden.

**API-Format**

Der `/config/schedules`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Diese Parameter sind zwar optional, doch wird ihre Verwendung dringend empfohlen, um den teuren Verwaltungsaufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Zeitpläne abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

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

Mit der folgenden Anfrage werden die letzten zehn Zeitpläne abgerufen, die innerhalb Ihres Unternehmens veröffentlicht wurden.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Zeitplänen für die angegebene Organisation als JSON zurück.

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
            "imsOrgId": "{ORG_ID}",
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
| `children.type` | Der Auftragstyp als Zeichenfolge. Die beiden unterstützten Typen sind &quot;batch_segmentation&quot;und &quot;export&quot;. |
| `children.properties` | Ein Objekt, das zusätzliche Eigenschaften im Zusammenhang mit dem Zeitplan enthält. |
| `children.properties.segments` | Durch Verwendung von `["*"]` wird sichergestellt, dass alle Segmente einbezogen werden. |
| `children.schedule` | Eine Zeichenfolge, die den Auftragsplan enthält. Aufträge können nur einmal pro Tag ausgeführt werden. Das bedeutet, dass Sie nicht planen können, dass ein Auftrag innerhalb eines Zeitraums von 24 Stunden mehrmals ausgeführt wird. Weitere Informationen zu Cron-Zeitplänen finden Sie im Anhang zum [Cron-Ausdrucksformat](#appendix). In diesem Beispiel bedeutet &quot;0 0 1 * *&quot;, dass dieser Zeitplan täglich um 1 Uhr ausgeführt wird. |
| `children.state` | Eine Zeichenfolge, die den Status des Zeitplans enthält. Die beiden unterstützten Status sind &quot;aktiv&quot;und &quot;inaktiv&quot;. Standardmäßig ist der Status auf &quot;inaktiv&quot;festgelegt. |

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `properties.segments` | **Erforderlich, wenn `type` gleich &quot;batch_segmentation&quot;ist.** Mit `["*"]` wird sichergestellt, dass alle Segmente einbezogen werden. |
| `schedule` | *Optional.* Eine Zeichenfolge, die den Zeitplan für den Auftrag enthält. Aufträge können nur einmal pro Tag ausgeführt werden. Das bedeutet, dass Sie nicht planen können, dass ein Auftrag innerhalb eines Zeitraums von 24 Stunden mehrmals ausgeführt wird. Weitere Informationen zu Cron-Zeitplänen finden Sie im Anhang zum [Cron-Ausdrucksformat](#appendix). In diesem Beispiel bedeutet &quot;0 0 1 * *&quot;, dass dieser Zeitplan täglich um 1 Uhr ausgeführt wird. <br><br>Wenn diese Zeichenfolge nicht angegeben wird, wird automatisch ein vom System generierter Zeitplan generiert. |
| `state` | *Optional.* Eine Zeichenfolge, die den Status des Zeitplans enthält. Die beiden unterstützten Status sind &quot;aktiv&quot;und &quot;inaktiv&quot;. Standardmäßig ist der Status auf &quot;inaktiv&quot;festgelegt. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zum von Ihnen neu erstellten Zeitplan zurück.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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

Sie können detaillierte Informationen zu einem bestimmten Zeitplan abrufen, indem Sie eine GET-Anfrage an den `/config/schedules` -Endpunkt senden und im Anfragepfad die Kennung des Zeitplans angeben, den Sie abrufen möchten.

**API-Format**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` -Wert des Zeitplans, den Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zum angegebenen Zeitplan zurück.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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
| `type` | Der Auftragstyp als Zeichenfolge. Unterstützt werden die Typen `batch_segmentation` und `export`. |
| `properties` | Ein Objekt, das zusätzliche Eigenschaften im Zusammenhang mit dem Zeitplan enthält. |
| `properties.segments` | Durch Verwendung von `["*"]` wird sichergestellt, dass alle Segmente einbezogen werden. |
| `schedule` | Eine Zeichenfolge, die den Auftragsplan enthält. Aufträge können nur einmal pro Tag ausgeführt werden, d. h., Sie können einen Auftrag nicht so planen, dass er während eines Zeitraums von 24 Stunden mehr als einmal ausgeführt wird. Weitere Informationen zu Cron-Zeitplänen finden Sie im Anhang zum [Cron-Ausdrucksformat](#appendix). In diesem Beispiel bedeutet &quot;0 0 1 * *&quot;, dass dieser Zeitplan täglich um 1 Uhr ausgeführt wird. |
| `state` | Eine Zeichenfolge, die den Status des Zeitplans enthält. Unterstützt werden die Status `active` und `inactive`. Standardmäßig lautet der Status `inactive`. |

## Aktualisieren von Details für einen bestimmten Zeitplan {#update}

Sie können einen bestimmten Zeitplan aktualisieren, indem Sie eine PATCH-Anfrage an den `/config/schedules` -Endpunkt senden und im Anfragepfad die Kennung des Zeitplans angeben, den Sie aktualisieren möchten.

Mit der PATCH-Anfrage können Sie entweder den [Status](#update-state) oder den [Cron-Zeitplan](#update-schedule) für einen einzelnen Zeitplan aktualisieren.

### Aktualisieren des Status eines Zeitplans {#update-state}

Sie können einen JSON Patch-Vorgang verwenden, um den Status des Zeitplans zu aktualisieren. Um den Status zu aktualisieren, deklarieren Sie die `path` -Eigenschaft als `/state` und setzen die `value` auf entweder `active` oder `inactive`. Weitere Informationen zum JSON Patch finden Sie in der Dokumentation zum [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902) .

**API-Format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` -Wert des Zeitplans, den Sie aktualisieren möchten. |

**Anfrage**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | Der Pfad des Werts, den Sie ändern möchten. Da Sie in diesem Fall den Status des Zeitplans aktualisieren, müssen Sie den Wert von `path` auf &quot;/state&quot;setzen. |
| `value` | Der aktualisierte Wert des Status des Zeitplans. Dieser Wert kann entweder als &quot;aktiv&quot;oder &quot;inaktiv&quot;festgelegt werden, um den Zeitplan zu aktivieren oder zu deaktivieren. Beachten Sie, dass Sie einen Zeitplan **nicht deaktivieren können, wenn die Organisation für Streaming aktiviert wurde.** |

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 204 (kein Inhalt) zurückgegeben.

### Cron-Zeitplan aktualisieren {#update-schedule}

Sie können einen JSON Patch-Vorgang verwenden, um den Cron-Zeitplan zu aktualisieren. Um den Zeitplan zu aktualisieren, deklarieren Sie die `path` -Eigenschaft als `/schedule` und setzen die `value` auf einen gültigen Cron-Zeitplan. Weitere Informationen zum JSON Patch finden Sie in der Dokumentation zum [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902) . Weitere Informationen zu Cron-Zeitplänen finden Sie im Anhang zum [Cron-Ausdrucksformat](#appendix).

**API-Format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` -Wert des Zeitplans, den Sie aktualisieren möchten. |

**Anfrage**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * * ?"
    }
]'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `path` | Der Pfad des Werts, den Sie aktualisieren möchten. Da Sie in diesem Fall den Cron-Zeitplan aktualisieren, müssen Sie den Wert von `path` auf `/schedule` setzen. |
| `value` | Der aktualisierte Wert des Cron-Zeitplans. Dieser Wert muss in Form eines Cron-Zeitplans angegeben werden. In diesem Beispiel wird der Zeitplan am zweiten Tag jedes Monats ausgeführt. |

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 204 (kein Inhalt) zurückgegeben.

## Löschen einzelner Zeitpläne

Sie können das Löschen eines bestimmten Zeitplans anfordern, indem Sie eine DELETE-Anfrage an den `/config/schedules` -Endpunkt senden und im Anfragepfad die Kennung des Zeitplans angeben, den Sie löschen möchten.

**API-Format**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` -Wert des Zeitplans, den Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 204 (kein Inhalt) zurückgegeben.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis davon, wie Zeitpläne funktionieren.

## Anhang {#appendix}

Im folgenden Anhang wird das Format der in Zeitplänen verwendeten Cron-Ausdrücke erläutert.

### Format

Ein Cron-Ausdruck ist eine Zeichenfolge aus 6 oder 7 Feldern. Der Ausdruck würde etwa wie folgt aussehen:

`0 0 12 * * ?`

In einer Cron-Ausdruckszeichenfolge stellt das erste Feld die Sekunden, das zweite die Minuten, das dritte Feld die Stunden, das vierte Feld den Tag des Monats, das fünfte Feld den Monat und das sechste Feld den Wochentag dar. Sie können optional auch ein siebtes Feld einfügen, das das Jahr darstellt.

| Feldname | Erforderlich | Mögliche Werte | Zulässige Sonderzeichen |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Ja | 0-59 | `, - * /` |
| Minutes | Ja | 0-59 | `, - * /` |
| Stunden | Ja | 0-23 | `, - * /` |
| Tag des Monats | Ja | 1-31 | `, - * ? / L W` |
| Monat | Ja | 1-12, JAN-DEC | `, - * /` |
| Wochentag | Ja | 1-7, SUN-SAT | `, - * ? / L #` |
| Jahr | Nein | Empty, 1970-2099 | `, - * /` |

>[!NOTE]
>
>Bei den Namen der Monate und den Namen der Wochentage wird zwischen **und nicht** Groß- und Kleinschreibung unterschieden. Daher entspricht `SUN` der Verwendung von `sun`.

Die zulässigen Sonderzeichen stehen für die folgende Bedeutung:

| Sonderzeichen | Beschreibung |
| ----------------- | ----------- |
| `*` | Dieser Wert wird verwendet, um **alle** -Werte in einem Feld auszuwählen. Wenn Sie beispielsweise `*` in das Feld &quot;Stunden&quot;eingeben, bedeutet dies **jede** Stunde. |
| `?` | Dieser Wert bedeutet, dass kein spezifischer Wert erforderlich ist. Dies wird in der Regel verwendet, um etwas in einem Feld anzugeben, in dem das Zeichen zulässig ist, in dem anderen jedoch nicht. Wenn Sie beispielsweise möchten, dass alle drei Monate ein Ereignis ausgelöst werden, sich jedoch nicht um den Wochentag kümmern, setzen Sie `3` in das Monatsfeld und `?` in das Wochentag-Feld. |
| `-` | Dieser Wert wird verwendet, um **einschließlich** Bereiche für das Feld anzugeben. Wenn Sie beispielsweise `9-15` in das Feld Stunden eingeben, würden die Stunden 9, 10, 11, 12, 13, 14 und 15 umfassen. |
| `,` | Dieser Wert wird verwendet, um zusätzliche Werte anzugeben. Wenn Sie beispielsweise `MON, FRI, SAT` in das Feld Wochentag setzen, würden die Wochentage Montag, Freitag und Samstag umfassen. |
| `/` | Dieser Wert wird zum Angeben von Inkrementen verwendet. Der vor dem `/` platzierte Wert bestimmt, von wo er erhöht wird, während der nach dem `/` platzierte Wert bestimmt, um wie viel er erhöht wird. Wenn Sie beispielsweise &quot;`1/7`&quot;in das Feld &quot;Minuten&quot;setzen, würden die Minuten 1, 8, 15, 22, 29, 36, 43, 50 und 57 umfassen. |
| `L` | Dieser Wert wird verwendet, um `Last` anzugeben, und hat je nachdem, von welchem Feld er verwendet wird, eine andere Bedeutung. Wenn es mit dem Tag des Monats-Felds verwendet wird, stellt es den letzten Tag des Monats dar. Wenn es allein mit dem Wochentag verwendet wird, stellt es den letzten Wochentag dar, nämlich Samstag (`SAT`). Wenn es zusammen mit dem Wochentag in Verbindung mit einem anderen Wert verwendet wird, stellt es den letzten Tag dieses Typs für den Monat dar. Wenn Sie beispielsweise `5L` in das Wochentag-Feld eintragen, würde dies **nur** den letzten Freitag des Monats einschließen. |
| `W` | Dieser Wert wird verwendet, um den Wochentag anzugeben, der dem angegebenen Tag am nächsten ist. Wenn Sie beispielsweise &quot;`18W`&quot;in das Monatsfeld setzen und der 18. dieses Monats einen Samstag war, würde dieser am Freitag, dem 17., der nächstgelegenen Wochentag, Trigger haben. Wenn der 18. des Monats ein Sonntag wäre, würde er am Montag am 19., dem nächstgelegenen Wochentag, Trigger haben. Wenn Sie `1W` in das Monatsfeld eintragen und der nächstgelegene Wochentag im Vormonat liegt, wird das Ereignis weiterhin am nächsten Wochentag des **aktuellen** Monats Trigger.</br></br>Außerdem können Sie `L` und `W` zu `LW` kombinieren, was den letzten Wochentag des Monats angibt. |
| `#` | Dieser Wert wird verwendet, um den n-ten Tag der Woche in einem Monat anzugeben. Der vor dem `#` platzierte Wert stellt den Wochentag dar, während der Wert, der nach dem `#` platziert wird, für welches Vorkommen im Monat es sich handelt. Wenn Sie beispielsweise `1#3` setzen, wird das Ereignis am dritten Sonntag des Monats Trigger. Wenn Sie `X#5` setzen und dieser Wochentag nicht zum fünften Mal vorkommt, wird das Ereignis **nicht** ausgelöst. Wenn Sie beispielsweise `1#5` setzen und es keinen fünften Sonntag in diesem Monat gibt, wird das Ereignis **nicht** ausgelöst. |

### Beispiele

Die folgende Tabelle zeigt Beispiel-Cron-Ausdruckszeichenfolgen und erklärt, was sie bedeuten.

| Ausdruck | Erklärung |
| ---------- | ----------- |
| `0 0 13 * * ?` | Das Ereignis wird jeden Tag um 13 Uhr ausgelöst. |
| `0 30 9 * * ? 2022` | Die Veranstaltung wird jeden Tag um 9:30 Uhr im Jahr 2022 ausgelöst. |
| `0 * 18 * * ?` | Das Ereignis wird jede Minute ausgelöst, beginnend um 18.00 Uhr und täglich um 18.59 Uhr. |
| `0 0/10 17 * * ?` | Das Ereignis wird alle zehn Minuten ausgelöst, beginnend um 17 Uhr und bis 18 Uhr, jeden Tag. |
| `0 13,38 5 ? 6 WED` | Die Veranstaltung wird jeden Mittwoch im Juni um 5:13 Uhr und um 5:38 Uhr ausgelöst. |
| `0 30 12 ? * 4#3` | Die Veranstaltung wird jeden Monat um 23:30 Uhr am dritten Mittwoch stattfinden. |
| `0 30 12 ? * 6L` | Das Ereignis wird am letzten Freitag jedes Monats um 23:30 Uhr ausgelöst. |
| `0 45 11 ? * MON-THU` | Die Veranstaltung wird jeden Montag, Dienstag, Mittwoch und Donnerstag um 11:45 Uhr ausgelöst. |