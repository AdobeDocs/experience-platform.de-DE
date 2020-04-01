---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die partielle Batchverarbeitung in Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---



# Partielle Batch-Erfassung

Partielle Stapelverarbeitung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform aufnehmen, während alle fehlerhaften Daten separat gestapelt werden, zusammen mit Details, warum sie ungültig sind.

Dieses Dokument bietet eine Anleitung zum Verwalten der partiellen Stapelverarbeitung.

Darüber hinaus bietet der [Anhang](#partial-batch-ingestion-error-types) zu diesem Lernprogramm eine Referenz zu Fehlertypen bei der Partiellen Stapelverarbeitung.

## Erste Schritte

Dieses Lernprogramm erfordert Arbeitskenntnisse zu den verschiedenen Adobe Experience Platform-Diensten, die mit der teilweisen Batchverarbeitung verbunden sind. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Stapelverarbeitung](./overview.md): Die Methode, mit der Platform Daten aus Datendateien wie CSV und Parquet erfasst und speichert.
- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich Aufrufe an Plattform-APIs durchführen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Aktivieren eines Datensatzes für die teilweise Stapelverarbeitung in der API

>[!NOTE] In diesem Abschnitt wird die Aktivierung eines Datensatzes für die teilweise Stapelverarbeitung mithilfe der API beschrieben. Anweisungen zur Verwendung der Benutzeroberfläche finden Sie im Abschnitt zum [Aktivieren eines Datensatzes für die teilweise Stapelverarbeitung im UI](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) -Schritt.

Sie können einen neuen Datensatz erstellen oder einen vorhandenen Datensatz mit aktivierter teilweiser Erfassung ändern.

Um einen neuen Datensatz zu erstellen, führen Sie die Schritte im Lernprogramm zum [Erstellen eines Datensatzes](../../catalog/api/create-dataset.md)aus. Nachdem Sie den Schritt zum *Erstellen eines Datensatzes* erreicht haben, fügen Sie das folgende Feld im Anforderungstext hinzu:

