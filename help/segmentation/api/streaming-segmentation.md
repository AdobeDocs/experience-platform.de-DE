---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;Streaming-Segmentierung;Streaming-Segmentierung;Kontinuierliche Auswertung
solution: Experience Platform
title: 'Ereignis in Echtzeit mit Streaming-Segmentierung bewerten '
topic-legacy: developer guide
description: Dieses Dokument enthält Beispiele zur Verwendung der Streaming-Segmentierung mit der Adobe Experience Platform Segmentation Service API.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
translation-type: tm+mt
source-git-commit: b4a04b52ff9a2b7a36fda58d70a2286fea600ff1
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 42%

---

# Bewerten Sie Ereignis in Echtzeit mit der Streaming-Segmentierung.

>[!NOTE]
>
>Im folgenden Dokument wird erläutert, wie die Streaming-Segmentierung mithilfe der API verwendet wird. Informationen zur Verwendung der Streaming-Segmentierung mithilfe der Benutzeroberfläche finden Sie im Handbuch [Streaming-Segmentierungsoberfläche](../ui/streaming-segmentation.md).

Die Streaming-Segmentierung für [!DNL Adobe Experience Platform] ermöglicht es Kunden, die Segmentierung in Echtzeit durchzuführen und sich dabei auf den Datenreichtum zu konzentrieren. Bei der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Streaming-Daten in [!DNL Platform] eingehen, was die Planung und Ausführung von Segmentierungsaufträgen erleichtert. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, wenn die Daten an [!DNL Platform] übergeben werden. Das bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>Streaming-Segmentierung kann nur zur Auswertung von Daten verwendet werden, die in Plattform gestreamt werden. Mit anderen Worten, Daten, die durch die Stapelverarbeitung erfasst werden, werden nicht durch Streaming-Segmentierung ausgewertet und werden zusammen mit dem nächtlich geplanten segmentierten Auftrag ausgewertet.

## Erste Schritte

