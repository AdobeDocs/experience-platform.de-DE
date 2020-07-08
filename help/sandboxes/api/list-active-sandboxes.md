---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Liste aktiver Sandboxen für den aktuellen Benutzer
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# Liste aktiver Sandboxen für den aktuellen Benutzer

>[!NOTE]
>
>Im Gegensatz zu anderen Endpunkten, die in der Sandbox-API bereitgestellt werden, steht dieser Endpunkt allen Benutzern zur Verfügung, auch solchen ohne Sandbox-Administratorzugriffsberechtigung.

Sie können die für den aktuellen Benutzer aktiven Sandboxen durch eine GET-Anforderung an den Stamm-Endpunkt (`/`) Liste werden.

**API-Format**

```http
GET /
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Sandboxen zurück, die für den aktuellen Benutzer aktiv sind, einschließlich Details wie `name`, `title`, `state`und `type`.

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
    ]
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
