---
keywords: Experience Platform;Home;beliebte Themen;Liste aktiver Sandboxen;Liste-Sandboxen
solution: Experience Platform
title: Liste Active Sandboxes für den aktuellen Benutzer in der API
topic: Entwicklerhandbuch
description: Sie können die für den aktuellen Benutzer aktiven Sandboxen Liste werden, indem Sie eine GET an den Stamm-Endpunkt anfordern.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 63%

---


# Liste aktiver Sandboxen für den aktuellen Benutzer in der API

>[!NOTE]
>
>Im Gegensatz zu anderen Endpunkten, die in der Sandbox-API bereitgestellt werden, steht dieser Endpunkt allen Benutzern zur Verfügung, auch solchen ohne Sandbox-Administrator-Zugriffsberechtigung.

Sie können die für den aktuellen Benutzer aktiven Sandboxes durch eine GET-Anfrage an den Root-Endpunkt (`/`) auflisten.

**API-Format**

```http
GET /{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse. Weitere Informationen finden Sie im Abschnitt zu [Abfrage parameters](#query). |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Sandboxes zurück, die für den aktuellen Benutzer aktiv sind, einschließlich Details wie `name`, `title`, `state` und `type`.

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
| `state` | Der aktuelle Verarbeitungsstatus der Sandbox. Der Status einer Sandbox kann wie folgt lauten: <ul><li>**Erstellen**: Die Sandbox wurde erstellt, wird jedoch weiterhin vom System bereitgestellt.</li><li>**Aktiv**: Die Sandbox ist erstellt und aktiv.</li><li>**Fehlgeschlagen**: Aufgrund eines Fehlers konnte die Sandbox nicht vom System bereitgestellt werden und ist deaktiviert.</li><li>**Gelöscht**: Die Sandbox wurde manuell deaktiviert.</li></ul> |
| `type` | Der Sandbox-Typ, entweder „Entwicklung“ oder „Produktion“. |
| `isDefault` | Eine boolesche Eigenschaft, die angibt, ob diese Sandbox die Standard-Sandbox für die Organisation ist. In der Regel ist dies die Produktions-Sandbox. |
| `eTag` | Eine Kennung für eine bestimmte Version der Sandbox. Dieser Wert erleichtert Versionskontrolle und Caching und wird bei jeder Änderung an der Sandbox aktualisiert. |

## Verwenden von Abfrageparametern {#query}

Die [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml)-API unterstützt die Verwendung von Abfragen-Parametern zum Anzeigen von Seiten- und Filterergebnissen bei der Auflistung von Sandboxen.

>[!NOTE]
>
>Die Parameter `limit` und `offset` für die Abfrage müssen zusammen angegeben werden. Wenn Sie nur eine angeben, gibt die API einen Fehler zurück. Wenn Sie none angeben, ist der Standardwert 50 und der Offset 0.

| Parameter | Beschreibung |
| --------- | ----------- |
| `limit` | Die maximale Anzahl von Datensätzen, die in der Antwort zurückgegeben werden. |
| `offset` | Die Anzahl der Entitäten vom ersten Datensatz zum Beginn (Offset) der Antwort-Liste. |
