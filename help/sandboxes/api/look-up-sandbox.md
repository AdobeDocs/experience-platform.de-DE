---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Nachschlagen einer Sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: ef423a8c1b412315d03cddf7d8c351a232eb509b
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 100%

---


# Nachschlagen einer Sandbox

Sie können eine Sandbox mittels GET-Anfrage nachschlagen, in der Sie im Anfragepfad die `name`-Eigenschaft der jeweiligen Sandbox angeben.

**API-Format**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name`-Eigenschaft der Sandbox, die Sie nachschlagen möchten. |

**Anfrage**

Mit der nachfolgenden Anfrage wird eine Sandbox namens „dev-2“ abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei erfolgreicher Antwort werden Details zur Sandbox einschließlich `name`, `title`, `state` und `type` zurückgegeben.

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
| `name` | Der Name der Sandbox. Dient zum Suchen in API-Aufrufen. |
| `title` | Der Anzeigename für die Sandbox. |
| `state` | Der aktuelle Verarbeitungsstatus der Sandbox. Der Status einer Sandbox kann wie folgt lauten: <ul><li>**Erstellen**: Die Sandbox wurde erstellt, wird jedoch weiterhin vom System bereitgestellt.</li><li>**Aktiv**: Die Sandbox ist erstellt und aktiv.</li><li>**Fehlgeschlagen**: Aufgrund eines Fehlers konnte die Sandbox nicht vom System bereitgestellt werden und ist deaktiviert.</li><li>**Gelöscht**: Die Sandbox wurde manuell deaktiviert.</li></ul> |
| `type` | Der Sandbox-Typ, entweder „Entwicklung“ oder „Produktion“. |
| `isDefault` | Eine boolesche Eigenschaft, die angibt, ob diese Sandbox die Standard-Sandbox für die Organisation ist. In der Regel ist dies die Produktions-Sandbox. |
| `eTag` | Eine Kennung für eine bestimmte Version der Sandbox. Dieser Wert erleichtert Versionskontrolle und Caching und wird bei jeder Änderung an der Sandbox aktualisiert. |