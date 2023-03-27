---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming-Erfassung; Erfassung; Streaming mehrerer Nachrichten; mehrere Nachrichten;
solution: Experience Platform
title: Senden mehrerer Nachrichten in einer einzelnen HTTP-Anfrage
type: Tutorial
description: Dieses Dokument enthält ein Tutorial zum Senden mehrerer Nachrichten an Adobe Experience Platform in einer einzelnen HTTP-Anfrage mithilfe der Streaming-Erfassung.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 3ad5c06db07b360df255d3afb1c177cc5de613bb
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 65%

---

# Mehrere Nachrichten in einer einzelnen HTTP-Anfrage senden

Beim Streaming von Daten an Adobe Experience Platform kann das Ausführen zahlreicher HTTP-Aufrufe teuer werden. Anstatt beispielsweise 200 HTTP-Anfragen mit Payloads von 1 KB zu erstellen, ist es viel effizienter, 1 HTTP-Anfrage mit 200 Nachrichten mit jeweils 1 KB und einer Payload von 200 KB zu erstellen. Bei korrekter Verwendung ist die Gruppierung mehrerer Nachrichten in einer einzigen Anfrage eine hervorragende Möglichkeit, die gesendeten Daten zu optimieren [!DNL Experience Platform].

Dieses Dokument enthält ein Tutorial zum Senden mehrerer Nachrichten an [!DNL Experience Platform] in einer einzelnen HTTP-Anfrage mithilfe der Streaming-Erfassung.

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis von Adobe Experience Platform voraus [!DNL Data Ingestion]. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

- [Datenerfassung - Übersicht](../home.md): Behandelt die Kernkonzepte von [!DNL Experience Platform Data Ingestion], einschließlich Erfassungsmethoden und Data Connectors.
- [Streaming-Erfassung - Übersicht](../streaming-ingestion/overview.md): Workflow und Bausteine der Streaming-Erfassung, wie Streaming-Verbindungen, Datensätze, [!DNL XDM Individual Profile]und [!DNL XDM ExperienceEvent].

