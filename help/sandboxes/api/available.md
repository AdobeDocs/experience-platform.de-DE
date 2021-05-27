---
keywords: Experience Platform; Startseite; beliebte Themen; Liste verfügbarer Sandboxes; Listen-Sandboxes
solution: Experience Platform
title: Verfügbarer Sandbox-API-Endpunkt
topic-legacy: developer guide
description: Sie können die für den aktuellen Benutzer verfügbaren Sandboxes auflisten, indem Sie eine GET-Anfrage an den verfügbaren Sandbox-Endpunkt senden.
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 41%

---

# Verfügbare Sandbox-Endpunkte

>[!NOTE]
>
>Im Gegensatz zu anderen Endpunkten, die in der Sandbox-API bereitgestellt werden, steht dieser Endpunkt allen Benutzern zur Verfügung, auch solchen ohne Sandbox-Administrator-Zugriffsberechtigung.

Sie können die für den aktuellen Benutzer verfügbaren Sandboxes auflisten, indem Sie eine GET-Anfrage an den verfügbaren Sandbox-Endpunkt senden.

**API-Format**

```http
GET /{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse. Eine Liste der verfügbaren Parameter finden Sie im Dokument [Anhang](./appendix.md#query) . |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Sandboxes zurück, die für den aktuellen Benutzer verfügbar sind, einschließlich Details wie `name`, `title`, `state` und `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name der Sandbox. Dient zum Suchen in API-Aufrufen. |
| `title` | Der Anzeigename für die Sandbox. |
| `state` | Der aktuelle Verarbeitungsstatus der Sandbox. Der Status einer Sandbox kann wie folgt lauten: <ul><li>`creating`: Die Sandbox wurde erstellt, wird jedoch weiterhin vom System bereitgestellt.</li><li>`active`: Die Sandbox wird erstellt und aktiv.</li><li>`failed`: Aufgrund eines Fehlers konnte die Sandbox nicht vom System bereitgestellt werden und ist deaktiviert.</li><li>`deleted`: Die Sandbox wurde manuell deaktiviert.</li></ul> |
| `type` | Der Sandbox-Typ, entweder „Entwicklung“ oder „Produktion“. |
| `isDefault` | Eine boolesche Eigenschaft, die angibt, ob diese Sandbox die standardmäßige Produktions-Sandbox für die Organisation ist. |
| `eTag` | Eine Kennung für eine bestimmte Version der Sandbox. Dieser Wert erleichtert Versionskontrolle und Caching und wird bei jeder Änderung an der Sandbox aktualisiert. |
