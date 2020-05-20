---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Berechtigungsnamen und Ressourcentypen der Liste
topic: developer guide
translation-type: tm+mt
source-git-commit: 7b354a96d70332cf7a7e9eff322cd3d6ee0fc96a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---


# Berechtigungsnamen und Ressourcentypen der Liste

Sie können die Namen aller Berechtigungen und Ressourcentypen Liste haben, indem Sie eine GET-Anforderung an den `/acl/reference` Endpunkt senden. Diese Namen können dann in API-Aufrufen verwendet werden, um effektive Richtlinien [für den aktuellen Benutzer](./effective-policies.md) Ansicht.

Eine **Berechtigung** ist eine Richtlinie, die über die Adobe Admin-Konsole verwaltet wird und einer Null- oder einer Ressourcenart-Richtlinie zugeordnet wird. Ein **Ressourcentyp** ist eine Richtlinie, die Lese-, Schreib- und/oder Löschfunktionen für einen bestimmten Plattformressourcentyp (z. B. Datensätze oder Schema) ermöglicht.

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

Eine erfolgreiche Antwort gibt ein `permissions` Objekt und ein `resource-types` Objekt zurück, die jeweils eine vollständige Liste der Namen für Zugriffsberechtigungen bzw. Ressourcentypen enthalten.

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
