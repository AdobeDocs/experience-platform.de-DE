---
solution: Experience Platform
title: API-Endpunkt für Zeitpläne
description: Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsvorgänge automatisch einmal täglich ausgeführt werden können.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 15%

---

# Zeitpläne-Endpunkt

Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsvorgänge automatisch einmal täglich ausgeführt werden können. Sie können den `/config/schedules`-Endpunkt verwenden, um eine Liste von Zeitplänen abzurufen, einen neuen Zeitplan zu erstellen, Details zu einem bestimmten Zeitplan abzurufen, einen bestimmten Zeitplan zu aktualisieren oder einen bestimmten Zeitplan zu löschen.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-API. Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderlichen Kopfzeilen sowie Beispiele für API-Aufrufe lesen können.

## Abrufen einer Liste von Zeitplänen {#retrieve-list}

Sie können eine Liste aller Zeitpläne für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den `/config/schedules`-Endpunkt stellen.

**API-Format**

Der `/config/schedules`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Obwohl diese Parameter optional sind, wird ihre Verwendung dringend empfohlen, um kostspieligen Aufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Zeitpläne abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

**Abfrageparameter**

+++ Eine Liste der verfügbaren Abfrageparameter.

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `start` | Gibt an, von welcher Seite der Offset beginnt. Der Standardwert ist 0. | `start=5` |
| `limit` | Gibt die Anzahl der Zeitpläne an, die zurückgegeben werden. Der Standardwert ist 100. | `limit=20` |

+++

**Anfrage**

Mit der folgenden Anfrage werden die letzten zehn in Ihrer Organisation veröffentlichten Zeitpläne abgerufen.

+++ Eine Beispielanfrage zum Abrufen einer Liste von Zeitplänen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Liste von Zeitplänen für die angegebene Organisation als JSON zurückgegeben.

>[!NOTE]
>
>Die folgende Antwort wurde aus Platzgründen gekürzt und zeigt nur den ersten zurückgegebenen Zeitplan an.

