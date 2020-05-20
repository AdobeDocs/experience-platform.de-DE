---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Eine Sandbox nachschlagen
topic: developer guide
translation-type: tm+mt
source-git-commit: ef423a8c1b412315d03cddf7d8c351a232eb509b
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 2%

---


# Eine Sandbox nachschlagen

Sie können eine einzelne Sandbox nachschlagen, indem Sie eine GET-Anforderung erstellen, die die `name` Eigenschaft der Sandbox im Anforderungspfad enthält.

**API-Format**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name` Eigenschaft der Sandbox, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anforderung ruft eine Sandbox mit dem Namen &quot;dev-2&quot;ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Details der Sandbox einschließlich ihrer `name`, `title`, `state`und `type`zurückgegeben.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name der Sandbox. Wird für Suchzwecke in API-Aufrufen verwendet. |
| `title` | Der Anzeigename für die Sandbox. |
| `state` | Der aktuelle Verarbeitungsstatus der Sandbox. Der Status einer Sandbox kann einer der folgenden sein: <ul><li>**Erstellen**: Die Sandbox wurde erstellt, wird jedoch weiterhin vom System bereitgestellt.</li><li>**aktiv**: Die Sandbox wird erstellt und aktiv.</li><li>**fehlgeschlagen**: Aufgrund eines Fehlers konnte die Sandbox nicht vom System bereitgestellt werden und ist deaktiviert.</li><li>**gelöscht**: Die Sandbox wurde manuell deaktiviert.</li></ul> |
| `type` | Der Sandbox-Typ, entweder &quot;Entwicklung&quot;oder &quot;Produktion&quot;. |
| `isDefault` | Eine boolesche Eigenschaft, die angibt, ob diese Sandbox die Standard-Sandbox für die Organisation ist. Normalerweise ist dies die Produktions-Sandbox. |
| `eTag` | Ein Bezeichner für eine bestimmte Version der Sandbox. Dieser Wert wird zur Versionskontrolle und zur Cacheeffizienz verwendet und wird bei jeder Änderung an der Sandbox aktualisiert. |