---
keywords: Experience Platform; Startseite; beliebte Themen; Cloud-Speicher; Cloud-Speicher
solution: Experience Platform
title: Erkunden eines cCloud-Speichersystems mithilfe der Flow Service-API
topic-legacy: overview
description: In diesem Tutorial wird die Flow Service-API verwendet, um ein Cloud-Speichersystem von Drittanbietern zu untersuchen.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 27%

---

# Erkunden Sie ein Cloud-Speichersystem mit der [!DNL Flow Service]-API.

In diesem Tutorial wird die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) verwendet, um ein Cloud-Speichersystem von Drittanbietern zu untersuchen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu einem Cloud-Speichersystem herstellen zu können.

### Verbindung-ID abrufen

Um einen Drittanbieter-Cloud-Speicher mit [!DNL Platform]-APIs zu untersuchen, müssen Sie über eine gültige Verbindungs-ID verfügen. Wenn Sie noch keine Verbindung für den Speicher haben, mit dem Sie arbeiten möchten, können Sie eine durch die folgenden Tutorials erstellen:

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

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Cloud-Speicher durchsuchen

Mithilfe der Verbindungs-ID für Ihren Cloud-Speicher können Sie Dateien und Verzeichnisse untersuchen, indem Sie GET-Anfragen ausführen. Bei der Durchführung von GET-Anfragen zur Erforschung Ihres Cloud-Speichers müssen Sie die Abfrageparameter einbeziehen, die in der folgenden Tabelle aufgeführt sind:

| Parameter | Beschreibung |
| --------- | ----------- |
| `objectType` | Der Typ des Objekts, das Sie untersuchen möchten. Legen Sie diesen Wert wie folgt fest: <ul><li>`folder`: Bestimmten Ordner durchsuchen</li><li>`root`: Durchsuchen Sie den Stammordner.</li></ul> |
| `object` | Dieser Parameter ist nur beim Anzeigen eines bestimmten Ordners erforderlich. Der Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. |

Verwenden Sie den folgenden Aufruf, um den Pfad der Datei zu finden, die Sie in [!DNL Platform] einbinden möchten:

**API-Format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONNECTION_ID}` | Die Verbindungs-ID für Ihren Cloud-Speicher-Quell-Connector. |
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

Eine erfolgreiche Antwort gibt ein Array von Dateien und Ordnern zurück, die im abgefragten Ordner gefunden wurden. Notieren Sie sich die `path`-Eigenschaft der Datei, die Sie hochladen möchten, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Dateistruktur Inspect

Um die Struktur der Datendatei aus Ihrem Cloud-Speicher zu überprüfen, führen Sie eine GET-Anfrage aus und geben Sie dabei den Pfad der Datei an und geben Sie als Abfrageparameter ein.

Sie können die Struktur einer Datendatei aus Ihrer Cloud-Speicherquelle überprüfen, indem Sie eine GET-Anfrage ausführen und dabei Pfad und Typ der Datei angeben. Sie können auch verschiedene Dateitypen wie CSV-, TSV- oder komprimierte JSON- und getrennte Dateien überprüfen, indem Sie deren Dateitypen als Teil der Abfrageparameter angeben.

**API-Format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die Verbindungs-ID Ihres Cloud-Speicher-Quell-Connectors. |
| `{FILE_PATH}` | Der Pfad zur Datei, die Sie überprüfen möchten. |
| `{FILE_TYPE}` | Der Dateityp. Zu den unterstützten Dateitypen gehören:<ul><li>DELIMITED</code>: Trennzeichen. DSV-Dateien müssen kommagetrennt sein.</li><li>JSON</code>: JavaScript-Objektnotation. JSON-Dateien müssen XDM-kompatibel sein</li><li>PARQUET</code>: Apache Parquet. Parquet-Dateien müssen XDM-konform sein.</li></ul> |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter, die zum Filtern von Ergebnissen verwendet werden können. Weitere Informationen finden Sie im Abschnitt [Abfrageparameter](#query) . |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der abgefragten Datei zurück, einschließlich Tabellennamen und Datentypen.

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

## Verwenden von Abfrageparametern {#query}

Die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) unterstützt die Verwendung von Abfrageparametern zur Vorschau und Überprüfung verschiedener Dateitypen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `columnDelimiter` | Der Einzelzeichenwert, den Sie als Spaltentrennzeichen zum Überprüfen von CSV- oder TSV-Dateien angegeben haben. Wenn der Parameter nicht angegeben ist, wird als Standardwert ein Komma `(,)` verwendet. |
| `compressionType` | Ein erforderlicher Abfrageparameter für die Vorschau einer komprimierten getrennten Datei oder JSON-Datei. Folgende komprimierte Dateien werden unterstützt: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## Nächste Schritte

In diesem Tutorial haben Sie Ihr Cloud-Speichersystem durchsucht, den Pfad der Datei gefunden, die Sie in [!DNL Platform] einbringen möchten, und ihre Struktur angesehen. Sie können diese Informationen im nächsten Tutorial zu [erfassen von Daten aus Ihrem Cloud-Speicher und bringen sie in Platform](../collect/cloud-storage.md).
