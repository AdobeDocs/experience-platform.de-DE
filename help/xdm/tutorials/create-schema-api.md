---
keywords: Experience Platform;Startseite;beliebte Themen;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schemaregistrierung;Schemaregistrierung;Schema;Schema;Schemata;Erstellen
solution: Experience Platform
title: Erstellen eines Schemas mit der Schema Registry-API
type: Tutorial
description: In diesem Tutorial werden die Schritte dazu erläutert, wie mithilfe der Schema Registry-API ein Schema unter Verwendung einer Standardklasse erstellt wird.
exl-id: fa487a5f-d914-48f6-8d1b-001a60303f3d
source-git-commit: 030874e91b88b18f7de0cc2d12200243b7ed1d31
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 37%

---

# Erstellen Sie ein Schema mit dem [!DNL Schema Registry] API

Die [!DNL Schema Registry] wird verwendet, um auf die [!DNL Schema Library] innerhalb von Adobe Experience Platform. Die [!DNL Schema Library] enthält Ressourcen, die Ihnen nach Adobe zur Verfügung gestellt werden; [!DNL Experience Platform] Partner und Anbieter, deren Anwendungen Sie verwenden. Die Registry bietet eine Benutzeroberfläche und RESTful-API, über die auf alle in der Bibliothek verfügbaren Ressourcen zugegriffen werden kann.

In diesem Tutorial wird die [!DNL Schema Registry] API, um Sie durch die Schritte zum Erstellen eines Schemas mithilfe einer Standardklasse zu führen. Wenn Sie die Benutzeroberfläche in [!DNL Experience Platform], die [Tutorial zum Schema Editor](create-schema-ui.md) enthält schrittweise Anweisungen zum Ausführen ähnlicher Aktionen im Schema-Editor.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemakomposition.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die [Entwicklerhandbuch](../api/getting-started.md) für wichtige Informationen, die Sie benötigen, um erfolgreich Aufrufe an die [!DNL Schema Registry] API. Dies umfasst Ihre `{TENANT_ID}`, das Konzept der &quot;Container&quot;und die erforderlichen Kopfzeilen für Anfragen (mit besonderem Augenmerk auf die `Accept` -Kopfzeile und die möglichen Werte).

In diesem Tutorial werden die Schritte zur Erstellung eines „Loyalty Members“-Schemas, also eines Schemas zur Beschreibung von Daten zu Mitgliedern eines Treueprogramms im Einzelhandel, erläutert. Falls gewünscht, können Sie zum Einstieg einen Blick auf das [vollständige „Loyalty Members“-Schema](#complete-schema) im Anhang werfen.

## Erstellen eines Schemas mit einer Standardklasse

Ein Schema kann als Entwurf für die Daten betrachtet werden, in die Sie Daten aufnehmen möchten [!DNL Experience Platform]. Jedes Schema besteht aus einer Klasse und keiner oder mehr Schemafeldgruppen. Das heißt, Sie müssen keine Feldergruppe hinzufügen, um ein Schema zu definieren, aber in den meisten Fällen wird mindestens eine Feldergruppe verwendet.

### Zuweisen einer Klasse

Der erste Schritt für die Erstellung eines Schemas besteht in der Auswahl einer Klasse. Die Klasse definiert zentrale Aspekte bezüglich des Verhaltens der Daten (Datensatzdaten gegenüber Zeitreihendaten) sowie die zur Beschreibung der aufzunehmenden Daten mindestens erforderlichen Felder.

Das Schema, das Sie in diesem Tutorial erstellen, verwendet die [!DNL XDM Individual Profile] -Klasse. [!DNL XDM Individual Profile] ist eine Standardklasse, die von Adobe zur Definition des Datensatzverhaltens bereitgestellt wird. Weitere Informationen zum Verhalten finden Sie unter [Grundlagen zum Aufbau von Schemas](../schema/composition.md).

Um eine Klasse zuzuweisen, wird ein API-Aufruf ausgeführt, über den ein neues Schema im Mandanten-Container (mittels POST-Anfrage) erstellt wird. Dieser Aufruf enthält die vom Schema zu implementierende Klasse. Ein Schema kann immer nur eine Klasse implementieren.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die Anfrage muss ein `allOf`-Attribut enthalten, das auf die `$id` einer Klasse verweist. Dieses Attribut definiert die „Basisklasse“, die das Schema implementiert. In diesem Beispiel ist die Basisklasse die [!DNL XDM Individual Profile] -Klasse. Die `$id`[!DNL XDM Individual Profile] der Klasse „“ wird als Wert des Felds `$ref` im Array `allOf` verwendet, wie unten dargestellt.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Members",
        "description": "Information for all members of the loyalty program",
        "allOf": [
            {
              "$ref": "https://ns.adobe.com/xdm/context/profile"
            }
        ]
      }'
