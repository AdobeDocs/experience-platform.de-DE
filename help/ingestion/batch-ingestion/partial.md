---
keywords: Experience Platform;Startseite;beliebte Themen;Batch-Aufnahme;Batch-Aufnahme;partielle Aufnahme;partielle Aufnahme;Fehler abrufen;Fehler abrufen;partielle Batch-Aufnahme;partielle Batch-Aufnahme;partielle Aufnahme;Aufnahme;Aufnahme;
solution: Experience Platform
title: Übersicht über die partielle Batch-Aufnahme
description: Dieses Dokument enthält eine Anleitung zum Verwalten der partiellen Batch-Erfassung.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 45%

---

# Partielle Batch-Erfassung

Partielle Batch-Erfassung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle fehlerhaften Daten in Batches separat verarbeitet werden (zusammen mit Details dazu, warum sie ungültig sind).

Dieses Dokument enthält eine Anleitung zum Verwalten der partiellen Batch-Erfassung.

## Erste Schritte

Diese Anleitung setzt grundlegende Kenntnisse zu den verschiedenen Adobe Experience Platform-Diensten voraus, die mit der partiellen Batch-Erfassung verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Batch-Aufnahme](./overview.md): Die Methode, die [!DNL Experience Platform] Daten aus Datendateien wie CSV und Parquet aufnimmt und speichert.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Experience Platform]-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Aktivieren eines Batches für die partielle Batch-Aufnahme in der API {#enable-api}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie einen Batch für die partielle Batch-Aufnahme mithilfe der -API aktivieren. Anweisungen zur Verwendung der Benutzeroberfläche finden Sie im Schritt [Aktivieren eines Batches für die partielle Batch-Aufnahme in der Benutzeroberfläche](#enable-ui).

Sie können einen neuen Batch mit aktivierter partieller Aufnahme erstellen.

Um einen neuen Batch zu erstellen, befolgen Sie die Schritte im [Entwicklerhandbuch zur Batch-Aufnahme](./api-overview.md). Nachdem Sie den Schritt **[!UICONTROL Batch erstellen]** erreicht haben, fügen Sie das folgende Feld zum Anfrageinhalt hinzu:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `enableErrorDiagnostics` | Eine Markierung, mit der [!DNL Experience Platform] detaillierte Fehlermeldungen über Ihren Batch generieren können. |
| `partialIngestionPercent` | Der Prozentsatz der akzeptablen Fehler, bevor der gesamte Batch fehlschlägt. In diesem Beispiel können also maximal 5 % des Batches Fehler sein, bevor er fehlschlägt. |


## Aktivieren eines Batches für die partielle Batch-Aufnahme in der Benutzeroberfläche {#enable-ui}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie einen Batch für die partielle Batch-Aufnahme über die Benutzeroberfläche aktivieren. Wenn Sie bereits einen Batch für die partielle Batch-Aufnahme mithilfe der API aktiviert haben, können Sie mit dem nächsten Abschnitt fortfahren.

Um einen Batch für die partielle Aufnahme über die [!DNL Experience Platform]-Benutzeroberfläche zu aktivieren, können Sie einen neuen Batch über Quellverbindungen erstellen, einen neuen Batch in einem vorhandenen Datensatz erstellen oder einen neuen Batch über den &quot;[!UICONTROL CSV-XDM-Fluss zuordnen] erstellen.

### Erstellen einer neuen Quellverbindung {#new-source}

Um eine neue Quellverbindung zu erstellen, führen Sie die in der [Quellen - Übersicht](../../sources/home.md) aufgelisteten Schritte aus. Nachdem Sie den Schritt **[!UICONTROL Datenflussdetails]** erreicht haben, notieren Sie sich die Felder **[!UICONTROL Partielle Aufnahme]** und **[!UICONTROL Fehlerdiagnose]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

Der Umschalter **[!UICONTROL Fehlerdiagnose]** wird nur angezeigt, wenn **[!UICONTROL Umschalter Partielle Aufnahme]** deaktiviert ist. Mit dieser Funktion können [!DNL Experience Platform] detaillierte Fehlermeldungen über Ihre aufgenommenen Batches generieren. Wenn der Umschalter **[!UICONTROL Partielle Aufnahme]** aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

### Verwenden eines vorhandenen Datensatzes {#existing-dataset}

Um einen vorhandenen Datensatz zu verwenden, wählen Sie zunächst einen Datensatz aus. Die Seitenleiste rechts enthält Informationen zum Datensatz.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

Der Umschalter **[!UICONTROL Fehlerdiagnose]** wird nur angezeigt, wenn **[!UICONTROL Umschalter Partielle Aufnahme]** deaktiviert ist. Mit dieser Funktion können [!DNL Experience Platform] detaillierte Fehlermeldungen über Ihre aufgenommenen Batches generieren. Wenn der Umschalter **[!UICONTROL Partielle Aufnahme]** aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

Jetzt können Sie Daten mit der Schaltfläche **Daten hinzufügen** hochladen und sie werden mit der partiellen Aufnahme aufgenommen.

### Verwenden des Flusses &quot;[!UICONTROL CSV zu XDM-Schema &#x200B;]&quot; {#map-flow}

Um den Fluss &quot;[!UICONTROL CSV zu XDM-Schema zuordnen] zu verwenden, führen Sie die im Tutorial [Zuordnen einer CSV-Datei“ ](../tutorials/map-csv/overview.md) Schritte aus. Nachdem Sie den Schritt **[!UICONTROL Daten hinzufügen]** erreicht haben, notieren Sie sich die Felder **[!UICONTROL Partielle Aufnahme]** und **[!UICONTROL Fehlerdiagnose]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

Der Umschalter **[!UICONTROL Fehlerdiagnose]** wird nur angezeigt, wenn **[!UICONTROL Umschalter Partielle Aufnahme]** deaktiviert ist. Mit dieser Funktion können [!DNL Experience Platform] detaillierte Fehlermeldungen über Ihre aufgenommenen Batches generieren. Wenn der Umschalter **[!UICONTROL Partielle Aufnahme]** aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch erzwungen.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Mit **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der akzeptablen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

## Nächste Schritte {#next-steps}

In dieser Anleitung wurde beschrieben, wie Sie einen Datensatz erstellen oder ändern, um die partielle Batch-Erfassung zu aktivieren. Weiterführende Informationen zur Batch-Erfassung finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](./api-overview.md).

Informationen zum Überwachen partieller Aufnahmefehler finden Sie im [Handbuch zur Fehlerdiagnose bei der Batch](../quality/error-diagnostics.md).
