---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch zur Schema Registry API
topic: developer guide
translation-type: tm+mt
source-git-commit: 387cbdebccb9ae54a2907d1afe220e9711927ca6
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---


# Entwicklerhandbuch zur Schema Registry API

Die Schema-Registrierung wird verwendet, um auf die Schema-Bibliothek in Adobe Experience Platform zuzugreifen und eine Benutzeroberfläche und RESTful-API bereitzustellen, über die alle verfügbaren Bibliotheksressourcen zugänglich sind.

Mithilfe der Schema Registry API können Sie grundlegende CRUD-Vorgänge durchführen, um alle Schema und zugehörigen Ressourcen, die Ihnen in der Adobe Experience Platform zur Verfügung stehen, Ansicht und zu verwalten. Dies umfasst die von Adobe, Experience Platform-Partnern und Anbietern, deren Anwendungen Sie verwenden, definierten Werte. Sie können auch API-Aufrufe verwenden, um neue Schema und Ressourcen für Ihr Unternehmen zu erstellen sowie bereits definierte Ansichten- und Bearbeitungsressourcen zu erstellen.

In diesem Entwicklerhandbuch finden Sie Anweisungen, wie Sie mit der Schema-Registrierungs-API Beginn ausführen können. Das Handbuch enthält dann Beispiel-API-Aufrufe für die Ausführung wichtiger Vorgänge mithilfe der Schema-Registrierung.

