---
keywords: Experience Platform; Startseite; beliebte Themen; API; Attributbasierte Zugriffssteuerung; attributbasierte Zugriffssteuerung
solution: Experience Platform
title: Produkt-API-Endpunkt
description: Mit dem Endpunkt /products in der API für die attributbasierte Zugriffssteuerung können Sie Produkte in Adobe Experience Platform programmgesteuert verwalten.
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 12%

---

# Endpunkt &quot;Produkte&quot;

>[!IMPORTANT]
>
>Die attribut-basierte Zugriffskontrolle ist derzeit in einer eingeschränkten Version für US-Kunden im Gesundheitswesen verfügbar. Diese Funktion steht allen Real-time Customer Data Platform-Kunden nach der vollständigen Veröffentlichung zur Verfügung.

Die `/products` -Endpunkt in der attributbasierten Zugriffssteuerungs-API können Sie Produkte sowie Berechtigungskategorien und Berechtigungssätze, die mit Produkten in Ihrer Organisation verknüpft sind, programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der API für die attributbasierte Zugriffskontrolle. Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Liste der berechtigten Produkte abrufen {#list}

Sie können eine Liste der berechtigten Produkte abrufen, indem Sie eine GET-Anfrage an die `/products` -Endpunkt.

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

Sie können Berechtigungskategorien für ein bestimmtes Produkt nachschlagen, indem Sie eine GET-Anfrage an die `/products/{PRODUCT_ID}/categories` -Endpunkt bei der Angabe Ihrer Produkt-ID.

**API-Format**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parameter | Beschreibung |
| --- | --- |
| {PRODUCT_ID} | Die Kennung des Produkts, das den Berechtigungskategorien zugeordnet ist, die Sie nachschlagen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden Berechtigungskategorien abgerufen, die mit `{PRODUCT_ID}`.

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

Sie können Berechtigungssätze für ein bestimmtes Produkt nachschlagen, indem Sie eine GET-Anfrage an die `/products/{PRODUCT_ID}/permission-sets` -Endpunkt bei der Angabe Ihrer Produkt-ID.

**API-Format**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parameter | Beschreibung |
| --- | --- |
| {PRODUCT_ID} | Die Kennung des Produkts, das mit den Berechtigungssätzen verknüpft ist, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anfrage ruft Berechtigungssätze ab, die mit `{PRODUCT_ID}`.

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
| `permission-sets` | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Administrator auf eine Rolle anwenden kann. Ein Administrator kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| `id` | Die entsprechende ID des abgefragten Berechtigungssatzes. |
| `name` | Der entsprechende Name des abgefragten Berechtigungssatzes. |
| `category` | Die verfügbare Berechtigungskategorie. |
| `permissions` | Zu den Berechtigungen gehört die Möglichkeit, Platform-Funktionen anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen. |
| `permissions.resource` | Das Asset oder Objekt, auf das ein Betreff zugreifen kann oder nicht. Ressourcen können Dateien, Anwendungen, Server oder sogar APIs sein. |
| `permissions.actions` | Die Aktion, die ein Betreff gegen eine abgefragte Ressource ausführen darf. Mögliche Werte sind: `view`, `read`, `create`, `edit`und `delete` |
