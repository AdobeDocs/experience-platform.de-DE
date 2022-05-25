---
keywords: Experience Platform; Startseite; beliebte Themen; Flussdienst; Aktualisieren von Ziel-Datenflüssen
solution: Experience Platform
title: Aktualisieren von Zieldatenflüssen mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Aktualisieren eines Ziel-Datenflusses beschrieben. Erfahren Sie, wie Sie den Datenfluss aktivieren oder deaktivieren, seine grundlegenden Informationen aktualisieren oder mithilfe der Flow Service-API Segmente und Attribute hinzufügen und entfernen.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 95dd6982eeecf6b13b6c8a6621b5e6563c25ae26
workflow-type: tm+mt
source-wordcount: '2419'
ht-degree: 40%

---

# Aktualisieren von Zieldatenflüssen mithilfe der Flow Service-API

In diesem Tutorial werden die Schritte zum Aktualisieren eines Ziel-Datenflusses beschrieben. Erfahren Sie, wie Sie den Datenfluss aktivieren oder deaktivieren, seine grundlegenden Informationen aktualisieren oder Segmente und Attribute mithilfe des [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Informationen zum Bearbeiten von Ziel-Datenflüssen mithilfe der Experience Platform-Benutzeroberfläche finden Sie unter [Bearbeiten von Aktivierungsflüssen](/help/destinations/ui/edit-activation.md).

## Erste Schritte {#get-started}

Für dieses Tutorial benötigen Sie eine gültige Fluss-ID. Wenn Sie keine gültige Fluss-ID haben, wählen Sie Ihr Ziel aus der [Zielkatalog](../catalog/overview.md) und führen Sie die Schritte aus, die beschrieben wurden, um [Verbindung zum Ziel herstellen](../ui/connect-destination.md) und [Daten aktivieren](../ui/activation-overview.md) vor dem Versuch dieses Tutorials.

>[!NOTE]
>
> Die Begriffe *Fluss* und *dataflow* werden in diesem Tutorial synonym verwendet. Im Kontext dieses Tutorials haben die dieselbe Bedeutung.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. ](../home.md)[!DNL Destinations] Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Ihren Datenfluss mit der [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in der Experience Platform, einschließlich derjenigen, die [!DNL Flow Service], werden auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Wenn die Variable `x-sandbox-name` -Kopfzeile nicht angegeben ist, werden Anfragen unter der `prod` Sandbox.

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Nachschlagen von Datenflussdetails {#look-up-dataflow-details}

Der erste Schritt bei der Aktualisierung Ihres Ziel-Datenflusses besteht darin, Datenflussdetails mit Ihrer Fluss-ID abzurufen. Sie können die aktuellen Details eines vorhandenen Datenflusses anzeigen, indem Sie eine GET-Anfrage an den `/flows`-Endpunkt stellen.

**API-Format**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Die eindeutige `id` für den Ziel-Datenfluss, den Sie abrufen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden Informationen zu Ihrer Fluss-ID abgerufen.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die aktuellen Details Ihres Datenflusses zurück, einschließlich der Version, der eindeutigen Kennung (`id`) und anderen relevanten Informationen.

```json
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## Aktualisieren des Dataflow-Namens und der Beschreibung {#update-dataflow}

Um den Namen und die Beschreibung Ihres Datenflusses zu aktualisieren, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service] API bei der Angabe Ihrer Fluss-ID, -Version und der neuen Werte, die Sie verwenden möchten.

>[!IMPORTANT]
>
>Die Kopfzeile `If-Match` ist bei einer PATCH-Anfrage erforderlich. Der Wert für diese Kopfzeile ist die eindeutige Version des Datenflusses, den Sie aktualisieren möchten. Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung eines Datenflusses aktualisiert.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Die folgende Anfrage aktualisiert den Namen und die Beschreibung Ihres Datenflusses.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Datenfluss aktivieren oder deaktivieren {#enable-disable-dataflow}

Wenn diese Option aktiviert ist, exportiert ein Datenfluss Profile in das Ziel. Datenflüsse sind standardmäßig aktiviert, können aber deaktiviert werden, um die Profilexporte anzuhalten.

Sie können einen vorhandenen Ziel-Datenfluss aktivieren oder deaktivieren, indem Sie eine POST-Anfrage an die [!DNL Flow Service] API und den Status bereitstellen, an den Sie den Fluss aktualisieren möchten.

**API-Format**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**Anfrage**

Die folgende Anfrage aktualisiert den Status Ihres Datenflusses auf &quot;Aktiviert&quot;.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Die folgende Anfrage aktualisiert den Status Ihres Datenflusses auf &quot;Deaktiviert&quot;.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Hinzufügen eines Segments zu einem Datenfluss {#add-segment}

Um ein Segment zum Ziel-Datenfluss hinzuzufügen, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service] API bei der Angabe Ihrer Fluss-ID, -Version und des Segments, das Sie hinzufügen möchten.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Mit der folgenden Anfrage wird einem vorhandenen Ziel-Datenfluss ein neues Segment hinzugefügt.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "triggerType": "AFTER_SEGMENT_EVAL",
               "endDate":"2022-03-10"
            }
         }
      }
   }
]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um ein Segment zu einem Datenfluss hinzuzufügen, verwenden Sie die Operation `add`. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. Verwenden Sie beim Hinzufügen eines Segments zu einem Datenfluss den im Beispiel angegebenen Pfad. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |
| `id` | Geben Sie die ID des Segments an, das Sie dem Ziel-Datenfluss hinzufügen. |
| `name` | **(Optional)**. Geben Sie den Namen des Segments an, das Sie dem Ziel-Datenfluss hinzufügen möchten. Beachten Sie, dass dieses Feld nicht obligatorisch ist und Sie ein Segment erfolgreich zum Ziel-Datenfluss hinzufügen können, ohne dessen Namen anzugeben. |
| `filenameTemplate` | Für *Batch-Ziele* nur. Dieses Feld ist nur erforderlich, wenn ein Segment zu einem Datenfluss in Batch-Dateiexport-Zielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br> Dieses Feld bestimmt das Dateinamenformat der Dateien, die an Ihr Ziel exportiert werden. <br> Die folgenden Optionen sind verfügbar: <br> <ul><li>`%DESTINATION_NAME%`: Obligatorisch. Die exportierten Dateien enthalten den Zielnamen.</li><li>`%SEGMENT_ID%`: Obligatorisch. Die exportierten Dateien enthalten die ID des exportierten Segments.</li><li>`%SEGMENT_NAME%`: **(Optional)**. Die exportierten Dateien enthalten den Namen des exportierten Segments.</li><li>`DATETIME(YYYYMMdd_HHmmss)` oder `%TIMESTAMP%`: **(Optional)**. Wählen Sie eine dieser beiden Optionen für Ihre Dateien aus, um den Zeitpunkt einzuschließen, zu dem sie von Experience Platform generiert werden.</li><li>`custom-text`: **(Optional)**. Ersetzen Sie diesen Platzhalter durch einen beliebigen benutzerdefinierten Text, den Sie am Ende Ihrer Dateinamen anhängen möchten.</li></ul> <br> Weitere Informationen zur Konfiguration von Dateinamen finden Sie im Abschnitt [Konfigurieren von Dateinamen](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) im Tutorial zur Aktivierung von Batch-Zielen. |
| `exportMode` | Für *Batch-Ziele* nur. Dieses Feld ist nur erforderlich, wenn ein Segment zu einem Datenfluss in Batch-Dateiexport-Zielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br> Obligatorisch. Wählen Sie `"DAILY_FULL_EXPORT"` oder `"FIRST_FULL_THEN_INCREMENTAL"` aus. Weitere Informationen zu den beiden Optionen finden Sie unter [Exportieren von vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Exportieren von inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) im Tutorial zur Aktivierung von Batch-Zielen. |
| `startDate` | Wählen Sie das Datum aus, an dem das Segment Profile in Ihr Ziel exportieren soll. |
| `frequency` | Für *Batch-Ziele* nur. Dieses Feld ist nur erforderlich, wenn ein Segment zu einem Datenfluss in Batch-Dateiexport-Zielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br> Obligatorisch. <br> <ul><li>Für den Exportmodus `"DAILY_FULL_EXPORT"` können Sie `ONCE` oder `DAILY` wählen.</li><li>Für den Exportmodus `"FIRST_FULL_THEN_INCREMENTAL"` können Sie `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"` wählen.</li></ul> |
| `triggerType` | Für *Batch-Ziele* nur. Dieses Feld ist nur erforderlich, wenn Sie die `"DAILY_FULL_EXPORT"` -Modus im `frequency` auswählen. <br> Obligatorisch. <br> <ul><li>Auswählen `"AFTER_SEGMENT_EVAL"` , damit der Aktivierungsauftrag unmittelbar nach Abschluss des täglichen Platform-Batch-Segmentierungsauftrags ausgeführt wird. Dadurch wird sichergestellt, dass bei der Ausführung des Aktivierungsauftrags die aktuellsten Profile nach Ihrem Ziel exportiert werden.</li><li>Auswählen `"SCHEDULED"` , damit der Aktivierungsauftrag zu einem festen Zeitpunkt ausgeführt wird. Dadurch wird sichergestellt, dass Experience Platform-Profildaten jeden Tag gleichzeitig exportiert werden. Je nachdem, ob der Batch-Segmentierungsauftrag vor dem Beginn des Aktivierungsvorgangs abgeschlossen wurde, sind die zu exportierenden  jedoch möglicherweise nicht die aktuellsten. Bei Auswahl dieser Option müssen Sie auch eine `startTime` um anzugeben, zu welchem Zeitpunkt in UTC die täglichen Exporte stattfinden sollen.</li></ul> |
| `endDate` | Für *Batch-Ziele* nur. Dieses Feld ist nur erforderlich, wenn ein Segment zu einem Datenfluss in Batch-Dateiexport-Zielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br> Nicht anwendbar bei der Auswahl von `"exportMode":"DAILY_FULL_EXPORT"` und `"frequency":"ONCE"`. <br> Legt das Datum fest, ab dem Segmentmitglieder nicht mehr in das Ziel exportiert werden. |
| `startTime` | Für *Batch-Ziele* nur. Dieses Feld ist nur erforderlich, wenn ein Segment zu einem Datenfluss in Batch-Dateiexport-Zielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br> Obligatorisch. Wählen Sie den Zeitpunkt aus, zu dem Dateien, die Mitglieder des Segments enthalten, generiert und an Ihr Ziel exportiert werden sollen. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Entfernen eines Segments aus einem Datenfluss {#remove-segment}

Um ein Segment aus einem vorhandenen Ziel-Datenfluss zu entfernen, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service] API bei der Bereitstellung Ihrer Fluss-ID, -Version und der Indexauswahl des Segments, das Sie entfernen möchten. Indizierung beginnt bei `0`. Beispielsweise entfernt die unten stehende Beispielanfrage das erste und zweite Segment aus dem Datenfluss.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Mit der folgenden Anfrage werden zwei Segmente aus einem vorhandenen Ziel-Datenfluss entfernt.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/0/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/1/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um ein Segment aus einem Datenfluss zu entfernen, verwenden Sie die `remove` Vorgang. |
| `path` | Gibt an, welches vorhandene Segment basierend auf dem Index der Segmentauswahl aus dem Ziel-Datenfluss entfernt werden soll. Um die Segmentreihenfolge in einem Datenfluss abzurufen, führen Sie einen GET-Aufruf an die `/flows` Endpunkt und überprüfen Sie die `transformations.segmentSelectors` -Eigenschaft. Um das erste Segment im Datenfluss zu löschen, verwenden Sie `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Komponenten eines Segments in einem Datenfluss aktualisieren {#update-segment}

Sie können Komponenten eines Segments in einem vorhandenen Ziel-Datenfluss aktualisieren. Sie können beispielsweise die Exportfrequenz ändern oder die Dateinamenvorlage bearbeiten. Führen Sie dazu eine PATCH-Anfrage an die [!DNL Flow Service] API bei der Angabe Ihrer Fluss-ID, Version und Indexauswahl des Segments, das Sie aktualisieren möchten. Indizierung beginnt bei `0`. Beispielsweise aktualisiert die nachstehende Anfrage das neunte Segment in einem Datenfluss.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Beim Aktualisieren eines Segments in einem vorhandenen Ziel-Datenfluss sollten Sie zunächst einen GET-Vorgang ausführen, um die Details des Segments abzurufen, das Sie aktualisieren möchten. Geben Sie dann alle Segmentinformationen in der Payload an, nicht nur die Felder, die Sie aktualisieren möchten. Im folgenden Beispiel wird benutzerdefinierter Text am Ende der Dateinamenvorlage hinzugefügt und die Häufigkeit des Exports wird von 6 Stunden auf 12 Stunden aktualisiert.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

Beschreibungen der Eigenschaften in der Payload finden Sie im Abschnitt . [Hinzufügen eines Segments zu einem Datenfluss](#add-segment).


**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

In den Beispielen unten finden Sie weitere Beispiele für Segmentkomponenten, die Sie in einem Datenfluss aktualisieren können.

## Aktualisieren Sie den Exportmodus eines Segments von geplant auf nach der Segmentauswertung {#update-export-mode}

+++ Klicken Sie auf ein Beispiel, bei dem ein Segmentexport aktualisiert wird, indem er täglich zu einem bestimmten Zeitpunkt aktiviert wird und täglich nach Abschluss des Batch-Segmentierungsauftrags von Platform aktiviert wird.

Das Segment wird täglich um 16:00 UTC exportiert.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

Das Segment wird jeden Tag nach Abschluss des täglichen Batch-Segmentierungsauftrags exportiert.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "AFTER_SEGMENT_EVAL",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Aktualisieren Sie die Dateinamenvorlage, um zusätzliche Felder in den Dateinamen einzuschließen. {#update-filename-template}

+++ Klicken Sie auf ein Beispiel, in dem die Dateinamenvorlage aktualisiert wird, um zusätzliche Felder in den Dateinamen einzuschließen.

Die exportierten Dateien enthalten den Zielnamen und die Segmentkennung der Experience Platform

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

Die exportierten Dateien enthalten den Zielnamen, die Segmentkennung der Experience Platform, das Datum und die Uhrzeit der Dateigenerierung durch die Experience Platform sowie benutzerdefinierten Text, der am Dateiende angehängt wird.


```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_%this is custom text%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Hinzufügen eines Profilattributs zu einem Datenfluss {#add-profile-attribute}

Um dem Ziel-Datenfluss ein Profilattribut hinzuzufügen, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service] API bei der Angabe Ihrer Fluss-ID, Version und des Profilattributs, das Sie hinzufügen möchten.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Mit der folgenden Anfrage wird einem vorhandenen Ziel-Datenfluss ein neues Profilattribut hinzugefügt.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um einem Datenfluss ein Profilattribut hinzuzufügen, verwenden Sie die `add` Vorgang. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. Verwenden Sie beim Hinzufügen eines Profilattributs zu einem Datenfluss den im Beispiel angegebenen Pfad. |
| `value.path` | Der Wert des Profilattributs, das Sie dem Datenfluss hinzufügen. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Entfernen eines Profilattributs aus einem Datenfluss {#remove-profile-attribute}

Um ein Profilattribut aus einem vorhandenen Ziel-Datenfluss zu entfernen, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service] API bei der Angabe Ihrer Fluss-ID, Version und Indexauswahl des zu entfernenden Profilattributs. Indizierung beginnt bei `0`. Beispielsweise entfernt die unten stehende Beispielanfrage das fünfte Profilattribut aus dem Datenfluss.


**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Mit der folgenden Anfrage wird ein Profilattribut aus einem vorhandenen Ziel-Datenfluss entfernt.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um ein Segment aus einem Datenfluss zu entfernen, verwenden Sie die `remove` Vorgang. |
| `path` | Gibt an, welches vorhandene Profilattribut basierend auf dem Index der Segmentauswahl aus dem Ziel-Datenfluss entfernt werden soll. Um die Reihenfolge der Profilattribute in einem Datenfluss abzurufen, führen Sie einen GET-Aufruf an die `/flows` Endpunkt und überprüfen Sie die `transformations.profileSelectors` -Eigenschaft. Um das erste Segment im Datenfluss zu löschen, verwenden Sie `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen für die Fehlermeldung bei der Experience Platform-API. Siehe [API-Status-Codes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) und [Fehler im Anfrage-Header](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

In diesem Tutorial haben Sie erfahren, wie Sie verschiedene Komponenten eines Ziel-Datenflusses aktualisieren, z. B. Segmente oder Profilattribute mit [!DNL Flow Service] API. Weitere Informationen zu Zielen finden Sie im Abschnitt [Ziele - Übersicht](../home.md).
