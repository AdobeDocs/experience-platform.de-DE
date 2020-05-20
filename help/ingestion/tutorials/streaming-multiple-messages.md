---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming mehrerer Nachrichten in einer einzelnen HTTP-Anforderung
topic: tutorial
translation-type: tm+mt
source-git-commit: cd251c0816a7e653596b6c3faaceb0cebad367ea
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 1%

---


# Senden mehrerer Nachrichten in einer einzelnen HTTP-Anforderung

Beim Streaming von Daten an Adobe Experience Platform können zahlreiche HTTP-Aufrufe teuer sein. Anstatt beispielsweise 200 HTTP-Anforderungen mit 1 KB Nutzlasten zu erstellen, ist es viel effizienter, 1 HTTP-Anforderung mit 200 Nachrichten mit jeweils 1 KB und einer Nutzlast von 200 KB zu erstellen. Bei korrekter Verwendung ist die Gruppierung mehrerer Nachrichten in einer einzigen Anforderung eine hervorragende Möglichkeit, Daten zu optimieren, die an Experience Platform gesendet werden.

Dieses Dokument bietet eine Anleitung zum Senden mehrerer Nachrichten an Experience Platform in einer einzigen HTTP-Anforderung mithilfe der Streaming-Erfassung.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der Adobe Experience Platform Data Ingestion. Bevor Sie dieses Lernprogramm beginnen, lesen Sie bitte die folgende Dokumentation:

- [Dateneinbettung - Übersicht](../home.md): Behandelt die Kernkonzepte der Experience Platform Data Ingestion, einschließlich Erfassungsmethoden und Data Connectors.
- [Übersicht](../streaming-ingestion/overview.md)zur Streaming-Erfassung: Der Arbeitsablauf und die Bausteine der Streaming-Erfassung, wie Streaming-Verbindungen, Datasets, XDM-Individuelles Profil und XDM ExperienceEvent.

Für dieses Lernprogramm müssen Sie außerdem das Lernprogramm &quot; [Authentifizierung für Adobe Experience Platform](../../tutorials/authentication.md) &quot;abgeschlossen haben, um erfolgreich Aufrufe an Plattform-APIs durchführen zu können. Das Abschließen des Authentifizierungslehrgangs stellt den Wert für den Autorisierungs-Header bereit, der für alle API-Aufrufe in diesem Lernprogramm erforderlich ist. Die Kopfzeile wird in Beispielaufrufen wie folgt angezeigt:

- Genehmigung: Träger `{ACCESS_TOKEN}`

Für alle POST-Anforderungen ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Erstellen einer Streaming-Verbindung

Sie müssen zunächst eine Streaming-Verbindung erstellen, bevor Sie Daten an Experience Platform Beginn-Streaming-Daten senden können. Lesen Sie die Anleitung zum [Erstellen einer Streaming-Verbindung](./create-streaming-connection.md) , um zu erfahren, wie Sie eine Streaming-Verbindung erstellen.

Nach der Registrierung einer Streaming-Verbindung haben Sie als Datenproduzent eine eindeutige URL, die zum Streamen von Daten an die Plattform verwendet werden kann.

## Streamen in einen Datensatz

Das folgende Beispiel zeigt, wie mehrere Nachrichten an einen bestimmten Datensatz innerhalb einer einzelnen HTTP-Anforderung gesendet werden. Fügen Sie die Datensatzkennnummer in die Kopfzeile der Nachricht ein, damit die Nachricht direkt darin aufgenommen wird.

