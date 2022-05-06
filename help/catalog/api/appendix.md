---
keywords: Experience Platform; Startseite; beliebte Themen; Catalog Service; Katalog-API; Anhang
solution: Experience Platform
title: Anhang zum Catalog Service API-Handbuch
topic-legacy: developer guide
description: Dieses Dokument enthält zusätzliche Informationen, die Sie bei der Arbeit mit der Catalog-API in Adobe Experience Platform unterstützen.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 79%

---

# [!DNL Catalog Service] Anhang zum API-Handbuch

Dieses Dokument enthält zusätzliche Informationen, die Sie bei der Arbeit mit dem [!DNL Catalog] API.

## Verwandte Objekte anzeigen {#view-interrelated-objects}

Einige [!DNL Catalog] Objekte können mit anderen verknüpft werden [!DNL Catalog] Objekte. Alle Felder, die in Antwort-Payloads das Präfix `@` aufweisen, bezeichnen verwandte Objekte. Die Werte für diese Felder haben die Form eines URI, der in einer separaten GET-Anfrage zum Abrufen der zugehörigen Objekte, die sie darstellen, genutzt werden kann.

Der Beispieldatensatz, der im Dokument zum [Nachschlagen eines bestimmten Datensatzes](look-up-object.md) zurückgegeben wird, enthält ein `files`-Feld mit dem folgenden URI-Wert: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. Der Inhalt des `files`-Felds kann durch Verwendung des URI als Pfad für eine neue GET-Anfrage angezeigt werden.

**API-Format**

```http
GET {OBJECT_URI}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_URI}` | Der vom verknüpften Objektfeld angegebene URI (ohne das `@`-Symbol). |

**Anfrage**

Folgende Anfrage nutzt den URI, der in der `files`-Eigenschaft des Beispieldatensatzes angegeben ist, um eine Liste der zugehörigen Dateien des Datensatzes abzurufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste verwandter Objekte zurück. In diesem Beispiel wird eine Liste mit Datensatzdateien zurückgegeben.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Mehrere Anfragen in einem einzelnen Aufruf stellen

Der Stamm-Endpunkt der [!DNL Catalog] API ermöglicht es, mehrere Anfragen innerhalb eines einzelnen Aufrufs zu stellen. Die Anfrage-Payload enthält eine Gruppe von Objekten, die normalerweise einzelne Anfragen darstellen würden, die dann der Reihenfolge nach ausgeführt werden.

Wenn es sich bei diesen Anforderungen um Änderungen oder Ergänzungen von [!DNL Catalog] und eine der Änderungen fehlschlägt, werden alle Änderungen rückgängig gemacht.

**API-Format**