```

**Antwort**

Bei erfolgreicher Anfrage wird der HTTP-Status-Code 201 (Erstellung bestätigt) mit einem Antworttext zurückgegeben, der Details zum neu erstellten Schema einschließlich `$id`, `meta:altIt` und `version` enthält. Diese Werte sind schreibgeschützt und werden von der [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/tenantId/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_tenantId.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310304048,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_tenantId"
}
```

### Nachschlagen eines Schemas

Um Ihr neu erstelltes Schema anzuzeigen, führen Sie eine Anfrage zum Nachschlagen (GET) aus, in der Sie die `meta:altId` oder die URL-codierte `$id`-URI des Schemas angeben.

**API-Format**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodiert `$id` des Schemas, das Sie nachschlagen möchten. |

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F533ca5da28087c44344810891b0f03d9\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

**Antwort**

Das Antwortformat hängt von der `Accept` -Header mit der -Anfrage gesendet. Experimentieren mit verschiedenen `Accept` Kopfzeilen, um zu sehen, welche am besten Ihren Anforderungen entspricht.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310304048,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:allFieldAccess": true
}
```

### Feldergruppe hinzufügen {#add-a-field-group}

Nachdem das &quot;Loyalty Members&quot;-Schema erstellt und bestätigt wurde, können Feldergruppen hinzugefügt werden.

Je nach ausgewählter Schemaklasse stehen verschiedene Standardfeldgruppen zur Verfügung. Jede Feldergruppe enthält eine `intendedToExtend` -Feld, das die Klassen definiert, mit denen diese Feldergruppe kompatibel ist.

Feldergruppen definieren Konzepte wie &quot;Name&quot;oder &quot;Adresse&quot;, die in jedem Schema wiederverwendet werden können, in dem dieselben Informationen erfasst werden sollen.

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodiert `$id` des Schemas, dem Sie die Feldergruppe hinzufügen. |

**Anfrage**

Mit dieser Anfrage wird das &quot;Loyalty Members&quot;-Schema dahingehend aktualisiert, dass es die Felder in den [[!UICONTROL Demografische Details] Feldergruppe](../field-groups/profile/demographic-details.md) (`profile-person-details`).

Durch Hinzufügen der `profile-person-details` -Feldergruppe, erfasst das &quot;Loyalty Members&quot;-Schema jetzt demografische Informationen für Mitglieder des Treueprogramms, z. B. ihren Vornamen, Nachnamen und Geburtstag.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-person-details"}}
      ]'
```

**Antwort**

Die Antwort zeigt die neu hinzugefügte Feldergruppe im `meta:extends` Array und enthält `$ref` zur Feldergruppe in der `allOf` -Attribut.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310912096,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "b480f28a35f356b237fc129e796074a3f33a7a67df273f6a8beaee1ec6465540",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### Hinzufügen weiterer Feldergruppen

Für die Schemas &quot;Mitglieder des Treueprogramms&quot;sind zwei weitere Standardfeldgruppen erforderlich, die Sie hinzufügen können, indem Sie die Schritte mit einer anderen Feldergruppe wiederholen.

>[!TIP]
>
>Es empfiehlt sich, alle verfügbaren Feldergruppen zu überprüfen, um sich mit den in den einzelnen Feldern enthaltenen Feldern vertraut zu machen. Sie können alle für eine bestimmte Klasse verfügbaren Feldergruppen auflisten (GET), indem Sie eine Anfrage für jeden der Container &quot;global&quot;und &quot;tenant&quot;ausführen und nur die Feldergruppen zurückgeben, bei denen das Feld &quot;meta:scheduledToExtend&quot;mit der von Ihnen verwendeten Klasse übereinstimmt. In diesem Fall ist es die [!DNL XDM Individual Profile] -Klasse, also die [!DNL XDM Individual Profile] `$id` wird verwendet:
>
>
```http
>GET /global/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>GET /tenant/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>```

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodiert `$id` des Schemas, das Sie aktualisieren. |

**Anfrage**

Mit dieser Anfrage wird das &quot;Loyalty Members&quot;-Schema dahingehend aktualisiert, dass es die Felder der folgenden Standardfeldgruppen enthält:

* [[!UICONTROL Persönliche Kontaktangaben]](../field-groups/profile/personal-contact-details.md) (`profile-personal-details`): Fügt Kontaktinformationen wie Privatadresse, E-Mail-Adresse und Privattelefon hinzu.
* [[!UICONTROL Treuedetails]](../field-groups/profile/loyalty-details.md) (`profile-loyalty-details`): Fügt Kontaktinformationen wie Privatadresse, E-Mail-Adresse und Privattelefon hinzu.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"}}
      ]'  
