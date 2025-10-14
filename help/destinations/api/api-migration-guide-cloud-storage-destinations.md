---
solution: Experience Platform
title: API-Migrationshandbuch für Cloud-Speicher-Ziele
description: Erfahren Sie mehr über die Änderungen im Workflow zum Aktivieren von Cloud-Speicher-Zielen im Rahmen der Migration zu den neuen Cloud-Speicher-Zielkarten mit zusätzlichen Funktionen.
type: Tutorial
exl-id: 4acaf718-794e-43a3-b8f0-9b19177a2bc0
source-git-commit: 4b9e7c22282a5531f2f25f3d225249e4eb0e178e
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 2%

---

# API-Migrationshandbuch für Cloud-Speicher-Ziele

>[!IMPORTANT]
>
>* Die auf dieser Seite beschriebene Funktion steht Kunden zur Verfügung, die die Pakete Real-Time CDP Prime und Ultimate erworben haben. Bitte wenden Sie sich an den Adobe-Support-Mitarbeiter, um weitere Informationen zu erhalten.

## Migrationskontext {#migration-context}

Ab [Oktober 2022](/help/release-notes/2022/october-2022.md#new-or-updated-destinations) können Sie die neuen Dateiexportfunktionen verwenden, um beim Exportieren von Dateien von Experience Platform auf erweiterte Anpassungsfunktionen zuzugreifen:

* Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* Möglichkeit zum Festlegen benutzerdefinierter Dateikopfzeilen in exportierten Dateien über den [&#x200B; Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* Möglichkeit zur Auswahl des [Dateityps](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) der exportierten Datei.
* Möglichkeit zum [Anpassen der Formatierung exportierter CSV-Datendateien](/help/destinations/ui/batch-destinations-file-formatting-options.md).

Diese Funktion wird von den unten aufgeführten Beta-Cloud-Speicherkarten unterstützt:

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

Beachten Sie, dass Sie derzeit in der Experience Platform-Benutzeroberfläche zwei nebeneinander liegende Zielkarten der drei Ziele sehen können. Nachfolgend sind die alten und neuen Ziele von [!DNL Amazon S3] aufgeführt. In allen Fällen sind die mit **Beta** markierten Karten die neuen Zielkarten.

![Abbildung der beiden Amazon S3-Zielkarten, die diese nebeneinander in einer Ansicht zeigt.](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Diese Ziele mit erweiterten Funktionen wurden ursprünglich als Beta-Version angeboten, *Adobe transferiert jetzt alle Real-Time CDP-Kunden zu den neuen Cloud-Speicher-Zielen*. Für Kunden, die bereits [!DNL Amazon S3], [!DNL Azure Blob] oder SFTP verwendet haben, bedeutet dies, dass vorhandene Datenflüsse zu den neuen Karten migriert werden. Weitere Informationen zu den spezifischen Änderungen im Rahmen der Migration finden Sie im Folgenden.

## Für wen diese Seite gilt {#who-this-applies-to}

Wenn Sie bereits die [Flow Service-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) zum Exportieren von Profilen an die Amazon S3-, Azure Blob- oder SFTP-Cloud-Speicherziele verwenden, gilt dieses API-Migrationshandbuch für Sie.

Wenn Sie Skripte in Ihren [!DNL Amazon S3]-, [!DNL Azure Blob]- oder SFTP-Cloud-Speicherorten auf den von Experience Platform exportierten Dateien ausführen, beachten Sie, dass sich einige Parameter in Bezug auf die Verbindungs- und Flussspezifikationen der neuen Karten sowie in Bezug auf den Zuordnungsschritt ändern.

Wenn Sie beispielsweise ein Skript verwenden, um Ziel-Datenflüsse zum [!DNL Amazon S3]-Ziel basierend auf der Verbindungsspezifikation des [!DNL Amazon S3]-Ziels zu filtern, beachten Sie, dass sich die Verbindungsspezifikation ändert, sodass Sie Ihre Filter aktualisieren müssen.

## Links zu relevanten Dokumentationen {#relevant-documentation-links}

Dieser Abschnitt enthält das entsprechende API-Tutorial und die Referenzdokumentation für die erweiterte Funktion zum Exportieren von Daten in Cloud-Speicher-Ziele.

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [API-Tutorial zum Exportieren von Zielgruppen in Cloud-Speicher-Ziele](/help/destinations/api/activate-segments-file-based-destinations.md)
* [Referenzdokumentation zur Destinations Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## Zusammenfassung der abwärtsinkompatiblen Änderungen {#summary-backwards-incompatible-changes}

Mit der Migration zu den neuen Zielen werden allen Ihren vorhandenen Datenflüssen zu [!DNL Amazon S3]-, [!DNL Azure Blob]- und SFTP-Zielen jetzt neue Zielverbindungen und Basisverbindungen zugewiesen. Der Schritt zur Profilzuordnung ändert sich ebenfalls. Abwärtsinkompatible Änderungen werden in den folgenden Abschnitten für jedes Ziel zusammengefasst. Weitere Informationen zu den Begriffen [&#x200B; unten stehenden Diagramm &#x200B;](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) Sie auch im Glossar „Ziele“.

![Übersichtsbild zum Migrationshandbuch](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### Abwärtsinkompatible Änderungen am [!DNL Amazon S3] {#changes-amazon-s3-destination}

Die abwärtsinkompatiblen Änderungen für die API-Benutzer sind eine aktualisierte `connection spec ID` und `flow spec ID`, wie in der folgenden Tabelle dargestellt:

| [!DNL Amazon S3] | Veraltet | Neu |
|---------|----------|---------|
| Flussspezifikation | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 1A0514A6-33D4-4C7F-AFF8-594799C47549 |
| Verbindungsspezifikation | 4890FC95-5A1F-4983-94BB-E060C08E3F81 | 4FCE964D-3F37-408F-9778-E597338A21EE |

Sehen Sie sich die vollständigen Beispiele für veraltete und neue Basisverbindungen und Zielverbindungen für [!DNL Amazon S3] in den folgenden Registerkarten an. Die zum Erstellen von Basisverbindungen für [!DNL Amazon S3] Ziele erforderlichen Parameter ändern sich nicht.

Ebenso gibt es keine abwärtsinkompatiblen Änderungen bei den Parametern, die zum Erstellen von Zielverbindungen erforderlich sind.

>[!BEGINTABS]

>[!TAB Veraltete Basisverbindung und Zielverbindung]

+++Alte [!DNL base connection] für [!DNL Amazon S3] anzeigen

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "amazon-s3",
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"640418e2-0000-0200-0000-6359b9ef0000\"",
  "etag": "\"640418e2-0000-0200-0000-6359b9ef0000\""
}
```

+++

+++Alte [!DNL target connection] für [!DNL Amazon S3] anzeigen

```json {line-numbers="true" start-line="1" highlight="12"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "ee86d122-10d3-434b-81c7-7252e4d747a7",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "params": {
    "mode": "S3",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "etag": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "ee86d122-10d3-434b-81c7-7252e4d747a7",
      "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Neue Basisverbindung und Zielverbindung]

+++Anzeigen neuer [!DNL base connection] für [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Amazon S3",
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"3708da21-0000-0200-0000-638940b10000\"",
  "etag": "\"3708da21-0000-0200-0000-638940b10000\""
}
```

+++

+++Anzeigen neuer [!DNL target connection] für [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12, 16-27"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "etag": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
      "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Abwärtsinkompatible Änderungen an [!DNL Azure Blob] Ziel {#changes-azure-blob-destination}

Die abwärtsinkompatiblen Änderungen für die API-Benutzer sind eine aktualisierte `connection spec ID` und `flow spec ID`, wie in der folgenden Tabelle dargestellt:

| [!DNL Azure Blob] | Veraltet | Neu |
|---------|----------|---------|
| Flussspezifikation | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 752d422f-b16f-4f0d-b1c6-26e448e3b388 |
| Verbindungsspezifikation | E258278B-A4CF-43AC-B158-4FA0CA0D948B | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

Sehen Sie sich die vollständigen Beispiele für veraltete und neue Basisverbindungen und Zielverbindungen für [!DNL Azure Blob] in den folgenden Registerkarten an. Die Parameter, die zum Erstellen von Basisverbindungen für Azure Blob-Ziele erforderlich sind, ändern sich nicht.

Ebenso gibt es keine abwärtsinkompatiblen Änderungen bei den Parametern, die zum Erstellen von Zielverbindungen erforderlich sind.

>[!BEGINTABS]

>[!TAB Veraltete Basisverbindung und Zielverbindung]

+++Alte [!DNL base connection] für [!DNL Azure Blob] anzeigen

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "azure-blob",
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  }, 
  "version": "\"d000d23c-0000-0200-0000-6299051c0000\"",
  "etag": "\"d000d23c-0000-0200-0000-6299051c0000\""
}
```

+++

+++Alte [!DNL target connection] für [!DNL Azure Blob] anzeigen

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "d10fcecf-9963-4062-820c-0f878be98805",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "params": {
    "mode": "AZURE_BLOB",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "etag": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d10fcecf-9963-4062-820c-0f878be98805",
      "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Neue Basisverbindung und Zielverbindung]

+++Anzeigen neuer [!DNL base connection] für [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Azure Blob Storage",
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",      
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"4008a892-0000-0200-0000-6389890d0000\"",
  "etag": "\"4008a892-0000-0200-0000-6389890d0000\""
}
```

+++

+++Anzeigen neuer [!DNL target connection] für [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "1329d183-a3ee-4454-ab3f-e2388082bf29",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "etag": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "1329d183-a3ee-4454-ab3f-e2388082bf29",
      "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Abwärtsinkompatible Änderungen am SFTP-Ziel {#changes-sftp-destination}

Die abwärtsinkompatiblen Änderungen für die API-Benutzer sind eine aktualisierte `connection spec ID` und `flow spec ID`, wie in der folgenden Tabelle dargestellt:

| SFTP | Veraltet | Neu |
|---------|----------|---------|
| Flussspezifikation | 71471eba-b620-49e4-90fd-23f1fa0174d8 | fd36aaaa4-bf2b-43fb-9387-43785eeeb799 |
| Verbindungsspezifikation | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965A81-B1C6-401B-99F8-22508F1E6A26 |

Zusätzlich zur aktualisierten Fluss- und Verbindungsspezifikation oben gibt es Änderungen an den Parametern, die beim Erstellen von SFTP-Basisverbindungen erforderlich sind.

* Zuvor erforderte die Basisverbindung für SFTP-Ziele einen `host`. Dieser Parameter wurde jetzt in `domain` umbenannt.

Sehen Sie sich die vollständigen Beispiele für veraltete und neue Basisverbindungen und Zielverbindungen für SFTP auf den unten stehenden Registerkarten an, wobei die sich ändernden Zeilen hervorgehoben sind. Die zum Erstellen von Zielverbindungen für SFTP-Ziele erforderlichen Parameter ändern sich nicht.

>[!BEGINTABS]

>[!TAB Veraltete Basisverbindung und Zielverbindung]

+++Legacy-[!DNL base connection] für SFTP anzeigen - Kennwortauthentifizierung

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "password": "<your-password>",
      "userName": "DPID12345",
      "host": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Alte [!DNL base connection] für [!DNL SFTP - SSH key] Authentifizierung anzeigen

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "sshKey": "<your-ssh-key>",
      "userName": "DPID12345",
      "port": 22
      "domain": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Alte [!DNL target connection] für SFTP anzeigen

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "params": {
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "etag": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
      "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Neue Basisverbindung und Zielverbindung]

+++Anzeigen neuer [!DNL base connection] für [!DNL SFTP - password authentication]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "password": "<your-password>",
      "port": 22      
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Anzeigen neuer [!DNL base connection] für die [!DNL SFTP - SSH key] Authentifizierung

```json {line-numbers="true" start-line="1" highlight="5,12"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "sshKey": "<your-ssh-key>",
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Anzeigen neuer [!DNL target connection] für SFTP

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "etag": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
      "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Abwärtskompatible Änderungen, die für [!DNL Amazon S3]-, [!DNL Azure Blob]- und SFTP-Ziele üblich sind {#changes-all-destinations}

Der Profilauswahlschritt in allen drei Zielen wird durch einen Zuordnungsschritt ersetzt, mit dem Sie die Spaltenüberschriften in Ihren exportierten Dateien bei Bedarf umbenennen können. Siehe die Abbildung unten nebeneinander mit dem alten Attributauswahlschritt auf der linken Seite und dem neuen Zuordnungsschritt auf der rechten Seite.

![Übersichtsbild zum Migrationshandbuch](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

Beachten Sie, wie das `profileSelectors` in den Legacy-Beispielen durch das neue `profileMapping` ersetzt wird.

Vollständige Informationen zum Einrichten des `profileMapping` finden Sie im [API-Tutorial zum Exportieren von Daten in Cloud-Speicher-Ziele](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB Alte Umwandlungsparameter]

+++Sehen Sie sich ein Beispiel für alte Umwandlungsparameter an.

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the audience selectors
  },  
  "profileSelectors": {
    "selectors": [
      {
        "type": "JSON_PATH",
        "value": {
          "path": "CORE",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "CORE",
            "destination": "CORE",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "CORE",
            "destinationXdmPath": "CORE"
          },
          "identity": {
            "namespace": "CORE"
          }
        }
      },
      ...
      {
        "type": "JSON_PATH",
        "value": {
          "path": "segmentMembership.status",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "segmentMembership.status",
            "destination": "segmentMembership.status",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "segmentMembership.status",
            "destinationXdmPath": "segmentMembership.status"
          }
        }
      }
    ],
    "mandatoryFields": [
      "CORE",
      "person.name.lastName",
      "personalEmail.address"
    ],
    "primaryFields": [
      {
        "identityNamespace": "CORE",
        "fieldType": "IDENTITY"
      }
    ]
  }
}
```

+++

>[!TAB Neue Umwandlungsparameter]

+++Sehen Sie sich ein Beispiel für Umwandlungsparameter nach der Migration an.

Beachten Sie im folgenden Konfigurationsbeispiel, wie `profileSelectors` Felder durch ein `profileMapping` ersetzt wurden.

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the audience selectors
  },  
  "mandatoryFields": [
    "CORE",
    "person_name_lastName",
    "personalEmail_address"
  ],
  "primaryFields": [
    {
      "identityNamespace": "CORE",
      "fieldType": "IDENTITY"
    }
  ],
  "identityMapping": {
    "mappings": []
  },
  "profileMapping": {
    "mappingId": "40dfd952fe09498ba65145c7a5de3e07",
    "mappingVersion": 0
  },
  "attributeMapping": {}
}
```

+++

>[!ENDTABS]

## Zeitplan und Aktionselemente für die Migration {#timeline-and-action-items}

Die Migration älterer Datenflüsse zu den neuen Zielkarten für [!DNL Amazon S3]-, [!DNL Azure Blob]- und SFTP-Ziele erfolgt, sobald Ihre Organisation für die Migration bereit ist, spätestens jedoch **26. Juli**.

Wenn das Migrationsdatum näher rückt, erhalten Sie eine Erinnerungs-E-Mail von Adobe. Zur Vorbereitung lesen Sie den Abschnitt Aktionselemente unten, um sich für die Migration vorzubereiten.

### Aktionselemente {#action-items}

Bereiten Sie sich zur Vorbereitung der Migration der [!DNL Amazon S3]-, [!DNL Azure Blob]- und SFTP-Cloud-Speicher-Ziele auf die neuen Karten bitte darauf vor, Ihre Skripte und automatisierten API-Aufrufe wie unten vorgeschlagen zu aktualisieren.

1. Aktualisieren Sie alle Skripte oder automatisierten API-Aufrufe für vorhandene [!DNL Amazon S3]-, [!DNL Azure Blob]- oder SFTP-Cloud-Speicher-Ziele bis zum 26. Juli 2023. Alle automatisierten API-Aufrufe oder -Skripte, die die veralteten Verbindungsspezifikationen oder Flussspezifikationen nutzen, müssen auf die neuen Verbindungsspezifikationen oder Flussspezifikationen aktualisiert werden.
2. Wenden Sie sich an Ihren Adobe-Kundenbetreuer, wenn Ihre Scripts vor dem 26. Juli aktualisiert wurden.
3. Beispielsweise kann die `targetConnectionSpecId` als Flag verwendet werden, um festzustellen, ob der Datenfluss zur neuen Zielkarte migriert wurde. Sie können Ihre Skripte mit einer `if` aktualisieren, um die veralteten und aktualisierten Zielverbindungsspezifikationen in `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` zu überprüfen und festzustellen, ob Ihr Datenfluss migriert wurde. Die IDs der veralteten und neuen Verbindungsspezifikationen werden für jedes Ziel in den jeweiligen Abschnitten auf dieser Seite angezeigt.
4. Ihr Adobe-Account-Team wird sich mit weiteren Informationen darüber in Verbindung setzen, wann Ihre Datenflüsse migriert werden.
5. Nach dem 26. Juli werden alle Datenflüsse migriert. Alle vorhandenen Datenflüsse verfügen jetzt über neue Fluss-Entitäten (Verbindungsspezifikationen, Flussspezifikationen, Basisverbindungen und Zielverbindungen). Alle Skripte oder API-Aufrufe auf Ihrer Seite, die die veralteten Fluss-Entitäten verwenden, funktionieren nicht mehr.

## Weitere Überlegungen zur Migration {#other-considerations}

Beachten Sie, dass es während oder nach der Migration keine Auswirkungen auf Ihren bestehenden Zeitplan für Exporte gibt.

## Nächste Schritte {#next-steps}

Durch das Lesen dieser Seite wissen Sie jetzt, ob Sie Maßnahmen zur Vorbereitung auf die Migration der Cloud-Speicher-Ziele ergreifen müssen. Sie wissen auch, auf welche Dokumentationsseiten verwiesen werden soll, wenn Sie API-basierte Workflows einrichten, um Dateien aus dem Experience Platform in Ihre bevorzugten Cloud-Speicher-Ziele zu exportieren. Als Nächstes können Sie sich das API-Tutorial ansehen, um [Daten in Cloud-Speicher-Ziele zu exportieren](/help/destinations/api/activate-segments-file-based-destinations.md).
