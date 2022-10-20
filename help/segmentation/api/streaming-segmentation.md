---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; Streaming-Segmentierung; Streaming-Segmentierung; kontinuierliche Auswertung
solution: Experience Platform
title: Bewerten von Ereignissen in nahezu Echtzeit mit Streaming-Segmentierung
topic-legacy: developer guide
description: Dieses Dokument enthält Beispiele zur Verwendung von Streaming-Segmentierung mit der Adobe Experience Platform Segmentation Service-API.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 5a4a8a8b77d06890f212a457e599b66aa46d8b7e
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 32%

---

# Auswerten von Ereignissen mit Streaming-Segmentierung nahezu in Echtzeit

>[!NOTE]
>
>Im folgenden Dokument wird die Verwendung der Streaming-Segmentierung mithilfe der API beschrieben. Informationen zur Verwendung der Streaming-Segmentierung mithilfe der Benutzeroberfläche finden Sie im Abschnitt [Handbuch zur Streaming-Segmentierungsbenutzeroberfläche](../ui/streaming-segmentation.md).

Streaming-Segmentierung in [!DNL Adobe Experience Platform] ermöglicht es Kunden, die Segmentierung nahezu in Echtzeit durchzuführen und sich dabei auf den Datenreichtum zu konzentrieren. Mit Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Streaming-Daten in [!DNL Platform], wodurch Segmentierungsaufträge einfacher geplant und ausgeführt werden müssen. Mit dieser Funktion können die meisten Segmentregeln jetzt ausgewertet werden, wenn die Daten an [!DNL Platform]bedeutet, dass die Segmentzugehörigkeit auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>Streaming-Segmentierung funktioniert mit allen Daten, die mit einer Streaming-Quelle erfasst wurden. Segmente, die mit einer Batch-basierten Quelle erfasst werden, werden nächtlich ausgewertet, selbst wenn sie für Streaming-Segmentierung geeignet sind.
>
>Darüber hinaus können Segmente, die mit Streaming-Segmentierung ausgewertet werden, zwischen idealer und tatsächlicher Mitgliedschaft wechseln, wenn das Segment auf einem anderen Segment basiert, das mithilfe der Batch-Segmentierung ausgewertet wird. Wenn beispielsweise Segment A auf Segment B basiert und Segment B mithilfe der Batch-Segmentierung ausgewertet wird, da Segment B nur alle 24 Stunden aktualisiert wird, entfernt sich Segment A weiter von den tatsächlichen Daten, bis es mit der Aktualisierung Segment B erneut synchronisiert wird.

## Erste Schritte

