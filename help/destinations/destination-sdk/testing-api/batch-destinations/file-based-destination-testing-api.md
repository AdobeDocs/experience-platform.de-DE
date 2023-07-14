---
description: Auf dieser Seite wird erläutert, wie Sie mit dem API-Endpunkt /testing/destinationInstance testen können, ob Ihr dateibasiertes Ziel richtig konfiguriert ist, und die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel überprüfen.
title: Testen Ihres dateibasierten Ziels mit Beispielprofilen
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: 9ac6b075af3805da4dad0dd6442d026ae96ab5c7
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 85%

---

# Testen Ihres dateibasierten Ziels mit Beispielprofilen

## Übersicht {#overview}

Auf dieser Seite wird erläutert, wie Sie den API-Endpunkt `/testing/destinationInstance` verwenden, um zu testen, ob Ihr dateibasiertes Ziel richtig konfiguriert ist, und um die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel zu überprüfen.

Sie können Anfragen an den Test-Endpunkt mit oder ohne Hinzufügen von [Beispielprofilen](file-based-sample-profile-generation-api.md) an den Aufruf stellen. Wenn Sie bei der Anfrage keine Profile senden, generiert die API automatisch ein Beispielprofil und fügt es der Anfrage hinzu.

Die automatisch generierten Beispielprofile enthalten allgemeine Daten. Wenn Sie Ihr Ziel mit benutzerdefinierten, intuitiveren Profildaten testen möchten, verwenden Sie die [Beispielprofilgenerierungs-API](file-based-sample-profile-generation-api.md) , um ein Beispielprofil zu generieren, dann die Antwort anzupassen und sie in die Anfrage an den Endpunkt `/testing/destinationInstance` aufzunehmen.

## Erste Schritte {#getting-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Voraussetzungen {#prerequisites}

Bevor Sie den Endpunkt `/testing/destinationInstance` verwenden, stellen Sie sicher, dass Sie die folgenden Bedingungen erfüllen:

* Sie haben ein vorhandenes dateibasiertes Ziel, das über das Destination SDK erstellt wurde, und Sie können es in Ihrem [Zielkatalog](../../../ui/destinations-workspace.md) sehen.
* Sie haben in der Experience Platform-Benutzeroberfläche mindestens einen Aktivierungsfluss für Ihr Ziel erstellt.
* Für eine erfolgreiche API-Anfrage benötigen Sie die Ziel-Instanz-ID, die der zu testenden Zielinstanz entspricht. Rufen Sie die Ziel-Instanz-ID ab, die Sie beim Durchsuchen einer Verbindung mit Ihrem Ziel in der Platform-Benutzeroberfläche im API-Aufruf über die URL verwenden sollten.

  ![Bild der Benutzeroberfläche, das zeigt, wie die Ziel-Instanz-ID von der URL abgerufen wird.](../../assets/testing-api/get-destination-instance-id.png)
* *Optional*: Wenn Sie Ihre Zielkonfiguration mit einem Beispielprofil testen möchten, das zum API-Aufruf hinzugefügt wurde, verwenden Sie den Endpunkt [/sample-profiles](file-based-sample-profile-generation-api.md), um ein Beispielprofil zu generieren, das auf Ihrem vorhandenen Quellschema basiert. Wenn Sie kein Beispielprofil angeben, generiert die API ein Profil und gibt es in der Antwort zurück.

## Testen Sie Ihre Zielkonfiguration, ohne Profile zum Aufruf hinzuzufügen {#test-without-adding-profiles}

**API-Format**

