---
keywords: Experience Platform;Startseite;beliebte Themen;Stapelverarbeitung;Stapelverarbeitung;Partielle Erfassung;Partielle Erfassung;Fehler abrufen;Fehler abrufen;Partielle Stapelverarbeitung;Partielle Stapelverarbeitung;Partielle Stapelverarbeitung;Partielle Erfassung;Einnahme;Einbettung; Einbettung;
solution: Experience Platform
title: Übersicht über die partielle Batch-Ingestion
topic-legacy: overview
description: Dieses Dokument enthält eine Anleitung zum Verwalten der partiellen Batch-Erfassung.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 42%

---

# Partielle Batch-Erfassung

Partielle Batch-Erfassung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle fehlerhaften Daten in Batches separat verarbeitet werden (zusammen mit Details dazu, warum sie ungültig sind).

Dieses Dokument enthält eine Anleitung zum Verwalten der partiellen Batch-Erfassung.

## Erste Schritte

Diese Anleitung setzt grundlegende Kenntnisse zu den verschiedenen Adobe Experience Platform-Diensten voraus, die mit der partiellen Batch-Erfassung verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Batch-Erfassung](./overview.md)[!DNL Platform]: Die Methode, mit der Daten aus Datendateien wie CSV und Parquet erfasst und speichert.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um [!DNL Platform]-APIs erfolgreich aufzurufen.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Aktivieren eines Stapels für die teilweise Stapelverarbeitung in der API {#enable-api}

>[!NOTE]
>
>In diesem Abschnitt wird die Aktivierung eines Stapels für die teilweise Stapelverarbeitung mithilfe der API beschrieben. Anweisungen zur Verwendung der Benutzeroberfläche finden Sie im Schritt [Stapel zur teilweisen Stapelverarbeitung in der Benutzeroberfläche](#enable-ui) aktivieren.

Sie können einen neuen Stapel mit aktivierter teilweiser Erfassung erstellen.

Gehen Sie zum Erstellen eines neuen Stapels wie im Handbuch [Stapelverarbeitungsentwickler](./api-overview.md) beschrieben vor. Nachdem Sie den Schritt **[!UICONTROL Stapel erstellen]** erreicht haben, fügen Sie das folgende Feld im Anforderungstext hinzu:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `enableErrorDiagnostics` | Ein Flag, mit dem [!DNL Platform] detaillierte Fehlermeldungen zu Ihrem Stapel generieren kann. |
| `partialIngestionPercentage` | Der Prozentsatz der akzeptablen Fehler, bevor der gesamte Batch fehlschlägt. In diesem Beispiel können also maximal 5 % des Stapels Fehler sein, bevor er fehlschlägt. |


## Aktivieren eines Stapels für die teilweise Stapelverarbeitung in der Benutzeroberfläche {#enable-ui}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie einen Stapel für die teilweise Stapelverarbeitung mithilfe der Benutzeroberfläche aktivieren. Wenn Sie bereits einen Stapel für die teilweise Stapelverarbeitung mithilfe der API aktiviert haben, können Sie mit dem nächsten Abschnitt fortfahren.

Um einen Stapel für die teilweise Erfassung über die [!DNL Platform]-Benutzeroberfläche zu aktivieren, können Sie einen neuen Stapel über Quellverbindungen erstellen, einen neuen Stapel in einem vorhandenen Datensatz erstellen oder einen neuen Stapel über den Befehl &quot;[!UICONTROL CSV zu XDM-Fluss] zuordnen&quot;erstellen.

### Neue Quellverbindung {#new-source} erstellen

Um eine neue Quellverbindung zu erstellen, führen Sie die aufgelisteten Schritte unter [Übersicht über die Quellen](../../sources/home.md) aus. Sobald Sie den Schritt **[!UICONTROL Datentiefe]** erreicht haben, beachten Sie die Felder **[!UICONTROL Partielle Erfassung]** und **[!UICONTROL Fehlerdiagnose]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

Der Umschalter **[!UICONTROL Fehlerdiagnose]** wird nur angezeigt, wenn der Umschalter **[!UICONTROL Partielle Erfassung]** deaktiviert ist. Mit dieser Funktion können [!DNL Platform] detaillierte Fehlermeldungen zu Ihren erfassten Stapeln generieren. Wenn der Umschalter **[!UICONTROL Partielle Erfassung]** aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

### Vorhandenen Datensatz verwenden {#existing-dataset}

Um einen vorhandenen Datensatz zu verwenden, wählen Sie einen Beginn aus, indem Sie einen Datensatz auswählen. Die Seitenleiste rechts enthält Informationen zum Datensatz.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

Der Umschalter **[!UICONTROL Fehlerdiagnose]** wird nur angezeigt, wenn der Umschalter **[!UICONTROL Partielle Erfassung]** deaktiviert ist. Mit dieser Funktion können [!DNL Platform] detaillierte Fehlermeldungen zu Ihren erfassten Stapeln generieren. Wenn der Umschalter **[!UICONTROL Partielle Erfassung]** aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

Jetzt können Sie Daten mit der Schaltfläche **Hinzufügen Daten** hochladen. Die Daten werden mit einer partiellen Erfassung erfasst.

### Verwenden Sie den Fluss &quot;[!UICONTROL CSV dem XDM-Schema zuordnen]&quot; {#map-flow}

Gehen Sie wie folgt vor, um den Fluss &quot;[!UICONTROL CSV zu XDM-Schema zuordnen]&quot;zu verwenden: [](../tutorials/map-a-csv-file.md) Sobald Sie den Schritt **[!UICONTROL Hinzufügen Daten]** erreicht haben, beachten Sie die Felder **[!UICONTROL Partielle Erfassung]** und **[!UICONTROL Fehlerdiagnose]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

Der Umschalter **[!UICONTROL Fehlerdiagnose]** wird nur angezeigt, wenn der Umschalter **[!UICONTROL Partielle Erfassung]** deaktiviert ist. Mit dieser Funktion können [!DNL Platform] detaillierte Fehlermeldungen zu Ihren erfassten Stapeln generieren. Wenn der Umschalter **[!UICONTROL Partielle Erfassung]** aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Die Fehlergrenze]** ermöglicht es Ihnen, den Prozentsatz der zulässigen Fehler festzulegen, bevor der gesamte Stapel fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

## Nächste Schritte {#next-steps}

In dieser Anleitung wurde beschrieben, wie Sie einen Datensatz erstellen oder ändern, um die partielle Batch-Erfassung zu aktivieren. Weiterführende Informationen zur Batch-Erfassung finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](./api-overview.md).

Informationen zur Überwachung von Fehlern bei der partiellen Erfassung finden Sie im Handbuch [Batch-Erfassungsfehlerdiagnose](../quality/error-diagnostics.md).
