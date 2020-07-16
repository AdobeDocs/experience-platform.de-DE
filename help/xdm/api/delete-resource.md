---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ressource löschen
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 63%

---


# Ressource löschen

It may occasionally be necessary to remove (DELETE) a resource from the [!DNL Schema Registry]. Es können nur Ressourcen gelöscht werden, die Sie im Mandanten-Container erstellt haben. Dies geschieht durch Ausführung einer DELETE-Anfrage mit der `$id` der Ressource, die Sie löschen möchten.

**API-Format**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_TYPE}` | The type of resource to be deleted from the [!DNL Schema Library]. Gültige Typen sind `datatypes`, `mixins`, `schemas` und `classes`. |
| `{RESOURCE_ID}` | Der URL-codierte `$id`-URI oder `meta:altId` der Ressource. |

**Anfrage**

Für DELETE-Anfragen sind keine Accept-Kopfzeilen erforderlich.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine GET-Anfrage (Nachschlagen) an die Ressource senden. You will need to include an Accept header in the request, but should receive an HTTP status 404 (Not Found) because the resource has been removed from the [!DNL Schema Registry].