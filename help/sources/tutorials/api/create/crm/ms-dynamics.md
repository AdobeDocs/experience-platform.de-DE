---
title: Erstellen einer Microsoft Dynamics-Basisverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Experience Platform mithilfe der Flow Service-API mit einem Microsoft Dynamics-Konto verbinden.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 14%

---

# Verbinden von [!DNL Microsoft Dynamics] mit Experience Platform mithilfe der [!DNL Flow Service]-API

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihre [!DNL Microsoft Dynamics] mithilfe der [[!DNL Flow Service] API) mit Adobe Experience Platform ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Experience Platform mithilfe der [!DNL Flow Service]-API erfolgreich mit einem Dynamics-Konto verbinden zu können.

### Sammeln erforderlicher Anmeldedaten

Um [!DNL Flow Service] mit [!DNL Dynamics] zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `serviceUri` | Die Service-URL Ihrer [!DNL Dynamics]. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics] Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics]. |

>[!TAB Service-Prinzipal- und Schlüsselauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]. Diese ID ist erforderlich, wenn die Service-Prinzipal- und schlüsselbasierte Authentifizierung verwendet wird. |
| `servicePrincipalKey` | Der geheime Schlüssel des Service-Prinzipals. Diese Berechtigung ist erforderlich, wenn die Authentifizierung über einen Service-Prinzipal und einen Schlüssel verwendet wird. |

>[!ENDTABS]

Weitere Informationen zu den ersten Schritten finden Sie [diesem  [!DNL Dynamics] Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Erstellen einer Basisverbindung

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL Dynamics] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Dynamics]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

