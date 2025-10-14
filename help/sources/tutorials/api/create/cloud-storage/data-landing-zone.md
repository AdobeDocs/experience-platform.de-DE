---
title: Verbinden der Data Landing Zone mit Adobe Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit der Data Landing Zone verbinden.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 13%

---

# Verbinden von [!DNL Data Landing Zone] mit Adobe Experience Platform mithilfe der Flow Service-API

>[!IMPORTANT]
>
>Diese Seite ist spezifisch für den [!DNL Data Landing Zone]-Quell *Connector* Experience Platform. Informationen zum Herstellen einer Verbindung zum [!DNL Data Landing Zone]-*-*-Connector finden Sie auf [[!DNL Data Landing Zone] Zieldokumentationsseite](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] ist eine sichere, Cloud-basierte Dateispeichereinrichtung, um Dateien in Adobe Experience Platform zu importieren. Daten werden nach sieben Tagen automatisch aus dem [!DNL Data Landing Zone] gelöscht.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer [!DNL Data Landing Zone]-Quellverbindung mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Dieses Tutorial enthält auch Anweisungen zum Abrufen Ihrer [!DNL Data Landing Zone] sowie zum Anzeigen und Aktualisieren Ihrer Anmeldeinformationen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Für dieses Tutorial müssen Sie auch das Handbuch unter [Erste Schritte mit Experience Platform-APIs](../../../../../landing/api-guide.md) lesen, um zu erfahren, wie Sie sich bei Experience Platform-APIs authentifizieren und die in der Dokumentation bereitgestellten Beispielaufrufe interpretieren.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine [!DNL Data Landing Zone]-Quellverbindung erstellen zu können.

## Abrufen einer verwendbaren Landing Zone

