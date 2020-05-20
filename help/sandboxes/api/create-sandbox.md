---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sandbox erstellen
topic: developer guide
translation-type: tm+mt
source-git-commit: ef423a8c1b412315d03cddf7d8c351a232eb509b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 2%

---


# Sandbox erstellen

Sie können eine neue Sandbox erstellen, indem Sie eine POST-Anforderung an den `/sandboxes` Endpunkt senden.

**API-Format**

```http
POST /sandboxes
```

**Anfrage**

Die folgende Anforderung erstellt eine neue Entwicklungs-Sandbox mit dem Namen &quot;dev-3&quot;.

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
| `name` | Der Bezeichner, der für den Zugriff auf die Sandbox in zukünftigen Anforderungen verwendet wird. Dieser Wert muss eindeutig sein, und die beste Methode besteht darin, ihn so beschreibend wie möglich zu machen. Darf keine Leerzeichen oder Großbuchstaben enthalten. |
| `title` | Ein für Menschen lesbarer Name, der für Anzeigezwecke in der Benutzeroberfläche der Plattform verwendet wird. |
| `type` | Der Typ der zu erstellenden Sandbox. Derzeit können nur Sandboxen vom Typ &quot;Entwicklung&quot;von einem Unternehmen erstellt werden. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Sandbox zurück und zeigt an, dass sie &quot;erstellt&quot; `state` ist.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE] Die Bereitstellung von Sandboxen durch das System dauert etwa 15 Minuten, danach `state` werden sie &quot;aktiv&quot;oder &quot;fehlgeschlagen&quot;.
