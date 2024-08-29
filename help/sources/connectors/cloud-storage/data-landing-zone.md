---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Data Landing Zone Source
description: Erfahren Sie, wie Sie die Data Landing Zone mit Adobe Experience Platform verbinden.
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecef17ed454c7b1f30543278bba6b0e3b70399da
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 33%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Diese Seite ist spezifisch für den [!DNL Data Landing Zone] *source* -Connector im Experience Platform. Informationen zum Herstellen einer Verbindung zum [!DNL Data Landing Zone] *Ziel*-Connector finden Sie auf der Seite [[!DNL Data Landing Zone] Zieldokumentation](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte [!DNL Azure Blob] Speicherschnittstelle, über die Sie auf eine sichere, Cloud-basierte Dateispeichereinrichtung zugreifen können, um Dateien in Platform zu laden. Sie haben Zugriff auf einen [!DNL Data Landing Zone]-Container pro Sandbox, und das gesamte Datenvolumen über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Produkt- und Services-Lizenz von Platform bereitgestellt werden. Alle Experience Platform-Kunden erhalten einen [!DNL Data Landing Zone] -Container pro Sandbox. Sie können Dateien in Ihren Container über [!DNL Azure Storage Explorer] oder Ihre Befehlszeilenschnittstelle lesen und schreiben.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung, und die Daten werden im Ruhezustand und bei der Übertragung mit standardmäßigen [!DNL Azure Blob]-Speichersicherheitsmechanismen geschützt. Mit der SAS-basierten Authentifizierung können Sie sicher über eine öffentliche Internetverbindung auf Ihren [!DNL Data Landing Zone]-Container zugreifen. Es sind keine Netzwerkänderungen erforderlich, damit Sie auf Ihren [!DNL Data Landing Zone] -Container zugreifen können. Dies bedeutet, dass Sie keine Zulassungslisten oder regionenübergreifenden Setups für Ihr Netzwerk konfigurieren müssen. Experience Platform erzwingt eine strikte Ablaufzeit von sieben Tagen für alle Dateien und Ordner, die in einen [!DNL Data Landing Zone] -Container hochgeladen wurden. Alle Dateien und Ordner werden nach sieben Tagen gelöscht.

>[!NOTE]
>
>Wenn Sie über [!DNL Azure Data Factory] auf [!DNL Data Landing Zone] zugreifen möchten, müssen Sie einen verknüpften Dienst für [!DNL Data Landing Zone] mit den von Experience Platform bereitgestellten [SAS-Anmeldedaten](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials) erstellen. Nachdem Sie den verknüpften Dienst erstellt haben, können Sie Ihre [!DNL Data Landing Zone] durchsuchen, indem Sie anstelle des standardmäßigen Stammpfads den Containerpfad auswählen.

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie bei der Benennung Ihrer Cloud-Speicherdateien oder -Verzeichnisse berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen, wie Steuerzeichen (z. B. `0x00` bis `0x1F`, `\u0081` usw.), ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Verwalten des Inhalts Ihrer Data Landing Zone{#manage-the-contents-of-your-data-landing-zone}

Sie können [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/de-de/features/storage-explorer/) verwenden, um die Inhalte Ihres [!DNL Data Landing Zone]-Containers zu verwalten.

Wählen Sie in der Benutzeroberfläche von [!DNL Azure Storage Explorer] das Verbindungssymbol im linken Navigationsbereich aus. Das Fenster **Ressource auswählen** wird angezeigt, in dem Sie Optionen für das Verbinden finden. Wählen Sie **[!DNL Blob container]** aus, um eine Verbindung zu [!DNL Data Landing Zone] herzustellen.

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

Wählen Sie als Nächstes **Shared Access Signature URL (SAS)** als Verbindungsmethode und klicken Sie dann auf **Weiter**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

Nach Auswahl Ihrer Verbindungsmethode müssen Sie als Nächstes einen **Anzeigenamen** und die **[!DNL Blob]Container-SAS-URL** angeben, die Ihrem [!DNL Data Landing Zone] -Container entsprechen.

>[!TIP]
>
>Sie können Ihre [!DNL Data Landing Zone] -Anmeldedaten aus dem Quellkatalog in der Platform-Benutzeroberfläche abrufen.

Geben Sie Ihre [!DNL Data Landing Zone] SAS-URL ein und wählen Sie dann **Weiter** aus.

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

Das Fenster **Zusammenfassung** wird angezeigt. Es gibt Ihnen einen Überblick über Ihre Einstellungen, einschließlich Informationen zu Ihrem [!DNL Blob]-Endpunkt und Berechtigungen. Wenn Sie bereit sind, klicken Sie auf **Verbinden**.

![Zusammenfassung](../../images/tutorials/create/dlz/summary.png)

Eine erfolgreiche Verbindung aktualisiert Ihre Benutzeroberfläche von [!DNL Azure Storage Explorer] mit Ihrem [!DNL Data Landing Zone]-Container.

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

Wenn Ihr [!DNL Data Landing Zone] -Container mit [!DNL Azure Storage Explorer] verbunden ist, können Sie jetzt mit dem Hochladen von Dateien in Ihren [!DNL Data Landing Zone] -Container beginnen. Wählen Sie zum Hochladen **Hochladen** und dann **Dateien hochladen** aus.

![upload](../../images/tutorials/create/dlz/upload.png)

Nachdem Sie die hochzuladende Datei ausgewählt haben, müssen Sie den [!DNL Blob]-Typ, als den Sie sie hochladen möchten, und das gewünschte Zielverzeichnis angeben. Wählen Sie abschließend **Upload** aus.

| [!DNL Blob] types | Beschreibung |
| --- | --- |
| Block [!DNL Blob] | Block [!DNL Blobs] ist für das effiziente Hochladen großer Datenmengen optimiert. Block [!DNL Blobs] ist die Standardoption für [!DNL Data Landing Zone]. |
| Anhängen von [!DNL Blob] | Das Anhängen von [!DNL Blobs] ist für das Anhängen von Daten an das Ende der Datei optimiert. |

![upload-files](../../images/tutorials/create/dlz/upload-files.png)

## Hochladen von Dateien in Ihre [!DNL Data Landing Zone] über die Befehlszeilenschnittstelle

Sie können auch die Befehlszeilenschnittstelle Ihres Geräts verwenden und auf die Upload-Dateien zu Ihrem [!DNL Data Landing Zone] zugreifen.

### Datei mit Bash hochladen

Im folgenden Beispiel werden Bash und cURL verwendet, um eine Datei mit der REST-API [!DNL Azure Blob Storage] in eine Datei mit dem Wert [!DNL Data Landing Zone] hochzuladen:

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

Im folgenden Beispiel wird [!DNL Microsoft's] Python v12 SDK verwendet, um eine Datei in ein [!DNL Data Landing Zone] hochzuladen:

>[!TIP]
>
>Im folgenden Beispiel wird zwar der vollständige SAS-URI verwendet, um eine Verbindung zu einem [!DNL Azure Blob] -Container herzustellen, Sie können jedoch andere Methoden und Vorgänge verwenden, um sich zu authentifizieren. Weitere Informationen finden Sie in diesem [[!DNL Microsoft] Dokument im Python v12 SDK](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) .

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

### Eine Datei mit [!DNL AzCopy] hochladen

Im folgenden Beispiel wird das Dienstprogramm [!DNL Microsoft's] [!DNL AzCopy] verwendet, um eine Datei in eine [!DNL Data Landing Zone] hochzuladen:

>[!TIP]
>
>Im folgenden Beispiel wird zwar der Befehl `copy` verwendet, Sie können jedoch mithilfe von [!DNL AzCopy] andere Befehle und Optionen zum Hochladen einer Datei in Ihren [!DNL Data Landing Zone] verwenden. Weitere Informationen finden Sie in diesem [[!DNL Microsoft AzCopy] Dokument](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) .

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## [!DNL Data Landing Zone] mit [!DNL Platform] verbinden

Die folgende Dokumentation enthält Informationen dazu, wie Sie Daten aus Ihrem [!DNL Data Landing Zone] -Container mit APIs oder der Benutzeroberfläche in Adobe Experience Platform importieren können.

### Verwenden von APIs

- [Erstellen einer [!DNL Data Landing Zone] Quellverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Verbinden von [!DNL Data Landing Zone] mit Platform über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>Private Links werden derzeit nicht unterstützt, wenn eine Verbindung mit Experience Platform über den [!DNL Data Landing Zone] hergestellt wird. Die einzigen unterstützten Zugriffsmethoden sind die in [hier](#manage-the-contents-of-your-data-landing-zone) aufgeführten Methoden.

