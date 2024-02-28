---
keywords: Experience Platform;home;popular topics;namespace;Namespace;Namespaces;Namespaces;Identitäts-Namespace;Identitäts-Namespace;Identität;Identität
solution: Experience Platform
title: Erstellen eines benutzerdefinierten Namespace in der Identity Service-API
description: Mithilfe der Identity-Namespace-API können Sie einen benutzerdefinierten Identitäts-Namespace erstellen, der nur für Ihr Unternehmen verfügbar ist.
role: Developer
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Erstellen eines benutzerdefinierten Namespace in der Identity Service-API

Verwenden der [!DNL Identity Namespace] API können Sie einen benutzerdefinierten Identitäts-Namespace erstellen, der nur für Ihr Unternehmen verfügbar ist.

Empfehlungen zum Erstellen benutzerdefinierter Namespaces finden Sie unter [Dokumentation zu den häufig gestellten Fragen zu Identity Service](../troubleshooting-guide.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Fahren Sie mit dem nächsten Tutorial zu [die native ID einer Identität auflisten](./list-native-id.md)
