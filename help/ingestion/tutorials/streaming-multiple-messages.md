---
keywords: Experience Platform;Startseite;beliebte Themen;Streaming-Aufnahme;Aufnahme;Streaming mehrerer Nachrichten;mehrere Nachrichten;
solution: Experience Platform
title: Senden mehrerer Nachrichten in einer einzigen HTTP-Anfrage
type: Tutorial
description: Dieses Dokument enthält ein Tutorial zum Senden mehrerer Nachrichten an Adobe Experience Platform innerhalb einer einzigen HTTP-Anfrage mithilfe der Streaming-Aufnahme.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 31c00e69dd92f7c3232e09f02da36c60cd8cf486
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 58%

---

# Senden mehrerer Nachrichten in einer einzigen HTTP-Anfrage

Beim Streaming von Daten an Adobe Experience Platform kann das Ausführen zahlreicher HTTP-Aufrufe teuer werden. Anstatt beispielsweise 200 HTTP-Anfragen mit Payloads von 1 KB zu erstellen, ist es viel effizienter, 1 HTTP-Anfrage mit 200 Nachrichten mit jeweils 1 KB und einer Payload von 200 KB zu erstellen. Bei richtiger Verwendung stellt das Gruppieren mehrerer Nachrichten in einer Anfrage eine hervorragende Möglichkeit dar, um die an [!DNL Experience Platform] gesendeten Daten zu optimieren.

Dieses Dokument enthält ein Tutorial zum Senden mehrerer Nachrichten an [!DNL Experience Platform] innerhalb einer einzelnen HTTP-Anfrage mithilfe der Streaming-Aufnahme.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der Adobe Experience Platform-[!DNL Data Ingestion] voraus. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

