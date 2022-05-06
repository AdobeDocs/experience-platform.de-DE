---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; Kantensegmentierung; Edge-Segmentierung; Streaming-Edge
solution: Experience Platform
title: 'Edge-Segmentierung mithilfe der API '
topic-legacy: developer guide
description: Dieses Dokument enthält Beispiele für die Verwendung der Kantensegmentierung mit der Adobe Experience Platform Segmentation Service-API.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 6%

---

# Edge-Segmentierung

>[!NOTE]
>
>Im folgenden Dokument erfahren Sie, wie Sie die Kantensegmentierung mithilfe der API durchführen. Informationen zur Kantensegmentierung mithilfe der Benutzeroberfläche finden Sie im Abschnitt [Handbuch zur Edge-Segmentierungsbenutzeroberfläche](../ui/edge-segmentation.md).
>
>Die Edge-Segmentierung ist jetzt allgemein für alle Platform-Benutzer verfügbar. Wenn Sie während der Beta-Phase Kantensegmente erstellt haben, sind diese Segmente weiterhin funktionsfähig.

Bei der Edge-Segmentierung können Segmente in Adobe Experience Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

>[!IMPORTANT]
>
> Die Edge-Daten werden an einem Edge-Server-Speicherort gespeichert, der am nächsten zum Erfassungsort liegt, und können an einem anderen Speicherort als dem als Hub (oder Prinzipal) für das Adobe Experience Platform-Rechenzentrum bezeichnet werden.
>
> Darüber hinaus berücksichtigt die Edge-Segmentierungsmodul nur Anforderungen an den Edge, an dem **one** mit Primärkennzeichnung versehene Identität, die mit nicht Edge-basierten primären Identitäten konsistent ist.

## Erste Schritte

Dieses Entwicklerhandbuch setzt ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die mit der Kantensegmentierung verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Verbraucherprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Segmentation]](../home.md): Ermöglicht die Erstellung von Segmenten und Zielgruppen aus Ihren [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.

Informationen zum erfolgreichen Aufrufen von Experience Platform-API-Endpunkten finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../landing/api-guide.md) , um mehr über erforderliche Kopfzeilen und das Lesen von Beispiel-API-Aufrufen zu erfahren.

## Kantensegmentierungs-Abfragetypen {#query-types}

Damit ein Segment mithilfe der Kantensegmentierung bewertet werden kann, muss die Abfrage den folgenden Richtlinien entsprechen:

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Einzelereignis | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | Personen, die einen Artikel zum Warenkorb hinzugefügt haben. |
| Einzelereignis, das ein Profil referenziert | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | Personen, die in den USA leben und die Homepage besucht haben. |
| Negatives einzelnes Ereignis mit einem Profilattribut | Jede Segmentdefinition, die auf ein negatives eingehendes Ereignis und ein oder mehrere Profilattribute verweist. | Menschen, die in den USA leben und **not** besuchte die Homepage. |
| Einzelereignisse innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis innerhalb von 24 Stunden verweist. | Personen, die die Homepage in den letzten 24 Stunden besucht haben. |
| Einzelnes Ereignis mit einem Profilattribut innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und ein einziges eingehendes Ereignis innerhalb von 24 Stunden verweist. | Personen, die in den USA leben und die die Homepage in den letzten 24 Stunden besucht haben. |
| Vernachlässigtes einzelnes Ereignis mit einem Profilattribut innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und ein negiertes eingehendes Ereignis innerhalb von 24 Stunden verweist. | Menschen, die in den USA leben und **not** die Homepage in den letzten 24 Stunden besucht haben. |
| Frequenzereignis innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die auf ein Ereignis verweist, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Malen stattfindet. | Besucher der Homepage **mindestens** fünf Mal in den letzten 24 Stunden. |
| Häufigkeitsereignis mit einem Profilattribut innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die sich auf ein oder mehrere Profilattribute und ein Ereignis bezieht, die innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Malen stattfinden. | Personen aus den USA, die die Homepage besucht haben **mindestens** fünf Mal in den letzten 24 Stunden. |
| Umgekehrtes Frequenzereignis mit einem Profil innerhalb eines Zeitfensters von 24 Stunden | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und ein negiertes Ereignis verweist, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Malen stattfindet. | Personen, die die Homepage nicht besucht haben **more** in den letzten 24 Stunden mehr als fünfmal. |
| Mehrere eingehende Treffer innerhalb eines Zeitprofils von 24 Stunden | Jede Segmentdefinition, die auf mehrere Ereignisse verweist, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen, die die Homepage besucht haben **oder** die Checkout-Seite innerhalb der letzten 24 Stunden besucht haben. |
| Mehrere Ereignisse mit einem Profil innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und mehrere Ereignisse verweist, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen aus den USA, die die Homepage besucht haben **und** die Checkout-Seite innerhalb der letzten 24 Stunden besucht haben. |

Zusätzlich wird das Segment **must** an eine Zusammenführungsrichtlinie gebunden sein, die an der Kante aktiv ist. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im Abschnitt [Leitfaden zu Zusammenführungsrichtlinien](../../profile/api/merge-policies.md).

## Alle für die Kantensegmentierung aktivierten Segmente abrufen

Sie können eine Liste aller Segmente abrufen, die für die Kantensegmentierung in Ihrer IMS-Organisation aktiviert sind, indem Sie eine GET-Anfrage an die `/segment/definitions` -Endpunkt.

**API-Format**

Um Segmente abzurufen, die für die Kantensegmentierung aktiviert sind, müssen Sie den Abfrageparameter einbeziehen `evaluationInfo.synchronous.enabled=true` im Anfragepfad.

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

Eine erfolgreiche Antwort gibt eine Reihe von Segmenten in Ihrer IMS-Organisation zurück, die für die Kantensegmentierung aktiviert sind. Detailliertere Informationen zur zurückgegebenen Segmentdefinition finden Sie im Abschnitt [Endleitfaden für Segmentdefinitionen](./segment-definitions.md).

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

## Erstellen eines Segments, das für die Kantensegmentierung aktiviert ist

Sie können ein Segment erstellen, das für die Kantensegmentierung aktiviert ist, indem Sie eine POST-Anfrage an die `/segment/definitions` -Endpunkt, der mit einem der [oben aufgeführte Kantensegmentierungs-Abfragetypen](#query-types).

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

>[!NOTE]
>
>Das folgende Beispiel stellt eine Standardanfrage zum Erstellen eines Segments dar. Weitere Informationen zum Erstellen einer Segmentdefinition finden Sie im Tutorial zu [Erstellen eines Segments](../tutorials/create-a-segment.md).

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

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Segmentdefinition zurück, die für die Kantensegmentierung aktiviert ist.

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

Nachdem Sie nun wissen, wie Sie Segmente mit aktivierter Kantensegmentierung erstellen, können Sie sie verwenden, um Anwendungsfälle für die Personalisierung von derselben Seite und nächsten Seiten zu aktivieren.

Weiterführende Informationen zum Durchführen ähnlicher Aktionen und zum Verwenden von Segmenten unter Einsatz der Benutzeroberfläche von Adobe Experience Platform finden Sie im [Segment Builder-Benutzerhandbuch](../ui/segment-builder.md).