```json
{
    ...
    "tags" : {
        "partialBatchIngestion":["errorThresholdPercentage:5"]
    },
    ...
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `errorThresholdPercentage` | Der Prozentsatz der akzeptablen Fehler, bevor der gesamte Stapel fehlschlägt. |

Um einen vorhandenen Datensatz zu ändern, führen Sie die Schritte im Entwicklerhandbuch für den [Katalog durch](../../catalog/api/update-object.md).

Innerhalb des Datensatzes müssen Sie das oben beschriebene Tag hinzufügen.

## Aktivieren eines Datensatzes für die teilweise Stapelverarbeitung in der Benutzeroberfläche

>[!NOTE] In diesem Abschnitt wird beschrieben, wie Sie einen Datensatz für die teilweise Stapelverarbeitung mithilfe der Benutzeroberfläche aktivieren. Wenn Sie bereits einen Datensatz für die teilweise Stapelverarbeitung mithilfe der API aktiviert haben, können Sie mit dem nächsten Abschnitt fortfahren.

Um einen Datensatz für die teilweise Erfassung über die Plattform-Benutzeroberfläche zu aktivieren, klicken Sie im linken Navigationsbereich auf **Datensätze** . Sie können entweder einen neuen Datensatz [erstellen](#create-a-new-dataset-with-partial-batch-ingestion-enabled) oder einen vorhandenen Datensatz [ändern](#modify-an-existing-dataset-to-enable-partial-batch-ingestion).

### Erstellen eines neuen Datensatzes mit aktivierter partieller Batchverarbeitung

Um einen neuen Datensatz zu erstellen, führen Sie die Schritte im Benutzerhandbuch zum [Datensatz aus](../../catalog/datasets/user-guide.md). Nachdem Sie den Schritt zum *Konfigurieren des Datensatzes* erreicht haben, beachten Sie die Felder *Partielle Eingabe* und *Fehlerdiagnose* .

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

Mit dem Umschalter *Partielle Erfassung* können Sie die Verwendung einer partiellen Stapelverarbeitung aktivieren oder deaktivieren.

Der Umschalter *Fehlerdiagnose* wird nur angezeigt, wenn der Umschalter für die *partielle Einbindung* deaktiviert ist. Mit dieser Funktion kann die Plattform detaillierte Fehlermeldungen zu den erfassten Stapeln generieren. Wenn der Umschalter für die *partielle* Eingabe aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

Mit dem *Fehlerschwellenwert* können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Stapel fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

### Vorhandene Datensätze ändern, um die teilweise Stapelverarbeitung zu aktivieren

Um einen vorhandenen Datensatz zu ändern, wählen Sie den zu ändernden Datensatz aus. Die Seitenleiste auf der rechten Seite enthält Informationen zum Datensatz.

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

Mit dem Umschalter *Partielle Erfassung* können Sie die Verwendung einer partiellen Stapelverarbeitung aktivieren oder deaktivieren.

Mit dem *Fehlerschwellenwert* können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Stapel fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

## Abrufen von Fehlern bei der partiellen Stapelverarbeitung

Wenn Stapel Fehler enthalten, müssen Sie Fehlerinformationen zu diesen Fehlern abrufen, damit Sie die Daten erneut erfassen können.

### Status prüfen

Um den Status des erfassten Stapels zu überprüfen, müssen Sie die ID des Stapels im Pfad einer GET-Anforderung angeben.

**API-Format**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Der `id` Wert des Stapels, dessen Status Sie überprüfen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zum Status des Stapels zurück.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

Wenn der Stapel einen Fehler aufweist und die Fehlerdiagnose aktiviert ist, lautet der Status &quot;success&quot;mit weiteren Informationen zum Fehler, der in einer herunterladbaren Fehlerdatei bereitgestellt wird.

## Nächste Schritte

In diesem Lernprogramm wurde beschrieben, wie Sie einen Datensatz erstellen oder ändern, um die teilweise Stapelverarbeitung zu aktivieren. Weitere Informationen zur Stapelverarbeitung finden Sie im [Entwicklerhandbuch](./api-overview.md)zur Stapelverarbeitung.

## Fehlertypen bei der Partielle Stapelverarbeitung

Bei der Partiellen Stapelverarbeitung gibt es beim Erfassen von Daten vier verschiedene Fehlertypen.

- [Unlesbare Dateien](#unreadable)
- [Ungültige Schemas oder Kopfzeilen](#schemas-headers)
- [Unveränderliche Zeilen](#unparsable)
- [Ungültige XDM-Konvertierung](#conversion)

### Unlesbare Dateien {#unreadable}

Wenn der erfasste Stapel unleserliche Dateien enthält, werden die Fehler des Stapels an den Stapel selbst angehängt. Weitere Informationen zum Abrufen des fehlgeschlagenen Stapels finden Sie im Handbuch zum [Abrufen fehlgeschlagener Stapel](../quality/retrieve-failed-batches.md).

### Ungültige Schemas oder Kopfzeilen {#schemas-headers}

Wenn der erfasste Stapel ein ungültiges Schema oder ungültige Header enthält, werden die Stapelfehler auf den Stapel selbst angehängt. Weitere Informationen zum Abrufen des fehlgeschlagenen Stapels finden Sie im Handbuch zum [Abrufen fehlgeschlagener Stapel](../quality/retrieve-failed-batches.md).

### Unveränderliche Zeilen {#unparsable}

Wenn der erfasste Stapel über nicht trennbare Zeilen verfügt, werden die Fehler des Stapels in einer Datei gespeichert, auf die mithilfe des unten beschriebenen Endpunkts zugegriffen werden kann.

**API-Format**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Der `id` Wert des Stapels, aus dem Sie Fehlerinformationen abrufen. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zu den nicht trennbaren Zeilen zurückgegeben.

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### Ungültige XDM-Konvertierung {#conversion}

Wenn der aufgezeichnete Stapel ungültige XDM-Konvertierungen enthält, werden die Fehler des Stapels in einer Datei gespeichert, auf die über den folgenden Endpunkt zugegriffen werden kann.

**API-Format**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Der `id` Wert des Stapels, aus dem Sie Fehlerinformationen abrufen. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zu den Fehlern bei der XDM-Konvertierung zurück.

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```
