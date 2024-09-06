---
solution: Experience Platform
title: Vorschau und Schätzung von API-Endpunkten
description: Bei der Entwicklung der Segmentdefinition können Sie die Schätzungs- und Vorschau-Tools in Adobe Experience Platform verwenden, um Informationen auf Zusammenfassungsebene anzuzeigen und so sicherzustellen, dass Sie die erwartete Zielgruppe isolieren.
role: Developer
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 11%

---

# Vorschau- und Schätzendpunkte

Bei der Entwicklung einer Segmentdefinition können Sie die Schätzungs- und Vorschau-Tools in Adobe Experience Platform verwenden, um Informationen auf Zusammenfassungsebene anzuzeigen und so sicherzustellen, dass Sie die erwartete Zielgruppe isolieren.

* **Vorschau** bietet paginierte Listen mit qualifizierten Profilen für eine Segmentdefinition, sodass Sie die Ergebnisse mit dem vergleichen können, was Sie erwarten.

* **Schätzungen** liefern statistische Informationen zu einer Segmentdefinition, z. B. die projizierte Zielgruppengröße, das Konfidenzintervall und die Standardabweichung von Fehlern.

>[!NOTE]
>
>Weitere Informationen zum Zugriff auf ähnliche Metriken im Zusammenhang mit Echtzeit-Kundenprofildaten, wie die Gesamtzahl der Profilfragmente und zusammengeführten Profile in bestimmten Namespaces oder den Profildatenspeicher als Ganzes, finden Sie im Endpunkthandbuch für die [Profilvorschau (Beispielvorschau)](../../profile/api/preview-sample-status.md), Teil des Entwicklerhandbuchs zur Profil-API.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service] -API. Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Anweisungen zum Lesen von Beispiel-API-Aufrufen.

## Erstellung von Schätzungen

Wenn die Aufnahme von Datensätzen in den Profilspeicher die Gesamtzahl der Profile um mehr als 5 % erhöht oder verringert, wird ein Sampling-Auftrag ausgelöst, um die Anzahl zu aktualisieren. Die Art und Weise, wie das Sampling von Daten ausgelöst wird, hängt von der Erfassungsmethode ab:

* **Batch-Erfassung:** Bei der Batch-Erfassung wird innerhalb von 15 Minuten nach erfolgreicher Aufnahme eines Batches in den Profilspeicher ein Auftrag ausgeführt, um die Anzahl zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht ist.
* **Streaming-Erfassung:** Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für eine Zu- oder Abnahme um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Anzahl zu aktualisieren.

Die Stichprobengröße der Prüfung hängt von der Gesamtanzahl der Entitäten in Ihrem Profilspeicher ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profilspeicher | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Millionen | 1 Million |
| Über 20 Millionen | 5 % der Gesamtgröße |

>[!NOTE]
>
>Die Ausführung von Schätzungen dauert in der Regel 10 bis 15 Sekunden, beginnend mit einer groben Schätzung und einer Verfeinerung, da mehr Datensätze gelesen werden.

## Neue Vorschau erstellen {#create-preview}

Sie können eine neue Vorschau erstellen, indem Sie eine POST-Anfrage an den `/preview` -Endpunkt senden.

>[!NOTE]
>
>Beim Erstellen eines Vorschauauftrags wird automatisch ein Schätzauftrag erstellt. Diese beiden Aufträge verwenden dieselbe ID.

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
| `predicateType` | Der Prädikatyp für den Abfrageausdruck unter `predicateExpression`. Derzeit ist der einzige akzeptierte Wert für diese Eigenschaft `pql/text`. |
| `predicateModel` | Der Name der Schemaklasse [!DNL Experience Data Model] (XDM), auf der die Profildaten basieren. |
| `graphType` | Der Diagrammtyp, aus dem Sie den Cluster abrufen möchten. Die unterstützten Werte sind &quot;`none`&quot;(keine Identitätszusammenfügung) und &quot;`pdg`&quot;(führt eine Identitätszusammenfügung basierend auf Ihrem privaten Identitätsdiagramm durch). |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) mit Details zur neu erstellten Vorschau zurück.

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
| `state` | Der aktuelle Status des Vorschauauftrags. Nach der anfänglichen Erstellung befindet er sich im Status &quot;NEU&quot;. Anschließend befindet er sich im Status &quot;WIRD AUSGEFÜHRT&quot;, bis die Verarbeitung abgeschlossen ist. Anschließend wird er zu &quot;RESULT_READY&quot;oder &quot;FEHLGESCHLAGEN&quot;. |
| `previewId` | Die ID des Vorschauauftrags, die für Nachschlagezwecke bei der Anzeige einer Schätzung oder Vorschau verwendet wird, wie im nächsten Abschnitt beschrieben. |