Dieses Entwicklerhandbuch setzt ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die mit Streaming-Segmentierung verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Verbraucherprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Segmentation]](../home.md): Ermöglicht die Erstellung von Segmenten und Zielgruppen aus Ihren [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich Aufrufe an [!DNL Platform] APIs.

### Lesen von Beispiel-API-Aufrufen

In diesem Entwicklerhandbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

Zum Ausführen spezifischer Anfragen können zusätzliche Kopfzeilen erforderlich sein. Die richtigen Kopfzeilen werden in jedem der Beispiele in diesem Dokument angezeigt. Achten Sie besonders auf die Beispielanfragen, um dafür zu sorgen, dass alle erforderlichen Kopfzeilen enthalten sind.

### Für Streaming-Segmentierung aktivierte Abfragetypen {#query-types}

>[!NOTE]
>
>Sie müssen die geplante Segmentierung für die Organisation aktivieren, damit Streaming-Segmentierung funktioniert. Informationen zur Aktivierung der geplanten Segmentierung finden Sie im Abschnitt [Abschnitt zur geplanten Segmentierung aktivieren](#enable-scheduled-segmentation)

Damit ein Segment mithilfe der Streaming-Segmentierung bewertet werden kann, muss die Abfrage den folgenden Richtlinien entsprechen.

| Abfragetyp | Details |
| ---------- | ------- |
| Einzelereignis | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. |
| Einzelnes Ereignis innerhalb eines relativen Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis verweist. |
| Einzelnes Ereignis mit Zeitfenster | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem Zeitfenster verweist. |
| Nur Profil | Jede Segmentdefinition, die nur auf ein Profilattribut verweist. |
| Einzelnes Ereignis mit einem Profilattribut | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profilattribute verweist. **Hinweis:** Die Abfrage wird sofort ausgewertet, wenn das Ereignis eintritt. Im Fall eines Profilereignisses muss die Integration jedoch 24 Stunden warten. |
| Einzelnes Ereignis mit einem Profilattribut innerhalb eines relativen Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis und ein oder mehrere Profilattribute verweist. |
| Segment von Segmenten | Jede Segmentdefinition, die einen oder mehrere Batch- oder Streaming-Segmente enthält. **Hinweis:** Wenn ein Segment von Segmenten verwendet wird, erfolgt eine Profildisqualifizierung **alle 24 Stunden**. |
| Mehrere Ereignisse mit Profilattribut | Jede Segmentdefinition, die auf mehrere Ereignisse verweist **innerhalb der letzten 24 Stunden** und (optional) ein oder mehrere Profilattribute hat. |

Eine Segmentdefinition **not** für Streaming-Segmentierung in den folgenden Szenarien aktiviert werden:

- Die Segmentdefinition umfasst Adobe Audience Manager-Segmente oder -Eigenschaften (AAM).
- Die Segmentdefinition umfasst mehrere Entitäten (Abfragen mit mehreren Entitäten).

Beachten Sie bei der Streaming-Segmentierung die folgenden Richtlinien:

| Abfragetyp | Richtlinie |
| ---------- | -------- |
| Einzelereignisabfrage | Das Lookback-Fenster ist nicht beschränkt. |
| Abfrage mit Ereignisverlauf | <ul><li>Das Lookback-Fenster ist auf **ein Tag**.</li><li>Eine strikte Bedingung für die Zeitreihenfolge **must** zwischen den Ereignissen vorhanden sind.</li><li>Abfragen mit mindestens einem negativen Ereignis werden unterstützt. Das gesamte Ereignis **cannot** eine Negation sein.</li></ul> |

Wenn eine Segmentdefinition geändert wird, sodass sie die Kriterien für Streaming-Segmentierung nicht mehr erfüllt, wird die Segmentdefinition automatisch von &quot;Streaming&quot;zu &quot;Batch&quot;geändert.

Darüber hinaus erfolgt die Aufhebung der Segmentqualifizierung, ähnlich wie bei der Segmentqualifizierung, in Echtzeit. Wenn sich eine Zielgruppe daher nicht mehr für ein Segment qualifiziert, wird sie sofort nicht qualifiziert. Wenn in der Segmentdefinition beispielsweise nach &quot;Alle Benutzer, die in den letzten drei Stunden rote Schuhe gekauft haben&quot;gefragt wird, werden nach drei Stunden alle Profile, die sich ursprünglich für die Segmentdefinition qualifiziert haben, nicht qualifiziert.

## Alle für Streaming-Segmentierung aktivierten Segmente abrufen

Sie können eine Liste aller Segmente abrufen, die für die Streaming-Segmentierung innerhalb Ihrer IMS-Organisation aktiviert sind, indem Sie eine GET-Anfrage an die `/segment/definitions` -Endpunkt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

Ein Segment wird automatisch für Streaming aktiviert, wenn es mit einem der [oben aufgeführte Streaming-Segmentierungstypen](#query-types).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>Dies ist eine Standardanfrage zum Erstellen eines Segments. Weitere Informationen zum Erstellen einer Segmentdefinition finden Sie im Tutorial zu [Erstellen eines Segments](../tutorials/create-a-segment.md).

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Definition des neu erstellten Streaming-fähigen Segments zurück.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
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

Nach dem Aktivieren der Streaming-Auswertung muss eine Grundlinie eingerichtet werden (danach ist das Segment immer auf dem neuesten Stand). Geplante Auswertung (auch als geplante Segmentierung bezeichnet) muss zuerst aktiviert werden, damit das System automatisch Grundlinien ausführt. Bei geplanter Segmentierung kann Ihre IMS-Organisation einen wiederkehrenden Zeitplan einhalten, um Exportaufträge automatisch zur Auswertung von Segmenten auszuführen.

>[!NOTE]
>
>Die geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile]. Wenn Ihr Unternehmen mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] in einer Sandbox-Umgebung können Sie keine geplante Auswertung verwenden.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schedule` | **(Erforderlich)** Eine Zeichenfolge, die den Auftragszeitplan enthält. Aufträge können nur einmal pro Tag ausgeführt werden, d. h., Sie können einen Auftrag nicht so planen, dass er während eines Zeitraums von 24 Stunden mehr als einmal ausgeführt wird. Das folgende Beispiel (`0 0 1 * * ?`) bedeutet, dass der Auftrag jeden Tag bei 1 ausgelöst wird.:00:00 UTC. Weitere Informationen finden Sie im Anhang im [Cron-Ausdrucksformat](./schedules.md#appendix) in der Dokumentation zu Zeitplänen innerhalb der Segmentierung. |
| `state` | *(Optional)* Zeichenfolge, die den Zeitplanstatus enthält. Verfügbare Werte: `active` und `inactive`. Der Standardwert ist `inactive`. Eine IMS-Organisation kann nur einen Zeitplan erstellen. Schritte zum Aktualisieren des Zeitplans finden Sie weiter unten in dieser Anleitung. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Zeitplans zurück.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
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

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state`-Eigenschaft ist im Text der POST-Anfrage (Erstellen) auf `active` gesetzt. Sie können einen Zeitplan aktivieren (setzen Sie `state` auf `active`), indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und die Kennung des Zeitplans in den Pfad einschließen.

**API-Format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Anfrage**

Die folgende Anfrage nutzt die [JSON-Patch-Formatierung](https://datatracker.ietf.org/doc/html/rfc6902), um den `state` des Zeitplans in `active` zu ändern.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Nachdem Sie sowohl neue als auch vorhandene Segmente für Streaming-Segmentierung aktiviert und die geplante Segmentierung aktiviert haben, um eine Grundlinie zu entwickeln und wiederkehrende Auswertungen durchzuführen, können Sie mit der Erstellung von Streaming-fähigen Segmenten für Ihre Organisation beginnen.

Weiterführende Informationen zum Durchführen ähnlicher Aktionen und zum Verwenden von Segmenten unter Einsatz der Benutzeroberfläche von Adobe Experience Platform finden Sie im [Segment Builder-Benutzerhandbuch](../ui/segment-builder.md).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zur Streaming-Segmentierung:

### Tritt die &quot;Nicht-Qualifizierung&quot;der Streaming-Segmentierung auch in Echtzeit auf?

In den meisten Fällen wird die Qualifizierung der Streaming-Segmentierung in Echtzeit aufgehoben. Streaming-Segmente, die Segmente von Segmenten verwenden, tun dies jedoch **not** in Echtzeit nicht qualifizieren, anstatt die Qualifizierung nach 24 Stunden aufzuheben.

### Auf welche Daten funktioniert Streaming-Segmentierung?

Streaming-Segmentierung funktioniert mit allen Daten, die mit einer Streaming-Quelle erfasst wurden. Segmente, die mit einer Batch-basierten Quelle erfasst werden, werden nächtlich ausgewertet, selbst wenn sie für Streaming-Segmentierung geeignet sind. Ereignisse, die in das System mit einem Zeitstempel von über 24 Stunden gestreamt werden, werden im nachfolgenden Batch-Auftrag verarbeitet.

### Wie werden Segmente als Batch- oder Streaming-Segmentierung definiert?

Ein Segment wird entweder als Batch- oder Streaming-Segmentierung basierend auf einer Kombination aus Abfragetyp und Ereignisverlaufsdauer definiert. Eine Liste der Segmente, die als Streaming-Segment ausgewertet werden, finden Sie im [Abschnitt zu Streaming-Segmentierungs-Abfragetypen](#query-types).

Beachten Sie, dass wenn ein Segment **both** ein `inSegment` -Ausdruck und eine direkte Kette von Einzelereignissen verwenden, kann sie nicht für Streaming-Segmentierung qualifiziert sein. Wenn Sie möchten, dass dieses Segment für Streaming-Segmentierung qualifiziert ist, sollten Sie die direkte Single-Event-Kette zu einem eigenen Segment machen.

### Warum steigt die Anzahl der &quot;insgesamt qualifizierten&quot;Segmente weiterhin, während die Zahl unter &quot;Letzte X Tage&quot;im Abschnitt mit den Segmentdetails bei null bleibt?

Die Anzahl der insgesamt qualifizierten Segmente wird aus dem täglichen Segmentierungsauftrag gezogen, der Zielgruppen enthält, die sich sowohl für Batch- als auch für Streaming-Segmente qualifizieren. Dieser Wert wird sowohl für Batch- als auch für Streaming-Segmente angezeigt.

Die Zahl unter &quot;Letzte X Tage&quot; **only** umfasst Zielgruppen, die für Streaming-Segmentierung qualifiziert sind, und **only** erhöht sich, wenn Sie Daten in das System gestreamt haben, und zählt für diese Streaming-Definition. Dieser Wert ist **only** wird für Streaming-Segmente angezeigt. Daher wird dieser Wert **kann** als 0 für Batch-Segmente anzeigen.

Wenn Sie also feststellen, dass die Zahl unter &quot;Letzte X Tage&quot;null ist und das Liniendiagramm ebenfalls null meldet, haben Sie **not** alle Profile in das System gestreamt, die für dieses Segment qualifiziert wären.