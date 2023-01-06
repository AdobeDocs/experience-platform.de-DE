---
keywords: Experience Platform; Startseite; beliebte Themen; Identitätsxid; XID
solution: Experience Platform
title: Native ID für eine Identität abrufen
description: Identitätsdaten werden in der Regel als ID-Zeichenfolgenwert und Identitäts-Namespace in erfassten XDM-Daten und bei der Bereitstellung einer Identität zur Verwendung in einem API-Aufruf bereitgestellt. Wenn Identitäten im Identity Service persistiert werden, wird eine Kennung generiert und der jeweiligen Identität zugewiesen. Diese Kennung wird als native XID bezeichnet. Platform-APIs, die Identitätsdaten erfordern, unterstützen die Nutzung dieser kompakteren Form für aggregierte Kennung und Namespace. XID ist eine Base64-kodierte Zeichenfolge.
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 69%

---

# Native Kennung für eine Identität abrufen

Identitätsdaten werden in der Regel als ID-Zeichenfolgenwert und Identitäts-Namespace in erfassten XDM-Daten und bei der Bereitstellung einer Identität zur Verwendung in einem API-Aufruf bereitgestellt. Wenn Identitäten beibehalten werden in [!DNL Identity Service], wird eine ID generiert und dieser Identität zugewiesen, die als native XID bezeichnet wird. [!DNL Platform] APIs, die Identitätsdaten erfordern, unterstützen die Verwendung dieses kompakteren Formulars für die aggregierte ID und den Namespace. XID ist eine Base64-kodierte Zeichenfolge.

>[!NOTE]
>
> Dieses Format ist vor allem für den internen Adobe-Gebrauch vorgesehen. Native XID als einzelner Wert ist platzsparender und wird intern innerhalb von verwendet [!DNL Platform] Lösungen zur Speicherung und Serialisierung. Sie ist jedoch nicht für Menschen lesbar, ist opak und erfordert einen separaten Aufruf, um sie zur Verwendung abzurufen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
