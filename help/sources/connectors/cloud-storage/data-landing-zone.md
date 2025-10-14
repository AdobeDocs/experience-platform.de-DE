---
title: Data Landing Zone Source
description: Erfahren Sie, wie Sie die Data Landing Zone mit Adobe Experience Platform verbinden
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 18%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Diese Seite ist spezifisch für den [!DNL Data Landing Zone]-Quell *Connector* Experience Platform. Informationen zum Herstellen einer Verbindung zum [!DNL Data Landing Zone]-*-*-Connector finden Sie auf [[!DNL Data Landing Zone] Zieldokumentationsseite](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, über die Sie auf eine sichere, Cloud-basierte Dateispeichereinrichtung zugreifen können, um Dateien in Experience Platform zu laden. Sie haben Zugriff auf einen [!DNL Data Landing Zone]-Container pro Sandbox, und das gesamte Datenvolumen über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Experience Platform-Produkt- und -Services-Lizenz bereitgestellt werden. Alle Kundinnen und Kunden von Experience Platform erhalten einen [!DNL Data Landing Zone]-Container pro Sandbox. Sie können Dateien in Ihrem Container lesen und schreiben, indem Sie [!DNL Azure Storage Explorer] oder die Befehlszeilenschnittstelle verwenden.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung, und die Daten werden im Ruhezustand und bei der Übertragung mit standardmäßigen [!DNL Azure Blob]-Speichersicherheitsmechanismen geschützt. Mit der SAS-basierten Authentifizierung können Sie sicher über eine öffentliche Internetverbindung auf Ihren [!DNL Data Landing Zone]-Container zugreifen. Für den Zugriff auf Ihren [!DNL Data Landing Zone]-Container sind keine Netzwerkänderungen erforderlich. Sie müssen also keine Zulassungslisten oder regionenübergreifende Setups für Ihr Netzwerk konfigurieren. Experience Platform erzwingt eine strikte siebentägige Gültigkeitsdauer für alle Dateien und Ordner, die in einen [!DNL Data Landing Zone]-Container hochgeladen werden. Alle Dateien und Ordner werden nach sieben Tagen gelöscht.

## Einrichten der [!DNL Data Landing Zone] für Experience Platform auf Azure {#azure}

Gehen Sie wie folgt vor, um zu erfahren, wie Sie Ihr [!DNL Data Landing Zone] für Experience Platform auf Azure einrichten können.

>[!NOTE]
>
>Experience Platform Wenn Sie über [!DNL Azure Data Factory] auf [!DNL Data Landing Zone] zugreifen möchten, müssen Sie einen verknüpften Service für [!DNL Data Landing Zone] mithilfe der von bereitgestellten [SAS](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials)Anmeldeinformationen erstellen. Nachdem Sie Ihren verknüpften Service erstellt haben, können Sie Ihre [!DNL Data Landing Zone] untersuchen, indem Sie den Container-Pfad anstelle des standardmäßigen Stammpfads auswählen.

### Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdateien oder -Verzeichnisse berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen, z. B. Steuerzeichen (`0x00` zu `0x1F`, `\u0081` usw.), ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

### Verwalten des Inhalts Ihrer Data Landing Zone{#manage-the-contents-of-your-data-landing-zone}

Sie können [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/de-de/features/storage-explorer/) verwenden, um die Inhalte Ihres [!DNL Data Landing Zone]-Containers zu verwalten.

Wählen Sie in der [!DNL Azure Storage Explorer]-Benutzeroberfläche im linken Navigationsbereich das Verbindungssymbol aus. Das Fenster **Ressource auswählen** wird angezeigt, in dem Sie Optionen für das Verbinden finden. Wählen Sie **[!DNL Blob container]** aus, um eine Verbindung zu [!DNL Data Landing Zone] herzustellen.

![Der ausgewählte Ressourcenarbeitsbereich in Azure Explorer.](../../images/tutorials/create/dlz/select-resource.png)

Wählen Sie als Nächstes **Shared Access Signature URL (SAS)** als Verbindungsmethode und klicken Sie dann auf **Weiter**.

![Die Verbindungsmethode im Azure Explorer mit ausgewählter Signatur für freigegebenen Zugriff auswählen.](../../images/tutorials/create/dlz/select-connection-method.png)

Nachdem Sie Ihre Verbindungsmethode ausgewählt haben, müssen Sie als Nächstes einen **Anzeigenamen** und die **[!DNL Blob]-Container-SAS-** angeben, die Ihrem [!DNL Data Landing Zone]-Container entspricht.

>[!TIP]
>
>Sie können Ihre [!DNL Data Landing Zone]-Anmeldeinformationen aus dem Quellkatalog in der Experience Platform-Benutzeroberfläche abrufen.

Geben Sie Ihre [!DNL Data Landing Zone] SAS-URL ein und klicken Sie dann auf **Weiter**

![Den Arbeitsbereich „Verbindungsinformationen eingeben“ im Azure Explorer, in den der Anzeigename und die SAS-URL eingegeben werden.](../../images/tutorials/create/dlz/enter-connection-info.png)

Das Fenster **Zusammenfassung** wird angezeigt. Es gibt Ihnen einen Überblick über Ihre Einstellungen, einschließlich Informationen zu Ihrem [!DNL Blob]-Endpunkt und Berechtigungen. Wenn Sie bereit sind, klicken Sie auf **Verbinden**.

![Der Übersichtsarbeitsbereich des Azure Explorers, in dem die Einstellungen Ihrer Ressourcenverbindung zusammengefasst sind.](../../images/tutorials/create/dlz/summary.png)

Eine erfolgreiche Verbindung aktualisiert Ihre Benutzeroberfläche von [!DNL Azure Storage Explorer] mit Ihrem [!DNL Data Landing Zone]-Container.

![Der Navigationsarbeitsbereich der Data Landing Zone im Azure Explorer.](../../images/tutorials/create/dlz/dlz-user-container.png)

Da Ihr [!DNL Data Landing Zone]-Container jetzt mit [!DNL Azure Storage Explorer] verbunden ist, können Sie damit beginnen, Dateien in Ihren [!DNL Data Landing Zone]-Container hochzuladen. Wählen Sie zum Hochladen **Hochladen** und dann **Dateien hochladen** aus.

![Der Arbeitsbereich „Dateien hochladen“ von Azure Explorer.](../../images/tutorials/create/dlz/upload.png)

Nachdem Sie die Datei ausgewählt haben, die Sie hochladen möchten, müssen Sie dann den [!DNL Blob], den Sie hochladen möchten, und Ihr gewünschtes Zielverzeichnis angeben. Wenn Sie fertig sind, wählen Sie **Hochladen** aus.

| [!DNL Blob] | Beschreibung |
| --- | --- |
| [!DNL Blob] | [!DNL Blobs] sind für das effiziente Hochladen großer Datenmengen optimiert. [!DNL Blobs] sind die Standardoption für [!DNL Data Landing Zone]. |
| [!DNL Blob] anhängen | Das Anhängen von [!DNL Blobs] wurde für das Anhängen von Daten an das Ende der Datei optimiert. |

![Das Fenster Dateien hochladen von Azure Explorer, in dem die ausgewählten Dateien, der Blob-Typ und die Zielkategorie angezeigt werden.](../../images/tutorials/create/dlz/upload-files.png)

### Hochladen von Dateien in Ihr [!DNL Data Landing Zone] über die Befehlszeilenschnittstelle

Sie können auch die Befehlszeilenschnittstelle Ihres Geräts verwenden und auf Dateien in Ihr [!DNL Data Landing Zone] zugreifen.

### Hochladen einer Datei mit Bash

Im folgenden Beispiel werden Bash und cURL verwendet, um mit der [!DNL Azure Blob Storage] REST-API eine Datei in eine [!DNL Data Landing Zone] hochzuladen:

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

### Hochladen einer Datei mit Python

Im folgenden Beispiel wird [!DNL Microsoft's] Python v12 SDK zum Hochladen einer Datei in eine [!DNL Data Landing Zone] verwendet:

>[!TIP]
>
>Während im folgenden Beispiel der vollständige SAS-URI zum Herstellen einer Verbindung mit einem [!DNL Azure Blob]-Container verwendet wird, können Sie zur Authentifizierung andere Methoden und Vorgänge verwenden. Weitere Informationen finden [[!DNL Microsoft]  in diesem Dokument zu Python v12](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python)SDK.

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

### Hochladen einer Datei mit [!DNL AzCopy]

Im folgenden Beispiel wird [!DNL Microsoft's] Dienstprogramm [!DNL AzCopy] zum Hochladen einer Datei in eine [!DNL Data Landing Zone] verwendet:

>[!TIP]
>
>Während im folgenden Beispiel der Befehl `copy` verwendet wird, können Sie mithilfe von [!DNL AzCopy] andere Befehle und Optionen verwenden, um eine Datei in Ihr [!DNL Data Landing Zone] hochzuladen. Weitere Informationen finden [[!DNL Microsoft AzCopy]  in diesem &#x200B;](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json).

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Einrichten der [!DNL Data Landing Zone] für Experience Platform auf Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](https://experienceleague.adobe.com/de/docs/experience-platform/landing/multi-cloud).

Gehen Sie wie folgt vor, um zu erfahren, wie Sie Ihr [!DNL Data Landing Zone] für Experience Platform auf Amazon Web Services (AWS) einrichten können.

### AUF DIE ZULASSUNGSLISTE SETZEN IP-Adresse für die Verbindung mit AWS

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform in AWS verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform auf AWS](../../ip-address-allow-list.md) .

### Einrichten der AWS-CLI und Ausführen von Vorgängen

- Lesen Sie das Handbuch unter [Installieren oder Aktualisieren auf die neueste Version der AWS-CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

### Konfigurieren von AWS CLI mit temporären Anmeldedaten

Verwenden Sie den AWS-`configure`, um Ihre CLI mit Zugriffsschlüsseln und einem Sitzungs-Token einzurichten.

```shell
aws configure
```

Geben Sie nach Aufforderung die folgenden Werte ein:

- AWS-Zugriffsschlüssel-ID: `{YOUR_ACCESS_KEY_ID}`
- Geheimer AWS-Zugriffsschlüssel: `{YOUR_SECRET_ACCESS_KEY}`
- Name der Standardregion: `{YOUR_REGION}` (z. B. `us-west-2`)
- Standardausgabeformat: `json`

Legen Sie als Nächstes das Sitzungs-Token fest:

```shell
aws configure set aws_session_token your-session-token
```

### Arbeiten mit Dateien in [!DNL Amazon S3]

>[!BEGINTABS]

>[!TAB Datei in Amazon S3 hochladen]

Vorlage:

```shell
aws s3 cp local-file-path s3://bucketName/dlzFolder/remote-file-Name
```

Beispiel:

```shell
aws s3 cp example.txt s3://bucketName/dlzFolder/example.txt
```


>[!TAB Datei von Amazon S3 herunterladen]

Vorlage:

```shell
aws s3 cp s3://bucketName/dlzFolder/remote-file local-file-path
```

Beispiel:

```shell
aws s3 cp s3://bucketName/dlzFolder/example.txt example.txt
```

>[!ENDTABS]

### Verwenden Sie Ihre [!DNL Data Landing Zone] Anmeldedaten, um sich bei der AWS-Konsole anzumelden

#### Extrahieren der Anmeldeinformationen

Zunächst müssen Sie Folgendes abrufen:

- `awsAccessKeyId`
- `awsSecretAccessKey`
- `awsSessionToken`

#### Erstellen eines Anmelde-Tokens

Verwenden Sie als Nächstes die extrahierten Anmeldeinformationen, um eine Sitzung zu erstellen und ein Anmelde-Token mit dem AWS Federation-Endpunkt zu generieren:

```py
import json
import requests
 
# Example DLZ response with credentials
response_json = '''{
    "credentials": {
        "awsAccessKeyId": "your-access-key",
        "awsSecretAccessKey": "your-secret-key",
        "awsSessionToken": "your-session-token"
    }
}'''
 
# Parse credentials
response_data = json.loads(response_json)
aws_access_key_id = response_data['credentials']['awsAccessKeyId']
aws_secret_access_key = response_data['credentials']['awsSecretAccessKey']
aws_session_token = response_data['credentials']['awsSessionToken']
 
# Create session dictionary
session = {
    'sessionId': aws_access_key_id,
    'sessionKey': aws_secret_access_key,
    'sessionToken': aws_session_token
}
 
# Generate the sign-in token
signin_token_url = "https://signin.aws.amazon.com/federation"
signin_token_payload = {
    "Action": "getSigninToken",
    "Session": json.dumps(session)
}
signin_token_response = requests.post(signin_token_url, data=signin_token_payload)
signin_token = signin_token_response.json()['SigninToken']
```

#### Erstellen der Anmelde-URL der AWS-Konsole

Sobald Sie über ein Anmelde-Token verfügen, können Sie die URL erstellen, die Sie in der AWS-Konsole protokolliert und direkt auf den gewünschten [!DNL Amazon S3] verweist.

```py
from urllib.parse import quote
 
# Define the S3 bucket and folder path you want to access
bucket_name = "your-bucket-name"
bucket_path = "your-bucket-folder"
 
# Construct the destination URL
destination_url = f"https://s3.console.aws.amazon.com/s3/buckets/{bucket_name}?prefix={bucket_path}/&tab=objects"
 
# Create the final sign-in URL
signin_url = f"https://signin.aws.amazon.com/federation?Action=login&Issuer=YourAppName&Destination={quote(destination_url)}&SigninToken={signin_token}"
 
print(f"Sign-in URL: {signin_url}")
```

#### Zugriff auf AWS Console

Navigieren Sie abschließend zur generierten URL, um sich mit Ihren [!DNL Data Landing Zone]-Anmeldeinformationen direkt bei der AWS-Konsole anzumelden. Dadurch erhalten Sie Zugriff auf einen bestimmten Ordner in einem [!DNL Amazon S3]. Die Anmelde-URL führt Sie direkt zu diesem Ordner, sodass Sie nur zulässige Daten sehen und verwalten können.

## Verbinden von [!DNL Data Landing Zone] mit Experience Platform

>[!IMPORTANT]
>
>- Um eine Verbindung zur Quelle herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Quellen anzeigen]** und **[!UICONTROL Quellen verwalten]** . Weitere Informationen finden Sie unter [Zugriffskontrolle - Übersicht](../../../access-control/home.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>
>- Private Links werden derzeit nicht unterstützt, wenn eine Verbindung zu Experience Platform über die -[!DNL Data Landing Zone] hergestellt wird. Die einzigen unterstützten Methoden für den Zugriff sind die [hier](#manage-the-contents-of-your-data-landing-zone) aufgelisteten Methoden.

Die folgende Dokumentation enthält Informationen dazu, wie Sie Daten aus Ihrem [!DNL Data Landing Zone]-Container mithilfe von APIs oder der Benutzeroberfläche in Adobe Experience Platform importieren können.

### Verwenden von APIs

- [Erstellen  [!DNL Data Landing Zone]  Quellverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Verbindung  [!DNL Data Landing Zone]  Experience Platform über die Benutzeroberfläche herstellen](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)

