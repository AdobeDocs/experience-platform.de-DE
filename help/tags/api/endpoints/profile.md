---
title: Endpunkt "Profile"
description: Erfahren Sie, wie Sie den Endpunkt /profiles in der Reactor-API aufrufen.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 6%

---

# Profil-Endpunkt

In der Reactor-API stellt ein Profil einen Adobe Experience Platform-Benutzer dar. Die Reactor-API unterhält keine eigene Benutzer- und Berechtigungsdatenbank und verlässt sich stattdessen auf Adobe-IDs, die vom Identitätsverwaltungssystem (IMS)](https://helpx.adobe.com/de/enterprise/using/identity.html) der Adobe verwaltet werden.[

Ein Profil enthält alle Informationen zum angemeldeten Benutzer, einschließlich aller IMS-Organisationen, zu denen er gehört, der Produktprofile, zu denen er in jeder Organisation gehört, und der Rechte, die ihm aus jedem Produktprofil zugewiesen sind.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md) , um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Aktuelles Profil abrufen {#lookup}

Sie können die Details des aktuell angemeldeten Profils abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/profile` stellen.

**API-Format**

```http
GET /profile
```

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Profils zurück.

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{IMS_ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{IMS_ORG_1}": {
          "name": "Example IMS Org A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{IMS_ORG_2}": {
          "name": "Example IMS Org B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```

