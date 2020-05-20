---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Löschen von Ressourcen
topic: developer guide
translation-type: tm+mt
source-git-commit: d9ab2b1226b051be43f8fc0dd222bc075caed6f0
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 7%

---


# Löschen von Ressourcen

Es kann gelegentlich erforderlich sein, eine Ressource aus der Schema-Registrierung zu entfernen (LÖSCHEN). Es können nur die Ressourcen gelöscht werden, die Sie im Pächter-Container erstellen. Dies geschieht durch eine DELETE-Anforderung mit der Ressource, `$id` die Sie löschen möchten.

**API-Format**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_TYPE}` | Der Typ der Ressource, die aus der Schema-Bibliothek gelöscht werden soll. Gültige Typen sind `datatypes`, `mixins`, `schemas`und `classes`. |
| `{RESOURCE_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` die Ressource. |

**Anfrage**

Zum LÖSCHEN von Anforderungen sind keine Accept-Header erforderlich.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 204 (Kein Inhalt) und einen leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine GET-Anforderung (Lookup) an die Ressource senden. Sie müssen einen Accept-Header in die Anforderung einbeziehen, sollten jedoch den HTTP-Status 404 (Nicht gefunden) erhalten, da die Ressource aus der Schema-Registrierung entfernt wurde.