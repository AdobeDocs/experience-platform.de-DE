---
keywords: Experience Platform;Startseite;beliebte Themen;Flow Service;Ziel-Datenflüsse aktualisieren
solution: Experience Platform
title: Aktualisieren von Zieldatenflüssen mithilfe der Flow Service-API
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Aktualisieren eines Ziel-Datenflusses beschrieben. Erfahren Sie, wie Sie den Datenfluss aktivieren oder deaktivieren, seine grundlegenden Informationen aktualisieren oder mithilfe der Flow Service-API Zielgruppen und Attribute hinzufügen und entfernen.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 30%

---

# Aktualisieren von Zieldatenflüssen mithilfe der Flow Service-API

In diesem Tutorial werden die Schritte zum Aktualisieren eines Ziel-Datenflusses beschrieben. Erfahren Sie, wie Sie den Datenfluss aktivieren oder deaktivieren, seine grundlegenden Informationen aktualisieren oder Zielgruppen und Attribute mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) hinzufügen und entfernen. Informationen zur Bearbeitung von Ziel-Datenflüssen mithilfe der Experience Platform-Benutzeroberfläche finden Sie unter [Bearbeiten von Aktivierungsflüssen](/help/destinations/ui/edit-activation.md).

## Erste Schritte {#get-started}

Für dieses Tutorial benötigen Sie eine gültige Fluss-ID. Wenn Sie keine gültige Fluss-ID haben, wählen Sie Ihr Ziel aus dem [Zielkatalog](../catalog/overview.md) und befolgen Sie die beschriebenen Schritte zum [Herstellen einer Verbindung mit dem Ziel](../ui/connect-destination.md) und [Aktivieren von Daten](../ui/activation-overview.md), bevor Sie dieses Tutorial ausführen.

