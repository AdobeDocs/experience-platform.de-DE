---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---


# Entdecken Sie ein Cloud-Datenspeicherung-System mit der [!DNL Flow Service] API

[!DNL Flow Service] dient zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um ein Cloud-Datenspeicherung-System eines Drittanbieters zu untersuchen.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] API eine erfolgreiche Verbindung zu einem Cloud-Datenspeicherung-System herzustellen.

### Grundverbindung abrufen

Um eine Cloud-Datenspeicherung von Drittanbietern mithilfe von [!DNL Platform] APIs zu untersuchen, müssen Sie über eine gültige Basis-Verbindungs-ID verfügen. Wenn Sie noch keine Basisverbindung für die Datenspeicherung haben, mit der Sie arbeiten möchten, können Sie eine dieser Übungen erstellen:

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azurblase Data Lake Datenspeicherung Gen2](../create/cloud-storage/adls-gen2.md)
* [Google Cloud Store](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur [!DNL Experience Platform] Fehlerbehebung.

### Werte für erforderliche Kopfzeilen sammeln

Um [!DNL Platform] APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Sämtliche Ressourcen in [!DNL Experience Platform]und auch die Ressourcen, die [!DNL Flow Service]gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Alle Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Entdecken Sie Ihre Cloud-Datenspeicherung

Mithilfe der Basisverbindung für Ihre Cloud-Datenspeicherung können Sie Dateien und Ordner durch GET-Anforderungen untersuchen. Bei GET-Anforderungen zur Erforschung Ihrer Cloud-Datenspeicherung müssen Sie die in der folgenden Tabelle aufgeführten Abfragen-Parameter einschließen:

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

## Überprüfen der Dateistruktur

Um die Struktur der Datendatei aus Ihrer Cloud-Datenspeicherung zu überprüfen, führen Sie eine GET-Anforderung durch und geben Sie dabei den Dateipfad als Dateiparameter an.

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

In diesem Lernprogramm haben Sie Ihr Cloud-Datenspeicherung-System erforscht, den Dateipfad gefunden, den Sie eintragen möchten, [!DNL Platform]und die Dateistruktur angezeigt. Sie können diese Informationen im nächsten Lernprogramm verwenden, um Daten aus Ihrer Cloud-Datenspeicherung zu [erfassen und in die Platform](../collect/cloud-storage.md)zu bringen.