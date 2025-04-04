---
keywords: Experience Platform;Startseite;beliebte Themen;Cloud-Speicher;Cloud-Speicher
title: Erkunden von Cloud-Speicherordnern mithilfe der Flow Service-API
description: In diesem Tutorial wird die Flow Service-API verwendet, um ein Cloud-Speichersystem eines Drittanbieters zu erkunden.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 15%

---

# Erkunden von Cloud-Speicherordnern mit der [!DNL Flow Service]-API

In diesem Tutorial erfahren Sie, wie Sie die Struktur und die Inhalte Ihres Cloud-Speichers mithilfe der [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/)-API untersuchen und in der Vorschau anzeigen.

>[!NOTE]
>
>Um Ihren Cloud-Speicher zu untersuchen, müssen Sie bereits über eine gültige Basisverbindungs-ID für eine Cloud-Speicherquelle verfügen. Wenn Sie diese ID nicht haben, finden Sie in der [Quellen - Übersicht](../../../home.md#cloud-storage) eine Liste der Cloud-Speicherquellen, mit denen Sie eine Basisverbindung erstellen können.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../landing/api-guide.md).

## Erkunden von Cloud-Speicherordnern

Sie können Informationen zur Struktur Ihrer Cloud-Speicherordner abrufen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API richten und dabei die Basisverbindungs-ID Ihrer Quelle angeben.

Bei der Durchführung von GET-Anfragen zur Untersuchung Ihres Cloud-Speichers müssen Sie die in der folgenden Tabelle aufgeführten Abfrageparameter einbeziehen:

| Parameter | Beschreibung |
| --------- | ----------- |
| `objectType` | Der Typ des Objekts, das Sie untersuchen möchten. Legen Sie diesen Wert wie folgt fest: <ul><li>`folder`: Erkunden eines bestimmten Verzeichnisses</li><li>`root`: Erkunden des Stammverzeichnisses.</li></ul> |
| `object` | Dieser Parameter ist nur beim Anzeigen eines bestimmten Ordners erforderlich. Der Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. |


**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindung Ihrer Cloud-Speicherquelle. |
| `{PATH}` | Der Pfad eines Verzeichnisses. |

**Anfrage**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array von Dateien und Ordnern zurück, die im abgefragten Verzeichnis gefunden wurden. Notieren Sie sich die `path`-Eigenschaft der Datei, die Sie hochladen möchten, da Sie sie im nächsten Schritt bereitstellen müssen, um die Struktur zu überprüfen.

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

## Überprüfen der Dateistruktur

Um die Dateistruktur aus Ihrem Cloud-Speicher zu überprüfen, führen Sie eine GET-Anfrage aus, während Sie den Dateipfad und -typ als Abfrageparameter angeben.

Sie können die Struktur einer Datendatei aus Ihrer Cloud-Speicherquelle überprüfen, indem Sie eine GET-Anfrage ausführen und dabei den Pfad und den Typ der Datei angeben. Sie können auch verschiedene Dateitypen wie CSV-, TSV- oder komprimierte JSON- und durch Trennzeichen getrennte Dateien untersuchen, indem Sie deren Dateitypen als Teil der Abfrageparameter angeben.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&fileType=delimited&encoding=ISO-8859-1;
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Die Verbindungs-ID Ihres Cloud-Speicher-Quell-Connectors. |
| `{FILE_PATH}` | Der Pfad zur Datei, die Sie überprüfen möchten. |
| `{FILE_TYPE}` | Der Typ der Datei. Zu den unterstützten Dateitypen gehören:<ul><li><code>GETRENNT</code>: Durch Trennzeichen getrennter Wert. DSV-Dateien müssen durch Kommas getrennt sein.</li><li><code>JSON</code>: JavaScript-Objektnotation. JSON-Dateien müssen XDM-kompatibel sein</li><li><code></code>In: Apache Parquet. Parquet-Dateien müssen XDM-kompatibel sein.</li></ul> |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter, mit denen Ergebnisse gefiltert werden können. Weitere Informationen finden Sie [ Abschnitt ](#query) Abfrageparameter . |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) unterstützt die Verwendung von Abfrageparametern zur Vorschau und Untersuchung verschiedener Dateitypen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `columnDelimiter` | Der Einzelzeichenwert, den Sie als Spaltentrennzeichen zum Prüfen von CSV- oder TSV-Dateien angegeben haben. Wenn der Parameter nicht angegeben ist, ist der Wert standardmäßig ein `(,)`. |
| `compressionType` | Ein erforderlicher Abfrageparameter für die Vorschau einer komprimierten oder durch Trennzeichen getrennten JSON-Datei. Folgende komprimierte Dateien werden unterstützt: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Definiert den Kodierungstyp, der beim Rendern der Vorschau verwendet werden soll. Die unterstützten Kodierungstypen sind: `UTF-8` und `ISO-8859-1`. **Hinweis**: Der `encoding`-Parameter ist nur verfügbar, wenn durch Trennzeichen getrennte CSV-Dateien aufgenommen werden. Andere Dateitypen werden mit der Standardcodierung `UTF-8` aufgenommen. |

## Nächste Schritte

In diesem Tutorial haben Sie Ihr Cloud-Speichersystem erkundet, den Pfad der Datei gefunden, die Sie in [!DNL Experience Platform] einbringen möchten, und ihre Struktur betrachtet. Sie können diese Informationen im nächsten Tutorial verwenden[ um Daten aus Ihrem Cloud-Speicher zu erfassen und in Experience Platform zu ](../collect/cloud-storage.md).