+++ Eine Beispielantwort beim Abrufen einer Liste von Zeitplänen.

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
| `_page.pageSize` | Die Größe der Zeitplanseite. |
| `children.name` | Der Name des Zeitplans als Zeichenfolge. |
| `children.type` | Der Typ des Auftrags als Zeichenfolge. Die beiden unterstützten Typen sind „batch_segmentation“ und „export“. |
| `children.properties` | Ein Objekt, das zusätzliche Eigenschaften im Zusammenhang mit dem Zeitplan enthält. |
| `children.properties.segments` | Durch die Verwendung von `["*"]` wird sichergestellt, dass alle Segmente enthalten sind. |
| `children.schedule` | Eine Zeichenfolge, die den Auftragsplan enthält. Aufträge können nur für die Ausführung einmal täglich geplant werden, d. h., Sie können nicht festlegen, dass ein Auftrag innerhalb eines Zeitraums von 24 Stunden mehrmals ausgeführt wird. Weitere Informationen zu Cron-Zeitplänen finden Sie im Anhang zum [Cron-Ausdrucksformat](#appendix). In diesem Beispiel bedeutet „0 0 1 * *&quot;, dass dieser Zeitplan jeden Tag um 1 Uhr morgens ausgeführt wird. |
| `children.state` | Eine Zeichenfolge, die den Status des Zeitplans enthält. Die beiden unterstützten Status sind „aktiv“ und „inaktiv“. Standardmäßig ist der Status auf „inaktiv“ festgelegt. |

+++

## Erstellen neuer Zeitpläne {#create}

Sie können einen neuen Zeitplan erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/config/schedules` senden.

**API-Format**

```http
POST /config/schedules
```

**Anfrage**

+++ Beispielanfrage zum Erstellen eines Zeitplans.

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
| `type` | **Erforderlich.** Der Auftragstyp als Zeichenfolge. Die beiden unterstützten Typen sind „batch_segmentation“ und „export“. |
| `properties` | **Erforderlich.** Ein Objekt, das zusätzliche dem Zeitplan zugehörige Eigenschaften enthält. |
| `properties.segments` | **Erforderlich, wenn `type` gleich „batch_segmentation“ ist.** Mit `["*"]` wird sichergestellt, dass alle Segmente einbezogen werden. |
| `schedule` | *Optional.* Eine Zeichenfolge, die den Zeitplan für den Auftrag enthält. Aufträge können nur für die Ausführung einmal täglich geplant werden, d. h., Sie können nicht festlegen, dass ein Auftrag innerhalb eines Zeitraums von 24 Stunden mehrmals ausgeführt wird. Weitere Informationen zu Cron-Zeitplänen finden Sie im Anhang zum [Cron-Ausdrucksformat](#appendix). In diesem Beispiel bedeutet „0 0 1 * *&quot;, dass dieser Zeitplan jeden Tag um 1 Uhr morgens ausgeführt wird. <br><br>Wenn diese Zeichenfolge nicht angegeben wird, wird automatisch ein systemgenerierter Zeitplan generiert. |
| `state` | *Optional.* Eine Zeichenfolge, die den Status des Zeitplans enthält. Die beiden unterstützten Status sind „aktiv“ und „inaktiv“. Standardmäßig ist der Status auf „inaktiv“ festgelegt. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zum von Ihnen neu erstellten Zeitplan zurück.

+++ Eine Beispielantwort beim Erstellen eines Zeitplans.

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

+++

## Abrufen einzelner Zeitpläne {#get}

Sie können detaillierte Informationen zu einem bestimmten Zeitplan abrufen, indem Sie eine GET-Anfrage an den `/config/schedules`-Endpunkt senden und im Anfragepfad die ID des Zeitplans angeben, den Sie abrufen möchten.

**API-Format**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert des Zeitplans, den Sie abrufen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Abrufen eines Zeitplans.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zum angegebenen Zeitplan zurück.

+++ Eine Beispielantwort beim Abrufen eines Zeitplans.

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
| `type` | Der Typ des Auftrags als Zeichenfolge. Unterstützt werden die Typen `batch_segmentation` und `export`. |
| `properties` | Ein Objekt, das zusätzliche Eigenschaften im Zusammenhang mit dem Zeitplan enthält. |
| `properties.segments` | Durch die Verwendung von `["*"]` wird sichergestellt, dass alle Segmente enthalten sind. |
| `schedule` | Eine Zeichenfolge, die den Auftragsplan enthält. Aufträge können nur einmal pro Tag ausgeführt werden, d. h., Sie können einen Auftrag nicht so planen, dass er während eines Zeitraums von 24 Stunden mehr als einmal ausgeführt wird. Weitere Informationen zu Cron-Zeitplänen finden Sie im Anhang zum [Cron-Ausdrucksformat](#appendix). In diesem Beispiel bedeutet „0 0 1 * *&quot;, dass dieser Zeitplan jeden Tag um 1 Uhr morgens ausgeführt wird. |
| `state` | Eine Zeichenfolge, die den Status des Zeitplans enthält. Unterstützt werden die Status `active` und `inactive`. Standardmäßig lautet der Status `inactive`. |

+++

## Aktualisieren von Details für einen bestimmten Zeitplan {#update}

Sie können einen bestimmten Zeitplan aktualisieren, indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und im Anfragepfad die ID des Zeitplans angeben, den Sie aktualisieren möchten.

Mit der PATCH-Anfrage können Sie entweder den [state](#update-state) oder den [cron-Zeitplan](#update-schedule) für einen einzelnen Zeitplan aktualisieren.

**API-Format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert des Zeitplans, den Sie aktualisieren möchten. |

>[!BEGINTABS]

>[!TAB Zeitplanstatus aktualisieren]

Sie können einen JSON-Patch-Vorgang verwenden, um den Status des Zeitplans zu aktualisieren. Um den Status zu aktualisieren, deklarieren Sie die `path`-Eigenschaft als `/state` und legen die `value` entweder auf `active` oder `inactive` fest. Weitere Informationen zu JSON-Patch-Vorgängen finden Sie in der Dokumentation [JSON-Patch](https://datatracker.ietf.org/doc/html/rfc6902).

**Anfrage**

+++ Eine Beispielanfrage zum Aktualisieren des Zeitplanstatus.

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

+++

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `path` | Der Pfad des Werts, den Sie ändern möchten. Da Sie in diesem Fall den Status des Zeitplans aktualisieren, müssen Sie den Wert von `path` auf &quot;/state“ festlegen. |
| `value` | Der aktualisierte Wert des Status des Zeitplans. Dieser Wert kann entweder als „aktiv“ oder „inaktiv“ festgelegt werden, um den Zeitplan zu aktivieren oder zu deaktivieren. Beachten Sie, **Sie einen Zeitplan** können, wenn die Organisation für Streaming aktiviert wurde. |

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 204 (kein Inhalt) zurückgegeben.

>[!TAB Aktualisieren des Cron-Zeitplans]

Sie können einen JSON-Patch-Vorgang verwenden, um den Cron-Zeitplan zu aktualisieren. Um den Zeitplan zu aktualisieren, deklarieren Sie die `path`-Eigenschaft als `/schedule` und legen Sie den `value` auf einen gültigen Cron-Zeitplan fest. Weitere Informationen zu JSON-Patch-Vorgängen finden Sie in der Dokumentation [JSON-Patch](https://datatracker.ietf.org/doc/html/rfc6902). Weitere Informationen zu Cron-Zeitplänen finden Sie im Anhang zum [Cron-Ausdrucksformat](#appendix).

>[!ENDTABS]

**Anfrage**

+++ Eine Beispielanfrage zum Aktualisieren des Zeitplans.

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
| `path` | Der Pfad des Werts, den Sie aktualisieren möchten. Da Sie in diesem Fall den Cron-Zeitplan aktualisieren, müssen Sie den Wert von `path` auf `/schedule` festlegen. |
| `value` | Der aktualisierte Wert des Cron-Zeitplans. Dieser Wert muss in Form eines Cron-Zeitplans angegeben werden. In diesem Beispiel wird der Zeitplan am zweiten Tag jedes Monats ausgeführt. |

+++

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 204 (kein Inhalt) zurückgegeben.

## Löschen einzelner Zeitpläne

Sie können das Löschen eines bestimmten Zeitplans anfordern, indem Sie eine DELETE-Anfrage an den `/config/schedules`-Endpunkt senden und im Anfragepfad die ID des Zeitplans angeben, den Sie löschen möchten.

**API-Format**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert des Zeitplans, den Sie löschen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Löschen eines Zeitplans.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 204 (kein Inhalt) zurückgegeben.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis davon, wie Zeitpläne funktionieren.

## Anhang {#appendix}

Im folgenden Anhang wird das Format der Cron-Ausdrücke erläutert, die in Zeitplänen verwendet werden.

### Format

Ein Cron-Ausdruck ist eine Zeichenfolge, die aus 6 oder 7 Feldern besteht. Der Ausdruck würde in etwa wie folgt aussehen:

`0 0 12 * * ?`

In einer Cron-Ausdruckszeichenfolge steht das erste Feld für die Sekunden, das zweite Feld steht für die Minuten, das dritte Feld steht für die Stunden, das vierte Feld steht für den Tag des Monats, das fünfte Feld steht für den Monat und das sechste Feld steht für den Tag der Woche. Optional können Sie auch ein siebtes Feld einfügen, das das Jahr darstellt.

| Feldname | Erforderlich | Mögliche Werte | Zulässige Sonderzeichen |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Ja | 0-59 | `, - * /` |
| Minutes | Ja | 0-59 | `, - * /` |
| Stunden | Ja | 0-23 | `, - * /` |
| Tag des Monats | Ja | 1-31 | `, - * ? / L W` |
| Monat | Ja | 1-12, JAN-DEZ | `, - * /` |
| Wochentag | Ja | 1-7, SUN-SAT | `, - * ? / L #` |
| Jahr | Nein | Leer, 1970-2099 | `, - * /` |

>[!NOTE]
>
>Bei den Namen der Monate und Namen der Wochentage wird **Groß-/** unterschieden. Daher entspricht `SUN` der Verwendung von `sun`.

Die zulässigen Sonderzeichen stellen die folgenden Bedeutungen dar:

| Sonderzeichen | Beschreibung |
| ----------------- | ----------- |
| `*` | Dieser Wert wird verwendet, um (**)** in einem Feld auszuwählen. Wenn Sie beispielsweise `*` im Feld Stunden eingeben, bedeutet dies **jede** Stunde. |
| `?` | Dieser Wert bedeutet, dass kein bestimmter Wert erforderlich ist. Dies wird im Allgemeinen verwendet, um etwas in einem Feld anzugeben, in dem das Zeichen zulässig ist, es aber im anderen Feld nicht anzugeben. Beispiel: Wenn Sie möchten, dass ein Ereignis an jedem 3. Tag des Monats ausgelöst wird, es Ihnen aber nicht egal ist, welcher Wochentag es ist, geben Sie `3` in das Feld Tag des Monats und `?` in das Feld Wochentag ein. |
| `-` | Dieser Wert wird verwendet, um **einschließlich** Bereiche für das Feld anzugeben. Wenn Sie beispielsweise `9-15` in das Feld Stunden eingeben, bedeutet dies, dass die Stunden 9, 10, 11, 12, 13, 14 und 15 umfassen. |
| `,` | Mit diesem Wert können Sie zusätzliche Werte angeben. Wenn Sie beispielsweise `MON, FRI, SAT` in das Feld Wochentag eingeben, bedeutet dies, dass die Wochentage Montag, Freitag und Samstag enthalten. |
| `/` | Mit diesem Wert werden die Inkremente angegeben. Der vor dem `/` platzierte Wert bestimmt, von wo aus er inkrementiert, während der nach dem `/` platzierte Wert bestimmt, um wie viel er inkrementiert. Wenn Sie beispielsweise `1/7` in das Feld Minuten eingeben, bedeutet dies, dass die Minuten 1, 8, 15, 22, 29, 36, 43, 50 und 57 enthalten. |
| `L` | Dieser Wert wird zum Angeben von `Last` verwendet und hat eine andere Bedeutung, je nachdem, von welchem Feld er verwendet wird. Wenn es mit dem Feld Tag des Monats verwendet wird, stellt es den letzten Tag des Monats dar. Wenn das Feld allein mit dem Wochentag verwendet wird, stellt es den letzten Wochentag dar, nämlich Samstag (`SAT`). Wird es zusammen mit einem anderen Wert mit dem Feld Wochentag verwendet, stellt es den letzten Tag dieses Typs für den Monat dar. Wenn Sie beispielsweise `5L` in das Feld Wochentag einfügen, würde es **nur** den letzten Freitag des Monats einschließen. |
| `W` | Dieser Wert wird verwendet, um den Wochentag anzugeben, der dem angegebenen Tag am nächsten liegt. Wenn Sie z. B. `18W` in das Feld Tag des Monats eingeben und der 18. dieses Monats ein Samstag ist, wird Freitag der 17. diesen Wochentag als Trigger haben. Wenn der 18. eines Monats ein Sonntag wäre, würde er am Montag den 19. Trigger machen, der dem Wochentag am nächsten liegt. Trigger Wenn Sie `1W` in das Feld Tag des Monats eingeben und der nächste Wochentag im Vormonat liegt, wird das Ereignis trotzdem am nächsten Wochentag des (aktuellen **Monats**.</br></br>Darüber hinaus können Sie `L` und `W` zu `LW` kombinieren, wobei der letzte Wochentag des Monats angegeben wird. |
| `#` | Mit diesem Wert wird der n-te Wochentag in einem Monat angegeben. Der vor dem `#` platzierte Wert steht für den Wochentag, während der nach dem `#` platzierte Wert für das Auftreten in dem Monat steht, in dem er liegt. Wenn Sie beispielsweise `1#3` angeben, wird das Ereignis am dritten Sonntag im Monat Trigger. Beachten Sie, dass das Ereignis nicht ausgelöst wird, wenn Sie `X#5` setzen und es an diesem Wochentag in diesem Monat **fünftes Auftreten**. Wenn Sie beispielsweise `1#5` setzen und es keinen fünften Sonntag in diesem Monat gibt, wird das Ereignis **nicht** ausgelöst. |

### Beispiele

Die folgende Tabelle zeigt Beispielzeichenfolgen für Cron-Ausdrücke und erläutert, was sie bedeuten.

| Ausdruck | Erklärung |
| ---------- | ----------- |
| `0 0 13 * * ?` | Die Veranstaltung findet jeden Tag um 13 Uhr statt. |
| `0 30 9 * * ? 2022` | Die Veranstaltung wird im Jahr 2022 jeden Tag um 9.30 Uhr stattfinden. |
| `0 * 18 * * ?` | Das Ereignis wird jede Minute ausgelöst, beginnend um 18 Uhr und endend um 18:59 Uhr, jeden Tag. |
| `0 0/10 17 * * ?` | Die Veranstaltung wird alle zehn Minuten ausgelöst, beginnend um 17 Uhr und endend um 18 Uhr, jeden Tag. |
| `0 13,38 5 ? 6 WED` | Die Veranstaltung wird jeden Mittwoch im Juni um 5:13 Uhr und um 5:38 Uhr stattfinden. |
| `0 30 12 ? * 4#3` | Die Veranstaltung findet jeden Monat um 12:30 Uhr am dritten Mittwoch statt. |
| `0 30 12 ? * 6L` | Die Veranstaltung wird am letzten Freitag eines jeden Monats um 12:30 Uhr stattfinden. |
| `0 45 11 ? * MON-THU` | Die Veranstaltung wird jeden Montag, Dienstag, Mittwoch und Donnerstag um 11:45 Uhr ausgelöst. |