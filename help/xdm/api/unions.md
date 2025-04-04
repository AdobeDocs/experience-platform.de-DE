---
keywords: Experience Platform;Startseite;beliebte Themen;api;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schema Registry;Schema Registry;Vereinigung;Vereinigungen;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Unions-API-Endpunkt
description: Mit dem Endpunkt "/unions“ in der Schema Registry-API können Sie XDM-Vereinigungsschemas in Ihrer Erlebnisanwendung programmgesteuert verwalten.
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 39%

---

# Vereinigungs-Endpunkt

Vereinigungen (oder Vereinigungsansichten) sind systemgenerierte, schreibgeschützte Schemata, die die Felder aller Schemata aggregieren, die dieselbe Klasse ([!DNL XDM ExperienceEvent] oder [!DNL XDM Individual Profile]) haben und für die [[!DNL Real-Time Customer Profile]](../../profile/home.md) aktiviert sind.

In diesem Dokument werden wesentliche Konzepte für die Arbeit mit Vereinigungen in der Schema Registry-API beschrieben, einschließlich Beispielaufrufen für verschiedene Vorgänge. Weitere allgemeine Informationen zu Vereinigungen in XDM finden Sie im Abschnitt zu Vereinigungen in den [Grundlagen der Schema-Komposition](../schema/composition.md#union).

## Vereinigungsschemafelder

Die [!DNL Schema Registry] enthält automatisch drei Schlüsselfelder innerhalb eines Vereinigungsschemas: `identityMap`, `timeSeriesEvents` und `segmentMembership`.

### Identitätszuordnung

Die `identityMap` eines Vereinigungsschemas ist eine Darstellung der bekannten Identitäten innerhalb der zugehörigen Datensatz-Schemata der Vereinigung. Die Identitätszuordnung teilt Identitäten in verschiedene Arrays auf, die nach Namensraum geordnet sind. Jede aufgelistete Identität ist selbst ein Objekt, das einen eindeutigen `id` enthält. Weitere Informationen finden Sie in der [Dokumentation für Identity Service](../../identity-service/home.md).

### Zeitreihenereignisse

Das `timeSeriesEvents`-Array ist eine Liste von Ereignissen aus Zeitreihen, die sich auf die Schemata beziehen, die der Vereinigung zugeordnet sind. Wenn Profildaten in Datensätze exportiert werden, wird dieses Array für jeden Datensatz eingeschlossen. Dies ist in verschiedenen Anwendungsfällen nützlich, z. B. beim Machine Learning, bei dem Modelle zusätzlich zu den Datensatzattributen den gesamten Verhaltensverlauf eines Profils benötigen.

### Segmentzugehörigkeitszuordnung

Die `segmentMembership` speichert die Ergebnisse der Auswertung einer Segmentdefinition. Wenn Segmentaufträge mit der [Segmentation-API](https://www.adobe.io/experience-platform-apis/references/segmentation/) erfolgreich ausgeführt werden, wird die Zuordnung aktualisiert. `segmentMembership` speichert auch alle vorab ausgewerteten Zielgruppen, die in Experience Platform aufgenommen werden, und ermöglicht so die Integration in andere Lösungen wie Adobe Audience Manager. Weitere Informationen finden Sie im Tutorial [Erstellen von Zielgruppen mithilfe ](../../segmentation/tutorials/create-a-segment.md) APIs“.

## Abrufen einer Liste von Vereinigungen {#list}

Wenn Sie das `union`-Tag für ein Schema festlegen, fügt der [!DNL Schema Registry] das Schema automatisch zur Vereinigung für die Klasse hinzu, auf der das Schema basiert. Wenn für die betreffende Klasse keine Vereinigung vorhanden ist, wird automatisch eine neue Vereinigung erstellt. Der `$id` für die Union ähnelt dem `$id` anderer [!DNL Schema Registry] Ressourcen, mit dem einzigen Unterschied, dass durch zwei Unterstriche und das Wort „union“ (`__union`) angehängt wird.

Sie können eine Liste der verfügbaren Vereinigungen anzeigen, indem Sie eine GET-Anfrage an den `/tenant/unions`-Endpunkt senden.

**API-Format**

```http
GET /tenant/unions
```

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

Das Format der Antwort hängt von der in der Anfrage gesendeten `Accept`-Kopfzeile ab. Die folgenden `Accept` Kopfzeilen sind für die Auflistung von Vereinigungen verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung jeder Ressource zurück. Dies ist die empfohlene Kopfzeile zum Auflisten von Ressourcen. (Limit: 300) |
| `application/vnd.adobe.xed+json` | Gibt für jede Ressource eine vollständige JSON-Klasse mit `$ref` und `allOf` zurück. (Limit: 300) |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) und ein `results`-Array im Antworttext zurück. Wenn Vereinigungen definiert wurden, werden die Details für jede Vereinigung als -Objekte innerhalb des -Arrays bereitgestellt. Wenn keine Vereinigungen definiert wurden, wird dennoch der HTTP-Status 200 (OK) zurückgegeben, jedoch das `results`-Array ist leer.

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## Vereinigung nachschlagen {#lookup}

Sie können eine bestimmte Vereinigung durch eine GET-Anfrage anzeigen, die die `$id` und, je nach Accept-Kopfzeile, einige oder alle Details der Vereinigung beinhaltet.

>[!NOTE]
>
>Vereinigungssuchvorgänge sind mit dem `/unions`- und `/schemas`-Endpunkt verfügbar, um sie für die Verwendung in [!DNL Profile] Exporten in einen Datensatz zu aktivieren.

**API-Format**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{UNION_ID}` | Der URL-kodierte `$id`-URI der Vereinigung, die Sie suchen möchten. Bei URIs für Vereinigungs-Schemata wird „__Vereinigung“ angehängt. |

{style="table-layout:auto"}

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Anfragen für das Nachschlagen von Vereinigungen erfordern, dass `version` in die Accept-Kopfzeile aufgenommen wird.

Die folgenden Accept-Kopfzeilen stehen für das Nachschlagen von Vereinigungs-Schemas zur Verfügung:

| Accept | Beschreibung |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Roh mit `$ref` und `allOf`. Umfasst Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` Attribute und `allOf` gelöst. Umfasst Titel und Beschreibungen. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Vereinigungsansicht aller Schemata zurück, die die Klasse implementieren, deren `$id` im Anfragepfad bereitgestellt wurde.

Das Antwortformat hängt von der Accept-Kopfzeile ab, die in der Anfrage gesendet wird. Experimentieren Sie mit verschiedenen Accept-Kopfzeilen, um die Antworten zu vergleichen und zu ermitteln, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## Aktivieren eines Schemas für die Vereinigungs-Mitgliedschaft {#enable}

Damit ein Schema in die Vereinigung für seine Klasse aufgenommen werden kann, muss zum `meta:immutableTags` des Schemas ein `union`-Tag hinzugefügt werden. Sie können dies erreichen, indem Sie eine PATCH-Anfrage stellen, um dem betreffenden Schema ein `meta:immutableTags`-Array mit einem einzelnen Zeichenfolgenwert von `union` hinzuzufügen. Ein ausführliches Beispiel finden [ im Handbuch ](./schemas.md#union)schemas endpoint“.

## Auflisten von Schemata in einer Vereinigung {#list-schemas}

Um zu sehen, welche Schemata Teil einer bestimmten Vereinigung sind, können Sie eine GET-Anfrage an den `/tenant/schemas`-Endpunkt senden. Mithilfe des Abfrageparameters `property` können Sie die Antwort so konfigurieren, dass nur Schemata zurückgegeben werden, die ein `meta:immutableTags`-Feld und eine `meta:class` gleich der Klasse enthalten, auf deren Vereinigung Sie zugreifen.

**API-Format**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die `$id` der Klasse, deren vereinigungsaktivierte Schemata Sie auflisten möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft eine Liste aller Schemas ab, die Teil der Vereinigung für die [!DNL XDM Individual Profile]-Klasse sind.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Format der Antwort hängt von der in der Anfrage gesendeten `Accept`-Kopfzeile ab. Die folgenden `Accept`-Kopfzeilen sind für die Auflistung von Schemata verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung jeder Ressource zurück. Dies ist die empfohlene Kopfzeile zum Auflisten von Ressourcen. (Limit: 300) |
| `application/vnd.adobe.xed+json` | Gibt das vollständige JSON-Schema für jede Ressource mit den ursprünglichen `$ref` und `allOf` zurück. (Limit: 300) |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt eine gefilterte Liste von Schemata zurück, die nur diejenigen enthalten, die zur angegebenen Klasse gehören und für die Vereinigungsmitgliedschaft aktiviert wurden. Beachten Sie, dass bei Verwendung mehrerer Abfrageparameter von einer AND-Beziehung ausgegangen wird.

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
