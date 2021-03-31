---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;Kantensegmentierung;Kantensegmentierung;Streaming-Kante;
solution: Experience Platform
title: 'Edge-Segmentierung mit der API '
topic: Entwicklerhandbuch
description: Dieses Dokument enthält Beispiele zur Verwendung der Segmentierung mit der Adobe Experience Platform Segmentation Service API.
translation-type: tm+mt
source-git-commit: 0c4625ec0728c8c94b72e3e16e7ecf45ea2d0c0b
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 10%

---


# Kantensegmentierung

>[!NOTE]
>
>Im folgenden Dokument wird erläutert, wie die Segmentierung von Kanten mithilfe der API durchgeführt wird. Informationen zur Kantensegmentierung mithilfe der Benutzeroberfläche finden Sie im Handbuch [Edge Segmentation UI guide](../ui/edge-segmentation.md).

Bei der Edge-Segmentierung können Segmente in Adobe Experience Platform sofort am Rand ausgewertet werden, sodass dieselben Anwendungsfälle für die Personalisierung der Seite und der nächsten Seite möglich sind.

## Erste Schritte

Dieses Entwicklerhandbuch erfordert ein funktionierendes Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste, die mit der Segmentierung von Kanten verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Verbraucherdatenquellen-Profil in Echtzeit, basierend auf aggregierten Daten aus mehreren Quellen.
- [[!DNL Segmentation]](../home.md): Ermöglicht das Erstellen von Segmenten und Audiencen aus Ihren  [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Um erfolgreich Aufrufe an API-Endpunkte durchzuführen, lesen Sie bitte das Handbuch [Erste Schritte mit Plattform-APIs](../../landing/api-guide.md), um mehr über erforderliche Kopfzeilen und das Lesen von Beispiel-API-Aufrufen zu erfahren.[!DNL Data Prep]

## Edge Segmentation Abfrage Types {#query-types}

Damit ein Segment mithilfe der Kantensegmentierung bewertet werden kann, muss die Abfrage den folgenden Richtlinien entsprechen:

| Abfragetyp | Details |
| ---------- | ------- |
| Eingehender Treffer | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. |
| Eingehender Treffer, der sich auf ein Profil bezieht | Eine Segmentdefinition, die sich auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profil-Attribute bezieht. |
| Häufigkeitsangaben Abfrage | Eine Segmentdefinition, die auf ein Ereignis verweist, das eine bestimmte Anzahl von Malen ausgeführt wird. |
| Abfrage der Häufigkeit, die auf ein Profil verweist | Eine Segmentdefinition, die sich auf ein Ereignis bezieht, das eine bestimmte Anzahl von Malen passiert und eines oder mehrere Profil-Attribute aufweist. |

{style=&quot;table-layout:auto&quot;}

Die folgenden Abfragen werden derzeit von der Kantensegmentierung unterstützt: **not**:

| Abfragetyp | Details |
| ---------- | ------- |
| Relatives Zeitfenster | Wenn sich eine Abfrage auf ein Zeitfenster bezieht, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |
| Negation | Wenn eine Abfrage eine Negation oder ein `not`-Ereignis enthält, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |
| Mehrere Ereignisse | Wenn eine Abfrage mehr als ein Ereignis enthält, kann sie nicht mithilfe der Kantensegmentierung bewertet werden. |

{style=&quot;table-layout:auto&quot;}

## Rufen Sie alle Segmente ab, die für die Kantensegmentierung aktiviert sind.

Sie können eine Liste aller Segmente abrufen, die in Ihrer IMS-Organisation für die Kantensegmentierung aktiviert sind, indem Sie eine GET an den `/segment/definitions`-Endpunkt anfordern.

**API-Format**

Um Segmente abzurufen, die für die Segmentierung der Kante aktiviert sind, müssen Sie den Parameter &quot;Abfrage&quot;`evaluationInfo.synchronous.enabled=true` in den Anforderungspfad einbeziehen.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird ein Array von Segmenten in Ihrer IMS-Organisation zurückgegeben, die für die Segmentierung der Kante aktiviert sind. Detailliertere Informationen zur zurückgegebenen Segmentdefinition finden Sie im Endpunktleitfaden [Segmentdefinitionen](./segment-definitions.md).

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

## Erstellen Sie ein Segment, das für die Segmentierung der Edge aktiviert ist.

Sie können ein Segment erstellen, das für die Kantensegmentierung aktiviert ist, indem Sie eine POST an den `/segment/definitions`-Endpunkt anfordern. Zusätzlich zu den oben aufgeführten Segmentierungstypen [der Kantensegmentierung müssen Sie das `evaluationInfo.synchronous.enabled`-Flag in der Nutzlast auf true setzen.](#query-types)

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

>[!NOTE]
>
>Das unten stehende Beispiel ist eine Standardanforderung zum Erstellen eines Segments. Weitere Informationen zum Erstellen einer Segmentdefinition finden Sie im Tutorial [Erstellen eines Segments](../tutorials/create-a-segment.md).

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
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | Das `evaluationInfo`-Objekt bestimmt den Typ der Bewertung, der die Segmentdefinition unterzogen wird. Um die Kantensegmentierung zu verwenden, setzen Sie `evaluationInfo.synchronous.enabled` mit dem Wert `true`. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Segmentdefinition zurück, die für die Segmentierung der Kante aktiviert ist.

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

Nachdem Sie wissen, wie Sie Segmente mit aktivierter Kantensegmentierung erstellen, können Sie diese verwenden, um Anwendungsfälle für die Personalisierung auf derselben Seite und auf der nächsten Seite zu aktivieren.

Weiterführende Informationen zum Durchführen ähnlicher Aktionen und zum Verwenden von Segmenten unter Einsatz der Benutzeroberfläche von Adobe Experience Platform finden Sie im [Segment Builder-Benutzerhandbuch](../ui/segment-builder.md).