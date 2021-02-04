---
keywords: Experience Platform;Home;beliebte Themen;Sandbox;Sandbox
solution: Experience Platform
title: Sandbox erstellen
topic: developer guide
description: Sie können eine neue Sandbox erstellen, indem Sie eine POST an den Endpunkt "/sandboxes"anfordern.
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 86%

---


# Sandbox erstellen

Sie können eine neue Sandbox erstellen, indem Sie eine POST-Anfrage an den `/sandboxes`-Endpunkt senden.

**API-Format**

```http
POST /sandboxes
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Entwicklungs-Sandbox mit dem Namen „dev-3“.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Die Kennung, die in zukünftigen Anfragen für den Zugriff auf die Sandbox verwendet wird. Dieser Wert muss eindeutig sein; Best Practice ist, ihn so beschreibend wie möglich zu gestalten. Darf keine Leerzeichen oder Großbuchstaben enthalten. |
| `title` | Ein für Menschen lesbarer Name, der für Anzeigezwecke in der Platform-Benutzeroberfläche verwendet wird. |
| `type` | Der Typ der zu erstellenden Sandbox. Derzeit können von einer Organisation nur Sandboxes vom Typ „Entwicklung“ erstellt werden. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Sandbox zurück und zeigt an, dass ihr `state` „wird erstellt“ lautet.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
> Die Bereitstellung von Sandboxes durch das System dauert etwa 15 Minuten, danach lautet ihr `state` „aktiv“ oder „fehlgeschlagen“.
