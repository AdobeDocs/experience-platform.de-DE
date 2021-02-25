---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: API-Endpunkt für berechnete Attribute
topic: guide
type: Dokumentation
description: In Adobe Experience Platform sind berechnete Attribute Funktionen, mit denen Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene Aggregat werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können. In diesem Handbuch wird das Erstellen, Ansicht, Aktualisieren und Löschen von berechneten Attributen mithilfe der Echtzeit-Customer Profil API beschrieben.
translation-type: tm+mt
source-git-commit: 4ed2b80ebfd87f8920462ae0a918b01bb13d4210
workflow-type: tm+mt
source-wordcount: '2279'
ht-degree: 61%

---


# (Alpha) API-Endpunkt für berechnete Attribute

>[!IMPORTANT]
>
>Die in diesem Dokument beschriebene Funktion für berechnete Attribute ist derzeit als Alphaversion erhältlich und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene Aggregat werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können. Dieses Handbuch enthält Beispiel-API-Aufrufe für die Durchführung grundlegender CRUD-Vorgänge mit dem Endpunkt `/computedAttributes`.

Um mehr über berechnete Attribute zu erfahren, lesen Sie zunächst die [Übersicht über berechnete Attribute](overview.md).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [Echtzeit-Client-Profil-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Profil-API - Erste Schritte](../api/getting-started.md) nach Links zur empfohlenen Dokumentation, einem Leitfaden zum Lesen der in diesem Dokument angezeigten Beispiel-API-Aufrufe und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer beliebigen Experience Platformen-API erforderlich sind.

## Berechnete Attributfelder konfigurieren

Um ein berechnetes Attribut zu erstellen, müssen Sie zunächst das Feld in einem Schema identifizieren, das den berechneten Attributwert enthält.

Informationen zum Erstellen eines berechneten Attributfelds in einem Schema finden Sie in der Dokumentation zu [Konfigurieren eines berechneten Attributs](configure-api.md).

>[!WARNING]
>
>Um mit dem API-Handbuch fortzufahren, müssen Sie über ein Feld für berechnete Attribute verfügen.

## Berechnetes Attribut erstellen {#create-a-computed-attribute}

Wenn Ihr berechnetes Attributfeld im aktivierten Schema Ihres Profils definiert ist, können Sie jetzt ein berechnetes Attribut konfigurieren. Wenn Sie dies noch nicht getan haben, befolgen Sie bitte den in der Dokumentation [Konfigurieren eines berechneten Attributs](configure-api.md) beschriebenen Arbeitsablauf.

Um ein berechnetes Attribut zu erstellen, starten Sie zunächst eine Anforderung an den `/config/computedAttributes`-Endpunkt mit einem Anforderungstext, der die Details des berechneten Attributs enthält, das Sie erstellen möchten.

**API-Format**

