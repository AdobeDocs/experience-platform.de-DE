---
title: API-Endpunkt für den Export von Audit-Ereignissen
description: Erfahren Sie, wie Sie Audit-Ereignisse in Experience Platform mithilfe der Audit Query API exportieren.
role: Developer
feature: Audits, API
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 4%

---

# Exportieren einer Liste von Audit-Ereignissen

Sie können Ereignisdaten abrufen, indem Sie eine GET-Anfrage an den `/audit/export`-Endpunkt stellen und dabei die Ereignisse angeben, die Sie in der Payload abrufen möchten.

**API-Format**

```http
GET /audit/export
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `timestamp` | Beim Filtern nach Zeitstempel wird empfohlen, einen Bereich mit den Operatoren > und &lt; anstelle eines exakten Werts zu verwenden. <br/>Beispiel: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | Der Status der Aktion. Ein Status kann einer der folgenden sein: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>Beispiel: `?property=status==Deny`. |
| `action` | Der Typ der Aktion, die für das Ereignis aufgezeichnet wurde. Eine Aktion kann eine der folgenden sein: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> Beispiel: `?property=action==Create`. |
| `user` | Der Benutzer, der das Ereignis ausgeführt hat. |
| `assetType` | Der Typ der Experience Platform-Ressource, für die die Aktion ausgeführt wurde. <br/>Beispiel: `?property=assetType==<an asset type>`. |

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Antwort**

Die Ergebnisse werden in eine CSV-Datei für den Export generiert. Eine erfolgreiche Antwort gibt HTTP 307 ohne Antworttext zurück. Ein Link zur Exportdatei wird im `Location` Antwort-Header bereitgestellt.