**API-Format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Um eine [!DNL Dynamics] Basisverbindung mit einfacher Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API und geben dabei Werte für die `serviceUri`, `username` und `password` Ihrer Verbindung an.

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für eine [!DNL Dynamics] mit einfacher Authentifizierung.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using basic auth",
      "auth": {
          "specName": "Basic Authentication for Dynamics-Online",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.serviceUri` | Der Service-URI, der Ihrer [!DNL Dynamics]-Instanz zugeordnet ist. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Dynamics]-Konto zugeordnet ist. |
| `auth.params.password` | Das mit Ihrem [!DNL Dynamics]-Konto verknüpfte Kennwort. |
| `connectionSpec.id` | Die [!DNL Dynamics]-Verbindungsspezifikations-ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Schlüsselbasierte Authentifizierung für Service-Prinzipal]

Um eine [!DNL Dynamics] Basisverbindung mit Authentifizierung über einen Schlüssel des Service zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API und geben dabei Werte für die `serviceUri`, `servicePrincipalId` und `servicePrincipalKey` Ihrer Verbindung an.

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für eine [!DNL Dynamics] mit einer schlüsselbasierten Authentifizierung, die einen einfachen Service-Prinzipal verwendet.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.serviceUri` | Der Service-URI, der Ihrer [!DNL Dynamics]-Instanz zugeordnet ist. |
| `auth.params.servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]. Diese ID ist erforderlich, wenn die Service-Prinzipal- und schlüsselbasierte Authentifizierung verwendet wird. |
| `auth.params.servicePrincipalKey` | Der geheime Schlüssel des Service-Prinzipals. Diese Berechtigung ist erforderlich, wenn die Authentifizierung über einen Service-Prinzipal und einen Schlüssel verwendet wird. |
| `connectionSpec.id` | Die [!DNL Dynamics]-Verbindungsspezifikations-ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## Erkunden von Datentabellen

Um Ihre [!DNL Dynamics]-Datentabellen zu untersuchen, stellen Sie eine GET-Anfrage an den `/connections/{BASE_CONNECTION_ID}/explore`-Endpunkt und geben Sie Ihre Basisverbindungs-ID als Teil der Abfrageparameter an.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindung. Verwenden Sie diese ID, um den Inhalt und die Struktur Ihrer Quelle zu untersuchen. |

**Anfrage**

Mit der folgenden Anfrage wird die Liste der verfügbaren Tabellen und Ansichten für eine [!DNL Dynamics] mit der Basisverbindungs-ID abgerufen: `dd668808-25da-493f-8782-f3433b976d1e`.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt die [!DNL Dynamics] Tabellen und Ansichten des Ordners auf der Stammebene zurück.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++

### Verwenden des Primärschlüssels zur Optimierung der Datenexploration

>[!NOTE]
>
>Nicht-Lookup-Attribute können nur bei Verwendung des Primärschlüssel-Ansatzes zur Optimierung verwendet werden.

Sie können Ihre Erkundungsabfragen optimieren, indem Sie `primaryKey` als Teil Ihrer Abfrageparameter bereitstellen. Sie müssen den Primärschlüssel der [!DNL Dynamics] angeben, wenn Sie `primaryKey` als Abfrageparameter angeben.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?preview=true&object={OBJECT}&objectType={OBJECT_TYPE}&previewCount=10&primaryKey={PRIMARY_KEY}
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindung. Verwenden Sie diese ID, um den Inhalt und die Struktur Ihrer Quelle zu untersuchen. |
| `preview` | Ein boolescher Wert, der die Datenvorschau ermöglicht. |
| `{OBJECT}` | Das [!DNL Dynamics] Objekt, das Sie untersuchen möchten. |
| `{OBJECT_TYPE}` | Der Typ des Objekts. |
| `previewCount` | Eine Einschränkung, die die zurückgegebene Vorschau auf eine bestimmte Anzahl von Datensätzen beschränkt. |
| `{PRIMARY_KEY}` | Der Primärschlüssel der Tabelle, die Sie für die Vorschau abrufen. |

**Anfrage**

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform-stage.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?preview=true&object=lead&objectType=table&previewCount=10&primaryKey=leadid' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

## Überprüfen der Tabellenstruktur

Um die Struktur einer bestimmten Tabelle zu überprüfen, stellen Sie eine GET-Anfrage an `/connections/{BASE_CONNECTION_ID}/explore` und geben Sie den Pfad zur bestimmten Tabelle als Abfrageparameter an.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindung. Verwenden Sie diese ID, um den Inhalt und die Struktur Ihrer Quelle zu untersuchen. |
| `{TABLE_PATH}` | Der Pfad zur bestimmten Tabelle, die Sie untersuchen möchten. |

**Anfrage**

Die folgende Anfrage ruft die Struktur und den Inhalt einer [!DNL Dynamics] mit dem Pfad `workflowdependency` ab.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den Inhalt des Pfads `workflowdependency` zurück.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## Prüfen der Struktur einer Ansicht

In [!DNL Dynamics] bezieht sich eine Ansicht auf die anzuzeigenden Spalten, die Breite jeder Spalte, das Standardsystem, in dem eine Liste von Datensätzen sortiert wird, und die Standardfilter, die angewendet werden, um zu beschränken, welche Datensätze in der Liste angezeigt werden.

Um die Ansichtsstruktur zu überprüfen, stellen Sie eine GET-Anfrage an `/connections/{BASE_CONNECTION_ID}/explore` und geben Sie den Ansichtspfad in Ihren Abfrageparametern an. Darüber hinaus müssen Sie `objectType` als `view` angeben.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindung. Verwenden Sie diese ID, um den Inhalt und die Struktur Ihrer Quelle zu untersuchen. |
| `{VIEW_PATH}` | Der Pfad zur Ansicht, die Sie überprüfen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden `accountView1` abgerufen.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur von `accountView1` zurück.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## Vorschau der Entitätstypansicht

Um eine Vorschau des Inhalts einer Ansicht anzuzeigen, stellen Sie eine GET-Anfrage an `/connections/{BASE_CONNECTION_ID}/explore` und nehmen Sie den Ansichtspfad sowie `preview=true` in die Abfrageparameter auf.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindung. Verwenden Sie diese ID, um den Inhalt und die Struktur Ihrer Quelle zu untersuchen. |
| `{VIEW_PATH}` | Der Pfad zur Ansicht, die Sie überprüfen möchten. |


**Anfrage**

Mit der folgenden Anfrage wird eine Vorschau des Inhalts von `accountView1` angezeigt.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den Inhalt von `accountView1` zurück.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## Erstellen einer Quellverbindung zur Aufnahmeansicht

Um eine Quellverbindung zu erstellen und eine Ansicht aufzunehmen, stellen Sie eine POST-Anfrage an den `/sourceConnections`-Endpunkt, geben Sie den Tabellennamen an und geben Sie `entityType` wie im Anfragetext `view` an.

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine [!DNL Dynamics] Quellverbindung und nimmt Ansichten auf.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort werden die neu generierte Quellverbindungs-ID und das entsprechende eTag zurückgegeben.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

### Verwenden des Primärschlüssels zur Optimierung des Datenflusses

Sie können Ihren [!DNL Dynamics] Datenfluss auch optimieren, indem Sie den Primärschlüssel als Teil der Parameter Ihres Anfragetexts angeben.

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine [!DNL Dynamics]-Quellverbindung, während der Primärschlüssel als `contactid` angegeben wird.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular"
      },
      "params": {
          "tableName": "contact",
          "primaryKey": "contactid"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `baseConnectionId` | Die ID der Basisverbindung. |
| `data.format` | Das Format der Daten. |
| `params.tableName` | Der Name der Tabelle in [!DNL Dynamics]. |
| `params.primaryKey` | Der Primärschlüssel der Tabelle, die die Abfragen optimiert. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die der [!DNL Dynamics] entspricht. |

+++

**Antwort**

Bei einer erfolgreichen Antwort werden die neu generierte Quellverbindungs-ID und das entsprechende eTag zurückgegeben.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++


## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Microsoft Dynamics]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um CRM-Daten mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/crm.md)
