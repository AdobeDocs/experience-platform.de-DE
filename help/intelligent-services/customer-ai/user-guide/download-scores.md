---
keywords: Experience Platform; Herunterladen von Bewertungen; Customer AI; beliebte Themen; Exportieren; Exportieren; Herunterladen von Kundenai; Bewertung von Kundenai
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Herunterladen von Bewertungen in Customer AI
description: Mit Customer AI können Sie Bewertungen im Parquet-Dateiformat herunterladen.
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 81%

---

# Herunterladen von Bewertungen in Customer AI

Dieses Dokument dient als Anleitung zum Herunterladen von Ergebnissen für Customer AI.

## Erste Schritte

Mit Customer AI können Sie Bewertungen im Parquet-Dateiformat herunterladen. Für dieses Tutorial müssen Sie den Abschnitt zum Herunterladen von Customer AI-Bewertungen in den [Ersten Schritten](../getting-started.md) gelesen und abgeschlossen haben.

Um auf Bewertungen für Customer AI zuzugreifen, benötigen Sie außerdem eine Dienstinstanz mit einem erfolgreichen Ausführungsstatus. Um eine neue Dienstinstanz zu erstellen, besuchen Sie [Konfigurieren einer Customer AI-Instanz](./configure.md). Wenn Sie kürzlich eine Dienstinstanz erstellt haben und diese sich noch in der Trainings- und Bewertungsphase befindet, warten Sie bitte 24 Stunden, bis sie fertig ist.

Derzeit gibt es zwei Möglichkeiten, Customer AI-Bewertungen herunterzuladen:

