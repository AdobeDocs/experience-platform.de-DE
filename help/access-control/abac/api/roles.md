---
keywords: Experience Platform;Startseite;beliebte Themen;api;attributbasierte Zugriffssteuerung;attributbasierte Zugriffssteuerung
solution: Experience Platform
title: Roles API-Endpunkt
description: Mit dem /roles-Endpunkt in der attributbasierten Zugriffssteuerungs-API können Sie Rollen in Adobe Experience Platform programmgesteuert verwalten.
role: Developer
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 27%

---

# Roles-Endpunkt

>[!NOTE]
>
>Wenn ein Benutzer-Token übergeben wird, muss der Benutzer des Tokens über eine „org admin“-Rolle für die angeforderte Organisation verfügen.

Rollen definieren den Zugriff, den ein Administrator, ein Spezialist oder ein Endbenutzer auf Ressourcen in Ihrer Organisation hat. In einer rollenbasierten Zugriffssteuerungsumgebung erfolgt die Bereitstellung des Benutzerzugriffs über gemeinsame Zuständigkeiten und Anforderungen. Eine Rolle verfügt über bestimmte Berechtigungen, wobei Mitglieder Ihrer Organisation je nach dem Umfang des Lese- oder Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden können.

Mit dem `/roles`-Endpunkt in der attributbasierten Zugriffssteuerungs-API können Sie Rollen in Ihrer Organisation programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der attributbasierten Zugriffssteuerungs-API. Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste von Rollen {#list}

Sie können alle vorhandenen Rollen, die zu Ihrer Organisation gehören, auflisten, indem Sie eine GET-Anfrage an den `/roles`-Endpunkt stellen.

**API-Format**

```http
GET /roles/
```

**Anfrage**

Mit der folgenden Anfrage wird eine Liste der Rollen abgerufen, die zu Ihrer Organisation gehören.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Bei einer erfolgreichen Antwort wird eine Liste der Rollen in Ihrer Organisation zurückgegeben, einschließlich Informationen zum jeweiligen Rollentyp, zu Berechtigungssätzen und Betreffattributen.

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft „description“ enthält zusätzliche Informationen über Ihre Rolle. |
| `roleType` | Der zugewiesene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihrer Organisation an, die für eine bestimmte Rolle bereitgestellt werden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Subjekt und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbeschriftungen an, die auf die abgefragte Rolle angewendet wurden. |

## Suchen einer Rolle {#lookup}

Sie können eine einzelne Rolle suchen, indem Sie eine GET-Anfrage stellen, die die entsprechende `roleId` im Anfragepfad enthält.

**API-Format**

```http
GET /roles/{ROLE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {ROLE_ID} | Die ID der Rolle, die Sie suchen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden Informationen zu `{ROLE_ID}` abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt Details für die abgefragte Rollen-ID zurück, einschließlich Informationen zu Rollentyp, Berechtigungssätzen und Betreffattributen.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft „description“ enthält zusätzliche Informationen über Ihre Rolle. |
| `roleType` | Der zugewiesene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihrer Organisation an, die für eine bestimmte Rolle bereitgestellt werden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Subjekt und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbeschriftungen an, die auf die abgefragte Rolle angewendet wurden. |

## Objekte nach Rollen-ID nachschlagen

Sie können auch Betreffe abrufen, indem Sie eine GET-Anfrage an den `/roles`-Endpunkt stellen und dabei eine {ROLE_ID} angeben.

**API-Format**

```http
GET /roles/{ROLE_ID}/subjects
```

| Parameter | Beschreibung |
| --- | --- |
| {ROLE_ID} | Die ID der Rolle, die den Betreffen zugeordnet ist, die Sie nachschlagen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden Subjekte abgerufen, die mit `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809` verknüpft sind.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die mit der abgefragten Rollen-ID verknüpften Subjekte zurückgegeben, einschließlich der entsprechenden Subjekt-ID und des Subjekttyps.

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `roleId` | Die mit dem abgefragten Betreff verknüpfte Rollenkennung. |
| `subjectType` | Der Typ des abgefragten Betreffs. |
| `subjectId` | Die ID, die dem abgefragten Betreff entspricht. |

## Erstellen einer Rolle {#create}

Um eine neue Rolle zu erstellen, stellen Sie eine POST-Anfrage an den `/roles`-Endpunkt und geben Sie dabei Werte für den Namen, die Beschreibung und den Rollentyp Ihrer Rolle an.

**API-Format**

```http
POST /roles/
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Rolle. Stellen Sie sicher, dass der Name Ihrer Rolle beschreibend ist, da Sie damit Informationen zu Ihrer Rolle nachschlagen können. |
| `description` | (Optional) Ein beschreibender Wert, den Sie einbeziehen können, um weitere Informationen zu Ihrer Rolle bereitzustellen. |
| `roleType` | Der zugewiesene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre neu erstellte Rolle mit der entsprechenden Rollen-ID sowie Informationen zum Rollentyp, zu den Berechtigungssätzen und zu den Betreffattributen zurückgegeben.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft „description“ enthält zusätzliche Informationen über Ihre Rolle. |
| `roleType` | Der zugewiesene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihrer Organisation an, die für eine bestimmte Rolle bereitgestellt werden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Subjekt und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbeschriftungen an, die auf die abgefragte Rolle angewendet wurden. |

## Aktualisieren einer Rolle {#patch}

Sie können die Eigenschaften einer Rolle aktualisieren, indem Sie eine PATCH-Anfrage an den `/roles`-Endpunkt senden und dabei die entsprechende Rollen-ID und die Werte für die Vorgänge angeben, die Sie anwenden möchten.

**API-Format**

```http
PATCH /roles/{ROLE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {ROLE_ID} | Die ID der Rolle, die Sie aktualisieren möchten. |

**Anfrage**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
      }
    ]
  }'
```

| Funktionsweise | Beschreibung |
| --- | --- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zum Aktualisieren der Rolle erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Pfad des zu aktualisierenden Parameters. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die aktualisierte Rolle zurück, einschließlich neuer Werte für die Eigenschaften, die Sie aktualisiert haben.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft „description“ enthält zusätzliche Informationen über Ihre Rolle. |
| `roleType` | Der zugewiesene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihrer Organisation an, die für eine bestimmte Rolle bereitgestellt werden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Subjekt und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbeschriftungen an, die auf die abgefragte Rolle angewendet wurden. |

## Aktualisieren einer Rolle anhand der Rollen-ID {#put}

Sie können eine Rolle aktualisieren, indem Sie eine PUT-Anfrage an den `/roles`-Endpunkt stellen und die Rollen-ID angeben, die der zu aktualisierenden Rolle entspricht.

**API-Format**

```http
PUT /roles/{ROLE_ID}
```

**Anfrage**

Die folgende Anfrage aktualisiert den Namen, die Beschreibung und den Rollentyp für die Rollen-ID: `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `name` | Der aktualisierte Name einer Rolle. |
| `description` | Die aktualisierte Beschreibung einer Rolle. |
| `roleType` | Der zugewiesene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |

**Antwort**

Bei einer erfolgreichen Antwort wird Ihre aktualisierte Rolle zurückgegeben, einschließlich neuer Werte für ihren Namen, ihre Beschreibung und ihren Rollentyp.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator role for ACME",
  "description": "New administrator role for ACME",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft „description“ enthält zusätzliche Informationen über Ihre Rolle. |
| `roleType` | Der zugewiesene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihrer Organisation an, die für eine bestimmte Rolle bereitgestellt werden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Subjekt und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbeschriftungen an, die auf die abgefragte Rolle angewendet wurden. |

## Betreff nach Funktions-ID aktualisieren

Um die mit einer Rolle verknüpften Betreffe zu aktualisieren, stellen Sie eine PATCH-Anfrage an den `/roles`-Endpunkt, wobei Sie die Rollen-ID der Betreffe angeben, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| Parameter | Beschreibung |
| --- | --- |
| {ROLE_ID} | Die ID der Rolle, die den zu aktualisierenden Betreffen zugeordnet ist. |

**Anfrage**

Die folgende Anfrage aktualisiert die mit `{ROLE_ID}` verknüpften Betreffe.

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/user",
        "value": "{USER ID}"
    }
]' 
```

| Funktionsweise | Beschreibung |
| --- | --- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zum Aktualisieren der Rolle erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Pfad des zu aktualisierenden Parameters. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt Ihre aktualisierte Rolle zurück, einschließlich neuer Werte für die Subjekte.

```json
{
  "subjects": [
    [
      {
        "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID",
        "subjectType": "user"
      }
    ]
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
      "templated": true
    }
  }
}
```

## Löschen einer Rolle {#delete}

Um eine Rolle zu löschen, stellen Sie eine DELETE-Anfrage an den `/roles`-Endpunkt und geben Sie dabei die ID der Rolle an, die Sie löschen möchten.

**API-Format**

```http
DELETE /roles/{ROLE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {ROLE_ID} | Die ID der Rolle, die Sie löschen möchten. |

**Anfrage**

Die folgende Anfrage löscht die Rolle mit der ID `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an die Rolle stellen. Sie erhalten den HTTP-Status 404 (Nicht gefunden), da die Rolle aus der Administration entfernt wurde.

## API-Anmeldedaten hinzufügen {#apicredential}

Um API-Anmeldeinformationen hinzuzufügen, stellen Sie eine PATCH-Anfrage an `/roles` Endpunkt und geben Sie dabei die Rollen-ID der Subjekte an.

**API-Format**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/api-integration",
        "value": "{TECHNICAL ACCOUNT ID}"
    }
]'   
```

| Funktionsweise | Beschreibung |
| --- | --- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zum Aktualisieren der Rolle erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Pfad des hinzuzufügenden Parameters. |
| `value` | Der Wert, dem Sie Ihren Parameter hinzufügen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.