+++

## Ergebnisse einer bestimmten Vorschau abrufen {#get-preview}

Sie können detaillierte Informationen zu einer bestimmten Vorschau abrufen, indem Sie eine GET-Anfrage an den `/preview` -Endpunkt senden und im Anfragepfad die Vorschau-ID angeben.

**API-Format**

```http
GET /preview/{PREVIEW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{PREVIEW_ID}` | Der `previewId` -Wert der Vorschau, die Sie abrufen möchten. |

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Vorschau zurück.

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
| `results` | Eine Liste der Entitäts-IDs zusammen mit den zugehörigen Identitäten. Die bereitgestellten Links können verwendet werden, um die angegebenen Entitäten mithilfe des [API-Endpunkts für den Profilzugriff](../../profile/api/entities.md) nachzuschlagen. |

+++

## Abrufen der Ergebnisse eines bestimmten Schätzauftrags {#get-estimate}

Nachdem Sie einen Vorschauauftrag erstellt haben, können Sie dessen `previewId` im Pfad einer GET-Anfrage an den `/estimate` -Endpunkt verwenden, um statistische Informationen über die Segmentdefinition anzuzeigen, einschließlich der projizierten Zielgruppengröße, des Konfidenzintervalls und der Standardabweichung für Fehler.

**API-Format**

```http
GET /estimate/{PREVIEW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{PREVIEW_ID}` | Ein Schätzauftrag wird nur ausgelöst, wenn ein Vorschauauftrag erstellt wird und die beiden Aufträge denselben ID-Wert für Nachschlagezwecke nutzen. Dies ist insbesondere der `previewId` -Wert, der beim Erstellen des Vorschauauftrags zurückgegeben wird. |

**Anfrage**

Die folgende Anfrage ruft die Ergebnisse eines bestimmten Schätzauftrags ab.

+++ Eine Beispielanfrage zum Abrufen eines Schätzauftrags.

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

+++ Eine Beispielantwort beim Abrufen eines Schätzauftrags.

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
| `estimatedNamespaceDistribution` | Ein Array von Objekten, das die Anzahl der Profile innerhalb der Segmentdefinition anzeigt, aufgeschlüsselt nach Identitäts-Namespace. Die Gesamtanzahl der Profile nach Namespace (addiert die für jeden Namespace angezeigten Werte) kann höher sein als die Profilzählungsmetrik, da ein Profil mit mehreren Namespaces verknüpft werden könnte. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet. |
| `state` | Der aktuelle Status des Vorschauauftrags. Der Status lautet &quot;WIRD AUSGEFÜHRT&quot;, bis die Verarbeitung abgeschlossen ist. Anschließend wird sie zu &quot;RESULT_READY&quot;oder &quot;FEHLGESCHLAGEN&quot;. |
| `_links.preview` | Wenn der `state` &quot;RESULT_READY&quot;ist, stellt dieses Feld eine URL zum Anzeigen der Schätzung bereit. |

+++

## Nächste Schritte

Nach dem Lesen dieses Handbuchs sollten Sie besser wissen, wie Sie mit Vorschauen und Schätzungen mithilfe der Segmentation-API arbeiten. Informationen zum Zugriff auf Metriken, die sich auf Ihre Echtzeit-Kundenprofildaten beziehen, wie z. B. die Gesamtzahl der Profilfragmente und zusammengeführten Profile in bestimmten Namespaces oder den Profildatenspeicher als Ganzes, finden Sie im Handbuch [Profilvorschau (`/previewsamplestatus`)-Endpunkt](../../profile/api/preview-sample-status.md).
