---
keywords: Experience Platform;Home;beliebte Themen;Sandbox;Sandbox
solution: Experience Platform
title: Sandbox in der API erstellen
topic: Entwicklerhandbuch
description: Sie können eine neue Sandbox erstellen, indem Sie eine POST an den Endpunkt "/sandboxes"anfordern.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 49%

---


# Erstellen einer Sandbox in der API

Sie können eine Entwicklungs- oder Produktions-Sandbox erstellen, indem Sie eine POST an den Endpunkt `/sandboxes` anfordern.

## Erstellen einer Entwicklungs-Sandbox

Um eine Entwicklungs-Sandbox zu erstellen, fordern Sie eine POST an den Endpunkt `/sandboxes` an und geben Sie den Wert `development` für die Eigenschaft `type` an.

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
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Die Kennung, die in zukünftigen Anfragen für den Zugriff auf die Sandbox verwendet wird. Dieser Wert muss eindeutig sein; Best Practice ist, ihn so beschreibend wie möglich zu gestalten. Dieser Wert darf keine Leerzeichen oder Sonderzeichen enthalten. |
| `title` | Ein für Menschen lesbarer Name, der für Anzeigezwecke in der Platform-Benutzeroberfläche verwendet wird. |
| `type` | Der Typ der zu erstellenden Sandbox. Der Wert für die `type`-Eigenschaft kann entweder Entwicklung oder Produktion sein. |

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

## Erstellen einer Produktions-Sandbox

>[!NOTE]
>
>Die Funktion &quot;Mehrere Produktions-Sandboxen&quot;befindet sich in der Betaphase.

Um eine Produktions-Sandbox zu erstellen, stellen Sie eine POST an den Endpunkt `/sandboxes` und geben Sie den Wert `production` für die Eigenschaft `type` an.

**API-Format**

```http
POST /sandboxes
```

**Anfrage**

Die folgende Anforderung erstellt eine neue Produktions-Sandbox mit dem Namen &quot;test-prod-sandbox&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Die Kennung, die in zukünftigen Anfragen für den Zugriff auf die Sandbox verwendet wird. Dieser Wert muss eindeutig sein; Best Practice ist, ihn so beschreibend wie möglich zu gestalten. Dieser Wert darf keine Leerzeichen oder Sonderzeichen enthalten. |
| `title` | Ein für Menschen lesbarer Name, der für Anzeigezwecke in der Platform-Benutzeroberfläche verwendet wird. |
| `type` | Der Typ der zu erstellenden Sandbox. Der Wert für die `type`-Eigenschaft kann entweder Entwicklung oder Produktion sein. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Sandbox zurück und zeigt an, dass ihr `state` „wird erstellt“ lautet.

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
