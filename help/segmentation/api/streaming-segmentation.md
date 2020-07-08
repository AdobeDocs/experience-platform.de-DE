---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming-Segmentierung
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 1%

---


# Bewerten Sie Ereignis in Echtzeit mit der Streaming-Segmentierung.

>[!NOTE]
>
>Im folgenden Dokument wird erläutert, wie die Streaming-Segmentierung mithilfe der API verwendet wird. Informationen zur Verwendung der Streaming-Segmentierung mithilfe der Benutzeroberfläche finden Sie im Handbuch [Segmentaufbau](../ui/overview.md#streaming-segmentation).

Die Streaming-Segmentierung für [!DNL Adobe Experience Platform] ermöglicht es Kunden, die Segmentierung in Echtzeit durchzuführen und sich dabei auf den Datenreichtum zu konzentrieren. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten eingehen, [!DNL Platform]was die Planung und Ausführung von Segmentierungsaufträgen verringert. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, während die Daten weitergegeben werden. [!DNL Platform]Das bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden.

![](../images/api/streaming-segment-evaluation.png)

## Erste Schritte

Dieses Entwicklerhandbuch erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die mit der Streaming-Segmentierung zusammenhängen. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches Verbraucherdatenquellen-Profil in Echtzeit, basierend auf aggregierten Daten aus mehreren Quellen.
- [!DNL Segmentation](../home.md): Ermöglicht das Erstellen von Segmenten und Audiencen aus Ihren [!DNL Real-time Customer Profile] Daten.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Platform] APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

Dieses Entwicklerhandbuch enthält Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur [!DNL Experience Platform] Fehlerbehebung.

### Werte für erforderliche Kopfzeilen sammeln

Um [!DNL Platform] APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind zu bestimmten virtuellen Sandboxen isoliert. Alle Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform]finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

Es können zusätzliche Header erforderlich sein, um bestimmte Anforderungen abzuschließen. Die richtigen Kopfzeilen werden in jedem der Beispiele in diesem Dokument angezeigt. Achten Sie besonders auf die Beispielanforderungen, um sicherzustellen, dass alle erforderlichen Header enthalten sind.

### Streaming-Segmentierungsaktivierung von Abfragen {#streaming-segmentation-query-types}

