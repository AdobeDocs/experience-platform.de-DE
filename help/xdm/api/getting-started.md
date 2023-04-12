---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schemaregistrierung; Schema Registry;
solution: Experience Platform
title: Erste Schritte mit der Schema Registry-API
description: Dieses Dokument bietet eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die Schema Registry-API durchführen.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 45%

---

# Erste Schritte mit der [!DNL Schema Registry]-API

Die [!DNL Schema Registry] Mit der API können Sie verschiedene XDM-Ressourcen (Experience-Datenmodell) erstellen und verwalten. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die [!DNL Schema Registry]-API durchführen.

## Voraussetzungen

Die Verwendung des Entwicklerhandbuchs setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemas.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

XDM verwendet die JSON-Schema-Formatierung, um die Struktur der erfassten Kundenerlebnisdaten zu beschreiben und zu validieren. Es wird daher dringend empfohlen, die [offizielle JSON-Schema-Dokumentation](https://json-schema.org/) für ein besseres Verständnis dieser zugrunde liegenden Technologie.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation der [!DNL Schema Registry]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die [!DNL Schema Registry], werden auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes finden Sie unter [!DNL Platform], siehe [Sandbox-Dokumentation](../../sandboxes/home.md).

Alle Nachschlageanfragen (GET) an die [!DNL Schema Registry] zusätzliche `Accept` -Kopfzeile, deren Wert das Format der von der API zurückgegebenen Informationen bestimmt. Weitere Informationen finden Sie unten im Abschnitt [Accept-Kopfzeile](#accept).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

## Ihre TENANT_ID {#know-your-tenant_id}

In den API-Handbüchern finden Sie Verweise auf eine `TENANT_ID`. Diese ID wird verwendet, um sicherzustellen, dass von Ihnen erstellte Ressourcen ordnungsgemäß benannt werden und in Ihrem Unternehmen enthalten sind. Wenn Sie Ihre ID nicht kennen, können Sie sie mit der folgenden GET-Anfrage abrufen:

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden Informationen zur Verwendung der Variablen [!DNL Schema Registry]. Dies beinhaltet ein `tenantId`-Attribut, dessen Wert Ihre `TENANT_ID` ist.

```JSON
{
  "imsOrg":"{ORG_ID}",
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
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
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
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
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

Aufrufe an die [!DNL Schema Registry] API erfordert die Verwendung einer `CONTAINER_ID`. Es gibt zwei Container, für die API-Aufrufe durchgeführt werden können: die `global` und `tenant` Container.

### Globaler Container

Die `global` Container enthält alle standardmäßigen Adoben und [!DNL Experience Platform] vom Partner bereitgestellte Klassen, Schemafeldgruppen, Datentypen und Schemas. Sie dürfen nur Listen- und Suchanfragen (GET) für die `global` Container.

Ein Beispiel für einen Aufruf, bei dem die `global` -Container würde wie folgt aussehen:

```http
GET /global/classes
```

### Mandanten-Container

Nicht zu verwechseln mit Ihrer eindeutigen `TENANT_ID`, die `tenant` -Container enthält alle Klassen, Feldergruppen, Datentypen, Schemata und Deskriptoren, die von einer Organisation definiert werden. Diese sind für jede Organisation eindeutig, d. h. sie sind für andere Organisationen nicht sichtbar oder verwaltbar. Sie können alle CRUD-Vorgänge (GET, POST, PUT, PATCH, DELETE) für Ressourcen ausführen, die Sie in der `tenant` Container.

Ein Beispiel für einen Aufruf, bei dem die `tenant` -Container würde wie folgt aussehen:

```http
POST /tenant/fieldgroups
```

Wenn Sie eine Klasse, Feldergruppe, ein Schema oder einen Datentyp in der `tenant` Behälter, wird er im [!DNL Schema Registry] und eine `$id` -URI, der Ihre `TENANT_ID`. Diese `$id` wird in der gesamten API verwendet, um auf bestimmte Ressourcen zu verweisen. Beispiele für Werte der `$id` finden Sie im nächsten Abschnitt.

## Ressourcenidentifizierung {#resource-identification}

XDM-Ressourcen werden mit einer `$id` -Attribut in Form eines URI, z. B. die folgenden Beispiele:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Um den URI REST-freundlicher zu gestalten, verfügen Schemata auch über eine Punktnotationskodierung des URI in einer Eigenschaft mit der Bezeichnung `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Aufrufe an die [!DNL Schema Registry] Die API unterstützt entweder die URL-kodierte `$id` URI oder `meta:altId` (Punktnotationsformat). Es empfiehlt sich, den URL-kodierten `$id`-URI zu verwenden, wenn Sie einen REST-Aufruf an die API ausführen, wie z. B.:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accept-Kopfzeile {#accept}

Bei der Ausführung von Listen- und Nachschlagevorgängen (GET) im [!DNL Schema Registry] API, eine `Accept` -Kopfzeile ist erforderlich, um das Format der von der API zurückgegebenen Daten zu bestimmen. Bei der Suche nach bestimmten Ressourcen muss auch eine Versionsnummer in die `Accept` -Kopfzeile.

In der folgenden Tabelle sind die kompatiblen `Accept` -Kopfzeilenwerte, einschließlich solcher mit Versionsnummern, zusammen mit Beschreibungen dessen, was die API zurückgibt, wenn sie verwendet werden.

| Accept | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Gibt nur eine Liste von IDs zurück. Dies wird am häufigsten für die Auflistung von Ressourcen verwendet. |
| `application/vnd.adobe.xed+json` | Gibt eine Liste des vollständigen JSON-Schemata einschließlich der ursprünglichen `$ref` und `allOf` zurück. Damit wird eine Liste der vollständigen Ressourcen zurückgegeben. |
| `application/vnd.adobe.xed+json; version=1` | Raw-XDM mit `$ref` und `allOf`. Beinhaltet Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref`-Attribute und `allOf` aufgelöst. Beinhaltet Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw-XDM mit `$ref` und `allOf`. Keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref`-Attribute und `allOf` aufgelöst. Keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref`-Attribute und `allOf` aufgelöst. Deskriptoren sind enthalten. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` und `allOf` aufgelöst, verfügt über Titel und Beschreibungen. Veraltete Felder werden mit einem `meta:status` Attribut `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Platform unterstützt derzeit nur eine Hauptversion für jedes Schema (`1`). Daher wird der Wert für `version` muss immer `1` bei der Durchführung von Suchanfragen, um die neueste Nebenversion des Schemas zurückzugeben. Weitere Informationen zur Schemaversionierung finden Sie im Unterabschnitt unten.

### Schemaversionierung {#versioning}

Schemaversionen werden durch `Accept` Kopfzeilen in der Schema Registry-API und in `schemaRef.contentType` Eigenschaften in nachgelagerten Platform-Dienst-API-Payloads.

Derzeit unterstützt Platform nur eine einzige Hauptversion (`1`) für jedes Schema. Gemäß [Regeln der Schemaentwicklung](../schema/composition.md#evolution)muss jede Schemaaktualisierung zerstörungsfrei sein, d. h. neue Nebenversionen eines Schemas (`1.2`, `1.3`usw.) sind immer abwärtskompatibel mit früheren Nebenversionen. Wenn Sie daher `version=1`, gibt die Schema Registry immer die Variable **latest** Hauptversion `1` eines Schemas verwenden, d. h. frühere Nebenversionen werden nicht zurückgegeben.

>[!NOTE]
>
>Die zerstörungsfreie Anforderung für die Schemaentwicklung wird erst erzwungen, nachdem das Schema von einem Datensatz referenziert wurde und einer der folgenden Fälle wahr ist:
>
>* Daten wurden in den Datensatz aufgenommen.
>* Der Datensatz wurde für die Verwendung im Echtzeit-Kundenprofil aktiviert (auch wenn keine Daten erfasst wurden).
>
>Wenn das Schema keinem Datensatz zugeordnet wurde, der eines der oben genannten Kriterien erfüllt, kann es geändert werden. In jedem Fall wird jedoch die `version` Komponente bleibt erhalten `1`.

## XDM-Feldbeschränkungen und Best Practices

Die Felder eines Schemas werden innerhalb seines `properties`-Objekts aufgelistet. Jedes Feld ist selbst ein Objekt, das Attribute zur Beschreibung und Beschränkung der Daten enthält, die das Feld enthalten kann. Weitere Informationen finden Sie im Handbuch [Definieren benutzerdefinierter Felder in der API](../tutorials/custom-fields-api.md) für Codebeispiele und optionale Einschränkungen für die am häufigsten verwendeten Datentypen.

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
   * Der Feldtyp kann auch mit einem beliebigen Datentyp in der Registry definiert werden. Siehe Abschnitt zu [Erstellen eines Datentyps](./data-types.md#create) im Endpunktleitfaden zu Datentypen finden Sie weitere Informationen.
* In `description` wird das Feld und relevante Informationen zu den Felddaten erklärt. Dies sollte in vollständigen Sätzen mit klarer Sprache geschrieben sein, damit jeder, der auf das Schema zugreift, die Absicht des Feldes verstehen kann.

## Nächste Schritte

Um mit dem Aufrufen der [!DNL Schema Registry]-API zu beginnen, wählen Sie eines der verfügbaren Handbücher zu Endpunkten.
