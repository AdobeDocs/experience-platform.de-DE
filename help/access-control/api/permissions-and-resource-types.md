---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerungs-Berechtigungen;Zugriffssteuerungs-Ressourcentypen;Zugriffssteuerungs-API
solution: Experience Platform
title: Referenz-API-Endpunkt
description: Über den Referenz-Endpunkt in der Access Control-API können Sie die Namen der verfügbaren Berechtigungen und Ressourcentypen anzeigen, die dann verwendet werden können, um effektive Zugriffssteuerungsrichtlinien für den aktuellen Benutzer anzuzeigen.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 59%

---

# Referenz-Endpunkt

>[!NOTE]
>
>Wenn ein Benutzer-Token übergeben wird, muss der Benutzer des Tokens über die Rolle &quot;org admin&quot;für die angeforderte Organisation verfügen.

Sie können die Namen aller Berechtigungen und Ressourcentypen auflisten, indem Sie eine GET-Anfrage an den `/acl/reference`-Endpunkt stellen. Diese Namen können dann in API-Aufrufen verwendet werden, um [Anzeigen effektiver Zugriffskontrollrichtlinien](./effective-policies.md) für den aktuellen Benutzer.

Eine Berechtigung ist eine Richtlinie, die über die Adobe Admin Console verwaltet wird und keiner bzw. mehr Richtlinien vom Typ Ressource zugeordnet ist. Ein Ressourcentyp ist eine Richtlinie, die Lese-, Schreib- und/oder Löschfunktionen für einen bestimmten Typ von [!DNL Platform]-Ressourcen (z. B. Datensätze oder Schemas) ermöglicht.

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
