---
keywords: Experience Platform;Startseite;beliebte Themen;Sandboxes auflisten
solution: Experience Platform
title: Sandbox-Typen-API-Endpunkt
description: Sie können eine Liste der unterstützten Sandbox-Typen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den Endpunkt /sandboxTypes stellen.
role: Developer
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 73%

---

# Endpunkt für Sandbox-Typen

Sie können eine Liste der unterstützten Sandbox-Typen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/sandboxTypes` senden.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste unterstützter Sandbox-Typen

Sie können eine Liste der unterstützten Sandbox-Typen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/sandboxTypes` senden.

**API-Format**

```http
GET /sandboxTypes
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Sandbox-Typen zurück, die für Ihr Unternehmen unterstützt werden.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