Für dieses Tutorial müssen Sie außerdem das Tutorial [Authentifizierung für Adobe Experience ](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um erfolgreich Aufrufe an Platform-APIs durchführen zu können.[!DNL Platform] Durch Abschließen des Authentifizierungs-Tutorials erhalten Sie den Wert für die Autorisierungs-Kopfzeile, der für alle API-Aufrufe in diesem Tutorial erforderlich ist. Die Kopfzeile wird in Beispielaufrufen wie folgt angezeigt:

- Authorization: Bearer `{ACCESS_TOKEN}`

Für alle POST-Anfragen ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Aufbauen einer Streaming-Verbindung

Sie müssen zunächst eine Streaming-Verbindung erstellen, bevor Sie mit dem Streaming von Daten an beginnen können [!DNL Experience Platform]. Lesen Sie die Anleitung zum [Aufbauen einer Streaming-Verbindung](./create-streaming-connection.md), um zu erfahren, wie Sie eine Streaming-Verbindung aufbauen.

Nach der Registrierung einer Streaming-Verbindung haben Sie als Datenproduzent eine eindeutige URL, die zum Streamen von Daten an Platform verwendet werden kann.

## Streamen in einen Datensatz

Das folgende Beispiel zeigt, wie mehrere Nachrichten an einen bestimmten Datensatz innerhalb einer einzelnen HTTP-Anfrage gesendet werden. Fügen Sie die Datensatz-ID in die Kopfzeile der Nachricht ein, damit die Nachricht direkt darin aufgenommen wird.

Sie können die ID für einen vorhandenen Datensatz mit der [!DNL Platform] Benutzeroberfläche oder Verwendung eines Auflistungsvorgangs in der API. Die Datensatz-ID finden Sie unter [Experience Platform](https://platform.adobe.com) durch **[!UICONTROL Datensätze]** auf den Datensatz, für den die ID verwendet werden soll, klicken und den String aus dem Feld Datensatz-ID auf **[!UICONTROL Info]** Registerkarte. Informationen zum Abrufen von Datensätzen mithilfe der API finden Sie unter [Katalogdienst – Überblick](../../catalog/home.md).

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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
- Die Kopfzeile der Nachricht sollte auf ein vorhandenes XDM-Schema verweisen, das im [!DNL Platform] Benutzeroberfläche.
- Die `datasetId` -Feld muss auf einen vorhandenen Datensatz in verweisen [!DNL Platform]und das zugehörige Schema mit dem Schema übereinstimmen muss, das im `header` -Objekt in jeder Nachricht im Anfrageinhalt.

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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

Die obige Beispielantwort zeigt Fehlermeldungen für die vorherige Anfrage. Ein Vergleich dieser Antwort mit der vorherigen gültigen Antwort ergibt, dass die Anfrage teilweise erfolgreich war. Eine Nachricht wurde erfolgreich aufgenommen und drei Nachrichten führten zu einem Fehler. Beachten Sie, dass beide Antworten den Status-Code „207“ zurückgeben. Weitere Informationen zu Status-Codes finden Sie in der Tabelle zu [Antwort-Codes](#response-codes) im Anhang dieses Tutorials.

Die erste Nachricht wurde erfolgreich gesendet an [!DNL Platform] und ist von den Ergebnissen der anderen Nachrichten nicht betroffen. Daher müssen Sie diese Nachricht nicht erneut einschließen, wenn Sie versuchen, die fehlgeschlagenen Nachrichten erneut zu senden.

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

Die dritte Nachricht schlug fehl, weil in der Kopfzeile eine ungültige Organisations-ID verwendet wurde. Die Organisation muss mit der {CONNECTION_ID} übereinstimmen, in der Sie veröffentlichen möchten. Um festzustellen, welche Organisations-ID mit der verwendeten Streaming-Verbindung übereinstimmt, können Sie eine `GET inlet` -Anfrage mithilfe der [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). Ein Beispiel zum Abrufen zuvor erstellter Streaming-Verbindungen finden Sie unter [Abrufen einer Streaming-Verbindung](./create-streaming-connection.md#get-data-collection-url).

Die vierte Meldung ist fehlgeschlagen, da sie nicht dem erwarteten XDM-Schema entsprach. Das `xdmSchema`, das in der Kopfzeile und im Text der Anfrage enthalten ist, stimmt nicht mit dem XDM-Schema der `{DATASET_ID}` überein. Durch das Korrigieren des Schemas in der Kopfzeile und im Nachrichtentext kann die DCCS-Validierung bestehen und erfolgreich an gesendet werden [!DNL Platform]. Der Nachrichtentext muss ebenfalls aktualisiert werden, um mit dem XDM-Schema der `{DATASET_ID}` , damit die Streaming-Validierung an [!DNL Platform]. Weitere Informationen zu Nachrichten, die erfolgreich an Platform gesendet werden, finden Sie im Abschnitt [Bestätigen von aufgenommenen Nachrichten](#confirm-messages-ingested) in diesem Tutorial.

### Abrufen von Fehlermeldungen von [!DNL Platform]

Fehlgeschlagene Nachrichten werden durch einen Fehlerstatus-Code im Antwort-Array identifiziert.
Die ungültigen Nachrichten werden in einem „Fehler“-Batch innerhalb des von der `{DATASET_ID}` angegebenen Datensatzes erfasst und gespeichert.

Weitere Informationen zum Wiederherstellen von fehlgeschlagenen Batch-Nachrichten finden Sie der Anleitung zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

## Bestätigen von aufgenommenen Nachrichten

Nachrichten, die die DCCS-Validierung bestehen, werden an gestreamt [!DNL Platform]. on [!DNL Platform], werden die Batch-Nachrichten durch Streaming-Validierung getestet, bevor sie in die [!DNL Data Lake]. Der Status von Batches, ob erfolgreich oder nicht, wird in dem von der `{DATASET_ID}` angegebenen Datensatz angezeigt.

Sie können den Status von Batch-Nachrichten anzeigen, die erfolgreich an gestreamt wurden [!DNL Platform] mithilfe der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com) durch **[!UICONTROL Datensätze]** Registerkarte auf den Datensatz klicken, an den Sie streamen, und die **[!UICONTROL Datensatzaktivität]** Registerkarte.

Batch-Nachrichten, die die Streaming-Validierung bestehen [!DNL Platform] werden in die [!DNL Data Lake]. Die Nachrichten stehen dann für die Analyse oder den Export zur Verfügung.

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie mehrere Nachrichten in einer einzigen Anfrage senden und überprüfen können, ob die Nachrichten erfolgreich in den Zieldatensatz aufgenommen wurden, können Sie mit dem Streaming Ihrer eigenen Daten an beginnen. [!DNL Platform]. Einen Überblick darüber, wie Sie aufgenommene Daten aus abfragen und abrufen können [!DNL Platform], siehe [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) Handbuch.

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zum Tutorial.

### Antwort-Codes

Die folgende Tabelle zeigt Status-Codes, die von erfolgreichen und fehlgeschlagenen Antwortnachrichten zurückgegeben werden.

| Status-Code | Beschreibung |
| :---: | --- |
| 207 | Obwohl &quot;207&quot;als Gesamt-Antwortstatus-Code verwendet wird, muss der Empfänger den Inhalt des Antworttextes mit mehreren Status konsultieren, um weitere Informationen über den Erfolg oder das Fehlschlagen der Methodenausführung zu erhalten. Der Antwort-Code wird in Erfolgs-, Teilerfolgs- wie auch in Fehlersituationen verwendet. |
| 400 | Es gab ein Problem mit der Anfrage. Im Antworttext finden Sie eine spezifischere Fehlermeldung (z. B. fehlten in der Nachrichten-Payload erforderliche Felder oder die Nachricht hatte ein unbekanntes xdm-Format). |
| 401 | Nicht autorisiert: Bei der Anfrage fehlt eine gültige Autorisierungskopfzeile. Dies wird nur bei Inlets zurückgegeben, für die die Authentifizierung aktiviert ist. |
| 403 | Nicht autorisiert: Das angegebene Autorisierungs-Token ist ungültig oder abgelaufen. Dies wird nur bei Inlets zurückgegeben, für die die Authentifizierung aktiviert ist. |
| 413 | Payload zu groß – Wird ausgelöst, wenn die Payload-Anfrage insgesamt größer als 1 MB ist. |
| 429 | Zu viele Anfragen innerhalb der angegebenen Zeitdauer. |
| 500 | Fehler bei der Verarbeitung der Payload. Im Antworttext finden Sie eine spezifischere Fehlermeldung (z. B. das Nachrichten-Payload-Schema wurde nicht angegeben oder entsprach nicht der XDM-Definition in [!DNL Platform]). |
| 503 | Der Service ist derzeit nicht verfügbar. Kunden sollten es mindestens dreimal mit einer exponentiellen Back-off-Strategie versuchen. |
