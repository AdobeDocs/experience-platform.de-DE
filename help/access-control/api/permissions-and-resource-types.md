---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Berechtigungsnamen und Ressourcentypen auflisten
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 79%

---


# Berechtigungsnamen und Ressourcentypen auflisten

Sie können die Namen aller Berechtigungen und Ressourcentypen auflisten, indem Sie eine GET-Anfrage an den `/acl/reference`-Endpunkt stellen. Diese Namen können dann in API-Aufrufen verwendet werden, um [effektive Richtlinien](./effective-policies.md) für den aktuellen Anwender anzuzeigen.

Eine **Berechtigung** ist eine Richtlinie, die über die Adobe Admin Console verwaltet wird und keiner bzw. mehr Richtlinien vom Typ Ressource zugeordnet ist. A **resource type** is a policy that enables read, write, and/or delete capabilities for a specific type of [!DNL Platform] resource (such as datasets or schemas).

**API-Format**

```http
GET /acl/reference
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein `permissions`-Objekt und ein `resource-types`-Objekt zurück, die jeweils eine vollständige Liste der Namen für Zugriffsberechtigungen bzw. Ressourcentypen enthalten.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
