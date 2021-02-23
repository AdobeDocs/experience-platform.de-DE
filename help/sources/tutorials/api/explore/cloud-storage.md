---
keywords: Experience Platform;Home;beliebte Themen;Cloud-Datenspeicherung;Cloud-Datenspeicherung
solution: Experience Platform
title: Durchsuchen eines cLoud-Datenspeicherung-Systems mithilfe der Flow Service API
topic: Übersicht
description: In diesem Lernprogramm wird die Flow Service API verwendet, um ein Cloud-Datenspeicherung-System eines Drittanbieters zu untersuchen.
translation-type: tm+mt
source-git-commit: 60a70352c2e13565fd3e8c44ae68e011a1d443a6
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 20%

---


# Entdecken Sie ein Cloud-Datenspeicherung-System mit der API[!DNL Flow Service]

Dieses Lernprogramm verwendet die [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml), um ein Cloud-Datenspeicherung-System eines Drittanbieters zu untersuchen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der [!DNL Flow Service]-API eine erfolgreiche Verbindung zu einem Cloud-Datenspeicherung-System herzustellen.

### Verbindungs-ID abrufen

Um eine Drittanbieter-Cloud-Datenspeicherung mithilfe von [!DNL Platform]-APIs zu untersuchen, müssen Sie über eine gültige Verbindungs-ID verfügen. Wenn Sie noch keine Verbindung zu der Datenspeicherung haben, mit der Sie arbeiten möchten, können Sie eine dieser Übungen erstellen:

* [[!DNL Amazon S3]](../create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)
* [[!DNL FTP]](../create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../create/cloud-storage/sftp.md)

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Flow Service] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Entdecken Sie Ihre Cloud-Datenspeicherung

Mithilfe der Verbindungs-ID für Ihre Cloud-Datenspeicherung können Sie Dateien und Verzeichnisse untersuchen, indem Sie GET anfordern. Bei der Durchführung von GET zur Erforschung Ihrer Cloud-Datenspeicherung müssen Sie die in der folgenden Tabelle aufgeführten Abfragen-Parameter einschließen:

| Parameter | Beschreibung |
| --------- | ----------- |
| `objectType` | Der Objekttyp, den Sie untersuchen möchten. Legen Sie diesen Wert wie folgt fest: <ul><li>`folder`: Einen bestimmten Ordner durchsuchen</li><li>`root`: Suchen Sie den Stammordner.</li></ul> |
| `object` | Dieser Parameter ist nur erforderlich, wenn ein bestimmtes Verzeichnis angezeigt wird. Sein Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. |

Verwenden Sie den folgenden Aufruf, um den Pfad der Datei zu finden, die Sie in [!DNL Platform] einbinden möchten:

**API-Format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONNECTION_ID}` | Die Verbindungs-ID für Ihren Cloud-Datenspeicherung-Quellanschluss. |
| `{PATH}` | Der Pfad eines Ordners. |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird ein Array von Dateien und Ordnern im abgefragten Ordner zurückgegeben. Beachten Sie die `path`-Eigenschaft der Datei, die Sie hochladen möchten, da Sie sie im nächsten Schritt bereitstellen müssen, um die Struktur zu überprüfen.

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

Um die Struktur der Datendatei in Ihrer Cloud-Datenspeicherung zu überprüfen, führen Sie eine GET durch und geben Sie dabei den Dateipfad und -typ als Abfrage-Parameter an.

Sie können die Struktur einer CSV- oder TSV-Datei überprüfen, indem Sie ein benutzerdefiniertes Trennzeichen als Abfrage-Rahmen angeben. Jeder einzelne Zeichenwert ist ein zulässiges Spaltentrennzeichen. Ist diese Angabe nicht verfügbar, wird ein Komma `(,)` als Standardwert verwendet.

**API-Format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=;
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=\t
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die Verbindungs-ID des Cloud-Datenspeicherung-Quellconnectors. |
| `{FILE_PATH}` | Der Pfad zu der Datei, die Sie überprüfen möchten. |
| `{FILE_TYPE}` | Der Typ der Datei. Folgende Dateitypen werden unterstützt:<ul><li>DELIMITED</code>: Trennzeichen-getrennter Wert. DSV-Dateien müssen kommagetrennt sein.</li><li>JSON</code>: JavaScript-Objektbeschreibung. JSON-Dateien müssen XDM-konform sein</li><li>PARQUET</code>: Apache Parquet. Parquet-Dateien müssen XDM-kompatibel sein.</li></ul> |
| `columnDelimiter` | Der Wert für ein einzelnes Zeichen, den Sie als Trennzeichen für Spalten angegeben haben, um CSV- oder TSV-Dateien zu überprüfen. Wenn der Parameter nicht angegeben ist, wird als Wert standardmäßig ein Komma `(,)` verwendet. |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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

In diesem Lernprogramm haben Sie Ihr Cloud-Datenspeicherung-System erforscht, den Dateipfad gefunden, den Sie in [!DNL Platform] einführen möchten, und die Dateistruktur angezeigt. Sie können diese Informationen im nächsten Lernprogramm zu [verwenden, um Daten aus Ihrer Cloud-Datenspeicherung zu erfassen und in Platform](../collect/cloud-storage.md) zu laden.