>[!NOTE]
>
> Die Begriffe *Fluss* und *Datenfluss* werden in diesem Tutorial synonym verwendet. Im Kontext dieses Tutorials haben sie dieselbe Bedeutung.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele](../home.md): [!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Ihren Datenfluss mithilfe der [!DNL Flow Service]-API erfolgreich aktualisieren zu können.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um Experience Platform-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, sind in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an Experience Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Wenn die `x-sandbox-name`-Kopfzeile nicht angegeben ist, werden Anfragen unter der `prod`-Sandbox aufgelöst.

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
| `{FLOW_ID}` | Der eindeutige `id` für den Ziel-Datenfluss, den Sie abrufen möchten. |

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

Bei einer erfolgreichen Antwort werden die aktuellen Details Ihres Datenflusses zurückgegeben, einschließlich der Version, der eindeutigen Kennung (`id`) und anderer relevanter Informationen.

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

## Aktualisieren des Datenflussnamens und der Beschreibung {#update-dataflow}

Um den Namen und die Beschreibung Ihres Datenflusses zu aktualisieren, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API aus und geben Sie dabei Ihre Fluss-ID, Version und die neuen Werte an, die Sie verwenden möchten.

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

## Aktivieren oder Deaktivieren des Datenflusses {#enable-disable-dataflow}

Wenn diese Option aktiviert ist, exportiert ein Datenfluss Profile an das Ziel. Datenflüsse sind standardmäßig aktiviert, können jedoch deaktiviert werden, um die Profilexporte anzuhalten.

Sie können einen vorhandenen Ziel-Datenfluss aktivieren oder deaktivieren, indem Sie eine POST-Anfrage an die [!DNL Flow Service]-API stellen und den Status angeben, auf den Sie den Fluss aktualisieren möchten.

**API-Format**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**Anfrage**

Die folgende Anfrage aktualisiert den Status Ihres Datenflusses auf „Aktiviert“.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Die folgende Anfrage aktualisiert den Status Ihres Datenflusses auf „Deaktiviert“.

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

## Hinzufügen einer Zielgruppe zu einem Datenfluss {#add-segment}

Um eine Zielgruppe zum Ziel-Datenfluss hinzuzufügen, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API durch und geben Sie dabei Ihre Fluss-ID, Version und die Zielgruppe an, die Sie hinzufügen möchten.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Die folgende Anfrage fügt eine neue Zielgruppe zu einem vorhandenen Ziel-Datenfluss hinzu.

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
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um eine Zielgruppe zu einem Datenfluss hinzuzufügen, verwenden Sie den Vorgang `add` . |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. Verwenden Sie beim Hinzufügen einer Zielgruppe zu einem Datenfluss den im Beispiel angegebenen Pfad. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |
| `id` | Geben Sie die ID der Zielgruppe an, die Sie dem Ziel-Datenfluss hinzufügen. |
| `name` | **(optional)**. Geben Sie den Namen der Zielgruppe an, die Sie dem Ziel-Datenfluss hinzufügen. Beachten Sie, dass dieses Feld nicht obligatorisch ist und Sie dem Ziel-Datenfluss erfolgreich eine Zielgruppe hinzufügen können, ohne ihren Namen anzugeben. |
| `filenameTemplate` | Nur *Batch* Ziele. Dieses Feld ist nur erforderlich, wenn eine Zielgruppe zu einem Datenfluss in Batch-Dateiexportzielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br> Dieses Feld bestimmt das Dateinamenformat der Dateien, die an Ihr Ziel exportiert werden. <br> Die folgenden Optionen sind verfügbar: <br> <ul><li>`%DESTINATION_NAME%`: Obligatorisch. Die exportierten Dateien enthalten den Zielnamen.</li><li>`%SEGMENT_ID%`: Obligatorisch. Die exportierten Dateien enthalten die ID der exportierten Zielgruppe.</li><li>`%SEGMENT_NAME%`: **(optional)**. Die exportierten Dateien enthalten den Namen der exportierten Zielgruppe.</li><li>`DATETIME(YYYYMMdd_HHmmss)` oder `%TIMESTAMP%`: **(Optional)**. Wählen Sie eine dieser beiden Optionen für Ihre Dateien aus, um den Zeitpunkt einzuschließen, zu dem sie von Experience Platform generiert werden.</li><li>`custom-text`: **(optional)**. Ersetzen Sie diesen Platzhalter durch einen beliebigen benutzerdefinierten Text, den Sie am Ende Ihrer Dateinamen anhängen möchten.</li></ul> <br> Weitere Informationen zur Konfiguration von Dateinamen finden Sie im Abschnitt [Konfigurieren von Dateinamen](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) im Tutorial zur Aktivierung von Batch-Zielen. |
| `exportMode` | Nur *Batch* Ziele. Dieses Feld ist nur erforderlich, wenn eine Zielgruppe zu einem Datenfluss in Batch-Dateiexportzielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br>. Wählen Sie `"DAILY_FULL_EXPORT"` oder `"FIRST_FULL_THEN_INCREMENTAL"` aus. Weitere Informationen zu den beiden Optionen finden Sie unter [Exportieren von vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Exportieren von inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) im Tutorial zur Aktivierung von Batch-Zielen. |
| `startDate` | Wählen Sie das Datum aus, an dem die Zielgruppe Profile in Ihr Ziel exportieren soll. |
| `frequency` | Nur *Batch* Ziele. Dieses Feld ist nur erforderlich, wenn eine Zielgruppe zu einem Datenfluss in Batch-Dateiexportzielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br>. <br> <ul><li>Für den Exportmodus `"DAILY_FULL_EXPORT"` können Sie `ONCE` oder `DAILY` wählen.</li><li>Für den Exportmodus `"FIRST_FULL_THEN_INCREMENTAL"` können Sie `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"` wählen.</li></ul> |
| `triggerType` | Nur *Batch* Ziele. Dieses Feld ist nur erforderlich, wenn Sie den `"DAILY_FULL_EXPORT"` im `frequency` auswählen. <br>. <br> <ul><li>Wählen Sie `"AFTER_SEGMENT_EVAL"` aus, damit der Aktivierungsvorgang unmittelbar nach Abschluss des täglichen Experience Platform-Batch-Segmentierungsvorgangs ausgeführt wird. Dadurch wird sichergestellt, dass bei der Ausführung des Aktivierungsvorgangs die aktuellen Profile nach Ihrem Ziel exportiert werden.</li><li>Wählen Sie `"SCHEDULED"` aus, damit der Aktivierungsvorgang zu einem festen Zeitpunkt ausgeführt wird. Dadurch wird sichergestellt, dass Experience Platform-Profildaten jeden Tag zur gleichen Zeit exportiert werden. Die Profile, die Sie exportieren, entsprechen jedoch möglicherweise nicht dem neuesten Stand. Dies hängt davon ab, ob der Batch-Segmentierungsvorgang vor dem Start des Aktivierungsvorgangs abgeschlossen wurde. Wenn Sie diese Option auswählen, müssen Sie auch eine `startTime` hinzufügen, um anzugeben, zu welchem Zeitpunkt in UTC die täglichen Exporte stattfinden sollen.</li></ul> |
| `endDate` | Nur *Batch* Ziele. Dieses Feld ist nur erforderlich, wenn eine Zielgruppe zu einem Datenfluss in Batch-Dateiexportzielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br> Nicht anwendbar bei der Auswahl von `"exportMode":"DAILY_FULL_EXPORT"` und `"frequency":"ONCE"`. <br> Legt das Datum fest, ab dem Zielgruppenmitglieder nicht mehr in das Ziel exportiert werden. |
| `startTime` | Nur *Batch* Ziele. Dieses Feld ist nur erforderlich, wenn eine Zielgruppe zu einem Datenfluss in Batch-Dateiexportzielen wie Amazon S3, SFTP oder Azure Blob hinzugefügt wird. <br>. Wählen Sie den Zeitpunkt aus, zu dem Dateien mit Mitgliedern der Zielgruppe generiert und an Ihr Ziel exportiert werden sollen. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Entfernen einer Zielgruppe aus einem Datenfluss {#remove-segment}

Um eine Zielgruppe aus einem vorhandenen Ziel-Datenfluss zu entfernen, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API durch und geben Sie dabei Ihre Fluss-ID, die Version und den Indexselektor der Zielgruppe an, die Sie entfernen möchten. Die Indizierung beginnt bei `0`. Beispielsweise entfernt die weiter unten stehende Beispielanfrage die erste und zweite Zielgruppe aus dem Datenfluss.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Die folgende Anfrage entfernt zwei Zielgruppen aus einem vorhandenen Ziel-Datenfluss.

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
   "path":"/transformations/0/params/segmentSelectors/selectors/0",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"/transformations/0/params/segmentSelectors/selectors/1",
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
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um eine Zielgruppe aus einem Datenfluss zu entfernen, verwenden Sie den Vorgang `remove` . |
| `path` | Gibt basierend auf dem Index des Zielgruppen-Selektors an, welche vorhandene Zielgruppe aus dem Ziel-Datenfluss entfernt werden soll. Um die Reihenfolge der Zielgruppen in einem Datenfluss abzurufen, führen Sie einen GET-Aufruf an den `/flows`-Endpunkt durch und überprüfen Sie die `transformations.segmentSelectors`. Um die erste Zielgruppe im Datenfluss zu löschen, verwenden Sie `"path":"/transformations/0/params/segmentSelectors/selectors/0"`. |


**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Aktualisieren von Komponenten einer Audience in einem Datenfluss {#update-segment}

Sie können Komponenten einer Zielgruppe in einem vorhandenen Ziel-Datenfluss aktualisieren. Beispielsweise können Sie die Exportfrequenz ändern oder die Dateinamenvorlage bearbeiten. Führen Sie dazu eine PATCH-Anfrage an die [!DNL Flow Service]-API durch und geben Sie dabei Ihre Fluss-ID, Version und den Indexselektor der Zielgruppe an, die Sie aktualisieren möchten. Die Indizierung beginnt bei `0`. Beispielsweise aktualisiert die nachstehende Anfrage die neunte Zielgruppe in einem Datenfluss.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Beim Aktualisieren einer Zielgruppe in einem vorhandenen Ziel-Datenfluss sollten Sie zunächst einen GET-Vorgang ausführen, um die Details der Zielgruppe abzurufen, die Sie aktualisieren möchten. Geben Sie dann alle Zielgruppeninformationen in der Payload an, nicht nur die Felder, die Sie aktualisieren möchten. Im folgenden Beispiel wird benutzerdefinierter Text am Ende der Dateinamenvorlage hinzugefügt und die Häufigkeit des Exportplans wird von 6 auf 12 Stunden aktualisiert.

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

Beschreibungen der Eigenschaften in der Payload finden Sie im Abschnitt [Hinzufügen einer Audience zu einem Datenfluss](#add-segment).


**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

In den folgenden Beispielen finden Sie weitere Beispiele für Zielgruppenkomponenten, die Sie in einem Datenfluss aktualisieren können.

## Aktualisieren des Exportmodus einer Zielgruppe von „Geplant“ in „Nach Zielgruppenbewertung“ {#update-export-mode}

+++ Klicken Sie hier, um ein Beispiel zu sehen, bei dem ein Zielgruppenexport nicht mehr jeden Tag zum angegebenen Zeitpunkt aktiviert wird, sondern jeden Tag nach Abschluss des Experience Platform-Batch-Segmentierungsvorgangs.

Die Zielgruppe wird täglich um 16:00 Uhr UTC :00.

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

Die Zielgruppe wird jeden Tag exportiert, nachdem der tägliche Batch-Segmentierungsauftrag abgeschlossen wurde.

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

## Aktualisieren Sie die Dateinamenvorlage, um zusätzliche Felder in den Dateinamen aufzunehmen {#update-filename-template}

+++ Klicken Sie hier, um ein Beispiel zu sehen, bei dem die Dateinamenvorlage aktualisiert wird, um zusätzliche Felder in den Dateinamen aufzunehmen

Die exportierten Dateien enthalten den Zielnamen und die Experience Platform-Zielgruppen-ID

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

Die exportierten Dateien enthalten den Zielnamen, die Experience Platform-Zielgruppen-ID, das Datum und die Uhrzeit der Dateigenerierung durch Experience Platform sowie benutzerdefinierten Text, der am Ende der Dateien angehängt wird.


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

Um ein Profilattribut zum Ziel-Datenfluss hinzuzufügen, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API aus und geben Sie dabei Ihre Fluss-ID, Version und das Profilattribut an, das Sie hinzufügen möchten.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Die folgende Anfrage fügt einem vorhandenen Ziel-Datenfluss ein neues Profilattribut hinzu.

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
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um ein Profilattribut zu einem Datenfluss hinzuzufügen, verwenden Sie den `add` . |
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

Um ein Profilattribut aus einem vorhandenen Ziel-Datenfluss zu entfernen, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API aus und geben Sie dabei Ihre Fluss-ID, Version und den Indexselektor des Profilattributs an, das Sie entfernen möchten. Die Indizierung beginnt bei `0`. Beispielsweise entfernt die weiter unten stehende Beispielanfrage das fünfte Profilattribut aus dem Datenfluss.


**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Die folgende Anfrage entfernt ein Profilattribut aus einem vorhandenen Ziel-Datenfluss.

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
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um eine Zielgruppe aus einem Datenfluss zu entfernen, verwenden Sie den Vorgang `remove` . |
| `path` | Gibt an, welches vorhandene Profilattribut basierend auf dem Index des Zielgruppenselektors aus dem Zieldatenfluss entfernt werden soll. Um die Reihenfolge der Profilattribute in einem Datenfluss abzurufen, führen Sie einen GET-Aufruf an den `/flows`-Endpunkt durch und überprüfen Sie die `transformations.profileSelectors`. Um die erste Zielgruppe im Datenfluss zu löschen, verwenden Sie `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Weitere Informationen [&#x200B; Interpretieren von Fehlerantworten finden Sie unter &#x200B;](/help/landing/troubleshooting.md#api-status-codes)API-Status-Codes[&#x200B; und &#x200B;](/help/landing/troubleshooting.md#request-header-errors)Fehler in der Anfragekopfzeile im Handbuch zur Fehlerbehebung bei Experience Platform .

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie gelernt, wie Sie verschiedene Komponenten eines Ziel-Datenflusses aktualisieren können, z. B. Zielgruppen oder Profilattribute mithilfe [!DNL Flow Service] API hinzufügen oder entfernen. Weitere Informationen zu Zielen finden Sie unter [Ziele - Übersicht](../home.md).
