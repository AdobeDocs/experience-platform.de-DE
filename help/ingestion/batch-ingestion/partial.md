---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;
solution: Experience Platform
title: Überblick über die Partielle Stapelverarbeitung
topic: overview
description: Dieses Dokument enthält eine Anleitung zum Verwalten der partiellen Batch-Erfassung.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 40%

---


# Partielle Batch-Erfassung

Partielle Batch-Erfassung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle fehlerhaften Daten in Batches separat verarbeitet werden (zusammen mit Details dazu, warum sie ungültig sind).

Dieses Dokument enthält eine Anleitung zum Verwalten der partiellen Batch-Erfassung.

## Erste Schritte

Diese Anleitung setzt grundlegende Kenntnisse zu den verschiedenen Adobe Experience Platform-Diensten voraus, die mit der partiellen Batch-Erfassung verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Batch-Erfassung](./overview.md)[!DNL Platform]: Die Methode, mit der Daten aus Datendateien wie CSV und Parquet erfasst und speichert.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

The following sections provide additional information that you will need to know in order to successfully make calls to [!DNL Platform] APIs.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

## Enable a batch for partial batch ingestion in the API {#enable-api}

>[!NOTE]
>
>In diesem Abschnitt wird die Aktivierung eines Stapels für die teilweise Stapelverarbeitung mithilfe der API beschrieben. For instructions on using the UI, please read the [enable a batch for partial batch ingestion in the UI](#enable-ui) step.

Sie können einen neuen Stapel mit aktivierter teilweiser Erfassung erstellen.

Um einen neuen Stapel zu erstellen, führen Sie die Schritte im Entwicklerhandbuch für die [Stapelverarbeitung](./api-overview.md)aus. Once you reach the **[!UICONTROL Create batch]** step, add the following field within the request body:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `enableErrorDiagnostics` | Ein Flag, mit dem detaillierte Fehlermeldungen zum Stapel generiert [!DNL Platform] werden können. |
| `partialIngestionPercentage` | Der Prozentsatz der akzeptablen Fehler, bevor der gesamte Batch fehlschlägt. In diesem Beispiel können also maximal 5 % des Stapels Fehler sein, bevor er fehlschlägt. |


## Enable a batch for partial batch ingestion in the UI {#enable-ui}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie einen Stapel für die teilweise Stapelverarbeitung mithilfe der Benutzeroberfläche aktivieren. Wenn Sie bereits einen Stapel für die teilweise Stapelverarbeitung mithilfe der API aktiviert haben, können Sie mit dem nächsten Abschnitt fortfahren.

Um einen Stapel für die teilweise Erfassung über die [!DNL Platform] Benutzeroberfläche zu aktivieren, können Sie einen neuen Stapel über Quellverbindungen erstellen, einen neuen Stapel in einem vorhandenen Datensatz erstellen oder einen neuen Stapel über den Fluss[!UICONTROL &quot;CSV zu XDM zuordnen&quot;erstellen].

### Neue Quellverbindung erstellen {#new-source}

Um eine neue Quellverbindung zu erstellen, führen Sie die in der Übersicht über die [Quellen](../../sources/home.md)aufgeführten Schritte aus. Once you reach the **[!UICONTROL Dataflow detail]** step, take note of the **[!UICONTROL Partial ingestion]** and **[!UICONTROL Error diagnostics]** fields.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

### Vorhandenen Datensatz verwenden {#existing-dataset}

Um einen vorhandenen Datensatz zu verwenden, wählen Sie einen Beginn aus, indem Sie einen Datensatz auswählen. Die Seitenleiste rechts enthält Informationen zum Datensatz.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

Jetzt können Sie Daten mit der Schaltfläche **Hinzufügen Daten** hochladen, die dann mit einer teilweisen Erfassung erfasst werden.

### Verwenden Sie den Fluss &quot;CSV[!UICONTROL zu XDM-Schema]zuordnen&quot; {#map-flow}

Um den Fluss &quot;CSV[!UICONTROL zu XDM-Schema]zuordnen&quot;zu verwenden, führen Sie die im Lernprogramm [CSV-Datei](../tutorials/map-a-csv-file.md)zuordnen aufgeführten Schritte aus. Once you reach the **[!UICONTROL Add data]** step, take note of the **[!UICONTROL Partial ingestion]** and **[!UICONTROL Error diagnostics]** fields.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

## Nächste Schritte {#next-steps}

In dieser Anleitung wurde beschrieben, wie Sie einen Datensatz erstellen oder ändern, um die partielle Batch-Erfassung zu aktivieren. Weiterführende Informationen zur Batch-Erfassung finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](./api-overview.md).

Informationen zur Überwachung von Fehlern bei der partiellen Erfassung finden Sie im Handbuch zur Fehlerdiagnose bei der [Stapelverarbeitung](../quality/error-diagnostics.md).
