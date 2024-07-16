---
solution: Experience Platform
title: Bearbeiten von Zielverbindungen mit der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie verschiedene Komponenten einer Zielverbindung mit der Flow Service-API bearbeiten.
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: 2a72f6886f7a100d0a1bf963eedaed8823a7b313
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 29%

---

# Bearbeiten von Zielverbindungen mit der Flow Service-API

In diesem Tutorial werden die Schritte zum Bearbeiten verschiedener Komponenten einer Zielverbindung beschrieben. Erfahren Sie, wie Sie mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) Authentifizierungsberechtigungen, den Exportspeicherort und mehr aktualisieren können.

>[!NOTE]
>
> Die in diesem Tutorial beschriebenen Bearbeitungsvorgänge werden derzeit nur über die Flow Service-API unterstützt.

## Erste Schritte {#get-started}

Für dieses Tutorial benötigen Sie eine gültige Datenfluss-ID. Wenn Sie keine gültige Datenfluss-ID haben, wählen Sie Ihr Ziel aus dem [Zielkatalog](../catalog/overview.md) aus und führen Sie die Schritte aus, die unter [Verbindung zum Ziel herstellen](../ui/connect-destination.md) und [Daten aktivieren](../ui/activation-overview.md) beschrieben sind, bevor Sie dieses Tutorial ausführen.

>[!NOTE]
>
> Die Begriffe *flow* und *dataflow* werden in diesem Tutorial synonym verwendet. Im Kontext dieses Tutorials haben sie dieselbe Bedeutung.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele](../home.md): [!DNL Destinations] sind vordefinierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Ihren Datenfluss mithilfe der [!DNL Flow Service] -API erfolgreich aktualisieren zu können.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmte virtuelle Sandboxes isoliert. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Wenn die Kopfzeile `x-sandbox-name` nicht angegeben ist, werden Anforderungen unter der Sandbox `prod` aufgelöst.

Für alle Anfragen, die eine Payload enthalten (`POST`, `PUT`, `PATCH`), ist eine zusätzliche Kopfzeile vom Medientyp erforderlich:

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
| `{FLOW_ID}` | Der eindeutige `id` -Wert für den Ziel-Datenfluss, den Sie abrufen möchten. |

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

Eine erfolgreiche Antwort gibt die aktuellen Details Ihres Datenflusses zurück, einschließlich der Version, der eindeutigen Kennung (`id`) und anderer relevanter Informationen. Am relevantesten für dieses Tutorial sind die in der Antwort unten hervorgehobenen Ziel- und Basis-Verbindungs-IDs. Sie verwenden diese IDs in den nächsten Abschnitten, um verschiedene Komponenten der Zielverbindung zu aktualisieren.

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

Die Komponenten einer Zielverbindung unterscheiden sich je nach Ziel. Beispielsweise können Sie bei [!DNL Amazon S3] -Zielen den Behälter und den Pfad aktualisieren, in den Dateien exportiert werden. Für [!DNL Pinterest] -Ziele können Sie Ihre [!DNL Pinterest Advertiser ID] aktualisieren und für [!DNL Google Customer Match] Ihre [!DNL Pinterest Account ID].

Um Komponenten einer Zielverbindung zu aktualisieren, führen Sie eine `PATCH` -Anfrage an den `/targetConnections/{TARGET_CONNECTION_ID}` -Endpunkt aus und geben Sie dabei Ihre Ziel-Verbindungs-ID, -Version und die neuen Werte ein, die Sie verwenden möchten. Denken Sie daran, dass Sie Ihre Ziel-Verbindungs-ID im vorherigen Schritt erhalten haben, als Sie einen vorhandenen Datenfluss zu Ihrem gewünschten Ziel überprüft haben.

>[!IMPORTANT]
>
>Die Kopfzeile `If-Match` ist bei einer `PATCH` -Anfrage erforderlich. Der Wert für diesen Header ist die eindeutige Version der Zielverbindung, die Sie aktualisieren möchten. Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung einer Flussentität wie Datenfluss, Zielverbindung und anderen aktualisiert.
>
> Um die neueste Version des eTag-Werts zu erhalten, stellen Sie eine GET-Anfrage an den `/targetConnections/{TARGET_CONNECTION_ID}` -Endpunkt, wobei `{TARGET_CONNECTION_ID}` die Ziel-Verbindungs-ID ist, die Sie aktualisieren möchten.
>
> Stellen Sie sicher, dass Sie den Wert der Kopfzeile `If-Match` in doppelte Anführungszeichen setzen, wie in den Beispielen unten bei der Durchführung von `PATCH` -Anfragen.

Im Folgenden finden Sie einige Beispiele für die Aktualisierung von Parametern in der Zielverbindungsspezifikation für verschiedene Zieltypen. Die allgemeine Regel zum Aktualisieren von Parametern für ein Ziel lautet jedoch wie folgt:

Rufen Sie die Datenfluss-ID der Verbindung ab > rufen Sie die Zielverbindungs-ID ab > `PATCH` die Zielverbindung mit aktualisierten Werten für die gewünschten Parameter.

