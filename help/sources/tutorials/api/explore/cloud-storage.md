---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 18%

---


# Entdecken Sie ein Cloud-Datenspeicherung-System mit der [!DNL Flow Service] API

[!DNL Flow Service] dient zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um ein Cloud-Datenspeicherung-System eines Drittanbieters zu untersuchen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect to a cloud storage system using the [!DNL Flow Service] API.

### Grundverbindung abrufen

Um eine Cloud-Datenspeicherung von Drittanbietern mithilfe von [!DNL Platform] APIs zu untersuchen, müssen Sie über eine gültige Basis-Verbindungs-ID verfügen. Wenn Sie noch keine Basisverbindung für die Datenspeicherung haben, mit der Sie arbeiten möchten, können Sie eine dieser Übungen erstellen:

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azurblase Data Lake Datenspeicherung Gen2](../create/cloud-storage/adls-gen2.md)
* [Google Cloud Store](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Entdecken Sie Ihre Cloud-Datenspeicherung

Mithilfe der Basisverbindung für Ihre Cloud-Datenspeicherung können Sie Dateien und Ordner untersuchen, indem Sie GET anfordern. Bei der Durchführung von GET zur Erforschung Ihrer Cloud-Datenspeicherung müssen Sie die in der folgenden Tabelle aufgeführten Abfragen-Parameter einschließen:

| Parameter | Beschreibung |
| --------- | ----------- |
| `objectType` | Der Objekttyp, den Sie untersuchen möchten. Legen Sie diesen Wert wie folgt fest: <ul><li>`folder`: Einen bestimmten Ordner durchsuchen</li><li>`root`: Suchen Sie den Stammordner.</li></ul> |
| `object` | Dieser Parameter ist nur erforderlich, wenn ein bestimmtes Verzeichnis angezeigt wird. Sein Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. |

Verwenden Sie den folgenden Aufruf, um den Pfad der Datei zu finden, die Sie einführen möchten [!DNL Platform]:

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID einer Cloud-Datenspeicherung-Basisverbindung. |
| `{PATH}` | Der Pfad eines Ordners. |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird ein Array von Dateien und Ordnern im abgefragten Ordner zurückgegeben. Notieren Sie sich die `path` Eigenschaft der Datei, die Sie hochladen möchten, da Sie sie im nächsten Schritt bereitstellen müssen, um die Struktur zu überprüfen.

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

## Inspect der Dateistruktur

Um die Struktur der Datendatei in Ihrer Cloud-Datenspeicherung zu überprüfen, führen Sie eine GET durch und geben Sie dabei den Dateipfad als Abfrage-Parameter an.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID einer Cloud-Datenspeicherung-Basisverbindung. |
| `{FILE_PATH}` | Pfad zu einer Datei. |
| `{FILE_TYPE}` | Der Typ der Datei. Folgende Dateitypen werden unterstützt:<ul><li>DELIMITED</code>: Trennzeichen-getrennter Wert. DSV-Dateien müssen kommagetrennt sein.</li><li>JSON</code>: JavaScript-Objektbeschreibung. JSON-Dateien müssen XDM-konform sein</li><li>PARQUET</code>: Apache Parquet. Parquet-Dateien müssen XDM-kompatibel sein.</li></ul> |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der abgefragten Datei einschließlich Tabellennamen und Datentypen zurück.

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## Nächste Schritte

In diesem Lernprogramm haben Sie Ihr Cloud-Datenspeicherung-System erforscht, den Dateipfad gefunden, den Sie eintragen möchten, [!DNL Platform]und die Dateistruktur angezeigt. Sie können diese Informationen im nächsten Lernprogramm verwenden, um Daten aus Ihrer Cloud-Datenspeicherung zu [erfassen und in Plattform](../collect/cloud-storage.md)zu übertragen.