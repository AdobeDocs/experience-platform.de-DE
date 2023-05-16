---
description: Erfahren Sie, wie Sie die Zielserverspezifikationen in Adobe Experience Platform Destination SDK über den Endpunkt "/authoring/destination-servers"konfigurieren.
title: Serverspezifikationen für Ziele, die mit Destination SDK erstellt wurden
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 11%

---


# Serverspezifikationen für Ziele, die mit Destination SDK erstellt wurden

Zielserverspezifikationen definieren den Typ der Zielplattform, die die Daten von Adobe Experience Platform erhält, sowie die Kommunikationsparameter zwischen Platform und Ihrem Ziel. Beispiel:

* A [Streaming](#streaming-example) Die Zielserverspezifikation definiert den HTTP-Server-Endpunkt, der die HTTP-Nachrichten von Platform erhält. Informationen zum Konfigurieren der Formatierung der HTTP-Aufrufe an den Endpunkt finden Sie im Abschnitt [Vorlagentypen](templating-specs.md) Seite.
* Ein [Amazon S3](#s3-example) Die Zielserverspezifikation definiert die [!DNL S3] Behältername und Pfad, in den Platform die Dateien exportiert.
* Ein [SFTP](#sftp-example) Die Zielserverspezifikation definiert den Hostnamen, das Stammverzeichnis, den Kommunikationsport und den Verschlüsselungstyp des SFTP-Servers, auf dem Platform die Dateien exportiert.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder sehen Sie die folgenden Übersichtsseiten zur Zielkonfiguration:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Sie können die Zielserverspezifikationen über die `/authoring/destination-servers` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielserverkonfiguration](../../authoring-api/destination-server/create-destination-server.md)
* [Aktualisieren der Zielserverkonfiguration](../../authoring-api/destination-server/update-destination-server.md)

Auf dieser Seite werden alle von Destination SDK unterstützten Zielservertypen mit allen Konfigurationsparametern angezeigt. Ersetzen Sie beim Erstellen Ihres Ziels die Parameterwerte durch Ihre eigenen.

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |

Wann [erstellen](../../authoring-api/destination-server/create-destination-server.md) oder [Aktualisieren](../../authoring-api/destination-server/update-destination-server.md) einen Zielserver verwenden, verwenden Sie eine der auf dieser Seite beschriebenen Servertypkonfigurationen. Stellen Sie je nach Integrationsanforderungen sicher, dass Sie die Beispielparameterwerte aus diesen Beispielen durch Ihre eigenen ersetzen.

## Hartkodierte bzw. vorlagenbasierte Felder {#templatized-fields}

Bei der Erstellung eines Zielservers durch Destination SDK können Sie die Parameterwerte für die Konfiguration entweder durch eine Hartkodierung in die Konfiguration oder durch Verwendung von Vorlagenfeldern definieren. Mit vorlagenbasierten Feldern können Sie vom Benutzer bereitgestellte Werte aus der Platform-Benutzeroberfläche lesen.

Die Zielserverparameter haben zwei konfigurierbare Felder. Diese Optionen bestimmen, ob Sie hartcodierte oder vorlagenbasierte Werte verwenden.

| Parameter | Typ | Beschreibung |
|---|---|---|
| `templatingStrategy` | Zeichenfolge | *Erforderlich.* Definiert, ob ein hartcodierter Wert vorhanden ist, der über die Variable `value` oder einen vom Benutzer konfigurierbaren Wert in der Benutzeroberfläche. Unterstützte Werte: <ul><li>`NONE`: Verwenden Sie diesen Wert, wenn Sie den Parameterwert über die `value` -Parameter (siehe nächste Zeile). Beispiel:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Verwenden Sie diesen Wert, wenn Ihre Benutzer in der Benutzeroberfläche einen Parameterwert angeben sollen. Beispiel: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Zeichenfolge | *Erforderlich*. Definiert den Parameterwert. Unterstützte Werttypen: <ul><li>**Hartkodierter Wert**: Verwenden Sie einen hartcodierten Wert (z. B. `"value": "my-storage-bucket"`), wenn Benutzer keinen Parameterwert in der Benutzeroberfläche eingeben müssen. Beim Hartkodieren eines Werts `templatingStrategy` sollte immer auf `NONE`.</li><li>**Vorlagenwert**: Verwenden Sie einen Vorlagenwert (z. B. `"value": "{{customerData.bucket}}"`), wenn Ihre Benutzer in der Benutzeroberfläche einen Parameterwert angeben sollen. Bei Verwendung von Vorlagenwerten `templatingStrategy` sollte immer auf `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Verwendung von hartcodierten bzw. vorlagenbasierten Feldern

Sowohl hartcodierte als auch vorlagenbasierte Felder verwenden je nach Art der Integration, die Sie erstellen, ihre eigenen Destinationen SDK.

**Verbindung zu Ihrem Ziel ohne Benutzereingabe herstellen**

Wenn Benutzer [Verbindung zu Ihrem Ziel herstellen](../../../ui/connect-destination.md) In der Platform-Benutzeroberfläche können Sie den Zielverbindungsprozess ohne Eingabe verarbeiten.

Dazu können Sie die Verbindungsparameter der Zielplattform in der Serverspezifikation hartcodieren. Wenn Sie in Ihrer Zielserverkonfiguration hartcodierte Parameterwerte verwenden, wird die Verbindung zwischen Adobe Experience Platform und Ihrer Zielplattform ohne Benutzereingabe verarbeitet.

Im folgenden Beispiel erstellt ein Partner einen Data Landing Zone-Zielserver mit der Variablen `path.value` -Feld fest codiert wird.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

Wenn Benutzer also die [Tutorial zur Zielverbindung](../../../ui/connect-destination.md), sehen sie keine [Authentifizierungsschritt](../../../ui/connect-destination.md#authenticate). Stattdessen wird die Authentifizierung von Platform durchgeführt, wie in der Abbildung unten dargestellt.

![UI-Bild, das den Authentifizierungsbildschirm zwischen Platform und einem DLZ-Ziel anzeigt.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Verbindung zu Ihrem Ziel mit Benutzereingaben herstellen**

Wenn die Verbindung zwischen Platform und Ihrem Ziel anhand einer bestimmten Benutzereingabe in der Platform-Benutzeroberfläche hergestellt werden soll, z. B. durch Auswahl eines API-Endpunkts oder Bereitstellung eines Feldwerts, können Sie in der Serverspezifikation vorlagenbasierte Felder verwenden, um die Benutzereingabe zu lesen und eine Verbindung mit Ihrer Zielplattform herzustellen.

Im folgenden Beispiel erstellt ein Partner eine [Echtzeit (Streaming)](#streaming-example) Integration und `url.value` -Feld verwendet den Vorlagenparameter `{{customerData.region}}` , um einen Teil des API-Endpunkts basierend auf der Benutzereingabe zu personalisieren.

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

Damit Benutzer einen Wert in der Platform-Benutzeroberfläche auswählen können, muss die `region` -Parameter muss auch im [Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md) als Kundendatenfeld verwenden, wie unten dargestellt:

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

Wenn Benutzer also die [Tutorial zur Zielverbindung](../../../ui/connect-destination.md)müssen sie eine Region auswählen, bevor sie eine Verbindung zur Zielplattform herstellen können. Wenn sie eine Verbindung zum Ziel herstellen, wird das Vorlagenfeld `{{customerData.region}}` durch den Wert ersetzt, den der Benutzer in der Benutzeroberfläche ausgewählt hat, wie in der Abbildung unten dargestellt.

![UI-Bild, das den Bildschirm für die Zielverbindung mit einem Regions-Selektor anzeigt.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Echtzeit-Zielserver (Streaming) {#streaming-example}

Mit diesem Zielservertyp können Sie Daten über HTTP-Anfragen von Adobe Experience Platform an Ihr Ziel exportieren. Die Server-Konfiguration enthält Informationen zum Server, der die Nachrichten erhält (der Server auf Ihrer Seite).

Dieser Prozess stellt Benutzerdaten als eine Reihe von HTTP-Nachrichten an Ihre Zielplattform bereit. Die folgenden Parameter bilden die Vorlage für HTTP-Server-Spezifikationen.

Das folgende Beispiel zeigt ein Beispiel für eine Zielserverkonfiguration für ein Echtzeit-Ziel (Streaming).

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | *Erforderlich.* Stellt einen Anzeigenamen Ihres Servers dar, der nur für Adobe sichtbar ist. Dieser Name ist für Partner oder Kunden nicht sichtbar. Beispiel: `Moviestar destination server`. |
| `destinationServerType` | Zeichenfolge | *Erforderlich.* Legen Sie hier fest `URL_BASED` für Streaming-Ziele. |
| `templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwendung `PEBBLE_V1` Wenn Sie ein vorlagenbasiertes Feld anstelle eines hartcodierten Werts im `value` -Feld. Verwenden Sie diese Option, wenn Sie einen Endpunkt wie haben: `https://api.moviestar.com/data/{{customerData.region}}/items`: Benutzer müssen den Endpunktbereich in der Platform-Benutzeroberfläche auswählen. </li><li> Verwendung `NONE` wenn keine vorlagenbasierte Transformation auf der Seite der Adobe erforderlich ist, z. B. wenn Sie einen Endpunkt wie: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Zeichenfolge | *Erforderlich.* Geben Sie die Adresse des API-Endpunkts ein, mit dem sich Experience Platform verbinden soll. |

{style="table-layout:auto"}

## [!DNL Amazon S3] Zielserver {#s3-example}

Mit diesem Zielserver können Sie Dateien mit Adobe Experience Platform-Daten in Ihren Amazon S3-Speicher exportieren.

Das folgende Beispiel zeigt ein Beispiel für eine Zielserverkonfiguration für ein Amazon S3-Ziel.

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihres Zielservers. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. So exportieren Sie Dateien in eine [!DNL Amazon S3] Bucket erstellen, setzen Sie dies auf `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `bucket.value` -Feld.<ul><li>Wenn Sie möchten, dass Ihre Benutzer ihren eigenen Behälternamen in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie die `value` -Feld, um einen Wert aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Behälternamen für Ihre Integration verwenden, z. B. `"bucket.value":"MyBucket"`setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Zeichenfolge | Der Name des [!DNL Amazon S3]-Buckets, der von diesem Ziel verwendet werden soll. Dies kann entweder ein Vorlagenfeld sein, das den Wert aus dem [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt (wie im Beispiel oben gezeigt) oder durch einen hartcodierten Wert, z. B. `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `path.value` -Feld.<ul><li>Wenn Sie möchten, dass Ihre Benutzer ihren eigenen Pfad in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie die `path.value` -Feld, um einen Wert aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Pfad für Ihre Integration verwenden, z. B. `"bucket.value":"/path/to/MyBucket"`setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Zeichenfolge | Der Pfad zum [!DNL Amazon S3] -Bucket, der von diesem Ziel verwendet werden soll. Dies kann entweder ein Vorlagenfeld sein, das den Wert aus dem [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt (wie im Beispiel oben gezeigt) oder durch einen hartcodierten Wert, z. B. `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] Zielserver {#sftp-example}

Mit diesem Zielserver können Sie Dateien mit Adobe Experience Platform-Daten in Ihre [!DNL SFTP] Speicherserver.

Das folgende Beispiel zeigt ein Beispiel für eine Zielserverkonfiguration für ein SFTP-Ziel.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihres Zielservers. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. So exportieren Sie Dateien in eine [!DNL SFTP] Ziel, setzen Sie dies auf `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `rootDirectory.value` -Feld.<ul><li>Wenn Sie möchten, dass Ihre Benutzer ihren eigenen Stammordnerpfad in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie die `rootDirectory.value` -Feld zum Lesen eines vom Benutzer bereitgestellten Werts aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Stammordnerpfad für Ihre Integration verwenden, z. B. `"rootDirectory.value":"Storage/MyDirectory"`setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Zeichenfolge | Der Pfad zum Ordner, in dem die exportierten Dateien gehostet werden. Dies kann entweder ein Vorlagenfeld sein, das den Wert aus dem [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt (wie im Beispiel oben gezeigt) oder durch einen hartcodierten Wert, z. B. `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `hostName.value` -Feld.<ul><li>Wenn Sie möchten, dass Ihre Benutzer ihren eigenen Hostnamen in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie die `hostName.value` -Feld zum Lesen eines vom Benutzer bereitgestellten Werts aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Hostnamen für Ihre Integration verwenden, z. B. `"hostName.value":"my.hostname.com"`setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Zeichenfolge | Der Hostname Ihres SFTP-Servers. Dies kann entweder ein Vorlagenfeld sein, das den Wert aus dem [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt (wie im Beispiel oben gezeigt) oder durch einen hartcodierten Wert, z. B. `"hostName.value":"my.hostname.com"`. |
| `port` | Ganzzahl | Der SFTP-Datei-Server-Port. |
| `encryptionMode` | Zeichenfolge | Gibt an, ob eine Dateiverschlüsselung verwendet werden soll. Unterstützte Werte: <ul><li>PGP</li><li>Keine</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) Zielserver {#adls-example}

Mit diesem Zielserver können Sie Dateien mit Adobe Experience Platform-Daten in Ihre [!DNL Azure Data Lake Storage] -Konto.

Das folgende Beispiel zeigt ein Beispiel für eine Zielserverkonfiguration für eine [!DNL Azure Data Lake Storage] Ziel.

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Azure Data Lake Storage]-Ziele `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `path.value` -Feld.<ul><li>Wenn Ihre Benutzer ihre [!DNL ADLS] Ordnerpfad in der Experience Platform-Benutzeroberfläche festlegen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie die `path.value` -Feld, um einen Wert aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Pfad für Ihre Integration verwenden, z. B. `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Zeichenfolge | Der Pfad zu Ihrer [!DNL ADLS] Speicherordner. Dies kann entweder ein Vorlagenfeld sein, das den Wert aus dem [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt (wie im Beispiel oben gezeigt) oder durch einen hartcodierten Wert, z. B. `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] Zielserver {#blob-example}

Mit diesem Zielserver können Sie Dateien mit Adobe Experience Platform-Daten in Ihre [!DNL Azure Blob Storage] Container.

Das folgende Beispiel zeigt ein Beispiel für eine Zielserverkonfiguration für eine [!DNL Azure Blob Storage] Ziel.

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Azure Blob Storage]-Ziele `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `path.value` -Feld.<ul><li>Wenn Sie möchten, dass Ihre Benutzer ihre eigenen [!DNL Azure Blob] [Speicherkonto-URI](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) Setzen Sie diesen Wert in der Experience Platform-Benutzeroberfläche auf `PEBBLE_V1`. In diesem Fall müssen Sie die `path.value` -Feld, um den Wert aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Pfad für Ihre Integration verwenden, z. B. `"path.value": "https://myaccount.blob.core.windows.net/"`setzen Sie diesen Wert auf `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Zeichenfolge | Der Pfad zu Ihrer [!DNL Azure Blob] Speicher. Dies kann entweder ein Vorlagenfeld sein, das den Wert aus dem [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt (wie im Beispiel oben gezeigt) oder durch einen hartcodierten Wert, z. B. `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `container.value` -Feld.<ul><li>Wenn Sie möchten, dass Ihre Benutzer ihre eigenen [!DNL Azure Blob] [Containername](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) Setzen Sie diesen Wert in der Experience Platform-Benutzeroberfläche auf `PEBBLE_V1`. In diesem Fall müssen Sie die `container.value` -Feld, um den Wert aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Container-Namen für Ihre Integration verwenden, z. B. `"path.value: myContainer"`setzen Sie diesen Wert auf `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Zeichenfolge | Der Name des Azure Blob Storage-Containers, der für dieses Ziel verwendet werden soll. Dies kann entweder ein Vorlagenfeld sein, das den Wert aus dem [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt (wie im Beispiel oben gezeigt) oder durch einen hartcodierten Wert, z. B. `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) Zielserver {#dlz-example}

Mit diesem Zielserver können Sie Dateien mit Platform-Daten in eine [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) Speicher.

Das folgende Beispiel zeigt ein Beispiel für eine Zielserverkonfiguration für eine [!DNL Data Landing Zone] ([!DNL DLZ]).

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Data Landing Zone]-Ziele `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `path.value` -Feld.<ul><li>Wenn Sie möchten, dass Ihre Benutzer ihre eigenen [!DNL Data Landing Zone] -Konto in der Experience Platform-Benutzeroberfläche festlegen, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie die `path.value` -Feld, um einen Wert aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Pfad für Ihre Integration verwenden, z. B. `"path.value": "https://myaccount.blob.core.windows.net/"`setzen Sie diesen Wert auf `NONE`. |
| `fileBasedDlzDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] Zielserver {#gcs-example}

Mit diesem Zielserver können Sie Dateien mit Platform-Daten in Ihre [!DNL Google Cloud Storage] -Konto.

Das folgende Beispiel zeigt ein Beispiel für eine Zielserverkonfiguration für eine [!DNL Google Cloud Storage] Ziel.

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Google Cloud Storage]-Ziele `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `bucket.value` -Feld.<ul><li>Wenn Sie möchten, dass Ihre Benutzer ihre eigenen [!DNL Google Cloud Storage] Behältername in der Benutzeroberfläche &quot;Experience Platform&quot;festlegen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie die `bucket.value` -Feld, um einen Wert aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Behälternamen für Ihre Integration verwenden, z. B. `"bucket.value": "my-bucket"`setzen Sie diesen Wert auf `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Zeichenfolge | Der Name des [!DNL Google Cloud Storage]-Buckets, der von diesem Ziel verwendet werden soll. Dies kann entweder ein Vorlagenfeld sein, das den Wert aus dem [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt (wie im Beispiel oben gezeigt) oder durch einen hartcodierten Wert, z. B. `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des Werts fest, der im `path.value` -Feld.<ul><li>Wenn Sie möchten, dass Ihre Benutzer ihre eigenen [!DNL Google Cloud Storage] Behälterpfad in der Experience Platform-Benutzeroberfläche festlegen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie die `path.value` -Feld, um einen Wert aus der [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Pfad für Ihre Integration verwenden, z. B. `"path.value": "/path/to/my-bucket"`setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Zeichenfolge | Der Pfad zum [!DNL Google Cloud Storage] Ordner, der von diesem Ziel verwendet werden soll. Dies kann entweder ein Vorlagenfeld sein, das den Wert aus dem [Kundendatenfelder](../destination-configuration/customer-data-fields.md) vom Benutzer ausgefüllt (wie im Beispiel oben gezeigt) oder durch einen hartcodierten Wert, z. B. `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, was eine Spezifikation für den Zielserver ist und wie Sie ihn konfigurieren können.

Weitere Informationen zu den anderen Ziel-Server-Komponenten finden Sie in den folgenden Artikeln:

* [Festlegen von Spezifikationen](templating-specs.md)
* [Nachrichtenformat](message-format.md)
* [Konfiguration der Dateiformatierung](file-formatting.md)