```http
POST /config/computedAttributes
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `name` | Name des berechneten Attributfelds als Zeichenfolge. |
| `path` | Pfad zum Feld mit dem berechneten Attribut. Dieser Pfad befindet sich im `properties`-Attribut des Schemas und sollte NICHT den Feldnamen im Pfad beinhalten. Lassen Sie beim Schreiben des Pfads die verschiedenen Ebenen von `properties`-Attributen weg. |
| `{TENANT_ID}` | Wenn Sie Ihre Mandantenkennung nicht kennen, lesen Sie bitte die Anleitung zum Finden Ihrer Mandantenkennung im [Entwicklerhandbuch zur Schema Registry](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Eine Beschreibung des berechneten Attributs. Dies ist besonders nützlich, wenn verschiedene berechnete Attribute definiert wurden, da sie Kollegen in Ihrer IMS-Organisation hilft, das gewünschte berechnete Attribut zu finden. |
| `expression.value` | Ein gültiger Ausdruck [!DNL Profile Query Language] (PQL). Berechnete Attribute unterstützen derzeit die folgenden Funktionen: sum, count, min, max und boolean. Eine Liste von Beispieldokumenten finden Sie in der [Beispiel-PQL-Ausdruck](expressions.md)-Dokumentation. |
| `schema.name` | Die Klasse, auf der das Schema mit dem berechneten Attributfeld basiert. Beispiel: `_xdm.context.experienceevent` bei einem Schema, das auf der XDM ExperienceEvent-Klasse basiert. |

**Antwort**

Ein erfolgreich erstelltes berechnetes Attribut gibt den HTTP-Status 200 (OK) und einen Antworttext mit den Details des neu erstellten berechneten Attributs zurück. Zu den Details gehört eine eindeutige, schreibgeschützte, systemgenerierte `id`, die bei anderen API-Vorgängen zum Verweisen auf das berechnete Attribut verwendet werden kann.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `id` | Eine eindeutige, schreibgeschützte, systemgenerierte ID, die bei anderen API-Vorgängen zum Verweisen auf das berechnete Attribut genutzt werden kann. |
| `imsOrgId` | Die IMS-Organisation, die mit dem berechneten Attribut verbunden ist, sollte mit dem in der Anfrage gesendeten Wert übereinstimmen. |
| `sandbox` | Das Sandbox-Objekt enthält Details zur Sandbox, in der das berechnete Attribut konfiguriert wurde. Diese Daten werden aus der in der Anfrage gesendeten Sandbox-Kopfzeile extrahiert. Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md). |
| `positionPath` | Ein Array, das den dekonstruierten `path` zum in der Anfrage gesendeten Feld enthält. |
| `returnSchema.meta:xdmType` | Der Typ des Felds, in dem das berechnete Attribut gespeichert wird. |
| `definedOn` | Ein Array, das die Vereinigungsschemas anzeigt, auf deren Basis das berechnete Attribut definiert wurde. Enthält ein Objekt pro Vereinigungsschema, d. h. es können mehrere Objekte im gleichen Array vorhanden sein, wenn das berechnete Attribut anhand verschiedener Klassen unterschiedlichen Schemas hinzugefügt wurde. |
| `active` | Ein boolescher Wert, der anzeigt, ob das berechnete Attribut aktuell aktiv ist oder nicht. Der Standardwert ist `true`. |
| `type` | Der Typ der erstellten Ressource; in diesem Fall ist „ComputedAttribute“ der Standardwert. |
| `createEpoch` und `updateEpoch` | Der Zeitpunkt, zu dem das berechnete Attribut erstellt bzw. zuletzt aktualisiert wurde. |

## Erstellen Sie ein berechnetes Attribut, das auf vorhandene berechnete Attribute verweist

Es ist auch möglich, ein berechnetes Attribut zu erstellen, das auf vorhandene berechnete Attribute verweist. Dazu müssen Sie zunächst eine POST an den `/config/computedAttributes`-Endpunkt anfordern. Der Anforderungstext enthält Verweise auf die berechneten Attribute im Feld `expression.value`, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
POST /config/computedAttributes
```

**Anfrage**

In diesem Beispiel wurden bereits zwei berechnete Attribute erstellt, die zur Definition eines dritten Attributs verwendet werden. Die vorhandenen berechneten Attribute sind:

* **`totalSpend`:** Erfasst den Gesamtdollarbetrag, den ein Kunde ausgegeben hat.
* **`countPurchases`:** Zählt die Anzahl der Käufe, die ein Kunde getätigt hat.

Die unten stehende Anforderung verweist auf die beiden vorhandenen berechneten Attribute, wobei gültige PQL verwendet werden, um das neue `averageSpend`-Attribut zu dividieren.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "averageSpend",
        "path" : "_{TENANT_ID}.purchaseSummary",
        "description" : "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `name` | Name des berechneten Attributfelds als Zeichenfolge. |
