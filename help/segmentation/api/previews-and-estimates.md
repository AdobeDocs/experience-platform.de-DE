---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zu Vorschauen und Schätzendpunkten
topic: developer guide
translation-type: tm+mt
source-git-commit: 41a5d816f9dc6e7c26141ff5e9173b1b5631d75e
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 7%

---


# Handbuch zu Vorschauen und Schätzendpunkten

Bei der Entwicklung Ihrer Segmentdefinition können Sie die Tools für Schätzung und Vorschau innerhalb der Informationen auf der Ebene der Ansicht verwenden, um sicherzustellen, dass Sie die erwartete Audience isolieren. [!DNL Adobe Experience Platform] **Vorschauen** bieten paginierte Listen von qualifizierten Profilen für eine Segmentdefinition, mit denen Sie die Ergebnisse mit Ihren Erwartungen vergleichen können. **Schätzungen** liefern statistische Informationen zu einer Segmentdefinition, z. B. die projizierte Audience, das Konfidenzintervall und die Standardabweichung.

## Erste Schritte

The endpoints used in this guide are part of the [!DNL Adobe Experience Platform Segmentation Service] API. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example API calls.

## Erstellung von Schätzungen

Die Art und Weise, wie die Datenerfassung ausgelöst wird, hängt von der Erfassungsmethode ab.

Zur Stapelverarbeitung wird der Profil-Store alle 15 Minuten automatisch überprüft, um festzustellen, ob ein neuer Stapel seit Ausführung des letzten Stichprobenauftrags erfolgreich aufgenommen wurde. Ist dies der Fall, wird der Profil-Store anschließend gescannt, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % verändert hat. Wenn diese Bedingungen erfüllt sind, wird ein neuer Stichprobenauftrag ausgelöst.

Zur Streaming-Erfassung wird der Profil-Store stündlich automatisch überprüft, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % verändert hat. Wenn diese Bedingung erfüllt ist, wird ein neuer Stichprobenauftrag ausgelöst.

Die Stichprobengröße der Überprüfung hängt von der Gesamtanzahl der Entitäten in Ihrem Profil-Store ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profil Store | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Mio. | 1 Mio. |
| Über 20 Mio. | 5 % des Gesamtbetrags |

>[!NOTE] Die Ausführung von Schätzungen dauert in der Regel 10 bis 15 Sekunden, beginnend mit einer groben Schätzung und einer Feinabstimmung, wenn mehr Datensätze gelesen werden.

## Create a new preview {#create-preview}

You can create a new preview by making a POST request to the `/preview` endpoint.

>[!NOTE] Beim Erstellen eines Auftrags für eine Vorschau wird automatisch ein Schätzauftrag erstellt. Diese beiden Aufträge verwenden dieselbe ID.

**API-Format**

```http
POST /preview
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile"
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `predicateExpression` | Der PQL-Ausdruck, um die Daten Abfrage. |
| `predicateType` | Der Vorhersagetyp für den Ausdruck Abfrage unter `predicateExpression`. Derzeit ist der einzige akzeptierte Wert für diese Eigenschaft `pql/text`. |
| `predicateModel` | Der Name des Experience Data Model (XDM)-Schemas, auf dem die Profil-Daten basieren. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) mit Details zu Ihrer neu erstellten Vorschau zurück.

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
| `state` | Der aktuelle Status des Auftrags für die Vorschau. Bei der Erstellung befindet es sich im Status &quot;NEU&quot;. Anschließend wird es im Status &quot;WIRD AUSGEFÜHRT&quot;ausgeführt, bis die Verarbeitung abgeschlossen ist. Anschließend wird es zu &quot;ERGEBNIS_BEREIT&quot;oder &quot;FEHLGESCHLAGEN&quot;. |
| `previewId` | Die ID des Auftrags für die Vorschau, der für Nachschlagezwecke bei Ansicht einer Schätzung oder Vorschau verwendet wird, wie im nächsten Abschnitt beschrieben. |

## Abrufen der Ergebnisse einer bestimmten Vorschau {#get-preview}

You can retrieve detailed information about a specific preview by making a GET request to the `/preview` endpoint and providing the preview ID in the request path.

**API-Format**

```http
GET /preview/{PREVIEW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{PREVIEW_ID}` | The `previewId` value of the preview you want to retrieve. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zur angegebenen Vorschau zurück.

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
        },
        "state": "RESULT_READY",
        "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
        }
    }],
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `results` | Eine Liste von Entitäts-IDs zusammen mit den zugehörigen Identitäten. Die bereitgestellten Links können verwendet werden, um die angegebenen Entitäten mithilfe der [Profil Access API](../../profile/api/entities.md)nachzuschlagen. |

## Abrufen der Ergebnisse eines bestimmten Schätzauftrags {#get-estimate}

Nachdem Sie einen Vorschau-Auftrag erstellt haben, können Sie ihn `previewId` im Pfad einer GET-Anforderung zum `/estimate` Endpunkt verwenden, um statistische Informationen zur Segmentdefinition wie die projizierte Audience, das Konfidenzintervall und die Standardabweichung für Fehler zu erhalten.

**API-Format**

```http
GET /estimate/{PREVIEW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{PREVIEW_ID}` | Ein Schätzauftrag wird nur ausgelöst, wenn ein Auftragsauftrag erstellt wird und die beiden Vorschauen denselben ID-Wert für Suchzwecke verwenden. Dies ist insbesondere der `previewId` Wert, der beim Erstellen des Auftrags für die Vorschau zurückgegeben wird. |

**Anfrage**

Die folgende Anfrage ruft die Ergebnisse eines bestimmten Schätzauftrags ab.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zum Schätzauftrag zurück.

```json
{
    "estimatedSize": 0,
    "numRowsToRead": 1,
    "state": "RESULT_READY",
    "profilesReadSoFar": 1,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 0,
    "totalRows": 1,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `state` | Der aktuelle Status des Auftrags für die Vorschau. Ist &quot;WIRD AUSGEFÜHRT&quot;bis die Verarbeitung abgeschlossen ist, und wird dann &quot;ERGEBNIS_BEREIT&quot;oder &quot;FEHLGESCHLAGEN&quot;. |
| `_links.preview` | Wenn der aktuelle Status des Vorschau-Auftrags &quot;RESULT_READY&quot;lautet, stellt dieses Attribut eine URL zur Ansicht der Schätzung bereit. |

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie nun ein besseres Verständnis dafür, wie Sie mit Vorschauen und Schätzungen arbeiten können. Weitere Informationen zu den anderen Segmentierungsdienst-API-Endpunkten finden Sie im Entwicklerhandbuch für den [Segmentierungsdienst](./overview.md).