---
keywords: Experience Platform;Home;beliebte Themen;
solution: Experience Platform
title: Verbinden der Dateneinstiegszone mit Adobe Experience Platform mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API Adobe Experience Platform mit Data Landing Zone verbinden.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 9%

---

# Verbinden von [!DNL Data Landing Zone] mit Adobe Experience Platform mithilfe der Flow Service-API

[!DNL Data Landing Zone] ist eine Cloud-basierte Datenspeicheranlage für temporäre Dateispeicher, die mit Adobe Experience Platform bereitgestellt wird. Daten werden nach sieben Tagen automatisch aus dem [!DNL Data Landing Zone] gelöscht.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer [!DNL Data Landing Zone]-Quellverbindung mit der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Dieses Tutorial enthält außerdem Anweisungen zum Abrufen Ihrer [!DNL Data Landing Zone]-Anmeldedaten sowie zum Anzeigen und Aktualisieren Ihrer Anmeldedaten.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine [!DNL Data Landing Zone]-Quellverbindung erstellen zu können.

Für dieses Tutorial müssen Sie außerdem das Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md) lesen, um zu erfahren, wie Sie sich bei Platform-APIs authentifizieren und die in der Dokumentation bereitgestellten Beispielaufrufe interpretieren können.

## Eine verwendbare Landingzone abrufen

Der erste Schritt bei der Verwendung von APIs für den Zugriff auf [!DNL Data Landing Zone] besteht darin, eine GET-Anfrage an den `/landingzone`-Endpunkt der [!DNL Connectors]-API zu stellen und dabei `type=user_drop_zone` als Teil Ihres Anfrage-Headers anzugeben.

**API-Format**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Header | Beschreibung |
| --- | --- |
| `user_drop_zone` | Der Typ `user_drop_zone` ermöglicht es der API, einen Einstiegszonen-Container von den anderen für Sie verfügbaren Behältertypen zu unterscheiden. |

**Anfrage**

Mit der folgenden Anfrage wird eine vorhandene Landingzone abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Antwort**

Die folgende Antwort gibt Informationen zu einer Landingzone zurück, einschließlich der zugehörigen `containerName` und `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `containerName` | Der Name der abgerufenen Landingzone. |
| `containerTTL` | Die Time-to-Live-Einstellung, die auf Ihre Daten in der Landingzone angewendet wird. Jede Person innerhalb einer bestimmten Landingzone wird nach sieben Tagen gelöscht. |

## Abrufen von [!DNL Data Landing Zone]-Anmeldeinformationen

Um Anmeldeinformationen für eine [!DNL Data Landing Zone] abzurufen, stellen Sie eine GET-Anfrage an den `/credentials`-Endpunkt der [!DNL Connectors]-API.

**API-Format**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**Anfrage**

Im folgenden Anfragebeispiel werden Anmeldeinformationen für eine vorhandene Landingzone abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Antwort**

Die folgende Antwort gibt die Anmeldeinformationen für Ihre Einstiegszone zurück, einschließlich Ihrer aktuellen `SASToken`- und `SASUri`-Anmeldeinformationen sowie der `storageAccountName`-Kennung, die Ihrem Einstiegszonen-Container entspricht.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `containerName` | Der Name Ihrer Landingzone. |
| `SASToken` | Das Token für die gemeinsame Zugriffssignatur für Ihre Landingzone. Diese Zeichenfolge enthält alle Informationen, die zum Autorisieren einer Anfrage erforderlich sind. |
| `SASUri` | Der URI der Freigegebenen Zugriffssignatur für Ihre Landingzone. Diese Zeichenfolge ist eine Kombination aus dem URI für die Landingzone, für die Sie authentifiziert werden, und dem zugehörigen SAS-Token. |


## Aktualisieren der [!DNL Data Landing Zone]-Anmeldedaten

Sie können `SASToken` aktualisieren, indem Sie eine POST-Anfrage an den `/credentials`-Endpunkt der [!DNL Connectors]-API richten.

**API-Format**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Header | Beschreibung |
| --- | --- |
| `user_drop_zone` | Der Typ `user_drop_zone` ermöglicht es der API, einen Einstiegszonen-Container von den anderen für Sie verfügbaren Behältertypen zu unterscheiden. |
| `refresh` | Mit der Aktion `refresh` können Sie Ihre Landingzone-Anmeldedaten zurücksetzen und automatisch ein neues `SASToken` generieren. |

**Anfrage**

Mit der folgenden Anfrage werden Ihre Landingzone-Anmeldedaten aktualisiert.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Antwort**

Die folgende Antwort gibt aktualisierte Werte für `SASToken` und `SASUri` zurück.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Dateistruktur und Inhalt der Landingzone

Sie können die Dateistruktur und den Inhalt Ihrer Landingzone durchsuchen, indem Sie eine GET-Anfrage an den Endpunkt `connectionSpecs` der [!DNL Flow Service]-API richten.

**API-Format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | Die Verbindungsspezifikations-ID, die [!DNL Data Landing Zone] entspricht. Diese feste ID lautet: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array von Dateien und Ordnern zurück, die im abgefragten Ordner gefunden wurden. Notieren Sie sich die `path`-Eigenschaft der Datei, die Sie hochladen möchten, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## Dateistruktur und Inhalt der Landingzone-Vorschau

Um die Dateistruktur in Ihrer Landingzone zu überprüfen, führen Sie eine GET-Anfrage aus, geben Sie dabei den Pfad der Datei an und geben Sie ihn als Abfrageparameter ein.

**API-Format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | Die Verbindungsspezifikations-ID, die [!DNL Data Landing Zone] entspricht. Diese feste ID lautet: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | Der Typ des Objekts, auf das Sie zugreifen möchten. | `file` |
| `{OBJECT}` | Pfad und Name des Objekts, auf das Sie zugreifen möchten. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | Der Dateityp. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Ein boolean -Wert, der definiert, ob die Dateivorschau unterstützt wird. | </ul><li>`true`</li><li>`false`</li></ul> |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der abgefragten Datei zurück, einschließlich Tabellennamen und Datentypen.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

## Quellverbindung erstellen

Eine Quellverbindung erstellt und verwaltet die Verbindung zur externen Quelle, von der aus Daten erfasst werden. Eine Quellverbindung besteht aus Informationen wie der Datenquelle, dem Datenformat und der Kennung der Quellverbindung, die zum Erstellen eines Datenflusses erforderlich ist. Eine Quellverbindungsinstanz ist für einen Mandanten und eine IMS-Organisation spezifisch.

Um eine Quellverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/sourceConnections`-Endpunkt der [!DNL Flow Service]-API.


**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer [!DNL Data Landing Zone]-Quellverbindung. |
| `data.format` | Das Format der Daten, die Sie an Platform übermitteln möchten. |
| `params.path` | Der Pfad zur Datei, die Sie in Platform laden möchten. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die [!DNL Data Landing Zone] entspricht. Diese feste ID lautet: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist im nächsten Tutorial zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie Ihre [!DNL Data Landing Zone]-Anmeldeinformationen abgerufen, die Dateistruktur durchsucht, um die Datei zu finden, die Sie an Platform übermitteln möchten, und eine Quellverbindung erstellt, um Ihre Daten an Platform zu übertragen. Sie können jetzt mit dem nächsten Tutorial fortfahren, in dem Sie erfahren, wie Sie [einen Datenfluss erstellen, um Cloud-Speicherdaten mit der  [!DNL Flow Service] API](../../collect/cloud-storage.md) an Platform zu bringen.
