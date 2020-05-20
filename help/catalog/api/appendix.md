---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zum Entwickler von Katalogdiensten
topic: developer guide
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---


# Handbuch zum Entwickler von Katalogdiensten

Dieses Dokument enthält zusätzliche Informationen, die Sie bei der Arbeit mit der Katalog-API unterstützen.

## Ansicht verwandter Objekte {#view-interrelated-objects}

Einige Katalogobjekte können mit anderen Katalogobjekten verknüpft werden. Alle Felder, denen `@` in Antwortnutzlasten ein Präfix vorangestellt wird, bezeichnen verwandte Objekte. Die Werte für diese Felder haben die Form eines URI, der in einer separaten GET-Anforderung zum Abrufen der zugehörigen Objekte, die sie darstellen, verwendet werden kann.

Der Beispieldataset, der im Dokument bei der [Suche nach einem bestimmten Datensatz](look-up-object.md) zurückgegeben wird, enthält ein `files` Feld mit dem folgenden URI-Wert: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. Der Inhalt des `files` Felds kann mit diesem URI als Pfad für eine neue GET-Anforderung angezeigt werden.

**API-Format**

```http
GET {OBJECT_URI}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_URI}` | Der vom verknüpften Objektfeld bereitgestellte URI (ohne das `@` Symbol). |

**Anfrage**

Die folgende Anforderung verwendet den URI, der die `files` Eigenschaft des Beispieldatasets enthält, um eine Liste der zugehörigen Dateien des Datensatzes abzurufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste verwandter Objekte zurück. In diesem Beispiel wird eine Liste von Datensatzdateien zurückgegeben.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Mehrere Anforderungen in einem einzelnen Aufruf

Der Stamm-Endpunkt der Katalog-API ermöglicht es, mehrere Anforderungen innerhalb eines einzelnen Aufrufs zu stellen. Die Anforderungs-Nutzlast enthält ein Array von Objekten, die normalerweise einzelne Anforderungen darstellen und dann in der richtigen Reihenfolge ausgeführt werden.

Wenn es sich bei diesen Anforderungen um Änderungen oder Ergänzungen zum Katalog handelt und eine der Änderungen fehlschlägt, werden alle Änderungen zurückgesetzt.

**API-Format**

```http
POST /
```

**Anfrage**

Die folgende Anforderung erstellt einen neuen Datensatz und erstellt dann zugehörige Ansichten für diesen Datensatz. Dieses Beispiel zeigt die Verwendung der Vorlagensprache für den Zugriff auf Werte, die in vorherigen Aufrufen zur Verwendung in nachfolgenden Aufrufen zurückgegeben wurden.

Wenn Sie beispielsweise auf einen Wert verweisen möchten, der von einer vorherigen Unteranforderung zurückgegeben wurde, können Sie einen Verweis im folgenden Format erstellen: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (dabei `{REQUEST_ID}` ist die vom Benutzer angegebene ID für die Unteranforderung, wie unten dargestellt). Mithilfe dieser Vorlagen können Sie auf jedes Attribut verweisen, das im Hauptteil des Antwortobjekts einer vorherigen Unteranforderung verfügbar ist.

