---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Erste Schritte mit der Schema Registry API
description: In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie die Schema-Registrierungs-API aufrufen.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 49%

---


# Getting started with the [!DNL Schema Registry] API

Mit der [!DNL Schema Registry] API können Sie verschiedene XDM-Ressourcen (Experience Data Model) erstellen und verwalten. This document provides an introduction to the core concepts you need to know before attempting to make calls to the [!DNL Schema Registry] API.

## Voraussetzungen 

Die Verwendung des Entwicklerhandbuchs erfordert ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemata.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

XDM verwendet JSON-Schema-Formatierung, um die Struktur der erfassten Kundenerlebnisdaten zu beschreiben und zu validieren. Es wird daher dringend empfohlen, die [offizielle JSON-Schema-Dokumentation](https://json-schema.org/) zu überprüfen, um ein besseres Verständnis dieser zugrunde liegenden Technologie zu erhalten.

## Lesen von Beispiel-API-Aufrufen

The [!DNL Schema Registry] API documentation provides example API calls to demonstrate how to format your requests. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Schema Registry], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox documentation](../../sandboxes/home.md).

All lookup (GET) requests to the [!DNL Schema Registry] require an additional `Accept` header, whose value determines the format of information returned by the API. Weitere Informationen finden Sie unten im Abschnitt [Accept-Kopfzeile](#accept).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

## Ihre TENANT_ID {#know-your-tenant_id}

In den API-Handbüchern finden Sie Verweise auf eine `TENANT_ID`. Diese Kennung stellt sicher, dass die von Ihnen erstellten Ressourcen den richtigen Namespace aufweisen und in Ihrer IMS-Organisation enthalten sind. Wenn Sie Ihre ID nicht kennen, können Sie sie mit der folgenden GET-Anfrage abrufen:

**API-Format**

```http
GET /stats
```

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

A successful response returns information regarding your organization&#39;s use of the [!DNL Schema Registry]. Dies beinhaltet ein `tenantId`-Attribut, dessen Wert Ihre `TENANT_ID` ist.

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## Die `CONTAINER_ID` {#container}

Calls to the [!DNL Schema Registry] API require the use of a `CONTAINER_ID`. There are two containers against which API calls can be made: the `global` container and the `tenant` container.

### Globaler Container

The `global` container holds all standard Adobe and [!DNL Experience Platform] partner provided classes, mixins, data types, and schemas. You may only perform list and lookup (GET) requests against the `global` container.

Ein Beispiel für einen Aufruf, der den `global` Container verwendet, würde wie folgt aussehen:

```http
GET /global/classes
```

### Mandanten-Container

Not to be confused with your unique `TENANT_ID`, the `tenant` container holds all classes, mixins, data types, schemas, and descriptors defined by an IMS Organization. Sie sind für jede Organisation eindeutig, d h. sie sind für andere IMS-Organisationen nicht sichtbar oder verwaltbar. You may perform all CRUD operations (GET, POST, PUT, PATCH, DELETE) against resources that you create in the `tenant` container.

Ein Beispiel für einen Aufruf, der den `tenant` Container verwendet, würde wie folgt aussehen:

```http
POST /tenant/mixins
```

When you create a class, mixin, schema or data type in the `tenant` container, it is saved to the [!DNL Schema Registry] and assigned an `$id` URI that includes your `TENANT_ID`. Diese `$id` wird in der gesamten API verwendet, um auf bestimmte Ressourcen zu verweisen. Beispiele für Werte der `$id` finden Sie im nächsten Abschnitt.

## Ressourcenidentifizierung {#resource-identification}

XDM-Ressourcen werden mit einem `$id` Attribut in Form eines URI identifiziert, wie z. B. die folgenden Beispiele:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Um den URI REST-freundlicher zu gestalten, verfügen Schemata auch über eine Punktnotationskodierung des URI in einer Eigenschaft mit der Bezeichnung `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Calls to the [!DNL Schema Registry] API will support either the URL-encoded `$id` URI or the `meta:altId` (dot-notation format). Es empfiehlt sich, den URL-kodierten `$id`-URI zu verwenden, wenn Sie einen REST-Aufruf an die API ausführen, wie z. B.:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accept-Kopfzeile {#accept}

When performing list and lookup (GET) operations in the [!DNL Schema Registry] API, an `Accept` header is required to determine the format of the data returned by the API. When looking up specific resources, a version number must also be included in the `Accept` header.

The following table lists compatible `Accept` header values, including those with version numbers, along with descriptions of what the API will return when they are used.

| Accept | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Gibt nur eine Liste von IDs zurück. Dies wird am häufigsten für die Auflistung von Ressourcen verwendet. |
| `application/vnd.adobe.xed+json` | Gibt eine Liste des vollständigen JSON-Schemata einschließlich der ursprünglichen `$ref` und `allOf` zurück. Damit wird eine Liste der vollständigen Ressourcen zurückgegeben. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw-XDM mit `$ref` und `allOf`. Beinhaltet Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref`-Attribute und `allOf` aufgelöst. Beinhaltet Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw-XDM mit `$ref` und `allOf`. Keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref`-Attribute und `allOf` aufgelöst. Keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref`-Attribute und `allOf` aufgelöst. Deskriptoren sind enthalten. |

>[!NOTE]
>
>Wenn Sie nur die Hauptversion (z.B. 1, 2, 3) angeben, gibt die Registrierung die neueste Nebenversion (z.B. .1, .2, .3) automatisch.

## XDM-Feldbeschränkungen und Best Practices

Die Felder eines Schemas werden innerhalb seines `properties`-Objekts aufgelistet. Jedes Feld ist selbst ein Objekt, das Attribute zur Beschreibung und Beschränkung der Daten enthält, die das Feld enthalten kann.

Weitere Informationen zum Definieren von Feldtypen in der API finden Sie im [Anhang](appendix.md) zu diesem Handbuch, einschließlich Codebeispielen und optionale Beschränkungen für die am häufigsten verwendeten Datentypen.

Das folgende Beispielfeld veranschaulicht ein korrekt formatiertes XDM-Feld, wobei weitere Einzelheiten zu den Benennungsbeschränkungen und Best Practices weiter unten aufgeführt sind. Diese Verfahren können auch bei der Definition anderer Ressourcen angewendet werden, die ähnliche Attribute enthalten.

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* Der Name eines Feldobjekts kann alphanumerische Zeichen, Bindestriche oder Unterstriche enthalten, darf jedoch **nicht** mit einem Unterstrich beginnen.
   * **Richtig:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Falsch:** `_fieldName`
* Die CamelCase-Notation (gemischte Groß-/Kleinschreibung) wird für den Namen des Feldobjekts bevorzugt. Beispiel: `fieldName`
* Das Feld sollte einen `title` in Titelschrift-Notation (erster Buchstabe groß) enthalten. Beispiel: `Field Name`
* Für das Feld ist ein `type` erforderlich.
   * Die Definition bestimmter Typen erfordert möglicherweise ein optionales `format`.
   * Wenn eine bestimmte Formatierung der Daten erforderlich ist, kann `examples` als Array hinzugefügt werden.
   * Der Feldtyp kann auch mit einem beliebigen Datentyp in der Registry definiert werden. See the section on [creating a data type](./data-types.md#create) in the data types endpoint guide for more information.
* In `description` wird das Feld und relevante Informationen zu den Felddaten erklärt. Dies sollte in vollständigen Sätzen mit klarer Sprache geschrieben sein, damit jeder, der auf das Schema zugreift, die Absicht des Feldes verstehen kann.

Weitere Informationen zum Definieren verschiedener Feldtypen in der API finden Sie im Dokument zu [Feldbeschränkungen](../schema/field-constraints.md) .

## Nächste Schritte

Um mit dem Aufrufen der [!DNL Schema Registry] API zu beginnen, wählen Sie eine der verfügbaren Endpunktleitfäden aus.
