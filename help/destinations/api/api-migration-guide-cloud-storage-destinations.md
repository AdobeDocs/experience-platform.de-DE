---
solution: Experience Platform
title: API-Migrationshandbuch für Cloud-Speicher-Ziele
description: Erfahren Sie mehr über die Änderungen im Workflow zur Aktivierung von Cloud-Speicher-Zielen im Rahmen der Migration zu den neuen Cloud-Speicher-Zielkarten mit zusätzlichen Funktionen.
type: Tutorial
source-git-commit: 6ed78a96f099fb4552716ac4a598c43f4d65cf37
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 3%

---

# API-Migrationshandbuch für Cloud-Speicher-Ziele

>[!IMPORTANT]
>
>* Die auf dieser Seite beschriebene Funktion steht Kunden zur Verfügung, die die Real-Time CDP Prime- und Ultimate-Pakete erworben haben. Bitte wenden Sie sich an den Adobe-Support-Mitarbeiter, um weitere Informationen zu erhalten.


## Migrationskontext {#migration-context}

Start [Oktober 2022](/help/release-notes/2022/october-2022.md#new-or-updated-destinations)können Sie die neuen Dateiexportfunktionen verwenden, um auf erweiterte Anpassungsfunktionen beim Exportieren von Dateien aus der Experience Platform zuzugreifen:

* Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* Möglichkeit, benutzerdefinierte Dateikopfzeilen in Ihren exportierten Dateien über die [neuer Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* Möglichkeit zur Auswahl der [Dateityp](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) der exportierten Datei.
* Fähigkeit [Formatierung exportierter CSV-Datendateien anpassen](/help/destinations/ui/batch-destinations-file-formatting-options.md).

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

Beachten Sie, dass Sie in der Experience Platform-Benutzeroberfläche derzeit zwei nebeneinander liegende Zielkarten der drei Ziele sehen können. Nachfolgend finden Sie die [!DNL Amazon S3] alte und neue Ziele. In jedem Fall werden die mit **Beta** sind die neuen Zielkarten.

![Abbildung der beiden Amazon S3-Zielkarten, die diese nebeneinander in einer Ansicht zeigt.](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Während diese Ziele mit verbesserter Funktionalität zunächst als Beta-Version angeboten wurden, *Adobe verschiebt jetzt alle Real-Time CDP-Kunden zu den neuen Cloud-Speicher-Zielen*. Für Kunden, die bereits [!DNL Amazon S3], [!DNL Azure Blob], oder SFTP, bedeutet dies, dass vorhandene Datenflüsse auf die neuen Karten migriert werden. Weitere Informationen zu den spezifischen Änderungen im Rahmen der Migration finden Sie im Abschnitt .

## Wer für diese Seite gilt {#who-this-applies-to}

Wenn Sie bereits die [Flussdienst-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) Um Profile in die Amazon S3-, Azure Blob- oder SFTP-Cloud-Speicher-Ziele zu exportieren, gilt dieses API-Migrationshandbuch für Sie.

Wenn Skripte in Ihrer [!DNL Amazon S3], [!DNL Azure Blob]- oder SFTP-Cloud-Speicher auf den exportierten Dateien aus Experience Platform - beachten Sie, dass sich einige Parameter in Bezug auf die Verbindungs- und Flussspezifikationen der neuen Karten sowie in Bezug auf den Zuordnungsschritt ändern.

Wenn Sie beispielsweise ein Skript zum Filtern von Ziel-Datenflüssen zum [!DNL Amazon S3] Ziel, basierend auf der Verbindungsspezifikation des [!DNL Amazon S3] Ziel, beachten Sie, dass sich die Verbindungsspezifikation ändert, sodass Sie Ihre Filter aktualisieren müssen.

## Relevante Dokumentationslinks {#relevant-documentation-links}

Dieser Abschnitt enthält das relevante API-Tutorial und die Referenzdokumentation für die erweiterte Funktion zum Exportieren von Daten in Cloud-Speicher-Ziele.

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [API-Tutorial zum Exportieren von Segmenten in Cloud-Speicher-Ziele](/help/destinations/api/activate-segments-file-based-destinations.md)
* [Referenzdokumentation zur Ziel Flow Service-API](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## Zusammenfassung abwärtsinkompatibler Änderungen {#summary-backwards-incompatible-changes}

Mit der Migration zu den neuen Zielen werden alle vorhandenen Datenflüsse zu [!DNL Amazon S3], [!DNL Azure Blob]und SFTP-Zielen werden nun neue Zielverbindungen und Basisverbindungen zugewiesen. Der Schritt zur Profilzuordnung ändert sich ebenfalls. Abwärtskompatible Änderungen werden in den folgenden Abschnitten für jedes Ziel zusammengefasst. Zeigen Sie auch die [Zielglossar](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) für weitere Informationen zu den Begriffen in der unten stehenden Abbildung.

![Übersichtsbild des Migrationshandbuchs](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### Abwärtskompatible Änderungen an der [!DNL Amazon S3] Ziel {#changes-amazon-s3-destination}

Die rückwärtsinkompatiblen Änderungen für die API-Benutzer sind eine aktualisierte `connection spec ID` und `flow spec ID` wie in der folgenden Tabelle dargestellt:

| [!DNL Amazon S3] | Veraltet | Neu |
|---------|----------|---------|
| Flussspezifikation | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Verbindungsspezifikation | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

Sehen Sie sich die vollständige alte und die neue Basisverbindung sowie Beispiele für Zielverbindungen an für [!DNL Amazon S3] in den Registerkarten unten. Die erforderlichen Parameter zum Erstellen von Basisverbindungen für [!DNL Amazon S3] -Ziele ändern sich nicht.

Ebenso gibt es keine rückwärtskompatiblen Änderungen an den Parametern, die zum Erstellen von Zielverbindungen erforderlich sind.

>[!BEGINTABS]

>[!TAB Alte Basisverbindung und Zielverbindung]

+++Legacy anzeigen [!DNL base connection] für [!DNL Amazon S3]

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

+++Legacy anzeigen [!DNL target connection] für [!DNL Amazon S3]

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

+++Neu anzeigen [!DNL base connection] für [!DNL Amazon S3]

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

+++Neu anzeigen [!DNL target connection] für [!DNL Amazon S3]

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

### Abwärtskompatible Änderungen an [!DNL Azure Blob] Ziel {#changes-azure-blob-destination}

Die rückwärtsinkompatiblen Änderungen für die API-Benutzer sind eine aktualisierte `connection spec ID` und `flow spec ID` wie in der folgenden Tabelle dargestellt:

| [!DNL Azure Blob] | Veraltet | Neu |
|---------|----------|---------|
| Flussspezifikation | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Verbindungsspezifikation | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

Sehen Sie sich die vollständige alte und die neue Basisverbindung sowie Beispiele für Zielverbindungen an für [!DNL Azure Blob] in den Registerkarten unten. Die Parameter, die zum Erstellen von Basisverbindungen für Azure Blob-Ziele erforderlich sind, ändern sich nicht.

Ebenso gibt es keine rückwärtskompatiblen Änderungen an den Parametern, die zum Erstellen von Zielverbindungen erforderlich sind.

>[!BEGINTABS]

>[!TAB Alte Basisverbindung und Zielverbindung]

+++Legacy anzeigen [!DNL base connection] für [!DNL Azure Blob]

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

+++Legacy anzeigen [!DNL target connection] für [!DNL Azure Blob]

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

+++Neu anzeigen [!DNL base connection] für [!DNL Azure Blob]

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

+++Neu anzeigen [!DNL target connection] für [!DNL Azure Blob]

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

### Abwärtskompatible Änderungen am SFTP-Ziel {#changes-sftp-destination}

Die rückwärtsinkompatiblen Änderungen für die API-Benutzer sind eine aktualisierte `connection spec ID` und `flow spec ID` wie in der folgenden Tabelle dargestellt:

| SFTP | Veraltet | Neu |
|---------|----------|---------|
| Flussspezifikation | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 354d6aad-4754-46e4-a576-1b384561c440 |
| Verbindungsspezifikation | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

Neben der oben aktualisierten Fluss- und Verbindungsspezifikation gibt es Änderungen an den Parametern, die beim Erstellen von SFTP-Basisverbindungen erforderlich sind.

* Zuvor war für die Basisverbindung für SFTP-Ziele ein `host` Parameter. Dieser Parameter wurde jetzt in `domain`.
* Für die Authentifizierung mit der SSH-Schlüsseloption benötigten die Authentifizierungsparameter in der Basisverbindung eine `port` -Option. Dieser Parameter ist jetzt veraltet und nicht mehr erforderlich.

Sehen Sie sich die vollständige alte und die neue Basisverbindung sowie die Beispiele für Zielverbindungen für SFTP auf den Registerkarten unten an, wobei die Zeilen, die sich ändern, hervorgehoben werden. Die Parameter, die zum Erstellen von Zielverbindungen für SFTP-Ziele erforderlich sind, ändern sich nicht.

>[!BEGINTABS]

>[!TAB Alte Basisverbindung und Zielverbindung]

+++Legacy anzeigen [!DNL base connection] für SFTP - Kennwortauthentifizierung

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

+++Legacy anzeigen [!DNL base connection] für [!DNL SFTP - SSH key] Authentifizierung

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

+++Legacy anzeigen [!DNL target connection] für SFTP

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

+++Neu anzeigen [!DNL base connection] für [!DNL SFTP - password authentication]

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
      "password": "<your-password>"
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

+++Neu anzeigen [!DNL base connection] für [!DNL SFTP - SSH key] Authentifizierung

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

+++Neu anzeigen [!DNL target connection] für SFTP

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

### Abwärtskompatible Änderungen, die [!DNL Amazon S3], [!DNL Azure Blob], und SFTP-Ziele {#changes-all-destinations}

Der Schritt zur Profilauswahl in allen drei Zielen wird durch einen Zuordnungsschritt ersetzt, mit dem Sie die Spaltenüberschriften in Ihren exportierten Dateien ggf. umbenennen können. Sehen Sie sich unten das Bild nebeneinander mit dem alten Schritt zur Attributauswahl auf der linken Seite und dem neuen Schritt zur Zuordnung auf der rechten Seite an.

![Übersichtsbild des Migrationshandbuchs](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

Beachten Sie, wie die `profileSelectors` -Objekt in den veralteten Beispielen wird durch die neue `profileMapping` -Objekt.

Vollständige Informationen zum Einrichten der `profileMapping` -Objekt im [API-Tutorial zum Exportieren von Daten in Cloud-Speicher-Ziele](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB Alte Transformationsparameter]

+++Beispiel für alte Transformationsparameter anzeigen

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
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

>[!TAB Neue Transformationsparameter]

+++Beispiel für Umwandlungsparameter nach der Migration anzeigen

Beachten Sie im folgenden Konfigurationsbeispiel wie `profileSelectors` -Felder wurden durch eine `profileMapping` -Objekt.

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
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

## Migrationszeitleiste und Aktionselemente {#timeline-and-action-items}

Die Migration von alten Datenflüssen zu den neuen Zielkarten für [!DNL Amazon S3], [!DNL Azure Blob]und SFTP-Ziele eintreten, sobald Ihr Unternehmen für die Migration bereit ist, spätestens jedoch **30. Juni 2023**.

Sie erhalten Erinnerungsnachrichten von Adobe, wenn das Migrationsdatum näher rückt. Lesen Sie in der Vorbereitung den Abschnitt Aktionselemente unten, um sich für die Migration vorzubereiten.

### Aktionselemente {#action-items}

Zur Vorbereitung der Migration der [!DNL Amazon S3], [!DNL Azure Blob]und SFTP-Cloud-Speicher-Ziele auf den neuen Karten verwenden, bereiten Sie sich auf die Aktualisierung Ihrer Skripte und automatisierten API-Aufrufe vor, wie unten vorgeschlagen.

1. Aktualisieren von Skripten oder automatisierten API-Aufrufen für vorhandene [!DNL Amazon S3], [!DNL Azure Blob], oder bis zum 30. Juni 2023 SFTP-Cloud-Speicher-Ziele. Alle automatisierten API-Aufrufe oder Skripte, die die veralteten Verbindungs- oder Flussspezifikationen nutzen, müssen auf die neuen Verbindungs- oder Flussspezifikationen aktualisiert werden.
2. Wenden Sie sich an Ihren Adobe-Kundenbetreuer, wenn Ihre Skripte vor dem 30. Juni aktualisiert wurden.
3. Beispiel: die `targetConnectionSpecId` kann als Flag verwendet werden, um zu bestimmen, ob der Datenfluss auf die neue Zielkarte migriert wurde. Sie können Ihre Skripte mit einer `if` -Bedingung, um sich die veralteten und aktualisierten Zielverbindungsspezifikationen in `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` und bestimmen, ob Ihr Datenfluss migriert wurde. Sie können die alten und neuen Verbindungsspezifikations-IDs in den spezifischen Abschnitten auf dieser Seite für jedes Ziel sehen.
4. Ihr Adobe-Kontoteam wird sich mit weiteren Informationen darüber in Verbindung setzen, wann Ihre Datenflüsse migriert werden.
5. Nach dem 30. Juni werden alle Datenflüsse migriert. Alle vorhandenen Datenflüsse verfügen jetzt über neue Flussentitäten (Verbindungs-, Fluss-, Basis- und Zielverbindungen). Skripte oder API-Aufrufe auf Ihrer Seite, die die Legacy-Fluss-Entitäten verwenden, funktionieren nicht mehr.

## Andere Migrationsaspekte {#other-considerations}

Beachten Sie, dass sich der vorhandene Zeitplan für Exporte während oder nach der Migration nicht auf ihn auswirkt.

## Nächste Schritte {#next-steps}

Durch Lesen dieser Seite wissen Sie jetzt, ob Sie Maßnahmen zur Vorbereitung der Migration der Cloud-Speicher-Ziele ergreifen müssen. Sie wissen auch, auf welche Dokumentationsseiten Sie bei der Einrichtung von API-basierten Workflows verweisen müssen, um Dateien aus der Experience Platform in Ihre bevorzugten Cloud-Speicher-Ziele zu exportieren. Als Nächstes können Sie das API-Tutorial zu [Exportieren von Daten in Cloud-Speicher-Ziele](/help/destinations/api/activate-segments-file-based-destinations.md).