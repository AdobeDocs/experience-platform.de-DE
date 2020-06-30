---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abrufen der nativen ID für eine Identität
topic: API guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---


# XID für eine Identität abrufen

Identitätsdaten werden in der Regel als ID-Zeichenfolgenwert und Identitäts-Namensraum in erfassten XDM-Daten und bei der Bereitstellung einer Identität für die Verwendung in einem API-Aufruf bereitgestellt. Wenn Identitäten beibehalten werden, [!DNL Identity Service]wird eine ID generiert und dieser Identität zugewiesen, die als native XID bezeichnet wird. [!DNL Platform] APIs, für die Identitätsdaten unterstützt werden müssen, verwenden dieses kompaktere Formular für die aggregierte ID und den Namensraum. XID ist eine Base64-kodierte Zeichenfolge.

>[!NOTE] Dieses Format ist vor allem für den internen Adobe-Gebrauch vorgesehen. Native XID als Singular-Wert ist platzsparender und wird intern in [!DNL Platform] Lösungen zur Datenspeicherung und Serialisierung verwendet. Es ist jedoch nicht für Menschen lesbar, es ist undurchsichtig und erfordert einen separaten Aufruf, um es zu verwenden.

Erwerben Sie die XID für einen angegebenen ID-Wert und einen Namensraum mithilfe des in diesem Abschnitt beschriebenen Dienstes.

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
