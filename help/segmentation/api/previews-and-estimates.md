---
solution: Experience Platform
title: API-Endpunkte für Vorschauen und Schätzungen
description: Bei der Entwicklung der Segmentdefinition können Sie die Tools Schätzung und Vorschau in Adobe Experience Platform verwenden, um Informationen auf Zusammenfassungsebene anzuzeigen und so sicherzustellen, dass Sie die erwartete Zielgruppe isolieren.
role: Developer
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: a374d261e3b34b30869f1a9e8486d52f5bd658cb
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 11%

---

# Vorschau und Schätzungen von Endpunkten

Bei der Entwicklung einer Segmentdefinition können Sie die Tools Schätzung und Vorschau in Adobe Experience Platform verwenden, um Informationen auf Zusammenfassungsebene anzuzeigen und so sicherzustellen, dass Sie die erwartete Zielgruppe isolieren.

* **Vorschauen** stellen paginierte Listen von qualifizierten Profilen für eine Segmentdefinition bereit, sodass Sie die Ergebnisse mit dem vergleichen können, was Sie erwarten.

* **Schätzungen** liefern statistische Informationen über eine Segmentdefinition, z. B. die projizierte Zielgruppengröße, das Konfidenzintervall und die Standardabweichung von Fehlern.

>[!NOTE]
>
>Informationen zum Zugriff auf ähnliche Metriken in Bezug auf Echtzeit-Kundenprofildaten, wie z. B. die Gesamtzahl der Profilfragmente und zusammengeführten Profile innerhalb bestimmter Namespaces oder den Profildatenspeicher als Ganzes, finden Sie im [Handbuch zum Profilvorschau-Endpunkt (Vorschaubeispielstatus)](../../profile/api/preview-sample-status.md), Teil des Entwicklerhandbuchs zur Profil-API.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-API. Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderlichen Kopfzeilen sowie Beispiele für API-Aufrufe lesen können.

## So werden Schätzungen generiert

Wenn die Aufnahme von Datensätzen in den Profilspeicher die Gesamtprofilanzahl um mehr als 3 % erhöht oder verringert, wird ein Sampling-Auftrag ausgelöst, um die Anzahl zu aktualisieren. Die Art und Weise, wie das Daten-Sampling ausgelöst wird, hängt von der Methode der Aufnahme ab:

* **Batch-Aufnahme:** Bei der Batch-Aufnahme innerhalb von 15 Minuten nach der erfolgreichen Aufnahme eines Batches in den Profilspeicher wird ein Auftrag ausgeführt, um die Anzahl zu aktualisieren, wenn der Schwellenwert von 3 % für die Erhöhung oder Verringerung erreicht wird.
* **Streaming-Aufnahme:** Bei Streaming-Daten-Workflows wird stündlich überprüft, ob der Schwellenwert von 3 % für die Erhöhung oder Verringerung erreicht wurde. Ist dies der Fall, wird automatisch ein Vorgang ausgelöst, um die Anzahl zu aktualisieren.

Die Stichprobengröße der Überprüfung hängt von der Gesamtzahl der Entitäten in Ihrem Profilspeicher ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profilspeicher | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Millionen | 1 Million |
| Über 20 Millionen | 5 % der Gesamtgröße |

>[!NOTE]
>
>Die Ausführung von Schätzungen dauert im Allgemeinen 10 bis 15 Sekunden, beginnend mit einer groben Schätzung und Verfeinerung, wenn mehr Datensätze gelesen werden.

## Erstellen einer neuen Vorschau {#create-preview}

Sie können eine neue Vorschau erstellen, indem Sie eine POST-Anfrage an den `/preview`-Endpunkt senden.

>[!NOTE]
>
>Ein Vorkalkulationsauftrag wird automatisch erstellt, wenn ein Vorschauauftrag erstellt wird. Diese beiden Vorgänge verwenden dieselbe ID.

**API-Format**

```http
POST /preview
```

**Anfrage**

+++ Beispielanfrage zum Erstellen einer Vorschau.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `predicateExpression` | Der PQL-Ausdruck, nach dem die Daten abgefragt werden. |
| `predicateType` | Der Prädikattyp für den Abfrageausdruck unter `predicateExpression`. Derzeit ist der einzige akzeptierte Wert für diese Eigenschaft `pql/text`. |
| `predicateModel` | Der Name der [!DNL Experience Data Model] (XDM)-Schemaklasse, auf der die Profildaten basieren. |
| `graphType` | Der Diagrammtyp, von dem Sie den Cluster abrufen möchten. Die unterstützten Werte sind `none` (führt keine Identitätszuordnung durch) und `pdg` (führt eine Identitätszuordnung basierend auf Ihrem privaten Identitätsdiagramm durch). |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 201 (Erstellt) mit Details zur neu erstellten Vorschau zurückgegeben.

