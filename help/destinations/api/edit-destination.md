---
solution: Experience Platform
title: Bearbeiten von Zielverbindungen mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie verschiedene Komponenten einer Zielverbindung mithilfe der Flow Service-API bearbeiten können.
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 25%

---

# Bearbeiten von Zielverbindungen mithilfe der Flow Service-API

In diesem Tutorial werden die Schritte zum Bearbeiten verschiedener Komponenten einer Zielverbindung beschrieben. Erfahren Sie, wie Sie Authentifizierungsdaten, den Exportspeicherort und mehr mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) aktualisieren.

>[!NOTE]
>
> Die in diesem Tutorial beschriebenen Bearbeitungsvorgänge werden derzeit nur über die Flow Service-API unterstützt.

## Erste Schritte {#get-started}

Für dieses Tutorial benötigen Sie eine gültige Datenfluss-ID. Wenn Sie keine gültige Datenfluss-ID haben, wählen Sie Ihr Ziel aus dem [Zielkatalog](../catalog/overview.md) und führen Sie die Schritte aus, die [Herstellen einer Verbindung mit dem Ziel](../ui/connect-destination.md) und [Aktivieren von Daten](../ui/activation-overview.md) beschrieben sind, bevor Sie dieses Tutorial ausführen.

>[!NOTE]
>
> Die Begriffe *Fluss* und *Datenfluss* werden in diesem Tutorial synonym verwendet. Im Kontext dieses Tutorials haben sie dieselbe Bedeutung.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele](../home.md): [!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Ihren Datenfluss mithilfe der [!DNL Flow Service]-API erfolgreich aktualisieren zu können.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um Experience Platform-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, sind in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an Experience Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Wenn die `x-sandbox-name`-Kopfzeile nicht angegeben ist, werden Anfragen unter der `prod`-Sandbox aufgelöst.

Für alle Anfragen mit einer Payload (`POST`, `PUT`, `PATCH`) ist eine zusätzliche Kopfzeile vom Typ „Medien“ erforderlich:

* `Content-Type: application/json`

## Nachschlagen von Datenflussdetails {#look-up-dataflow-details}

Der erste Schritt bei der Bearbeitung Ihrer Zielverbindung besteht darin, Datenflussdetails mit Ihrer Fluss-ID abzurufen. Sie können die aktuellen Details eines vorhandenen Datenflusses anzeigen, indem Sie eine GET-Anfrage an den `/flows`-Endpunkt stellen.

>[!TIP]
>
>Sie können die Experience Platform-Benutzeroberfläche verwenden, um die gewünschte Datenfluss-ID eines Ziels abzurufen. Gehen Sie **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]**, wählen Sie den gewünschten Zieldatenfluss aus und suchen Sie die Ziel-ID in der rechten Leiste. Die Ziel-ID ist der Wert, den Sie als Fluss-ID im nächsten Schritt verwenden werden.
>
> ![Abrufen der Ziel-ID über die Experience Platform-Benutzeroberfläche](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API-Format**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige `id` für den Ziel-Datenfluss, den Sie abrufen möchten. |

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

Bei einer erfolgreichen Antwort werden die aktuellen Details Ihres Datenflusses zurückgegeben, einschließlich der Version, der eindeutigen Kennung (`id`) und anderer relevanter Informationen. Am relevantesten für dieses Tutorial sind die Zielverbindungs- und Basisverbindungs-IDs, die in der folgenden Antwort hervorgehoben sind. Sie werden diese IDs in den nächsten Abschnitten verwenden, um verschiedene Komponenten der Zielverbindung zu aktualisieren.

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

## Bearbeiten der Zielverbindungskomponenten (Speicherort und andere Komponenten) {#patch-target-connection}

Die Komponenten einer Zielverbindung unterscheiden sich je nach Ziel. Beispielsweise können Sie für [!DNL Amazon S3] Ziele den Bucket und den Pfad aktualisieren, in den Dateien exportiert werden. Für [!DNL Pinterest] Ziele können Sie Ihre [!DNL Pinterest Advertiser ID] aktualisieren und für [!DNL Google Customer Match] können Sie Ihre [!DNL Pinterest Account ID] aktualisieren.

Um Komponenten einer Zielverbindung zu aktualisieren, führen Sie eine `PATCH`-Anfrage an den Endpunkt `/targetConnections/{TARGET_CONNECTION_ID}` aus und geben Sie dabei Ihre Zielverbindungs-ID, die Version und die neuen Werte an, die Sie verwenden möchten. Denken Sie daran, dass Sie im vorherigen Schritt Ihre Zielverbindungs-ID erhalten haben, als Sie einen vorhandenen Datenfluss zu Ihrem gewünschten Ziel überprüft haben.

>[!IMPORTANT]
>
>Bei einer `PATCH`-Anfrage ist die `If-Match`-Kopfzeile erforderlich. Der Wert für diese Kopfzeile ist die eindeutige Version der Zielverbindung, die Sie aktualisieren möchten. Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung einer Flussentität aktualisiert, z. B. Datenfluss, Zielverbindung und andere.
>
> Um die neueste Version des eTag-Werts abzurufen, führen Sie eine GET-Anfrage an den `/targetConnections/{TARGET_CONNECTION_ID}`-Endpunkt durch, wobei `{TARGET_CONNECTION_ID}` die Zielverbindungs-ID ist, die Sie aktualisieren möchten.
>
> Stellen Sie sicher, dass Sie bei `PATCH` Anfragen den Wert des `If-Match`-Headers in doppelte Anführungszeichen setzen, wie in den Beispielen unten.

Im Folgenden finden Sie einige Beispiele für die Aktualisierung von Parametern in der Zielverbindungsspezifikation für verschiedene Zieltypen. Die allgemeine Regel zum Aktualisieren der Parameter für jedes Ziel lautet jedoch wie folgt:

Abrufen der Datenfluss-ID der Verbindung > Abrufen der Zielverbindungs-ID > `PATCH` der Zielverbindung mit aktualisierten Werten für die gewünschten Parameter.

>[!BEGINSHADEBOX]

**API-Format**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

Die folgende Anfrage aktualisiert die `bucketName`- und `path` einer [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) Zielverbindung.

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

Bei einer erfolgreichen Antwort werden Ihre Zielverbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Zielverbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager und Google Ad Manager 360]

