---
keywords: Experience Platform; home; beliebte Themen; Catalog Service; Katalog-API; Anhang
solution: Experience Platform
title: Anhang zum Catalog Service API-Handbuch
description: Dieses Dokument enthält zusätzliche Informationen, die Sie bei der Arbeit mit der Catalog-API in Adobe Experience Platform unterstützen.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 80%

---

# [!DNL Catalog Service] Anhang zum API-Handbuch

Dieses Dokument enthält zusätzliche Informationen, die Sie bei der Arbeit mit dem [!DNL Catalog] API.

## Verwandte Objekte anzeigen {#view-interrelated-objects}

Einige [!DNL Catalog] Objekte können mit anderen verknüpft werden [!DNL Catalog] Objekte. Alle Felder, die in Antwort-Payloads das Präfix `@` aufweisen, bezeichnen verwandte Objekte. Die Werte für diese Felder haben die Form eines URI, der in einer separaten GET-Anfrage zum Abrufen der zugehörigen Objekte, die sie darstellen, genutzt werden kann.

Der Beispieldatensatz, der im Dokument zum [Nachschlagen eines bestimmten Datensatzes](look-up-object.md) zurückgegeben wird, enthält ein `files`-Feld mit dem folgenden URI-Wert: `"@/datasetFiles?datasetId={DATASET_ID}"`. Der Inhalt des `files`-Felds kann durch Verwendung des URI als Pfad für eine neue GET-Anfrage angezeigt werden.

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
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
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
