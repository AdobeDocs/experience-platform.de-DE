---
description: Auf dieser Seite wird erläutert, wie Sie mit dem API-Endpunkt /sample-profiles von Destination SDK Beispielprofile generieren können, die auf einem Quellschema basieren. Sie können diese Beispielprofile verwenden, um Ihre dateibasierte Zielkonfiguration zu testen.
title: Erstellen von Beispielprofilen basierend auf einem Quellschema
source-git-commit: fa092e4d1828d9ecd5bc98e3f225fa377f38065f
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 13%

---


# Erstellen von Beispielprofilen basierend auf einem Quellschema

## Übersicht {#overview}

Der erste Schritt beim Testen Ihres dateibasierten Ziels besteht darin, die `/sample-profiles` -Endpunkt, um ein Beispielprofil zu generieren, das auf Ihrem vorhandenen Quellschema basiert.

Beispielprofile sollen Ihnen dabei helfen, die JSON-Struktur eines Profils zu verstehen. Darüber hinaus erhalten Sie damit ein Backbone, das Sie mit Ihren eigenen Profildaten anpassen können, um weitere Zieltests durchzuführen.

## Erste Schritte {#getting-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](./getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Voraussetzungen {#prerequisites}

Bevor Sie die `/sample-profiles` -Endpunkt verwenden, stellen Sie sicher, dass Sie die folgenden Bedingungen erfüllen:

* Sie haben ein vorhandenes dateibasiertes Ziel, das über die Destination SDK erstellt wurde, und Sie können es in Ihrem [Zielkatalog](../ui/destinations-workspace.md).
* Sie haben in der Experience Platform-Benutzeroberfläche mindestens einen Aktivierungsfluss für Ihr Ziel erstellt. Die `/sample-profiles` -Endpunkt erstellt die Profile basierend auf dem Quellschema, das Sie in Ihrem Aktivierungsablauf definiert haben. Siehe [Aktivierungs-Tutorial](../ui/activate-batch-profile-destinations.md) , um zu erfahren, wie Sie einen Aktivierungsfluss erstellen.
* Für eine erfolgreiche API-Anfrage benötigen Sie die Ziel-Instanz-ID, die der zu testenden Zielinstanz entspricht. Rufen Sie die Ziel-Instanz-ID ab, die Sie beim Durchsuchen einer Verbindung mit Ihrem Ziel in der Platform-Benutzeroberfläche im API-Aufruf über die URL verwenden sollten.

   ![UI-Bild, das zeigt, wie die Ziel-Instanz-ID von der URL abgerufen wird.](assets/get-destination-instance-id.png)

## Generieren von Beispielprofilen für Zieltests {#generate-sample-profiles}

Sie können Beispielprofile basierend auf Ihrem Quellschema generieren, indem Sie eine GET-Anfrage an die `/sample-profiles` -Endpunkt mit der Ziel-Instanz-ID des Ziels, das Sie testen möchten.

**API-Format**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Abfrageparameter | Beschreibung |
| -------- | ----------- |
| `destinationInstanceId` | Die ID der Zielinstanz, für die Sie Beispielprofile generieren. Siehe [Voraussetzungen](#prerequisites) für weitere Informationen zum Abrufen dieser ID. |
| `count` | *Optional*. Die Anzahl der Beispielprofile, die Sie generieren möchten. Der Parameter kann Werte zwischen `1 - 1000`. Wenn diese Eigenschaft nicht definiert ist, generiert die API ein einzelnes Beispielprofil. |

**Anfrage**

Die folgende Anfrage generiert ein Beispielprofil basierend auf dem in der Zielinstanz definierten Quellschema mit dem entsprechenden `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count=2' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit der angegebenen Anzahl von Beispielprofilen mit Segmentmitgliedschaft, Identitäten und Profilattributen zurück, die dem Quell-XDM-Schema entsprechen.

>[!NOTE]
>
> Die Antwort gibt nur Segmentzugehörigkeit, Identitäten und Profilattribute zurück, die in der Zielinstanz verwendet werden. Auch wenn Ihr Quellschema andere Felder enthält, werden diese ignoriert.

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![Bild, das die Zuordnung von der Benutzeroberfläche zu den Feldern aus der API-Antwort anzeigt.](assets/sample-api-response-mapping.png)

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `segmentMembership` | Ein map -Objekt, das die Segmentmitgliedschaften des Kontakts beschreibt. Weitere Informationen finden Sie unter `segmentMembership`, lesen [Details zur Segmentzugehörigkeit](../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Ein Zeitstempel, der angibt, wann sich dieses Profil zuletzt für das Segment qualifiziert hat. |
| `status` | Gibt an, ob die Segmentzugehörigkeit im Rahmen der aktuellen Anforderung realisiert wurde. Folgende Werte werden akzeptiert: <ul><li>`existing`: Das Profil war bereits vor der Anfrage Teil des Segments und behält weiterhin seine Mitgliedschaft bei.</li><li>`realized`: Das Profil gibt das Segment als Teil der aktuellen Anforderung ein.</li><li>`exited`: Das Profil beendet das Segment als Teil der aktuellen Anforderung.</li></ul> |
| `identityMap` | Ein Feld vom Typ Zuordnung , das die verschiedenen Identitätswerte einer Person zusammen mit den zugehörigen Namespaces beschreibt. Weitere Informationen finden Sie unter `identityMap`, siehe [Grundlage der Schemakomposition](../../xdm/schema/composition.md#identityMap). |

{style=&quot;table-layout:auto&quot;}

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Beispielprofile basierend auf dem Quellschema generieren, das Sie in Ihrem Ziel konfiguriert haben [Aktivierungsfluss](../ui/activate-batch-profile-destinations.md).

Sie können diese Profile jetzt anpassen oder so verwenden, wie sie von der API zurückgegeben werden, um [Testen der dateibasierten Zielkonfiguration](file-based-destination-testing-api.md).