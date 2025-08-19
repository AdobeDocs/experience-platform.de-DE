---
title: Azure Blob Source Connector - Übersicht
description: Erfahren Sie, wie Sie Ihr Azure Blob-Konto mit Experience Platform verbinden
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: f659d78eebc1c5e74021f9a41a2a489389a6588e
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 21%

---

# [!DNL Azure Blob Storage]

[!DNL Azure Blob Storage] ist ein Cloud-basierter Objektspeicher-Service, der von [!DNL Microsoft Azure] bereitgestellt wird. Es wurde entwickelt, um große Mengen unstrukturierter Daten zu speichern, z. B. Text, Bilder, Videos, Backups und Protokolle. Sie können [!DNL Azure Blob Storage] verwenden, um große Mengen unstrukturierter Daten wie Dokumente, Bilder, Videos und Audiodateien zu speichern und zu verwalten. Es eignet sich ideal für die Sicherung und Archivierung von Daten, die Unterstützung der Notfall-Wiederherstellung und die Handhabung von Big Data-Workloads für Analysen.

Verwenden Sie die [!DNL Azure Blob Storage], um Ihr Konto zu verbinden und Daten von [!DNL Azure Blob Storage] in Adobe Experience Platform aufzunehmen.

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte, um die erforderliche Einrichtung abzuschließen, bevor Sie Ihr [!DNL Azure Blob Storage]-Konto mit Experience Platform verbinden.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung ](../../ip-address-allow-list.md) Experience Platform.

>[!IMPORTANT]
>
>Die [!DNL Azure Blob]-Quelle unterstützt keine Konnektivität derselben Region mit Experience Platform. Wenn Ihre [!DNL Azure] dieselbe Netzwerkregion wie Experience Platform verwendet, kann keine Verbindung zu Experience Platform-Quellen hergestellt werden. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt.

### Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

### [!DNL Azure Blob Storage] bei Experience Platform authentifizieren {#authentication}

Sie können Ihr [!DNL Azure Blob Storage]-Konto mit Experience Platform verbinden, indem Sie die folgenden Authentifizierungstypen verwenden:

- **Kontoschlüsselauthentifizierung**: Verwendet den Zugriffsschlüssel des Speicherkontos zur Authentifizierung und Verbindung mit Ihrem [!DNL Azure Blob Storage].
- **Shared Access Signature (SAS)**: Verwendet einen SAS-URI, um delegierten, zeitlich begrenzten Zugriff auf Ressourcen in Ihrem [!DNL Azure Blob Storage]-Konto bereitzustellen.
- **Service-Prinzipal-basierte Authentifizierung**: Verwendet einen Azure Active Directory (AAD)-Service-Prinzipal (Client-ID und Geheimnis) zur sicheren Authentifizierung bei Ihrem Azure Blob Storage-Konto.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihr [!DNL Azure Blob Storage]-Konto mithilfe der Kontoschlüsselauthentifizierung mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `connectionString` | Die [!DNL Azure Blob Storage] Verbindungszeichenfolge für Ihr Speicherkonto. Diese Zeichenfolge enthält die Informationen, die zur Authentifizierung und Verbindung mit Ihrer [!DNL Azure Blob Storage]-Instanz erforderlich sind. Beispielformat: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | Der Name des [!DNL Azure Blob Storage]-Containers, in dem Ihre Datendateien gespeichert werden. Ein Container organisiert einen Satz von Blobs, ähnlich einem Verzeichnis in einem Dateisystem. |
| `folderPath` | Der Pfad innerhalb des angegebenen Containers, in dem sich Ihre Dateien befinden. Dies ist ein optionaler Unterverzeichnispfad (virtueller Ordner) innerhalb des Containers. Wenn Sie das Feld leer lassen, wird der Stamm des Containers verwendet. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Azure Blob Storage] ist `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Hinweis**: Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

Weitere Informationen zur Verwendung der Kontoschlüsselauthentifizierung mit [!DNL Azure Blob Storage] finden Sie im offiziellen [Microsoft Azure-Authentifizierungshandbuch](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication).

>[!TAB Shared Access Signature]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihr [!DNL Azure Blob Storage]-Konto mithilfe einer freigegebenen Zugriffssignatur mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `SasURI` | Der Signatur-URI für den gemeinsamen Zugriff, den Sie als alternativen Authentifizierungstyp zum Verbinden Ihres Kontos verwenden können. Das SAS-URI-Muster lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. Weitere Informationen finden Sie in diesem [!DNL Azure] Dokument zu [Shared Access Signature URIs](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | Der Name des [!DNL Azure Blob Storage]-Containers, in dem Ihre Datendateien gespeichert werden. Ein Container organisiert einen Satz von Blobs, ähnlich einem Verzeichnis in einem Dateisystem. |
| `folderPath` | Der Pfad innerhalb des angegebenen Containers, in dem sich Ihre Dateien befinden. Dies ist ein optionaler Unterverzeichnispfad (virtueller Ordner) innerhalb des Containers. Wenn Sie das Feld leer lassen, wird der Stamm des Containers verwendet. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Azure Blob Storage] ist `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Hinweis**: Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

Weitere Informationen zur Verwendung der freigegebenen Zugriffssignatur mit [!DNL Azure Blob Storage] finden Sie im offiziellen [Authentifizierungshandbuch für Microsoft Azure](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication).

>[!TAB Auf Service-Prinzipalen basierende Authentifizierung]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihr [!DNL Azure Blob Storage]-Konto mithilfe einer auf Service-Prinzipalen basierenden Authentifizierung mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `serviceEndpoint` | Die Endpunkt-URL Ihres [!DNL Azure Blob Storage]. Normalerweise im Format: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `accountKind` | Der Typ Ihres [!DNL Azure Blob Storage]. Häufige Werte sind `StorageV2`, `BlobStorage` oder `Storage`. |
| `servicePrincipalId` | Die Client-/Anwendungs-ID des für die Authentifizierung verwendeten Azure Active Directory (AAD)-Service-Prinzipals. |
| `servicePrincipalKey` | Das mit dem Azure-Service-Prinzipal verknüpfte Client-Geheimnis oder Kennwort. |
| `tenant` | Die Azure Active Directory (AAD)-Mandanten-ID, in der der Service-Prinzipal registriert ist. |
| `container` | Der Name des Azure Blob Storage-Containers, in dem Ihre Datendateien gespeichert werden. |
| `folderPath` | Der Pfad innerhalb des angegebenen Containers, in dem sich Ihre Dateien befinden. Dies ist ein optionaler Unterverzeichnispfad (virtueller Ordner) innerhalb des Containers. Wenn Sie das Feld leer lassen, wird der Stamm des Containers verwendet. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für Azure Blob Storage ist `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Hinweis**: Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

Weitere Informationen zur Verwendung der Authentifizierung über Service-Prinzipale mit [!DNL Azure Blob Storage] finden Sie im offiziellen [Microsoft Azure-Authentifizierungshandbuch](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication).

>[!ENDTABS]

## [!DNL Azure Blob Storage] mit [!DNL Experience Platform] verbinden

Die folgende Dokumentation enthält Informationen zum Verbinden von Azure Blob mit Adobe Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

### Verwenden von APIs

- [Verbindung  [!DNL Azure Blob Storage]  Experience Platform herstellen](../../tutorials/api/create/cloud-storage/blob.md)
- [Untersuchen der Datenstruktur und des Inhalts einer Cloud-Speicherquelle mit der Flow Service-API](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Verbindung  [!DNL Azure Blob Storage]  Experience Platform herstellen](../../tutorials/ui/create/cloud-storage/blob.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
