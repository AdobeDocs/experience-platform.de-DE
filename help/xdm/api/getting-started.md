---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;
solution: Experience Platform
title: Erste Schritte mit der Schema Registry API
description: In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie die Schema-Registrierungs-API aufrufen.
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 39%

---

# Erste Schritte mit der API[!DNL Schema Registry]

Mit der [!DNL Schema Registry]-API können Sie verschiedene XDM-Ressourcen (Experience Data Model) erstellen und verwalten. Dieses Dokument bietet eine Einführung in die Kernkonzepte, die Sie kennen müssen, bevor Sie Aufrufe an die [!DNL Schema Registry]-API durchführen.

## Voraussetzungen

Die Verwendung des Entwicklerhandbuchs erfordert ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemas.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

XDM verwendet JSON-Schema-Formatierung, um die Struktur der erfassten Kundenerlebnisdaten zu beschreiben und zu validieren. Es wird daher dringend empfohlen, die [offizielle JSON-Schema-Dokumentation](https://json-schema.org/) zu überprüfen, um ein besseres Verständnis dieser zugrunde liegenden Technologie zu erhalten.

## Lesen von Beispiel-API-Aufrufen

Die [!DNL Schema Registry]-API-Dokumentation enthält Beispiel-API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Schema Registry] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Dokumentation](../../sandboxes/home.md).

