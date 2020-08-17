---
keywords: Experience Platform;home;popular topics;namespace;Namespace;namespaces;Namespaces;identity namespace;Identity namespace;identity;Identity
solution: Experience Platform
title: Benutzerdefinierten Namespace erstellen
topic: API guide
description: Mithilfe der Identitäts-Namensraum-API können Sie einen benutzerdefinierten Identitäts-Namensraum erstellen, der nur für Ihr Unternehmen verfügbar ist.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 10%

---


# Erstellen eines benutzerspezifischen Namensraums

Mithilfe der [!DNL Identity Namespace] API können Sie einen benutzerdefinierten Identitäts-Namensraum erstellen, der nur für Ihr Unternehmen verfügbar ist.

Empfehlungen zum Erstellen benutzerdefinierter Namensraum finden Sie in [der FAQ-Dokumentation](../troubleshooting-guide.md)zum Identitätsdienst.

>[!NOTE]
>
>Namensraum sind ein Qualifikator für Identitäten. Daher kann ein Namensraum, sobald er erstellt wurde, nicht gelöscht werden.

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

Proceed to the next tutorial to [list the native ID of an identity](./list-native-id.md)