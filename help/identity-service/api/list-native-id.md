---
keywords: Experience Platform;home;popular topics;identity xid;XID
solution: Experience Platform
title: Native Kennung für eine Identität abrufen
topic: API guide
description: Identitätsdaten werden in der Regel als ID-Zeichenfolgenwert und Identitäts-Namespace in erfassten XDM-Daten und bei der Bereitstellung einer Identität zur Verwendung in einem API-Aufruf bereitgestellt. Wenn Identitäten im Identity Service persistiert werden, wird eine Kennung generiert und der jeweiligen Identität zugewiesen. Diese Kennung wird als native XID bezeichnet. Platform-APIs, die Identitätsdaten erfordern, unterstützen die Nutzung dieser kompakteren Form für aggregierte Kennung und Namespace. XID ist eine Base64-kodierte Zeichenfolge.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 74%

---


# XID für eine Identität abrufen

Identitätsdaten werden in der Regel als ID-Zeichenfolgenwert und Identitäts-Namespace in erfassten XDM-Daten und bei der Bereitstellung einer Identität zur Verwendung in einem API-Aufruf bereitgestellt. When identities are persisted in [!DNL Identity Service], an ID is generated and assigned to that identity, called the native XID. [!DNL Platform] APIs, für die Identitätsdaten unterstützt werden müssen, verwenden dieses kompaktere Formular für die aggregierte ID und den Namensraum. XID ist eine Base64-kodierte Zeichenfolge.

>[!NOTE]
>
> Dieses Format ist vor allem für den internen Adobe-Gebrauch vorgesehen. Native XID as a singular value is more space efficient and is what is used internally within [!DNL Platform] solutions for storage and serialization. Sie ist jedoch nicht für Menschen lesbar, ist opak und erfordert einen separaten Aufruf, um sie zur Verwendung abzurufen.

Verschaffen Sie sich die XID für einen angegebenen ID-Wert und Namespace mithilfe des in diesem Abschnitt beschriebenen Diensts.

**API-Format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**Anfrage**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
