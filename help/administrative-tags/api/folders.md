---
title: Ordner-Endpunkt
description: Erfahren Sie, wie Sie Ordner mit den Adobe Experience Platform-APIs erstellen, aktualisieren, verwalten und löschen.
role: Developer
exl-id: ee43d699-725d-4ffd-a71b-049eeb3b4d7c
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 5%

---

# Ordner-Endpunkt

>[!IMPORTANT]
>
>Die Endpunkt-URL für diesen Satz von Endpunkten ist `https://experience.adobe.io`.

Ordner sind eine Funktion, mit der Sie Ihre Geschäftsobjekte besser organisieren können, um die Navigation und Kategorisierung zu erleichtern.

Dieses Handbuch enthält Informationen zum besseren Verständnis von Ordnern und enthält Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der API.

## Erste Schritte

Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Anweisungen zum Lesen von Beispiel-API-Aufrufen.

## Abrufen einer Ordnerliste {#list}

Sie können eine Liste von Ordnern abrufen, die zu Ihrem Unternehmen gehören, indem Sie eine GET-Anfrage an den Endpunkt `/folder` senden und den Ordnertyp und die ID des übergeordneten Ordners angeben.

**API-Format**

```http
GET /folder/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Der Typ der Objekte, die im Ordner enthalten sind. Zu den unterstützten Werten gehören `segment` und `dataset`. |
| `{PARENT_FOLDER_ID}` | Die Kennung des übergeordneten Ordners, aus dem Sie die Ordnerliste abrufen. Um eine Liste aller übergeordneten Ordner anzuzeigen, verwenden Sie die Ordner-ID `root`. |

**Anfrage**

++ + Eine Beispielanfrage zum Auflisten aller Datensatzordner der obersten Ebene

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste aller Ordner der obersten Ebene für den Datensatz in Ihrem Unternehmen zurück.

++ + Eine Beispielantwort mit einer Liste aller Ordner der obersten Ebene für den Datensatz in Ihrem Unternehmen.

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## Neuen Ordner erstellen {#create}

Sie können einen neuen Ordner erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/folder` senden und den Ordnertyp angeben.

**API-Format**

```http
POST /folder/{FOLDER_TYPE}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Der Typ der Objekte, die im Ordner enthalten sind. Zu den unterstützten Werten gehören `segment` und `dataset`. |

**Anfrage**

++ + Eine Beispielanfrage zum Erstellen eines neuen Ordners.

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folder/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name des Ordners, den Sie erstellen möchten. |
| `parentId` | Die ID des übergeordneten Ordners. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrem neu erstellten Ordner zurück.

++ + Eine Beispielantwort mit Details zum neu erstellten Ordner.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die Kennung des neu erstellten Ordners. |
| `createdBy` | Die ID des Benutzers, der den Ordner erstellt hat. |
| `createdAt` | Der Zeitstempel der Erstellung des Ordners. |
| `modifiedBy` | Die ID des Benutzers, der den Ordner zuletzt geändert hat. |
| `modifiedAt` | Der Zeitstempel der letzten Ordneraktualisierung. |

+++

## Bestimmten Ordner abrufen {#get}

Sie können einen bestimmten Ordner abrufen, der zu Ihrem Unternehmen gehört, indem Sie eine GET-Anfrage an den Endpunkt `/folder` senden und den Ordnertyp und die Kennung des Ordners angeben.

**API-Format**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Der Typ der Objekte, die im Ordner enthalten sind. Zu den unterstützten Werten gehören `segment` und `dataset`. |
| `{FOLDER_ID}` | Die Kennung des Ordners, den Sie abrufen. |

**Anfrage**

++ + Eine Beispielanfrage zum Abrufen eines bestimmten Ordners

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zum angeforderten Ordner zurück.

++ + Eine Beispielantwort mit Details zum angeforderten Ordner.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die Kennung des angeforderten Ordners. |
| `name` | Der Name des angeforderten Ordners. |
| `parentId` | Die ID des übergeordneten Ordners. |
| `createdBy` | Die ID des Benutzers, der den Ordner erstellt hat. |
| `createdAt` | Der Zeitstempel der Erstellung des Ordners. |
| `modifiedBy` | Die ID des Benutzers, der den Ordner zuletzt aktualisiert hat. |
| `modifiedAt` | Der Zeitstempel der letzten Ordneraktualisierung. |
| `status` | Der Status des angeforderten Ordners. Zu den unterstützten Werten gehören `IN_USE` und `ARCHIVED`. |

+++

## Validieren eines angegebenen Ordners {#validate}

Sie können überprüfen, ob ein Ordner Objekte enthalten darf, indem Sie eine GET-Anfrage an den Endpunkt `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` senden und sowohl den Ordnertyp als auch die -ID angeben.

**API-Format**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Der Typ der Objekte, die im Ordner enthalten sind. Zu den unterstützten Werten gehören `segment` und `dataset`. |
| `{FOLDER_ID}` | Die Kennung des Ordners, den Sie überprüfen. |

**Anfrage**

++ + Eine Beispielanfrage zum Validieren eines bestimmten Ordners

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Ein erfolgreicher Status gibt den HTTP-Status 200 mit Details zum Ordner zurück, den Sie validieren.

++ + Eine Beispielantwort enthält Details zum validierten Ordner

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## Aktualisieren eines bestimmten Ordners {#update}

Sie können die Details eines bestimmten Ordners, der zu Ihrem Unternehmen gehört, aktualisieren, indem Sie eine PATCH-Anfrage an den Endpunkt `/folder` senden und den Ordnertyp und die Kennung des Ordners angeben.

**API-Format**

```http
PATCH /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Der Typ der Objekte, die im Ordner enthalten sind. Zu den unterstützten Werten gehören `segment` und `dataset`. |
| `{FOLDER_ID}` | Die ID des Ordners, den Sie aktualisieren. |

**Anfrage**

++ + Eine Beispielanfrage zum Aktualisieren eines bestimmten Ordners

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Informationen zu Ihrem neu aktualisierten Ordner zurück.

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## Löschen eines bestimmten Ordners {#delete}

Sie können einen bestimmten Ordner, der zu Ihrem Unternehmen gehört, löschen, indem Sie eine DELETE-Anfrage an den Ordner &quot;`/folder`&quot;senden und den Ordnertyp und die Kennung des Ordners angeben.

***API-Format**

```http
DELETE /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Der Typ der Objekte, die im Ordner enthalten sind. Zu den unterstützten Werten gehören `segment` und `dataset`. |
| `{FOLDER_ID}` | Die Kennung des Ordners, den Sie löschen. |

**Anfrage**

++ + Eine Beispielanfrage zum Löschen eines bestimmten Ordners

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einem Nachrichtentext zurück, der Sie über das Löschen des Ordners informiert.

```json
{
    "message": "delete request accepted successfully"
}
```

## Nächste Schritte

Nach Lesen dieses Handbuchs erfahren Sie jetzt, wie Sie Ordner mit der Adobe Experience Platform-API erstellen, verwalten und löschen.
