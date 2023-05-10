---
keywords: Experience Platform;Startseite;beliebte Themen;Flow Service;
title: (Beta) Erstellen eines Flusslaufs für die On-Demand-Aufnahme mithilfe der Flow Service-API
description: In diesem Tutorial werden die Schritte zum Erstellen eines Flusslaufs für die On-Demand-Erfassung mithilfe der Flow Service-API beschrieben.
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 795b1af6421c713f580829588f954856e0a88277
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 14%

---

# (Beta) Erstellen Sie einen Flusslauf für die On-Demand-Erfassung mithilfe der [!DNL Flow Service] API

>[!IMPORTANT]
>
>Die On-Demand-Erfassung befindet sich derzeit in der Beta-Phase und Ihr Unternehmen hat möglicherweise noch keinen Zugriff darauf. Die in dieser Dokumentation beschriebene Funktionalität kann sich ändern.

Flussläufe stellen eine Instanz der Flussausführung dar. Wenn beispielsweise ein Fluss planmäßig um 9:00 Uhr, 10:00 Uhr und 11:00 Uhr ausgeführt wird, haben Sie drei Instanzen eines Flusslaufs. Flussläufe sind spezifisch für Ihre jeweilige Organisation.

Die On-Demand-Erfassung bietet Ihnen die Möglichkeit, einen Fluss zu erstellen, der für einen bestimmten Datenfluss ausgeführt wird. Auf diese Weise können Ihre Benutzer einen Flusslauf erstellen, der auf den angegebenen Parametern basiert, und einen Erfassungszyklus ohne Service-Token erstellen. Die On-Demand-Erfassung wird nur für Batch-Quellen unterstützt.

In diesem Tutorial werden die Schritte zum Verwenden der On-Demand-Erfassung und zum Erstellen eines Flusslaufs mit dem [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

>[!NOTE]
>
>Um einen Flusslauf zu erstellen, müssen Sie zunächst über die Fluss-ID eines Datenflusses verfügen, der für die einmalige Erfassung geplant ist.

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Erstellen eines Flusslaufs für eine tabellenbasierte Quelle

Um einen Fluss für eine tabellenbasierte Quelle zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service] API bei Angabe der Kennung des Flusses, für den Sie die Ausführung erstellen möchten, sowie der Werte für Start-, Endzeit- und Delta-Spalte.

>[!TIP]
>
>Tabellenbasierte Quellen umfassen die folgenden Quellkategorien: Werbung, Analysen, Einverständnis und Präferenzen, CRMs, Kundenerfolg, Datenbank, Marketing-Automatisierung, Zahlungen und Protokolle.

**API-Format**

```http
POST /runs/
```

**Anfrage**

Die folgende Anfrage erstellt einen Flusslauf für Fluss-ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Sie müssen nur die Variable `deltaColumn` beim Erstellen des ersten Flusslaufs. Danach `deltaColumn` wird als Teil von `copy` Transformation im Fluss und wird als Quelle der Wahrheit behandelt. Alle Versuche, die `deltaColumn` -Wert durch die Flusslaufparameter führt zu einem Fehler.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `flowId` | Die ID des Flusses, mit dem der Fluss erstellt wird. |
| `params.startTime` | Eine Ganzzahl, die die Startzeit der Ausführung definiert. Der Wert wird in Unix Epochenzeit dargestellt. |
| `params.windowStartTime` | Eine Ganzzahl, die die Startzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Eine Ganzzahl, die die Endzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `params.deltaColumn` | Die Delta-Spalte ist erforderlich, um die Daten zu partitionieren und neu aufgenommene Daten von historischen Daten zu trennen. **Hinweis**: Die `deltaColumn` wird nur bei der Erstellung des ersten Durchlaufs benötigt. |
| `params.deltaColumn.name` | Der Name der Delta-Spalte. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Flusslaufs zurück, einschließlich der eindeutigen Ausführung `id`.

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID des neu erstellten Flusslaufs. Siehe Handbuch unter [Abruf-Flussspezifikationen](../api/collect/database-nosql.md#specs) für weitere Informationen zu tabellenbasierten Ausführungsspezifikationen. |
| `etag` | Die Ressourcenversion des Flusslaufs. |
<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## Erstellen eines Flusslaufs für eine dateibasierte Quelle

Um einen Fluss für eine dateibasierte Quelle zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service] API bei Angabe der Kennung des Workflows, für den Sie die Ausführung erstellen möchten, und der Werte für Start- und Endzeit.

>[!TIP]
>
>Dateibasierte Quellen enthalten alle Cloud-Speicherquellen.

**API-Format**

```http
POST /runs/
```

**Anfrage**

Die folgende Anfrage erstellt einen Flusslauf für Fluss-ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `flowId` | Die ID des Flusses, mit dem der Fluss erstellt wird. |
| `params.startTime` | Eine Ganzzahl, die die Startzeit der Ausführung definiert. Der Wert wird in Unix Epochenzeit dargestellt. |
| `params.windowStartTime` | Eine Ganzzahl, die die Startzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Eine Ganzzahl, die die Endzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Flusslaufs zurück, einschließlich der eindeutigen Ausführung `id`.


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID des neu erstellten Flusslaufs. Siehe Handbuch unter [Abruf-Flussspezifikationen](../api/collect/database-nosql.md#specs) für weitere Informationen zu tabellenbasierten Ausführungsspezifikationen. |
| `etag` | Die Ressourcenversion des Flusslaufs. |

## Überwachen der Durchsatzabläufe

Nach der Erstellung des Flusslaufs können Sie die erfassten Daten überwachen, um Informationen über die Durchlaufvorgänge, den Abschlussstatus und Fehler anzuzeigen. Informationen zum Überwachen Ihrer Flussläufe mithilfe der API finden Sie im Tutorial zu [Überwachen von Datenflüssen in der API ](./monitor.md). Informationen zum Überwachen Ihrer Flussläufe mithilfe der Platform-Benutzeroberfläche finden Sie im Handbuch unter [Überwachen von Datenflüssen zu Quellen mithilfe des Monitoring-Dashboards](../../../dataflows/ui/monitor-sources.md).
