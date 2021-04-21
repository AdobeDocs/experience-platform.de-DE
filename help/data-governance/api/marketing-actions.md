---
keywords: Experience Platform;Home;beliebte Themen;Politikdurchsetzung;Marketingaktionen API;API-basierte Durchsetzung;Datenverwaltung
solution: Experience Platform
title: API-Endpunkt für Marketingaktionen
topic-legacy: developer guide
description: Eine Marketingaktion im Rahmen der Adobe Experience Platform-Datenverwaltung ist eine Maßnahme, die ein Datenbenutzer in der Experience Platform ergreift und bei der überprüft werden muss, ob die Datenverwendungsrichtlinien verletzt wurden.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 5%

---

# Endpunkt der Marketing-Aktionen

Eine Marketingaktion im Zusammenhang mit dem Adobe Experience Platform [!DNL Data Governance] ist eine Aktion, die ein [!DNL Experience Platform]-Datenbenutzer durchführt und bei der überprüft werden muss, ob die Datenverwendungsrichtlinien verletzt wurden.

Sie können Marketingaktionen für Ihr Unternehmen mithilfe des Endpunkts `/marketingActions` in der Policy Service API verwalten.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Abrufen einer Liste von Marketingaktionen {#list}

Sie können eine Liste von Kern- oder benutzerspezifischen Marketingaktionen abrufen, indem Sie eine GET an `/marketingActions/core` oder `/marketingActions/custom` anfordern.

**API-Format**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Anfrage**

Die folgende Anforderung ruft eine Liste von benutzerspezifischen Marketingaktionen ab, die von Ihrem Unternehmen verwaltet werden.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details für jede abgerufene Marketingaktion zurück, einschließlich `name` und `href`. Der Wert `href` wird zur Identifizierung der Marketingaktion verwendet, wenn [eine Datenverwendungsrichtlinie](policies.md#create-policy) erstellt wird.

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
| `_page.count` | Die Gesamtzahl der zurückgegebenen Marketingaktionen. |
| `children` | Ein Array von Objekten, die die Details der abgerufenen Marketingaktionen enthalten. |
| `name` | Der Name der Marketingaktion, die als eindeutiger Bezeichner fungiert, wenn [eine bestimmte Marketingaktion](#lookup) sucht. |
| `_links.self.href` | Eine URI-Referenz für die Marketingaktion, mit der das `marketingActionsRefs`-Array abgeschlossen werden kann, wenn [eine Datenverwendungsrichtlinie](policies.md#create-policy) erstellt wird. |

## Suchen Sie nach einer bestimmten Marketingaktion {#lookup}

Sie können die Details einer bestimmten Marketingaktion nachschlagen, indem Sie die `name`-Eigenschaft der Marketingaktion in den Pfad einer GET-Anforderung aufnehmen.

**API-Format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Die `name`-Eigenschaft der Marketingaktion, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anforderung ruft eine benutzerdefinierte Marketingaktion mit dem Namen `combineData` ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Antwortobjekt enthält die Details für die Marketingaktion, einschließlich des Pfads (`_links.self.href`), der zum Verweisen auf die Marketingaktion benötigt wird, wenn [eine Datenverwendungsrichtlinie](policies.md#create-policy) (`marketingActionsRefs`) definiert wird.

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

## Erstellen oder aktualisieren Sie eine benutzerdefinierte Marketingaktion {#create-update}

Sie können eine neue benutzerspezifische Marketingaktion erstellen oder eine vorhandene aktualisieren, indem Sie den vorhandenen oder beabsichtigten Namen der Marketingaktion in den Pfad einer PUT-Anforderung aufnehmen.

**API-Format**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion, die erstellt oder aktualisiert werden soll. Wenn im System bereits eine Marketingaktion mit dem angegebenen Namen vorhanden ist, wird diese Marketingaktion aktualisiert. Wenn keine Marketingaktion vorhanden ist, wird eine neue Marketingaktion für den angegebenen Namen erstellt. |

**Anfrage**

Die folgende Anforderung erstellt eine neue Marketingaktion mit dem Namen `crossSiteTargeting`, sofern im System noch keine Marketingaktion mit demselben Namen vorhanden ist. Wenn eine `crossSiteTargeting`-Marketingaktion vorhanden ist, wird diese Marketingaktion stattdessen auf der Grundlage der in der Nutzlast bereitgestellten Eigenschaften aktualisiert.

```shell
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
| `name` | Der Name der Marketingaktion, die erstellt oder aktualisiert werden soll. <br><br>**WICHTIG**: Diese Eigenschaft muss mit dem  `{MARKETING_ACTION_NAME}` im Pfad übereinstimmen, andernfalls tritt ein HTTP-400-Fehler (Fehlerhafte Anforderung) auf. Mit anderen Worten, nach Erstellung einer Marketingaktion kann deren `name`-Eigenschaft nicht mehr geändert werden. |
| `description` | Eine optionale Beschreibung, um weitere Kontexte für die Marketingaktion anzugeben. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Marketingaktion zurück. Wenn eine vorhandene Marketingaktion aktualisiert wurde, gibt die Antwort den HTTP-Status 200 (OK) zurück. Wenn eine neue Marketingaktion erstellt wurde, gibt die Antwort den HTTP-Status 201 (Erstellt) zurück.

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

## Löschen Sie eine benutzerdefinierte Marketingaktion {#delete}

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
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) mit einem leeren Antworttext zurück.

Sie können den Löschvorgang bestätigen, indem Sie versuchen, [die Marketingaktion](#look-up) anzuzeigen. Sie sollten einen HTTP 404-Fehler (nicht gefunden) erhalten, wenn die Marketingaktion aus dem System entfernt wurde.
