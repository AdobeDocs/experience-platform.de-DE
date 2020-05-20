---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming-Segmentierung
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 2%

---


# Bewerten Sie Ereignis in Echtzeit mit der Streaming-Segmentierung (Beta).

>[!NOTE] Die Streaming-Segmentierung ist eine Beta-Funktion und steht auf Anfrage zur Verfügung.

Die Streaming-Segmentierung (auch als kontinuierliche Abfrage bezeichnet) ist die Möglichkeit, einen Kunden sofort zu bewerten, sobald ein Ereignis in eine bestimmte Segmentgruppe aufgenommen wird. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, wenn die Daten an Adobe Experience Platform übergeben werden. Das bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden.

![](../images/api/streaming-segment-evaluation.png)

## Erste Schritte

Dieses Entwicklerhandbuch erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die mit der Streaming-Segmentierung zusammenhängen. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches Verbraucherdatenquellen-Profil in Echtzeit, basierend auf aggregierten Daten aus mehreren Quellen.
- [Segmentierung](../home.md): Ermöglicht das Erstellen von Segmenten und Audiencen aus Ihren Echtzeit-Daten zum Profil von Kunden.
- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich Aufrufe an Plattform-APIs durchführen zu können.

### Lesen von Beispiel-API-Aufrufen

Dieses Entwicklerhandbuch enthält Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchführen zu können, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

Es können zusätzliche Header erforderlich sein, um bestimmte Anforderungen abzuschließen. Die richtigen Kopfzeilen werden in jedem der Beispiele in diesem Dokument angezeigt. Achten Sie besonders auf die Beispielanforderungen, um sicherzustellen, dass alle erforderlichen Header enthalten sind.

### Streaming-Segmentierungsaktivierung von Abfragen

In der folgenden Tabelle werden die verschiedenen Segmentierungsarten und Abfragen, unabhängig davon, ob sie Streaming-Segmentierung unterstützen, Liste.

| Abfrage | Abfrage | Unterstützung der Streaming-Segmentierung |
| ---------- | ------------ | --------------------------------- |
| Einfache demografische | &quot;Gib mir alle Leute, deren Adresse in Kanada ist.&quot; | Unterstützt |
| Zeitreihen-Ereignis | &quot;Gib mir alle Leute, die Lightroom heruntergeladen haben.&quot; | Unterstützt |
| Demografie und Zeitreihen | &quot;Gib mir alle Leute, die in Kanada leben und in den letzten 30 Tagen eine Bestellung aufgegeben haben.&quot; | Unterstützt |
| Fehlen von Ereignissen | &quot;Gib mir alle Menschen, die zwei verschiedene Einkaufswagen innerhalb von zwei Tagen aufgegeben haben.&quot; | Unterstützt |
| Mehrere Entitäten | &quot;Gib mir alle Leute, deren Berechtigungstyp &quot;Erfahren&quot; ist.&quot; | Nicht unterstützt |
| Erweiterte PQL-Funktionen | &quot;Geben Sie mir alle Profile, die in der letzten Woche eine Bestellung aufgegeben haben, und fügen Sie die SKU und den Namen für alle gekauften Produkte bei.&quot; | Nicht unterstützt |

## Rufen Sie alle für die Streaming-Segmentierung aktivierten Segmente ab

Bevor Sie ein neues Streaming-fähiges Segment erstellen oder ein vorhandenes Segment für Streaming-fähig aktualisieren, sollten Sie sicherstellen, dass Sie keine Informationen duplizieren, indem Sie eine Liste aller Streaming-fähigen Segmente abrufen.

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
  -H 'x-sandbox-name: {SANDBOX_NAME'
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

Nachdem Sie bestätigt haben, dass das Segment, das Sie erstellen möchten, noch nicht vorhanden ist, können Sie ein neues Segment erstellen, das für die Streaming-Segmentierung aktiviert ist.

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

Mit der folgenden Anforderung wird ein neues Segment erstellt, bei dem die Streaming-Segmentierung aktiviert ist. Note that the `continuous` section is set to `enabled: true`.

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

>[!NOTE] Dies ist eine Standardanforderung zum Erstellen eines Segments, wobei der hinzugefügte Parameter des `continuous` Abschnitts auf `enabled: true`eingestellt ist. Weitere Informationen zum Erstellen einer Segmentdefinition finden Sie in der Dokumentation zur [Segmenterstellung](../tutorials/create-a-segment.md).

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

## Vorhandenes Segment für Streaming-Segmentierung aktivieren

Sie können ein vorhandenes Segment für die Streaming-Segmentierung aktivieren, indem Sie die ID der Segmentdefinition im Pfad einer PATCH-Anforderung angeben. Darüber hinaus muss die Nutzlast dieser PATCH-Anforderung die vollständigen Details der vorhandenen Segmentdefinition enthalten, auf die zugegriffen werden kann, indem eine GET-Anforderung an die betreffende Segmentdefinition gestellt wird.

### Vorhandene Segmentdefinition suchen

Um eine vorhandene Segmentdefinition nachzuschlagen, müssen Sie ihre ID im Pfad einer GET-Anforderung angeben.

**API-Format**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | Die ID der Segmentdefinition, die Sie nachschlagen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt Details zur angeforderten Segmentdefinition zurück.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] Für die nächste Anforderung benötigen Sie die vollständigen Details der Segmentdefinition, die in dieser Antwort zurückgegeben wurden. Bitte kopieren Sie die Details dieser Antwort, die im Text der nächsten Anforderung verwendet werden soll.

### Vorhandenes Segment für Streaming-Segmentierung aktivieren

Nachdem Sie die Details des Segments kennen, das Sie aktualisieren möchten, können Sie eine PATCH-Anforderung ausführen, um das Segment zu aktualisieren, um die Streaming-Segmentierung zu aktivieren.

**API-Format**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**Anfrage**

Die Nutzlast der folgenden Anforderung stellt die Details der Segmentdefinition (die im [vorherigen Schritt](#look-up-an-existing-segment-definition)abgerufen wurde) bereit und aktualisiert sie, indem sie ihre `continuous.enabled` Eigenschaft in `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
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

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu aktualisierten Segmentdefinition zurück.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
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
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## Geplante Evaluierung aktivieren

Nachdem die Streaming-Bewertung aktiviert wurde, muss eine Grundlinie erstellt werden (danach ist das Segment immer auf dem neuesten Stand). Dies erfolgt automatisch durch das System, die geplante Evaluierung (auch als geplante Segmentierung bezeichnet) muss jedoch zuerst aktiviert werden, damit die Basisberechnung durchgeführt werden kann.

Mit der geplanten Segmentierung kann Ihr IMS-Org einen wiederkehrenden Zeitplan erstellen, um Exportaufträge automatisch auszuführen, um Segmente auszuwerten.

>[!NOTE] Geplante Auswertung kann für Sandboxen mit maximal fünf (5) Zusammenführungsrichtlinien für XDM Individuelles Profil aktiviert werden. Wenn Ihr Unternehmen über mehr als fünf Richtlinien zum Zusammenführen von XDM-Profilen innerhalb einer einzelnen Sandbox-Umgebung verfügt, können Sie keine geplante Auswertung verwenden.

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

Weitere Informationen zum Durchführen ähnlicher Aktionen und zum Arbeiten mit Segmenten mithilfe der Benutzeroberfläche von Adobe Experience Platform finden Sie im [Segment Builder-Benutzerhandbuch](../ui/overview.md).