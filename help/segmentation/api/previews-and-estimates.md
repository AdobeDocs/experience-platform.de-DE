---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;Vorschauen;Schätzungen;Vorschauen und Schätzungen;Schätzungen und Vorschauen;API;API;
solution: Experience Platform
title: Endpunkte für Vorschauen und Schätzungen
topic: developer guide
description: Während Sie Ihre Segmentdefinition entwickeln, können Sie die Tools für Schätzung und Vorschau innerhalb von Adobe Experience Platform verwenden, um Informationen auf Ansicht-Zusammenfassungsebene zu erhalten, um sicherzustellen, dass Sie die erwartete Audience isolieren.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 7%

---


# Endpunkte für Vorschauen und Schätzungen

Während Sie Ihre Segmentdefinition entwickeln, können Sie die Tools für Schätzung und Vorschau innerhalb von [!DNL Adobe Experience Platform] verwenden, um Informationen auf Ansicht-Zusammenfassungsebene zu erhalten, um sicherzustellen, dass Sie die erwartete Audience isolieren. **In der** Vorschau werden paginierte Listen von qualifizierten Profilen für eine Segmentdefinition angezeigt, sodass Sie die Ergebnisse mit Ihren Erwartungen vergleichen können. **Die** Schätzwerte liefern statistische Informationen zu einer Segmentdefinition, z. B. die projizierte Audience, das Konfidenzintervall und die Standardabweichung für Fehler.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der API [!DNL Adobe Experience Platform Segmentation Service]. Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach wichtigen Informationen, die Sie kennen müssen, um die API erfolgreich aufzurufen, einschließlich erforderlicher Kopfzeilen und Anleitungen zum Lesen von Beispiel-API-Aufrufen.

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
| `predicateModel` | Der Name des [!DNL Experience Data Model] (XDM)-Schemas, auf dem die Profil-Daten basieren. |

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
| `results` | Eine Liste von Entitäts-IDs zusammen mit den zugehörigen Identitäten. Die bereitgestellten Links können zum Nachschlagen der angegebenen Entitäten mit dem [[!DNL Profile Access API]](../../profile/api/entities.md) verwendet werden. |

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

Nach dem Lesen dieses Handbuchs haben Sie nun ein besseres Verständnis dafür, wie Sie mit Vorschauen und Schätzungen arbeiten können. Weitere Informationen zu den anderen [!DNL Segmentation Service] API-Endpunkten finden Sie im [Handbuch für den Entwickler des Segmentierungsdienstes](./overview.md).