```http
POST /
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Datensatz und erzeugt dann verwandte Ansichten für diesen Datensatz. Dieses Beispiel veranschaulicht den Einsatz von Vorlagensprache für den Zugriff auf Werte, die in vorherigen Aufrufen zur Verwendung in nachfolgenden Aufrufen zurückgegeben wurden.

Wenn Sie beispielsweise auf einen Wert verweisen möchten, der von einer vorherigen Unteranfrage zurückgegeben wurde, können Sie im folgenden Format einen Verweis erstellen: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (dabei ist `{REQUEST_ID}` die vom Anwender angegebene Kennung für die Unteranfrage, wie unten dargestellt). Mithilfe dieser Vorlagen können Sie auf jedes Attribut verweisen, das im Text des Antwortobjekts einer vorherigen Unteranfrage verfügbar ist.

>[!NOTE]
>
> Wenn eine ausgeführte Unteranfrage nur den Verweis auf ein Objekt zurückgibt (wie es bei den meisten POST- und PUT-Anfragen in der Catalog-API Standard ist), wird dieser Verweis als Alias für den Wert `id` verwendet und kann als `<<{OBJECT_ID}.id>>` genutzt werden.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `id` | Vom Anwender angegebene Kennung, die an das Antwortobjekt angehängt wird, damit Sie Anfragen Antworten zuordnen können. [!DNL Catalog] speichert diesen Wert nicht und gibt ihn in der Antwort lediglich zu Referenzzwecken zurück. |
| `resource` | Der Ressourcenpfad relativ zum Stammverzeichnis der [!DNL Catalog] API. Das Protokoll und die Domain sollten nicht Teil dieses Werts sein und sollten mit dem Präfix „/“ versehen werden. <br/><br/> Wenn Sie PATCH oder DELETE als Unteranfrage verwenden`method`, fügen Sie die Objektkennung in den Ressourcenpfad ein. Nicht zu verwechseln mit dem vom Benutzer bereitgestellten `id`verwendet der Ressourcenpfad die Kennung der [!DNL Catalog] Objekt selbst (z. B. `resource: "/dataSets/1234567890"`). |
| `method` | Der Name der Methode (GET, PUT, POST, PATCH oder DELETE), die mit der in der Anfrage ausgeführten Aktion verknüpft ist. |
| `body` | Das JSON-Dokument, das in einer POST-, PUT- oder PATCH-Anfrage normalerweise als Payload übergeben wird. Diese Eigenschaft ist bei GET- oder DELETE-Anfragen nicht erforderlich. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Gruppe von Objekten, die die einzelnen Anfragen zugewiesene `id` enthalten, den HTTP-Status-Code für die jeweilige Anfrage und den `body` (Text) der Antwort zurück. Da alle drei Beispielanfragen neue Objekte erstellen sollten, wird die `body` von jedem Objekt ist ein Array, das nur die ID des neu erstellten Objekts enthält, ebenso wie der Standard mit den erfolgreichsten POST-Antworten in [!DNL Catalog].

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

Gehen Sie beim Prüfen der Antwort auf eine Mehrfachanfrage sorgfältig vor, da Sie den Code jeder einzelnen Unteranfrage prüfen und sich nicht allein auf den HTTP-Status-Code für die übergeordnete POST-Anfrage verlassen müssen.  Es ist möglich, dass eine einzelne Unteranfrage einen 404-Fehler zurückgibt (z. B. GET-Anfrage für eine ungültige Ressource), während die übergeordnete Anfrage 200 zurückgibt.

## Zusätzliche Anfragekopfzeilen

[!DNL Catalog] umfasst verschiedene Kopfzeilenkonventionen, damit Sie die Integrität Ihrer Daten bei Aktualisierungen wahren können.

### If-Match

Es empfiehlt sich, mithilfe von Objektversionierung die Art von Datenbeschädigung zu verhindern, die auftritt, wenn ein Objekt von mehreren Anwendern nahezu gleichzeitig gespeichert wird.

Beim Aktualisieren eines Objekts wird empfohlen, zunächst einen API-Aufruf zu tätigen, um das zu aktualisierende Objekt anzuzeigen (GET). In der Antwort enthalten (und bei jedem Aufruf, bei dem die Antwort ein einzelnes Objekt enthält) ist eine `E-Tag`-Kopfzeile, die die Version des Objekts enthält. Durch Hinzufügen der Objektversion als Anfragekopfzeile namens `If-Match` in Ihren Aktualisierungsaufrufen (PUT oder PATCH) wird dafür gesorgt, dass die Aktualisierung nur dann erfolgreich ausgeführt wird, wenn die Version weiterhin gleich ist. Dies trägt dazu bei, Datenkollisionen zu verhindern.

Wenn die Versionen nicht übereinstimmen (das Objekt wurde nach dem Abruf durch Sie von einen anderen Prozess geändert), erhalten Sie den HTTP-Status 412 (Fehler bei Vorbedingung), der angibt, dass der Zugriff auf die Zielressource verweigert wurde.

### Pragma

Es kann vorkommen, dass Sie ein Objekt prüfen möchten, ohne die Informationen zu speichern. Durch Verwendung der `Pragma`-Kopfzeile mit dem Wert `validate-only` können Sie POST- oder PUT-Anfragen ausschließlich zu Validierungszwecken senden, wodurch verhindert wird, dass Änderungen an den Daten persistiert werden.

## Datenkomprimierung

Komprimierung ist eine [!DNL Experience Platform] -Dienst, der Daten aus kleinen Dateien in größeren Dateien zusammenführt, ohne Daten zu ändern. Aus Leistungsgründen kann es sinnvoll sein, mehrere kleine Dateien in größeren Dateien zu kombinieren, um bei Abfragen schneller auf Daten zugreifen zu können.

Wenn die Dateien in einem erfassten Batch komprimiert wurden, werden die zugehörigen [!DNL Catalog] -Objekt wird zu Überwachungszwecken aktualisiert.
