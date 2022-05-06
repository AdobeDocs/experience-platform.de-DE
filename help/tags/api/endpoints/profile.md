---
title: Profil-Endpunkt
description: Erfahren Sie, wie Sie den /profiles-Endpunkt in der Reactor-API aufrufen.
exl-id: d0434098-f49a-45f3-9772-488bd3c134aa
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 100%

---

# Profil-Endpunkt

In der Reactor-API stellt ein Profil einen Adobe Experience Platform-Benutzer dar. Die Reactor-API unterhält keine eigene Benutzer- und Berechtigungsdatenbank und verlässt sich stattdessen auf Adobe IDs, die vom [Identity Management System (IMS) von Adobe](https://helpx.adobe.com/de/enterprise/using/identity.html) verwaltet werden.

Ein Profil enthält alle Informationen zum angemeldeten Benutzer, einschließlich aller IMS-Organisationen, zu denen er gehört, der Produktprofile, zu denen er in jeder Organisation gehört, und der Rechte, die ihm aus jedem Produktprofil zugewiesen sind.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Abrufen des aktuellen Profils {#lookup}

Sie können die Details des aktuell angemeldeten Profils abrufen, indem Sie eine GET-Anfrage an den `/profile`-Endpunkt stellen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
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