1. Wenn Sie die Bewertungen auf der jeweiligen Ebene herunterladen möchten und/oder das Echtzeit-Kundenprofil nicht aktiviert ist, navigieren Sie zu [Auffinden der Datensatz-ID](#dataset-id).
2. Wenn Sie Profil aktiviert haben und Segmente herunterladen möchten, die Sie mit Customer AI konfiguriert haben, gehen Sie zu [Herunterladen eines mit Customer AI konfigurierten Segments](#segment).

## Ermitteln Ihrer Datensatz-ID {#dataset-id}

Klicken Sie in Ihrer Dienstinstanz für Customer AI-Einblicke auf das Dropdown-Menü *Mehr Aktionen* und wählen Sie **[!UICONTROL Auf Bewertungen zugreifen]** aus.

![Mehr Aktionen](../images/insights/more-actions.png)

Es wird ein neues Dialogfeld mit einem Link zur Dokumentation zum Herunterladen von Bewertungen und der Datensatz-ID Ihrer aktuellen Instanz angezeigt. Kopieren Sie die Datensatz-ID in die Zwischenablage und fahren Sie mit dem nächsten Schritt fort.

![Datensatz-ID](../images/download-scores/access-scores.png)

## Abrufen Ihrer Batch-Kennung {#retrieve-your-batch-id}

Rufen Sie mit Ihrer Datensatz-ID aus dem vorherigen Schritt die Catalog-API auf, um eine Batch-Kennung abzurufen. Für diesen API-Aufruf werden zusätzliche Abfrageparameter verwendet, um den neuesten erfolgreichen Batch anstelle einer Liste von Batches Ihrer Organisation zurückzugeben. Um weitere Batches zurückzugeben, erhöhen Sie die Zahl für den Parameter limit query auf den gewünschten Wert, der zurückgegeben werden soll. Weitere Informationen zu den verfügbaren Parametertypen für die Abfrage finden Sie im Handbuch zum [Filtern von Katalogdaten mithilfe von Abfrageparametern](../../../catalog/api/filter-data.md).

**API-Format**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATASET_ID}` | Die im Dialogfeld „Auf Bewertungen zugreifen“ verfügbare Datensatz-ID. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die ein Batch-ID-Objekt enthält. In diesem Beispiel ist der Schlüsselwert für das zurückgegebene Objekt die Batch-ID `01E5QSWCAASFQ054FNBKYV6TIQ`. Kopieren Sie Ihre Batch-Kennung, um sie beim nächsten API-Aufruf zu verwenden.

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5cd9146b31dae914b75f654f"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## Abrufen des nächsten API-Aufrufs mit Ihrer Batch-Kennung {#retrieve-the-next-api-call-with-your-batch-id}

Sobald Sie über eine Batch-Kennung verfügen, können Sie eine neue GET-Anfrage an `/batches` vornehmen. Die Anfrage gibt einen Link zurück, der als die nächste API-Anfrage verwendet wird.

**API-Format**

```http
GET batches/{BATCH_ID}/files
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die im vorherigen Schritt [Abrufen Ihrer Batch-Kennung](#retrieve-your-batch-id) abgerufene Batch-Kennung. |

**Anfrage**

Stellen Sie mithilfe Ihrer Batch-Kennung die folgende Anfrage.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die ein `_links`-Objekt enthält. Innerhalb des `_links`-Objekts befindet sich ein `href` mit einem neuen API-Aufruf als Wert. Kopieren Sie diesen Wert, um mit dem nächsten Schritt fortzufahren.

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## Abrufen Ihrer Dateien {#retrieving-your-files}

Verwenden Sie den `href`-Wert, den Sie im vorherigen Schritt als API-Aufruf erhalten haben, und stellen Sie eine neue GET-Anfrage, um Ihr Dateiverzeichnis abzurufen.

**API-Format**

```http
GET files/{DATASETFILE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATASETFILE_ID}` | Die dataSetFile-ID wird im `href`-Wert des [vorherigen Schritts](#retrieve-the-next-api-call-with-your-batch-id) zurückgegeben. Sie ist auch im `data`-Array unter dem Objekttyp `dataSetFileId` verfügbar. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält ein Daten-Array, das einen einzelnen Eintrag oder eine Liste von Dateien enthalten kann, die zu diesem Verzeichnis gehören. Das folgende Beispiel enthält eine Liste von Dateien und wurde aus Gründen der Lesbarkeit komprimiert. In diesem Szenario müssen Sie der URL jeder Datei folgen, um auf die Datei zugreifen zu können.

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `_links.self.href` | Die URL der GET-Anfrage, mit der eine Datei in Ihr Verzeichnis heruntergeladen wird. |


Kopieren Sie den `href`-Wert für ein beliebiges Dateiobjekt im `data`-Array und fahren Sie dann mit dem nächsten Schritt fort.

## Herunterladen Ihrer Dateidaten

Um Ihre Dateidaten herunterzuladen, stellen Sie eine GET-Anfrage an den `"href"`-Wert, den Sie im vorherigen Schritt [Abrufen Ihrer Dateien](#retrieving-your-files) kopiert haben.

>[!NOTE]
>
> Wenn Sie diese Anfrage direkt in der Befehlszeile ausführen, werden Sie möglicherweise aufgefordert, eine Ausgabe nach den Kopfzeilen Ihrer Anfrage hinzuzufügen. Im folgenden Anfragebeispiel wird `--output {FILENAME.FILETYPE}` verwendet.

**API-Format**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATASETFILE_ID}` | Die dataSetFile-ID wird im `href`-Wert eines [vorherigen Schritts](#retrieve-the-next-api-call-with-your-batch-id) zurückgegeben. |
| `{FILE_NAME}` | Der Name der Datei. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>Vergewissern Sie sich, dass Sie sich im richtigen Verzeichnis oder Ordner befinden, in dem die Datei gespeichert werden soll, bevor Sie die GET-Anfrage stellen.

**Antwort**

Die Antwort lädt die angeforderte Datei in Ihr aktuelles Verzeichnis herunter. In diesem Beispiel lautet der Dateiname „filename.parquet“.

![Endgerät](../images/download-scores/response.png)

## Herunterladen eines mit Customer AI konfigurierten Segments {#segment}

Alternativ können Sie Ihre Bewertungsdaten herunterladen, indem Sie Ihre Zielgruppe in einen Datensatz exportieren. Nachdem ein Segmentierungsauftrag erfolgreich abgeschlossen wurde (der Wert des `status`-Attributs lautet „SUCCEEDED“ (GELUNGEN)), können Sie Ihre Zielgruppe in einen Datensatz exportieren. In diesem Datensatz ist die Zielgruppe zugänglich und bearbeitbar. Weitere Informationen zur Segmentierung finden Sie in [Segmentierung – Übersicht](../../../segmentation/home.md).

>[!IMPORTANT]
>
>Um diese Exportmethode zu verwenden, muss das Echtzeit-Kundenprofil für den Datensatz aktiviert werden.

Im Abschnitt zum [Exportieren eines Segments](../../../segmentation/tutorials/evaluate-a-segment.md) im Handbuch zur Segmentauswertung werden die erforderlichen Schritte zum Exportieren eines Zielgruppendatensatzes beschrieben. Das Handbuch beschreibt und enthält Beispiele für Folgendes:

- **Erstellen eines Zielgruppendatensatzes:** Erstellen Sie den Datensatz, um Mitglieder der Zielgruppe aufzunehmen.
- **Generieren von Zielgruppenprofilen im Datensatz:** Füllen Sie den Datensatz mit individuellen XDM-Profilen auf der Grundlage der Ergebnisse eines Segmentauftrags.
- **Überwachen des Exportfortschritts:** Überprüfen Sie den aktuellen Fortschritt des Exportvorgangs.
- **Lesen von Zielgruppendaten:** Rufen Sie die resultierenden individuellen XDM-Profile ab, die die Mitglieder Ihrer Zielgruppe repräsentieren.

## Nächste Schritte

In diesem Dokument wurden die Schritte zum Herunterladen von Customer AI-Bewertungen beschrieben. Sie können sich jetzt die weiteren angebotenen [Intelligent Services](../../home.md) und Handbücher ansehen.
