---
keywords: Experience Platform; Startseite; beliebte Themen; Cloud-Speicher; Cloud-Speicher
title: Durchsuchen von Cloud-Speicherordnern mithilfe der Flow Service-API
description: In diesem Tutorial wird die Flow Service-API verwendet, um ein Cloud-Speichersystem von Drittanbietern zu untersuchen.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 88e6f084ce1b857f785c4c1721d514ac3b07e80b
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 19%

---

# Durchsuchen Sie Ihre Cloud-Speicherordner mit dem [!DNL Flow Service] API

In diesem Tutorial erfahren Sie, wie Sie die Struktur und den Inhalt Ihres Cloud-Speichers mithilfe des [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
>Um Ihren Cloud-Speicher untersuchen zu können, müssen Sie bereits über eine gültige Basis-Verbindungs-ID für eine Cloud-Speicherquelle verfügen. Wenn Sie diese ID nicht haben, sehen Sie sich die [Quellen - Übersicht](../../../home.md#cloud-storage) für eine Liste der Cloud-Speicher-Quellen, mit denen Sie eine Basisverbindung erstellen können.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../landing/api-guide.md).

## Durchsuchen Sie Ihre Cloud-Speicher-Ordner.

Sie können Informationen über die Struktur Ihrer Cloud-Speicher-Ordner abrufen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] API bei gleichzeitiger Angabe der grundlegenden Verbindungs-ID Ihrer Quelle.

Bei der Durchführung von GET-Anfragen zur Erforschung Ihres Cloud-Speichers müssen Sie die Abfrageparameter einbeziehen, die in der folgenden Tabelle aufgeführt sind:

| Parameter | Beschreibung |
| --------- | ----------- |
| `objectType` | Der Typ des Objekts, das Sie untersuchen möchten. Legen Sie diesen Wert wie folgt fest: <ul><li>`folder`: Bestimmten Ordner durchsuchen</li><li>`root`: Durchsuchen Sie den Stammordner.</li></ul> |
| `object` | Dieser Parameter ist nur beim Anzeigen eines bestimmten Ordners erforderlich. Der Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. |


**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Kennung der Basisverbindung Ihrer Cloud-Speicherquelle. |
| `{PATH}` | Der Pfad eines Ordners. |

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

Eine erfolgreiche Antwort gibt ein Array von Dateien und Ordnern zurück, die im abgefragten Ordner gefunden wurden. Beachten Sie die `path` -Eigenschaft der Datei, die Sie hochladen möchten, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

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
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&ileType=delimited&encoding=ISO-8859-1;
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Die Verbindungs-ID Ihres Cloud-Speicher-Quell-Connectors. |
| `{FILE_PATH}` | Der Pfad zur Datei, die Sie überprüfen möchten. |
| `{FILE_TYPE}` | Der Dateityp. Zu den unterstützten Dateitypen gehören:<ul><li>DELIMITED</code>: Trennzeichen. DSV-Dateien müssen kommagetrennt sein.</li><li>JSON</code>: JavaScript-Objektnotation. JSON-Dateien müssen XDM-kompatibel sein</li><li>PARQUET</code>: Apache Parquet. Parquet-Dateien müssen XDM-konform sein.</li></ul> |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter, die zum Filtern von Ergebnissen verwendet werden können. Siehe Abschnitt zu [Abfrageparameter](#query) für weitere Informationen. |

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

Die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) unterstützt die Verwendung von Abfrageparametern zur Vorschau und Überprüfung verschiedener Dateitypen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `columnDelimiter` | Der Einzelzeichenwert, den Sie als Spaltentrennzeichen zum Überprüfen von CSV- oder TSV-Dateien angegeben haben. Wenn der Parameter nicht angegeben ist, wird standardmäßig ein Komma verwendet `(,)`. |
| `compressionType` | Ein erforderlicher Abfrageparameter für die Vorschau einer komprimierten getrennten Datei oder JSON-Datei. Folgende komprimierte Dateien werden unterstützt: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Definiert, welcher Kodierungstyp für die Wiedergabe der Vorschau verwendet werden soll. Folgende Kodierungstypen werden unterstützt: `UTF-8` und `ISO-8859-1`. **Hinweis**: Die `encoding` -Parameter ist nur verfügbar, wenn durch Trennzeichen getrennte CSV-Dateien aufgenommen werden. Andere Dateitypen werden mit der Standardkodierung erfasst. `UTF-8`. |

## Nächste Schritte

In diesem Tutorial haben Sie Ihr Cloud-Speichersystem durchsucht und den Pfad der Datei gefunden, die Sie in einführen möchten. [!DNL Platform]und die Struktur angezeigt. Sie können diese Informationen im nächsten Tutorial zu [Daten aus Ihrem Cloud-Speicher erfassen und in Platform integrieren](../collect/cloud-storage.md).