```http
POST /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Anfrage**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Pfadparameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Die ID der Zielinstanz, für die Sie Beispielprofile generieren. Im Abschnitt [Voraussetzungen](#prerequisites) finden Sie weitere Informationen zum Abrufen dieser ID. |

**Antwort**

Bei einer erfolgreiche Antwort wird der HTTP-Status 200 zusammen mit der Antwort-Payload zurückgegeben.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
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
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `activations` | Gibt die Zielgruppen-ID und die Flusslaufs-ID für jede aktivierte Zielgruppe zurück. Die Anzahl der Aktivierungseinträge (und der zugehörigen generierten Dateien) entspricht der Anzahl der Zielgruppen, die auf der Zielinstanz zugeordnet sind. <br><br> Beispiel: Wenn Sie der Zielinstanz zwei Zielgruppen zugeordnet haben, wird die `activations` -Array enthält zwei Einträge. Jede aktivierte Audience entspricht einer exportierten Datei. |
| `results` | Gibt die ID der Zielinstanz und die IDs der Flussausführung zurück, die Sie zum Aufrufen der [Ergebnis-API](file-based-destination-results-api.md) verwenden können, um die Integration weiter zu testen. |
| `inputProfiles` | Gibt die von der API automatisch generierten Beispielprofile zurück. |

{style="table-layout:auto"}

## Testen Sie Ihre Zielkonfiguration mit Profilen, die zum Aufruf hinzugefügt wurden {#test-with-added-profiles}

Um Ihr Ziel mit benutzerdefinierten, intuitiveren Profildaten zu testen, können Sie die vom Endpunkt [/sample-profiles](file-based-sample-profile-generation-api.md) erhaltene Antwort mit Werten Ihrer Wahl anpassen und das benutzerdefinierte Profil in die Anfrage an den Endpunkt `/testing/destinationInstance` einschließen.

**API-Format**

```http
POST  /testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Anfrage**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' 
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
   "profiles":[
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
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}'
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Die Ziel-Instanz-ID des Ziels, das Sie testen.  Die ID der Zielinstanz, für die Sie Beispielprofile generieren. Im Abschnitt [Voraussetzungen](#prerequisites) finden Sie weitere Informationen zum Abrufen dieser ID. |
| `profiles` | Array, das ein oder mehrere Profile enthalten kann. Verwenden Sie den [Beispielprofil-API-Endpunkt](file-based-sample-profile-generation-api.md), um Profile zu generieren, die in diesem API-Aufruf verwendet werden. |

**Antwort**

Bei einer erfolgreiche Antwort wird der HTTP-Status 200 zusammen mit der Antwort-Payload zurückgegeben.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
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
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `activations` | Gibt die Zielgruppen-ID und die Flusslaufs-ID für jede aktivierte Zielgruppe zurück. Die Anzahl der Aktivierungseinträge (und der zugehörigen generierten Dateien) entspricht der Anzahl der Zielgruppen, die auf der Zielinstanz zugeordnet sind. <br><br> Beispiel: Wenn Sie der Zielinstanz zwei Zielgruppen zugeordnet haben, wird die `activations` -Array enthält zwei Einträge. Jede aktivierte Audience entspricht einer exportierten Datei. |
| `results` | Gibt die ID der Zielinstanz und die IDs der Flussausführung zurück, die Sie zum Aufrufen der [Ergebnis-API](file-based-destination-results-api.md) verwenden können, um die Integration weiter zu testen. |
| `inputProfiles` | Gibt die benutzerdefinierten Beispielprofile zurück, die Sie in der API-Anfrage übergeben haben. |

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihre dateibasierte Zielkonfiguration testen können.

Wenn Sie eine gültige API-Antwort erhalten haben, funktioniert Ihr Ziel ordnungsgemäß. Wenn Sie genauere Informationen über Ihren Aktivierungsfluss erhalten möchten, können Sie die Eigenschaft `results` aus der Antwort verwenden, um [detaillierte Aktivierungsergebnisse anzuzeigen](file-based-destination-results-api.md).

Wenn Sie ein öffentliches Ziel erstellen, können Sie jetzt [Ihre Zielkonfiguration zur Überprüfung an Adobe senden](../../guides/submit-destination.md).
