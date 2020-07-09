---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die partielle Batchaufnahme der Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 0be45675e4a2e3308cb77a8bbe3189f09c2b6fd8
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 1%

---



# Partielle Batch-Erfassung

Partielle Stapelverarbeitung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform aufnehmen, während alle fehlerhaften Daten separat in Batches aufgenommen werden, zusammen mit Details, warum sie ungültig sind.

Dieses Dokument bietet eine Anleitung zum Verwalten der partiellen Stapelverarbeitung.

Darüber hinaus bietet der [Anhang](#appendix) zu diesem Lernprogramm eine Referenz zu Fehlertypen bei der Partiellen Stapelverarbeitung.

## Erste Schritte

Dieses Tutorial erfordert ein Arbeitswissen der verschiedenen Adobe Experience Platformen-Services, die mit der teilweisen Stapelverarbeitung verbunden sind. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Stapelverarbeitung](./overview.md): Die Methode, mit der Daten aus Datendateien wie CSV und Parquet [!DNL Platform] erfasst und gespeichert werden.
- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Platform] APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur [!DNL Experience Platform] Fehlerbehebung.

### Werte für erforderliche Kopfzeilen sammeln

Um [!DNL Platform] APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform]finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Aktivieren eines Stapels für die teilweise Stapelverarbeitung in der API {#enable-api}

>[!NOTE]
>
>In diesem Abschnitt wird die Aktivierung eines Stapels für die teilweise Stapelverarbeitung mithilfe der API beschrieben. Anweisungen zur Verwendung der Benutzeroberfläche finden Sie im Schritt Benutzeroberfläche [im Abschnitt Stapel zur teilweisen Stapelverarbeitung](#enable-ui) aktivieren.

Sie können einen neuen Stapel mit aktivierter teilweiser Erfassung erstellen.

Um einen neuen Stapel zu erstellen, führen Sie die Schritte im Entwicklerhandbuch für die [Stapelverarbeitung](./api-overview.md)aus. Nachdem Sie den Schritt Stapel *erstellen* erreicht haben, fügen Sie das folgende Feld im Anforderungstext hinzu:

```json
{
    ...
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
    ...
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `enableErrorDiagnostics` | Ein Flag, mit dem detaillierte Fehlermeldungen zum Stapel generiert [!DNL Platform] werden können. |
| `partialIngestionPercentage` | Der Prozentsatz der akzeptablen Fehler, bevor der gesamte Stapel fehlschlägt. In diesem Beispiel können also maximal 5 % des Stapels Fehler sein, bevor er fehlschlägt. |


## Aktivieren eines Stapels für die teilweise Stapelverarbeitung in der Benutzeroberfläche {#enable-ui}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie einen Stapel für die teilweise Stapelverarbeitung mithilfe der Benutzeroberfläche aktivieren. Wenn Sie bereits einen Stapel für die teilweise Stapelverarbeitung mithilfe der API aktiviert haben, können Sie mit dem nächsten Abschnitt fortfahren.

Um einen Stapel für die teilweise Erfassung über die [!DNL Platform] Benutzeroberfläche zu aktivieren, können Sie einen neuen Stapel über Quellverbindungen erstellen, einen neuen Stapel in einem vorhandenen Datensatz erstellen oder einen neuen Stapel über den Fluss[!UICONTROL &quot;CSV zu XDM zuordnen&quot;erstellen].

### Neue Quellverbindung erstellen {#new-source}

Um eine neue Quellverbindung zu erstellen, führen Sie die in der Übersicht über die [Quellen](../../sources/home.md)aufgeführten Schritte aus. Nachdem Sie den Schritt für die *[!UICONTROL Datenfelddetails]* erreicht haben, beachten Sie die Felder *[!UICONTROL Partielle Erfassung]* und *[!UICONTROL Fehlerdiagnose]* .

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Mit dem Umschalter *[!UICONTROL Partielle Erfassung]* können Sie die Verwendung einer partiellen Stapelverarbeitung aktivieren oder deaktivieren.

Der Umschalter für die *[!UICONTROL Fehlerdiagnose]* wird nur angezeigt, wenn der Umschalter für die *[!UICONTROL partielle Erfassung]* deaktiviert ist. Mit dieser Funktion können Sie detaillierte Fehlermeldungen [!DNL Platform] zu den erfassten Stapeln generieren. Wenn der Umschalter *[!UICONTROL für die teilweise Erfassung]* aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Mit dem *[!UICONTROL Fehlerschwellenwert]* können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Stapel fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

### Vorhandenen Datensatz verwenden {#existing-dataset}

Um einen vorhandenen Datensatz zu verwenden, wählen Sie einen Beginn aus, indem Sie einen Datensatz auswählen. Die Seitenleiste auf der rechten Seite enthält Informationen zum Datensatz.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Mit dem Umschalter *[!UICONTROL Partielle Erfassung]* können Sie die Verwendung einer partiellen Stapelverarbeitung aktivieren oder deaktivieren.

Der Umschalter für die *[!UICONTROL Fehlerdiagnose]* wird nur angezeigt, wenn der Umschalter für die *[!UICONTROL partielle Erfassung]* deaktiviert ist. Mit dieser Funktion können Sie detaillierte Fehlermeldungen [!DNL Platform] zu den erfassten Stapeln generieren. Wenn der Umschalter *[!UICONTROL für die teilweise Erfassung]* aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Mit dem *[!UICONTROL Fehlerschwellenwert]* können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Stapel fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

Jetzt können Sie Daten mit der Schaltfläche **Hinzufügen Daten** hochladen, die dann mit einer teilweisen Erfassung erfasst werden.

### Verwenden Sie den Fluss &quot;CSV[!UICONTROL zu XDM-Schema]zuordnen&quot; {#map-flow}

Um den Fluss &quot;CSV[!UICONTROL zu XDM-Schema]zuordnen&quot;zu verwenden, führen Sie die im Lernprogramm [CSV-Datei](../tutorials/map-a-csv-file.md)zuordnen aufgeführten Schritte aus. Nachdem Sie den *HinzufügenDatenschritt* erreicht haben, beachten Sie die Felder *[!UICONTROL Partielle Erfassung]* und *[!UICONTROL Fehlerdiagnose]* .

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Mit dem Umschalter *[!UICONTROL Partielle Erfassung]* können Sie die Verwendung einer partiellen Stapelverarbeitung aktivieren oder deaktivieren.

Der Umschalter für die *[!UICONTROL Fehlerdiagnose]* wird nur angezeigt, wenn der Umschalter für die *[!UICONTROL partielle Erfassung]* deaktiviert ist. Mit dieser Funktion können Sie detaillierte Fehlermeldungen [!DNL Platform] zu den erfassten Stapeln generieren. Wenn der Umschalter *[!UICONTROL für die teilweise Erfassung]* aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Mit dem *[!UICONTROL Fehlerschwellenwert]* können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Stapel fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

## Abrufen von Fehlern bei der partiellen Stapelverarbeitung {#retrieve-errors}

Wenn Stapel Fehler enthalten, müssen Sie Fehlerinformationen zu diesen Fehlern abrufen, damit Sie die Daten erneut erfassen können.

### Status prüfen {#check-status}

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
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
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

## Nächste Schritte {#next-steps}

In diesem Lernprogramm wurde beschrieben, wie Sie einen Datensatz erstellen oder ändern, um die teilweise Stapelverarbeitung zu aktivieren. Weitere Informationen zur Stapelverarbeitung finden Sie im [Entwicklerhandbuch](./api-overview.md)zur Stapelverarbeitung.

## Fehlertypen bei der Partielle Stapelverarbeitung {#appendix}

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
