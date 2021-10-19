---
keywords: Experience Platform;home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;Kantensegmentierung;Kantensegmentierung;Streaming-Kante;
solution: Experience Platform
title: 'Edge-Segmentierung mit der API '
topic-legacy: developer guide
description: Dieses Dokument enthält Beispiele für die Verwendung der Kantensegmentierung mit der Adobe Experience Platform Segmentation Service API.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: c89971668839555347e9b84c7c0a4ff54a394c1a
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 8%

---

# Kantensegmentierung (Beta)

>[!NOTE]
>
>Im folgenden Dokument wird erläutert, wie die Kantensegmentierung mithilfe der API durchgeführt wird. Informationen zur Kantensegmentierung mithilfe der Benutzeroberfläche finden Sie in der [Hilfslinie für die Benutzeroberfläche für Kantensegmentierung](../ui/edge-segmentation.md). Außerdem befindet sich die Edge-Segmentierung derzeit in der Beta-Phase. Die Dokumentation und Funktionalität können sich ändern.

Mit der Edge-Segmentierung können Segmente in Adobe Experience Platform unmittelbar am Rand ausgewertet werden, sodass dieselben Anwendungsfälle für die Personalisierung der Seite und der nächsten Seite möglich sind.

## Erste Schritte

Dieses Entwicklerleitfaden erfordert ein Arbeitsverständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die mit der Segmentierung von Kanten verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein vereinheitlichtes Konsumentenkennwort in Echtzeit, basierend auf aggregierten Daten aus mehreren Quellen.
- [[!DNL Segmentation]](../home.md): Ermöglicht das Erstellen von Segmenten und Audiencen aus Ihren [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Lesen Sie das Handbuch, um erfolgreich Aufrufe von API-Endpunkten der Experience Platform zu ermöglichen unter [Erste Schritte mit Plattform-APIs](../../landing/api-guide.md) um sich über erforderliche Kopfzeilen und das Lesen von Beispiel-API-Aufrufen zu informieren.

## Abfrage der Kantensegmentierung {#query-types}

Damit ein Segment mithilfe der Kantensegmentierung bewertet werden kann, muss die Abfrage den folgenden Richtlinien entsprechen:

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Einzelnes Ereignis | Eine Segmentdefinition, die sich auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung bezieht. | Personen, die dem Warenkorb ein Artikel hinzugefügt haben. |
| Einzelnes Ereignis, das sich auf ein Profil bezieht | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und ein einzelnes ankommendes Ereignis ohne Zeitbeschränkung bezieht. | Personen, die in den USA leben und die Homepage besucht haben. |
| Negatives einzelnes Ereignis mit einem Profil-Attribut | Eine Segmentdefinition, die sich auf ein negatives eintreffendes Ereignis und ein oder mehrere Profil-Attribute bezieht | Menschen, die in den USA leben und **nicht** besuchte die Homepage. |
| Einzelnes Ereignis innerhalb eines 24-Stunden-Fensters | Eine Segmentdefinition, die sich auf ein einzelnes ankommendes Ereignis innerhalb von 24 Stunden bezieht. | Personen, die die Homepage in den letzten 24 Stunden besucht haben. |
| Einzelnes Ereignis mit einem Profil-Attribut und einem 24-Stunden-Zeitfenster | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und ein negiertes einzelnes ankommendes Ereignis innerhalb von 24 Stunden bezieht. | Personen, die in den USA leben und die Homepage in den letzten 24 Stunden besucht haben. |
| Negiertes einzelnes Ereignis mit einem Profil-Attribut innerhalb eines 24-Stunden-Fensters | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und ein negiertes einzelnes ankommendes Ereignis innerhalb von 24 Stunden bezieht. | Menschen, die in den USA leben und **nicht** besuchte die Homepage in den letzten 24 Stunden. |
| Häufigkeitsangaben innerhalb eines 24-Stunden-Ereignisses | Eine Segmentdefinition, die sich auf ein Ereignis bezieht, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Ereignissen aufweist. | Personen, die die Homepage besucht haben **mindestens** fünf Mal in den letzten 24 Stunden. |
| Ereignis der Häufigkeit mit einem Profil-Attribut innerhalb eines 24-Stunden-Fensters | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute bezieht und ein Ereignis, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Ereignissen aufnimmt. | Personen aus den USA, die die Homepage besucht haben **mindestens** fünf Mal in den letzten 24 Stunden. |
| Negatives Frequenzfenster mit einem Profil innerhalb eines 24-Stunden-Ereignisses | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und ein negiertes Ereignis bezieht, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Ereignissen aufnimmt. | Personen, die die Startseite nicht besucht haben **mehr** in den letzten 24 Stunden mehr als fünf Mal. |
| Mehrere eingehende Treffer innerhalb eines Profils von 24 Stunden | Eine Segmentdefinition, die sich auf mehrere Ereignis bezieht, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen, die die Homepage besucht haben **oder** hat die Checkout-Seite innerhalb der letzten 24 Stunden besucht. |
| Mehrere Ereignisse mit einem Profil innerhalb eines 24-Stunden-Fensters | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und mehrere Ereignis bezieht, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen aus den USA, die die Homepage besucht haben **und** hat die Checkout-Seite innerhalb der letzten 24 Stunden besucht. |

{style=&quot;table-layout:auto&quot;}

## Alle Segmente abrufen, die für die Kantensegmentierung aktiviert sind

Sie können eine Liste aller Segmente abrufen, die für die Kantensegmentierung in Ihrer IMS-Organisation aktiviert sind, indem Sie eine GET an die `/segment/definitions` Endpunkt.

**API-Format**

Um Segmente abzurufen, die für die Kantensegmentierung aktiviert sind, müssen Sie den Parameter &quot;Abfrage&quot;angeben. `evaluationInfo.synchronous.enabled=true` im Anforderungspfad.

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

Eine erfolgreiche Antwort gibt eine Reihe von Segmenten in Ihrer IMS-Organisation zurück, die für die Kantensegmentierung aktiviert sind. Ausführlichere Informationen zur zurückgegebenen Segmentdefinition finden Sie im [Endpunkt für Segmentdefinitionen](./segment-definitions.md).

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

## Segment erstellen, das für die Kantensegmentierung aktiviert ist

Sie können ein Segment erstellen, das für die Kantensegmentierung aktiviert ist, indem Sie eine POST an die `/segment/definitions` Endpunkt, der mit einem der [oben aufgeführte Abfragen zur Segmentierung von Kanten](#query-types).

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

>[!NOTE]
>
>Das Beispiel unten ist eine Standardanforderung zum Erstellen eines Segments. Weitere Informationen zum Erstellen einer Segmentdefinition finden Sie im Tutorial unter [ein Segment erstellen](../tutorials/create-a-segment.md).

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

Da Sie nun wissen, wie Sie Segmente mit aktivierter Kantensegmentierung erstellen, können Sie diese verwenden, um Anwendungsfälle für die Personalisierung derselben Seite und nächster Seite zu aktivieren.

Weiterführende Informationen zum Durchführen ähnlicher Aktionen und zum Verwenden von Segmenten unter Einsatz der Benutzeroberfläche von Adobe Experience Platform finden Sie im [Segment Builder-Benutzerhandbuch](../ui/segment-builder.md).
