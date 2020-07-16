---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch zur Schema Registry-API
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 72%

---


# [!DNL Schema Registry] API-Entwicklerleitfaden

The [!DNL Schema Registry] is used to access the Schema Library within Adobe Experience Platform, providing a user interface and RESTful API from which all available library resources are accessible.

Mithilfe der Schema Registry-API können Sie grundlegende CRUD-Vorgänge ausführen, um alle Schemata und zugehörigen Ressourcen anzuzeigen und zu verwalten, die Ihnen in der Adobe Experience Platform zur Verfügung stehen. This includes those defined by Adobe, [!DNL Experience Platform] partners, and vendors whose applications you use. Sie können API-Aufrufe auch verwenden, um neue Schemata und Ressourcen für Ihre Organisation zu erstellen sowie bereits definierte Ressourcen anzuzeigen und zu bearbeiten.

This developer guide provides steps to help you start using the [!DNL Schema Registry] API. Das Handbuch enthält Beispiel-API-Aufrufe für die Ausführung wichtiger Vorgänge mithilfe von [!DNL Schema Registry].

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [!DNL Experience Data Model (XDM) System](../home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemata.
* [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Schema Registry] API.

## Lesehilfe für Beispiel-API-Aufrufe

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

## Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Schema Registry], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

All lookup (GET) requests to the [!DNL Schema Registry] require an additional Accept header, whose value determines the format of information returned by the API. Weitere Informationen finden Sie unten im Abschnitt [Accept-Kopfzeile](#accept).

Für alle Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* Inhaltstyp: application/json

## Ihre TENANT_ID {#know-your-tenant_id}

In diesem Handbuch finden Sie Verweise auf eine `TENANT_ID`. Diese ID wird verwendet, um sicherzustellen, dass die von Ihnen erstellten Ressourcen den richtigen Namespace haben und in Ihrer IMS-Organisation enthalten sind. Wenn Sie Ihre ID nicht kennen, können Sie sie mit der folgenden GET-Anfrage abrufen:

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

* `tenantId`: Der `TENANT_ID`-Wert für Ihre IMS-Organisation.

## Die `CONTAINER_ID` {#container}

Calls to the [!DNL Schema Registry] API require the use of a `CONTAINER_ID`. Es gibt zwei Container, für die API-Aufrufe durchgeführt werden können: der **globale Container** und der **Mandanten-Container**.

### Globaler Container

The global container holds all standard Adobe and [!DNL Experience Platform] partner provided classes, mixins, data types, and schemas. Sie dürfen nur Listen- und Suchanfragen (GET) für den globalen Container ausführen.

### Mandanten-Container

Nicht zu verwechseln mit Ihrer eindeutigen `TENANT_ID`, enthält der Mandanten-Container alle Klassen, Mixins, Datentypen, Schemata und Deskriptoren, die von einer IMS-Organisation definiert wurden. Sie sind für jede Organisation eindeutig, d h. sie sind für andere IMS-Organisationen nicht sichtbar oder verwaltbar. Sie können alle CRUD-Vorgänge (GET, POST, PUT, PATCH, DELETE) für die Ressourcen ausführen, die Sie im Mandanten-Container erstellen.

When you create a class, mixin, schema or data type in the tenant container, it is saved to the [!DNL Schema Registry] and assigned an `$id` URI that includes your `TENANT_ID`. Diese `$id` wird in der gesamten API verwendet, um auf bestimmte Ressourcen zu verweisen. Beispiele für Werte der `$id` finden Sie im nächsten Abschnitt.

## Schema-Identifizierung {#schema-identification}

Schemata werden mit einem `$id`-Attribut in Form eines URI identifiziert, z. B.:
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Um den URI REST-freundlicher zu gestalten, verfügen Schemata auch über eine Punktnotationskodierung des URI in einer Eigenschaft mit der Bezeichnung `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Aufrufe der Schema Registry-API unterstützen entweder den URL-kodierten `$id`-URI oder die `meta:altId` (Punktnotationsformat). Es empfiehlt sich, den URL-kodierten `$id`-URI zu verwenden, wenn Sie einen REST-Aufruf an die API ausführen, wie z. B.:
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accept-Kopfzeile {#accept}

When performing list and lookup (GET) operations in the [!DNL Schema Registry] API, an Accept header is required to determine the format of the data returned by the API. Bei der Suche nach bestimmten Ressourcen muss auch eine Versionsnummer in der Accept-Kopfzeile enthalten sein.

In der folgenden Tabelle sind kompatible Accept-Kopfzeilenwerte aufgeführt, einschließlich solcher mit Versionsnummern, sowie Beschreibungen dessen, was die API zurückgibt, wenn sie verwendet werden.

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
>Wenn Sie nur die `major`-Version (z. B. 1, 2, 3) angeben, gibt die Registry automatisch die neueste `minor`-Version (z. B. .1, .2, .3) zurück.

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
   * Der Feldtyp kann auch mit einem beliebigen Datentyp in der Registry definiert werden. Weitere Informationen finden Sie im Abschnitt zum [Erstellen eines Datentyps](create-data-type.md) in diesem Handbuch.
* In `description` wird das Feld und relevante Informationen zu den Felddaten erklärt. Dies sollte in vollständigen Sätzen mit klarer Sprache geschrieben sein, damit jeder, der auf das Schema zugreift, die Absicht des Feldes verstehen kann.

Weitere Informationen zum Definieren von Feldtypen in der API finden Sie im [Anhang](appendix.md).

## Nächste Schritte

This document covered the prerequisite knowledge required to make calls to the [!DNL Schema Registry] API, including required authentication credentials. Sie können nun mit den in diesem Entwicklerhandbuch enthaltenen Beispielaufrufen fortfahren und deren Anweisungen befolgen. Ausführliche schrittweise Anweisungen zum Erstellen eines Schemas in der API finden Sie im folgenden [Tutorial](../tutorials/create-schema-api.md).
