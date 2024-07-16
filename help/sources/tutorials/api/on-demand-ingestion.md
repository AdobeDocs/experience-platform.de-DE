---
keywords: Experience Platform;Startseite;beliebte Themen;Flow Service;
title: Erstellen eines Flusslaufs für die On-Demand-Erfassung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API einen Flusslauf für die On-Demand-Erfassung erstellen.
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: cea12160656ba0724789db03e62213022bacd645
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 13%

---

# Erstellen eines Flusslaufs für die On-Demand-Erfassung mithilfe der [!DNL Flow Service]-API

Flussläufe stellen eine Instanz der Flussausführung dar. Wenn beispielsweise ein Fluss planmäßig um 9:00 Uhr, 10:00 Uhr und 11:00 Uhr ausgeführt wird, haben Sie drei Instanzen eines Flusslaufs. Flussläufe sind spezifisch für Ihre jeweilige Organisation.

Die On-Demand-Erfassung bietet Ihnen die Möglichkeit, einen Fluss zu erstellen, der für einen bestimmten Datenfluss ausgeführt wird. Auf diese Weise können Ihre Benutzer einen Flusslauf erstellen, der auf den angegebenen Parametern basiert, und einen Erfassungszyklus ohne Service-Token erstellen. Die On-Demand-Erfassung wird nur für Batch-Quellen unterstützt.

In diesem Tutorial werden die Schritte zum Verwenden der On-Demand-Erfassung und zum Erstellen eines Flusslaufs mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben.

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

Um einen Fluss für eine tabellenbasierte Quelle zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service] -API und geben Sie dabei die Kennung des Flusses an, für den Sie die Ausführung erstellen möchten, sowie Werte für Start-, Endzeit- und Delta-Spalte.

>[!TIP]
>
>Zu den tabellenbasierten Quellen gehören die folgenden Quellkategorien: Werbung, Analysen, Zustimmung und Voreinstellungen, CRMs, Kundenerfolg, Datenbank, Marketing-Automatisierung, Zahlungen und Protokolle.

**API-Format**

```http
POST /runs/
```

**Anfrage**

Die folgende Anfrage erstellt einen Flusslauf für die Fluss-ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Sie müssen nur den Wert `deltaColumn` angeben, wenn Sie den ersten Flusslauf erstellen. Danach wird `deltaColumn` als Teil der `copy`-Transformation im Fluss gepatcht und als &quot;Source of Truth&quot;behandelt. Alle Versuche, den Wert `deltaColumn` durch die Ausführungsparameter des Flusses zu ändern, führen zu einem Fehler.

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
| `params.startTime` | Die geplante Zeit, zu der der On-Demand-Fluss beginnt. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.windowStartTime` | Das früheste Datum und die früheste Uhrzeit, aus der Daten abgerufen werden. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Datum und Uhrzeit des Abrufs der Daten. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.deltaColumn` | Die Delta-Spalte ist erforderlich, um die Daten zu partitionieren und neu aufgenommene Daten von historischen Daten zu trennen. **Hinweis**: Der `deltaColumn` ist nur erforderlich, wenn Sie Ihren ersten Flusslauf erstellen. |
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
| `id` | Die ID des neu erstellten Flusslaufs. Weitere Informationen zu tabellenbasierten Ausführungsspezifikationen finden Sie im Handbuch zum [Abrufen von Flussspezifikationen](../api/collect/database-nosql.md#specs) . |
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

Um einen Fluss für eine dateibasierte Quelle zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service] -API und geben Sie dabei die ID des Flusses an, für den Sie die Ausführung erstellen möchten, sowie die Werte für Start- und Endzeit.

>[!TIP]
>
>Dateibasierte Quellen enthalten alle Cloud-Speicherquellen.

**API-Format**

```http
POST /runs/
```

**Anfrage**

Die folgende Anfrage erstellt einen Flusslauf für die Fluss-ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

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
| `params.startTime` | Die geplante Zeit, zu der der On-Demand-Fluss beginnt. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.windowStartTime` | Das früheste Datum und die früheste Uhrzeit, aus der Daten abgerufen werden. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Datum und Uhrzeit des Abrufs der Daten. Dieser Wert wird in Unix-Zeit dargestellt. |

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
| `id` | Die ID des neu erstellten Flusslaufs. Weitere Informationen zu tabellenbasierten Ausführungsspezifikationen finden Sie im Handbuch zum [Abrufen von Flussspezifikationen](../api/collect/database-nosql.md#specs) . |
| `etag` | Die Ressourcenversion des Flusslaufs. |

## Überwachen der Durchsatzabläufe

Nach der Erstellung des Flusslaufs können Sie die erfassten Daten überwachen, um Informationen über die Durchlaufvorgänge, den Abschlussstatus und Fehler anzuzeigen. Informationen zum Überwachen Ihrer Flussläufe mithilfe der API finden Sie im Tutorial zum [Überwachen von Datenflüssen in der API](./monitor.md). Informationen zum Überwachen Ihrer Flussläufe mithilfe der Platform-Benutzeroberfläche finden Sie im Handbuch zum [Überwachen von Datenflüssen für Quellen mithilfe des Monitoring-Dashboards](../../../dataflows/ui/monitor-sources.md).
