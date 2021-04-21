---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffskontrolle-Berechtigungen;Zugriffskontrolle-Ressourcentypen;Zugriffskontrolle-API
solution: Experience Platform
title: Referenz-API-Endpunkt
topic-legacy: developer guide
description: Mit der Zugriffskontrolle in Adobe Experience Platform können Sie Rollen und Berechtigungen für verschiedene Plattformfunktionen mithilfe des Adobe Admin Console verwalten. Sie können die Namen aller Berechtigungen und Ressourcentypen Liste haben, indem Sie eine GET an den Endpunkt /acl/reference in der Zugriffskontrolle-API anfordern. Diese Namen können dann in API-Aufrufen verwendet werden, um effektive Richtlinien für den aktuellen Anwender anzuzeigen.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 51%

---

# Referenz-Endpunkt

Sie können die Namen aller Berechtigungen und Ressourcentypen auflisten, indem Sie eine GET-Anfrage an den `/acl/reference`-Endpunkt stellen. Diese Namen können dann in API-Aufrufen verwendet werden, um [effektive Richtlinien](./effective-policies.md) für den aktuellen Anwender anzuzeigen.

Eine Berechtigung ist eine Richtlinie, die über die Adobe Admin Console verwaltet wird und keiner bzw. mehr Richtlinien vom Typ Ressource zugeordnet ist. Ein Ressourcentyp ist eine Richtlinie, die Lese-, Schreib- und/oder Löschfunktionen für einen bestimmten Typ von [!DNL Platform]-Ressource (z. B. DataSets oder Schema) aktiviert.

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
