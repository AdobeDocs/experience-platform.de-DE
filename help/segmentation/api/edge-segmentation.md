---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; Kantensegmentierung; Edge-Segmentierung; Streaming-Edge
solution: Experience Platform
title: 'Edge-Segmentierung mithilfe der API '
topic-legacy: developer guide
description: Dieses Dokument enthält Beispiele für die Verwendung der Kantensegmentierung mit der Adobe Experience Platform Segmentation Service-API.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 3de00fb9ae5348b129a499cfd81d8db6dbac2d46
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 17%

---

# Edge-Segmentierung (Beta)

>[!NOTE]
>
>Im folgenden Dokument erfahren Sie, wie Sie die Kantensegmentierung mithilfe der API durchführen. Informationen zur Kantensegmentierung mithilfe der Benutzeroberfläche finden Sie im [UI-Handbuch zur Kantensegmentierung](../ui/edge-segmentation.md). Darüber hinaus befindet sich die Kantensegmentierung derzeit in der Betaphase. Die Dokumentation und Funktionalität können sich ändern.

Bei der Edge-Segmentierung können Segmente in Adobe Experience Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

## Erste Schritte

Dieses Entwicklerhandbuch setzt ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste voraus, die mit der Kantensegmentierung verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Verbraucherprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Segmentation]](../home.md): Ermöglicht die Erstellung von Segmenten und Zielgruppen aus Ihren  [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Lesen Sie für erfolgreiche Aufrufe an [!DNL Data Prep]-API-Endpunkte das Handbuch für [Erste Schritte mit Platform-APIs](../../landing/api-guide.md), um mehr über erforderliche Kopfzeilen und Beispiele für API-Aufrufe zu erfahren.

## Kantensegmentierungs-Abfragetypen {#query-types}

Damit ein Segment mithilfe der Kantensegmentierung bewertet werden kann, muss die Abfrage den folgenden Richtlinien entsprechen:

| Abfragetyp | Details |
| ---------- | ------- |
| Eingehender Treffer | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. |
| Eingehender Treffer, der sich auf ein Profil bezieht | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profilattribute verweist. |
| Frequenzabfrage | Jede Segmentdefinition, die auf ein Ereignis verweist, das mindestens eine bestimmte Anzahl von Malen stattfindet. |
| Frequenzabfrage, die sich auf ein Profil bezieht | Jede Segmentdefinition, die auf ein Ereignis verweist, das mindestens eine bestimmte Anzahl von Malen stattfindet und mindestens ein Profilattribut aufweist. |

{style=&quot;table-layout:auto&quot;}

Die folgenden Abfragetypen werden derzeit von der Kantensegmentierung unterstützt: **nicht**:

| Abfragetyp | Details |
| ---------- | ------- |
| Relatives Zeitfenster | Wenn sich eine Abfrage auf ein Zeitfenster bezieht, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |
| Negation | Wenn eine Abfrage eine Negation oder ein `not` -Ereignis enthält, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |
| Mehrere Ereignisse | Wenn eine Abfrage mehr als ein Ereignis enthält, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |

{style=&quot;table-layout:auto&quot;}

## Alle für die Kantensegmentierung aktivierten Segmente abrufen

Sie können eine Liste aller Segmente abrufen, die für die Kantensegmentierung in Ihrer IMS-Organisation aktiviert sind, indem Sie eine GET-Anfrage an den Endpunkt `/segment/definitions` stellen.

**API-Format**

Um für die Kantensegmentierung aktivierte Segmente abzurufen, müssen Sie den Abfrageparameter `evaluationInfo.synchronous.enabled=true` in den Anfragepfad einbeziehen.

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

Eine erfolgreiche Antwort gibt eine Reihe von Segmenten in Ihrer IMS-Organisation zurück, die für die Kantensegmentierung aktiviert sind. Detailliertere Informationen zur zurückgegebenen Segmentdefinition finden Sie im [Endpunktleitfaden für Segmentdefinitionen](./segment-definitions.md).

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

## Erstellen eines Segments, das für die Kantensegmentierung aktiviert ist

Sie können ein Segment erstellen, das für die Kantensegmentierung aktiviert ist, indem Sie eine POST-Anfrage an den Endpunkt `/segment/definitions` stellen, der mit einem der oben aufgeführten [Kantensegmentierungs-Abfragetypen](#query-types) übereinstimmt.

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

>[!NOTE]
>
>Das folgende Beispiel stellt eine Standardanfrage zum Erstellen eines Segments dar. Weitere Informationen zum Erstellen einer Segmentdefinition finden Sie im Tutorial zum Erstellen eines Segments](../tutorials/create-a-segment.md).[

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

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Segmentdefinition zurück, die für die Kantensegmentierung aktiviert ist.

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

Nachdem Sie nun wissen, wie Sie Segmente mit aktivierter Kantensegmentierung erstellen, können Sie sie verwenden, um Anwendungsfälle für die Personalisierung von derselben Seite und nächsten Seiten zu aktivieren.

Weiterführende Informationen zum Durchführen ähnlicher Aktionen und zum Verwenden von Segmenten unter Einsatz der Benutzeroberfläche von Adobe Experience Platform finden Sie im [Segment Builder-Benutzerhandbuch](../ui/segment-builder.md).
