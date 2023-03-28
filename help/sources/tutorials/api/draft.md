---
keywords: Experience Platform; Startseite; beliebte Themen; Flussdienst;
title: Entwürfe von Datenflüssen mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Ihre Datenflüsse mithilfe der Flow Service-API in einen Entwurfsstatus setzen.
badge: label="New Feature" type="Positive"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 18%

---

# Entwerfen von Datenflüssen mithilfe der Flow Service-API

Speichern Sie Ihre Datenflüsse bei Verwendung der Flow Service-API als Entwürfe, indem Sie die Variable `mode=draft` Abfrageparameter während des Flusserstellungsaufrufs. Entwürfe können später mit neuen Informationen aktualisiert und veröffentlicht werden, sobald sie fertig sind. In diesem Tutorial werden die Schritte zum Festlegen Ihrer Datenflüsse in einen Entwurfsstatus mithilfe der Flow Service-API beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Voraussetzungen

Für dieses Tutorial müssen Sie bereits die Assets generiert haben, die zum Erstellen eines Datenflusses erforderlich sind. Dazu gehört Folgendes:

* Eine authentifizierte Basisverbindung
* eine Quellverbindung
* Ein Ziel-XDM-Schema
* Ein Zieldatensatz
* Zielverbindung
* Zuordnung

Wenn Sie diese Werte noch nicht haben, wählen Sie eine Quelle aus [den Katalog in der Quellenübersicht](../../home.md). Befolgen Sie dann die Anweisungen der angegebenen Quelle, um die Assets zu generieren, die zum Entwerfen eines Datenflusses erforderlich sind.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Festlegen des Status eines Datenflusses auf Entwurf

Die folgenden Abschnitte beschreiben den Prozess zum Festlegen eines Datenflusses als Entwurf, zum Aktualisieren des Datenflusses, zum Veröffentlichen des Datenflusses und schließlich zum Löschen des Datenflusses.

### Datenfluss entwerfen

Um einen Datenfluss als Entwurf festzulegen, stellen Sie eine POST-Anfrage an die `/flows` Endpunkt beim Hinzufügen von `mode=draft` als Abfrageparameter. Auf diese Weise können Sie einen Datenfluss erstellen und als Entwurf speichern.

**API-Format**

```http
POST /flows?mode=draft
```

| Parameter | Beschreibung |
| --- | --- |
| `mode` | Ein vom Benutzer bereitgestellter Abfrageparameter, der den Status des Datenflusses bestimmt. Um einen Datenfluss als Entwurf festzulegen, legen Sie `mode` nach `draft`. |

**Anfrage**

Mit der folgenden Anfrage wird ein Datenfluss-Entwurf erstellt.

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die `id` und die entsprechenden `etag` Ihres Datenflusses.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Datenfluss aktualisieren

Um Ihren Entwurf zu aktualisieren, stellen Sie eine PATCH-Anfrage an die `/flows` -Endpunkt angeben, während Sie die Kennung des Datenflusses angeben, den Sie aktualisieren möchten. In diesem Schritt müssen Sie auch eine `If-Match` -Header-Parameter, der dem `etag` des Datenflusses, den Sie aktualisieren möchten.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Mit den folgenden Anfragen werden dem entworfenen Datenfluss Zuordnungstransformationen hinzugefügt.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**Antwort**

Bei einer erfolgreichen Antwort wird Ihre Fluss-ID zurückgegeben und `etag`. Um die Änderung zu überprüfen, können Sie eine GET-Anfrage an die `/flows` -Endpunkt bei der Bereitstellung Ihrer Fluss-ID.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Datenfluss veröffentlichen

Sobald Ihr Entwurf zur Veröffentlichung bereit ist, stellen Sie eine POST-Anfrage an die `/flows` -Endpunkt und geben die ID des Entwurfs-Datenflusses an, den Sie veröffentlichen möchten, sowie einen Aktionsvorgang für die Veröffentlichung.

**API-Format**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parameter | Beschreibung |
| --- | --- |
| `op` | Ein Aktionsvorgang, der den Status des abgefragten Datenflusses aktualisiert. Um einen Entwurf-Datenfluss zu veröffentlichen, legen Sie `op` nach `publish`. |

**Anfrage**

Mit der folgenden Anfrage wird Ihr Datenfluss-Entwurf veröffentlicht.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die ID und die entsprechende `etag` Ihres Datenflusses.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Löschen eines Datenflusses

Um Ihren Datenfluss zu löschen, stellen Sie eine DELETE-Anfrage an die `/flows` -Endpunkt angegeben, während Sie die Kennung des Datenflusses angeben, den Sie löschen möchten. Ausführliche Anweisungen zum Löschen eines Datenflusses mithilfe der Flow Service-API finden Sie im Handbuch unter [Löschen eines Datenflusses in der API](./delete-dataflows.md).