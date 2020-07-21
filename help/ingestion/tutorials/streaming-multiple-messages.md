---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming mehrerer Nachrichten in einer einzelnen HTTP-Anfrage
topic: tutorial
translation-type: tm+mt
source-git-commit: 80392190c7fcae9b6e73cc1e507559f834853390
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 75%

---


# Senden mehrerer Nachrichten in einer einzelnen HTTP-Anfrage

Beim Streaming von Daten an Adobe Experience Platform können mehrfache HTTP-Aufrufe teuer sein. Anstatt beispielsweise 200 HTTP-Anfragen mit 1-KB-Payloads zu erstellen, ist es deutlich effizienter, eine HTTP-Anfrage mit 200 jeweils 1 KB großen Nachrichten und einer einzelnen Payload von 200 KB anzulegen. When used correctly, grouping multiple messages within a single request is an excellent way to optimize data being sent to [!DNL Experience Platform].

This document provides a tutorial for sending multiple messages to [!DNL Experience Platform] within a single HTTP request using streaming ingestion.

## Erste Schritte

This tutorial requires a working understanding of Adobe Experience Platform [!DNL Data Ingestion]. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

- [Dateneinbettung - Übersicht](../home.md): Behandelt die Kernkonzepte von [!DNL Experience Platform Data Ingestion]einschließlich Erfassungsmethoden und Data Connectors.
- [Übersicht](../streaming-ingestion/overview.md)zur Streaming-Erfassung: Arbeitsablauf und Bausteine der Streaming-Erfassung, wie Streaming-Verbindungen, Datasets [!DNL XDM Individual Profile]und [!DNL XDM ExperienceEvent].

Für dieses Tutorial müssen Sie außerdem das Tutorial [Authentifizierung für Adobe Experience ](../../tutorials/authentication.md) abgeschlossen haben, um erfolgreich Aufrufe an Platform-APIs durchführen zu können. [!DNL Platform] Durch Abschließen des Authentifizierungs-Tutorials erhalten Sie den Wert für die Autorisierungs-Kopfzeile, der für alle API-Aufrufe in diesem Tutorial erforderlich ist. Die Kopfzeile wird in Beispielaufrufen wie folgt angezeigt:

- Autorisierung: Träger `{ACCESS_TOKEN}`

Für alle POST-Anfragen ist eine zusätzliche Kopfzeile erforderlich:

- Inhaltstyp: application/json

## Aufbauen einer Streaming-Verbindung

You must first create a streaming connection before you can start streaming data to [!DNL Experience Platform]. Lesen Sie die Anleitung zum [Aufbauen einer Streaming-Verbindung](./create-streaming-connection.md), um zu erfahren, wie Sie eine Streaming-Verbindung aufbauen.

Nach der Registrierung einer Streaming-Verbindung haben Sie als Datenproduzent eine eindeutige URL, die zum Streamen von Daten an Platform verwendet werden kann.

## Streamen in einen Datensatz

Das folgende Beispiel zeigt, wie mehrere Nachrichten an einen bestimmten Datensatz innerhalb einer einzelnen HTTP-Anfrage gesendet werden. Fügen Sie die Datensatz-ID in die Kopfzeile der Nachricht ein, damit die Nachricht direkt darin aufgenommen wird.

