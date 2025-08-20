---
title: API-Endpunkt für Audit-Ereignisse
description: Erfahren Sie, wie Sie Audit-Ereignisse in Experience Platform mithilfe der Audit Query API abrufen.
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: dec895e3ea625fb86d1891bad713185d39c47c81
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 20%

---

# Audit events-Endpunkt

Audit-Protokolle werden verwendet, um Details zu Benutzeraktivitäten für verschiedene Services und Funktionen bereitzustellen. Jede in einem Protokoll aufgezeichnete Aktion enthält Metadaten, die den Aktionstyp, das Datum und die Uhrzeit, die E-Mail-ID der oder des Benutzenden, die oder der die Aktion durchgeführt hat, und weitere für den Aktionstyp relevante Attribute angeben. Mit dem `/audit/events`-Endpunkt in der [!DNL Audit Query]-API können Sie Ereignisdaten für die Aktivität Ihres Unternehmens in [!DNL Experience Platform] programmgesteuert abrufen.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Bevor Sie fortfahren, lesen Sie im Handbuch [Erste Schritte](./getting-started.md) die Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Audit-Ereignisse auflisten

Sie können Ereignisdaten abrufen, indem Sie eine GET-Anfrage an den `/audit/events`-Endpunkt stellen und dabei die Ereignisse angeben, die Sie in der Payload abrufen möchten.

**API-Format**

```http
GET /audit/events
```

Die [!DNL Audit Query]-API unterstützt die Verwendung von Abfrageparametern zum Seiten- und Filtern von Ergebnissen beim Auflisten von Ereignissen.

| Parameter | Beschreibung |
| --- | --- |
| `limit` | Die maximale Anzahl von Datensätzen, die in der Antwort zurückgegeben werden sollen. Der `limit` ist 50. |
| `start` | Ein Zeiger auf das erste Element für die zurückgegebenen Suchergebnisse. Um auf die nächste Ergebnisseite zuzugreifen, sollte dieser Parameter um denselben Wert inkrementiert werden, der durch das Limit angegeben wird. Beispiel: Um auf die nächste Ergebnisseite für eine Anfrage mit limit=50 zuzugreifen, verwenden Sie den Parameter start=50, dann start=100 für die nachfolgende Seite usw. |
| `queryId` | Wenn Sie eine Abfrage an den /audit/events-Endpunkt stellen, enthält die Antwort eine queryId-Zeichenfolgeneigenschaft. Um dieselbe Abfrage in einem separaten Aufruf durchzuführen, können Sie den Wert der ID als einzelnen Abfrageparameter verwenden, anstatt die Suchparameter erneut manuell zu konfigurieren. |

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt die resultierenden Datenpunkte für die in der Anfrage angegebenen Metriken und Filter zurück.

```json
{
  "_embedded": {
    "events": [
      {
        "id": "6ecc125d-da03-4882-a944-88c707ddc3f7",
        "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
        "permissionResource": "Dataset",
        "permissionType": "WRITE",
        "assetType": "Dataset",
        "action": "Create",
        "status": "Allow",
        "failureCode": "",
        "timestamp": "2025-06-24T16:50:28.318+0000",
        "version": "1.0",
        "imsOrgId": "{ORGANIZATION_ID}",
        "region": "VA7",
        "authId": "e6b46821-e2b4-4729-952f-2e4afd713b31",
        "assetId": "685ad754fb1abe2b263df4b3",
        "assetName": "my-dataset",
        "sandboxName": "prod",
        "sandboxId": "{SANDBOX_ID}",
        "userEmail": "{USER_EMAIL}",
        "userIpAddresses": [
          "130.*.*.*",
          "10.*.*.*"
        ],
        "enhancedEvents": [
          {
            "id": "0ee91e42-ac46-4f35-a01a-f74a1569c404",
            "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
            "permissionResource": "Dataset",
            "permissionType": "Write",
            "assetType": "Dataset",
            "action": "Create",
            "status": "Success",
            "failureCode": "",
            "timestamp": "2025-06-24T16:50:28.883+0000",
            "assetId": "685ad754fb1abe2b263df4b3",
            "assetName": "my-dataset"
          }
        ]
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?property=user%253D%253Ddraghici%2540adobe.com"
    },
    "page": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3&limit=50{&start}",
      "templated": true
    }
  },
  "page": {
    "size": 1,
    "totalElements": 1,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `events` | Ein Array, dessen Objekte die einzelnen in der Anfrage angegebenen Ereignisse darstellen. Jedes -Objekt enthält Informationen zur Filterkonfiguration und die zurückgegebenen Ereignisdaten. |
| `userEmail` | Die E-Mail-Adresse des Benutzers, der das Ereignis ausgeführt hat. |
| `eventType` | Der Ereignistyp. Zu den Ereignistypen gehören `Core` und `Enhanced`. |
| `imsOrgId` | Die ID der Organisation, unter der das Ereignis stattgefunden hat. |
| `permissionResource` | Das Produkt oder die Funktion, das bzw. die die Berechtigung zum Ausführen der Aktion erteilt hat. Eine Ressource kann eine der folgenden sein: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | Der an der Aktion beteiligte Berechtigungstyp. |
| `assetType` | Der Typ der Experience Platform-Ressource, für die die Aktion ausgeführt wurde. |
| `assetId` | Eine eindeutige Kennung für die Experience Platform-Ressource, für die die Aktion ausgeführt wurde. |
| `assetName` | Der Name der Experience Platform-Ressource, für die die Aktion ausgeführt wurde. |
| `action` | Der Typ der Aktion, die für das Ereignis aufgezeichnet wurde. Eine Aktion kann eine der folgenden sein: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | Der Status der Aktion. Ein Status kann einer der folgenden sein: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
