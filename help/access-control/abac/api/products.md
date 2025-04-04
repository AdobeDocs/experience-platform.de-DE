---
keywords: Experience Platform;Startseite;beliebte Themen;api;attributbasierte Zugriffssteuerung;attributbasierte Zugriffssteuerung
solution: Experience Platform
title: Produkt-API-Endpunkt
description: Mit dem Endpunkt /products in der attributbasierten Zugriffssteuerungs-API können Sie Produkte in Adobe Experience Platform programmgesteuert verwalten.
role: Developer
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 21%

---

# Produkt-Endpunkt

>[!NOTE]
>
>Wenn ein Benutzer-Token übergeben wird, muss der Benutzer des Tokens über eine „org admin“-Rolle für die angeforderte Organisation verfügen.

Mit dem `/products`-Endpunkt in der attributbasierten Zugriffssteuerungs-API können Sie Produkte sowie mit Produkten in Ihrer Organisation verknüpfte Berechtigungskategorien und Berechtigungssätze programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der attributbasierten Zugriffssteuerungs-API. Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste mit zulässigen Produkten {#list}

Sie können eine Liste benannter Produkte abrufen, indem Sie eine GET-Anfrage an den `/products`-Endpunkt stellen.

**API-Format**

```http
GET /products/
```

**Anfrage**

Mit der folgenden Anfrage wird eine Liste mit zulässigen Produkten Ihrer Organisation abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von berechtigten Produkten zurück, die zu Ihrer Organisation gehören.

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

## Berechtigungskategorien nach Produkt-ID nachschlagen

Sie können Berechtigungskategorien für ein bestimmtes Produkt nachschlagen, indem Sie eine GET-Anfrage an den `/products/{PRODUCT_ID}/categories`-Endpunkt stellen und dabei Ihre Produkt-ID angeben.

**API-Format**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parameter | Beschreibung |
| --- | --- |
| {PRODUCT_ID} | Die ID des Produkts, das den Berechtigungskategorien zugeordnet ist, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anfrage ruft die mit `{PRODUCT_ID}` verknüpften Berechtigungskategorien ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt die Berechtigungskategorien zurück, die mit der von Ihnen abgefragten Produkt-ID verknüpft sind.

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
| `category` | Die Berechtigungskategorien, die in der abgefragten Produkt-ID verfügbar sind. |
| `name` | Der Name der Berechtigungskategorie. |

## Berechtigungssätze nach Produkt-ID nachschlagen

Sie können Berechtigungssätze für ein bestimmtes Produkt suchen, indem Sie eine GET-Anfrage an den `/products/{PRODUCT_ID}/permission-sets`-Endpunkt stellen und dabei Ihre Produkt-ID angeben.

**API-Format**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parameter | Beschreibung |
| --- | --- |
| {PRODUCT_ID} | Die ID des Produkts, das den Berechtigungssätzen zugeordnet ist, die Sie nachschlagen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden Berechtigungssätze abgerufen, die mit `{PRODUCT_ID}` verknüpft sind.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt die Berechtigungssätze zurück, die mit der von Ihnen abgefragten Produkt-ID verknüpft sind.

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
| `permissions` | Zu den Berechtigungen gehört die Möglichkeit, Experience Platform-Funktionen anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen. |
| `permissions.resource` | Das Asset oder Objekt, auf das ein Subjekt zugreifen kann oder nicht. Bei Ressourcen kann es sich um Dateien, Anwendungen, Server oder sogar APIs handeln. |
| `permissions.actions` | Die Aktion, die ein Subjekt für eine abgefragte Ressource ausführen darf. Mögliche Werte sind: `view`, `read`, `create`, `edit` und `delete` |
