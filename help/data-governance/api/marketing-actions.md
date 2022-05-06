---
keywords: Experience Platform;Startseite;beliebte Themen;Richtliniendurchsetzung;Marketing-Aktionen-API;API-basierte Durchsetzung;Data Governance
solution: Experience Platform
title: API-Endpunkt für Marketing-Aktionen
topic-legacy: developer guide
description: Eine Marketing-Aktion bezeichnet im Kontext des Data Governance-Frameworks eine Aktion, die ein Datennutzer von Adobe Experience Platform ergreift und bei der geprüft werden muss, ob gegen Datennutzungsrichtlinien verstoßen wurde.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 100%

---

# Endpunkt der Marketing-Aktionen

Eine Marketing-Aktion bezeichnet im Kontext der Adobe Experience Platform Data Governance eine Aktion, die ein Datennutzer von [!DNL Experience Platform] ergreift und bei der geprüft werden muss, ob gegen Datennutzungsrichtlinien verstoßen wurde.

Sie können Marketing-Aktionen für Ihr Unternehmen mithilfe des `/marketingActions`-Endpunkts in der Richtlinien-Service-API verwalten.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [[!DNL Policy Service] -API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Bevor Sie fortfahren, lesen Sie im Handbuch [Erste Schritte](./getting-started.md) die Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Abrufen einer Liste von Marketing-Aktionen {#list}

Sie können eine Liste von Kern- oder benutzerspezifischen Marketing-Aktionen abrufen, indem Sie eine GET-Anfrage an `/marketingActions/core` oder `/marketingActions/custom` senden.

**API-Format**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Anfrage**

Die folgende Anfrage ruft eine Liste von benutzerspezifischen Marketing-Aktionen ab, die von Ihrem Unternehmen verwaltet werden.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details für jede abgerufene Marketing-Aktion zurück, einschließlich `name` und `href`. Der Wert `href` wird beim [Erstellen einer Datennutzungsrichtlinie](policies.md#create-policy) zur Identifizierung der Marketing-Aktion verwendet.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `_page.count` | Die Gesamtzahl der zurückgegebenen Marketing-Aktionen. |
| `children` | Ein Array von Objekten, die die Details der abgerufenen Marketing-Aktionen enthalten. |
| `name` | Der Name der Marketing-Aktion, die beim [Suchen nach einer bestimmten Marketing-Aktion](#lookup) als eindeutige Kennung fungiert. |
| `_links.self.href` | Eine URI-Referenz für die Marketing-Aktion, mit der beim [Erstellen einer Datenverwendungsrichtlinie](policies.md#create-policy) das `marketingActionsRefs`-Array abgeschlossen werden kann. |

## Suchen Sie nach einer bestimmten Marketing-Aktion {#lookup}

Sie können die Details einer bestimmten Marketing-Aktion nachschlagen, indem Sie die `name`-Eigenschaft der Marketing-Aktion in den Pfad einer GET-Anfrage aufnehmen.

**API-Format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Die `name`-Eigenschaft der Marketing-Aktion, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anfrage ruft eine benutzerdefinierte Marketing-Aktion mit dem Namen `combineData` ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Antwortobjekt enthält die Details zur Marketing-Aktion, einschließlich des Pfads (`_links.self.href`), der beim [Definieren einer Datenverwendungsrichtlinie](policies.md#create-policy) zum Verweisen auf die Marketing-Aktion benötigt wird (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
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

## Erstellen oder aktualisieren einer benutzerspezifischen Marketing-Aktion {#create-update}

Sie können eine neue benutzerspezifische Marketing-Aktion erstellen oder eine vorhandene aktualisieren, indem Sie den vorhandenen oder beabsichtigten Namen der Marketing-Aktion in den Pfad einer PUT-Anfrage aufnehmen.

**API-Format**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die erstellt oder aktualisiert werden soll. Wenn im System bereits eine Marketing-Aktion mit dem angegebenen Namen vorhanden ist, wird diese Marketing-Aktion aktualisiert. Wenn noch keine Marketing-Aktion vorhanden ist, wird eine neue mit dem angegebenen Namen erstellt. |

**Anfrage**

Die folgende Anfrage erstellt eine neue Marketing-Aktion mit dem Namen `crossSiteTargeting`, sofern im System noch keine Marketing-Aktion mit demselben Namen vorhanden ist. Wenn eine `crossSiteTargeting`-Marketing-Aktion vorhanden ist, wird diese stattdessen auf der Grundlage der in der Payload bereitgestellten Eigenschaften aktualisiert.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name der Marketing-Aktion, die erstellt oder aktualisiert werden soll. <br><br>**WICHTIG**: Diese Eigenschaft muss mit dem `{MARKETING_ACTION_NAME}` im Pfad übereinstimmen, andernfalls tritt ein HTTP-400-Fehler (Bad Request) auf. Mit anderen Worten: Nach dem Erstellen einer Marketing-Aktion kann deren Eigenschaft `name` nicht mehr geändert werden. |
| `description` | Eine optionale Beschreibung, um mehr Kontexte für die Marketing-Aktion anzugeben. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Marketing-Aktion zurück. Wenn eine vorhandene Marketing-Aktion aktualisiert wurde, gibt die Antwort den HTTP-Status 200 (OK) zurück. Wenn eine neue Marketing-Aktion erstellt wurde, gibt die Antwort den HTTP-Status 201 (Created) zurück.

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
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

## Löschen einer benutzerspezifischen Marketing-Aktion {#delete}

Sie können eine benutzerspezifische Marketing-Aktion löschen, indem Sie deren Namen in den Pfad einer DELETE-Anfrage aufnehmen.

>[!NOTE]
>
>Marketing-Aktionen, die von bestehenden Richtlinien referenziert werden, können nicht gelöscht werden. Der Versuch, eine solche Marketing-Aktionen zu löschen, führt zu einem HTTP-400-Fehler (Bad Request) in Kombination mit einer Meldung, in der die IDs aller Richtlinien enthalten sind, die auf die Marketing-Aktion verweisen.

**API-Format**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) mit einem leeren Antworttext zurück.

Sie können überprüfen, ob der Löschvorgang erfolgreich war, indem Sie versuchen, [nach der die Marketing-Aktion zu suchen](#look-up). Dies sollte zu einem HTTP-404-Fehler (Not Found) führen, wenn die Marketing-Aktion aus dem System entfernt wurde.
