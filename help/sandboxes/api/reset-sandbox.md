---
keywords: Experience Platform;Home;beliebte Themen;Sandbox zurücksetzen
solution: Experience Platform
title: Sandbox in der API zurücksetzen
topic: Entwicklerhandbuch
description: Sandboxes, die der Entwicklung dienen, verfügen über eine Funktion zum „Zurücksetzen auf Werkseinstellungen“, mit der alle nicht standardmäßigen Ressourcen aus einer Sandbox gelöscht werden. Sie können eine Sandbox zurücksetzen, indem Sie eine PUT anfordern, die den Namen der Sandbox im Anforderungspfad enthält.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 77%

---


# Zurücksetzen einer Sandbox in der API

Sandboxes, die der Entwicklung dienen, verfügen über eine Funktion zum „Zurücksetzen auf Werkseinstellungen“, mit der alle nicht standardmäßigen Ressourcen aus einer Sandbox gelöscht werden. Sie können eine Sandbox zurücksetzen, indem Sie eine PUT-Anfrage stellen, die im Anfragepfad den Namen (`name`) der Sandbox enthält.

**API-Format**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name`-Eigenschaft der Sandbox, die Sie zurücksetzen möchten. |

**Anfrage**

Durch folgende Anfrage wird eine Sandbox mit dem Namen „dev-2“ zurückgesetzt.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `action` | Dieser Parameter muss in der Anfrage-Payload mit dem Wert „reset“ angegeben werden, damit die Sandbox zurückgesetzt wird. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Sandbox zurück und zeigt an, dass ihr Status (`state`) „wird zurückgesetzt“ lautet.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
> Nach dem Zurücksetzen einer Sandbox dauert es etwa 15 Minuten, bis sie vom System bereitgestellt wird. Nach dem Bereitstellen ändert sich der Status (`state`) der Sandbox in „aktiv“ oder „fehlgeschlagen“.