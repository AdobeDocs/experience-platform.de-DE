---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerungs-Berechtigungen;Zugriffssteuerungs-Ressourcentypen;Zugriffssteuerungs-API
solution: Experience Platform
title: Referenz-API-Endpunkt
description: Mit dem Referenz-Endpunkt in der Zugriffssteuerungs-API können Sie die Namen der verfügbaren Berechtigungen und Ressourcentypen anzeigen, die dann verwendet werden können, um effektive Zugriffssteuerungsrichtlinien für den aktuellen Benutzer anzuzeigen.
role: Developer
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 59%

---

# Referenz-Endpunkt

>[!NOTE]
>
>Wenn ein Benutzer-Token übergeben wird, muss der Benutzer des Tokens über eine „org admin“-Rolle für die angeforderte Organisation verfügen.

Sie können die Namen aller Berechtigungen und Ressourcentypen auflisten, indem Sie eine GET-Anfrage an den `/acl/reference`-Endpunkt stellen. Diese Namen können dann in API-Aufrufen verwendet werden, um [effektive Zugriffssteuerungsrichtlinien anzuzeigen](./effective-policies.md) für den aktuellen Benutzer.

Eine Berechtigung ist eine Richtlinie, die über die Adobe Admin Console verwaltet wird und keiner bzw. mehr Richtlinien vom Typ Ressource zugeordnet ist. Ein Ressourcentyp ist eine Richtlinie, die Lese-, Schreib- und/oder Löschfunktionen für einen bestimmten Typ von [!DNL Experience Platform]-Ressourcen (z. B. Datensätze oder Schemata) ermöglicht.

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
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