- [Übersicht über die Datenaufnahme](../home.md): Behandelt die grundlegenden Konzepte der [!DNL Experience Platform Data Ingestion], einschließlich Aufnahmemethoden und Daten-Connectoren.
- [Streaming-Aufnahme - &#x200B;](../streaming-ingestion/overview.md): Der Workflow und die Bausteine der Streaming-Aufnahme, wie Streaming-Verbindungen, Datensätze, [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent].

Für dieses Tutorial müssen Sie auch das Tutorial [Authentifizierung bei Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Experience Platform] APIs erfolgreich aufrufen zu können. Durch Abschließen des Authentifizierungs-Tutorials erhalten Sie den Wert für die Autorisierungs-Kopfzeile, der für alle API-Aufrufe in diesem Tutorial erforderlich ist. Die Kopfzeile wird in Beispielaufrufen wie folgt angezeigt:

- Authorization: Bearer `{ACCESS_TOKEN}`

Für alle POST-Anfragen ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Aufbauen einer Streaming-Verbindung

Sie müssen zunächst eine Streaming-Verbindung erstellen, bevor Sie mit dem Streaming von Daten an [!DNL Experience Platform] beginnen können. Lesen Sie die Anleitung zum [Aufbauen einer Streaming-Verbindung](./create-streaming-connection.md), um zu erfahren, wie Sie eine Streaming-Verbindung aufbauen.

Nach der Registrierung einer Streaming-Verbindung verfügen Sie als Datenproduzent über eine eindeutige URL, mit der Daten an Experience Platform gestreamt werden können.

## Streamen in einen Datensatz

Das folgende Beispiel zeigt, wie mehrere Nachrichten an einen bestimmten Datensatz innerhalb einer einzelnen HTTP-Anfrage gesendet werden. Fügen Sie die Datensatz-ID in die Kopfzeile der Nachricht ein, damit die Nachricht direkt darin aufgenommen wird.

Sie können die ID für einen vorhandenen Datensatz über die [!DNL Experience Platform]-Benutzeroberfläche oder einen Listenvorgang in der API abrufen. Die Datensatz-ID finden Sie auf [Experience Platform](https://platform.adobe.com), indem Sie auf die Registerkarte **[!UICONTROL Datasets]** klicken, auf den Datensatz klicken, für den Sie die ID haben möchten, und die Zeichenfolge aus dem Feld Datensatz-ID auf der Registerkarte **[!UICONTROL Info]** kopieren. Informationen zum Abrufen von Datensätzen mithilfe der API finden Sie unter [Katalogdienst – Überblick](../../catalog/home.md).

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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
- Das Feld `imsOrgId` in der Kopfzeile der Nachricht muss mit der Inlet-Definition übereinstimmen. Wenn die Anfrage-Payload kein `imsOrgId` Feld enthält, fügt das [!DNL Data Collection Core Service] (DCCS) das Feld automatisch hinzu.
- Die Kopfzeile der Nachricht sollte auf ein vorhandenes XDM-Schema verweisen, das in der [!DNL Experience Platform]-Benutzeroberfläche erstellt wurde.
- Das Feld `datasetId` muss auf einen vorhandenen Datensatz in [!DNL Experience Platform] verweisen, und sein Schema muss mit dem Schema übereinstimmen, das im `header`-Objekt in jeder Nachricht im Anfragetext bereitgestellt wird.

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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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

Die erste Nachricht wurde erfolgreich an [!DNL Experience Platform] gesendet und ist von den Ergebnissen der anderen Nachrichten nicht betroffen. Daher müssen Sie diese Nachricht nicht erneut einschließen, wenn Sie versuchen, die fehlgeschlagenen Nachrichten erneut zu senden.

Die zweite Nachricht schlug fehl, weil der Nachrichtentext fehlte. Die Erfassungsanfrage erwartet, dass Nachrichtenelemente gültige Kopfzeilen- und Textabschnitte aufweisen. Durch Hinzufügen des folgenden Codes nach der Kopfzeile in der zweiten Nachricht wird die Anfrage korrigiert, sodass die zweite Nachricht die Überprüfung besteht:

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

Die dritte Nachricht schlug aufgrund der Verwendung einer ungültigen Organisations-ID in der Kopfzeile fehl. Die Organisation muss mit der {CONNECTION_ID} übereinstimmen, an die Sie posten möchten. Um festzustellen, welche Organisations-ID mit der von Ihnen verwendeten Streaming-Verbindung übereinstimmt, können Sie eine `GET inlet` mithilfe der [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) ausführen. Ein Beispiel zum Abrufen zuvor erstellter Streaming-Verbindungen finden Sie unter [Abrufen einer Streaming-Verbindung](./create-streaming-connection.md#get-data-collection-url).

Die vierte Meldung ist fehlgeschlagen, da sie nicht dem erwarteten XDM-Schema entsprach. Das `xdmSchema`, das in der Kopfzeile und im Text der Anfrage enthalten ist, stimmt nicht mit dem XDM-Schema der `{DATASET_ID}` überein. Wenn Sie das Schema in der Kopfzeile und im Hauptteil der Nachricht korrigieren, kann es die DCCS-Validierung bestehen und erfolgreich an [!DNL Experience Platform] gesendet werden. Außerdem muss der Nachrichtentext so aktualisiert werden, dass er dem XDM-Schema des `{DATASET_ID}` entspricht, damit die Streaming-Validierung bei [!DNL Experience Platform] erfolgreich ist. Weiterführende Informationen dazu, was mit Nachrichten passiert, die erfolgreich an Experience Platform gestreamt werden, finden [&#x200B; im Abschnitt &quot;](#confirm-messages-ingested) aufgenommener Nachrichten bestätigen“ dieses Tutorials.

### Abrufen fehlgeschlagener Nachrichten von [!DNL Experience Platform]

Fehlgeschlagene Nachrichten werden durch einen Fehlerstatus-Code im Antwort-Array identifiziert.
Die ungültigen Nachrichten werden in einem „Fehler“-Batch innerhalb des von der `{DATASET_ID}` angegebenen Datensatzes erfasst und gespeichert.

Weitere Informationen zum Wiederherstellen von fehlgeschlagenen Batch-Nachrichten finden Sie der Anleitung zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

## Bestätigen von aufgenommenen Nachrichten

Nachrichten, die die DCCS-Validierung bestehen, werden an [!DNL Experience Platform] gestreamt. [!DNL Experience Platform] werden die Batch-Nachrichten durch Streaming-Validierung getestet, bevor sie in die [!DNL Data Lake] aufgenommen werden. Der Status von Batches, ob erfolgreich oder nicht, wird in dem von der `{DATASET_ID}` angegebenen Datensatz angezeigt.

Sie können den Status von Batch-Nachrichten, die erfolgreich an [!DNL Experience Platform] gestreamt wurden, mithilfe der [Experience Platform](https://platform.adobe.com)Benutzeroberfläche anzeigen, indem Sie zur Registerkarte **[!UICONTROL Datasets]** gehen, auf den Datensatz klicken, an den Sie streamen, und die Registerkarte **[!UICONTROL Dataset Activity]** überprüfen.

Batch-Nachrichten, die bei der Streaming-Validierung [!DNL Experience Platform] erfolgreich sind, werden in die [!DNL Data Lake] aufgenommen. Die Nachrichten stehen dann für die Analyse oder den Export zur Verfügung.

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie mehrere Nachrichten in einer einzigen Anfrage senden und überprüfen können, wann Nachrichten erfolgreich in den Zieldatensatz aufgenommen wurden, können Sie damit beginnen, Ihre eigenen Daten an [!DNL Experience Platform] zu streamen. Eine Übersicht darüber, wie Sie aufgenommene Daten von [!DNL Experience Platform] abfragen und abrufen können, finden Sie im [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zum Tutorial.

### Antwort-Codes

Die folgende Tabelle zeigt Status-Codes, die von erfolgreichen und fehlgeschlagenen Antwortnachrichten zurückgegeben werden.

| Status-Code | Beschreibung |
| :---: | --- |
| 207 | Obwohl „207“ als Code für den Gesamtantwortstatus verwendet wird, muss der Empfänger den Inhalt des Antworttextes mit mehreren Status konsultieren, um weitere Informationen über den Erfolg oder Misserfolg der Methodenausführung zu erhalten. Der Antwort-Code wird in Erfolgs-, Teilerfolgs- wie auch in Fehlersituationen verwendet. |
| 400 | Es gab ein Problem mit der Anfrage. Im Antworttext finden Sie eine spezifischere Fehlermeldung (z. B. fehlten in der Nachrichten-Payload erforderliche Felder oder die Nachricht hatte ein unbekanntes xdm-Format). |
| 401 | Nicht autorisiert: Bei der Anfrage fehlt eine gültige Autorisierungskopfzeile. Dies wird nur bei Inlets zurückgegeben, für die die Authentifizierung aktiviert ist. |
| 403 | Nicht autorisiert: Das angegebene Autorisierungs-Token ist ungültig oder abgelaufen. Dies wird nur bei Inlets zurückgegeben, für die die Authentifizierung aktiviert ist. |
| 413 | Payload zu groß – Wird ausgelöst, wenn die Payload-Anfrage insgesamt größer als 1 MB ist. |
| 429 | Zu viele Anfragen innerhalb der angegebenen Zeitdauer. |
| 500 | Fehler bei der Verarbeitung der Payload. Im Antworttext finden Sie eine spezifischere Fehlermeldung (z. B. das Nachrichten-Payload-Schema nicht angegeben oder stimmte nicht mit der XDM-Definition in [!DNL Experience Platform] überein). |
| 503 | Der Service ist derzeit nicht verfügbar. Kunden sollten es mindestens dreimal mit einer exponentiellen Back-off-Strategie versuchen. |