>[!IMPORTANT]
>
>Sie müssen über die Zugriffssteuerungsberechtigung **[!UICONTROL Quellen verwalten]** verfügen, um die [!DNL Data Landing Zone]-APIs verwenden und `type=user_drop_zone` abrufen zu können. Weitere Informationen finden Sie unter [Zugriffskontrolle - Übersicht](../../../../../access-control/home.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Der erste Schritt bei der Verwendung von APIs für den Zugriff auf [!DNL Data Landing Zone] besteht darin, eine GET-Anfrage an den `/landingzone`-Endpunkt der [!DNL Connectors]-API zu stellen und dabei `type=user_drop_zone` als Teil Ihres Anfrage-Headers bereitzustellen.

**API-Format**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| Kopfzeilen | Beschreibung |
| --- | --- |
| `user_drop_zone` | Der `user_drop_zone` ermöglicht es der API, einen Landing Zone-Container von den anderen Containertypen zu unterscheiden, die Ihnen zur Verfügung stehen. |

**Anfrage**

Mit der folgenden Anfrage wird eine vorhandene Landing Zone abgerufen.

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

Je nach Anbieter gibt eine erfolgreiche Anfrage Folgendes zurück:

>[!BEGINTABS]

>[!TAB Antwort auf Azure]

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `containerName` | Der Name der Landing Zone, die Sie abgerufen haben. |
| `containerTTL` | Die Gültigkeitsdauer (in Tagen), die auf Ihre Daten in der Landing Zone angewendet wird. Alle innerhalb einer bestimmten Landing Zone werden nach sieben Tagen gelöscht. |


>[!TAB Antwort auf AWS]

```json
{
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "dlz-adf-connectors"
  },
  "dataTTL": {
    "timeUnit": "days",
    "timeQuantity": 7
  },
  "dlzProvider": "Amazon S3"
}
```

>[!ENDTABS]


## [!DNL Data Landing Zone] abrufen

Um Anmeldeinformationen für eine [!DNL Data Landing Zone] abzurufen, stellen Sie eine GET-Anfrage an den `/credentials`-Endpunkt der [!DNL Connectors]-API.

**API-Format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**Anfrage**

Im folgenden Anfragebeispiel werden Anmeldeinformationen für eine vorhandene Landing Zone abgerufen.

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

Je nach Anbieter gibt eine erfolgreiche Anfrage Folgendes zurück:

>[!BEGINTABS]

>[!TAB Antwort auf Azure]

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `containerName` | Der Name Ihres [!DNL Data Landing Zone]. |
| `SASToken` | Das Shared Access Signature Token für Ihre [!DNL Data Landing Zone]. Diese Zeichenfolge enthält alle Informationen, die zum Autorisieren einer Anfrage erforderlich sind. |
| `storageAccountName` | Der Name Ihres Speicherkontos. |
| `SASUri` | Der Shared Access Signature-URI für Ihre [!DNL Data Landing Zone]. Diese Zeichenfolge ist eine Kombination aus dem URI zum [!DNL Data Landing Zone], für den Sie authentifiziert werden, und dem entsprechenden SAS-Token. |
| `expiryDate` | Das Datum, an dem Ihr SAS-Token abläuft. Sie müssen Ihr Token vor dem Ablaufdatum aktualisieren, um es weiterhin in Ihrer Anwendung zum Hochladen von Daten in die [!DNL Data Landing Zone] verwenden zu können. Wenn Sie Ihr Token nicht vor dem angegebenen Ablaufdatum manuell aktualisieren, wird es automatisch aktualisiert und ein neues Token bereitgestellt, wenn der Aufruf der GET-Anmeldeinformationen ausgeführt wird. |

>[!TAB Antwort auf AWS]

```json
{
  "credentials": {
    "clientId": "example-client-id",
    "awsAccessKeyId": "example-access-key-id",
    "awsSecretAccessKey": "example-secret-access-key",
    "awsSessionToken": "example-session-token"
  },
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "user_drop_zone"
  },
  "dlzProvider": "Amazon S3",
  "expiryTime": 1735689599
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `credentials.clientId` | Die Client-ID Ihres [!DNL Data Landing Zone] in AWS. |
| `credentials.awsAccessKeyId` | Die Zugriffsschlüssel-ID Ihres [!DNL Data Landing Zone] in AWS. |
| `credentials.awsSecretAccessKey` | Der geheime Zugriffsschlüssel Ihrer [!DNL Data Landing Zone] in AWS. |
| `credentials.awsSessionToken` | Ihr AWS-Sitzungs-Token. |
| `dlzPath.bucketName` | Der Name Ihres AWS-Buckets. |
| `dlzPath.dlzFolder` | Der [!DNL Data Landing Zone] Ordner, auf den Sie zugreifen. |
| `dlzProvider` | Der [!DNL Data Landing Zone], den Sie verwenden. Für Amazon wird dies [!DNL Amazon S3]. |
| `expiryTime` | Die Ablaufzeit in Unix-Zeit. |

>[!ENDTABS]

### Abrufen der erforderlichen Felder mithilfe von APIs

Nachdem Sie Ihr Token generiert haben, können Sie die erforderlichen Felder programmgesteuert abrufen, indem Sie die folgenden Anfragebeispiele verwenden:

>[!BEGINTABS]

>[!TAB Python]

```py
import requests
 
# API endpoint
url = "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone"
 
headers = {
    "Authorization": "{TOKEN}",
    "Content-Type": "application/json",
    "x-gw-ims-org-id": "{ORG_ID}",
    "x-api-key": "{API_KEY}"
}
 
# Send GET request to the API
response = requests.get(url, headers=headers)
 
# Check if the request was successful
if response.status_code == 200:
    # Parse the response as JSON (if applicable)
    data = response.json()
 
    # Print or work with the fetched data 
    print(" Sas Token:", data['SASToken'])
    print(" Container Name:",  data['containerName'])
    print("\n")
 
else:
    # Print an error message if the request failed
    print(f"Failed to fetch data. Status code: {response.status_code}")
    print(f"Response: {response.text}")
```

>[!TAB Java]


```java
package org.example;
 
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
 
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.DefaultHttpClient;
 
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
 
public class Main {
    public static void main(String[] args) {
 
        ObjectMapper objectMapper = new ObjectMapper();
 
        try {
 
            DefaultHttpClient httpClient = new DefaultHttpClient();
            HttpGet getRequest = new HttpGet(
                "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone");
            getRequest.addHeader("accept", "application/json");
            getRequest.addHeader("Authorization","<TOKEN>");
            getRequest.addHeader("Content-Type", "application/json");
            getRequest.addHeader("x-gw-ims-org-id", "<ORG_ID>");
            getRequest.addHeader("x-api-key", "<API_KEY>");
 
            HttpResponse response = httpClient.execute(getRequest);
 
            if (response.getStatusLine().getStatusCode() != 200) {
                throw new RuntimeException("Failed : HTTP error code : "
                    + response.getStatusLine().getStatusCode());
            }
 
            final JsonNode jsonResponse = objectMapper.readTree(response.getEntity().getContent());
 
            System.out.println("\nOutput from API Response .... \n");
            System.out.printf("ContainerName: %s%n", jsonResponse.at("/containerName").textValue());
            System.out.printf("SASToken: %s%n", jsonResponse.at("/SASToken").textValue());
 
            httpClient.getConnectionManager().shutdown();
 
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

>[!ENDTABS]


## Aktualisieren [!DNL Data Landing Zone] Anmeldeinformationen

Sie können Ihre `SASToken` aktualisieren, indem Sie eine POST-Anfrage an den `/credentials`-Endpunkt der [!DNL Connectors]-API stellen.

**API-Format**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Kopfzeilen | Beschreibung |
| --- | --- |
| `user_drop_zone` | Der `user_drop_zone` ermöglicht es der API, einen Landing Zone-Container von den anderen Containertypen zu unterscheiden, die Ihnen zur Verfügung stehen. |
| `refresh` | Mit der `refresh` Aktion können Sie Ihre Anmeldeinformationen für die Landing Zone zurücksetzen und automatisch eine neue `SASToken` generieren. |

**Anfrage**

Die folgende Anfrage aktualisiert Ihre Anmeldeinformationen für die Landing Zone.

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

Die folgende Antwort gibt aktualisierte Werte für Ihre `SASToken` und `SASUri` zurück.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## Dateistruktur und Inhalte der Landing Zone erkunden

Sie können die Dateistruktur und den Inhalt Ihrer Landing Zone untersuchen, indem Sie eine GET-Anfrage an den `connectionSpecs`-Endpunkt der [!DNL Flow Service]-API stellen.

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

Eine erfolgreiche Antwort gibt ein Array von Dateien und Ordnern zurück, die im abgefragten Verzeichnis gefunden wurden. Notieren Sie sich die `path`-Eigenschaft der Datei, die Sie hochladen möchten, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

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

## Vorschau der Dateistruktur und des Inhalts der Landing Zone

Um die Dateistruktur in Ihrer Landing Zone zu überprüfen, führen Sie eine GET-Anfrage aus, wobei Sie den Dateipfad und den Typ als Abfrageparameter angeben.

**API-Format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | Die Verbindungsspezifikations-ID, die [!DNL Data Landing Zone] entspricht. Diese feste ID lautet: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | Der Typ des Objekts, auf das Sie zugreifen möchten. | `file` |
| `{OBJECT}` | Der Pfad und der Name des Objekts, auf das Sie zugreifen möchten. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | Der Typ der Datei. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Ein boolescher Wert, der definiert, ob die Dateivorschau unterstützt wird. | </ul><li>`true`</li><li>`false`</li></ul> |

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

### `determineProperties` verwenden, um Dateieigenschaftsinformationen eines [!DNL Data Landing Zone] automatisch zu erkennen

Sie können den `determineProperties`-Parameter verwenden, um Eigenschafteninformationen des Dateiinhalts Ihrer [!DNL Data Landing Zone] automatisch zu erkennen, wenn Sie einen GET-Aufruf ausführen, um den Inhalt und die Struktur Ihrer Quelle zu untersuchen.

#### `determineProperties` Anwendungsfälle

In der folgenden Tabelle sind verschiedene Szenarien aufgeführt, auf die Sie stoßen können, wenn Sie den `determineProperties` Abfrageparameter verwenden oder manuell Informationen zu Ihrer Datei angeben.

| `determineProperties` | `queryParams` | Antwort |
| --- | --- | --- |
| True | K. A. | Wenn `determineProperties` als Abfrageparameter angegeben wird, erfolgt die Erkennung der Dateieigenschaften, und die Antwort gibt einen neuen `properties` zurück, der Informationen zum Dateityp, zum Komprimierungstyp und zum Spaltentrennzeichen enthält. |
| K. A. | True | Wenn die Werte für Dateityp, Komprimierungstyp und Spaltentrennzeichen manuell als Teil von `queryParams` bereitgestellt werden, werden sie zum Generieren des Schemas verwendet und dieselben Eigenschaften werden als Teil der Antwort zurückgegeben. |
| True | True | Wenn beide Optionen gleichzeitig ausgeführt werden, wird ein Fehler zurückgegeben. |
| K. A. | K. A. | Wenn keine der beiden Optionen bereitgestellt wird, wird ein Fehler zurückgegeben, da es keine Möglichkeit gibt, Eigenschaften für die Antwort abzurufen. |

**API-Format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `determineProperties` | Mit diesem Abfrageparameter kann die [!DNL Flow Service]-API Informationen zu den Eigenschaften Ihrer Datei erkennen, einschließlich Informationen zu Dateityp, Komprimierungstyp und Spaltentrennzeichen. | `true` |

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

Bei einer erfolgreichen Antwort wird die Struktur der abgefragten Datei zurückgegeben, einschließlich Dateinamen und Datentypen sowie eines `properties` Schlüssels, der Informationen zu `fileType`, `compressionType` und `columnDelimiter` enthält.

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
| `properties.fileType` | Der entsprechende Dateityp der abgefragten Datei. Die unterstützten Dateitypen sind: `delimited`, `json` und `parquet`. |
| `properties.compressionType` | Der entsprechende Komprimierungstyp, der für die abgefragte Datei verwendet wird. Folgende Komprimierungstypen werden unterstützt: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Das entsprechende Spaltentrennzeichen, das für die abgefragte Datei verwendet wird. Jeder einzelne Zeichenwert ist als Spaltentrennzeichen zulässig. Der Standardwert ist ein `(,)`. |


## Erstellen einer Quellverbindung

Eine Quellverbindung erstellt und verwaltet die Verbindung zu der externen Quelle, aus der Daten erfasst werden. Eine Quellverbindung besteht aus Informationen wie Datenquelle, Datenformat und der Quellverbindungs-ID, die zum Erstellen eines Datenflusses erforderlich sind. Eine Quellverbindungsinstanz ist für einen Mandanten und eine Organisation spezifisch.

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
| `name` | Der Name Ihrer [!DNL Data Landing Zone]-Quellverbindung. |
| `data.format` | Das Format der Daten, die an Experience Platform übermittelt werden sollen. |
| `params.path` | Der Pfad zur Datei, die Sie an Experience Platform übermitteln möchten. |
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

In diesem Tutorial haben Sie Ihre [!DNL Data Landing Zone]-Anmeldeinformationen abgerufen, die Dateistruktur untersucht, um die Datei zu finden, die Sie in Experience Platform importieren möchten, und eine Quellverbindung erstellt, um mit dem Übertragen Ihrer Daten an Experience Platform zu beginnen. Sie können jetzt mit dem nächsten Tutorial fortfahren, in dem Sie erfahren, wie Sie [einen Datenfluss erstellen, um Cloud-Speicherdaten mithilfe der -API  [!DNL Flow Service]  Experience Platform zu &#x200B;](../../collect/cloud-storage.md).