Sie können die ID für einen vorhandenen Datensatz über die Plattform-Benutzeroberfläche oder über einen Listingvorgang in der API abrufen. Die Dataset-ID kann auf der [Experience Platform](https://platform.adobe.com) gefunden werden, indem Sie zur Registerkarte &quot; **Datensätze** &quot;auf den Datensatz klicken, für den die ID verwendet werden soll, und die Zeichenfolge aus dem Feld &quot; **Dataset-ID** &quot;auf der Registerkarte &quot; **Info** &quot;kopieren. Informationen zum Abrufen von Datensätzen mithilfe der API finden Sie in der Übersicht über den [Katalogdienst](../../catalog/home.md) .

Anstelle eines vorhandenen Datensatzes können Sie einen neuen Datensatz erstellen. Weitere Informationen zum Erstellen eines Datensatzes mithilfe von APIs [finden Sie im Tutorial zum](../../catalog/api/create-dataset.md) Erstellen eines Datensatzes mit APIs.

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
        "source": {
          "name": "GettingStarted"
        },
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
        "source": {
          "name": "GettingStarted"
        },
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

Eine erfolgreiche Antwort gibt einen HTTP-Status 207 (Multi-Status) zurück. Bei der Überprüfung des Antwortkörpers werden weitere Details zum Erfolg oder Misserfolg der einzelnen in der Anforderung ausgeführten Methoden angezeigt. Für jedes Element des Anforderungsmeldungen-Arrays wird eine Antwort zurückgegeben. Nachfolgend sehen Sie ein Beispiel für eine erfolgreiche Antwort ohne Nachrichtenfehler:

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

Weitere Informationen zu Statuscodes finden Sie in der Tabelle zu [Antwortcodes](#response-codes) im Anhang dieses Lernprogramms.

## Identifizieren Sie fehlgeschlagene Nachrichten.

Im Vergleich zum Senden einer Anforderung mit einer einzelnen Nachricht gibt es beim Senden einer HTTP-Anforderung mit mehreren Nachrichten weitere Faktoren, die in Betracht gezogen werden sollten, z. B.: wie zu identifizieren ist, wann Daten nicht gesendet wurden, welche spezifischen Nachrichten nicht gesendet wurden und wie sie abgerufen werden können und was mit Daten passiert, die erfolgreich sind, wenn andere Nachrichten in derselben Anforderung fehlschlagen.

Bevor Sie mit diesem Tutorial fortfahren, sollten Sie zunächst das Handbuch zum [Abrufen fehlgeschlagener Stapel](../quality/retrieve-failed-batches.md) lesen.

### Anforderungs-Nutzlast mit gültigen und ungültigen Nachrichten senden

Das folgende Beispiel zeigt, was passiert, wenn der Stapel gültige und ungültige Meldungen enthält.

Die Anforderungs-Nutzlast ist ein Array von JSON-Objekten, die das Ereignis im XDM-Schema darstellen. Beachten Sie, dass für eine erfolgreiche Validierung der Nachricht folgende Bedingungen erfüllt sein müssen:
- Das `imsOrgId` Feld im Nachrichtenkopf muss mit der Einzugsdefinition übereinstimmen. Wenn die Anforderungs-Nutzlast kein `imsOrgId` Feld enthält, fügt der Datenerfassungs-Core-Service (DCCS) das Feld automatisch hinzu.
- Die Kopfzeile der Nachricht sollte auf ein vorhandenes XDM-Schema verweisen, das in der Plattform-Benutzeroberfläche erstellt wurde.
- Das `datasetId` Feld muss auf einen vorhandenen Datensatz in der Plattform verweisen und sein Schema muss mit dem Schema übereinstimmen, das im Objekt innerhalb der einzelnen Meldungen im Anforderungstext bereitgestellt `header` wird.

**API-Format**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{CONNECTION_ID}` | Die ID des erstellten Dateneingangs. |

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
        "source": {
          "name": "GettingStarted"
        },
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
        "source": {
          "name": "GettingStarted"
        },
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
        "source": {
          "name": "GettingStarted"
        },
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
        "source": {
          "name": "GettingStarted"
        },
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
        "source": {
          "name": "GettingStarted"
        },
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

Die Antwortnutzlast enthält einen Status für jede Nachricht zusammen mit einer GUID in der , die für die Verfolgung verwendet werden kann `xactionId` .

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

Die obige Beispielantwort zeigt Fehlermeldungen für die vorherige Anforderung. Wenn Sie diese Antwort mit der vorherigen gültigen Antwort vergleichen, können Sie feststellen, dass die Anforderung teilweise erfolgreich war. Eine Nachricht wurde erfolgreich erfasst und drei Nachrichten führten zu einem Fehler. Beachten Sie, dass beide Antworten den Statuscode &quot;207&quot;zurückgeben. Weitere Informationen zu Statuscodes finden Sie in der Tabelle zu [Antwortcodes](#response-codes) im Anhang dieses Lernprogramms.

Die erste Nachricht wurde erfolgreich an Platform gesendet und wird von den Ergebnissen der anderen Nachrichten nicht beeinflusst. Daher müssen Sie diese Meldung nicht erneut einschließen, wenn Sie versuchen, die fehlgeschlagenen Nachrichten erneut zu senden.

Die zweite Meldung schlug fehl, weil ihr kein Nachrichtentext fehlte. Die Erfassungsanforderung erwartet, dass Meldungselemente gültige Kopfzeilen- und Textkörperabschnitte haben. Durch Hinzufügen des folgenden Codes nach der Kopfzeile in der zweiten Meldung wird die Anforderung behoben, sodass die zweite Meldung die Überprüfung weiterleiten kann:

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

Die dritte Meldung ist fehlgeschlagen, da eine ungültige IMS-Organisations-ID in der Kopfzeile verwendet wird. Die IMS-Organisation muss mit der {CONNECTION_ID} übereinstimmen, die Sie veröffentlichen möchten. Um festzustellen, welche IMS-Organisations-ID mit der verwendeten Streaming-Verbindung übereinstimmt, können Sie eine `GET inlet` Anforderung mithilfe der [Dateneinbetungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)durchführen. Ein Beispiel zum Abrufen zuvor erstellter Streaming-Verbindungen finden Sie unter [Abrufen einer Streaming-Verbindung](./create-streaming-connection.md#get-data-collection-url) .

Die vierte Meldung ist fehlgeschlagen, da sie nicht dem erwarteten XDM-Schema entsprach. Die `xdmSchema` in der Kopfzeile und im Hauptteil der Anforderung enthaltenen Elemente stimmen nicht mit dem XDM-Schema des `{DATASET_ID}`Berichts überein. Durch die Korrektur des Schemas im Nachrichtenkopf und -körper kann die DCCS-Überprüfung erfolgreich an die Plattform gesendet werden. Der Nachrichtentext muss auch aktualisiert werden, um mit dem XDM-Schema des zu übereinstimmen, `{DATASET_ID}` damit die Streaming-Validierung auf der Plattform durchgeführt werden kann. Weitere Informationen zu Nachrichten, die erfolgreich an die Plattform gesendet werden, finden Sie im Abschnitt [Bestätigungsmeldungen](#confirm-messages-ingested) zu diesem Lernprogramm.

### Fehlermeldungen von der Plattform abrufen

Fehlgeschlagene Meldungen werden durch einen Fehlerstatuscode im Antwortarray identifiziert.
Die ungültigen Meldungen werden in einem &quot;Fehler&quot;-Batch innerhalb des von `{DATASET_ID}`angegebenen Datensatzes erfasst und gespeichert.

Weitere Informationen zum Wiederherstellen von fehlgeschlagenen Stapelmeldungen finden Sie im Handbuch zum [Abrufen fehlgeschlagener Stapel](../quality/retrieve-failed-batches.md) .

## Nachrichten bestätigen

Meldungen, die die DCCS-Validierung übergeben, werden an die Plattform gestreamt. Auf der Plattform werden die Batch-Nachrichten durch Streaming-Validierung getestet, bevor sie in den Datensee aufgenommen werden. Der Status von Stapeln, ob erfolgreich oder nicht, wird in dem von `{DATASET_ID}`angegebenen Datensatz angezeigt.

Sie können den Status von Batch-Nachrichten, die mit der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com) erfolgreich auf eine Plattform gestreamt werden, über die Registerkarte &quot; **Datasets** &quot;Ansicht, auf den Datensatz, zu dem Sie streamen, klicken und die Registerkarte &quot; **DataSet-Aktivität** &quot;überprüfen.

Stapelmeldungen, die die Streaming-Validierung auf der Plattform übergeben, werden in den Datensee aufgenommen. Die Meldungen stehen dann für die Analyse oder den Export zur Verfügung.

## Nächste Schritte

Nachdem Sie jetzt wissen, wie Sie mehrere Nachrichten in einer einzigen Anforderung senden und überprüfen können, ob die Nachrichten erfolgreich in den Dataset der Zielgruppe aufgenommen wurden, können Sie Beginn-Streaming Ihrer eigenen Daten an die Plattform durchführen. Eine Übersicht über die Abfrage und den Abruf von erfassten Daten von der Plattform finden Sie im Handbuch [Datenzugriff](../../data-access/tutorials/dataset-data.md) .

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zum Tutorial.

### Antwortcodes

Die folgende Tabelle zeigt Statuscodes, die von erfolgreichen und fehlgeschlagenen Antwortmeldungen zurückgegeben werden.

| Statuscode | Beschreibung |
| :---: | --- |
| 207 | Obwohl &quot;207&quot;als Gesamt-Antwortstatuscode verwendet wird, muss der Empfänger den Inhalt des Multistatus-Antwortkörpers für weitere Informationen zum Erfolg oder Misserfolg der Methodenausführung konsultieren. Der Antwortcode wird in Erfolgs-, Teil- und auch in Fehlersituationen verwendet. |
| 400 | Es gab ein Problem mit der Bitte. Im Antworttext finden Sie eine spezifischere Fehlermeldung (z. B. fehlte die Nachrichtennutzlast erforderliche Felder oder die Meldung war unbekanntes xdm-Format). |
| 401 | Nicht autorisiert: Anforderung fehlender gültiger Autorisierungsheader. Dies wird nur bei Inlets zurückgegeben, für die die Authentifizierung aktiviert ist. |
| 403 | Nicht autorisiert:  Das angegebene Autorisierungstoken ist ungültig oder abgelaufen. Dies wird nur bei Inlets zurückgegeben, für die die Authentifizierung aktiviert ist. |
| 413 | Nutzlast zu groß - Wird ausgelöst, wenn die Nutzdatenanforderung insgesamt größer als 1 MB ist. |
| 429 | Zu viele Anfragen innerhalb der angegebenen Zeitdauer. |
| 500 | Fehler bei der Verarbeitung der Nutzlast. Im Antworttext finden Sie eine spezifischere Fehlermeldung (z. B. das Message Payload-Schema wurde nicht angegeben oder entsprach nicht der XDM-Definition in der Plattform). |
| 503 | Der Dienst ist derzeit nicht verfügbar. Kunden sollten es mindestens dreimal mit einer exponentiellen Back-off-Strategie versuchen. |