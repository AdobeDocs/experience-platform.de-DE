---
title: Export-API-Endpunkt für Audit-Ereignisse
description: Erfahren Sie, wie Sie Prüfereignisse in Experience Platform mithilfe der Auditabfrage-API exportieren.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Liste von Prüfereignissen exportieren

Sie können Ereignisdaten abrufen, indem Sie eine GET-Anfrage an die `/audit/export` -Endpunkt, der die Ereignisse angibt, die Sie in der Payload abrufen möchten.

**API-Format**

```http
GET /audit/export
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `timestamp` | Beim Filtern nach Zeitstempel empfiehlt es sich, einen Bereich mit den Operatoren > und &lt; anstelle eines exakten Werts zu verwenden. <br/>Beispiel: ?property=timestamp&lt;2020-02-08T02:46:48.610862Z&amp;property=timestamp>2020-01-01T02:46:48.610862Z |
| `status` | Der Status der Aktion. Ein Status kann einer der folgenden sein: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |
| `action` | Die Art der Aktion, die für das Ereignis aufgezeichnet wurde. Eine Aktion kann eine der folgenden sein: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `user` | Der Benutzer, der das Ereignis ausgeführt hat. |
| `assetType` | Der Typ der Platform-Ressource, für die die Aktion ausgeführt wurde. |

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

Die Ergebnisse werden in einer CSV-Datei für den Export generiert. Eine erfolgreiche Antwort gibt HTTP 307 ohne Antworttext zurück. Ein Link zur Exportdatei wird im Abschnitt `Location` Antwortheader.
