---
solution: Experience Platform
title: Bearbeiten von Zielverbindungen mit der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie verschiedene Komponenten einer Zielverbindung mit der Flow Service-API bearbeiten.
source-git-commit: 956ac5d210d54526e886e57b8ea37ab4b3fbab8a
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 33%

---

# Bearbeiten von Zielverbindungen mit der Flow Service-API

In diesem Tutorial werden die Schritte zum Bearbeiten verschiedener Komponenten einer Zielverbindung beschrieben. Erfahren Sie, wie Sie mithilfe des [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Die in diesem Tutorial beschriebenen Bearbeitungsvorgänge werden derzeit nur über die Flow Service-API unterstützt.

## Erste Schritte {#get-started}

Für dieses Tutorial benötigen Sie eine gültige Datenfluss-ID. Wenn Sie keine gültige Datenfluss-ID haben, wählen Sie Ihr Ziel aus der [Zielkatalog](../catalog/overview.md) und führen Sie die Schritte aus, die beschrieben wurden, um [Verbindung zum Ziel herstellen](../ui/connect-destination.md) und [Daten aktivieren](../ui/activation-overview.md) vor dem Versuch dieses Tutorials.

>[!NOTE]
>
> Die Begriffe *Fluss* und *dataflow* werden in diesem Tutorial synonym verwendet. Im Kontext dieses Tutorials haben sie dieselbe Bedeutung.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. ](../home.md)[!DNL Destinations] Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Ihren Datenfluss mit der [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in der Experience Platform, einschließlich derjenigen, die [!DNL Flow Service], werden auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Wenn die Variable `x-sandbox-name` -Kopfzeile nicht angegeben ist, werden Anfragen unter der `prod` Sandbox.

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Nachschlagen von Datenflussdetails {#look-up-dataflow-details}

Der erste Schritt bei der Bearbeitung Ihrer Zielverbindung besteht darin, Datenflussdetails mit Ihrer Fluss-ID abzurufen. Sie können die aktuellen Details eines vorhandenen Datenflusses anzeigen, indem Sie eine GET-Anfrage an den `/flows`-Endpunkt stellen.

>[!TIP]
>
>Sie können die Experience Platform-Benutzeroberfläche verwenden, um die gewünschte Datenfluss-ID eines Ziels zu erhalten. Navigieren Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]**, wählen Sie den gewünschten Ziel-Datenfluss aus und suchen Sie die Ziel-ID in der rechten Leiste. Die Ziel-ID ist der Wert, den Sie im nächsten Schritt als Fluss-ID verwenden werden.
>
> ![Abrufen der Ziel-ID über die Experience Platform-Benutzeroberfläche](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API-Format**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Die eindeutige `id` für den Ziel-Datenfluss, den Sie abrufen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden Informationen zu Ihrer Fluss-ID abgerufen.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die aktuellen Details Ihres Datenflusses zurück, einschließlich der Version, der eindeutigen Kennung (`id`) und anderen relevanten Informationen. Am relevantesten für dieses Tutorial sind die in der Antwort unten hervorgehobenen Ziel- und Basis-Verbindungs-IDs. Sie verwenden diese IDs in den nächsten Abschnitten, um verschiedene Komponenten der Zielverbindung zu aktualisieren.

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## Bearbeiten von Zielverbindungskomponenten (Speicherort und andere Komponenten) {#patch-target-connection}

Die Komponenten einer Zielverbindung unterscheiden sich je nach Ziel. Beispiel: für [!DNL Amazon S3] -Ziele festzulegen, können Sie den Behälter und Pfad aktualisieren, in den Dateien exportiert werden. Für [!DNL Pinterest] Ziele, können Sie Ihre [!DNL Pinterest Advertiser ID] und [!DNL Google Customer Match] Sie können [!DNL Pinterest Account ID].

Um Komponenten einer Zielverbindung zu aktualisieren, führen Sie eine PATCH-Anfrage an die `/targetConnections/{TARGET_CONNECTION_ID}` -Endpunkt unter Angabe Ihrer Ziel-Verbindungs-ID, -Version und der neuen Werte, die Sie verwenden möchten. Denken Sie daran, dass Sie Ihre Ziel-Verbindungs-ID im vorherigen Schritt erhalten haben, als Sie einen vorhandenen Datenfluss zu Ihrem gewünschten Ziel überprüft haben.

>[!IMPORTANT]
>
>Die Kopfzeile `If-Match` ist bei einer PATCH-Anfrage erforderlich. Der Wert für diesen Header ist die eindeutige Version der Zielverbindung, die Sie aktualisieren möchten. Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung einer Flussentität wie Datenfluss, Zielverbindung und anderen aktualisiert.
>
> Um die neueste Version des eTag-Werts zu erhalten, stellen Sie eine GET-Anfrage an die `/targetConnections/{TARGET_CONNECTION_ID}` Endpunkt, wobei `{TARGET_CONNECTION_ID}` ist die Ziel-Verbindungs-ID, die Sie aktualisieren möchten.

Im Folgenden finden Sie einige Beispiele für die Aktualisierung von Parametern in der Zielverbindungsspezifikation für verschiedene Zieltypen. Die allgemeine Regel zum Aktualisieren von Parametern für ein Ziel lautet jedoch wie folgt:

Rufen Sie die Datenflug-ID der Verbindung ab, rufen Sie die Zielverbindungs-ID ab und PATCH Sie die Zielverbindung mit aktualisierten Werten für die gewünschten Parameter.

>[!BEGINSHADEBOX]

**API-Format**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

Die folgende Anfrage aktualisiert die `bucketName` und `path` Parameter eines [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) Zielverbindung.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Ziel-Verbindungs-ID und ein aktualisiertes Etag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] -API verwenden und dabei Ihre Ziel-Verbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager und Google Ad Manager 360]

