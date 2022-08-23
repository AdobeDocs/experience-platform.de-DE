---
keywords: Experience Platform; Startseite; beliebte Themen; Flussdienst;
title: (Beta) Erstellen eines Flusslaufs für die On-Demand-Aufnahme mithilfe der Flow Service-API
description: In diesem Tutorial werden die Schritte zum Erstellen eines Flusslaufs für die On-Demand-Erfassung mithilfe der Flow Service-API beschrieben.
source-git-commit: ab496c7a32c20487f47850c2c571976dff57704f
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 10%

---

# (Beta) Erstellen Sie einen Flusslauf für die On-Demand-Erfassung mithilfe der [!DNL Flow Service] API

>[!IMPORTANT]
>
>Die On-Demand-Erfassung befindet sich derzeit in der Beta-Phase und Ihr Unternehmen hat möglicherweise noch keinen Zugriff darauf. Die in dieser Dokumentation beschriebene Funktionalität kann sich ändern.

Flussläufe stellen eine Instanz der Flussausführung dar. Wenn beispielsweise ein Fluss planmäßig um 9:00 Uhr, 10:00 Uhr und 11:00 Uhr ausgeführt wird, haben Sie drei Instanzen eines Flusslaufs. Flussläufe sind spezifisch für Ihre jeweilige Organisation.

Die On-Demand-Erfassung bietet Ihnen die Möglichkeit, einen Fluss zu erstellen, der für einen bestimmten Datenfluss ausgeführt wird. Auf diese Weise können Ihre Benutzer einen Flusslauf erstellen, der auf den angegebenen Parametern basiert, und einen Erfassungszyklus ohne Service-Token erstellen.

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
| `params.windowStartTime` | Eine Ganzzahl, die die Startzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Eine Ganzzahl, die die Endzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `params.deltaColumn` | Die Delta-Spalte ist erforderlich, um die Daten zu partitionieren und neu aufgenommene Daten von historischen Daten zu trennen. |
| `params.deltaColumn.name` | Der Name der Delta-Spalte. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Flusslaufs zurück, einschließlich der eindeutigen Ausführung `id`.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567",
        "deltaColumn": {
            "name": "DOB"
        }
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID des neu erstellten Flusslaufs. Siehe Handbuch unter [Abruf-Flussspezifikationen](../api/collect/database-nosql.md#specs) für weitere Informationen zu tabellenbasierten Ausführungsspezifikationen. |
| `createdAt` | Der Unix-Zeitstempel, der angibt, wann der Fluss erstellt wurde. |
| `updatedAt` | Der Unix-Zeitstempel, der angibt, wann der Fluss zuletzt aktualisiert wurde. |
| `createdBy` | Die Organisations-ID des Benutzers, der den Flusslauf erstellt hat. |
| `updatedBy` | Die Organisations-ID des Benutzers, der die Flussausführung zuletzt aktualisiert hat. |
| `createdClient` | Der Anwendungs-Client, der die Flussausführung erstellt hat. |
| `updatedClient` | Der Anwendungs-Client, der die Flussausführung zuletzt aktualisiert hat. |
| `sandboxId` | Die ID der Sandbox, die den Fluss-Lauf enthält. |
| `sandboxName` | Der Name der Sandbox, die den Fluss-Lauf enthält. |
| `imsOrgId` | Die Organisations-ID. |
| `flowId` | Die ID des Flusses, für den der Fluss ausgeführt wird. |
| `params.windowStartTime` | Eine Ganzzahl, die die Startzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Eine Ganzzahl, die die Endzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `params.deltaColumn` | Die Delta-Spalte ist erforderlich, um die Daten zu partitionieren und neu aufgenommene Daten von historischen Daten zu trennen. **Hinweis**: Die `deltaColumn` wird nur bei der Erstellung des ersten Durchlaufs benötigt. |
| `params.deltaColumn.name` | Der Name der Delta-Spalte. |
| `etag` | Die Ressourcenversion des Flusslaufs. |
| `metrics` | Diese Eigenschaft zeigt eine Statuszusammenfassung für die Flussausführung an. |

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
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `flowId` | Die ID des Flusses, mit dem der Fluss erstellt wird. |
| `params.windowStartTime` | Eine Ganzzahl, die die Startzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Eine Ganzzahl, die die Endzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Flusslaufs zurück, einschließlich der eindeutigen Ausführung `id`.


```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567"
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID des neu erstellten Flusslaufs. Siehe Handbuch unter [Abruf-Flussspezifikationen](../api/collect/cloud-storage.md#specs) für weitere Informationen zu dateibasierten Ausführungsspezifikationen. |
| `createdAt` | Der Unix-Zeitstempel, der angibt, wann der Fluss erstellt wurde. |
| `updatedAt` | Der Unix-Zeitstempel, der angibt, wann der Fluss zuletzt aktualisiert wurde. |
| `createdBy` | Die Organisations-ID des Benutzers, der den Flusslauf erstellt hat. |
| `updatedBy` | Die Organisations-ID des Benutzers, der die Flussausführung zuletzt aktualisiert hat. |
| `createdClient` | Der Anwendungs-Client, der die Flussausführung erstellt hat. |
| `updatedClient` | Der Anwendungs-Client, der die Flussausführung zuletzt aktualisiert hat. |
| `sandboxId` | Die ID der Sandbox, die den Fluss-Lauf enthält. |
| `sandboxName` | Der Name der Sandbox, die den Fluss-Lauf enthält. |
| `imsOrgId` | Die Organisations-ID. |
| `flowId` | Die ID des Flusses, für den der Fluss ausgeführt wird. |
| `params.windowStartTime` | Eine Ganzzahl, die die Startzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `params.windowEndTime` | Eine Ganzzahl, die die Endzeit des Fensters definiert, während dem Daten abgerufen werden sollen. Der Wert wird in Unix-Zeit dargestellt. |
| `etag` | Die Ressourcenversion des Flusslaufs. |
| `metrics` | Diese Eigenschaft zeigt eine Statuszusammenfassung für die Flussausführung an. |


## Überwachen der Durchsatzabläufe

Nach der Erstellung des Flusslaufs können Sie die erfassten Daten überwachen, um Informationen über die Durchlaufvorgänge, den Abschlussstatus und Fehler anzuzeigen. Informationen zum Überwachen Ihrer Flussläufe mithilfe der API finden Sie im Tutorial zu [Überwachen von Datenflüssen in der API ](./monitor.md). Informationen zum Überwachen Ihrer Flussläufe mithilfe der Platform-Benutzeroberfläche finden Sie im Handbuch unter [Überwachen von Datenflüssen zu Quellen mithilfe des Monitoring-Dashboards](../../../dataflows/ui/monitor-sources.md).