>[!NOTE] Wenn eine ausgeführte Unteranforderung nur den Verweis auf ein Objekt zurückgibt (wie dies bei den meisten POST- und PUT-Anforderungen in der Katalog-API der Standard ist), wird dieser Verweis als Alias für den Wert verwendet `id` und kann als `<<{OBJECT_ID}.id>>`verwendet werden.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Vom Benutzer bereitgestellte ID, die an das Antwortobjekt angehängt wird, damit Sie Anforderungen an Antworten zuordnen können. Katalog speichert diesen Wert nicht und gibt ihn lediglich zu Referenzzwecken in der Antwort zurück. |
| `resource` | Der Ressourcenpfad relativ zum Stammordner der Katalog-API. Das Protokoll und die Domäne sollten nicht Teil dieses Werts sein und mit &quot;/&quot;versehen werden. <br/><br/> Wenn Sie PATCH oder DELETE als Unteranforderung verwenden, `method`fügen Sie die Objekt-ID in den Ressourcenpfad ein. Dieser Ressourcenpfad ist nicht mit dem vom Benutzer bereitgestellten zu verwechseln `id`, sondern verwendet die ID des Katalogobjekts selbst (z. B. `resource: "/dataSets/1234567890"`). |
| `method` | Der Name der Methode (GET, PUT, POST, PATCH oder DELETE), die sich auf die in der Anforderung stattfindende Aktion bezieht. |
| `body` | Das JSON-Dokument, das normalerweise als Payload in einer POST-, PUT- oder PATCH-Anforderung übergeben wird. Diese Eigenschaft ist für GET- oder DELETE-Anforderungen nicht erforderlich. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array von Objekten zurück, das die `id` der jeweiligen Anforderung zugewiesenen Objekte, den HTTP-Statuscode für die einzelne Anforderung und die Antwort enthält `body`. Da bei den drei Musteranforderungen alle neue Objekte erstellt werden sollten, handelt es sich bei dem `body` Objekt jeweils um ein Array, das nur die ID des neu erstellten Objekts enthält, ebenso wie bei den erfolgreichsten POST-Antworten im Katalog.

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

Gehen Sie beim Prüfen der Antwort auf eine Mehrfachanforderung sorgfältig vor, da Sie den Code jeder einzelnen Teilanforderung überprüfen müssen und sich nicht nur auf den HTTP-Statuscode für die übergeordnete POST-Anforderung verlassen müssen.  Es ist möglich, dass eine einzelne Unteranforderung eine 404 zurückgibt (z. B. eine GET-Anforderung für eine ungültige Ressource), während die Gesamtanforderung 200 zurückgibt.

## Zusätzliche Anforderungsheader

Der Katalog enthält mehrere Kopfzeilenkonventionen, mit denen Sie die Integrität Ihrer Daten während der Aktualisierung beibehalten können.

### If-Match

Es empfiehlt sich, mithilfe der Objektversionsfunktion die Art von Datenbeschädigung zu verhindern, die auftritt, wenn ein Objekt von mehreren Benutzern nahezu gleichzeitig gespeichert wird.

Beim Aktualisieren eines Objekts wird empfohlen, zunächst einen API-Aufruf an die Ansicht (GET) des zu aktualisierenden Objekts durchzuführen. In der Antwort enthalten (und bei jedem Aufruf, bei dem die Antwort ein einzelnes Objekt enthält) ist ein `E-Tag` Header, der die Version des Objekts enthält. Das Hinzufügen der Objektversion als Anforderungsheader mit dem Namen `If-Match` in Ihren Aktualisierungsaufrufen (PUT oder PATCH) führt dazu, dass die Aktualisierung nur dann erfolgreich ist, wenn die Version immer noch gleich ist, was dazu beiträgt, Datenkollisionen zu verhindern.

Wenn die Versionen nicht übereinstimmen (das Objekt wurde nach dem Abrufen durch einen anderen Prozess geändert), erhalten Sie den HTTP-Status 412 (Vorbedingung fehlgeschlagen), der angibt, dass der Zugriff auf die Zielgruppe-Ressource verweigert wurde.

### Pragma

Gelegentlich möchten Sie ein Objekt überprüfen, ohne die Informationen zu speichern. Die Verwendung der `Pragma` Kopfzeile mit dem Wert `validate-only` &quot;erlaubt es Ihnen, POST- oder PUT-Anfragen nur zu Überprüfungszwecken zu senden, wodurch verhindert wird, dass Änderungen an den Daten bestehen bleiben.

## Datenvergleich

Compaction ist ein Experience Platform-Dienst, der Daten aus kleinen Dateien in größere Dateien zusammenführt, ohne Daten zu ändern. Aus Leistungsgründen ist es manchmal sinnvoll, kleine Dateien in größere Dateien zu kombinieren, um bei der Abfrage schneller auf die Daten zugreifen zu können.

Wenn die Dateien in einem erfassten Stapel komprimiert wurden, wird das zugehörige Katalogobjekt für Überwachungszwecke aktualisiert.