---
solution: Experience Platform
title: Auswerten von Ereignissen mit Streaming-Segmentierung nahezu in Echtzeit
description: Dieses Dokument enthält Beispiele für die Verwendung der Streaming-Segmentierung mit der Segmentierungs-Service-API von Adobe Experience Platform.
role: Developer
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: e6e9abc7ffe27a2ff9c4ccf4ca243cabdae3d631
workflow-type: tm+mt
source-wordcount: '2052'
ht-degree: 63%

---

# Auswerten von Ereignissen mit Streaming-Segmentierung nahezu in Echtzeit

>[!NOTE]
>
>Im folgenden Dokument wird die Verwendung der Streaming-Segmentierung mithilfe der API beschrieben. Informationen zur Verwendung der Streaming-Segmentierung mithilfe der Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche für die Streaming-Segmentierung](../ui/streaming-segmentation.md).

Mit der Streaming-Segmentierung in [!DNL Adobe Experience Platform] können Kundinnen und Kunden die Segmentierung nahezu in Echtzeit durchführen und sich dabei auf die Relevanz der Daten konzentrieren. Im Rahmen der Streaming-Segmentierung erfolgt jetzt eine Segmentqualifizierung, wenn Streaming-Daten in [!DNL Platform] aufgenommen werden. So wird die Notwendigkeit verringert, Segmentierungsvorgänge zu planen und auszuführen. Mit dieser Funktion können die meisten Segmentregeln jetzt ausgewertet werden, während Daten an [!DNL Platform] übermittelt werden. Das bedeutet, dass die Segmentzugehörigkeit auch ohne Ausführung geplanter Segmentierungsvorgänge auf dem neuesten Stand gehalten wird.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>Die Streaming-Segmentierung funktioniert bei allen Daten, die über eine Streaming-Quelle aufgenommen wurden. Segmente, die mit einer Batch-basierten Quelle erfasst werden, werden jede Nacht ausgewertet, selbst wenn sie für die Streaming-Segmentierung geeignet sind.
>
>Darüber hinaus können Segmentdefinitionen, die mit Streaming-Segmentierung ausgewertet werden, zwischen idealer und tatsächlicher Zugehörigkeit wechseln, wenn die Segmentdefinition auf einer anderen Segmentdefinition basiert, die mithilfe der Batch-Segmentierung ausgewertet wird. Wenn beispielsweise Segment A auf Segment B basiert und Segment B mithilfe der Batch-Segmentierung ausgewertet wird, entfernt sich Segment A weiter von den tatsächlichen Daten, bis es mit der Aktualisierung von Segment B erneut synchronisiert wird, da Segment B nur alle 24 Stunden aktualisiert wird.

## Erste Schritte

