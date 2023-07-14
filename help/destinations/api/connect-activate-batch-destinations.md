---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Verbinden mit Batch-Zielen und Aktivieren von Daten mit der Flow Service-API
description: Schrittweise Anleitungen zur Verwendung der Flow Service-API zum Erstellen eines Batch-Cloud-Speichers oder E-Mail-Marketing-Ziels in Experience Platform und zum Aktivieren von Daten
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '3399'
ht-degree: 80%

---

# Verbinden mit Batch-Zielen und Aktivieren von Daten mit der Flow Service-API

>[!IMPORTANT]
> 
>Um eine Verbindung mit einem Ziel herzustellen, benötigen Sie die **[!UICONTROL Zugriffssteuerungsberechtigung]** [Ziele verwalten](/help/access-control/home.md#permissions).
>
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Zugriffskontrollberechtigungen]** **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und [Segmente anzeigen](/help/access-control/home.md#permissions).
>
>Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

In diesem Tutorial erfahren Sie, wie Sie die Flow Service-API verwenden, um per Batch ein [Cloud-Speicher-Ziel](../catalog/cloud-storage/overview.md) oder ein [E-Mail-Marketing-Ziel](../catalog/email-marketing/overview.md) zu erstellen, einen Datenfluss zu Ihrem neu erstellten Ziel zu erstellen und Daten über CSV-Dateien zu Ihrem neu erstellten Ziel zu exportieren.

In diesem Tutorial wird für alle Beispiele das Ziel [!DNL Adobe Campaign] verwendet, die Schritte sind aber für alle Batch-Cloud-Speicher-Ziele und E-Mail-Marketing-Ziele identisch.

![Übersicht - Schritte zum Erstellen eines Ziels und Aktivieren von Zielgruppen](../assets/api/email-marketing/overview.png)

Wenn Sie die Platform-Benutzeroberfläche bevorzugen, um eine Verbindung zu einem Ziel herzustellen und Daten zu aktivieren, finden Sie weitere Informationen in den Tutorials [Verbinden eines Ziels](../ui/connect-destination.md) und [Aktivieren von Zielgruppendaten für Batch-Profilexportziele](../ui/activate-batch-profile-destinations.md).

## Erste Schritte {#get-started}

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md): [!DNL Adobe Experience Platform Segmentation Service] ermöglicht Ihnen das Erstellen von Zielgruppen in [!DNL Adobe Experience Platform] von [!DNL Real-Time Customer Profile] Daten.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen sollten, um Daten für Batch-Ziele in Platform zu aktivieren.

### Sammeln erforderlicher Anmeldeinformationen {#gather-required-credentials}

Um die Schritte in diesem Tutorial abzuschließen, sollten Sie die folgenden Anmeldeinformationen haben, je nach Zieltyp, mit dem Sie Zielgruppen verbinden und aktivieren.

* Für [!DNL Amazon S3]-Verbindungen: `accessId`, `secretKey`
* Für [!DNL Amazon S3]-Verbindungen zu [!DNL Adobe Campaign]: `accessId`, `secretKey`
* Für SFTP-Verbindungen: `domain`, `port`, `username`, `password` oder `sshKey` (abhängig von der Verbindungsmethode zum FTP-Speicherort)
* Für [!DNL Azure Blob]-Verbindungen: `connectionString`