## Voraussetzungen

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas.
* [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Schema Registry API erfolgreich aufrufen zu können.

## Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich derjenigen, die zur Schema Registry gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Alle GET-Anfragen an die Schema Registry erfordern einen zusätzlichen Accept-Header, dessen Wert das Format der von der API zurückgegebenen Informationen bestimmt. Weitere Informationen finden Sie im Abschnitt [Accept-Kopfzeile](#accept) .

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

* Content-Type: application/json

## Ihre TENANT_ID kennen {#know-your-tenant_id}

In diesem Handbuch werden Verweise auf eine `TENANT_ID`Seite angezeigt. Diese ID wird verwendet, um sicherzustellen, dass die von Ihnen erstellten Ressourcen korrekt benannt und in Ihrer IMS-Organisation enthalten sind. Wenn Sie Ihre ID nicht kennen, können Sie sie mit der folgenden GET-Anforderung abrufen:

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

Eine erfolgreiche Antwort gibt Informationen zur Verwendung der Schema-Registrierung durch Ihr Unternehmen zurück. Dazu gehört ein `tenantId` Attribut, dessen Wert Ihre `TENANT_ID`ist.

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

* `tenantId`: Der `TENANT_ID` Wert für Ihre IMS-Organisation.

## Verstehen Sie die `CONTAINER_ID` {#container}

Für Aufrufe der Schema Registry-API muss eine `CONTAINER_ID`Variable verwendet werden. Es gibt zwei Container, für die API-Aufrufe durchgeführt werden können: der **globale Container** und der **Mieter-Container**.

### Globaler Container

Der globale Container umfasst alle standardmäßigen Adobe- und Experience Platform-Partnerklassen, -mixins, -Datentypen und -Schema. Sie können nur Listen- und Nachschlagetforderungen (GET) für den globalen Container ausführen.

### Mandanten-Container

Der Mieter-Container enthält alle Klassen, Mixins, Datentypen, Schema und Deskriptoren, die von einer IMS-Organisation definiert werden, `TENANT_ID`und ist nicht mit Ihrer Unikalität zu verwechseln. Sie sind für jede Organisation individuell, d. h. sie sind nicht sichtbar oder von anderen IMS-Orgs zu verwalten. Sie können alle CRUD-Vorgänge (GET, POST, PUT, PATCH, DELETE) für die Ressourcen ausführen, die Sie im Mieter-Container erstellen.

Wenn Sie eine Klasse, ein Mixin, ein Schema oder einen Datentyp im Mieter-Container erstellen, wird diese in der Schema-Registrierung gespeichert und eine `$id` URI zugewiesen, die Ihre `TENANT_ID`ID enthält. Dies `$id` wird in der gesamten API verwendet, um auf bestimmte Ressourcen zu verweisen. Beispiele für `$id` Werte finden Sie im nächsten Abschnitt.

## Schema-ID {#schema-identification}

Schema werden mit einem `$id` Attribut in Form eines URI identifiziert, z. B.:
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Um den URI REST-freundlicher zu gestalten, verfügen Schema auch über eine Punktschreibungskodierung des URI in einer Eigenschaft mit der Bezeichnung `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Durch Aufrufe der Schema Registry-API wird entweder der URL-kodierte `$id` URI oder das `meta:altId` (Punkt-Notation-Format) unterstützt. Es empfiehlt sich, den URL-kodierten `$id` URI zu verwenden, wenn ein REST-Aufruf an die API erfolgt, wie z. B.:
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Kopfzeile akzeptieren {#accept}

Bei der Ausführung von Liste- und Abfragevorgängen (GET) in der Schema Registry-API ist ein Accept-Header erforderlich, um das Format der von der API zurückgegebenen Daten zu bestimmen. Wenn Sie nach bestimmten Ressourcen suchen, muss eine Versionsnummer auch in der Kopfzeile &quot;Akzeptieren&quot;enthalten sein.

Die folgende Tabelle enthält Listen, die mit den Accept-Header-Werten kompatibel sind, einschließlich derer mit Versionsnummern, sowie Beschreibungen, was die API bei der Verwendung zurückgibt.

| Accept | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Gibt nur eine Liste von IDs zurück. Dies wird am häufigsten für die Auflistung von Ressourcen verwendet. |
| `application/vnd.adobe.xed+json` | Gibt eine Liste des vollständigen JSON-Schemas mit dem Original `$ref` und `allOf` inbegriffen zurück. Damit wird eine Liste voller Ressourcen zurückgegeben. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Rohes XDM mit `$ref` und `allOf`. Hat Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` Attribute und `allOf` gelöst. Hat Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Rohes XDM mit `$ref` und `allOf`. Keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` Attribute und `allOf` gelöst. Keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` Attribute und `allOf` gelöst. Deskriptoren sind enthalten. |

>[!NOTE] Wenn Sie nur die `major` Version (z.B. 1, 2, 3) angeben, gibt die Registrierung die neueste `minor` Version (z.B. .1, .2, .3) automatisch.

## XDM-Feldbeschränkungen und bewährte Verfahren

Die Felder eines Schemas werden innerhalb seines `properties` Objekts aufgelistet. Jedes Feld ist selbst ein Objekt, das Attribute zur Beschreibung und Einschränkung der Daten enthält, die das Feld enthalten kann.

Weitere Informationen zum Definieren von Feldtypen in der API finden Sie im [Anhang](appendix.md) zu diesem Handbuch, einschließlich Codebeispiele und optionale Einschränkungen für die am häufigsten verwendeten Datentypen.

Das folgende Beispielfeld zeigt ein ordnungsgemäß formatiertes XDM-Feld mit weiteren Details zu Benennungsbeschränkungen und Best Practices. Diese Verfahren können auch angewendet werden, wenn andere Ressourcen definiert werden, die ähnliche Attribute enthalten.

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

* Der Name eines Feldobjekts kann alphanumerische Zeichen, Bindestriche oder Unterstriche enthalten, **darf jedoch nicht** mit einem Unterstrich versehen sein.
   * **Richtig:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Falsch:** `_fieldName`
* camelCase wird für den Namen des Feldobjekts bevorzugt. Beispiel: `fieldName`
* Das Feld sollte eine `title`in der Titelleiste geschriebene Zeichenfolge enthalten. Beispiel: `Field Name`
* Für das Feld ist ein `type`Feld erforderlich.
   * Die Definition bestimmter Typen kann optional sein `format`.
   * Wenn eine bestimmte Formatierung der Daten erforderlich ist, `examples` kann sie als Array hinzugefügt werden.
   * Der Feldtyp kann auch mit einem beliebigen Datentyp in der Registrierung definiert werden. Weitere Informationen finden Sie im Abschnitt zum [Erstellen eines Datentyps](create-data-type.md) in diesem Handbuch.
* Im `description` Abschnitt werden das Feld und die relevanten Informationen zu Felddaten erläutert. Es sollte in vollen Sätzen mit klarer Sprache geschrieben werden, damit jeder, der auf das Schema zugreift, die Absicht des Feldes verstehen kann.

Weitere Informationen zum Definieren von Feldtypen in der API finden Sie im [Anhang](appendix.md) .

## Nächste Schritte

Dieses Dokument deckte die erforderlichen Kenntnisse ab, um die Schema Registry API aufzurufen, einschließlich der erforderlichen Authentifizierungsdaten. Sie können nun zu den Beispielaufrufen in diesem Entwicklerhandbuch fortfahren und deren Anweisungen folgen. Eine ausführliche schrittweise Anleitung zum Erstellen eines Schemas in der API finden Sie im folgenden [Lernprogramm](../tutorials/create-schema-api.md).