**Anfrage**

Die folgende Anfrage aktualisiert die Parameter einer [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) oder [[!DNL Google Ad Manager 360] Ziel](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) Verbindung zum Hinzufügen der neuen [**[!UICONTROL Segment-ID an Segmentname anhängen]**](/help/release-notes/2023/april-2023.md#destinations) -Feld.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Ziel-Verbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] -API verwenden und dabei Ihre Ziel-Verbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Anfrage**

Die folgende Anfrage aktualisiert die `advertiserId` Parameter eines [[!DNL Pinterest] Zielverbindung](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Ziel-Verbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] -API verwenden und dabei Ihre Ziel-Verbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Bearbeiten von Basisverbindungskomponenten (Authentifizierungsparameter und andere Komponenten) {#patch-base-connection}

Die Komponenten einer Basisverbindung unterscheiden sich je nach Ziel. Beispiel: für [!DNL Amazon S3] Ziele, können Sie den Zugriffsschlüssel und den geheimen Schlüssel für Ihre [!DNL Amazon S3] Standort.

Um Komponenten einer Basisverbindung zu aktualisieren, führen Sie eine PATCH-Anfrage an die `/connections` -Endpunkt unter Angabe Ihrer Basis-Verbindungs-ID, -Version und der neuen Werte, die Sie verwenden möchten.

Denken Sie daran, dass Sie Ihre Basis-Verbindungs-ID in einem vorherigen Schritt erhalten haben, als Sie einen vorhandenen Datenfluss zu Ihrem gewünschten Ziel überprüft haben.

>[!IMPORTANT]
>
>Die Kopfzeile `If-Match` ist bei einer PATCH-Anfrage erforderlich. Der Wert für diesen Header ist die eindeutige Version der Basisverbindung, die Sie aktualisieren möchten. Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung einer Flussentität wie Datenfluss, Basisverbindung usw. aktualisiert.
>
> Um die neueste Version des Etag-Werts zu erhalten, stellen Sie eine GET-Anfrage an die `/connections/{BASE_CONNECTION_ID}` Endpunkt, wobei `{BASE_CONNECTION_ID}` ist die Basisverbindungs-ID, die Sie aktualisieren möchten.

Im Folgenden finden Sie einige Beispiele für die Aktualisierung von Parametern in der Basisverbindungsspezifikation für verschiedene Typen von Zielen. Die allgemeine Regel zum Aktualisieren von Parametern für ein Ziel lautet jedoch wie folgt:

Rufen Sie die Datenfluss-ID der Verbindung ab, rufen Sie die Basisverbindungs-ID ab und PATCH Sie die Basisverbindung mit aktualisierten Werten für die gewünschten Parameter.

>[!BEGINSHADEBOX]

**API-Format**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

Die folgende Anfrage aktualisiert die `accessId` und `secretKey` Parameter eines [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) Zielverbindung.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Basisverbindungs-ID und ein aktualisiertes E-Tag angegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] API bei gleichzeitiger Angabe Ihrer Basis-Verbindungs-ID.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**Anfrage**

Die folgende Anfrage aktualisiert die Parameter eines [[!DNL Azure Blob] Ziel](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) Verbindung zum Aktualisieren der Verbindungszeichenfolge, die für die Verbindung mit einer Azure Blob-Instanz erforderlich ist.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Basisverbindungs-ID und ein aktualisiertes E-Tag angegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] API bei gleichzeitiger Angabe Ihrer Basis-Verbindungs-ID.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen für die Fehlermeldung bei der Experience Platform-API. Siehe [API-Statuscodes](/help/landing/troubleshooting.md#api-status-codes) und [Fehler in der Anfragekopfzeile](/help/landing/troubleshooting.md#request-header-errors) Weitere Informationen zur Interpretation von Fehlerantworten finden Sie im Handbuch zur Fehlerbehebung bei Platform .

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfahren, wie Sie verschiedene Komponenten einer Zielverbindung mit dem [!DNL Flow Service] API. Weitere Informationen zu Zielen finden Sie im Abschnitt [Ziele - Übersicht](../home.md).