>[!NOTE]
>
>Die Anmeldeinformationen `accessId`, `secretKey` für [!DNL Amazon S3]-Verbindungen und `accessId`, `secretKey` für [!DNL Amazon S3]-Verbindungen zu [!DNL Adobe Campaign] sind identisch.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln der Werte für erforderliche und optionale Kopfzeilen {#gather-values-headers}

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Ressourcen in [!DNL Experience Platform] lassen sich in spezifischen virtuellen Sandboxes isolieren. Bei Anfragen an [!DNL Platform]-APIs können Sie den Namen und die ID der Sandbox angeben, in der der Vorgang ausgeführt werden soll. Dies sind optionale Parameter.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

### API-Referenzdokumentation {#api-reference-documentation}

Eine zugehörige Referenzdokumentation für alle API-Vorgänge finden Sie in diesem Tutorial. Weitere Informationen finden Sie in der [Flow Service-API-Dokumentation zu Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). Wir empfehlen, dass Sie dieses Tutorial und die API-Referenzdokumentation parallel verwenden.

## Abrufen der Liste der verfügbaren Ziele {#get-the-list-of-available-destinations}

![Übersicht über die Zielschritte – Schritt 1](../assets/api/batch-destination/step1.png)

Als ersten Schritt sollten Sie entscheiden, für welches Ziel Daten aktiviert werden sollen. Führen Sie zunächst einen Aufruf durch, um eine Liste der verfügbaren Ziele anzufordern, mit denen Sie eine Verbindung herstellen und Zielgruppen aktivieren können. Führen Sie die folgende GET-Anfrage an den `connectionSpecs`-Endpunkt aus, um eine Liste der verfügbaren Ziele zu erhalten:

**API-Format**

```http
GET /connectionSpecs
```

**Anfrage**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Antwort**

Eine erfolgreiche Antwort enthält eine Liste der verfügbaren Ziele und ihre eindeutigen Kennungen (`id`). Notieren Sie sich den Wert des Ziels, das Sie verwenden möchten, da Sie ihn in weiteren Schritten benötigen werden. Wenn Sie beispielsweise Zielgruppen verbinden und bereitstellen möchten, um [!DNL Adobe Campaign], suchen Sie in der Antwort nach dem folgenden Snippet:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

Die nachstehende Tabelle enthält die Verbindungsspezifikations-IDs für häufig verwendete Batch-Ziele:

| Ziel | Verbindungsspezifikations-ID |
---------|----------|
| [!DNL Adobe Campaign] | `0b23e41a-cb4a-4321-a78f-3b654f5d7d97` |
| [!DNL Amazon S3] | `4890fc95-5a1f-4983-94bb-e060c08e3f81` |
| [!DNL Azure Blob] | `e258278b-a4cf-43ac-b158-4fa0ca0d948b` |
| [!DNL Oracle Eloqua] | `c1e44b6b-e7c8-404b-9031-58f0ef760604` |
| [!DNL Oracle Responsys] | `a5e28ddf-e265-426e-83a1-9d03a3a6822b` |
| [!DNL Salesforce Marketing Cloud] | `f599a5b3-60a7-4951-950a-cc4115c7ea27` |
| SFTP | `64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0` |

{style="table-layout:auto"}

## Verbinden mit Ihren [!DNL Experience Platform]-Daten {#connect-to-your-experience-platform-data}

![Übersicht über die Zielschritte – Schritt 2](../assets/api/batch-destination/step2.png)

Als Nächstes müssen Sie eine Verbindung zu Ihren [!DNL Experience Platform]-Daten herstellen, um Profildaten exportieren und in Ihrem bevorzugten Ziel aktivieren zu können. Dies umfasst zwei Unterschritte, die nachfolgend beschrieben werden.

1. Sie müssen zunächst einen Aufruf ausführen, um den Zugriff auf Ihre Daten in [!DNL Experience Platform] zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Führen Sie dann unter Verwendung der Basisverbindungs-ID einen weiteren Aufruf durch, in dem Sie eine *Quellverbindung* erstellen, die die Verbindung zu Ihren [!DNL Experience Platform]-Daten herstellt.

### Autorisieren des Zugriffs auf Ihre Daten in [!DNL Experience Platform]

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `name` | Geben Sie einen Namen für die Basisverbindung zum [!DNL Profile Store] von Experience Platform an. |
| `description` | Optional können Sie eine Beschreibung für die Basisverbindung angeben. |
| `connectionSpec.id` | Verwenden Sie die Verbindungsspezifikations-ID für den [Profile Store von Experience Platform](/help/profile/home.md#profile-data-store) – `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Notieren Sie sich diesen Wert, da Sie ihn im nächsten Schritt zum Erstellen der Quellverbindung benötigen werden.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Verbinden mit Ihren [!DNL Experience Platform]-Daten {#connect-to-platform-data}

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile Store",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `name` | Geben Sie einen Namen für die Quellverbindung zum [!DNL Profile Store] von Experience Platform an. |
| `description` | Optional können Sie eine Beschreibung für die Quellverbindung angeben. |
| `connectionSpec.id` | Verwenden Sie die Verbindungsspezifikations-ID für den [Profile Store von Experience Platform](/help/profile/home.md#profile-data-store) – `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |
| `baseConnectionId` | Verwenden Sie die Basisverbindungs-ID, die Sie im vorherigen Schritt erhalten haben. |
| `data.format` | `CSV` ist derzeit das einzige unterstützte Dateiexportformat. |

{style="table-layout:auto"}

**Antwort**

Bei einer erfolgreichen Antwort wird der eindeutige Bezeichner (`id`) für die neu erstellte Quellverbindung zum [!DNL Profile Store] zurückgegeben. Dadurch wird bestätigt, dass Sie erfolgreich eine Verbindung zu Ihren [!DNL Experience Platform]-Daten hergestellt haben. Notieren Sie sich diesen Wert, da Sie ihn in einem späteren Schritt benötigen werden.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```

## Herstellen einer Verbindung zum Batch-Ziel {#connect-to-batch-destination}

![Übersicht über die Zielschritte – Schritt 3](../assets/api/batch-destination/step3.png)

In diesem Schritt richten Sie eine Verbindung zu Ihrem gewünschten Batch-Cloud-Speicher- oder E-Mail-Marketing-Ziel ein. Dies umfasst zwei Unterschritte, die nachfolgend beschrieben werden.

1. Sie müssen zunächst einen Aufruf ausführen, um den Zugriff auf die Zielplattform zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Mithilfe der Kennung der Basisverbindung führen Sie dann einen weiteren Aufruf aus, mit dem Sie eine *Zielverbindung erstellen*. In dem Aufruf sind der Ort in Ihrem Speicherkonto, an dem die exportierten Datendateien bereitgestellt werden, sowie das Format der zu exportierenden Daten angegeben.

### Autorisieren des Zugriffs auf das Batch-Ziel {#authorize-access-to-batch-destination}

**API-Format**

```http
POST /connections
```

**Anfrage**

Die nachstehende Anfrage stellt eine Basisverbindung zu [!DNL Adobe Campaign]-Zielen her. Behalten Sie je nach Speicherort, an den Sie die Dateien exportieren möchten ([!DNL Amazon S3], SFTP, [!DNL Azure Blob]), die entsprechende `auth`-Spezifikation bei und löschen Sie die anderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "auth": {
        "specName": "S3",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }        
    "auth": {
        "specName": "Azure Blob",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }    
}'
```

Siehe die folgenden Beispielanfragen zum Herstellen einer Verbindung zu anderen unterstützten Batch-Cloud-Speicher- und E-Mail-Marketing-Zielen.

+++ Beispielanfrage zum Herstellen einer Verbindung zu [!DNL Amazon S3]-Zielen

Die nachstehende Anfrage stellt eine Basisverbindung zu [!DNL Amazon S3]-Zielen her.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Amazon S3",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "auth": {
        "specName": "Access Key",
        "params": {
            "s3AccessKey": "{AMAZON_S3_ACCESS_KEY}",
            "s3SecretKey": "{AMAZON_S3_SECRET_KEY}"
        }
    }
}'
```

+++

+++ Beispielanfrage zum Herstellen einer Verbindung zu [!DNL Azure Blob]-Zielen

Die nachstehende Anfrage stellt eine Basisverbindung zu [!DNL Azure Blob]-Zielen her.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Azure Blob",
    "description": "Summer advertising campaign",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "auth": {
        "specName": "ConnectionString",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }
}'
```

+++

+++ Beispielanfrage zum Herstellen einer Verbindung zu [!DNL Oracle Eloqua]-Zielen

Die nachstehende Anfrage stellt eine Basisverbindung zu [!DNL Oracle Eloqua]-Zielen her. Behalten Sie je nach Speicherort, an den Sie die Dateien exportieren möchten, die entsprechende `auth`-Spezifikation bei und löschen Sie die anderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Eloqua destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Beispielanfrage zum Herstellen einer Verbindung zu [!DNL Oracle Responsys]-Zielen

Die nachstehende Anfrage stellt eine Basisverbindung zu [!DNL Oracle Responsys]-Zielen her. Behalten Sie je nach Speicherort, an den Sie die Dateien exportieren möchten, die entsprechende `auth`-Spezifikation bei und löschen Sie die anderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Responsys destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Beispielanfrage zum Herstellen einer Verbindung zu [!DNL Salesforce Marketing Cloud]-Zielen

Die nachstehende Anfrage stellt eine Basisverbindung zu [!DNL Salesforce Marketing Cloud]-Zielen her. Behalten Sie je nach Speicherort, an den Sie die Dateien exportieren möchten, die entsprechende `auth`-Spezifikation bei und löschen Sie die anderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Salesforce Marketing Cloud",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Beispielanfrage für die Verbindung mit SFTP mit Passwortzielen

Die nachstehende Anfrage stellt eine Basisverbindung zu SFTP-Zielen her.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to SFTP with password",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
}'
```

+++

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `name` | Geben Sie einen Namen für die Basisverbindung zum Batch-Ziel an. |
| `description` | Optional können Sie eine Beschreibung für die Basisverbindung angeben. |
| `connectionSpec.id` | Verwenden Sie die Verbindungsspezifikations-ID für Ihr gewünschtes Batch-Ziel. Sie haben diese ID im Schritt [Abrufen der Liste der verfügbaren Ziele](#get-the-list-of-available-destinations) erhalten. |
| `auth.specname` | Gibt das Authentifizierungsformat für das Ziel an. Um den specName für Ihr Ziel zu ermitteln, führen Sie einen [GET-Aufruf an den Verbindungsspezifikationen-Endpunkt](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec) durch, wobei Sie die Verbindungsspezifikation Ihres gewünschten Ziels angeben. Suchen Sie in der Antwort nach dem Parameter `authSpec.name`. <br> Bei Adobe Campaign-Zielen können Sie beispielsweise eine der folgenden Optionen verwenden: `S3`, `SFTP with Password` oder `SFTP with SSH Key`. |
| `params` | Je nach Ziel, mit dem Sie eine Verbindung herstellen, müssen Sie unterschiedliche erforderliche Authentifizierungsparameter angeben. Bei Verbindungen des Typs Amazon S3 müssen Sie Ihre Zugriffs-ID und den geheimen Schlüssel für Ihren Speicherort im Amazon S3-Speicher angeben. <br> Um die erforderlichen Parameter für Ihr Ziel zu ermitteln, führen Sie einen [GET-Aufruf an den Verbindungsspezifikationen-Endpunkt](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec) durch, wobei Sie die Verbindungsspezifikation Ihres gewünschten Ziels angeben. Suchen Sie in der Antwort nach dem Parameter `authSpec.spec.required`. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Notieren Sie sich diesen Wert, da Sie ihn im nächsten Schritt benötigen, um eine Zielverbindung zu erstellen.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Speicherort und Datenformat angeben {#specify-storage-location-data-format}

[!DNL Adobe Experience Platform] exportiert Daten für Batch-E-Mail-Marketing- und Cloud-Speicher-Ziele in Form von [!DNL CSV]-Dateien. In diesem Schritt können Sie den Pfad in Ihrem Speicherort ermitteln, an dem die Dateien exportiert werden.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] teilt die Exportdateien automatisch mit 5 Millionen Datensätzen (Zeilen) pro Datei auf. Jede Zeile stellt ein Profil dar.
>
>Bei aufgeteilten Dateien wird eine Nummer an den Namen angehängt, die anzeigt, dass die Datei Teil eines größeren Exports ist, z. B. `filename.csv`, `filename_2.csv`, `filename_3.csv`.

**API-Format**

```http
POST /targetConnections
```

**Anfrage**

Die nachstehende Anfrage stellt eine Zielverbindung zu [!DNL Adobe Campaign]-Zielen her, um zu bestimmen, wo die exportierten Dateien an Ihrem Speicherort abgelegt werden sollen. Behalten Sie je nach Speicherort, an den Sie die Dateien exportieren möchten, die entsprechende `params`-Spezifikation bei und löschen Sie die anderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

Siehe die folgenden Beispielanfragen zum Einrichten eines Speicherorts für andere unterstützte Batch-Cloud-Speicher- und E-Mail-Marketing-Ziele.

+++ Beispielanfrage zum Einrichten eines Speicherorts für [!DNL Amazon S3]-Ziele

Die nachstehende Anfrage stellt eine Zielverbindung zu [!DNL Amazon S3]-Zielen her, um zu bestimmen, wo die exportierten Dateien an Ihrem Speicherort abgelegt werden sollen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Amazon S3",
    "description": "Connection to Amazon S3",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ Beispielanfrage zum Einrichten eines Speicherorts für [!DNL Azure Blob]-Ziele

Die nachstehende Anfrage stellt eine Zielverbindung zu [!DNL Azure Blob]-Zielen her, um zu bestimmen, wo die exportierten Dateien an Ihrem Speicherort abgelegt werden sollen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Azure Blob",
    "description": "Connection to Azure Blob",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ Beispielanfrage zum Einrichten eines Speicherorts für [!DNL Oracle Eloqua]-Ziele

Die nachstehende Anfrage stellt eine Zielverbindung zu [!DNL Oracle Eloqua]-Zielen her, um zu bestimmen, wo die exportierten Dateien an Ihrem Speicherort abgelegt werden sollen. Behalten Sie je nach Speicherort, an den Sie die Dateien exportieren möchten, die entsprechende `params`-Spezifikation bei und löschen Sie die anderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Eloqua",
    "description": "Connection to Oracle Eloqua",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ Beispielanfrage zum Einrichten eines Speicherorts für [!DNL Oracle Responsys]-Ziele

Die nachstehende Anfrage stellt eine Zielverbindung zu [!DNL Oracle Responsys]-Zielen her, um zu bestimmen, wo die exportierten Dateien an Ihrem Speicherort abgelegt werden sollen. Behalten Sie je nach Speicherort, an den Sie die Dateien exportieren möchten, die entsprechende `params`-Spezifikation bei und löschen Sie die anderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Responsys",
    "description": "Connection to Oracle Responsys",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ Beispielanfrage zum Einrichten eines Speicherorts für [!DNL Salesforce Marketing Cloud]-Ziele

Die nachstehende Anfrage stellt eine Zielverbindung zu [!DNL Salesforce Marketing Cloud]-Zielen her, um zu bestimmen, wo die exportierten Dateien an Ihrem Speicherort abgelegt werden sollen. Behalten Sie je nach Speicherort, an den Sie die Dateien exportieren möchten, die entsprechende `params`-Spezifikation bei und löschen Sie die anderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Salesforce Marketing Cloud",
    "description": "Connection to Salesforce Marketing Cloud",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ Beispielanfrage zum Einrichten eines Speicherorts für SFTP-Ziele

Die folgende Anfrage stellt eine Zielverbindung zu SFTP-Zielen her, um zu bestimmen, wo die exportierten Dateien an Ihrem Speicherort abgelegt werden sollen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for SFTP",
    "description": "Connection to SFTP",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
    }
}'
```

