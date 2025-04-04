---
keywords: Experience Platform;Startseite;beliebte Themen;identity xid;XID
solution: Experience Platform
title: Abrufen der nativen ID für eine Identität
description: Identitätsdaten werden in der Regel als ID-Zeichenfolgenwert und Identitäts-Namespace in erfassten XDM-Daten und bei der Bereitstellung einer Identität zur Verwendung in einem API-Aufruf bereitgestellt. Wenn Identitäten im Identity Service persistiert werden, wird eine Kennung generiert und der jeweiligen Identität zugewiesen. Diese Kennung wird als native XID bezeichnet. Experience Platform-APIs, für die Identitätsdaten unterstützt werden müssen, verwenden dieses kompaktere Formular für die aggregierte ID und den Namespace. XID ist eine Base64-kodierte Zeichenfolge.
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 58%

---

# Native Kennung für eine Identität abrufen

Identitätsdaten werden in der Regel als ID-Zeichenfolgenwert und Identitäts-Namespace in erfassten XDM-Daten und bei der Bereitstellung einer Identität zur Verwendung in einem API-Aufruf bereitgestellt. Wenn Identitäten in [!DNL Identity Service] persistiert werden, wird eine ID generiert und dieser Identität zugewiesen, die als native XID bezeichnet wird. [!DNL Experience Platform] APIs, für die Identitätsdaten unterstützt werden müssen, verwenden dieses kompaktere Formular für die aggregierte ID und den Namespace. XID ist eine Base64-kodierte Zeichenfolge.

>[!NOTE]
>
>Dieses Format ist hauptsächlich für den internen Gebrauch von Adobe vorgesehen. Die native XID als Einzelwert ist platzsparender und wird intern in [!DNL Experience Platform]-Lösungen für die Speicherung und Serialisierung verwendet. Sie ist jedoch nicht für Menschen lesbar, ist opak und erfordert einen separaten Aufruf, um sie zur Verwendung abzurufen.

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