Für alle Nachschlageanforderungen (GET) an die [!DNL Schema Registry] ist eine zusätzliche `Accept`-Kopfzeile erforderlich, deren Wert das Format der von der API zurückgegebenen Informationen bestimmt. Weitere Informationen finden Sie unten im Abschnitt [Accept-Kopfzeile](#accept).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

## Ihre TENANT_ID {#know-your-tenant_id}

In den API-Handbüchern werden Verweise auf ein `TENANT_ID` angezeigt. Diese Kennung stellt sicher, dass die von Ihnen erstellten Ressourcen den richtigen Namespace aufweisen und in Ihrer IMS-Organisation enthalten sind. Wenn Sie Ihre ID nicht kennen, können Sie sie mit der folgenden GET-Anfrage abrufen:

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

Eine erfolgreiche Antwort gibt Informationen zur Verwendung von [!DNL Schema Registry] in Ihrem Unternehmen zurück. Dies beinhaltet ein `tenantId`-Attribut, dessen Wert Ihre `TENANT_ID` ist.

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

Für Aufrufe der API [!DNL Schema Registry] ist die Verwendung eines `CONTAINER_ID` erforderlich. Es gibt zwei Container, für die API-Aufrufe durchgeführt werden können: den Container `global` und den Container `tenant`.

### Globaler Container

Der `global`-Container enthält alle Standardklassen und [!DNL Experience Platform] vom Partner bereitgestellte Adoben, Mixins, Datentypen und Schema. Sie können nur Liste- und Suchanfragen (GET) für den `global`-Container ausführen.

Ein Beispiel für einen Aufruf mit dem Container `global` würde wie folgt aussehen:

```http
GET /global/classes
```

### Mandanten-Container

Der `tenant`-Container enthält alle Klassen, Mixins, Datentypen, Schema und Deskriptoren, die von einer IMS-Organisation definiert werden. `TENANT_ID` Sie sind für jede Organisation eindeutig, d h. sie sind für andere IMS-Organisationen nicht sichtbar oder verwaltbar. Sie können alle CRUD-Vorgänge (GET, POST, PUT, PATCH, DELETE) für Ressourcen ausführen, die Sie im Container `tenant` erstellen.

Ein Beispiel für einen Aufruf mit dem Container `tenant` würde wie folgt aussehen:

```http
POST /tenant/mixins
```

Wenn Sie eine Klasse, ein Mixin, ein Schema oder einen Datentyp im Container `tenant` erstellen, wird diese im Ordner [!DNL Schema Registry] gespeichert und eine `$id` URI zugewiesen, die Ihre `TENANT_ID` enthält. Diese `$id` wird in der gesamten API verwendet, um auf bestimmte Ressourcen zu verweisen. Beispiele für Werte der `$id` finden Sie im nächsten Abschnitt.

## Ressourcen-ID {#resource-identification}

XDM-Ressourcen werden mit einem `$id`-Attribut in Form eines URI identifiziert, z. B. die folgenden Beispiele:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Um den URI REST-freundlicher zu gestalten, verfügen Schemata auch über eine Punktnotationskodierung des URI in einer Eigenschaft mit der Bezeichnung `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Durch Aufrufe der API [!DNL Schema Registry] wird entweder der URL-kodierte `$id`-URI oder das `meta:altId`-Format (Punkt-Notation) unterstützt. Es empfiehlt sich, den URL-kodierten `$id`-URI zu verwenden, wenn Sie einen REST-Aufruf an die API ausführen, wie z. B.:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accept-Kopfzeile {#accept}

Bei Liste- und Lookup-Vorgängen in der API [!DNL Schema Registry] ist ein `Accept`-Header erforderlich, um das Format der von der API zurückgegebenen Daten zu bestimmen. Wenn Sie nach bestimmten Ressourcen suchen, muss eine Versionsnummer auch in der `Accept`-Kopfzeile enthalten sein.

Die folgenden tabellarischen Listen sind mit `Accept`-Header-Werten kompatibel, einschließlich solcher mit Versionsnummern, zusammen mit Beschreibungen, was die API bei der Verwendung zurückgibt.

| Accept | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Gibt nur eine Liste von IDs zurück. Dies wird am häufigsten für die Auflistung von Ressourcen verwendet. |
| `application/vnd.adobe.xed+json` | Gibt eine Liste des vollständigen JSON-Schemata einschließlich der ursprünglichen `$ref` und `allOf` zurück. Damit wird eine Liste der vollständigen Ressourcen zurückgegeben. |
| `application/vnd.adobe.xed+json; version=1` | Raw-XDM mit `$ref` und `allOf`. Beinhaltet Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref`-Attribute und `allOf` aufgelöst. Beinhaltet Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw-XDM mit `$ref` und `allOf`. Keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref`-Attribute und `allOf` aufgelöst. Keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref`-Attribute und `allOf` aufgelöst. Deskriptoren sind enthalten. |

>[!NOTE]
>
>Plattform unterstützt derzeit nur eine Hauptversion für jedes Schema (`1`). Daher muss der Wert für `version` immer `1` sein, wenn Suchanfragen ausgeführt werden, damit die neueste Nebenversion des Schemas zurückgegeben wird. Weitere Informationen zur Schema-Versionierung finden Sie im Unterabschnitt unten.

### Schema-Versionierung {#versioning}

Schema-Versionen werden von `Accept`-Headern in der Schema Registry-API und in den `schemaRef.contentType`-Eigenschaften in den nachgelagerten Platform-Dienst-API-Nutzdaten referenziert.

Derzeit unterstützt Platform nur eine Hauptversion (`1`) für jedes Schema. Gemäß den [Regeln der Schema-Evolution](../schema/composition.md#evolution) muss jede Aktualisierung auf ein Schema nicht destruktiv sein, d. h., neue Nebenversionen eines Schemas (`1.2`, `1.3` usw.) sind immer abwärtskompatibel zu früheren Nebenversionen. Bei Angabe von `version=1` gibt die Schema-Registrierung daher immer die **neueste** Hauptversion `1` eines Schemas zurück, d. h., frühere Nebenversionen werden nicht zurückgegeben.

>[!NOTE]
>
>Die nicht destruktive Anforderung der Schema-Evolution wird erst erzwungen, nachdem das Schema von einem Datensatz referenziert wurde und einer der folgenden Fälle zutrifft:
>
>* Daten wurden in den Datensatz aufgenommen.
>* Der Datensatz wurde für die Verwendung im Echtzeit-Kundendaten-Profil aktiviert (auch wenn keine Daten erfasst wurden).

>
>
Wenn das Schema nicht mit einem Datensatz verknüpft wurde, der eines der oben genannten Kriterien erfüllt, können Änderungen daran vorgenommen werden. In allen Fällen bleibt die `version`-Komponente jedoch weiterhin bei `1`.

## XDM-Feldbeschränkungen und Best Practices

Die Felder eines Schemas werden innerhalb seines `properties`-Objekts aufgelistet. Jedes Feld ist selbst ein Objekt, das Attribute zur Beschreibung und Beschränkung der Daten enthält, die das Feld enthalten kann.

Weitere Informationen zum Definieren von Feldtypen in der API finden Sie im Handbuch [Feldbeschränkungen](../schema/field-constraints.md) für dieses Handbuch, einschließlich Codebeispiele und optionale Einschränkungen für die am häufigsten verwendeten Datentypen.

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
   * Der Feldtyp kann auch mit einem beliebigen Datentyp in der Registry definiert werden. Weitere Informationen finden Sie im Abschnitt [Erstellen eines Datentyps](./data-types.md#create) im Datentypen-Endpunkthandbuch.
* In `description` wird das Feld und relevante Informationen zu den Felddaten erklärt. Dies sollte in vollständigen Sätzen mit klarer Sprache geschrieben sein, damit jeder, der auf das Schema zugreift, die Absicht des Feldes verstehen kann.

Weitere Informationen zum Definieren verschiedener Feldtypen in der API finden Sie im Dokument zu [Feldbeschränkungen](../schema/field-constraints.md).

## Nächste Schritte

Um mit dem Aufrufen der API zu beginnen, wählen Sie eine der verfügbaren Endpunktleitfäden aus.[!DNL Schema Registry]