Dieses Entwicklerhandbuch setzt Grundkenntnisse der verschiedenen [!DNL Adobe Experience Platform]-Services voraus, die mit Streaming-Segmentierungen zusammenhängen. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen beruht.
- [[!DNL Segmentation]](../home.md): Ermöglicht die Erstellung von Zielgruppen mithilfe von Segmentdefinitionen und anderen externen Quellen aus Ihren [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Platform]-APIs erfolgreich aufrufen zu können.

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
>Sie müssen die geplante Segmentierung für die Organisation aktivieren, damit die Streaming-Segmentierung funktioniert. Informationen zur Aktivierung der geplanten Segmentierung finden Sie im [Abschnitt zum Aktivieren einer geplanten Segmentierung](#enable-scheduled-segmentation).

Damit eine Segmentdefinition mithilfe der Streaming-Segmentierung bewertet werden kann, muss die Abfrage den folgenden Richtlinien entsprechen.

| Abfragetyp | Details |
| ---------- | ------- |
| Einzelnes Ereignis innerhalb eines Zeitfensters von weniger als 24 Stunden | Jede Segmentdefinition, die innerhalb eines Zeitfensters von weniger als 24 Stunden auf ein einzelnes eingehendes Ereignis verweist. |
| Nur Profil | Jede Segmentdefinition, die nur auf ein Profilattribut verweist. |
| Einzelnes Ereignis mit einem Profilattribut innerhalb eines relativen Zeitfensters von weniger als 24 Stunden | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem oder mehreren Profilattributen verweist und innerhalb eines relativen Zeitfensters von weniger als 24 Stunden auftritt. |
| Segment von Segmenten | Jede Segmentdefinition, die eine oder mehrere Batch- oder Streaming-Segmentdefinitionen enthält. **Hinweis:** Wenn das Segment von Segmenten mit **Batch**-Segmentdefinitionen verwendet wird, kann es **24 Stunden**, bis eine Profildisqualifizierung erfolgt. Wenn das Segment von Segmenten mit **Streaming**-Segmentdefinitionen verwendet wird, erfolgt die Profildisqualifizierung auf Streaming-Weise. |
| Mehrere Ereignisse mit einem Profilattribut | Jede Segmentdefinition, die **innerhalb der letzten 24 Stunden** auf mehrere Ereignisse verweist und (optional) ein oder mehrere Profilattribute hat. |

Eine Segmentdefinition wird für die Streaming-Segmentierung in den folgenden Szenarien **nicht** aktiviert:

- Die Segmentdefinition umfasst Segmente oder Merkmale aus Adobe Audience Manager (AAM).
- Die Segmentdefinition umfasst mehrere Entitäten (Abfragen mit mehreren Entitäten).
- Die Segmentdefinition umfasst eine Kombination aus einem einzelnen Ereignis und einem `inSegment`-Ereignis.
   - Wenn das im `inSegment`-Ereignis enthaltene Segment jedoch nur ein Profil ist, wird die Segmentdefinition für die Streaming-Segmentierung **aktiviert**.
- Die Segmentdefinition verwendet „Jahr ignorieren“ als Teil ihrer Zeitbeschränkungen.

Bitte beachten Sie bei der Streaming-Segmentierung die folgenden Richtlinien:

| Abfragetyp | Richtlinie |
| ---------- | -------- |
| Einzelereignisabfrage | Das Lookback-Fenster ist nicht beschränkt. |
| Abfrage mit Ereignisverlauf | <ul><li>Das Lookback-Fenster ist auf **einen Tag** beschränkt.</li><li>Es **muss** eine strikte Bedingung für die zeitliche Reihenfolge zwischen den Ereignissen vorhanden sein.</li><li>Abfragen mit mindestens einem negierten Ereignis werden unterstützt. Das gesamte Ereignis kann jedoch **keine** Negation sein.</li></ul> |

Wenn eine Segmentdefinition geändert wird, sodass sie die Kriterien für die Streaming-Segmentierung nicht mehr erfüllt, wird die Segmentdefinition automatisch von „Streaming“ zu „Batch“ geändert.

Darüber hinaus erfolgt die Aufhebung der Segmentqualifikation, ähnlich wie die Segmentqualifikation selbst, in Echtzeit. Wenn sich ein Profil nicht mehr für eine Segmentdefinition qualifiziert, wird die Qualifizierung daher sofort aufgehoben. Wenn in der Segmentdefinition beispielsweise nach „Alle Benutzenden, die in den letzten drei Stunden rote Schuhe gekauft haben“ gefragt wird, wird die Qualifikation nach drei Stunden für alle Profile, die sich ursprünglich für die Segmentdefinition qualifiziert haben, aufgehoben.

## Abrufen aller für die Streaming-Segmentierung aktivierten Segmentdefinitionen

Sie können eine Liste aller Segmentdefinitionen abrufen, die für die Streaming-Segmentierung in Ihrem Unternehmen aktiviert sind, indem Sie eine GET-Anfrage an den `/segment/definitions`-Endpunkt stellen.

**API-Format**

Um Streaming-fähige Segmentdefinitionen abzurufen, müssen Sie den Abfrageparameter `evaluationInfo.continuous.enabled=true` in den Anfragepfad aufnehmen.

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

Eine erfolgreiche Antwort gibt ein Array von Segmentdefinitionen in Ihrer Organisation zurück, die für die Streaming-Segmentierung aktiviert sind.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

## Erstellen einer für Streaming aktivierten Segmentdefinition

Eine Segmentdefinition wird automatisch für Streaming aktiviert, wenn sie mit einem der [oben aufgeführten Streaming-Segmentierungstypen“ ](#query-types).

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
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    }
}'
```

>[!NOTE]
>
>Dies ist eine Standardanfrage zum Erstellen einer Segmentdefinition. Weiterführende Informationen zum Erstellen einer Segmentdefinition finden Sie im Tutorial zum [ einer Segmentdefinition ](../tutorials/create-a-segment.md).

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Definition des neu erstellten Streaming-fähigen Segments zurück.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
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

Nachdem die Streaming-Auswertung aktiviert wurde, muss eine Baseline erstellt werden (wonach die Segmentdefinition immer auf dem neuesten Stand ist). Geplante Auswertungen (auch als geplante Segmentierung bezeichnet) müssen zuerst aktiviert werden, damit das System automatisch Grundlinien erstellt. Bei einer geplanten Segmentierung kann Ihr Unternehmen einen wiederkehrenden Zeitplan einhalten, um Exportaufträge automatisch auszuführen und Segmentdefinitionen auszuwerten.

>[!NOTE]
>
>Die geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihre Organisation in einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verfügt, können Sie keine geplante Auswertung verwenden.

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
| `properties.segments` | **(Erforderlich, wenn `type` gleich `batch_segmentation`)** Durch Verwendung von `["*"]` wird sichergestellt, dass alle Segmentdefinitionen enthalten sind. |
| `schedule` | **(Erforderlich)** Eine Zeichenfolge, die den Auftragszeitplan enthält. Aufträge können nur einmal pro Tag ausgeführt werden, d. h., Sie können einen Auftrag nicht so planen, dass er während eines Zeitraums von 24 Stunden mehr als einmal ausgeführt wird. Das folgende Beispiel (`0 0 1 * * ?`) bedeutet, dass der Auftrag jeden Tag um 1:00:00 Uhr (UTC) ausgelöst wird. Weitere Informationen finden Sie im Anhang zum [Cron-Ausdrucksformat](./schedules.md#appendix) in der Dokumentation zu Zeitplänen innerhalb der Segmentierung. |
| `state` | *(Optional)* Zeichenfolge, die den Zeitplanstatus enthält. Verfügbare Werte: `active` und `inactive`. Der Standardwert ist `inactive`. Eine Organisation kann nur einen Zeitplan erstellen. Schritte zum Aktualisieren des Zeitplans finden Sie weiter unten in dieser Anleitung. |

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

Nachdem Sie sowohl neue als auch vorhandene Segmentdefinitionen für die Streaming-Segmentierung und die geplante Segmentierung aktiviert haben, um eine Baseline zu entwickeln und wiederkehrende Auswertungen durchzuführen, können Sie für Ihr Unternehmen mit der Erstellung von Segmentdefinitionen mit aktiviertem Streaming beginnen.

Informationen zum Ausführen ähnlicher Aktionen und zum Arbeiten mit Segmentdefinitionen mithilfe der Adobe Experience Platform-Benutzeroberfläche finden Sie im [Segment Builder-Benutzerhandbuch](../ui/segment-builder.md).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zur Streaming-Segmentierung:

### Tritt die „Nicht-Qualifizierung“ der Streaming-Segmentierung auch in Echtzeit auf?

In den meisten Fällen geschieht die Aufhebung der Qualifizierung von Streaming-Segmentierungen in Echtzeit. Für Streaming-Segmentdefinitionen, die Segmente von Segmenten verwenden, wird die Qualifizierung jedoch **nicht** in Echtzeit aufgehoben, sondern erst nach 24 Stunden.

### Mit welchen Daten arbeitet die Streaming-Segmentierung?

Die Streaming-Segmentierung funktioniert bei allen Daten, die über eine Streaming-Quelle aufgenommen wurden. Segmente, die mit einer Batch-basierten Quelle erfasst werden, werden jede Nacht ausgewertet, selbst wenn sie für die Streaming-Segmentierung geeignet sind. In das System gestreamte Ereignisse mit einem Zeitstempel, der älter als 24 Stunden ist, werden im nachfolgenden Batch-Vorgang verarbeitet.

### Wie werden Segmentdefinitionen als Batch- oder Streaming-Segmentierung definiert?

Eine Segmentdefinition wird entweder als Batch- oder Streaming-Segmentierung basierend auf einer Kombination aus Abfragetyp und Ereignisverlaufsdauer definiert. Eine Liste der Segmentdefinitionen, die als Streaming-Segment bewertet werden, finden Sie [ Abschnitt „Abfragetypen von Streaming-Segmentierungen](#query-types).

Bitte beachten Sie, dass ein Segment, das **sowohl** einen `inSegment`-Ausdruck als auch eine direkte Einzelereigniskette enthält, nicht für die Streaming-Segmentierung in Frage kommt. Wenn Sie möchten, dass diese Segmentdefinition für die Streaming-Segmentierung qualifiziert ist, sollten Sie die direkte Einzelereigniskette zu einer eigenen Segmentdefinition machen.

### Warum steigt die Anzahl der „insgesamt qualifizierten“ Segmentdefinitionen weiter an, während die Zahl unter „Letzte X Tage“ im Abschnitt mit den Segmentdefinitionsdetails bei null bleibt?

Die Anzahl der insgesamt qualifizierten Segmentdefinitionen wird aus dem täglichen Segmentierungsauftrag abgerufen, der Zielgruppen enthält, die sowohl für Batch- als auch für Streaming-Segmentdefinitionen qualifiziert sind. Dieser Wert wird sowohl für Batch- als auch für Streaming-Segmentdefinitionen angezeigt.

Die Zahl unter „Letzte X Tage“ umfasst **nur** Zielgruppen, die für Streaming-Segmentierung qualifiziert sind. Sie erhöht sich **nur** dann, wenn Sie Daten in das System gestreamt haben, und zählt dann für diese Streaming-Definition. Dieser Wert wird **nur** für Streaming-Segmentdefinitionen angezeigt. Daher wird dieser Wert **kann** für Batch-Segmentdefinitionen als 0 angezeigt.

Wenn Sie also feststellen, dass die Zahl unter „Letzte X Tage“ null ist und das Liniendiagramm ebenfalls null zeigt, haben Sie **Profile in** System gestreamt, die für diese Segmentdefinition qualifiziert wären.

### Wie lange dauert es, bis eine Segmentdefinition verfügbar ist?

Es dauert bis zu einer Stunde, bis eine Segmentdefinition verfügbar ist.

### Gibt es Einschränkungen bei den Daten, die in gestreamt werden?

Damit gestreamte Daten in der Streaming-Segmentierung verwendet werden können **muss** Abstand zwischen den in gestreamten Ereignissen bestehen. Wenn innerhalb derselben Sekunde zu viele Ereignisse gestreamt werden, behandelt Platform diese Ereignisse als von Bots generierte Daten und verwirft sie. Als Best Practice sollten Sie **mindestens** fünf Sekunden zwischen den Ereignisdaten haben, um sicherzustellen, dass die Daten ordnungsgemäß verwendet werden.
