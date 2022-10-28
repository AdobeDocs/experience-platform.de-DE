---
keywords: Experience Platform;Startseite;beliebte Themen;
solution: Experience Platform
title: Verbinden der Dateneinstiegszone mit Adobe Experience Platform mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API Adobe Experience Platform mit Data Landing Zone verbinden.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 20%

---

# Verbinden [!DNL Data Landing Zone] Adobe Experience Platform mithilfe der Flow Service-API

[!DNL Data Landing Zone] ist eine sichere, Cloud-basierte Dateispeicheranlage, mit der Dateien in Adobe Experience Platform importiert werden können. Daten werden automatisch aus der [!DNL Data Landing Zone] nach sieben Tagen.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer [!DNL Data Landing Zone] Quellverbindung mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Dieses Tutorial enthält auch Anweisungen zum Abrufen Ihrer [!DNL Data Landing Zone], sowie das Anzeigen und Aktualisieren Ihrer Anmeldedaten.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich eine [!DNL Data Landing Zone] Quellverbindung mithilfe der [!DNL Flow Service] API.

Für dieses Tutorial müssen Sie außerdem das Handbuch lesen unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md) , um zu erfahren, wie Sie sich bei Platform-APIs authentifizieren und die in der Dokumentation bereitgestellten Beispielaufrufe interpretieren.

## Eine verwendbare Landingzone abrufen

Der erste Schritt bei der Verwendung von APIs für den Zugriff [!DNL Data Landing Zone] ist es, eine GET-Anfrage an die `/landingzone` Endpunkt der [!DNL Connectors] API bei Bereitstellung `type=user_drop_zone` als Teil Ihres Anfrage-Headers.

**API-Format**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Header | Beschreibung |
| --- | --- |
| `user_drop_zone` | Die `user_drop_zone` Mit dem -Typ kann die API einen Einstiegszonen-Container von den anderen für Sie verfügbaren Behältertypen unterscheiden. |

**Anfrage**

Mit der folgenden Anfrage wird eine vorhandene Landingzone abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `containerTTL` | Die Ablaufzeit (in Tagen), die auf Ihre Daten in der Landingzone angewendet wird. Jede Person innerhalb einer bestimmten Landingzone wird nach sieben Tagen gelöscht. |

## Abrufen [!DNL Data Landing Zone] Anmeldeinformationen

So rufen Sie Anmeldeinformationen für ein [!DNL Data Landing Zone], stellen Sie eine GET-Anfrage an die `/credentials` Endpunkt der [!DNL Connectors] API.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Antwort**

Die folgende Antwort gibt die Anmeldeinformationen für Ihre Landingzone zurück, einschließlich Ihrer aktuellen `SASToken` und `SASUri`sowie `storageAccountName` , der Ihrem Landingzone-Container entspricht.

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


## Aktualisieren [!DNL Data Landing Zone] Anmeldeinformationen

Sie können Ihre `SASToken` , indem Sie eine POST an die `/credentials` Endpunkt der [!DNL Connectors] API.

**API-Format**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Header | Beschreibung |
| --- | --- |
| `user_drop_zone` | Die `user_drop_zone` Mit dem -Typ kann die API einen Einstiegszonen-Container von den anderen für Sie verfügbaren Behältertypen unterscheiden. |
| `refresh` | Die `refresh` Mit dieser Aktion können Sie Ihre Landingzone-Anmeldedaten zurücksetzen und automatisch eine neue `SASToken`. |

**Anfrage**

Mit der folgenden Anfrage werden Ihre Landingzone-Anmeldedaten aktualisiert.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Antwort**