>[!NOTE]
>
>Sie müssen die geplante Segmentierung für das Unternehmen aktivieren, damit die Streaming-Segmentierung funktioniert. Informationen zur Aktivierung der geplanten Segmentierung finden Sie im Abschnitt zur [Aktivierung der geplanten Segmentierung](#enable-scheduled-segmentation)

Damit ein Segment mithilfe der Streaming-Segmentierung bewertet werden kann, muss die Abfrage den folgenden Richtlinien entsprechen.

| Abfrage | Details |
| ---------- | ------- |
| Eingehender Treffer | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. |
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis **innerhalb der letzten sieben Tage** verweist. |
| Eingehender Treffer, der sich auf ein Profil bezieht | Eine Segmentdefinition, die sich auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profil-Attribute bezieht. |
| Eingehender Treffer, der sich auf ein Profil innerhalb eines relativen Zeitfensters bezieht | Eine Segmentdefinition, die sich **innerhalb der letzten sieben Tage** auf ein einzelnes eingehendes Ereignis und ein oder mehrere Profil-Attribute bezieht. |
| Mehrere Ereignis, die auf ein Profil verweisen | Eine Segmentdefinition, die sich **innerhalb der letzten 24 Stunden** auf mehrere Ereignis bezieht und (optional) ein oder mehrere Profil-Attribute besitzt. |

Im folgenden Abschnitt werden Segmentdefinitionsbeispiele Liste, die für die Streaming-Segmentierung **nicht** aktiviert werden.

| Abfrage | Details |
| ---------- | ------- | 
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Wenn sich die Segmentdefinition auf ein eingehendes Ereignis bezieht, das **nicht** innerhalb der **letzten sieben Tage** liegt. Zum Beispiel innerhalb der **letzten zwei Wochen**. |
| Eingehender Treffer, der sich auf ein Profil in einem relativen Fenster bezieht | Die folgenden Optionen unterstützen **keine** Streaming-Segmentierung:<ul><li>Ein eingehendes Ereignis **nicht** innerhalb der **letzten sieben Tage**.</li><li>Eine Segmentdefinition, die Segmente oder Eigenschaften des Adobe Audience Managers (AAM) enthält.</li></ul> |
| Mehrere Ereignis, die auf ein Profil verweisen | Die folgenden Optionen unterstützen **keine** Streaming-Segmentierung:<ul><li>Ein Ereignis, das **nicht** innerhalb **der letzten 24 Stunden** auftritt.</li><li>Eine Segmentdefinition, die Segmente oder Eigenschaften des Adobe Audience Managers (AAM) enthält.</li></ul> |
| Abfragen mit mehreren Entitäten | Abfragen mit mehreren Entitäten werden durch Streaming-Segmentierung insgesamt **nicht** unterstützt. |

Darüber hinaus gelten einige Richtlinien für die Streaming-Segmentierung:

| Abfrage | Leitlinie |
| ---------- | -------- |
| Abfrage mit einem Ereignis | Das Rückblickfenster ist auf **sieben Tage** begrenzt. |
| Abfrage mit Ereignis-Verlauf | <ul><li>Das Lookback-Fenster ist auf **einen Tag** beschränkt.</li><li>Zwischen den Ereignissen **muss** eine strikte Zeitbestellbedingung bestehen.</li><li>Nur einfache Zeitreihenfolgen (vor und nach) zwischen den Ereignissen sind zulässig.</li><li>Die einzelnen Ereignis **können nicht** negiert werden. Die gesamte Abfrage **kann** jedoch negiert werden.</li></ul> |

## Rufen Sie alle Segmente ab, die für die Streaming-Segmentierung aktiviert sind.

Sie können eine Liste aller Segmente abrufen, die für die Streaming-Segmentierung innerhalb Ihrer IMS-Organisation aktiviert sind, indem Sie eine GET-Anforderung an den `/segment/definitions` Endpunkt senden.

**API-Format**

Um Streaming-fähige Segmente abzurufen, müssen Sie den Parameter &quot;Abfrage&quot; `evaluationInfo.continuous.enabled=true` in den Anforderungspfad einbeziehen.

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

Eine erfolgreiche Antwort gibt ein Array von Segmenten in Ihrer IMS-Organisation zurück, die für die Streaming-Segmentierung aktiviert sind.

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

## Erstellen eines Streaming-fähigen Segments

Ein Segment wird automatisch für das Streaming aktiviert, wenn es mit einem der oben [aufgeführten](#streaming-segmentation-query-types)Streaming-Segmentierungstypen übereinstimmt.

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
>Hierbei handelt es sich um eine Standardanforderung für das Erstellen eines Segments. Weitere Informationen zum Erstellen einer Segmentdefinition finden Sie im Tutorial zum [Erstellen eines Segments](../tutorials/create-a-segment.md).

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Segmentdefinition mit aktiviertem Streaming zurück.

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

## Geplante Evaluierung aktivieren {#enable-scheduled-segmentation}

Nachdem die Streaming-Bewertung aktiviert wurde, muss eine Grundlinie erstellt werden (danach ist das Segment immer auf dem neuesten Stand). Zuerst muss eine geplante Evaluierung (auch als geplante Segmentierung bezeichnet) aktiviert werden, damit das System automatisch Baselining durchführen kann. Bei der geplanten Segmentierung kann Ihr IMS-Org an einen wiederkehrenden Zeitplan festhalten, um Exportaufträge automatisch zur Segmentauswertung auszuführen.

>[!NOTE]
>
>Geplante Auswertung kann für Sandboxen mit maximal fünf (5) Zusammenführungsrichtlinien für XDM Individuelles Profil aktiviert werden. Wenn Ihr Unternehmen über mehr als fünf Richtlinien zum Zusammenführen von XDM-Profilen innerhalb einer einzelnen Sandbox-Umgebung verfügt, können Sie keine geplante Auswertung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anforderung an den `/config/schedules` Endpunkt senden, können Sie einen Zeitplan erstellen und die Uhrzeit einschließen, zu der der Zeitplan ausgelöst werden soll.

**API-Format**

```http
POST /config/schedules
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Zeitplan basierend auf den in der Nutzlast bereitgestellten Spezifikationen erstellt.

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
| `properties.segments` | **(Erforderlich, wenn`type`gleich`batch_segmentation`)** Die Verwendung `["*"]` stellt sicher, dass alle Segmente einbezogen werden. |
| `schedule` | **(Erforderlich)** Eine Zeichenfolge, die den Auftragsplan enthält. Aufträge können nur einmal pro Tag ausgeführt werden, d. h., Sie können nicht planen, dass ein Auftrag mehr als einmal während eines Zeitraums von 24 Stunden ausgeführt wird. Das folgende Beispiel (`0 0 1 * * ?`) bedeutet, dass der Auftrag jeden Tag um 1:00:00 UTC ausgelöst wird. Weitere Informationen finden Sie in der Dokumentation zum [Cron-Ausdruck](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . |
| `state` | *(Optional)* String, der den Planstatus enthält. Verfügbare Werte: `active` und `inactive`. Der Standardwert ist `inactive`. Eine IMS-Organisation kann nur einen Zeitplan erstellen. Schritte zum Aktualisieren des Zeitplans sind weiter unten in diesem Lernprogramm verfügbar. |

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

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state` Eigenschaft ist im Anforderungstext &quot;Erstellen&quot;(POST) auf `active` eingestellt. Sie können einen Zeitplan aktivieren ( `state` auf `active`), indem Sie eine PATCH-Anforderung an den `/config/schedules` Endpunkt senden und die ID des Zeitplans in den Pfad einschließen.

**API-Format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Anfrage**

Die folgende Anforderung verwendet die [JSON-Patch-Formatierung](http://jsonpatch.com/) , um den Zeitplan `state` zu aktualisieren `active`.

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

Bei einer erfolgreichen Aktualisierung werden ein leerer Antworttext und HTTP-Status 204 (Kein Inhalt) zurückgegeben.

Derselbe Vorgang kann zum Deaktivieren eines Zeitplans verwendet werden, indem der &quot;Wert&quot;in der vorherigen Anforderung durch &quot;inaktiv&quot;ersetzt wird.

## Nächste Schritte

Nachdem Sie jetzt sowohl neue als auch vorhandene Segmente für die Streaming-Segmentierung aktiviert und die geplante Segmentierung aktiviert haben, um eine Grundlage zu entwickeln und wiederkehrende Bewertungen durchzuführen, können Sie mit der Erstellung von Segmenten für Ihr Unternehmen beginnen.

Weitere Informationen zum Durchführen ähnlicher Aktionen und zum Arbeiten mit Segmenten mithilfe der Benutzeroberfläche &quot;Adobe Experience Platform&quot;finden Sie im [Segment Builder-Benutzerhandbuch](../ui/overview.md).