+++ Eine Beispielantwort beim Erstellen einer Vorschau.

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `state` | Der aktuelle Status des Vorschauauftrags. Nach der erstmaligen Erstellung weist es den Status „NEU“ auf. Anschließend wird der Status „WIRD AUSGEFÜHRT“ angezeigt, bis die Verarbeitung abgeschlossen ist. Danach wird sie zu „RESULT_READY“ oder „FAILED“. |
| `previewId` | Die ID des Vorschauauftrags, der zu Suchzwecken beim Anzeigen einer Schätzung oder Vorschau verwendet werden soll, wie im nächsten Abschnitt beschrieben. |

+++

## Abrufen der Ergebnisse einer bestimmten Vorschau {#get-preview}

Sie können detaillierte Informationen zu einer bestimmten Vorschau abrufen, indem Sie eine GET-Anfrage an den `/preview`-Endpunkt senden und die Vorschau-ID im Anfragepfad angeben.

**API-Format**

```http
GET /preview/{PREVIEW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{PREVIEW_ID}` | Der `previewId` der Vorschau, die Sie abrufen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Abrufen einer Vorschau.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

+++ Eine Beispielantwort beim Abrufen einer Vorschau.

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit detaillierten Informationen zur angegebenen Vorschau zurück.

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `results` | Eine Liste der Entitäts-IDs zusammen mit den zugehörigen Identitäten. Die bereitgestellten Links können mithilfe des Profilzugriffs-API[Endpunkts zum Nachschlagen der angegebenen Entitäten &#x200B;](../../profile/api/entities.md). |

+++

## Abrufen der Ergebnisse eines bestimmten Schätzauftrags {#get-estimate}

Nachdem Sie einen Vorschauauftrag erstellt haben, können Sie dessen `previewId` im Pfad einer GET-Anfrage an den `/estimate`-Endpunkt verwenden, um statistische Informationen zur Segmentdefinition anzuzeigen, einschließlich der projizierten Zielgruppengröße, des Konfidenzintervalls und der Standardabweichung von Fehlern.

**API-Format**

```http
GET /estimate/{PREVIEW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{PREVIEW_ID}` | Ein Vorkalkulationsauftrag wird nur ausgelöst, wenn ein Vorschauauftrag erstellt wird und die beiden Aufträge denselben ID-Wert für Suchzwecke verwenden. Dies ist insbesondere der `previewId` Wert, der bei der Erstellung des Vorschauauftrags zurückgegeben wurde. |

**Anfrage**

Die folgende Anfrage ruft die Ergebnisse eines bestimmten Schätzauftrags ab.

+++ Eine Beispielanfrage zum Abrufen eines geschätzten Auftrags.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zum Schätzauftrag zurück.

+++ Beispielantwort beim Abrufen eines geschätzten Auftrags.

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | Ein Array von Objekten, das die Anzahl der Profile in der Segmentdefinition aufgeschlüsselt nach Identity-Namespace anzeigt. Die Gesamtzahl der Profile nach Namespace (die Summe der für jeden Namespace angezeigten Werte) kann höher sein als die Profilzählungsmetrik, da ein Profil mit mehreren Namespaces verknüpft sein kann. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet. |
| `state` | Der aktuelle Status des Vorschauauftrags. Der Status ist „WIRD AUSGEFÜHRT“, bis die Verarbeitung abgeschlossen ist. Ab diesem Zeitpunkt ist er „RESULT_READY“ oder „FAILED“. |
| `_links.preview` | Wenn die `state` „RESULT_READY“ lautet, stellt dieses Feld eine URL zum Anzeigen der Schätzung bereit. |

+++

## Nächste Schritte

Nach dem Lesen dieses Handbuchs sollten Sie ein besseres Verständnis davon haben, wie Sie mit Vorschauen und Schätzungen mithilfe der Segmentierungs-API arbeiten. Informationen zum Zugriff auf Metriken, die sich auf Ihre Echtzeit-Kundenprofildaten beziehen, z. B. die Gesamtzahl der Profilfragmente und zusammengeführten Profile innerhalb bestimmter Namespaces oder den Profildatenspeicher als Ganzes, finden Sie im [Handbuch zum Profilvorschau-Endpunkt (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).
