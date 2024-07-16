---
keywords: Experience Platform;home;popular topics;api;Attribute-Based Access Control;attribute-based access control
solution: Experience Platform
title: Produkt-API-Endpunkt
description: Mit dem Endpunkt /products in der API für die attributbasierte Zugriffssteuerung können Sie Produkte in Adobe Experience Platform programmgesteuert verwalten.
role: Developer
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 25%

---

# Endpunkt &quot;Produkte&quot;

>[!NOTE]
>
>Wenn ein Benutzer-Token übergeben wird, muss der Benutzer des Tokens über die Rolle &quot;org admin&quot;für die angeforderte Organisation verfügen.

Mit dem Endpunkt `/products` in der attributbasierten Zugriffssteuerungs-API können Sie Produkte sowie Berechtigungskategorien und Berechtigungssätze, die mit Produkten in Ihrer Organisation verknüpft sind, programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der API für die attributbasierte Zugriffskontrolle. Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Liste der berechtigten Produkte abrufen {#list}

Sie können eine Liste berechtigter Produkte abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/products` senden.

**API-Format**

```http
GET /products/
```

**Anfrage**

Mit der folgenden Anfrage wird eine Liste der berechtigten Produkte Ihrer Organisation abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste der berechtigten Produkte zurück, die zu Ihrem Unternehmen gehören.

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die entsprechende ID des abgefragten Produkts. |
| `name` | Der Name des abgefragten Produkts. |
| `serviceCode` | Der entsprechende Service-Code des abgefragten Produkts. |

## Suchen nach Berechtigungskategorien nach Produkt-ID

Sie können nach Berechtigungskategorien für ein bestimmtes Produkt suchen, indem Sie eine GET-Anfrage an den Endpunkt `/products/{PRODUCT_ID}/categories` richten und dabei Ihre Produkt-ID angeben.

**API-Format**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parameter | Beschreibung |
| --- | --- |
| {PRODUCT_ID} | Die Kennung des Produkts, das den Berechtigungskategorien zugeordnet ist, die Sie nachschlagen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden die mit `{PRODUCT_ID}` verknüpften Berechtigungskategorien abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Berechtigungskategorien zurückgegeben, die mit der von Ihnen abgefragten Produkt-ID verknüpft sind.

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `category` | Die Berechtigungskategorien, die innerhalb der abgefragten Produkt-ID verfügbar sind. |
| `name` | Der Name der Berechtigungskategorie. |

## Berechtigungssätze nach Produkt-ID nachschlagen

Sie können nach Berechtigungssätzen für ein bestimmtes Produkt suchen, indem Sie eine GET-Anfrage an den `/products/{PRODUCT_ID}/permission-sets` -Endpunkt richten und dabei Ihre Produkt-ID angeben.

**API-Format**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parameter | Beschreibung |
| --- | --- |
| {PRODUCT_ID} | Die Kennung des Produkts, das mit den Berechtigungssätzen verknüpft ist, die Sie nachschlagen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden die mit `{PRODUCT_ID}` verknüpften Berechtigungssätze abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die mit der abgefragten Produkt-ID verknüpften Berechtigungssätze zurückgegeben.

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `permission-sets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `id` | Die entsprechende ID des abgefragten Berechtigungssatzes. |
| `name` | Der entsprechende Name des abgefragten Berechtigungssatzes. |
| `category` | Die verfügbare Berechtigungskategorie. |
| `permissions` | Zu den Berechtigungen gehört die Möglichkeit, Adobe Campaign-Funktionen anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemata und die Verwaltung von Datensätzen. |
| `permissions.resource` | Das Asset oder Objekt, auf das ein Betreff zugreifen kann oder nicht. Ressourcen können Dateien, Anwendungen, Server oder sogar APIs sein. |
| `permissions.actions` | Die Aktion, die ein Betreff gegen eine abgefragte Ressource ausführen darf. Mögliche Werte sind: `view`, `read`, `create`, `edit` und `delete` |