**Anfrage**

Die folgende Anfrage aktualisiert die Parameter einer [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md)- oder [[!DNL Google Ad Manager 360] Ziel](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details)-Verbindung, um das neue Feld [**[!UICONTROL Zielgruppen-ID an Zielgruppennamen anhängen]**](/help/release-notes/2023/april-2023.md#destinations) hinzuzufügen.

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

Bei einer erfolgreichen Antwort werden Ihre Zielverbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Zielverbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Anfrage**

Die folgende Anfrage aktualisiert den `advertiserId`-Parameter einer [[!DNL Pinterest] Zielverbindung](/help/destinations/catalog/advertising/pinterest.md#parameters).

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

Bei einer erfolgreichen Antwort werden Ihre Zielverbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Zielverbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Bearbeiten von Basisverbindungskomponenten (Authentifizierungsparameter und andere Komponenten) {#patch-base-connection}

Bearbeiten Sie die Basisverbindung, wenn Sie die Anmeldeinformationen eines Ziels aktualisieren möchten. Die Komponenten einer Basisverbindung unterscheiden sich je nach Ziel. Beispielsweise können Sie für [!DNL Amazon S3] Ziele den Zugriffsschlüssel und den geheimen Schlüssel für Ihren [!DNL Amazon S3] Speicherort aktualisieren.

Um Komponenten einer Basisverbindung zu aktualisieren, führen Sie eine `PATCH`-Anfrage an den `/connections`-Endpunkt durch und geben Sie dabei Ihre Basisverbindungs-ID, die Version und die neuen Werte an, die Sie verwenden möchten.

Denken Sie daran, dass Sie Ihre Basisverbindungs-ID in einem [vorherigen Schritt](#look-up-dataflow-details) erhalten haben, als Sie einen vorhandenen Datenfluss zu Ihrem gewünschten Ziel für die `baseConnection` überprüft haben.

>[!IMPORTANT]
>
>Bei einer `PATCH`-Anfrage ist die `If-Match`-Kopfzeile erforderlich. Der Wert für diese Kopfzeile ist die eindeutige Version der Basisverbindung, die Sie aktualisieren möchten. Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung einer Fluss-Entität aktualisiert, z. B. Datenfluss, Basisverbindung und andere.
>
> Um die neueste Version des Etag-Werts abzurufen, führen Sie eine GET-Anfrage an den `/connections/{BASE_CONNECTION_ID}`-Endpunkt durch, wobei `{BASE_CONNECTION_ID}` die Basisverbindungs-ID ist, die Sie aktualisieren möchten.
>
> Stellen Sie sicher, dass Sie bei `PATCH` Anfragen den Wert des `If-Match`-Headers in doppelte Anführungszeichen setzen, wie in den Beispielen unten.

Im Folgenden finden Sie einige Beispiele für die Aktualisierung von Parametern in der Basisverbindungsspezifikation für verschiedene Zieltypen. Die allgemeine Regel zum Aktualisieren der Parameter für jedes Ziel lautet jedoch wie folgt:

Abrufen der Datenfluss-ID der Verbindung > Abrufen der Basisverbindungs-ID > `PATCH` der Basisverbindung mit aktualisierten Werten für die gewünschten Parameter.

>[!BEGINSHADEBOX]

**API-Format**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

Die folgende Anfrage aktualisiert die `accessId`- und `secretKey` einer [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) Zielverbindung.

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

Bei einer erfolgreichen Antwort werden Ihre Basisverbindungs-ID und ein aktualisiertes E-Tag angegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Basisverbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**Anfrage**

Die folgende Anfrage aktualisiert die Parameter einer [[!DNL Azure Blob] Ziel](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate)-Verbindung, um die zum Herstellen einer Verbindung mit einer Azure Blob-Instanz erforderliche Verbindungszeichenfolge zu aktualisieren.

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

Bei einer erfolgreichen Antwort werden Ihre Basisverbindungs-ID und ein aktualisiertes E-Tag angegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Basisverbindungs-ID angeben.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Weitere Informationen [ Interpretieren von Fehlerantworten finden Sie unter ](/help/landing/troubleshooting.md#api-status-codes)API-Status-Codes[ und ](/help/landing/troubleshooting.md#request-header-errors)Fehler in der Anfragekopfzeile im Handbuch zur Fehlerbehebung bei Experience Platform .

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie gelernt, wie Sie verschiedene Komponenten einer Zielverbindung mithilfe der [!DNL Flow Service]-API aktualisieren können. Weitere Informationen zu Zielen finden Sie unter [Ziele - Übersicht](../home.md).
