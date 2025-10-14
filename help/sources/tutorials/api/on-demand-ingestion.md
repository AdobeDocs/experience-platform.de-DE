---
keywords: Experience Platform;Startseite;beliebte Themen;Flow Service;
title: Erstellen einer Flussausführung für die On-Demand-Aufnahme mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Flussausführung für die On-Demand-Aufnahme erstellen
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 10%

---

# Erstellen einer Flussausführung für die On-Demand-Aufnahme mithilfe der [!DNL Flow Service]-API

Flussausführungen stellen eine Instanz der Flussausführung dar. Beispiel: Wenn ein Fluss so geplant ist, dass er stündlich um 9:00 Uhr, um 10:00 Uhr und um 11:00 Uhr ausgeführt wird, gibt es drei Instanzen eines Flussdurchgangs. Flussausführungen sind spezifisch für Ihre bestimmte Organisation.

Die On-Demand-Aufnahme bietet Ihnen die Möglichkeit, eine Flussausführung für einen bestimmten Datenfluss zu erstellen. Auf diese Weise können Ihre Benutzerinnen und Benutzer ohne Service-Token eine Flussausführung erstellen, die auf bestimmten Parametern basiert, und einen Aufnahmezyklus erstellen. Die On-Demand-Aufnahme wird nur für Batch-Quellen unterstützt.

In diesem Tutorial werden die Schritte zur Verwendung der On-Demand-Aufnahme und zur Erstellung einer Flussausführung mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben.

## Erste Schritte

>[!NOTE]
>
>Um eine Flussausführung zu erstellen, müssen Sie zunächst über die Fluss-ID eines Datenflusses verfügen, der für die einmalige Aufnahme geplant ist.

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [&#x200B; mit Experience Platform-APIs](../../../landing/api-guide.md).

## Erstellen einer Flussausführung für eine tabellenbasierte Quelle

Um einen Fluss für eine tabellenbasierte Quelle zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API. Geben Sie dabei die ID des Flusses an, für den Sie die Ausführung erstellen möchten, sowie Werte für Startzeit, Endzeit und Delta-Spalte.

>[!TIP]
>
>Zu den tabellenbasierten Quellen gehören die folgenden Quellkategorien: Werbung, Analysen, Einverständnis und Voreinstellungen, CRMs, Kundenerfolg, Datenbank, Marketing-Automatisierung, Zahlungen und Protokolle.

**API-Format**

```http
POST /runs/
```

**Anfrage**

Die folgende Anfrage erstellt eine Flussausführung für die Fluss-ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Sie müssen die `deltaColumn` nur beim Erstellen Ihrer ersten Flussausführung angeben. Danach werden `deltaColumn` als Teil `copy` Transformation im Fluss gepatcht und als Quelle der Wahrheit behandelt. Jeder Versuch, den `deltaColumn` über die Flussausführungsparameter zu ändern, führt zu einem Fehler.

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
| `flowId` | Die ID des Flusses, für den die Flussausführung erstellt wird. |
| `params.startTime` | Der geplante Zeitpunkt, zu dem die Ausführung des On-Demand-Flusses beginnt. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.windowStartTime` | Das früheste Datum und die früheste Uhrzeit, von dem/der die Daten abgerufen werden. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Datum und Uhrzeit, zu der die Daten abgerufen werden. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.deltaColumn` | Die Delta-Spalte ist erforderlich, um die Daten zu unterteilen und neu aufgenommene Daten von historischen Daten zu trennen. **Hinweis**: Die `deltaColumn` wird nur beim Erstellen der ersten Flussausführung benötigt. |
| `params.deltaColumn.name` | Der Name der Delta-Spalte. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Flussausführung zurück, einschließlich der eindeutigen `id`.

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
| `id` | Die ID der neu erstellten Flussausführung. Weitere Informationen zu tabellenbasierten [&#x200B; finden Sie &#x200B;](../api/collect/database-nosql.md#specs) Handbuch unter Abrufen von Flussspezifikationen . |
| `etag` | Die Ressourcenversion der Flussausführung. |

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

## Erstellen einer Flussausführung für eine dateibasierte Quelle

Um einen Fluss für eine dateibasierte Quelle zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API. Geben Sie dabei die ID des Flusses an, für den Sie den Durchlauf erstellen möchten, sowie die Werte für Startzeit und Endzeit.

>[!TIP]
>
>Dateibasierte Quellen umfassen alle Cloud-Speicherquellen.

**API-Format**

```http
POST /runs/
```

**Anfrage**

Die folgende Anfrage erstellt eine Flussausführung für die Fluss-ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

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
| `flowId` | Die ID des Flusses, für den die Flussausführung erstellt wird. |
| `params.startTime` | Der geplante Zeitpunkt, zu dem die Ausführung des On-Demand-Flusses beginnt. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.windowStartTime` | Das früheste Datum und die früheste Uhrzeit, von dem/der die Daten abgerufen werden. Dieser Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Datum und Uhrzeit, zu der die Daten abgerufen werden. Dieser Wert wird in Unix-Zeit dargestellt. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Flussausführung zurück, einschließlich der eindeutigen `id`.


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
| `id` | Die ID der neu erstellten Flussausführung. Weitere Informationen zu tabellenbasierten [&#x200B; finden Sie &#x200B;](../api/collect/database-nosql.md#specs) Handbuch unter Abrufen von Flussspezifikationen . |
| `etag` | Die Ressourcenversion der Flussausführung. |

## Überwachen von Flussausführungen

Nachdem Ihr Flussvorgang erstellt wurde, können Sie die Daten überwachen, die darin aufgenommen werden, um Informationen zu Flussausführungen, Abschlussstatus und Fehlern anzuzeigen. Informationen zum Überwachen Ihrer Datenflüsse mithilfe der API finden Sie im Tutorial [Überwachen von Datenflüssen in der API](./monitor.md). Informationen zum Überwachen Ihrer Flussausführungen mit der Experience Platform-Benutzeroberfläche finden Sie im Handbuch [Überwachen von Quelldatenflüssen mithilfe des Überwachungs-Dashboards](../../../dataflows/ui/monitor-sources.md).
