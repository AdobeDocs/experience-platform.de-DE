---
solution: Experience Platform
title: Edge-Segmentierung mithilfe der API
description: Dieses Dokument enthält Beispiele für die Verwendung der Edge-Segmentierung mit der Segmentierungs-Service-API von Adobe Experience Platform.
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 828a586f0264147676da5c43c73d3b3b9d50b9c2
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 70%

---

# Edge-Segmentierung

>[!NOTE]
>
>Im folgenden Dokument erfahren Sie, wie Sie die Edge-Segmentierung mithilfe der API durchführen. Informationen zur Edge-Segmentierung mithilfe der Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche der Edge-Segmentierung](../ui/edge-segmentation.md).
>
>Die Edge-Segmentierung ist jetzt allgemein für alle Benutzenden von Platform verfügbar. Wenn Sie während der Beta-Phase Edge-Segmentdefinitionen erstellt haben, sind diese Segmentdefinitionen weiterhin funktionsfähig.

Bei der Segmentierung in Edge werden Segmentdefinitionen in Adobe Experience Platform sofort am Edge ausgewertet, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

>[!IMPORTANT]
>
> Die Edge-Daten werden an dem Edge-Server-Standort gespeichert, der am nächsten zum Erfassungsort liegt. Sie können auch an einem anderen Speicherort als dem als Hub (oder Prinzipal) für das Adobe Experience Platform-Rechenzentrum festgelegten gespeichert werden.
>
> Außerdem wird die Edge-Segmentierungs-Engine nur Edge-Anfragen berücksichtigen, wenn **eine** primär markierte Identität vorhanden ist, was im Einklang mit nicht-Edge-basierten primären Identitäten steht.

## Erste Schritte

Dieses Entwicklerhandbuch setzt Grundkenntnisse der verschiedenen [!DNL Adobe Experience Platform]-Services voraus, die mit Edge-Segmentierungen zusammenhängen. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen beruht.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht das Erstellen von Zielgruppen aus [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.

Lesen Sie für erfolgreiche Aufrufe an API-Endpunkte in Experience Platform das Handbuch [Erste Schritte mit Platform-APIs](../../landing/api-guide.md), um mehr über erforderliche Kopfzeilen und Beispiele für API-Aufrufe zu erfahren.

## Abfragetypen für Edge-Segmentierungen {#query-types}

Damit ein Segment mithilfe der Edge-Segmentierung ausgewertet werden kann, muss die Abfrage den folgenden Richtlinien entsprechen:

| Abfragetyp | Details |
| ---------- | ------- |
| Einzelnes Ereignis innerhalb eines Zeitfensters von weniger als 24 Stunden | Jede Segmentdefinition, die innerhalb eines Zeitfensters von weniger als 24 Stunden auf ein einzelnes eingehendes Ereignis verweist. |
| Nur Profil | Jede Segmentdefinition, die nur auf ein Profilattribut verweist. |
| Einzelnes Ereignis mit einem Profilattribut innerhalb eines relativen Zeitfensters von weniger als 24 Stunden | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem oder mehreren Profilattributen verweist und innerhalb eines relativen Zeitfensters von weniger als 24 Stunden auftritt. |
| Segment von Segmenten | Jede Segmentdefinition, die eine oder mehrere Batch- oder Streaming-Segmentdefinitionen enthält. **Hinweis:** Wenn das Segment von Segmenten mit **Batch**-Segmentdefinitionen verwendet wird, kann es **24 Stunden**, bis eine Profildisqualifizierung erfolgt. Wenn das Segment von Segmenten mit **Streaming**-Segmentdefinitionen verwendet wird, erfolgt die Profildisqualifizierung auf Streaming-Weise. |
| Mehrere Ereignisse mit einem Profilattribut | Jede Segmentdefinition, die auf mehrere nicht sequenzielle Ereignisse **innerhalb der letzten 24**) verweist und (optional) ein oder mehrere Profilattribute hat. |

Zusätzlich **muss** das Segment an eine Zusammenführungsrichtlinie gebunden sein, die an Edge aktiv ist. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im [Handbuch zu Zusammenführungsrichtlinien](../../profile/api/merge-policies.md).

Eine Segmentdefinition wird für die Edge-Segmentierung in den folgenden Szenarien **nicht** aktiviert:

- Die Segmentdefinition umfasst eine Kombination aus einem einzelnen Ereignis und einem `inSegment`-Ereignis.
   - Wenn es sich bei dem im `inSegment`-Ereignis enthaltenen Segment jedoch nur um ein Profil handelt, **wird** die Segmentdefinition für die Edge-Segmentierung aktiviert.
- Die Segmentdefinition verwendet „Jahr ignorieren“ als Teil ihrer Zeitbeschränkungen.

## Abrufen aller für die Edge-Segmentierung aktivierten Segmente

Sie können eine Liste aller Segmente abrufen, die für die Edge-Segmentierung in Ihrem Unternehmen aktiviert sind, indem Sie eine GET-Anfrage an den `/segment/definitions`-Endpunkt stellen.

**API-Format**

Um Segmente abzurufen, die für die Edge-Segmentierung aktiviert sind, müssen Sie den Abfrageparameter `evaluationInfo.synchronous.enabled=true` in den Anfragepfad aufnehmen.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array von Segmenten in Ihrer Organisation zurück, die für die Edge-Segmentierung aktiviert sind. Detailliertere Informationen zur zurückgegebenen Segmentdefinition finden Sie im [Handbuch zum Segmentdefinitionenendpunkt](./segment-definitions.md).

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
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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

## Erstellen eines Segments, das für die Edge-Segmentierung aktiviert ist

Sie können ein Segment erstellen, das für die Edge-Segmentierung aktiviert ist, indem Sie eine POST-Anfrage an den `/segment/definitions`-Endpunkt stellen, der [einem der oben aufgeführten Abfragetypen für die Edge-Segmentierung entspricht](#query-types).

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

>[!NOTE]
>
>Das folgende Beispiel stellt eine Standardanfrage zum Erstellen eines Segments dar. Weiterführende Informationen zum Erstellen einer Segmentdefinition finden Sie im Tutorial zum [Erstellen von Segmenten](../tutorials/create-a-segment.md).

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
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    }
}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Details der neu erstellten Segmentdefinition zurückgegeben, die für die Edge-Segmentierung aktiviert ist.

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
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie Segmente mit aktivierter Edge-Segmentierung erstellen, können Sie sie verwenden, um Anwendungsfälle für die Personalisierung der gleichen Seite und der nächsten Seite zu ermöglichen.

Weiterführende Informationen zum Durchführen ähnlicher Aktionen und zum Verwenden von Segmenten unter Einsatz der Benutzeroberfläche von Adobe Experience Platform finden Sie im [Segment Builder-Benutzerhandbuch](../ui/segment-builder.md).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zur Edge-Segmentierung:

### Wie lange dauert es, bis ein Segment im Edge Network verfügbar ist?

Es dauert bis zu einer Stunde, bis ein Segment im Edge Network verfügbar ist.
