---
keywords: Experience Platform;Startseite;beliebte Themen;Namespace;Namespace;Namespaces;Namespaces;Identitäts-Namespace;Identitäts-Namespace;Identität;Identität
solution: Experience Platform
title: Erstellen eines benutzerdefinierten Namespace in der Identity Service-API
topic-legacy: API guide
description: Mithilfe der Identity-Namespace-API können Sie einen benutzerdefinierten Identitäts-Namespace erstellen, der nur für Ihr Unternehmen verfügbar ist.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Erstellen eines benutzerdefinierten Namespace in der Identity Service-API

Mit der API [!DNL Identity Namespace] können Sie einen benutzerdefinierten Identitäts-Namespace erstellen, der nur für Ihr Unternehmen verfügbar ist.

Empfehlungen zum Erstellen benutzerdefinierter Namespaces finden Sie in der [FAQ-Dokumentation zum Identity Service](../troubleshooting-guide.md).

>[!NOTE]
>
>Namespaces sind ein Qualifizierer für Identitäten. Daher kann ein Namespace nach seiner Erstellung nicht mehr gelöscht werden.

**API-Format**

```http
POST /idnamespace/identities
```

**Anfrage**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**Antwort**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## Nächste Schritte

Fahren Sie mit dem nächsten Tutorial zu [Auflisten der nativen ID einer Identität](./list-native-id.md) fort.
