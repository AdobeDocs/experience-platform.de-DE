---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Marketing-Aktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 5%

---


# Endpunkt der Marketing-Aktionen

A marketing action, in the context of the Adobe Experience Platform [!DNL Data Governance], is an action that an [!DNL Experience Platform] data consumer takes, for which there is a need to check for violations of data usage policies.

Sie können Marketingaktionen für Ihr Unternehmen mithilfe des `/marketingActions` Endpunkts in der Policy Service-API verwalten.

## Erste Schritte

The API endpoints used in this guide are part of the [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](./getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer beliebigen [!DNL Experience Platform] API erforderlich sind.

## Eine Liste von Marketingaktionen abrufen {#list}

Sie können eine Liste von Kern- oder benutzerspezifischen Marketingaktionen abrufen, indem Sie eine GET-Anforderung an `/marketingActions/core` bzw. `/marketingActions/custom`an diese senden.

**API-Format**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Anfrage**

The following request retrieves a list of custom marketing actions maintained by your organization.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details zu jeder abgerufenen Marketingaktion zurück, einschließlich ihrer `name` und `href`. The `href` value is used to identify the marketing action when [creating a data usage policy](policies.md#create-policy).

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `_page.count` | The total number of marketing actions returned. |
| `children` | Ein Array von Objekten, die die Details der abgerufenen Marketingaktionen enthalten. |
| `name` | The name of the marketing action, which acts as its unique identifier when [looking up a specific marketing action](#lookup). |
| `_links.self.href` | Eine URI-Referenz für die Marketingaktion, die zum Abschließen des `marketingActionsRefs` Arrays beim [Erstellen einer Datenverwendungsrichtlinie](policies.md#create-policy)verwendet werden kann. |

## Suchen Sie nach einer bestimmten Marketingaktion {#lookup}

Sie können die Details einer bestimmten Marketingaktion nachschlagen, indem Sie die `name` Eigenschaft der Marketingaktion in den Pfad einer GET-Anforderung aufnehmen.

**API-Format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | The `name` property of the marketing action you want to look up. |

**Anfrage**

The following request retrieves a custom marketing action named `combineData`.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Antwortobjekt enthält die Details zur Marketingaktion, einschließlich des Pfads (`_links.self.href`), der zum Verweisen auf die Marketingaktion beim [Definieren einer Datenverwendungsrichtlinie](policies.md#create-policy) (`marketingActionsRefs`) erforderlich ist.

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## Erstellen oder Aktualisieren einer benutzerdefinierten Marketingaktion {#create-update}

Sie können eine neue benutzerspezifische Marketingaktion erstellen oder eine vorhandene aktualisieren, indem Sie den vorhandenen oder beabsichtigten Namen der Marketingaktion in den Pfad einer PUT-Anforderung aufnehmen.

**API-Format**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | The name of the marketing action to be created or updated. Wenn im System bereits eine Marketingaktion mit dem angegebenen Namen vorhanden ist, wird diese Marketingaktion aktualisiert. Wenn keine Marketingaktion vorhanden ist, wird eine neue Marketingaktion für den angegebenen Namen erstellt. |

**Anfrage**

Die folgende Anforderung erstellt eine neue Marketingaktion mit dem Namen `crossSiteTargeting`, sofern im System noch keine Marketingaktion mit demselben Namen vorhanden ist. Wenn eine `crossSiteTargeting` Marketingaktion vorhanden ist, wird diese Marketingaktion stattdessen anhand der in der Nutzlast bereitgestellten Eigenschaften aktualisiert.

```sh
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | The name of the marketing action to be created or updated. <br><br>**WICHTIG **: Diese Eigenschaft muss mit dem`{MARKETING_ACTION_NAME}`im Pfad übereinstimmen, andernfalls tritt ein HTTP-400-Fehler (Fehlerhafte Anforderung) auf. Mit anderen Worten, sobald eine Marketingaktion erstellt wurde, kann ihre`name`Eigenschaft nicht mehr geändert werden. |
| `description` | Eine optionale Beschreibung, um weitere Kontexte für die Marketingaktion anzugeben. |

**Antwort**

A successful response returns the details of the marketing action. Wenn eine vorhandene Marketingaktion aktualisiert wurde, gibt die Antwort den HTTP-Status 200 (OK) zurück. Wenn eine neue Marketingaktion erstellt wurde, gibt die Antwort den HTTP-Status 201 (Erstellt) zurück.

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## Löschen einer benutzerdefinierten Marketingaktion {#delete}

Sie können eine benutzerspezifische Marketingaktion löschen, indem Sie deren Namen in den Pfad einer DELETE-Anforderung eintragen.

>[!NOTE]
>
>Marketingaktionen, die von bestehenden Richtlinien referenziert werden, können nicht gelöscht werden. Der Versuch, eine dieser Marketingaktionen zu löschen, führt zu einem HTTP-400-Fehler (Ungültige Anforderung) zusammen mit einer Meldung, die die IDs aller Richtlinien enthält, die auf die Marketingaktion verweisen.

**API-Format**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | The name of the marketing action you want to delete. |

**Anfrage**

```sh
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) mit einem leeren Antworttext zurück.

Sie können den Löschvorgang bestätigen, indem Sie versuchen, die Marketingaktion [nachzuschlagen](#look-up). Sie sollten einen HTTP 404-Fehler (nicht gefunden) erhalten, wenn die Marketingaktion aus dem System entfernt wurde.