+++


| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `name` | Geben Sie einen Namen für die Zielverbindung zum Batch-Ziel an. |
| `description` | Optional können Sie eine Beschreibung für die Zielverbindung angeben. |
| `baseConnectionId` | Verwenden Sie die ID der Basisverbindung, die Sie im obigen Schritt erstellt haben. |
| `connectionSpec.id` | Verwenden Sie die Verbindungsspezifikations-ID für Ihr gewünschtes Batch-Ziel. Sie haben diese ID im Schritt [Abrufen der Liste der verfügbaren Ziele](#get-the-list-of-available-destinations) erhalten. |
| `params` | Je nach Ziel, mit dem Sie eine Verbindung herstellen, müssen Sie für Ihren Speicherort unterschiedliche erforderliche Parameter angeben. Bei Verbindungen des Typs Amazon S3 müssen Sie Ihre Zugriffs-ID und den geheimen Schlüssel für Ihren Speicherort im Amazon S3-Speicher angeben. <br> Um die erforderlichen Parameter für Ihr Ziel zu ermitteln, führen Sie einen [GET-Aufruf an den Verbindungsspezifikationen-Endpunkt](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec) durch, wobei Sie die Verbindungsspezifikation Ihres gewünschten Ziels angeben. Suchen Sie in der Antwort nach dem Parameter `targetSpec.spec.required`. |
| `params.mode` | Abhängig vom unterstützten Modus für Ihr Ziel müssen Sie hier einen anderen Wert angeben. Um die erforderlichen Parameter für Ihr Ziel zu ermitteln, führen Sie einen [GET-Aufruf an den Verbindungsspezifikationen-Endpunkt](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec) durch, wobei Sie die Verbindungsspezifikation Ihres gewünschten Ziels anzugeben. Suchen Sie in der Antwort nach dem Parameter `targetSpec.spec.properties.mode.enum` und wählen Sie den gewünschten Modus aus. |
| `params.bucketName` | Geben Sie bei S3-Verbindungen den Namen des Behälters an, in den Dateien exportiert werden sollen. |
| `params.path` | Geben Sie bei S3-Verbindungen den Dateipfad in Ihrem Speicherort an, an den Dateien exportiert werden sollen. |
| `params.format` | `CSV` ist derzeit der einzige unterstützte Dateiexporttyp. |

{style="table-layout:auto"}

**Antwort**

Bei einer erfolgreichen Antwort wird die eindeutige Kennung (`id`) für die neu erstellte Zielverbindung zu Ihrem Batch-Ziel zurückgegeben. Notieren Sie sich diesen Wert, da Sie ihn in späteren Schritten benötigen werden.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Erstellen eines Datenflusses {#create-dataflow}

![Übersicht über die Zielschritte – Schritt 4](../assets/api/batch-destination/step4.png)

Mithilfe der Flussspezifikation, der Quellverbindungs- und der Zielverbindungs-IDs können Sie nun einen Datenfluss zwischen Ihren [!DNL Experience Platform]-Daten und dem Ziel erstellen, in das Sie Datendateien exportieren werden. Stellen Sie sich diesen Schritt wie den Bau einer Pipeline vor, durch die später Daten zwischen [!DNL Experience Platform] und dem gewünschten Ziel fließen werden.

Um einen Datenfluss zu erstellen, führen Sie eine POST-Anfrage durch (wie unten dargestellt) und geben Sie dabei die unten genannten Werte in der Payload an.

**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "activate audiences to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate audiences to Adobe Campaign",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ],
        "transformations": [
            {
                "name": "GeneralTransform",
                "params": {
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `name` | Geben Sie einen Namen für den Datenfluss an, den Sie erstellen. |
| `description` | Optional können Sie eine Beschreibung für den Datenfluss angeben. |
| `flowSpec.Id` | Verwenden Sie die Flussspezifikations-ID für das Batch-Ziel, mit dem Sie eine Verbindung herstellen möchten. Um die Flussspezifikations-ID abzurufen, führen Sie einen GET-Vorgang für den Endpunkt `flowspecs` durch, wie in der [API-Referenzdokumentation für Flussspezifikationen](https://www.adobe.io/experience-platform-apis/references/flow-service/#operation/retrieveFlowSpec) beschrieben. Suchen Sie in der Antwort nach `upsTo` und kopieren Sie die entsprechende ID des Batch-Ziels, mit dem Sie eine Verbindung herstellen möchten. Suchen Sie zum Beispiel für Adobe Campaign nach `upsToCampaign` und kopieren Sie den `id`-Parameter. |
| `sourceConnectionIds` | Verwenden Sie die Quellverbindungs-ID, die Sie im Schritt [Verbinden mit Ihren Experience Platform-Daten](#connect-to-your-experience-platform-data) erhalten haben. |
| `targetConnectionIds` | Verwenden Sie die Zielverbindungs-ID, die Sie im Schritt [Verbinden mit dem Batch-Ziel](#connect-to-batch-destination) erhalten haben. |
| `transformations` | Im nächsten Schritt werden Sie diesen Abschnitt mit den Zielgruppen und Profilattributen füllen, die aktiviert werden sollen. |

Die nachstehende Tabelle enthält die Flussspezifikations-IDs für häufig verwendete Batch-Ziele:

| Ziel | Flussspezifikations-ID |
---------|----------|
| Alle Cloud-Speicher-Ziele ([!DNL Amazon S3], SFTP, [!DNL Azure Blob]) und [!DNL Oracle Eloqua] | `71471eba-b620-49e4-90fd-23f1fa0174d8` |
| [!DNL Oracle Responsys] | `51d675ce-e270-408d-91fc-22717bdf2148` |
| [!DNL Salesforce Marketing Cloud] | `493b2bd6-26e4-4167-ab3b-5e910bba44f0` |

**Antwort**

Bei einer erfolgreichen Antwort werden die Kennung (`id`) des neu erstellten Datenflusses und ein `etag` zurückgegeben. Notieren Sie sich beide Werte, da Sie sie im nächsten Schritt benötigen werden, um Zielgruppen zu aktivieren und Datendateien zu exportieren.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Daten an Ihr neues Ziel aktivieren {#activate-data}

![Übersicht über die Zielschritte – Schritt 5](../assets/api/batch-destination/step5.png)

Nachdem Sie alle Verbindungen sowie den Datenfluss erstellt haben, können Sie jetzt Ihre Profildaten für die Zielplattform aktivieren. In diesem Schritt wählen Sie aus, welche Zielgruppen und Profilattribute an das Ziel exportiert werden sollen.

Sie können auch das Dateibenennungsformat der exportierten Dateien bestimmen und festlegen, welche Attribute als [Deduplizierungsschlüssel](../ui/activate-batch-profile-destinations.md#mandatory-keys) oder [obligatorische Attribute](../ui/activate-batch-profile-destinations.md#mandatory-attributes) verwendet werden sollen. In diesem Schritt können Sie auch den Zeitplan für das Senden von Daten an das Ziel festlegen.

Um Zielgruppen für Ihr neues Ziel zu aktivieren, müssen Sie einen JSON-PATCH-Vorgang ausführen, der dem unten stehenden Beispiel ähnelt. Sie können mehrere Zielgruppen und Profilattribute in einem Aufruf aktivieren. Weiterführende Informationen zu JSON PATCH finden Sie in der [RFC-Spezifikation](https://tools.ietf.org/html/rfc6902).

**API-Format**

```http
PATCH /flows
```

**Anfrage**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
    {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                } 
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "triggerType": "SCHEDULED",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                },   
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `{DATAFLOW_ID}` | Verwenden Sie in der URL die ID des Datenflusses, den Sie im vorherigen Schritt erstellt haben. |
| `{ETAG}` | Rufen Sie die `{ETAG}` aus der Antwort im vorherigen Schritt, [Erstellen eines Datenflusses](#create-dataflow). Das Antwortformat im vorherigen Schritt hat Escape-Anführungszeichen. Sie müssen die nicht maskierten Werte in der Kopfzeile der Anfrage verwenden. Siehe Beispiel unten: <br> <ul><li>Reaktionsbeispiel: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>Wert, der in Ihrer Anfrage verwendet werden soll: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung eines Datenflusses aktualisiert. |
| `{SEGMENT_ID}` | Geben Sie die Zielgruppen-ID an, die Sie an dieses Ziel exportieren möchten. Informationen zum Abrufen der Zielgruppen-IDs für die Zielgruppen, die Sie aktivieren möchten, finden Sie unter [Abrufen einer Zielgruppendefinition](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) in der Experience Platform-API-Referenz. |
| `{PROFILE_ATTRIBUTE}` | Beispiel: `"person.lastName"` |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um einem Datenfluss eine Zielgruppe hinzuzufügen, verwenden Sie die `add` Vorgang. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. Verwenden Sie beim Hinzufügen einer Zielgruppe zu einem Datenfluss den im Beispiel angegebenen Pfad. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |
| `id` | Geben Sie die ID der Audience an, die Sie dem Ziel-Datenfluss hinzufügen möchten. |
| `name` | *Optional*. Geben Sie den Namen der Audience an, die Sie dem Ziel-Datenfluss hinzufügen möchten. Beachten Sie, dass dieses Feld nicht erforderlich ist und Sie dem Ziel-Datenfluss erfolgreich eine Zielgruppe hinzufügen können, ohne dessen Namen anzugeben. |
| `filenameTemplate` | Dieses Feld bestimmt das Dateinamenformat der Dateien, die an Ihr Ziel exportiert werden. <br> Die folgenden Optionen sind verfügbar: <br> <ul><li>`%DESTINATION_NAME%`: Obligatorisch. Die exportierten Dateien enthalten den Zielnamen.</li><li>`%SEGMENT_ID%`: Obligatorisch. Die exportierten Dateien enthalten die Kennung der exportierten Audience.</li><li>`%SEGMENT_NAME%`: Optional. Die exportierten Dateien enthalten den Namen der exportierten Audience.</li><li>`DATETIME(YYYYMMdd_HHmmss)` oder `%TIMESTAMP%`: Optional. Wählen Sie eine dieser beiden Optionen für Ihre Dateien aus, um den Zeitpunkt einzuschließen, zu dem sie von Experience Platform generiert werden.</li><li>`custom-text`: Optional. Ersetzen Sie diesen Platzhalter durch einen beliebigen benutzerdefinierten Text, den Sie am Ende Ihrer Dateinamen anhängen möchten.</li></ul> <br> Weitere Informationen zur Konfiguration von Dateinamen finden Sie im Abschnitt [Konfigurieren von Dateinamen](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) im Tutorial zur Aktivierung von Batch-Zielen. |
| `exportMode` | Obligatorisch. Wählen Sie `"DAILY_FULL_EXPORT"` oder `"FIRST_FULL_THEN_INCREMENTAL"` aus. Weitere Informationen zu den beiden Optionen finden Sie unter [Exportieren von vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Exportieren von inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) im Tutorial zur Aktivierung von Batch-Zielen. |
| `startDate` | Wählen Sie das Datum aus, an dem die Audience mit dem Export von Profilen in Ihr Ziel beginnen soll. |
| `frequency` | Obligatorisch. <br> <ul><li>Für den Exportmodus `"DAILY_FULL_EXPORT"` können Sie `ONCE` oder `DAILY` wählen.</li><li>Für den Exportmodus `"FIRST_FULL_THEN_INCREMENTAL"` können Sie `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"` wählen.</li></ul> |
| `triggerType` | Für *Batch-Ziele* nur. Dieses Feld ist nur erforderlich, wenn Sie die `"DAILY_FULL_EXPORT"` -Modus im `frequency` auswählen. <br> Obligatorisch. <br> <ul><li>Auswählen `"AFTER_SEGMENT_EVAL"` , damit der Aktivierungsauftrag unmittelbar nach Abschluss des täglichen Platform-Batch-Segmentierungsauftrags ausgeführt wird. Dadurch wird sichergestellt, dass bei der Ausführung des Aktivierungsvorgangs die aktuellen Profile nach Ihrem Ziel exportiert werden.</li><li>Auswählen `"SCHEDULED"` , damit der Aktivierungsauftrag zu einem festen Zeitpunkt ausgeführt wird. Dadurch wird sichergestellt, dass Experience Platform-Profildaten jeden Tag gleichzeitig exportiert werden. Je nachdem, ob der Batch-Segmentierungsauftrag vor dem Beginn des Aktivierungsvorgangs abgeschlossen wurde, sind die zu exportierenden  jedoch möglicherweise nicht die aktuellsten. Bei Auswahl dieser Option müssen Sie auch eine `startTime` um anzugeben, zu welchem Zeitpunkt in UTC die täglichen Exporte stattfinden sollen.</li></ul> |
| `endDate` | Für *Batch-Ziele* nur. Dieses Feld ist nur erforderlich, wenn einem Datenfluss in Batch-Dateiexport-Zielen wie Amazon S3, SFTP oder Azure Blob eine Zielgruppe hinzugefügt wird. <br> Nicht anwendbar bei der Auswahl von `"exportMode":"DAILY_FULL_EXPORT"` und `"frequency":"ONCE"`. <br> Legt das Datum fest, an dem Audience-Mitglieder nicht mehr in das Ziel exportiert werden. |
| `startTime` | Für *Batch-Ziele* nur. Dieses Feld ist nur erforderlich, wenn einem Datenfluss in Batch-Dateiexport-Zielen wie Amazon S3, SFTP oder Azure Blob eine Zielgruppe hinzugefügt wird. <br> Obligatorisch. Wählen Sie den Zeitpunkt aus, zu dem Dateien mit Mitgliedern der Audience generiert und an Ihr Ziel exportiert werden sollen. |

{style="table-layout:auto"}

>[!TIP]
>
> Siehe [Komponenten einer Zielgruppe in einem Datenfluss aktualisieren](/help/destinations/api/update-destination-dataflows.md#update-segment) um zu erfahren, wie Sie verschiedene Komponenten (Dateinamenvorlage, Exportzeit usw.) exportierter Zielgruppen aktualisieren.

**Antwort**

Suchen Sie nach einer „202 Accepted“-Antwort. Es wird kein Antworttext zurückgegeben. Um zu überprüfen, ob die Anfrage korrekt war, lesen Sie den nächsten Schritt [Validieren des Datenflusses](#validate-dataflow).

## Validieren des Datenflusses {#validate-dataflow}

![Übersicht über die Zielschritte – Schritt 6](../assets/api/batch-destination/step6.png)

Als letzten Schritt im Tutorial sollten Sie überprüfen, ob die Zielgruppen und Profilattribute dem Datenfluss korrekt zugeordnet wurden.

Führen Sie zur Validierung die folgende GET-Anfrage aus:

**API-Format**

```http
GET /flows
```

**Anfrage**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Verwenden Sie den Datenfluss aus dem vorherigen Schritt.
* `{ETAG}`: Verwenden Sie das eTag aus dem vorherigen Schritt.

**Antwort**

Die zurückgegebene Antwort sollte im `transformations` Parameter: die Zielgruppen und Profilattribute, die Sie im vorherigen Schritt gesendet haben. Ein Beispielparameter `transformations` in der Antwort könnte wie folgt aussehen:

```json
"transformations":[
   {
      "name":"GeneralTransform",
      "params":{
         "profileSelectors":{
            "selectors":[
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"homeAddress.countryCode",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"homeAddress.countryCode",
                        "destination":"homeAddress.countryCode",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"homeAddress.countryCode",
                        "destinationXdmPath":"homeAddress.countryCode"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.firstName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.firstName",
                        "destination":"person.name.firstName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.firstName",
                        "destinationXdmPath":"person.name.firstName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.lastName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.lastName",
                        "destination":"person.name.lastName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.lastName",
                        "destinationXdmPath":"person.name.lastName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"personalEmail.address",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"personalEmail.address",
                        "destination":"personalEmail.address",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"personalEmail.address",
                        "destinationXdmPath":"personalEmail.address"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"segmentMembership.status",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"segmentMembership.status",
                        "destination":"segmentMembership.status",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"segmentMembership.status",
                        "destinationXdmPath":"segmentMembership.status"
                     }
                  }
               }
            ],
            "mandatoryFields":[
               "person.name.firstName",
               "person.name.lastName"
            ],
            "primaryFields":[
               {
                  "fieldType":"ATTRIBUTE",
                  "attributePath":"personalEmail.address"
               }
            ]
         },
         "segmentSelectors":{
            "selectors":[
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                     "name":"Interested in Mountain Biking",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"DAILY_FULL_EXPORT",
                     "schedule":{
                        "frequency":"ONCE",
                        "startDate":"2021-12-20",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               },
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"25768be6-ebd5-45cc-8913-12fb3f348613",
                     "name":"Loyalty Segment",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                     "schedule":{
                        "frequency":"EVERY_6_HOURS",
                        "startDate":"2021-12-22",
                        "endDate":"2021-12-31",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               }
            ]
         }
      }
   }
]
```

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen für die Fehlermeldung bei der Experience Platform-API. Siehe [API-Statuscodes](/help/landing/troubleshooting.md#api-status-codes) und [Fehler in der Anfragekopfzeile](/help/landing/troubleshooting.md#request-header-errors) Weitere Informationen zur Interpretation von Fehlerantworten finden Sie im Handbuch zur Fehlerbehebung bei Platform .

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie Platform erfolgreich mit einem Ihrer bevorzugten Batch-Cloud-Speicher- oder E-Mail-Marketing-Ziele verbunden und einen Datenfluss zum entsprechenden Ziel eingerichtet, um Datendateien zu exportieren. Ausgehende Daten können jetzt im Ziel für E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle genutzt werden. Auf den folgenden Seiten finden Sie weitere Details, z. B. wie Sie vorhandene Datenflüsse mit der Flow Service-API bearbeiten:

* [Ziele – Übersicht](../home.md)
* [Zielkatalog – Übersicht](../catalog/overview.md)
* [Aktualisieren von Zieldatenflüssen mithilfe der Flow Service-API](../api/update-destination-dataflows.md)
