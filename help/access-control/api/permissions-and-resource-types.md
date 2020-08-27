---
keywords: Experience Platform;home;popular topics;access control permissions;access control resource types;access control api
solution: Experience Platform
title: Berechtigungsnamen und Ressourcentypen auflisten
topic: developer guide
description: Mit der Zugriffskontrolle in Adobe Experience Platform können Sie Rollen und Berechtigungen für verschiedene Plattformfunktionen mithilfe des Adobe Admin Console verwalten. Sie können die Namen aller Berechtigungen und Ressourcentypen Liste haben, indem Sie eine GET an den Endpunkt /acl/reference anfordern. Diese Namen können dann in API-Aufrufen verwendet werden, um effektive Richtlinien für den aktuellen Anwender anzuzeigen.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 62%

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
