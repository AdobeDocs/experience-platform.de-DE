---
keywords: Experience Platform; Startseite; beliebte Themen; Batch-Erfassung; Batch-Erfassung; partielle Erfassung; partielle Erfassung; Fehler abrufen; Fehler abrufen; partielle Batch-Erfassung; partielle Batch-Erfassung; Teil; Erfassung; Aufnahme;
solution: Experience Platform
title: Partielle Batch-Erfassung - Übersicht
topic-legacy: overview
description: Dieses Dokument enthält eine Anleitung zum Verwalten der partiellen Batch-Erfassung.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: d380b4d2a75efb1c34010a30c619649a7b99643c
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 46%

---

# Partielle Batch-Erfassung

Partielle Batch-Erfassung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle fehlerhaften Daten in Batches separat verarbeitet werden (zusammen mit Details dazu, warum sie ungültig sind).

Dieses Dokument enthält eine Anleitung zum Verwalten der partiellen Batch-Erfassung.

## Erste Schritte

Diese Anleitung setzt grundlegende Kenntnisse zu den verschiedenen Adobe Experience Platform-Diensten voraus, die mit der partiellen Batch-Erfassung verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Batch-Erfassung](./overview.md)[!DNL Platform]: Die Methode, mit der Daten aus Datendateien wie CSV und Parquet erfasst und speichert.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich Aufrufe an [!DNL Platform] APIs.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Aktivieren eines Batches für die partielle Batch-Erfassung in der API {#enable-api}

>[!NOTE]
>
>In diesem Abschnitt wird die Aktivierung eines Batches für die partielle Batch-Erfassung mithilfe der API beschrieben. Anweisungen zur Verwendung der Benutzeroberfläche finden Sie in der [Aktivieren eines Batches für die partielle Batch-Erfassung in der Benutzeroberfläche](#enable-ui) Schritt.

Sie können einen neuen Batch mit aktivierter partieller Erfassung erstellen.

Gehen Sie wie im Abschnitt [Entwicklerhandbuch zur Batch-Erfassung](./api-overview.md). Sobald Sie die **[!UICONTROL Batch erstellen]** -Schritt, fügen Sie das folgende Feld im Anfragetext hinzu:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `enableErrorDiagnostics` | Eine Markierung, die Folgendes ermöglicht: [!DNL Platform] , um detaillierte Fehlermeldungen zu Ihrem Batch zu generieren. |
| `partialIngestionPercent` | Der Prozentsatz der akzeptablen Fehler, bevor der gesamte Batch fehlschlägt. In diesem Beispiel können also maximal 5 % des Batches Fehler sein, bevor er fehlschlägt. |


## Aktivieren eines Batches für die partielle Batch-Erfassung in der Benutzeroberfläche {#enable-ui}

>[!NOTE]
>
>In diesem Abschnitt wird die Aktivierung eines Batches für die partielle Batch-Erfassung mithilfe der Benutzeroberfläche beschrieben. Wenn Sie einen Batch bereits für die partielle Batch-Erfassung mithilfe der API aktiviert haben, können Sie mit dem nächsten Abschnitt fortfahren.

So aktivieren Sie einen Batch für die partielle Erfassung über [!DNL Platform] Benutzeroberfläche: Sie können einen neuen Batch über Quellverbindungen erstellen, einen neuen Batch in einem vorhandenen Datensatz erstellen oder einen neuen Batch über die[!UICONTROL Zuordnen von CSV zu XDM-Fluss]&quot;.

### Neue Quellverbindung erstellen {#new-source}

Gehen Sie wie im Abschnitt [Quellen - Übersicht](../../sources/home.md). Sobald Sie die **[!UICONTROL Datenflussdetails]** -Schritt, beachten Sie die **[!UICONTROL Partielle Erfassung]** und **[!UICONTROL Fehlerdiagnose]** -Felder.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

Die **[!UICONTROL Fehlerdiagnose]** Umschalten wird nur angezeigt, wenn **[!UICONTROL Partielle Erfassung]** -Umschalter deaktiviert ist. Diese Funktion ermöglicht [!DNL Platform] , um detaillierte Fehlermeldungen zu den erfassten Batches zu generieren. Wenn die Variable **[!UICONTROL Partielle Erfassung]** Umschalter aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch durchgesetzt.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

### Verwenden eines vorhandenen Datensatzes {#existing-dataset}

Um einen vorhandenen Datensatz zu verwenden, wählen Sie zunächst einen Datensatz aus. Die Seitenleiste rechts enthält Informationen zum Datensatz.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

Die **[!UICONTROL Fehlerdiagnose]** Umschalten wird nur angezeigt, wenn **[!UICONTROL Partielle Erfassung]** -Umschalter deaktiviert ist. Diese Funktion ermöglicht [!DNL Platform] , um detaillierte Fehlermeldungen zu den erfassten Batches zu generieren. Wenn die Variable **[!UICONTROL Partielle Erfassung]** Umschalter aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch durchgesetzt.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

Jetzt können Sie Daten mit dem **Daten hinzufügen** und wird mithilfe der partiellen Erfassung erfasst.

### Verwenden Sie die[!UICONTROL Zuordnen von CSV zu XDM-Schema]&quot; Fluss {#map-flow}

So verwenden Sie &quot;[!UICONTROL Zuordnen von CSV zu XDM-Schema]&quot;, folgen Sie den aufgelisteten Schritten im Abschnitt [Tutorial zur CSV-Datei zuordnen](../tutorials/map-csv/overview.md). Sobald Sie die **[!UICONTROL Daten hinzufügen]** -Schritt, beachten Sie die **[!UICONTROL Partielle Erfassung]** und **[!UICONTROL Fehlerdiagnose]** -Felder.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

Die **[!UICONTROL Fehlerdiagnose]** Umschalten wird nur angezeigt, wenn **[!UICONTROL Partielle Erfassung]** -Umschalter deaktiviert ist. Diese Funktion ermöglicht [!DNL Platform] , um detaillierte Fehlermeldungen zu den erfassten Batches zu generieren. Wenn die Variable **[!UICONTROL Partielle Erfassung]** Umschalter aktiviert ist, wird die erweiterte Fehlerdiagnose automatisch durchgesetzt.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Fehlerschwellenwert]** Sie können den Prozentsatz der akzeptablen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

## Nächste Schritte {#next-steps}

In dieser Anleitung wurde beschrieben, wie Sie einen Datensatz erstellen oder ändern, um die partielle Batch-Erfassung zu aktivieren. Weiterführende Informationen zur Batch-Erfassung finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](./api-overview.md).

Informationen zur Überwachung von Fehlern bei der partiellen Erfassung finden Sie im Abschnitt [Handbuch zur Fehlerdiagnose bei der Batch-Erfassung](../quality/error-diagnostics.md).
