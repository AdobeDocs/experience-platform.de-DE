---
keywords: Experience Platform;home;popular topics;api;Attribute-Based Access Control;attribute-based access control
solution: Experience Platform
title: Rollen-API-Endpunkt
description: Mit dem Endpunkt /roles in der API für die attributbasierte Zugriffssteuerung können Sie Rollen in Adobe Experience Platform programmgesteuert verwalten.
role: Developer
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 27%

---

# Benutzerendpunkt

>[!NOTE]
>
>Wenn ein Benutzer-Token übergeben wird, muss der Benutzer des Tokens über die Rolle &quot;org admin&quot;für die angeforderte Organisation verfügen.

Rollen definieren den Zugriff, den ein Administrator, ein Spezialist oder ein Endbenutzer auf Ressourcen in Ihrem Unternehmen hat. In einer rollenbasierten Zugriffssteuerungsumgebung erfolgt die Bereitstellung des Benutzerzugriffs über gemeinsame Zuständigkeiten und Anforderungen. Eine Rolle verfügt über bestimmte Berechtigungen, wobei Mitglieder Ihrer Organisation je nach dem Umfang des Lese- oder Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden können.

Die `/roles` -Endpunkt in der attributbasierten API zur Zugriffskontrolle können Sie Rollen in Ihrem Unternehmen programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der API für die attributbasierte Zugriffskontrolle. Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Liste von Rollen abrufen {#list}

Sie können alle vorhandenen Rollen Ihres Unternehmens auflisten, indem Sie eine GET-Anfrage an die `/roles` -Endpunkt.

**API-Format**

```http
GET /roles/
```

**Anfrage**

Mit der folgenden Anfrage wird eine Liste der Rollen abgerufen, die zu Ihrem Unternehmen gehören.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Bei einer erfolgreichen Antwort wird eine Liste der Rollen in Ihrer Organisation zurückgegeben, einschließlich Informationen zu ihrem jeweiligen Rollentyp, Berechtigungssätzen und Themenattributen.

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
| `id` | Die Kennung, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft &quot;description&quot;enthält zusätzliche Informationen zu Ihrer Rolle. |
| `roleType` | Der vorgesehene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihres Unternehmens an, die für eine bestimmte Rolle bereitgestellt wurden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Betreff und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbezeichnungen an, die auf die abgefragte Rolle angewendet wurden. |

## Rolle nachschlagen {#lookup}

Sie können eine einzelne Rolle nachschlagen, indem Sie eine GET anfordern, die die entsprechende `roleId` im Anfragepfad.

**API-Format**

```http
GET /roles/{ROLE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {ROLE_ID} | Die ID der Rolle, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anfrage ruft Informationen für `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden Details zur abgefragten Rollen-ID zurückgegeben, einschließlich Informationen zum Rollentyp, zu Berechtigungssätzen und zu den Themenattributen.

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
| `id` | Die Kennung, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft &quot;description&quot;enthält zusätzliche Informationen zu Ihrer Rolle. |
| `roleType` | Der vorgesehene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihres Unternehmens an, die für eine bestimmte Rolle bereitgestellt wurden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Betreff und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbezeichnungen an, die auf die abgefragte Rolle angewendet wurden. |

## Suchen von Benutzern nach Rollen-ID

Sie können auch Objekte abrufen, indem Sie eine GET-Anfrage an die `/roles` Endpunkt beim Bereitstellen von {ROLE_ID}.

**API-Format**

```http
GET /roles/{ROLE_ID}/subjects
```

| Parameter | Beschreibung |
| --- | --- |
| {ROLE_ID} | Die ID der Rolle, die den Themen zugeordnet ist, die Sie nachschlagen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden die mit `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die mit der abgefragten Rollen-ID verknüpften Betreffs zurückgegeben, einschließlich der entsprechenden Betreff-ID und des Betrefftyps.

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
| `roleId` | Die mit dem abgefragten Betreff verknüpfte Rollen-ID. |
| `subjectType` | Der Typ des abgefragten Betreffs. |
| `subjectId` | Die Kennung, die dem abgefragten Betreff entspricht. |

## Erstellen einer Rolle {#create}

Um eine neue Rolle zu erstellen, stellen Sie eine POST-Anfrage an die `/roles` -Endpunkt hinzugefügt, während Werte für den Namen, die Beschreibung und den Rollentyp Ihrer Rolle angegeben werden.

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
| `description` | (Optional) Ein beschreibender Wert, den Sie angeben können, um weitere Informationen zu Ihrer Rolle bereitzustellen. |
| `roleType` | Der vorgesehene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre neu erstellte Rolle mit der zugehörigen Rollen-ID sowie Informationen zum Rollentyp, zu den Berechtigungssätzen und zu den Themenattributen zurückgegeben.

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
| `id` | Die Kennung, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft &quot;description&quot;enthält zusätzliche Informationen zu Ihrer Rolle. |
| `roleType` | Der vorgesehene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihres Unternehmens an, die für eine bestimmte Rolle bereitgestellt wurden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Betreff und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbezeichnungen an, die auf die abgefragte Rolle angewendet wurden. |

## Rolle aktualisieren {#patch}

Sie können die Eigenschaften einer Rolle aktualisieren, indem Sie eine PATCH-Anfrage an die `/roles` -Endpunkt hinzugefügt, während Sie die entsprechende Rollen-ID und Werte für die Vorgänge angeben, die Sie anwenden möchten.

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
| `op` | Der Vorgangsaufruf, mit dem die zum Aktualisieren der Rolle erforderliche Aktion definiert wird. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Pfad des zu aktualisierenden Parameters. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die aktualisierte Rolle zurück, einschließlich neuer Werte für die Eigenschaften, die Sie aktualisieren möchten.

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
| `id` | Die Kennung, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft &quot;description&quot;enthält zusätzliche Informationen zu Ihrer Rolle. |
| `roleType` | Der vorgesehene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihres Unternehmens an, die für eine bestimmte Rolle bereitgestellt wurden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Betreff und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbezeichnungen an, die auf die abgefragte Rolle angewendet wurden. |

## Aktualisieren einer Rolle nach Rollen-ID {#put}

Sie können eine Rolle aktualisieren, indem Sie eine PUT-Anfrage an die `/roles` -Endpunkt und die Rolle-ID angeben, die der Rolle entspricht, die Sie aktualisieren möchten.

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
| `roleType` | Der vorgesehene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |

**Antwort**

Bei einer erfolgreichen Antwort wird Ihre aktualisierte Rolle zurückgegeben, einschließlich neuer Werte für Name, Beschreibung und Rollentyp.

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
| `id` | Die Kennung, die der Rolle entspricht. Diese ID wird automatisch generiert. |
| `name` | Der Name Ihrer Rolle. |
| `description` | Die Eigenschaft &quot;description&quot;enthält zusätzliche Informationen zu Ihrer Rolle. |
| `roleType` | Der vorgesehene Typ der Rolle. Die möglichen Werte für den Rollentyp sind: `user-defined` und `system-defined`. |
| `permissionSets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `sandboxes` | Diese Eigenschaft zeigt die Sandboxes innerhalb Ihres Unternehmens an, die für eine bestimmte Rolle bereitgestellt wurden. |
| `subjectAttributes` | Die Attribute, die die Korrelation zwischen einem Betreff und den Platform-Ressourcen angeben, auf die sie Zugriff haben. |
| `subjectAttributes.labels` | Zeigt die Datennutzungsbezeichnungen an, die auf die abgefragte Rolle angewendet wurden. |

## Betreff nach Rollen-ID aktualisieren

Um die mit einer Rolle verknüpften Themen zu aktualisieren, stellen Sie eine PATCH-Anfrage an die `/roles` -Endpunkt und geben die Rollen-ID der Themen an, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| Parameter | Beschreibung |
| --- | --- |
| {ROLE_ID} | Die Kennung der Rolle, die den zu aktualisierenden Betreffen zugeordnet ist. |

**Anfrage**

Die folgende Anfrage aktualisiert die Betreffs, die mit `{ROLE_ID}`.

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
| `op` | Der Vorgangsaufruf, mit dem die zum Aktualisieren der Rolle erforderliche Aktion definiert wird. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Pfad des zu aktualisierenden Parameters. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort wird Ihre aktualisierte Rolle zurückgegeben, einschließlich neuer Werte für die Betreffs.

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

Um eine Rolle zu löschen, stellen Sie eine DELETE-Anfrage an die `/roles` -Endpunkt beim Angeben der ID der Rolle, die Sie löschen möchten.

**API-Format**

```http
DELETE /roles/{ROLE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {ROLE_ID} | Die ID der Rolle, die Sie löschen möchten. |

**Anfrage**

Die folgende Anfrage löscht die Rolle mit der ID von `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine Nachschlageanfrage (GET) für die Rolle ausführen. Sie erhalten den HTTP-Status 404 (Nicht gefunden), da die Rolle aus der Verwaltung entfernt wurde.

## API-Berechtigung hinzufügen {#apicredential}

Um eine API-Berechtigung hinzuzufügen, stellen Sie eine PATCH-Anfrage an `/roles` -Endpunkt und geben die Rollen-ID der Betreffs an.

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
| `op` | Der Vorgangsaufruf, mit dem die zum Aktualisieren der Rolle erforderliche Aktion definiert wird. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Pfad des hinzuzufügenden Parameters. |
| `value` | Der Wert, mit dem Sie Ihren Parameter hinzufügen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.
