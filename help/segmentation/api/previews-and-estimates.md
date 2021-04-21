---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;Vorschauen;Schätzungen;Vorschauen und Schätzungen;Schätzungen und Vorschauen;API;API;
solution: Experience Platform
title: Vorschauen und Schätzwerte für API-Endpunkte
topic-legacy: developer guide
description: Während die Segmentdefinition entwickelt wird, können Sie die Tools für Schätzung und Vorschau innerhalb von Adobe Experience Platform verwenden, um Informationen auf der Ebene der Ansicht zusammenzufassen, um sicherzustellen, dass Sie die erwartete Audience isolieren.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 6%

---

# Endpunkte für Vorschauen und Schätzungen

Beim Entwickeln einer Segmentdefinition können Sie die Tools für Schätzung und Vorschau innerhalb von Adobe Experience Platform verwenden, um Informationen auf Ansicht-Ebene zu erhalten, um sicherzustellen, dass Sie die erwartete Audience isolieren.

* **In der** Vorschau werden paginierte Listen von qualifizierten Profilen für eine Segmentdefinition angezeigt, sodass Sie die Ergebnisse mit Ihren Erwartungen vergleichen können.

* **Die** Schätzwerte liefern statistische Informationen zu einer Segmentdefinition, z. B. die projizierte Audience, das Konfidenzintervall und die Standardabweichung für Fehler.

>[!NOTE]
>
>Weitere Informationen zum Zugriff auf ähnliche Metriken im Zusammenhang mit Echtzeit-Kundendaten wie die Gesamtanzahl der Profil-Fragmente und zusammengeführten Profil in bestimmten Namensräumen oder den Profil-Datenspeicher insgesamt finden Sie im [Profil-Vorschau (Vorschau-Musterstatus)-Endpunkt-Handbuch](../../profile/api/preview-sample-status.md), Teil des Profil-API-Entwicklerhandbuchs.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der API [!DNL Adobe Experience Platform Segmentation Service]. Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach wichtigen Informationen, die Sie kennen müssen, um die API erfolgreich aufzurufen, einschließlich erforderlicher Kopfzeilen und Anleitungen zum Lesen von Beispiel-API-Aufrufen.

## Erstellung von Schätzungen

Wenn die Erfassung von Datensätzen im Profil Store die Gesamtanzahl der Profil um mehr als 5 % erhöht oder verringert, wird ein Stichprobenauftrag ausgelöst, um die Anzahl zu aktualisieren. Die Art und Weise, wie die Datenerfassung ausgelöst wird, hängt von der Erfassungsmethode ab:

* **Stapelverarbeitung:** Bei Stapelverarbeitung wird innerhalb von 15 Minuten nach erfolgreichem Einsetzen eines Stapels in den Profil Store ein Auftrag ausgeführt, um die Zählung zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde.
* **Streaming-Erfassung:** Bei Workflows von Streaming-Daten wird stündlich geprüft, ob der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Auftrag ausgelöst, um die Anzahl zu aktualisieren.

Die Stichprobengröße der Überprüfung hängt von der Gesamtanzahl der Entitäten in Ihrem Profil-Store ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profil Store | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Mio. | 1 Mio. |
| Über 20 Mio. | 5 % des Gesamtbetrags |

>[!NOTE]
>
>Die Ausführung von Schätzungen dauert in der Regel 10 bis 15 Sekunden, beginnend mit einer groben Schätzung und einer Feinabstimmung, wenn mehr Datensätze gelesen werden.

## Neue Vorschau {#create-preview} erstellen

Sie können eine neue Vorschau erstellen, indem Sie eine POST an den `/preview`-Endpunkt anfordern.

>[!NOTE]
>
>Beim Erstellen eines Auftrags für eine Vorschau wird automatisch ein Schätzauftrag erstellt. Diese beiden Aufträge verwenden dieselbe ID.

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
| `predicateModel` | Der Name der [!DNL Experience Data Model] (XDM) Schema-Klasse, auf der die Profil-Daten basieren. |

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

Sie können detaillierte Informationen zu einer bestimmten Vorschau abrufen, indem Sie eine GET an den Endpunkt `/preview` anfordern und die Vorschauen-ID im Anforderungspfad angeben.

**API-Format**

```http
GET /preview/{PREVIEW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{PREVIEW_ID}` | Der `previewId`-Wert der Vorschau, die Sie abrufen möchten. |

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
| `results` | Eine Liste von Entitäts-IDs zusammen mit den zugehörigen Identitäten. Die bereitgestellten Links können zum Nachschlagen der angegebenen Entitäten verwendet werden, indem der [API-Endpunkt für den Zugriff auf Profile](../../profile/api/entities.md) verwendet wird. |

## Abrufen der Ergebnisse eines bestimmten Schätzauftrags {#get-estimate}

Nachdem Sie einen Vorschau-Auftrag erstellt haben, können Sie dessen `previewId` im Pfad einer GET-Anforderung zum `/estimate`-Endpunkt verwenden, um statistische Informationen zur Segmentdefinition wie die projizierte Audience, das Konfidenzintervall und die Standardabweichung für Fehler Ansicht.

**API-Format**

```http
GET /estimate/{PREVIEW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{PREVIEW_ID}` | Ein Schätzauftrag wird nur ausgelöst, wenn ein Auftragsauftrag erstellt wird und die beiden Vorschauen denselben ID-Wert für Suchzwecke verwenden. Dies ist insbesondere der Wert `previewId`, der beim Erstellen des Auftrags für die Vorschau zurückgegeben wird. |

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
| `estimatedNamespaceDistribution` | Ein Array von Objekten, das die Anzahl der Profil innerhalb des Segments nach Identitäts-Namensraum unterteilt anzeigt. Die Gesamtanzahl der Profil nach Namensraum (addieren Sie die für jeden Namensraum angezeigten Werte) kann höher als die Metrik für die Anzahl der Profil sein, da ein Profil mit mehreren Namensräumen verknüpft werden könnte. Wenn ein Kunde beispielsweise auf mehr als einem Kanal mit Ihrer Marke interagiert, werden mehrere Namensraum mit diesem Kunden verknüpft. |
| `state` | Der aktuelle Status des Auftrags für die Vorschau. Der Status lautet &quot;WIRD AUSGEFÜHRT&quot;, bis die Verarbeitung abgeschlossen ist. Anschließend wird er &quot;ERGEBNIS_READY&quot;oder &quot;FEHLGESCHLAGEN&quot;. |
| `_links.preview` | Wenn `state` &quot;RESULT_READY&quot;ist, stellt dieses Feld eine URL zur Ansicht der Schätzung bereit. |

## Nächste Schritte

Nach dem Lesen dieses Handbuchs sollten Sie mit der Segmentierungs-API ein besseres Verständnis für die Arbeit mit Vorschauen und Schätzungen haben. Informationen zum Zugriff auf Metriken zu Ihren Echtzeit-Kundendaten, wie z. B. die Gesamtanzahl der Profil-Fragmente und zusammengeführten Profil in bestimmten Namensräumen oder dem Profil-Datenspeicher insgesamt, finden Sie im Endpunkt-Handbuch [Profil-Vorschau (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).
