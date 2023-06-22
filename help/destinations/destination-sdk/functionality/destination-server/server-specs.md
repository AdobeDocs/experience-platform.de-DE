---
description: Erfahren Sie, wie Sie die Ziel-Server-Spezifikationen im Adobe Experience Platform Destination SDK über den Endpunkt „/authoring/destination-servers“ konfigurieren.
title: Server-Spezifikationen für Ziele, die mit Destination SDK erstellt wurden
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: ht
source-wordcount: '2750'
ht-degree: 100%

---


# Server-Spezifikationen für Ziele, die mit Destination SDK erstellt wurden

Ziel-Server-Spezifikationen definieren den Typ der Zielplattform, die die Daten von Adobe Experience Platform erhält, sowie die Kommunikationsparameter zwischen Platform und Ihrem Ziel. Beispiel:

* Eine [Streaming](#streaming-example)-Ziel-Server-Spezifikation definiert den HTTP-Server-Endpunkt, der die HTTP-Nachrichten von Platform erhält. Informationen zum Konfigurieren der Formatierung der HTTP-Aufrufe an den Endpunkt finden Sie auf der Seite [Spezifikationen für Vorlagentypen](templating-specs.md).
* Eine [Amazon S3](#s3-example)-Ziel-Server-Spezifikation definiert den [!DNL S3]-Behälternamen und -Pfad, in den Platform die Dateien exportiert.
* Eine [SFTP](#sftp-example)-Ziel-Server-Spezifikation definiert den Host-Namen, das Stammverzeichnis, den Kommunikations-Port und den Verschlüsselungstyp des SFTP-Servers, auf den Platform die Dateien exportiert.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm in der Dokumentation zu [Konfigurationsoptionen](../configuration-options.md) oder auf den folgenden Übersichtsseiten zur Zielkonfiguration:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Sie können die Ziel-Server-Spezifikationen über den Endpunkt `/authoring/destination-servers` konfigurieren. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md)
* [Aktualisieren einer Ziel-Server-Konfiguration](../../authoring-api/destination-server/update-destination-server.md)

Auf dieser Seite werden alle von Destination SDK unterstützten Ziel-Server-Typen mit allen Konfigurationsparametern angezeigt. Ersetzen Sie beim Erstellen Ihres Ziels die Parameterwerte durch Ihre eigenen.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |

Wenn Sie einen Ziel-Server [erstellen](../../authoring-api/destination-server/create-destination-server.md) oder [aktualisieren](../../authoring-api/destination-server/update-destination-server.md), verwenden Sie eine der auf dieser Seite beschriebenen Konfigurationen des Server-Typs. Stellen Sie je nach Integrationsanforderungen sicher, dass Sie die Beispielparameterwerte aus diesen Beispielen durch Ihre eigenen ersetzen.

## Hartcodierte bzw. vorlagenbasierte Felder {#templatized-fields}

Bei der Erstellung eines Ziel-Servers durch Destination SDK können Sie die Parameterwerte für die Konfiguration entweder durch eine Hartcodierung in die Konfiguration oder durch Verwendung von Vorlagenfeldern definieren. Mit vorlagenbasierten Feldern können Sie von Benutzenden bereitgestellte Werte aus der Platform-Benutzeroberfläche lesen.

Die Ziel-Server-Parameter haben zwei konfigurierbare Felder. Diese Optionen bestimmen, ob Sie hartcodierte oder vorlagenbasierte Werte verwenden.

| Parameter | Typ | Beschreibung |
|---|---|---|
| `templatingStrategy` | Zeichenfolge | *Erforderlich.* Definiert, ob ein hartcodierter Wert vorhanden ist, der über das Feld `value` bereitgestellt wird, oder ein von Benutzenden konfigurierbarer Wert in der Benutzeroberfläche. Unterstützte Werte: <ul><li>`NONE`: Verwenden Sie diesen Wert, wenn Sie den Parameterwert über den Parameter `value` hartcodieren (siehe nächste Zeile). Beispiel:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Verwenden Sie diesen Wert, wenn Ihre Benutzerinnen und Benutzer in der Benutzeroberfläche einen Parameterwert angeben sollen. Beispiel: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Zeichenfolge | *Erforderlich*. Definiert den Parameterwert. Unterstützte Werttypen: <ul><li>**Hartcodierter Wert**: Verwenden Sie einen hartcodierten Wert (z. B. `"value": "my-storage-bucket"`), wenn Benutzerinnen und Benutzer keinen Parameterwert in der Benutzeroberfläche eingeben müssen. Beim Hartcodieren eines Werts sollte `templatingStrategy` immer auf `NONE` festgelegt werden.</li><li>**Vorlagenwert**: Verwenden Sie einen Vorlagenwert (z. B. `"value": "{{customerData.bucket}}"`), wenn Ihre Benutzerinnen und Benutzer einen Parameterwert in der Benutzeroberfläche angeben sollen. Bei Verwendung von Vorlagenwerten sollte `templatingStrategy` immer auf `PEBBLE_V1` festgelegt werden.</li></ul> |

{style="table-layout:auto"}

### Wann hartcodierte bzw. vorlagenbasierte Felder verwendet werden sollten

Sowohl hartcodierte als auch vorlagenbasierte Felder haben ihre eigene Verwendung in Destination SDK, je nachdem, welche Art von Integration Sie erstellen.

**Herstellen einer Verbindung zu Ihrem Ziel ohne Benutzereingabe**

Wenn Benutzerinnen und Benutzer in der Platform-Benutzeroberfläche eine [Verbindung zu Ihrem Ziel herstellen](../../../ui/connect-destination.md), möchten Sie vielleicht den Verbindungsprozess zum Ziel ohne Benutzereingabe abwickeln.

Dazu können Sie die Verbindungsparameter der Zielplattform in der Server-Spezifikation hartcodieren. Wenn Sie in Ihrer Ziel-Server-Konfiguration hartcodierte Parameterwerte verwenden, wird die Verbindung zwischen Adobe Experience Platform und Ihrer Zielplattform ohne Benutzereingabe veranlasst.

Im folgenden Beispiel erstellt ein Partner einen Data Landing Zone(DLZ)-Ziel-Server, wobei das Feld `path.value` hartcodiert ist..

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

Wenn Benutzerinnen und Benutzer das [Tutorial zur Zielverbindung](../../../ui/connect-destination.md) durchlaufen, sehen sie also keinen [Authentifizierungsschritt](../../../ui/connect-destination.md#authenticate). Stattdessen wird die Authentifizierung von Platform durchgeführt, wie in der Abbildung unten dargestellt.

![UI-Bild, das den Authentifizierungsbildschirm zwischen Platform und einem DLZ-Ziel anzeigt.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Herstellen einer Verbindung zu Ihrem Ziel mit Benutzereingabe**

Wenn die Verbindung zwischen Platform und Ihrem Ziel anhand einer bestimmten Benutzereingabe in der Platform-Benutzeroberfläche hergestellt werden soll, z. B. durch Auswahl eines API-Endpunkts oder Angabe eines Feldwerts, können Sie in der Server-Spezifikation vorlagenbasierte Felder verwenden, um die Benutzereingabe zu lesen und eine Verbindung mit Ihrer Zielplattform herzustellen.

Im folgenden Beispiel erstellt ein Partner eine [Echtzeit (Streaming)](#streaming-example)-Integration, und das Feld `url.value` verwendet den Vorlagenparameter `{{customerData.region}}`, um einen Teil des API-Endpunkts basierend auf der Benutzereingabe zu personalisieren.

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

Damit Benutzerinnen und Benutzer einen Wert in der Platform-Benutzeroberfläche auswählen können, muss der Parameter `region` auch in der [Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md) als Kundendatenfeld definiert werden, wie unten dargestellt:

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

Wenn Benutzerinnen und Benutzer das [Tutorial zur Zielverbindung](../../../ui/connect-destination.md) durchlaufen, müssen sie dann erst eine Region auswählen, bevor sie eine Verbindung zur Zielplattform herstellen können. Wenn sie eine Verbindung zum Ziel herstellen, wird das Vorlagenfeld `{{customerData.region}}` durch den Wert ersetzt, den sie in der Benutzeroberfläche ausgewählt haben, wie in der Abbildung unten dargestellt.

![UI-Bild, das den Bildschirm für die Zielverbindung mit einem Regionen-Selektor anzeigt.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Echtzeit-Ziel-Server (Streaming) {#streaming-example}

Mit diesem Ziel-Server-Typ können Sie Daten von Adobe Experience Platform über HTTP-Anfragen an Ihr Ziel exportieren. Die Server-Konfiguration enthält Informationen zum Server, der die Nachrichten erhält (der Server auf Ihrer Seite).

Dieser Prozess stellt Benutzerdaten als eine Reihe von HTTP-Nachrichten an Ihre Zielplattform bereit. Die folgenden Parameter bilden die Vorlage für HTTP-Server-Spezifikationen.

Das folgende Beispiel zeigt ein Beispiel einer Ziel-Server-Konfiguration für ein Echtzeit-Ziel (Streaming).

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
| `name` | Zeichenfolge | *Erforderlich.* Stellt einen Anzeigenamen Ihres Servers dar, der nur für Adobe sichtbar ist. Dieser Name ist weder für Partner noch für Kundinnen und Kunden sichtbar. Beispiel: `Moviestar destination server`. |
| `destinationServerType` | Zeichenfolge | *Erforderlich.* Legen Sie dieses für Streaming-Ziele auf `URL_BASED` fest. |
| `templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Sie im Feld `value` einen hartcodierten Wert verwenden und nicht ein Vorlagenfeld. Verwenden Sie diese Option, wenn Sie einen Endpunkt wie `https://api.moviestar.com/data/{{customerData.region}}/items` haben, wo die Benutzerinnen und Benutzer die Region des Endpunkts in der Platform-Benutzeroberfläche auswählen müssen. </li><li> Verwenden Sie `NONE`, wenn auf Seiten von Adobe keine vorlagenbasierte Transformation erforderlich ist, z. B. wenn Sie einen Endpunkt wie `https://api.moviestar.com/data/items` haben. </li></ul> |
| `value` | Zeichenfolge | *Erforderlich.* Geben Sie die Adresse des API-Endpunkts ein, mit dem sich Experience Platform verbinden soll. |

{style="table-layout:auto"}

## [!DNL Amazon S3]-Ziel-Server {#s3-example}

Mit diesem Ziel-Server können Sie Dateien, die Adobe Experience Platform-Daten enthalten, in Ihren Amazon S3-Speicher exportieren.

Das folgende Beispiel zeigt ein Beispiel einer Ziel-Server-Konfiguration für ein Amazon S3-Ziel.

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
| `name` | Zeichenfolge | Der Name Ihres Ziel-Servers. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Um Dateien in einen [!DNL Amazon S3]-Bucket zu exportieren, setzen Sie diesen Wert auf `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `bucket.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihren eigenen Behälternamen in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Behälternamen für Ihre Integration verwenden, z. B. `"bucket.value":"MyBucket"`, setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Zeichenfolge | Der Name des [!DNL Amazon S3]-Behälters, der von diesem Ziel verwendet werden soll. Dabei kann es sich entweder um ein Vorlagenfeld handeln, das den Wert aus den von den Benutzenden ausgefüllten [Kundendatenfeldern](../destination-configuration/customer-data-fields.md) liest (wie im Beispiel oben gezeigt), oder um einen hartcodierten Wert, z. B. `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `path.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihren eigenen Pfad in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `path.value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten für Ihre Integration verwenden, z. B. `"bucket.value":"/path/to/MyBucket"`, setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Zeichenfolge | Der Pfad des [!DNL Amazon S3]-Behälters, der von diesem Ziel verwendet werden soll. Dabei kann es sich entweder um ein Vorlagenfeld handeln, das den Wert aus den von den Benutzenden ausgefüllten [Kundendatenfeldern](../destination-configuration/customer-data-fields.md) liest (wie im Beispiel oben gezeigt), oder um einen hartcodierten Wert, z. B. `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP]-Ziel-Server {#sftp-example}

Mit diesem Ziel-Server können Sie Dateien mit Adobe Experience Platform-Daten in Ihren [!DNL SFTP] Speicher-Server exportieren.

Das folgende Beispiel zeigt ein Beispiel einer Ziel-Server-Konfiguration für ein SFTP-Ziel.

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
| `name` | Zeichenfolge | Der Name Ihres Ziel-Servers. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Um Dateien in ein [!DNL SFTP]-Ziel zu exportieren, setzen Sie dies auf `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `rootDirectory.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihren eigenen Stammordnerpfad in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `rootDirectory.value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Stammordnerpfad für Ihre Integration verwenden, z. B. `"rootDirectory.value":"Storage/MyDirectory"`, setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Zeichenfolge | Der Pfad zum Verzeichnis, in dem die exportierten Dateien gespeichert werden. Dabei kann es sich entweder um ein Vorlagenfeld handeln, das den Wert aus den von den Benutzenden ausgefüllten [Kundendatenfeldern](../destination-configuration/customer-data-fields.md) liest (wie im Beispiel oben gezeigt), oder um einen hartcodierten Wert, z. B. `"value":"Storage/MyDirectory"`. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `hostName.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihren eigenen Host-Namen in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `hostName.value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Host-Namen für Ihre Integration verwenden, z. B. `"hostName.value":"my.hostname.com"`, setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Zeichenfolge | Der Host-Name Ihres SFTP-Servers. Dabei kann es sich entweder um ein Vorlagenfeld handeln, das den Wert aus den von den Benutzenden ausgefüllten [Kundendatenfeldern](../destination-configuration/customer-data-fields.md) liest (wie im Beispiel oben gezeigt), oder um einen hartcodierten Wert, z. B. `"hostName.value":"my.hostname.com"`. |
| `port` | Ganzzahl | Der SFTP-Datei-Server-Port. |
| `encryptionMode` | Zeichenfolge | Gibt an, ob eine Dateiverschlüsselung verwendet werden soll. Unterstützte Werte: <ul><li>PGP</li><li>Keine</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) -Ziel-Server {#adls-example}

Mit diesem Ziel-Server können Sie Dateien mit Adobe Experience Platform-Daten in Ihr [!DNL Azure Data Lake Storage]-Konto exportieren.

Das folgende Beispiel zeigt ein Beispiel einer Ziel-Server-Konfiguration für ein [!DNL Azure Data Lake Storage]-Ziel.

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
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `path.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihren [!DNL ADLS]-Ordnerpfad in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `path.value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten für Ihre Integration verwenden, z. B. `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`, setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Zeichenfolge | Der Pfad zu Ihrem [!DNL ADLS]-Speicherordner. Dabei kann es sich entweder um ein Vorlagenfeld handeln, das den Wert aus den von den Benutzenden ausgefüllten [Kundendatenfeldern](../destination-configuration/customer-data-fields.md) liest (wie im Beispiel oben gezeigt), oder um einen hartcodierten Wert, z. B. `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage]-Ziel-Server {#blob-example}

Mit diesem Ziel-Server können Sie Dateien mit Adobe Experience Platform-Daten in Ihren [!DNL Azure Blob Storage]-Container exportieren.

Das folgende Beispiel zeigt ein Beispiel einer Ziel-Server-Konfiguration für ein [!DNL Azure Blob Storage]-Ziel.

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
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `path.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihren eigenen [!DNL Azure Blob] [Speicherkonto-URI](https://learn.microsoft.com/de-de/azure/storage/blobs/storage-blobs-introduction) in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `path.value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten für Ihre Integration verwenden, z. B. `"path.value": "https://myaccount.blob.core.windows.net/"`, setzen Sie diesen Wert auf `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Zeichenfolge | Der Pfad zu Ihrem [!DNL Azure Blob]-Speicher. Dabei kann es sich entweder um ein Vorlagenfeld handeln, das den Wert aus den von den Benutzenden ausgefüllten [Kundendatenfeldern](../destination-configuration/customer-data-fields.md) liest (wie im Beispiel oben gezeigt), oder um einen hartcodierten Wert, z. B. `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `container.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihren eigenen [!DNL Azure Blob]-[Container-Namen](https://learn.microsoft.com/de-de/azure/storage/blobs/storage-blobs-introduction) in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `container.value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Container-Namen für Ihre Integration verwenden, z. B. `"path.value: myContainer"`, setzen Sie diesen Wert auf `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Zeichenfolge | Der Name des Azure Blob Storage-Containers, der für dieses Ziel verwendet werden soll. Dabei kann es sich entweder um ein Vorlagenfeld handeln, das den Wert aus den von den Benutzenden ausgefüllten [Kundendatenfeldern](../destination-configuration/customer-data-fields.md) liest (wie im Beispiel oben gezeigt), oder um einen hartcodierten Wert, z. B. `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) -Ziel-Server {#dlz-example}

Mit diesem Ziel-Server können Sie Dateien mit Platform-Daten in einen [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md)-Speicher exportieren.

Das folgende Beispiel zeigt ein Beispiel einer Ziel-Server-Konfiguration für ein [!DNL Data Landing Zone]-Ziel ([!DNL DLZ]).

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
| `fileBasedDlzDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `path.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihr eigenes [!DNL Data Landing Zone] -Konto in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `path.value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten für Ihre Integration verwenden, z. B. `"path.value": "https://myaccount.blob.core.windows.net/"`, setzen Sie diesen Wert auf `NONE`. |
| `fileBasedDlzDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage]-Ziel-Server {#gcs-example}

Mit diesem Ziel-Server können Sie Dateien mit Platform-Daten in Ihr [!DNL Google Cloud Storage] -Konto exportieren.

Das folgende Beispiel zeigt ein Beispiel einer Ziel-Server-Konfiguration für ein [!DNL Google Cloud Storage]-Ziel.

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
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `bucket.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihren eigenen [!DNL Google Cloud Storage]-Behälternamen in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `bucket.value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten Behälternamen für Ihre Integration verwenden, z. B. `"bucket.value": "my-bucket"`, setzen Sie diesen Wert auf `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Zeichenfolge | Der Name des [!DNL Google Cloud Storage]-Behälters, der von diesem Ziel verwendet werden soll. Dabei kann es sich entweder um ein Vorlagenfeld handeln, das den Wert aus den von den Benutzenden ausgefüllten [Kundendatenfeldern](../destination-configuration/customer-data-fields.md) liest (wie im Beispiel oben gezeigt), oder um einen hartcodierten Wert, z. B. `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich*. Legen Sie diesen Wert entsprechend dem Typ des im Feld `path.value` verwendeten Wertes fest.<ul><li>Wenn Sie möchten, dass Ihre Benutzerinnen und Benutzer ihren eigenen [!DNL Google Cloud Storage]-Behälterpfad in der Experience Platform-Benutzeroberfläche eingeben, setzen Sie diesen Wert auf `PEBBLE_V1`. In diesem Fall müssen Sie das Feld `path.value` mit einer Vorlage versehen, um einen Wert aus den [Kundendatenfeldern](../destination-configuration/customer-data-fields.md), die von den Benutzenden ausgefüllt werden, zu lesen. Dieser Anwendungsfall wird im obigen Beispiel gezeigt.</li><li>Wenn Sie einen hartcodierten für Ihre Integration verwenden, z. B. `"path.value": "/path/to/my-bucket"`, setzen Sie diesen Wert auf `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Zeichenfolge | Der Pfad zum [!DNL Google Cloud Storage]-Ordner, der von diesem Ziel verwendet werden soll. Dabei kann es sich entweder um ein Vorlagenfeld handeln, das den Wert aus den von den Benutzenden ausgefüllten [Kundendatenfeldern](../destination-configuration/customer-data-fields.md) liest (wie im Beispiel oben gezeigt), oder um einen hartcodierten Wert, z. B. `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, was eine Spezifikation für den Ziel-Server ist und wie Sie diese konfigurieren können.

Weitere Informationen zu den anderen Ziel-Server-Komponenten finden Sie in den folgenden Artikeln:

* [Vorlagenspezifikationen](templating-specs.md)
* [Nachrichtenformat](message-format.md)
* [Konfiguration der Dateiformatierung](file-formatting.md)