| `path` | Pfad zum Feld mit dem berechneten Attribut. Dieser Pfad befindet sich im `properties`-Attribut des Schemas und sollte NICHT den Feldnamen im Pfad beinhalten. Lassen Sie beim Schreiben des Pfads die verschiedenen Ebenen von `properties`-Attributen weg. |
| `{TENANT_ID}` | Wenn Sie Ihre Mandantenkennung nicht kennen, lesen Sie bitte die Anleitung zum Finden Ihrer Mandantenkennung im [Entwicklerhandbuch zur Schema Registry](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Eine Beschreibung des berechneten Attributs. Dies ist besonders nützlich, wenn verschiedene berechnete Attribute definiert wurden, da sie Kollegen in Ihrer IMS-Organisation hilft, das gewünschte berechnete Attribut zu finden. |
| `expression.value` | Ein gültiger PQL-Ausdruck. Berechnete Attribute unterstützen derzeit die folgenden Funktionen: sum, count, min, max und boolean. Eine Liste von Beispieldokumenten finden Sie in der [Beispiel-PQL-Ausdruck](expressions.md)-Dokumentation.<br/><br/>In diesem Beispiel verweist der Ausdruck auf zwei vorhandene berechnete Attribute. Auf die Attribute wird mit den Werten `path` und `name` des berechneten Attributs verwiesen, wie sie in dem Schema angezeigt werden, in dem die berechneten Attribute definiert wurden. Beispiel: Das `path` des ersten referenzierten berechneten Attributs ist `_{TENANT_ID}.purchaseSummary` und das `name` ist `totalSpend`. |
| `schema.name` | Die Klasse, auf der das Schema mit dem berechneten Attributfeld basiert. Beispiel: `_xdm.context.experienceevent` bei einem Schema, das auf der XDM ExperienceEvent-Klasse basiert. |

**Antwort**

Ein erfolgreich erstelltes berechnetes Attribut gibt den HTTP-Status 200 (OK) und einen Antworttext mit den Details des neu erstellten berechneten Attributs zurück. Zu den Details gehört eine eindeutige, schreibgeschützte, systemgenerierte `id`, die bei anderen API-Vorgängen zum Verweisen auf das berechnete Attribut verwendet werden kann.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
      },
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `id` | Eine eindeutige, schreibgeschützte, systemgenerierte ID, die bei anderen API-Vorgängen zum Verweisen auf das berechnete Attribut genutzt werden kann. |
| `imsOrgId` | Die IMS-Organisation, die mit dem berechneten Attribut verbunden ist, sollte mit dem in der Anfrage gesendeten Wert übereinstimmen. |
| `sandbox` | Das Sandbox-Objekt enthält Details zur Sandbox, in der das berechnete Attribut konfiguriert wurde. Diese Daten werden aus der in der Anfrage gesendeten Sandbox-Kopfzeile extrahiert. Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md). |
| `positionPath` | Ein Array, das den dekonstruierten `path` zum in der Anfrage gesendeten Feld enthält. |
| `returnSchema.meta:xdmType` | Der Typ des Felds, in dem das berechnete Attribut gespeichert wird. |
| `definedOn` | Ein Array, das die Vereinigungsschemas anzeigt, auf deren Basis das berechnete Attribut definiert wurde. Enthält ein Objekt pro Vereinigungsschema, d. h. es können mehrere Objekte im gleichen Array vorhanden sein, wenn das berechnete Attribut anhand verschiedener Klassen unterschiedlichen Schemas hinzugefügt wurde. |
| `active` | Ein boolescher Wert, der anzeigt, ob das berechnete Attribut aktuell aktiv ist oder nicht. Der Standardwert ist `true`. |
| `type` | Der Typ der erstellten Ressource; in diesem Fall ist „ComputedAttribute“ der Standardwert. |
| `createEpoch` und `updateEpoch` | Der Zeitpunkt, zu dem das berechnete Attribut erstellt bzw. zuletzt aktualisiert wurde. |

## Berechnete Attribute aufrufen

Beim Arbeiten mit berechneten Attributen unter Verwendung der API gibt es zwei Optionen zum Aufrufen berechneter Attribute, die Ihre Organisation definiert hat. Die erste besteht im Auflisten aller berechneten Attribute, die zweite im Anzeigen eines bestimmten berechneten Attributs anhand seiner eindeutigen `id`.

Die Schritte für beide Zugriffsmuster werden in diesem Dokument beschrieben. Wählen Sie zu Beginn eine der folgenden Optionen aus:

* **[Liste aller vorhandenen berechneten Attribute](#list-all-computed-attributes):** Geben Sie eine Liste aller von Ihrem Unternehmen erstellten berechneten Attribute zurück.
* **[Ansicht eines bestimmten berechneten Attributs](#view-a-computed-attribute):** Geben Sie die Details eines einzelnen berechneten Attributs zurück, indem Sie seine ID während der Anforderung angeben.

### Liste aller berechneten Attribute {#list-all-computed-attributes}

Ihre IMS-Organisation kann mehrere berechnete Attribute erstellen; durch Richten einer GET-Anfrage an den `/config/computedAttributes`-Endpunkt können Sie alle vorhandenen berechneten Attribute für Ihre Organisation auflisten.

**API-Format**

```http
GET /config/computedAttributes
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort umfasst ein `_page`-Attribut, das die Gesamtzahl der berechneten Attribute (`totalCount`) und die Zahl der berechneten Attribute auf der Seite (`pageSize`) angibt.

Die Antwort enthält auch ein `children`-Array, das aus einem oder mehreren Objekten besteht, von denen jedes die Details zu einem berechneten Attribut enthält. Wenn Ihr Unternehmen über keine berechneten Attribute verfügt, sind `totalCount` und `pageSize` 0 (null) und das `children`-Array leer.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `_page.totalCount` | Die Gesamtzahl der von Ihrer IMS-Organisation definierten berechneten Attribute. |
| `_page.pageSize` | Die Zahl der berechneten Attribute, die auf dieser Ergebnisseite zurückgegeben werden. Wenn `pageSize` gleich `totalCount` ist, bedeutet das, dass nur eine Seite mit Ergebnissen vorhanden ist und alle berechneten Attribute zurückgegeben wurden. Wenn die Werte ungleich sind, gibt es weitere Seiten mit Ergebnissen, die aufgerufen werden können. Weiterführende Informationen finden Sie unter `_links.next`. |
| `children` | Ein Array, das aus einem oder mehreren Objekten besteht, von denen jedes die Details zu einem einzelnen berechneten Attribut enthält. Wenn keine berechneten Attribute definiert wurden, ist das `children`-Array leer. |
| `id` | Ein eindeutiger, schreibgeschützter, systemgenerierter Wert, der einem berechneten Attribut bei der Erstellung automatisch zugewiesen wird. Weiterführende Informationen zu den Komponenten eines berechneten Attributobjekts finden Sie im Abschnitt zum [Erstellen eines berechneten Attributs](#create-a-computed-attribute) weiter oben in diesem Tutorial. |
| `_links.next` | Wenn eine einzelne Seite mit berechneten Attributen zurückgegeben wird, ist `_links.next` ein leeres Objekt (wie in der obigen Beispielantwort dargestellt). Wenn Ihre Organisation über viele berechnete Attribute verfügt, werden diese auf mehreren Seiten zurückgegeben, auf die Sie mittels einer GET-Anfrage an den `_links.next`-Wert zugreifen können. |

### Berechnetes Attribut anzeigen {#view-a-computed-attribute}

Sie können ein bestimmtes berechnetes Attribut Ansicht haben, indem Sie eine GET an den Endpunkt `/config/computedAttributes` anfordern und die berechnete Attribut-ID in den Anforderungspfad aufnehmen.

**API-Format**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{ATTRIBUTE_ID}` | Die Kennung des berechneten Attributs, das Sie anzeigen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Berechnetes Attribut aktualisieren

Wenn Sie merken, dass Sie ein vorhandenes berechnetes Attribut aktualisieren müssen, senden Sie eine PATCH-Anfrage an den `/config/computedAttributes`-Endpunkt und schließen die Kennung des berechneten Attributs, das Sie aktualisieren möchten, in den Anfragepfad ein.

**API-Format**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{ATTRIBUTE_ID}` | Die Kennung des berechneten Attributs, das Sie aktualisieren möchten. |

**Anfrage**

Diese Anfrage nutzt die [JSON Patch-Formatierung](http://jsonpatch.com/), um den „value“ (Wert) des Felds „expression“ (Ausdruck) zu aktualisieren.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Eigenschaft | Beschreibung |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Ein gültiger Ausdruck [!DNL Profile Query Language] (PQL). Berechnete Attribute unterstützen derzeit die folgenden Funktionen: sum, count, min, max und boolean. Eine Liste von Beispieldokumenten finden Sie in der [Beispiel-PQL-Ausdruck](expressions.md)-Dokumentation. |

**Antwort**

Bei erfolgreicher Aktualisierung werden der HTTP-Status 204 (Kein Inhalt) und ein leerer Antworttext zurückgegeben. Wenn Sie sich vergewissern möchten, dass die Aktualisierung erfolgreich war, können Sie eine GET-Anfrage ausführen, um das berechnete Attribut mit seiner Kennung anzuzeigen.

## Berechnetes Attribut löschen

Sie können ein berechnetes Attribut mithilfe der API auch löschen. Dies geschieht durch Richten einer DELETE-Anfrage an den `/config/computedAttributes`-Endpunkt und Einschließen der Kennung des berechneten Attributs, das Sie löschen möchten, in den Anfragepfad.

>[!NOTE]
>
>Seien Sie beim Löschen eines berechneten Attributs vorsichtig, da es möglicherweise in mehr als einem Schema verwendet wird und der DELETE-Vorgang nicht rückgängig gemacht werden kann.

**API-Format**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{ATTRIBUTE_ID}` | Die Kennung des berechneten Attributs, das Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Antwort**

Bei erfolgreicher Löschanfrage werden der HTTP-Status 200 (OK) und ein leerer Antworttext zurückgegeben. Um sicherzugehen, dass der Löschvorgang erfolgreich war, können Sie eine GET-Anfrage ausführen und das berechnete Attribut anhand seiner Kennung nachschlagen. Wenn das Attribut gelöscht wurde, erhalten Sie den HTTP-Fehlerstatus 404 (Nicht gefunden).

## Erstellen einer Segmentdefinition, die auf ein berechnetes Attribut verweist

Mit Adobe Experience Platform können Sie Segmente erstellen, die eine Gruppe spezifischer Attribute oder Verhaltensweisen aus einer Gruppe von Profilen definieren. Eine Segmentdefinition enthält einen Ausdruck, der eine in PQL geschriebene Abfrage kapselt. Diese Ausdruck können auch auf berechnete Attribute verweisen.

Im folgenden Beispiel wird eine Segmentdefinition erstellt, die auf ein vorhandenes berechnetes Attribut verweist. Weitere Informationen zu Segmentdefinitionen und deren Verwendung in der Segmentierungsdienst-API finden Sie im Handbuch [API-Endpunkt für Segmentdefinitionen](../../segmentation/api/segment-definitions.md).

Erstellen Sie zunächst eine POST an den `/segment/definitions`-Endpunkt und geben Sie das berechnete Attribut im Anforderungstext an.

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein eindeutiger Name für das Segment als Zeichenfolge. |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |
| `schema.name` | Das Schema, das den Entitäten im Segment zugeordnet ist. Besteht aus einem `id`- oder `name`-Feld. |
| `expression` | Ein Objekt, das Felder mit Informationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruck-Typ an. Derzeit wird nur &quot;PQL&quot;unterstützt. |
| `expression.format` | Gibt die Wertstruktur des Ausdrucks an. Derzeit wird nur `pql/text` unterstützt. |
| `expression.value` | Ein gültiger PQL-Ausdruck, in diesem Beispiel enthält er einen Verweis auf ein vorhandenes berechnetes Attribut. |

Weitere Informationen zu Segmentdefinitionsattributen finden Sie in den Beispielen, die im API-Endpunktleitfaden [für Segmentdefinitionen](../../segmentation/api/segment-definitions.md) bereitgestellt werden.

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Segmentdefinition zurück. Weitere Informationen zu Antwortobjekten der Segmentdefinition finden Sie im Handbuch [API-Endpunkt für Segmentdefinitionen](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## Nächste Schritte

Nachdem Sie sich mit den Grundlagen berechneter Attribute vertraut gemacht haben, können Sie nun mit der Definition berechneter Attribute für Ihre Organisation beginnen.