>[!BEGINSHADEBOX]

**API-Format**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

Die folgende Anfrage aktualisiert die Parameter `bucketName` und `path` einer [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) -Zielverbindung.

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

Bei einer erfolgreichen Antwort werden Ihre Ziel-Verbindungs-ID und ein aktualisiertes Etag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] -API richten und dabei Ihre Ziel-Verbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager und Google Ad Manager 360]

**Anfrage**

Die folgende Anfrage aktualisiert die Parameter einer [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) - oder [[!DNL Google Ad Manager 360] Ziel](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) -Verbindung, um das neue Feld [**[!UICONTROL Zielgruppen-ID an Zielgruppenname anhängen]**](/help/release-notes/2023/april-2023.md#destinations) hinzuzufügen.

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

Bei einer erfolgreichen Antwort werden Ihre Ziel-Verbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] -API richten und dabei Ihre Ziel-Verbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Anfrage**

Die folgende Anfrage aktualisiert den Parameter `advertiserId` einer [[!DNL Pinterest] Zielverbindung](/help/destinations/catalog/advertising/pinterest.md#parameters).

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

Bei einer erfolgreichen Antwort werden Ihre Ziel-Verbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] -API richten und dabei Ihre Ziel-Verbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Bearbeiten von Basisverbindungskomponenten (Authentifizierungsparameter und andere Komponenten) {#patch-base-connection}

Bearbeiten Sie die Basisverbindung, wenn Sie die Anmeldeinformationen eines Ziels aktualisieren möchten. Die Komponenten einer Basisverbindung unterscheiden sich je nach Ziel. Beispielsweise können Sie bei [!DNL Amazon S3] -Zielen den Zugriffsschlüssel und den geheimen Schlüssel auf Ihren [!DNL Amazon S3] -Speicherort aktualisieren.

Um Komponenten einer Basisverbindung zu aktualisieren, führen Sie eine `PATCH` -Anfrage an den `/connections` -Endpunkt aus und geben Sie dabei Ihre Basis-Verbindungs-ID, -Version und die neuen Werte ein, die Sie verwenden möchten.

Denken Sie daran, dass Sie Ihre Basis-Verbindungs-ID in einem [vorherigen Schritt](#look-up-dataflow-details) erhalten haben, als Sie einen vorhandenen Datenfluss zum gewünschten Ziel für den Parameter `baseConnection` überprüft haben.

>[!IMPORTANT]
>
>Die Kopfzeile `If-Match` ist bei einer `PATCH` -Anfrage erforderlich. Der Wert für diesen Header ist die eindeutige Version der Basisverbindung, die Sie aktualisieren möchten. Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung einer Flussentität wie Datenfluss, Basisverbindung usw. aktualisiert.
>
> Um die neueste Version des Etag-Werts zu erhalten, stellen Sie eine GET-Anfrage an den `/connections/{BASE_CONNECTION_ID}` -Endpunkt, wobei `{BASE_CONNECTION_ID}` die Basisverbindungs-ID ist, die Sie aktualisieren möchten.
>
> Stellen Sie sicher, dass Sie den Wert der Kopfzeile `If-Match` in doppelte Anführungszeichen setzen, wie in den Beispielen unten bei der Durchführung von `PATCH` -Anfragen.

Im Folgenden finden Sie einige Beispiele für die Aktualisierung von Parametern in der Basisverbindungsspezifikation für verschiedene Typen von Zielen. Die allgemeine Regel zum Aktualisieren von Parametern für ein Ziel lautet jedoch wie folgt:

Rufen Sie die Datenfluss-ID der Verbindung ab > rufen Sie die Basisverbindungs-ID ab > `PATCH` die Basisverbindung mit aktualisierten Werten für die gewünschten Parameter.

>[!BEGINSHADEBOX]

**API-Format**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

Die folgende Anfrage aktualisiert die Parameter `accessId` und `secretKey` einer [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) -Zielverbindung.

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

Bei einer erfolgreichen Antwort werden Ihre Basisverbindungs-ID und ein aktualisiertes E-Tag angegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] -API richten und dabei Ihre Basis-Verbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**Anfrage**

Die folgende Anfrage aktualisiert die Parameter einer [[!DNL Azure Blob] Ziel](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) -Verbindung, um die Verbindungszeichenfolge zu aktualisieren, die für die Verbindung mit einer Azure Blob-Instanz erforderlich ist.

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

Bei einer erfolgreichen Antwort werden Ihre Basisverbindungs-ID und ein aktualisiertes E-Tag angegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] -API richten und dabei Ihre Basis-Verbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Experience Platform API-Fehlermeldungsprinzipien. Weitere Informationen zur Interpretation von Fehlerantworten finden Sie unter [API-Status-Codes](/help/landing/troubleshooting.md#api-status-codes) und [Fehler in der Anforderungsheader](/help/landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfahren, wie Sie verschiedene Komponenten einer Zielverbindung mit der [!DNL Flow Service] -API aktualisieren. Weitere Informationen zu Zielen finden Sie in der [Zielübersicht](../home.md).