Die folgende Antwort gibt aktualisierte Werte für Ihre `SASToken` und `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Dateistruktur und Inhalt der Landingzone

Sie können die Dateistruktur und den Inhalt Ihrer Landingzone durchsuchen, indem Sie eine GET-Anfrage an die `connectionSpecs` Endpunkt der [!DNL Flow Service] API.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array von Dateien und Ordnern zurück, die im abgefragten Ordner gefunden wurden. Beachten Sie die `path` -Eigenschaft der Datei, die Sie hochladen möchten, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der abgefragten Datei zurück, einschließlich Dateinamen und Datentypen.

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

### Verwendung `determineProperties` zur automatischen Erkennung der Dateieigenschaftsinformationen eines [!DNL Data Landing Zone]

Sie können die `determineProperties` Parameter zur automatischen Erkennung von Eigenschafteninformationen des Dateiinhalts Ihrer [!DNL Data Landing Zone] wenn Sie einen GET-Aufruf durchführen, um den Inhalt und die Struktur Ihrer Quelle zu untersuchen.

#### `determineProperties` Anwendungsfälle

In der folgenden Tabelle werden verschiedene Szenarien beschrieben, auf die Sie bei der Verwendung der `determineProperties` Abfrageparameter oder manuelles Bereitstellen von Informationen zu Ihrer Datei.

| `determineProperties` | `queryParams` | Antwort |
| --- | --- | --- |
| True | K. A. | Wenn `determineProperties` wird als Abfrageparameter bereitgestellt, wird die Erkennung der Dateieigenschaften durchgeführt und die Antwort gibt eine neue `properties` -Schlüssel, der Informationen zum Dateityp, zum Komprimierungstyp und zum Spaltentrennzeichen enthält. |
| K. A. | True | Wenn die Werte für Dateityp, Komprimierungstyp und Spaltentrennzeichen manuell als Teil von `queryParams`, werden sie zum Generieren des Schemas verwendet und dieselben Eigenschaften werden als Teil der Antwort zurückgegeben. |
| True | True | Wenn beide Optionen gleichzeitig ausgeführt werden, wird ein Fehler zurückgegeben. |
| K. A. | K. A. | Wenn keine der beiden Optionen angegeben wird, wird ein Fehler zurückgegeben, da es keine Möglichkeit gibt, Eigenschaften für die Antwort abzurufen. |

**API-Format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `determineProperties` | Dieser Abfrageparameter ermöglicht die [!DNL Flow Service] API zur Erkennung von Informationen zu den Eigenschaften Ihrer Datei, einschließlich Informationen zum Dateityp, zum Komprimierungstyp und zum Spaltentrennzeichen. | `true` |

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der abgefragten Datei einschließlich Dateinamen und Datentypen sowie eine `properties` Schlüssel, enthält Informationen zu `fileType`, `compressionType`und `columnDelimiter`.

+++Hier klicken

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| Eigenschaft | Beschreibung |
| --- | --- |
| `properties.fileType` | Der entsprechende Dateityp der abgefragten Datei. Folgende Dateitypen werden unterstützt: `delimited`, `json`und `parquet`. |
| `properties.compressionType` | Der entsprechende Komprimierungstyp, der für die abgefragte Datei verwendet wird. Folgende Komprimierungstypen werden unterstützt: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Das entsprechende Spaltentrennzeichen, das für die abgefragte Datei verwendet wird. Jeder einzelne Zeichenwert ist als Spaltentrennzeichen zulässig. Der Standardwert ist ein Komma `(,)`. |


## Erstellen einer Quellverbindung

Eine Quellverbindung erstellt und verwaltet die Verbindung zu der externen Quelle, aus der Daten erfasst werden. Eine Quellverbindung besteht aus Informationen wie der Datenquelle, dem Datenformat und der Kennung der Quellverbindung, die zum Erstellen eines Datenflusses erforderlich ist. Eine Quellverbindungsinstanz ist für einen Mandanten und eine IMS-Organisation spezifisch.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Der Name Ihres [!DNL Data Landing Zone] Quellverbindung. |
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

In diesem Tutorial haben Sie Ihre [!DNL Data Landing Zone] Anmeldeinformationen, die Dateistruktur durchsucht, um die Datei zu finden, die Sie in Platform laden möchten, und eine Quellverbindung erstellt, um Ihre Daten an Platform zu übertragen. Sie können jetzt mit dem nächsten Tutorial fortfahren, in dem Sie erfahren, wie Sie [Erstellen Sie einen Datenfluss, um Cloud-Speicherdaten mit der [!DNL Flow Service] API](../../collect/cloud-storage.md).
