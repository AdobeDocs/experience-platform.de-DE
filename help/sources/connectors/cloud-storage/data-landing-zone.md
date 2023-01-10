---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Datenquelle der Einstiegszone
description: Erfahren Sie, wie Sie die Einstiegszone für Daten mit Adobe Experience Platform verbinden.
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 48%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, die Ihnen Zugriff auf eine sichere, Cloud-basierte Dateispeichereinrichtung gewährt, um Dateien in Platform zu laden. Sie haben Zugriff auf einen [!DNL Data Landing Zone]-Container pro Sandbox, und das gesamte Datenvolumen über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Produkt- und Services-Lizenz von Platform bereitgestellt werden. Alle Kundinnen und Kunden von Platform sowie die zugehörigen Anwendungs-Services wie [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] und [!DNL Adobe Real-Time Customer Data Platform] erhalten einen [!DNL Data Landing Zone]-Container pro Sandbox. Sie können Dateien in Ihren Container lesen und schreiben, indem Sie [!DNL Azure Storage Explorer] oder der Befehlszeilenschnittstelle.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung, und die Daten werden im Ruhezustand und bei der Übertragung mit standardmäßigen [!DNL Azure Blob]-Speichersicherheitsmechanismen geschützt. Mit der SAS-basierten Authentifizierung können Sie sicher über eine öffentliche Internetverbindung auf Ihren [!DNL Data Landing Zone]-Container zugreifen. Für die Verwendung Ihres [!DNL Data Landing Zone]-Containers sind keine Netzwerkänderungen erforderlich. Sie müssen also keine Zulassungslisten oder regionenübergreifende Setups für Ihr Netzwerk konfigurieren. Platform erzwingt für alle Dateien, die in eine [!DNL Data Landing Zone] Container. Alle Dateien werden nach sieben Tagen gelöscht.

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie bei der Benennung Ihrer Cloud-Speicherdateien oder -Verzeichnisse berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus werden einige ASCII- oder Unicode-Zeichen, wie Steuerzeichen (wie `0x00` nach `0x1F`, `\u0081`usw.), sind ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Verwalten des Inhalts Ihrer [!DNL Data Landing Zone]

Sie können [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/de-de/features/storage-explorer/) verwenden, um die Inhalte Ihres [!DNL Data Landing Zone]-Containers zu verwalten.

Im [!DNL Azure Storage Explorer] -Benutzeroberfläche das Verbindungssymbol im linken Navigationsbereich auswählen. Das Fenster **Ressource auswählen** wird angezeigt, in dem Sie Optionen für das Verbinden finden. Auswählen **[!DNL Blob container]** zur Verbindung mit [!DNL Data Landing Zone].

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

Wählen Sie als Nächstes **Shared Access Signature URL (SAS)** als Verbindungsmethode und klicken Sie dann auf **Weiter**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

Nach Auswahl der Verbindungsmethode müssen Sie als Nächstes eine **Anzeigename** und **[!DNL Blob]Container-SAS-URL** , die Ihrer [!DNL Data Landing Zone] Container.

>[!TIP]
>
>Sie können Ihre [!DNL Data Landing Zone] Anmeldedaten aus dem Quellkatalog in der Platform-Benutzeroberfläche.

Geben Sie Ihre SAS-URL für die [!DNL Data Landing Zone] an und klicken Sie dann auf **Weiter**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

Das Fenster **Zusammenfassung** wird angezeigt. Es gibt Ihnen einen Überblick über Ihre Einstellungen, einschließlich Informationen zu Ihrem [!DNL Blob]-Endpunkt und Berechtigungen. Wenn Sie bereit sind, klicken Sie auf **Verbinden**.

![Zusammenfassung](../../images/tutorials/create/dlz/summary.png)

Eine erfolgreiche Verbindung aktualisiert Ihre Benutzeroberfläche von [!DNL Azure Storage Explorer] mit Ihrem [!DNL Data Landing Zone]-Container.

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

Mit [!DNL Data Landing Zone] Container, der mit [!DNL Azure Storage Explorer], können Sie jetzt mit dem Hochladen von Dateien in Ihre [!DNL Data Landing Zone] Container. Wählen Sie zum Hochladen **Hochladen** und wählen Sie **Hochladen von Dateien**.

![hochladen](../../images/tutorials/create/dlz/upload.png)

Nachdem Sie die hochzuladende Datei ausgewählt haben, müssen Sie die [!DNL Blob] Geben Sie ein, dass Sie es als und das gewünschte Zielverzeichnis hochladen möchten. Wenn Sie fertig sind, wählen Sie **Hochladen**.

| [!DNL Blob] Typen | Beschreibung |
| --- | --- |
| Block [!DNL Blob] | Block [!DNL Blobs] sind für das effiziente Hochladen großer Datenmengen optimiert. Block [!DNL Blobs] sind die Standardoption für [!DNL Data Landing Zone]. |
| Anhängen [!DNL Blob] | Anhängen [!DNL Blobs] sind für das Anhängen von Daten an das Dateiende optimiert. |

![upload-files](../../images/tutorials/create/dlz/upload-files.png)

## Hochladen von Dateien in Ihre [!DNL Data Landing Zone] über die Befehlszeilenschnittstelle

Sie können auch die Befehlszeilenschnittstelle Ihres Geräts verwenden und auf die Upload-Dateien zu Ihrem [!DNL Data Landing Zone].

### Datei mit Bash hochladen

Im folgenden Beispiel werden Bash und cURL verwendet, um eine Datei in eine [!DNL Data Landing Zone] mit dem [!DNL Azure Blob Storage] REST-API:

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### Datei mit Python hochladen

Das folgende Beispiel verwendet [!DNL Microsoft's] Python v12 SDK zum Hochladen einer Datei in ein [!DNL Data Landing Zone]:

>[!TIP]
>
>Während im folgenden Beispiel der vollständige SAS-URI zum Herstellen einer Verbindung zu einem [!DNL Azure Blob] -Container können Sie andere Methoden und Vorgänge zur Authentifizierung verwenden. Siehe dies [[!DNL Microsoft] Dokument zum Python v12 SDK](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) für weitere Informationen.

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### Eine Datei hochladen mit [!DNL AzCopy]

Das folgende Beispiel verwendet [!DNL Microsoft's] [!DNL AzCopy] Dienstprogramm zum Hochladen einer Datei in eine [!DNL Data Landing Zone]:

>[!TIP]
>
>Während im folgenden Beispiel die Variable `copy` können Sie andere Befehle und Optionen verwenden, um eine Datei in Ihre [!DNL Data Landing Zone]verwendet [!DNL AzCopy]. Siehe dies [[!DNL Microsoft AzCopy] Dokument](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) für weitere Informationen.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Verbinden [!DNL Data Landing Zone] nach [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen zum Datenimport von [!DNL Data Landing Zone] -Container mit Adobe Experience Platform mithilfe von APIs oder der Benutzeroberfläche erstellen.

### Verwenden von APIs

- [Erstellen Sie eine [!DNL Data Landing Zone] Quellverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Verbinden von  [!DNL Data Landing Zone]  mit Platform über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