```

**Antwort**

Die Antwort zeigt die neu hinzugefügten Feldergruppen im `meta:extends` Array und enthält `$ref` zur Feldergruppe in der `allOf` -Attribut.

Das &quot;Loyalty Members&quot;-Schema sollte jetzt vier `$ref` -Werte in `allOf` array: `profile`, `profile-person-details`, `profile-personal-details`und `profile-loyalty-details` wie unten dargestellt.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.2",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673311559934,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1de5ed1a07e3478719952f0a8c94d5e5390d5a9a998761adb4cf1989137fd6ea",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### Neue Feldergruppe definieren

Beim Standard [!UICONTROL Treuedetails] Feldergruppe bietet nützliche loyalitätsbezogene Felder für das Schema. Es gibt zusätzliche Treuefelder, die nicht in Standardfeldgruppen enthalten sind.

Um diese Felder hinzuzufügen, können Sie Ihre eigenen benutzerdefinierten Feldergruppen im `tenant` Container. Diese Feldergruppen sind für Ihre Organisation eindeutig und können von niemandem außerhalb Ihrer Organisation eingesehen oder bearbeitet werden.

Um eine neue Feldergruppe zu erstellen (POST), muss Ihre Anforderung eine `meta:intendedToExtend` -Feld, das die `$id` für die Basisklassen, mit denen die Feldergruppe kompatibel ist, zusammen mit den Eigenschaften, die die Feldergruppe enthalten soll.

Alle benutzerdefinierten Eigenschaften müssen unter Ihrer `TENANT_ID` um Kollisionen mit anderen Feldergruppen oder Feldern zu vermeiden.

**API-Format**

```http
POST /tenant/fieldgroups
```

**Anfrage**

Diese Anfrage erstellt eine neue Feldergruppe mit einer `loyaltyTier` -Objekt, das vier spezifische Felder für das Treueprogramm eines Unternehmens enthält: `id`, `effectiveDate`, `currentThreshold`und `nextThreshold`.

```SHELL
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Tier",
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Captures info about the current loyalty tier of a customer.",
        "definitions": {
          "loyaltyTier": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "loyaltyTier": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "title": "Loyalty Tier Identifier",
                        "type": "string",
                        "description": "Loyalty Tier Identifier."
                      },
                      "effectiveDate": {
                        "title": "Effective Date",
                        "type": "string",
                        "format": "date-time",
                        "description": "Date the member joined their current loyalty tier."
                      },
                      "currentThreshold": {
                        "title": "Current Point Threshold",
                        "type": "integer",
                        "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                      },
                      "nextThreshold": {
                        "title": "Next Point Threshold",
                        "type": "integer",
                        "description": "The number of loyalty points the member must accrue to graduate to the next tier."
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/loyaltyTier"
          }
        ]
      }'
```

**Antwort**

Bei erfolgreicher Anfrage wird der HTTP-Status-Code 201 (Erstellt) mit einem Antworttext zurückgegeben, der die Details der neu erstellten Feldergruppe einschließlich der `$id`, `meta:altIt`und `version`. Diese Werte sind schreibgeschützt und werden von der [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "type": "object",
              "properties": {
                "id": {
                  "title": "Loyalty Tier Identifier",
                  "type": "string",
                  "description": "Loyalty Tier Identifier.",
                  "meta:xdmType": "string"
                },
                "effectiveDate": {
                  "title": "Effective Date",
                  "type": "string",
                  "format": "date-time",
                  "description": "Date the member joined their current loyalty tier.",
                  "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                  "title": "Current Point Threshold",
                  "type": "integer",
                  "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                  "meta:xdmType": "int"
                },
                "nextThreshold": {
                  "title": "Next Point Threshold",
                  "type": "integer",
                  "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                  "meta:xdmType": "int"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673313004645,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### Hinzufügen der benutzerdefinierten Feldergruppe zum Schema

Sie können nun dieselben Schritte für [Hinzufügen einer Standardfeldgruppe](#add-a-field-group) , um diese neu erstellte Feldergruppe Ihrem Schema hinzuzufügen.

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodiert `$id` des Schemas. |

**Anfrage**

Mit dieser Anfrage wird das &quot;Loyalty Members&quot;-Schema aktualisiert (PATCH), um die Felder in die neue Feldergruppe &quot;Loyalitätsstufe&quot;aufzunehmen.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"}}
      ]'
```

**Antwort**

Sie können sehen, dass die Feldergruppe erfolgreich hinzugefügt wurde, da die Antwort jetzt die neu hinzugefügte Feldergruppe in der `meta:extends` -Array und enthalten eine `$ref` zur Feldergruppe in der `allOf` -Attribut.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Anzeigen des aktuellen Schemas

Sie können jetzt eine GET-Anfrage ausführen, um das aktuelle Schema anzuzeigen und zu sehen, wie die hinzugefügten Feldgruppen zur Gesamtstruktur des Schemas beigetragen haben.

**API-Format**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodiert `$id` des Schemas. |

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**Antwort**

