---
keywords: Experience Platform; Startseite; beliebte Themen; Listen-Sandboxes
solution: Experience Platform
title: Sandbox-Typen-API-Endpunkt
topic-legacy: developer guide
description: Sie können eine Liste der unterstützten Sandbox-Typen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den Endpunkt /sandboxTypes stellen.
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 45%

---

# Sandbox-Typen-Endpunkt

Sie können eine Liste der unterstützten Sandbox-Typen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/sandboxTypes` senden.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um Links zur zugehörigen Dokumentation zu erhalten, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Liste der unterstützten Sandbox-Typen abrufen

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