You can get the ID for an existing dataset using the [!DNL Platform] UI or using a listing operation in the API. Sie können die Datensatz-ID in [Experience Platform](https://platform.adobe.com) auf der Registerkarte **[!UICONTROL Datensätze]** ermitteln, indem Sie auf den Datensatz klicken, für den die ID verwendet werden soll, und die Zeichenfolge aus dem Feld **[!UICONTROL Datensatz-ID]** auf der Registerkarte **[!UICONTROL Info]** kopieren. Informationen zum Abrufen von Datensätzen mithilfe der API finden Sie unter [Katalogdienst – Überblick](../../catalog/home.md).

Anstatt einen vorhandenen Datensatz zu verwenden, können Sie einen neuen Datensatz erstellen. Weitere Informationen zum Erstellen eines Datensatzes mithilfe von APIs finden Sie im Tutorial [Erstellen eines Datensatzes mithilfe von APIs](../../catalog/api/create-dataset.md).

**API-Format**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{CONNECTION_ID}` | Die ID der erstellten Streaming-Verbindung. |

**Anfrage**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Fernie Snow",
              "quantity": 30,
              "priceTotal": 7.8
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 207 (Multi-Status) zurück. Bei der Überprüfung des Antworttextes werden weitere Details zum Erfolg oder Misserfolg der einzelnen in der Anfrage ausgeführten Methoden angezeigt. Für jedes Element des Anfragemeldungs-Arrays wird eine Antwort zurückgegeben. Nachfolgend sehen Sie ein Beispiel für eine erfolgreiche Antwort ohne Nachrichtenfehler:

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

Weitere Informationen zu Status-Codes finden Sie in der Tabelle zu [Antwort-Codes](#response-codes) im Anhang dieses Tutorials.

## Identifizieren von fehlgeschlagenen Nachrichten

Im Vergleich zum Senden einer Anfrage mit einer einzelnen Nachricht gibt es beim Senden einer HTTP-Anfrage mit mehreren Nachrichten weitere Faktoren, die in Betracht gezogen werden sollten, z. B. wie zu identifizieren ist, wann Daten nicht gesendet wurden, welche spezifischen Nachrichten nicht gesendet wurden und wie sie abgerufen werden können und was mit Daten passiert, die erfolgreich sind, wenn andere Nachrichten in derselben Anfrage fehlschlagen.

Bevor Sie mit diesem Tutorial fortfahren, sollten Sie zunächst das Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md) lesen.

### Senden von Anfrage-Payload mit gültigen und ungültigen Nachrichten

Das folgende Beispiel zeigt, was passiert, wenn der Batch gültige und ungültige Meldungen enthält.

Die Anfrage-Payload ist ein Array von JSON-Objekten, die das Ereignis im XDM-Schema darstellen. Beachten Sie, dass für eine erfolgreiche Validierung der Nachricht folgende Bedingungen erfüllt sein müssen:
- Das Feld `imsOrgId` in der Kopfzeile der Nachricht muss mit der Inlet-Definition übereinstimmen. Wenn die Anfrage-Payload das Feld `imsOrgId` nicht enthält, fügt der  (DCCS) das Feld automatisch hinzu.[!DNL Data Collection Core Service]
- The header of the message should reference an existing XDM schema created in the [!DNL Platform] UI.
- The `datasetId` field needs to reference an existing dataset in [!DNL Platform], and its schema needs to match the schema provided in the `header` object within each message included in the request body.

**API-Format**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{CONNECTION_ID}` | Die ID des erstellten Daten-Inlets. |

**Anfrage**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Antwort**

Die Antwort-Payload enthält einen Status für jede Nachricht zusammen mit einer GUID in der `xactionId`, die für die Verfolgung verwendet werden kann.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        }
    ]
}
```

Die obige Beispielantwort zeigt Fehlermeldungen für die vorherige Anfrage. Ein Vergleich dieser Antwort mit der vorherigen gültigen Antwort ergibt, dass die Anfrage teilweise erfolgreich war. Eine Nachricht wurde erfolgreich aufgenommen und drei Nachrichten führten zu einem Fehler. Beachten Sie, dass beide Antworten den Status-Code „207“ zurückgeben. Weitere Informationen zu Status-Codes finden Sie in der Tabelle zu [Antwort-Codes](#response-codes) im Anhang dieses Tutorials.

The first message was successfully sent to [!DNL Platform] and is not affected by the results of the other messages. Daher müssen Sie diese Nachricht nicht erneut einschließen, wenn Sie versuchen, die fehlgeschlagenen Nachrichten erneut zu senden.

Die zweite Nachricht schlug fehl, weil der Nachrichtentext fehlte. Die Erfassungsanfrage erwartet, dass Nachrichtenelemente gültige Kopfzeilen- und Textabschnitte aufweisen. Durch Hinzufügen des folgenden Codes nach der Kopfzeile in der zweiten Nachricht wird die Anfrage korrigiert, sodass die zweite Nachricht die Überprüfung besteht:

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

Die dritte Meldung ist fehlgeschlagen, da eine ungültige IMS-Organisations-ID in der Kopfzeile verwendet wird. Die IMS-Organisation muss mit der {CONNECTION_ID} übereinstimmen, auf der Sie veröffentlichen möchten. To determine which IMS organization ID matches the streaming connection you are using, you can perform a `GET inlet` request using the [!DNL Data Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml). Ein Beispiel zum Abrufen zuvor erstellter Streaming-Verbindungen finden Sie unter [Abrufen einer Streaming-Verbindung](./create-streaming-connection.md#get-data-collection-url).

Die vierte Meldung ist fehlgeschlagen, da sie nicht dem erwarteten XDM-Schema entsprach. Das `xdmSchema`, das in der Kopfzeile und im Text der Anfrage enthalten ist, stimmt nicht mit dem XDM-Schema der `{DATASET_ID}` überein. Correcting the schema in the message header and body allows it to pass DCCS validation and be successfully sent to [!DNL Platform]. The message body must also be updated to match the XDM schema of the `{DATASET_ID}` for it to pass streaming validation on [!DNL Platform]. Weitere Informationen zu Nachrichten, die erfolgreich an Platform gesendet werden, finden Sie im Abschnitt [Bestätigen von aufgenommenen Nachrichten](#confirm-messages-ingested) in diesem Tutorial.

### Abrufen von Fehlermeldungen von [!DNL Platform]

Fehlgeschlagene Nachrichten werden durch einen Fehlerstatus-Code im Antwort-Array identifiziert.
Die ungültigen Nachrichten werden in einem „Fehler“-Batch innerhalb des von der `{DATASET_ID}` angegebenen Datensatzes erfasst und gespeichert.

Weitere Informationen zum Wiederherstellen von fehlgeschlagenen Batch-Nachrichten finden Sie der Anleitung zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

## Bestätigen von aufgenommenen Nachrichten

Messages that pass DCCS validation are streamed to [!DNL Platform]. On [!DNL Platform], the batch messages are tested by streaming validation before being ingested into the [!DNL Data Lake]. Der Status von Batches, ob erfolgreich oder nicht, wird in dem von der `{DATASET_ID}` angegebenen Datensatz angezeigt.

You can view the status of batch messages that successfully stream to [!DNL Platform] using the [Experience Platform UI](https://platform.adobe.com) by going to the **[!UICONTROL Datasets]** tab, clicking on the dataset you are streaming to, and checking the **[!UICONTROL Dataset Activity]** tab.

Batch messages that pass streaming validation on [!DNL Platform] are ingested into the [!DNL Data Lake]. Die Nachrichten stehen dann für die Analyse oder den Export zur Verfügung.

## Nächste Schritte

Now that you know how to send multiple messages in a single request and verify when messages are successfully ingested into the target dataset, you can start streaming your own data to [!DNL Platform]. For an overview of how to query and retrieve ingested data from [!DNL Platform], see the [!DNL Data Access](../../data-access/tutorials/dataset-data.md) guide.

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zum Tutorial.

### Antwort-Codes

Die folgende Tabelle zeigt Status-Codes, die von erfolgreichen und fehlgeschlagenen Antwortnachrichten zurückgegeben werden.

| Status-Code | Beschreibung |
| :---: | --- |
| 207 | Obwohl „207“ als Gesamt-Antwortstatus-Code verwendet wird, muss der Empfänger den Inhalt des Multistatus-Antworttextes für weitere Informationen zum Erfolg oder Misserfolg der Methodenausführung konsultieren. Der Antwort-Code wird in Erfolgs-, Teilerfolgs- wie auch in Fehlersituationen verwendet. |
| 400 | Es gab ein Problem mit der Anfrage. Im Antworttext finden Sie eine spezifischere Fehlermeldung (z. B. fehlten in der Nachrichten-Payload erforderliche Felder oder die Nachricht hatte ein unbekanntes xdm-Format). |
| 401 | Nicht autorisiert: Bei der Anfrage fehlt eine gültige Autorisierungskopfzeile. Dies wird nur bei Inlets zurückgegeben, für die die Authentifizierung aktiviert ist. |
| 403 | Nicht autorisiert: Das angegebene Autorisierungs-Token ist ungültig oder abgelaufen. Dies wird nur bei Inlets zurückgegeben, für die die Authentifizierung aktiviert ist. |
| 413 | Payload zu groß – Wird ausgelöst, wenn die Payload-Anfrage insgesamt größer als 1 MB ist. |
| 429 | Zu viele Anfragen innerhalb der angegebenen Zeitdauer. |
| 500 | Fehler bei der Verarbeitung der Payload. Im Antworttext finden Sie eine spezifischere Fehlermeldung (z. B. das Nachrichten-Payload-Schema wurde nicht angegeben oder entsprach nicht der XDM-Definition in [!DNL Platform]). |
| 503 | Der Dienst ist derzeit nicht verfügbar. Kunden sollten es mindestens dreimal mit einer exponentiellen Back-off-Strategie versuchen. |