Durch Verwendung der Variablen `application/vnd.adobe.xed-full+json; version=1` `Accept` -Kopfzeile, können Sie das vollständige Schema sehen, das alle Eigenschaften anzeigt. Diese Eigenschaften sind die von der Klasse und den Feldergruppen hinzugefügten Felder, die zum Erstellen des Schemas verwendet wurden. In der folgenden Beispielantwort werden nur die kürzlich hinzugefügten Felder für Leerzeichen angezeigt. Das vollständige Schema einschließlich aller Eigenschaften und ihren Attributen finden Sie im [Anhang](#appendix) am Ende dieses Dokuments.

under `"properties"`, können Sie die `_{TENANT_ID}` -Namespace, der beim Hinzufügen der benutzerdefinierten Feldergruppe erstellt wurde. Innerhalb dieses Namespace ist die `loyaltyTier` -Objekt und die Felder, die bei der Erstellung der Feldergruppe definiert wurden.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "type": "object",
              "properties": {
                "id": {
                  "title": "Loyalty Tier Identifier",
                  "type": "string",
                  "description": "Loyalty Tier Identifier.",
                  "meta:xdmType": "string"
                },
                "effectiveDate": {
                  "title": "Effective Date",
                  "type": "string",
                  "format": "date-time",
                  "description": "Date the member joined their current loyalty tier.",
                  "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                  "title": "Current Point Threshold",
                  "type": "integer",
                  "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                  "meta:xdmType": "int"
                },
                "nextThreshold": {
                  "title": "Next Point Threshold",
                  "type": "integer",
                  "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                  "meta:xdmType": "int"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673313004645,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### Erstellen eines Datentyps

Die von Ihnen erstellte Feldergruppe &quot;Loyalitätsstufe&quot;enthält spezifische Eigenschaften, die in anderen Schemas nützlich sein können. So können diese Daten etwa als Teil eines Erlebnisereignisses aufgenommen oder von einem Schema verwendet werden, das eine andere Klasse implementiert. Im vorliegenden Fall empfiehlt es sich, die Objekthierarchie als Datentyp zu speichern, da dieser die Wiederverwendung der Definition an anderer Stelle erleichtert.

Bei Datentypen muss eine Objekthierarchie nur einmal definiert werden. Anschließend kann sie, ganz ähnlich wie bei jedem anderen Typ von Skalar, in einem Feld darauf verweisen.

Mit anderen Worten: Datentypen ermöglichen die konsistente Verwendung von Strukturen mit mehreren Feldern mit mehr Flexibilität als Feldgruppen, da sie an einer beliebigen Stelle in ein Schema eingefügt werden können, indem sie als &quot;Typ&quot;eines Felds hinzugefügt werden.

**API-Format**

```http
POST /tenant/datatypes
```

**Anfrage**

Die Definition eines Datentyps erfordert `meta:extends` oder `meta:intendedToExtend` -Felder und -Felder müssen nicht unter Ihrer Mandanten-ID verschachtelt sein, um Kollisionen zu vermeiden.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Tier",
        "type": "object",
        "description": "Loyalty Tier data type",
        "definitions": {
          "loyaltyTier": {
            "type": "object",
            "properties": {
              "id": {
                "title": "Loyalty Tier Identifier",
                "type": "string",
                "description": "Loyalty Tier Identifier."
              },
              "effectiveDate": {
                "title": "Effective Date",
                "type": "string",
                "format": "date-time",
                "description": "Date the member joined their current loyalty tier."
              },
              "currentThreshold": {
                "title": "Current Point Threshold",
                "type": "integer",
                "description": "The minimum number of loyalty points the member must maintain to remain in the       current tier."
              },
              "nextThreshold": {
                "title": "Next Point Threshold",
                "type": "integer",
                "description": "The number of loyalty points the member must accrue to graduate to the next tier."
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/loyaltyTier"
          }
        ]
      }'
```

**Antwort**

Bei erfolgreicher Anfrage wird der HTTP-Statuscode 201 (Erstellung bestätigt) mit einem Antworttext zurückgegeben, der Details zum neu erstellten Datentyp einschließlich `$id`, `meta:altIt` und `version` enthält. Diese Werte sind schreibgeschützt und werden von der [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
  "meta:altId": "_{TENANT_ID}.datatypes.c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Loyalty Tier data type",
  "definitions": {
    "loyaltyTier": {
      "type": "object",
      "properties": {
        "id": {
          "title": "Loyalty Tier Identifier",
          "type": "string",
          "description": "Loyalty Tier Identifier.",
          "meta:xdmType": "string"
        },
        "effectiveDate": {
          "title": "Effective Date",
          "type": "string",
          "format": "date-time",
          "description": "Date the member joined their current loyalty tier.",
          "meta:xdmType": "date-time"
        },
        "currentThreshold": {
          "title": "Current Point Threshold",
          "type": "integer",
          "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
          "meta:xdmType": "int"
        },
        "nextThreshold": {
          "title": "Next Point Threshold",
          "type": "integer",
          "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
          "meta:xdmType": "int"
        }
      },
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673378256699,
    "repo:lastModifiedDate": 1673378256699,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "8afba84c0c9a68126a7a1389f8523a1112bdf4405badc6dcddbbb4a0e18f5cdb",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Mittels Anfrage zum Nachschlagen (GET) unter Angabe der URL-codierten `$id`-URI des Schemas können Sie den neuen Datentyp direkt anzeigen. Stellen Sie sicher, dass Sie die `version` in `Accept` -Kopfzeile für eine Suchanfrage.

### Verwenden des Datentyps im Schema

Nachdem der Datentyp Treueebene erstellt wurde, können Sie die `loyaltyTier` in der Feldergruppe, die Sie erstellt haben, um anstelle der zuvor vorhandenen Felder auf den Datentyp zu verweisen.

**API-Format**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{FIELD_GROUP_ID}` | Die `meta:altId` oder URL-kodiert `$id` der zu aktualisierenden Feldergruppe. |

**Anfrage**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "replace",
          "path": "/definitions/loyaltyTier/properties/_{TENANT_ID}/properties",
          "value": {
            "loyaltyTier": {
              "title": "Loyalty Tier",
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
              "description": "Loyalty tier info"
            }
          }
        }
      ]'
```

**Antwort**

Die Antwort enthält jetzt einen Verweis (`$ref`) zum Datentyp in der `loyaltyTier` -Objekt anstelle der zuvor definierten Felder.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.1",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "title": "Loyalty Tier",
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
              "description": "Loyalty tier info",
              "type": "object",
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673378970276,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "4df8fa56d00991590364606bb2e219e1ea8f5717a51c0e6ae57ca956830b6a27",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

Wenn Sie jetzt eine GET-Anfrage zum Nachschlagen des Schemas ausführen, wird die `loyaltyTier` -Eigenschaft zeigt den Verweis auf den Datentyp unter `meta:referencedFrom`:

```JSON
"_{TENANT_ID}": {
  "type": "object",
  "meta:xdmType": "object",
  "properties": {
    "loyaltyTier": {
      "title": "Loyalty Tier",
      "description": "Loyalty tier info",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "id": {
          "title": "Loyalty Tier Identifier",
          "type": "string",
          "description": "Loyalty Tier Identifier.",
          "meta:xdmType": "string"
        },
        "effectiveDate": {
          "title": "Effective Date",
          "type": "string",
          "format": "date-time",
          "description": "Date the member joined their current loyalty tier.",
          "meta:xdmType": "date-time"
        },
        "currentThreshold": {
          "title": "Current Point Threshold",
          "type": "integer",
          "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
          "meta:xdmType": "int"
        },
        "nextThreshold": {
          "title": "Next Point Threshold",
          "type": "integer",
          "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
          "meta:xdmType": "int"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
    }
  }
}
```

### Definieren eines Identitätsdeskriptors

Schemas werden zur Aufnahme von Daten in [!DNL Experience Platform]. Genutzt werden diese Daten schließlich von einer Vielzahl von Services, um eine umfassende, zentrale Sicht auf einzelne Personen zu schaffen. Für diesen Prozess wichtige Felder können als Identität klassifiziert und die in diesen Feldern aufgenommenen Daten in das Identitätsdiagramm der jeweiligen Person integriert werden. Auf die Diagrammdaten kann dann zugegriffen werden durch [[!DNL Real-Time Customer Profile]](../../profile/home.md) und andere [!DNL Experience Platform] -Services, um eine zusammengesetzte Ansicht jedes einzelnen Kunden bereitzustellen.

Zu den Feldern, die üblicherweise als &quot;Identität&quot;markiert sind, gehören: E-Mail-Adresse, Telefonnummer [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de), CRM-ID oder andere eindeutige ID-Felder. Für eine Klassifizierung als Identitätsfeld eignen sich alle eindeutigen Kennungen, die für Ihr Unternehmen spezifisch sind.

Identitätsdeskriptoren signalisieren, dass die `sourceProperty` des `sourceSchema` ist eine eindeutige Kennung, die als Identität betrachtet werden sollte.

Weitere Informationen zur Arbeit mit Deskriptoren finden Sie im [Schema Registry-Entwicklerhandbuch](../api/getting-started.md).

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anfrage definiert einen Identitätsdeskriptor für die `personalEmail.address` -Feld für das &quot;Loyalty Members&quot;-Schema. Diese Funktion [!DNL Experience Platform] die E-Mail-Adresse des Treuemitglieds als Kennung zu verwenden, um Informationen über die Person zusammenzufügen. Durch diesen Aufruf wird dieses Feld auch als primäre Identität für das Schema festgelegt, indem `xdm:isPrimary` nach `true`, die [Aktivieren des Schemas zur Verwendung im Echtzeit-Kundenprofil](#profile).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

>[!NOTE]
>
>Sie können verfügbare &quot;xdm:namespace&quot;-Werte auflisten oder neue erstellen, indem Sie die [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). Je nachdem, welcher „xdm:namespace“ verwendet wird, kann der Wert für „xdm:property“ entweder „xdm:code“ oder „xdm:id“ lauten.

**Antwort**

Bei erfolgreicher Anfrage wird der HTTP-Status-Code 201 (Erstellung bestätigt) mit einem Antworttext zurückgegeben, der Details zum neu erstellten Deskriptor und der ihm zugehörigen `@id` enthält. `@id` ist ein schreibgeschütztes Feld, das von der zugewiesen wird und in der API als Verweis auf den Deskriptor dient.[!DNL Schema Registry]

```JSON
{
  "@id": "719a4391897c097786efbaa6d4262bb928a1cd88540344c6",
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "imsOrg": "{ORG_ID}",
  "version": "1",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": true,
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production"
}
```

## Schema zur Verwendung in aktivieren [!DNL Real-Time Customer Profile] {#profile}

Sobald auf das Schema ein primärer Identitätsdeskriptor angewendet wurde, können Sie das Schema &quot;Mitglieder des Treueprogramms&quot;für die Verwendung durch [!DNL Real-Time Customer Profile] durch Hinzufügen eines `union` -Tag auf `meta:immutableTags` -Attribut.

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Vereinigungsansichten finden Sie im Abschnitt zu [Vereinigungen](../api/unions.md) im [!DNL Schema Registry] Entwicklerhandbuch.

### Hinzufügen einer `union` Tag

Damit ein Schema in die Vereinigungsansicht aufgenommen werden kann, muss die `union` -Tag hinzugefügt werden. `meta:immutableTags` -Attribut des Schemas. Dies erfolgt über eine PATCH-Anfrage, um das Schema zu aktualisieren und eine `meta:immutableTags` Array mit dem Wert `union`.

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodiert `$id` des Schemas, das Sie für Profil aktivieren. |

**Anfrage**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Antwort**

Die Antwort bestätigt den erfolgreiche Durchführung der Operation und gibt für das Schema nun das übergeordnete Attribut `meta:immutableTags` als Array mit dem Wert „union“ zurück.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.4",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673380280074,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:immutableTags": [
    "union"
  ],
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### Auflisten von Schemas in einer Vereinigung

Sie haben Ihr Schema jetzt erfolgreich zum [!DNL XDM Individual Profile] Vereinigung. Eine Liste aller dieser Vereinigung zugehörigen Schemas erhalten Sie mittels GET-Anfrage, in der Sie zum Filtern der Antwort entsprechende Abfrageparameter angeben.

Über den Abfrageparameter `property` können Sie bestimmen, dass nur Schemas zurückgegeben werden, die ein Feld `meta:immutableTags` beinhalten, dessen Wert `meta:class` mit der `$id` der Klasse „“ übereinstimmt.[!DNL XDM Individual Profile]

**API-Format**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

**Anfrage**

Die folgende Beispielanfrage gibt alle Schemas zurück, die Teil der [!DNL XDM Individual Profile] Vereinigung.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort liefert eine gefilterte Liste all jener Schemas, die beide Bedingungen erfüllen. Beachten Sie, dass bei Abfragen mit mehreren Parametern eine UND-Beziehung impliziert wird. Das Format der Listenantwort hängt von der `Accept` -Kopfzeile, die in der Anfrage gesendet wird.

```JSON
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d29a200b5deb6cfb55d3b865ef627f33",
      "meta:altId": "_{TENANT_ID}.schemas.d29a200b5deb6cfb55d3b865ef627f33",
      "version": "1.2",
      "title": "Profile Schema"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/5d70026f5522fc60b3c81f6523b83c86",
      "meta:altId": "_{TENANT_ID}.schemas.5d70026f5522fc60b3c81f6523b83c86",
      "version": "1.3",
      "title": "CRM Onboarding"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
      "meta:altId": "_{TENANT_ID}.schemas.653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
      "version": "1.1",
      "title": "Profile consents"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
      "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
      "version": "1.4",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
    "orderby": "updated",
    "next": null,
    "count": 4
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
    }
  }
}
```

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich ein Schema erstellt, das sowohl Standardfeldgruppen als auch eine von Ihnen definierte Feldergruppe enthält. Dieses Schema können Sie verwenden, um einen Datensatz zu erstellen und Datensatzdaten in Adobe Experience Platform aufzunehmen.

Das im Rahmen dieses Tutorials erstellte „Loyalty Members“-Schema steht in seiner vollständigen Form im nachfolgenden Anhang zur Verfügung. Beim Betrachten des Schemas können Sie sehen, wie die Feldergruppen zur Gesamtstruktur beitragen und welche Felder für die Datenerfassung verfügbar sind.

Wenn Sie weitere Schemas erstellen, können Sie mithilfe von Beziehungsdeskriptoren Beziehungen zwischen ihnen definieren. Weitere Informationen hierzu finden Sie im Tutorial zum Thema [Definieren einer Beziehung zwischen zwei Schemas](relationship-api.md). Ausführliche Beispiele dazu, wie Sie alle weiteren für die Arbeit mit der Schema Registry-API verfügbaren Operationen (GET, POST, PUT, PATCH und DELETE) ausführen, finden Sie im [Schema Registry-Entwicklerhandbuch](../api/getting-started.md).

## Anhang {#appendix}

Die nachfolgenden Informationen dienen als Ergänzung zum API-Tutorial.

## Vollständiges „Loyalty Members“-Schema {#complete-schema}

Im Rahmen dieses Tutorials wird ein Schema zur Beschreibung der Mitglieder eines Treueprogramms im Einzelhandel erstellt.

Das Schema implementiert die [!DNL XDM Individual Profile] und kombiniert mehrere Feldergruppen. Es erfasst Informationen über die Mitglieder des Treueprogramms mithilfe des Standardsatzes [!DNL Demographic Details], [!UICONTROL Persönliche Kontaktangaben]und [!UICONTROL Treuedetails] Feldergruppen sowie über eine benutzerdefinierte Feldergruppe &quot;Treuestufe&quot;, die während des Tutorials definiert wird.

Nachfolgend ist das „Loyalty Members“-Schema in seiner abschließenden Form im JSON-Format dargestellt:

+++ Gesamtes Schema anzeigen

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.4",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyTier": {
          "title": "Loyalty Tier",
          "description": "Loyalty tier info",
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "id": {
              "title": "Loyalty Tier Identifier",
              "type": "string",
              "description": "Loyalty Tier Identifier.",
              "meta:xdmType": "string"
            },
            "effectiveDate": {
              "title": "Effective Date",
              "type": "string",
              "format": "date-time",
              "description": "Date the member joined their current loyalty tier.",
              "meta:xdmType": "date-time"
            },
            "currentThreshold": {
              "title": "Current Point Threshold",
              "type": "integer",
              "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
              "meta:xdmType": "int"
            },
            "nextThreshold": {
              "title": "Next Point Threshold",
              "type": "integer",
              "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
              "meta:xdmType": "int"
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
        }
      },
      "meta:xdmType": "object"
    },
    "_id": {
      "title": "Identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "A unique identifier for the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "@id"
    },
    "_repo": {
      "properties": {
        "createDate": {
          "type": "string",
          "format": "date-time",
          "meta:immutable": true,
          "meta:usereditable": false,
          "examples": [
            "2004-10-23T12:00:00-06:00"
          ],
          "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
          "meta:xdmType": "date-time",
          "meta:xdmField": "repo:createDate"
        },
        "modifyDate": {
          "type": "string",
          "format": "date-time",
          "meta:usereditable": false,
          "examples": [
            "2004-10-23T12:00:00-06:00"
          ],
          "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
          "meta:xdmType": "date-time",
          "meta:xdmField": "repo:modifyDate"
        }
      },
      "type": "object",
      "meta:xdmType": "object",
      "meta:xedConverted": true
    },
    "billingAddress": {
      "title": "Billing Address",
      "description": "Billing postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:billingAddress"
    },
    "createdByBatchID": {
      "title": "Created by batch identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "The dataset files in Catalog which has been originating the creation of the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:createdByBatchID"
    },
    "faxPhone": {
      "title": "Fax Phone",
      "description": "Fax phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the phone number.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:faxPhone"
    },
    "homeAddress": {
      "title": "Home Address",
      "description": "A home postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:homeAddress"
    },
    "homePhone": {
      "title": "Home Phone",
      "description": "Home phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the phone number.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:homePhone"
    },
    "loyalty": {
      "type": "object",
      "description": "Captures details related to the customer's loyalty rewards.",
      "properties": {
        "joinDate": {
          "title": "Program Join Date",
          "type": "string",
          "format": "date-time",
          "description": "Date which the visitor registered for the loyalty program.",
          "meta:xdmType": "date-time",
          "meta:xdmField": "xdm:joinDate"
        },
        "loyaltyID": {
          "title": "Program ID",
          "type": "array",
          "items": {
            "type": "string",
            "meta:xdmType": "string"
          },
          "description": "The loyalty program ID(s) associated with a specific user, if they are enrolled in the client's loyalty program.",
          "meta:xdmType": "array",
          "meta:xdmField": "xdm:loyaltyID"
        },
        "points": {
          "title": "Program Points Balance",
          "type": "number",
          "description": "Current balance of the loyalty points/awards in a visitor's loyalty account.",
          "meta:xdmType": "number",
          "meta:xdmField": "xdm:points"
        },
        "pointsExpiration": {
          "title": "Points Expiration",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "pointsExpirationDate": {
                "type": "string",
                "format": "date-time",
                "description": "Date on which the given portion of the loyalty points expire.",
                "meta:xdmType": "date-time",
                "meta:xdmField": "xdm:pointsExpirationDate"
              },
              "pointsExpiring": {
                "title": "Points Expiring",
                "type": "number",
                "description": "Point balance expiring as of the associated expiration date.",
                "meta:xdmType": "number",
                "meta:xdmField": "xdm:pointsExpiring"
              }
            },
            "meta:xdmType": "object"
          },
          "meta:xdmType": "array",
          "meta:xdmField": "xdm:pointsExpiration"
        },
        "pointsRedeemed": {
          "title": "Points Redeemed",
          "type": "number",
          "description": "Amount of points applied toward a purchase or otherwise redeemed.",
          "meta:xdmType": "number",
          "meta:xdmField": "xdm:pointsRedeemed"
        },
        "program": {
          "title": "Program Name",
          "type": "string",
          "description": "This should define the loyalty progam in which a visitor is enrolled.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:program"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "Captures the visitor's loyalty progam status, such as active, disabled, or suspended.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "tier": {
          "title": "Tier",
          "type": "string",
          "description": "Captures the loyalty progam tier in which a visitor is enrolled.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:tier"
        },
        "upgradeDate": {
          "title": "Program Name",
          "type": "string",
          "description": "Date which the customer was upgraded to the next tier level.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:upgradeDate"
        }
      },
      "meta:xdmType": "object",
      "meta:xdmField": "xdm:loyalty"
    },
    "mailingAddress": {
      "title": "Mailing Address",
      "description": "Mailing postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:mailingAddress"
    },
    "mobilePhone": {
      "title": "Mobile Phone",
      "description": "Mobile phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the phone number.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:mobilePhone"
    },
    "modifiedByBatchID": {
      "title": "Modified by batch identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:modifiedByBatchID"
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "birthDate": {
          "title": "Birth date(YYYY-MM-DD)",
          "type": "string",
          "format": "date",
          "description": "The full date a person was born.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:birthDate"
        },
        "birthDayAndMonth": {
          "title": "Birth date (MM-DD)",
          "type": "string",
          "pattern": "[0-1][0-9]-[0-9][0-9]",
          "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:birthDayAndMonth"
        },
        "birthYear": {
          "title": "Birth year",
          "type": "integer",
          "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date.",
          "minimum": 1,
          "maximum": 32767,
          "meta:xdmType": "short",
          "meta:xdmField": "xdm:birthYear"
        },
        "gender": {
          "title": "Gender",
          "type": "string",
          "enum": [
            "male",
            "female",
            "not_specified",
            "non_specific"
          ],
          "meta:enum": {
            "male": "Male",
            "female": "Female",
            "not_specified": "Not Specified",
            "non_specific": "Non-specific"
          },
          "description": "Gender identity of the person.\n",
          "default": "not_specified",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:gender"
        },
        "maritalStatus": {
          "title": "Marital Status",
          "type": "string",
          "enum": [
            "married",
            "single",
            "divorced",
            "widowed",
            "not_specified"
          ],
          "meta:enum": {
            "married": "Married",
            "single": "Single",
            "divorced": "Divorced",
            "widowed": "Widowed",
            "not_specified": "Not Specified"
          },
          "description": "Describes a person's relationship with a significant other.",
          "default": "not_specified",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:maritalStatus"
        },
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "courtesyTitle": {
              "title": "Courtesy title",
              "type": "string",
              "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:courtesyTitle"
            },
            "firstName": {
              "title": "First name",
              "type": "string",
              "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:firstName"
            },
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:fullName"
            },
            "lastName": {
              "title": "Last name",
              "type": "string",
              "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:lastName"
            },
            "middleName": {
              "title": "Middle name",
              "type": "string",
              "description": "Middle, alternative, or additional names supplied between the first name and last name.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:middleName"
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:suffix"
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        },
        "nationality": {
          "title": "Nationality",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:nationality"
        },
        "taxId": {
          "title": "Tax ID",
          "type": "string",
          "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
          "meta:status": "deprecated",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:taxId"
        },
        "type": {
          "title": "Type",
          "type": "string",
          "description": "The type of individual in different business contexts like B2C.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:type"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
      "meta:xdmField": "xdm:person"
    },
    "personID": {
      "title": "Person ID",
      "description": "Unique identifier of Person/Profile fragment.",
      "type": "string",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:personID"
    },
    "personalEmail": {
      "title": "Personal Email",
      "description": "A personal email address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "address": {
          "title": "Address",
          "type": "string",
          "format": "email",
          "description": "The technical address, for example, 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:address",
          "minLength": 1
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Additional display information that maybe available, for example, Microsoft Outlook rich address controls display 'John Smith smithjr@company.uk', 'John Smith' part is data that would be placed in the label.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary email indicator. A profile can have only one `primary` email address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the email address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "type": {
          "title": "Type",
          "type": "string",
          "description": "The way the account relates to the person for example 'work' or 'personal'.",
          "meta:enum": {
            "unknown": "Unknown",
            "personal": "Personal",
            "work": "Work",
            "education": "Education"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:type"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
      "meta:xdmField": "xdm:personalEmail",
      "required": [
        "address"
      ]
    },
    "repositoryCreatedBy": {
      "title": "Created by user identifier",
      "type": "string",
      "description": "User ID of who created the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:repositoryCreatedBy"
    },
    "repositoryLastModifiedBy": {
      "title": "Modified by user identifier",
      "type": "string",
      "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:repositoryLastModifiedBy"
    },
    "shippingAddress": {
      "title": "Shipping Address",
      "description": "Shipping postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:shippingAddress"
    }
  },
  "required": [
    "personalEmail"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673380280074,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:immutableTags": [
    "union"
  ],
  "meta:allFieldAccess": true
}
```

+++