Dieses Entwicklerhandbuch erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste, die mit der Streaming-Segmentierung zusammenhängen. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Verbraucherdatenquellen-Profil in Echtzeit, basierend auf aggregierten Daten aus mehreren Quellen.
- [[!DNL Segmentation]](../home.md): Ermöglicht das Erstellen von Segmenten und Audiencen aus Ihren  [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um [!DNL Platform]-APIs erfolgreich aufzurufen.

### Lesen von Beispiel-API-Aufrufen

In diesem Entwicklerhandbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

Zum Ausführen spezifischer Anfragen können zusätzliche Kopfzeilen erforderlich sein. Die richtigen Kopfzeilen werden in jedem der Beispiele in diesem Dokument angezeigt. Achten Sie besonders auf die Beispielanfragen, um dafür zu sorgen, dass alle erforderlichen Kopfzeilen enthalten sind.

### Für Streaming-Segmentierung aktivierte Abfragetypen  {#streaming-segmentation-query-types}

>[!NOTE]
>
>Sie müssen die geplante Segmentierung für das Unternehmen aktivieren, damit die Streaming-Segmentierung funktioniert. Informationen zur Aktivierung der geplanten Segmentierung finden Sie im Abschnitt [Geplante Segmentierung aktivieren](#enable-scheduled-segmentation)

Damit ein Segment mithilfe der Streaming-Segmentierung bewertet werden kann, muss die Abfrage den folgenden Richtlinien entsprechen.

| Abfragetyp | Details |
| ---------- | ------- |
| Eingehender Treffer | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. |
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis verweist. |
| Eingehender Treffer mit einem Zeitfenster | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem Zeitfenster verweist. |
| Nur Profil | Eine Segmentdefinition, die nur auf ein Profil-Attribut verweist. |
| Eingehender Treffer, der sich auf ein Profil bezieht | Eine Segmentdefinition, die sich auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profil-Attribute bezieht. |
| Eingehender Treffer, der sich auf ein Profil innerhalb eines relativen Zeitfensters bezieht | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis und ein oder mehrere Profil-Attribute verweist. |
| Segment der Segmente | Jede Segmentdefinition, die ein oder mehrere Batch- oder Streaming-Segmente enthält. **Hinweis:** Wenn ein Segmentsegment verwendet wird, erfolgt der Profil-Disqualifizierung  **alle 24 Stunden**. |
| Mehrere Ereignis, die auf ein Profil verweisen | Eine Segmentdefinition, die auf mehrere Ereignis **innerhalb der letzten 24 Stunden** und (optional) verweist, verfügt über ein oder mehrere Profil-Attribute. |

Eine Segmentdefinition wird für die Streaming-Segmentierung in den folgenden Szenarien **nicht** aktiviert:

- Die Segmentdefinition umfasst Adobe Audience Manager-Segmente oder -Eigenschaften (AAM).
- Die Segmentdefinition umfasst mehrere Entitäten (Abfragen mit mehreren Entitäten).

Darüber hinaus gelten einige Richtlinien bei der Streaming-Segmentierung:

| Abfragetyp | Leitlinie |
| ---------- | -------- |
| Abfrage mit einem Ereignis | Das Lookback-Fenster unterliegt keinen Einschränkungen. |
| Abfrage mit Ereignis-Verlauf | <ul><li>Das Lookback-Fenster ist auf **einen Tag** beschränkt.</li><li>Zwischen den Ereignissen muss eine strikte Bedingung für die zeitliche Reihenfolge **vorhanden sein.**</li><li>Abfragen mit mindestens einem negierten Ereignis werden unterstützt. Das gesamte Ereignis **kann jedoch keine Negation sein.**</li></ul> |

## Rufen Sie alle Segmente ab, die für die Streaming-Segmentierung aktiviert sind.

Sie können eine Liste aller Segmente abrufen, die für die Streaming-Segmentierung in Ihrer IMS-Organisation aktiviert sind, indem Sie eine GET an den `/segment/definitions`-Endpunkt anfordern.

**API-Format**

Um Streaming-fähige Segmente abzurufen, müssen Sie den Abfrageparameter `evaluationInfo.continuous.enabled=true` in den Anfragepfad einbeziehen.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Gruppe von Segmenten in Ihrer IMS-Organisation zurück, die für Streaming-Segmentierung aktiviert sind.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Streaming-fähiges Segment erstellen

Ein Segment wird automatisch für Streaming aktiviert, wenn es mit einem der oben aufgeführten Streaming-Segmenttypen [übereinstimmt.](#streaming-segmentation-query-types)

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

>[!NOTE]
>
>Hierbei handelt es sich um eine Standardanforderung für das Erstellen eines Segments. Weitere Informationen zum Erstellen einer Segmentdefinition finden Sie im Tutorial [Erstellen eines Segments](../tutorials/create-a-segment.md).

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Definition des neu erstellten Streaming-fähigen Segments zurück.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Geplante Auswertung aktivieren {#enable-scheduled-segmentation}

Nach dem Aktivieren der Streaming-Auswertung muss eine Grundlinie eingerichtet werden (danach ist das Segment immer auf dem neuesten Stand). Zuerst muss eine geplante Evaluierung (auch als geplante Segmentierung bezeichnet) aktiviert werden, damit das System automatisch Baselining durchführen kann. Bei der geplanten Segmentierung kann Ihr IMS-Org an einen wiederkehrenden Zeitplan festhalten, um Exportaufträge automatisch zur Segmentauswertung auszuführen.

>[!NOTE]
>
>Geplante Evaluierung kann für Sandboxen mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihr Unternehmen über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] in einer einzelnen Sandbox-Umgebung verfügt, können Sie keine geplante Auswertung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anfrage an den `/config/schedules`-Endpunkt senden, können Sie einen Zeitplan erstellen und die genaue Zeit einschließen, zu der der Zeitplan ausgelöst werden soll.

**API-Format**

```http
POST /config/schedules
```

**Anfrage**

Mit der folgenden Anfrage wird basierend auf den in der Payload bereitgestellten Angaben ein neuer Zeitplan erstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | **(Erforderlich)** Der Name des Zeitplans. Muss eine Zeichenfolge sein. |
| `type` | **(Erforderlich)** Der Auftragstyp im Zeichenfolgenformat. Die unterstützten Typen sind `batch_segmentation` und `export`. |
| `properties` | **(Erforderlich)** Ein Objekt, das zusätzliche Eigenschaften im Zusammenhang mit dem Zeitplan enthält. |
| `properties.segments` | **(Erforderlich, wenn `type` gleich `batch_segmentation`)** Die Verwendung von `["*"]` stellt sicher, dass alle Segmente einbezogen werden. |
| `schedule` | **(Erforderlich)** Eine Zeichenfolge, die den Auftragszeitplan enthält. Aufträge können nur einmal pro Tag ausgeführt werden, d. h., Sie können einen Auftrag nicht so planen, dass er während eines Zeitraums von 24 Stunden mehr als einmal ausgeführt wird. Das folgende Beispiel (`0 0 1 * * ?`) bedeutet, dass der Auftrag jeden Tag um 1:00:00 Uhr (UTC) ausgelöst wird. Weiterführende Informationen finden Sie in der Dokumentation zum [Cron-Ausdrucksformat](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). |
| `state` | *(Optional)* Zeichenfolge, die den Zeitplanstatus enthält. Verfügbare Werte: `active` und `inactive`. Der Standardwert ist `inactive`. Eine IMS-Organisation kann nur einen Zeitplan erstellen. Schritte zum Aktualisieren des Zeitplans finden Sie weiter unten in dieser Anleitung. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Zeitplans zurück.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
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

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state`-Eigenschaft ist im Text der POST-Anfrage (Erstellen) auf `active` gesetzt. Sie können einen Zeitplan aktivieren (setzen Sie `state` auf `active`), indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und die Kennung des Zeitplans in den Pfad einschließen.

**API-Format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Anfrage**

Die folgende Anfrage nutzt die [JSON-Patch-Formatierung](http://jsonpatch.com/), um den `state` des Zeitplans in `active` zu ändern.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Antwort**

Bei erfolgreicher Aktualisierung werden ein leerer Antworttext und der HTTP-Status 204 (Kein Inhalt) zurückgegeben.

Derselbe Vorgang kann zum Deaktivieren eines Zeitplans verwendet werden, indem der „Wert“ in der vorherigen Anfrage durch „inactive“ ersetzt wird.

## Nächste Schritte

Nachdem Sie jetzt sowohl neue als auch vorhandene Segmente für die Streaming-Segmentierung aktiviert und die geplante Segmentierung aktiviert haben, um eine Grundlinie zu entwickeln und wiederkehrende Bewertungen durchzuführen, können Sie mit der Erstellung Streaming-fähiger Segmente für Ihr Unternehmen beginnen.

Weiterführende Informationen zum Durchführen ähnlicher Aktionen und zum Verwenden von Segmenten unter Einsatz der Benutzeroberfläche von Adobe Experience Platform finden Sie im [Segment Builder-Benutzerhandbuch](../ui/segment-builder.md).
