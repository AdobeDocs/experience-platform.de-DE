---
solution: Experience Platform
title: Exportieren von Datensätzen mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie mit der Flow Service-API Datensätze für ausgewählte Ziele exportieren können.
type: Tutorial
exl-id: f23a4b22-da04-4b3c-9b0c-790890077eaa
source-git-commit: 28e07c464eb05ba7c20b132d430fccac15d8806e
workflow-type: tm+mt
source-wordcount: '3526'
ht-degree: 18%

---

# Exportieren von Datensätzen mithilfe der [!DNL Flow Service API]

>[!AVAILABILITY]
>
>* Diese Funktion steht Kunden zur Verfügung, die das Real-Time CDP Prime- und Ultimate-Package, Adobe Journey Optimizer oder Customer Journey Analytics erworben haben. Wenden Sie sich für weitere Informationen an Ihren Adobe-Support-Mitarbeiter.

In diesem Artikel wird der Workflow erläutert, der zur Verwendung der [!DNL Flow Service API] zum Export [Datensätze](/help/catalog/datasets/overview.md) von Adobe Experience Platform zu Ihrem bevorzugten Cloud-Speicher, z. B. [!DNL Amazon S3], SFTP-Speicherorten oder [!DNL Google Cloud Storage].

>[!TIP]
>
>Sie können Datensätze auch über die Experience Platform-Benutzeroberfläche exportieren. Lesen Sie die [Tutorial zur Benutzeroberfläche von Datensätzen exportieren](/help/destinations/ui/export-datasets.md) für weitere Informationen.

## Für den Export verfügbare Datensätze {#datasets-to-export}

Die Datensätze, die Sie exportieren können, hängen von der Experience Platform-Anwendung (Real-Time CDP, Adobe Journey Optimizer), der Ebene (Prime oder Ultimate) und den von Ihnen gekauften Add-ons (z. B. Data Distiller) ab.

Siehe Abschnitt [Tabelle auf der UI-Tutorial-Seite](/help/destinations/ui/export-datasets.md#datasets-to-export) , um zu verstehen, welche Datensätze exportiert werden können.

## Unterstützte Ziele {#supported-destinations}

Derzeit können Sie Datensätze zu den im Screenshot hervorgehobenen und unten aufgeführten Cloud-Speicher-Zielen exportieren.

![Ziele, die Datensatzexporte unterstützen](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Erste Schritte {#get-started}

![Übersicht - Schritte zum Erstellen eines Ziels und Exportieren von Datensätzen](../assets/api/export-datasets/export-datasets-api-workflow-get-started.png)

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Platform datasets]](/help/catalog/datasets/overview.md): Alle Daten, die erfolgreich in Adobe Experience Platform erfasst wurden, bleiben im [!DNL Data Lake] als Datensätze. Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Datensätze enthalten auch Metadaten, die verschiedene Aspekte der in ihnen gespeicherten Daten beschreiben.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um Datensätze in Cloud-Speicher-Ziele in Platform zu exportieren.

### Erforderliche Berechtigungen {#permissions}

Zum Exportieren von Datensätzen benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Datensatzziele verwalten und aktivieren]** Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um sicherzustellen, dass Sie über die erforderlichen Berechtigungen zum Exportieren von Datensätzen verfügen und dass das Ziel den Export von Datensätzen unterstützt, durchsuchen Sie den Zielkatalog. Wenn ein Ziel über die Steuerung **[!UICONTROL Aktivieren]** oder **[!UICONTROL Datensätze exportieren]** verfügt, dann haben Sie die entsprechenden Berechtigungen.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln der Werte für erforderliche und optionale Kopfzeilen {#gather-values-headers}

Um Aufrufe an [!DNL Platform] APIs verwenden, müssen Sie zunächst die [Tutorial zur Experience Platform-Authentifizierung](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de). Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

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

Eine zugehörige Referenzdokumentation für alle API-Vorgänge finden Sie in diesem Tutorial. Siehe Abschnitt [[!DNL Flow Service] - Dokumentation zur Ziel-API auf der Adobe Developer-Website](https://developer.adobe.com/experience-platform-apis/references/destinations/). Wir empfehlen, dass Sie dieses Tutorial und die API-Referenzdokumentation parallel verwenden.

### Glossar {#glossary}

Beschreibungen der Begriffe, auf die Sie in diesem API-Tutorial treffen werden, finden Sie im [Glossarabschnitt](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) der API-Referenzdokumentation.

### Zusammenstellen von Verbindungs- und Flussspezifikationen für Ihr gewünschtes Ziel {#gather-connection-spec-flow-spec}

Bevor Sie mit dem Workflow zum Exportieren eines Datensatzes beginnen, identifizieren Sie die Verbindungsspezifikationen und Flussspezifikations-IDs des Ziels, an das Sie Datensätze exportieren möchten. Verwenden Sie die nachstehende Tabelle als Referenz.


| Ziel | Verbindungsspezifikation | Flussspezifikation |
---------|----------|---------|
| [!DNL Amazon S3] | `4fce964d-3f37-408f-9778-e597338a21ee` | `269ba276-16fc-47db-92b0-c1049a3c131f` |
| [!DNL Azure Blob Storage] | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `95bd8965-fc8a-4119-b9c3-944c2c2df6d2` |
| [!DNL Azure Data Lake Gen 2(ADLS Gen2)] | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| [!DNL Data Landing Zone(DLZ)] | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| [!DNL Google Cloud Storage] | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `354d6aad-4754-46e4-a576-1b384561c440` |

{style="table-layout:auto"}

Sie benötigen diese IDs, um verschiedene [!DNL Flow Service] -Entitäten. Sie müssen auch auf Teile der [!DNL Connection Spec] selbst, um bestimmte Entitäten einzurichten, damit Sie die [!DNL Connection Spec] von [!DNL Flow Service APIs]. Siehe die folgenden Beispiele zum Abrufen von Verbindungsspezifikationen für alle Ziele in der Tabelle:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

+++Retrieve [!DNL connection spec] für [!DNL Amazon S3]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwort**

+++[!DNL Amazon S3] - Verbindungsspezifikation

```json
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure-Blobspeicher]

**Anfrage**

+++Retrieve [!DNL connection spec] für [!DNL Azure Blob Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6d6b59bf-fb58-4107-9064-4d246c0e5bb2' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwort**

+++[!DNL Azure Blob Storage] – [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Anfrage**

+++Retrieve [!DNL connection spec] für [!DNL Azure Data Lake Gen 2(ADLS Gen2])

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be2c3209-53bc-47e7-ab25-145db8b873e1' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwort**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] – [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Anfrage**

+++Retrieve [!DNL connection spec] für [!DNL Data Landing Zone(DLZ)]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/10440537-2a7b-4583-ac39-ed38d4b848e8' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwort**

+++[!DNL Data Landing Zone(DLZ)] – [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Google Cloud Storage]

**Anfrage**

+++Retrieve [!DNL connection spec] für [!DNL Google Cloud Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/c5d93acb-ea8b-4b14-8f53-02138444ae99' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwort**

+++[!DNL Google Cloud Storage] – [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB SFTP]

**Anfrage**

+++Retrieve [!DNL connection spec] für SFTP

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/36965a81-b1c6-401b-99f8-22508f1e6a26' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwort**

+++SFTP - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!ENDTABS]

Gehen Sie wie folgt vor, um einen Datensatz-Datenfluss zu einem Cloud-Speicher-Ziel einzurichten. Bei einigen Schritten unterscheiden sich die Anforderungen und Antworten zwischen den verschiedenen Cloud-Speicher-Zielen. Verwenden Sie in diesen Fällen die Registerkarten auf der Seite, um die Anforderungen und Antworten abzurufen, die spezifisch für das Ziel sind, mit dem Sie Datensätze verbinden und exportieren möchten. Stellen Sie sicher, dass Sie die richtige [!DNL connection spec] und [!DNL flow spec] für das Ziel, das Sie konfigurieren.

## Liste von Datensätzen abrufen {#retrieve-list-of-available-datasets}

![Abbildung von Schritt 1 im Workflow &quot;Datensätze exportieren&quot;](../assets/api/export-datasets/export-datasets-api-workflow-retrieve-datasets.png)

Um eine Liste von Datensätzen abzurufen, die für die Aktivierung infrage kommen, führen Sie zunächst einen API-Aufruf an den unten stehenden Endpunkt durch.

>[!BEGINSHADEBOX]

**Anfrage**

+++Abrufen zulässiger Datensätze - Anfrage

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/23598e46-f560-407b-88d5-ea6207e49db0/configs?outputType=activationDatasets&outputField=datasets&start=0&limit=20&properties=name,state' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

Beachten Sie, dass zum Abrufen von geeigneten Datensätzen die [!DNL connection spec] Die in der Anfrage-URL verwendete ID muss die Data Lake-Quell-Verbindungsspezifikations-ID sein. `23598e46-f560-407b-88d5-ea6207e49db0`und die beiden Abfrageparameter `outputField=datasets` und `outputType=activationDatasets` muss angegeben werden. Alle anderen Abfrageparameter werden standardmäßig von der [Catalog Service-API](https://developer.adobe.com/experience-platform-apis/references/catalog/).

+++

**Antwort**

+++Datensätze abrufen - Antwort

```json
{
    "items": [
        {
            "id": "5ef3e324052581191aa6a466",
            "name": "AAM Authenticated Profiles Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e3259ad2a1191ab7dd7d",
            "name": "AAM Devices Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e325582424191b1beb42",
            "name": "AAM Devices Profile Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328582424191b1beb44",
            "name": "AAM Realtime",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328fe742a191b2b3ea5",
            "name": "AAM Realtime Profile Updates",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        }
    ],
    "pageInfo": {
        "start": 0,
        "end": 4,
        "total": 149,
        "hasNext": true
    }
}
```

+++

>[!ENDSHADEBOX]

Eine erfolgreiche Antwort enthält eine Liste von Datensätzen, die für die Aktivierung infrage kommen. Diese Datensätze können beim Erstellen der Quellverbindung im nächsten Schritt verwendet werden.

Informationen zu den verschiedenen Antwortparametern für jeden zurückgegebenen Datensatz finden Sie im Abschnitt [Entwicklerdokumentation für die Datensatz-API](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets).

## Erstellen einer Quellverbindung {#create-source-connection}

![Abbildung von Schritt 2 im Workflow &quot;Datensätze exportieren&quot;](../assets/api/export-datasets/export-datasets-api-workflow-create-source-connection.png)

Nachdem Sie die Liste der Datensätze abgerufen haben, die Sie exportieren möchten, können Sie mit diesen Datensatz-IDs eine Quellverbindung erstellen.

>[!BEGINSHADEBOX]

**Anfrage**

+++Quellverbindung erstellen - Anfrage

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="12,16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
  "name": "Connecting to Data Lake",
  "description": "Data Lake source connection to export datasets",
  "connectionSpec": {
    "id": "23598e46-f560-407b-88d5-ea6207e49db0", // this connection spec ID is always the same for Source Connections
    "version": "1.0"
  },
  "params": {
    "datasets": [ // datasets to activate
      {
        "dataSetId": "5ef3e3259ad2a1191ab7dd7d",
        "name": "AAM Devices Data"
      }
    ]
  }
}'
```

+++



**Antwort**

+++Quellverbindung erstellen - Antwort

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

Eine erfolgreiche Antwort gibt die ID (`id`) der neu erstellten Quellverbindung und einer `etag`. Notieren Sie sich die Kennung der Quellverbindung, wie Sie sie später beim Erstellen des Datenflusses benötigen.

Beachten Sie auch Folgendes:

* Die in diesem Schritt erstellte Quellverbindung muss mit einem Datenfluss verknüpft werden, damit seine Datensätze für ein Ziel aktiviert werden. Siehe [Erstellen eines Datenflusses](#create-dataflow) Informationen zum Verknüpfen einer Quellverbindung mit einem Datenfluss.
* Die Datensatz-IDs einer Quellverbindung können nach der Erstellung nicht mehr geändert werden. Wenn Sie Datensätze zu einer Quellverbindung hinzufügen oder daraus entfernen müssen, müssen Sie eine neue Quellverbindung erstellen und die Kennung der neuen Quellverbindung mit dem Datenfluss verknüpfen.

## Erstellen einer Basisverbindung (Ziel) {#create-base-connection}

![Abbildung von Schritt 3 im Workflow &quot;Datensätze exportieren&quot;](../assets/api/export-datasets/export-datasets-api-workflow-create-base-connection.png)

Eine Basisverbindung speichert die Anmeldeinformationen sicher in Ihrem Ziel. Je nach Zieltyp können die für die Authentifizierung an diesem Ziel erforderlichen Anmeldeinformationen variieren. Um diese Authentifizierungsparameter zu finden, rufen Sie zunächst die [!DNL connection spec] für Ihr gewünschtes Ziel, wie im Abschnitt beschrieben [Verbindungsspezifikationen und Flussspezifikationen sammeln](#gather-connection-spec-flow-spec) und dann die `authSpec` der Antwort. Verweisen Sie auf die folgenden Registerkarten für die `authSpec` Eigenschaften aller unterstützten Ziele.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] Anzeige [!DNL auth spec]

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die Authentifizierungsparameter in der [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Access Key",
                    "type": "KeyBased",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines auth params required for connecting to amazon-s3",
                        "type": "object",
                        "properties": {
                            "s3AccessKey": {
                                "description": "Access key id",
                                "type": "string",
                                "pattern": "^[A-Z2-7]{20}$"
                            },
                            "s3SecretKey": {
                                "description": "Secret access key for the user account",
                                "type": "string",
                                "format": "password",
                                "pattern": "^[A-Za-z0-9\/\\+]{40}$"
                            }
                        },
                        "required": [
                            "s3SecretKey",
                            "s3AccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB Azure-Blobspeicher]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] Anzeige [!DNL auth spec]

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die Authentifizierungsparameter in der [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "ConnectionString",
                    "type": "ConnectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Connection String for Azure Blob based destinations",
                        "type": "object",
                        "properties": {
                            "connectionString": {
                                "description": "connection string for login",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] Anzeige [!DNL auth spec]

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die Authentifizierungsparameter in der [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Azure Service Principal Auth",
                    "type": "AzureServicePrincipal",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "type": "object",
                        "properties": {
                            "url": {
                                "description": "Endpoint for Azure Data Lake Storage Gen2.",
                                "type": "string"
                            },
                            "servicePrincipalId": {
                                "description": "Service Principal Id to connect to ADLSGen2.",
                                "type": "string"
                            },
                            "servicePrincipalKey": {
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "type": "string",
                                "format": "password"
                            },
                            "tenant": {
                                "description": "Tenant information(domain name or tenant ID).",
                                "type": "string"
                            }
                        },
                        "required": [
                            "servicePrincipalKey",
                            "url",
                            "tenant",
                            "servicePrincipalId"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Data Landing Zone (DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] Anzeige [!DNL auth spec]

>[!NOTE]
>
>Für das Data Landing Zone-Ziel ist kein [!DNL auth spec].

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [],
//...
```

+++

>[!TAB Google Cloud Storage]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] Anzeige [!DNL auth spec]

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die Authentifizierungsparameter in der [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Google Cloud Storage authentication credentials",
                    "type": "GoogleCloudStorageAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to google cloud storage connector.",
                        "type": "object",
                        "properties": {
                            "accessKeyId": {
                                "description": "Access Key Id for the user account",
                                "type": "string"
                            },
                            "secretAccessKey": {
                                "description": "Secret Access Key for the user account",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] Anzeige [!DNL auth spec]

>[!NOTE]
>
>Das SFTP-Ziel enthält zwei separate Elemente im [!DNL auth spec], da es sowohl die Authentifizierung von Passwörtern als auch von SSH-Schlüsseln unterstützt.

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die Authentifizierungsparameter in der [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "SFTP with Password",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations with a password",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "password": {
                                "description": "Password",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "password",
                            "domain",
                            "username"
                        ]
                    }
                },
                {
                    "name": "SFTP with SSH Key",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations using SSH Key",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "sshKey": {
                                "description": "Base64 string of the private SSH key",
                                "type": "string",
                                "format": "password",
                                "contentEncoding": "base64",
                                "uiAttributes": {
                                    "tooltip": {
                                        "id": "platform_destinations_connect_sftp_ssh",
                                        "fallbackUrl": "http://www.adobe.com/go/destinations-sftp-connection-parameters-en "
                                    }
                                }
                            }
                        },
                        "required": [
                            "sshKey",
                            "domain",
                            "username"
                        ]
                    }
                }
            ],
//...
```

+++

>[!ENDTABS]

Verwenden der im Authentifizierungsspezifikat angegebenen Eigenschaften (d. h. `authSpec` aus der Antwort) können Sie eine Basisverbindung mit den erforderlichen Anmeldeinformationen erstellen, die für jeden Zieltyp spezifisch sind, wie in den folgenden Beispielen dargestellt:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

+++[!DNL Amazon S3] - Grundlegende Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsberechtigungen finden Sie im Abschnitt [beim Ziel authentifizieren](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) auf der Zieldokumentationsseite für Amazon S3.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Access Key",
    "params": {
      "s3SecretKey": "<Add secret key>",
      "s3AccessKey": "<Add access key>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwort**

+++[!DNL Amazon S3] Basisverbindungsantwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure-Blobspeicher]

**Anfrage**

+++[!DNL Azure Blob Storage] - Grundlegende Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsberechtigungen finden Sie im Abschnitt [beim Ziel authentifizieren](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) auf der Seite mit der Dokumentation zum Azure Blob Storage-Ziel.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Blob Storage Base Connection",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "connectionString": "<Add Azure Blob connection string>"
    }
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwort**

+++[!DNL Azure Blob Storage] - Antwort auf Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Anfrage**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Grundlegende Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsberechtigungen finden Sie im Abschnitt [beim Ziel authentifizieren](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) Abschnitt der Zieldokumentation für Azure Data Lake Gen 2 (ADLS Gen2).

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Data Lake Gen 2(ADLS Gen2) Base Connection",
  "auth": {
    "specName": "Azure Service Principal Auth",
    "params": {
      "servicePrincipalKey": "<Add servicePrincipalKey>",
      "url": "<Add url>",
      "tenant": "<Add tenant>",
      "servicePrincipalId": "<Add servicePrincipalId>"
    }
  },
  "connectionSpec": {
    "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwort**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Antwort auf Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Anfrage**

+++[!DNL Data Landing Zone(DLZ)] - Grundlegende Verbindungsanforderung

>[!TIP]
>
>Für das Data Landing Zone-Ziel sind keine Authentifizierungsberechtigungen erforderlich. Weitere Informationen finden Sie im Abschnitt [beim Ziel authentifizieren](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) auf der Zieldokumentationsseite der Data Landing Zone .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone(DLZ) Base Connection"
}'
```

+++

**Antwort**

+++[!DNL Data Landing Zone] - Antwort auf Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Anfrage**

+++[!DNL Google Cloud Storage] - Grundlegende Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsberechtigungen finden Sie im Abschnitt [beim Ziel authentifizieren](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) auf der Zieldokumentationsseite für Google Cloud Storage .

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Google Cloud Storage Base Connection",
  "auth": {
    "specName": "Google Cloud Storage authentication credentials",
    "params": {
      "accessKeyId": "<Add accessKeyId>",
      "secretAccessKey": "<Add secret Access Key>"
    }
  },
  "connectionSpec": {
    "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwort**

+++[!DNL Google Cloud Storage] - Antwort auf Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Anfrage**

+++SFTP mit Passwort - Grundlegende Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsberechtigungen finden Sie im Abschnitt [beim Ziel authentifizieren](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) auf der Seite mit der Dokumentation zum SFTP-Ziel.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with password Base Connection",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "password": "<Add password>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

+++SFTP mit SSH-Schlüssel - Basis-Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsberechtigungen finden Sie im Abschnitt [beim Ziel authentifizieren](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) auf der Seite mit der Dokumentation zum SFTP-Ziel.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwort**

+++SFTP - Antwort auf Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Notieren Sie die Verbindungs-ID aus der Antwort. Diese ID ist im nächsten Schritt beim Erstellen der Zielverbindung erforderlich.

## Erstellen einer Zielverbindung {#create-target-connection}

![Abbildung von Schritt 4 im Workflow &quot;Datensätze exportieren&quot;](../assets/api/export-datasets/export-datasets-api-workflow-create-target-connection.png)

Als Nächstes müssen Sie eine Zielverbindung erstellen, in der die Exportparameter für Ihre Datensätze gespeichert werden. Zu den Exportparametern gehören Speicherort, Dateiformat, Komprimierung und andere Details. Siehe Abschnitt `targetSpec` Eigenschaften, die in der Verbindungsspezifikation des Ziels bereitgestellt werden, um die unterstützten Eigenschaften für jeden Zieltyp zu verstehen. Verweisen Sie auf die folgenden Registerkarten für die `targetSpec` Eigenschaften aller unterstützten Ziele.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] Anzeigen der Zielverbindungsparameter

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die [!DNL target spec] Parameter in der Verbindungsspezifikation. Im folgenden Beispiel sehen Sie auch, welche Zielparameter *not* gilt für Datensatzexport-Ziele.

```json {line-numbers="true" start-line="1" highlight="10,41,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_bucket",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_folderpath",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Azure-Blobspeicher]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] Anzeigen der Zielverbindungsparameter

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die [!DNL target spec] Parameter in der Verbindungsspezifikation. Im folgenden Beispiel sehen Sie auch, welche Zielparameter *not* gilt für Datensatzexport-Ziele.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Output path (relative) indicating where to upload the data",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\'\\(\\)]+$"
                        },
                        "container": {
                            "title": "Container",
                            "description": "Container within the storage where to upload the data",
                            "type": "string",
                            "pattern": "^[a-z0-9](?!.*--)[a-z0-9-]{1,61}[a-z0-9]$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "container",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++


>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] Anzeigen der Zielverbindungsparameter

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die [!DNL target spec] Parameter in der Verbindungsspezifikation. Im folgenden Beispiel sehen Sie auch, welche Zielparameter *not* gilt für Datensatzexport-Ziele.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions":{...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Data Landing Zone (DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] Anzeigen der Zielverbindungsparameter

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die [!DNL target spec] Parameter in der Verbindungsspezifikation. Im folgenden Beispiel sehen Sie auch, welche Zielparameter *not* gilt für Datensatzexport-Ziele.

```json {line-numbers="true" start-line="1" highlight="9,21,36"}
"items": [
    {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
        "name": "Data Landing Zone",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [],
        "encryptionSpecs": [],
        "targetSpec": { // describes the target connection parameters
            "name": "User based target",
            "type": "UserNamespace",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "properties": {
                    "path": {
                        "title": "Folder path",
                        "description": "Enter the path to your Azure Data Lake Storage folder",
                        "type": "string"
                    },
                    "fileType": {...}, // not applicable to dataset destinations
                    "datasetFileType": {
                        "conditional": {
                            "field": "flowSpec.attributes._workflow",
                            "operator": "CONTAINS",
                            "value": "DATASETS"
                        },
                        "title": "File Type",
                        "description": "Select file format",
                        "type": "string",
                        "enum": [
                            "JSON",
                            "PARQUET"
                        ]
                    },
                    "csvOptions": {...}, // not applicable to dataset destinations
                    "compression": {
                        "title": "Compression format",
                        "description": "Select the desired file compression format.",
                        "type": "string",
                        "enum": [
                            "NONE",
                            "GZIP"
                        ]
                    }
                },
                "required": [
                    "path",
                    "datasetFileType",
                    "compression",
                    "fileType"
                ]
            }
//...
```

+++

>[!TAB Google Cloud Storage]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] Anzeigen der Zielverbindungsparameter

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die [!DNL target spec] Parameter in der Verbindungsspezifikation. Im folgenden Beispiel sehen Sie auch, welche Zielparameter *not* gilt für Datensatzexport-Ziele.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?!^goog.*$)(?!^.*g(o|0)(o|0)gle.*$)(((?=^.{3,63}$)(^([a-z0-9]|[a-z0-9][a-z0-9\\-_]*)[a-z0-9]$))|((?=^.{3,222}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])\\.)*([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])$)))"
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] Anzeigen der Zielverbindungsparameter

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im [!DNL connection spec] Beispiel unten, das zusätzliche Informationen darüber bereitstellt, wo die [!DNL target spec] Parameter in der Verbindungsspezifikation. Im folgenden Beispiel sehen Sie auch, welche Zielparameter *not* gilt für Datensatzexport-Ziele.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "remotePath": {
                            "title": "Folder path",
                            "description": "Enter your folder path",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "GZIP",
                                "NONE"
                            ]
                        }
                    },
                    "required": [
                        "remotePath",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                },
//...
```

+++

>[!ENDTABS]


Mithilfe des obigen Spezifikationen können Sie eine zielgerichtete Verbindungsanforderung erstellen, die speziell auf Ihr gewünschtes Cloud-Speicher-Ziel zugeschnitten ist, wie in den Registerkarten unten dargestellt.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

+++[!DNL Amazon S3] - Target-Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Zieldetails ausfüllen](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) Abschnitt [!DNL Amazon S3] Zieldokumentationsseite
>Für andere unterstützte Werte von `datasetFileType`finden Sie in der API-Referenzdokumentation.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwort**

+++Target-Verbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure-Blobspeicher]

**Anfrage**

+++[!DNL Azure Blob Storage] - Target-Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Zieldetails ausfüllen](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) Abschnitt [!DNL Azure Blob Storage] Zieldokumentationsseite
>Für andere unterstützte Werte von `datasetFileType`finden Sie in der API-Referenzdokumentation.


Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwort**

+++Target-Verbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Anfrage**

+++[!DNL Azure Blob Storage] - Target-Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Zieldetails ausfüllen](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) -Abschnitt des Azure [!DNL Data Lake Gen 2(ADLS Gen2)] Zieldokumentationsseite
>Für andere unterstützte Werte von `datasetFileType`finden Sie in der API-Referenzdokumentation.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Data Lake Gen 2(ADLS Gen2) Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwort**

+++Target-Verbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Anfrage**

+++[!DNL Data Landing Zone] - Target-Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Zieldetails ausfüllen](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) Abschnitt [!DNL Data Landing Zone] Zieldokumentationsseite
>Für andere unterstützte Werte von `datasetFileType`finden Sie in der API-Referenzdokumentation.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Data Landing Zone Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwort**

+++Target-Verbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Anfrage**

+++[!DNL Google Cloud Storage] - Target-Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Zieldetails ausfüllen](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) Abschnitt [!DNL Google Cloud Storage] Zieldokumentationsseite
>Für andere unterstützte Werte von `datasetFileType`finden Sie in der API-Referenzdokumentation.


Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Google Cloud Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwort**

+++Target-Verbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Anfrage**

+++SFTP - Target-Verbindungsanforderung

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Zieldetails ausfüllen](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) auf der Seite mit der Dokumentation zum SFTP-Ziel.
>Für andere unterstützte Werte von `datasetFileType`finden Sie in der API-Referenzdokumentation.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "SFTP Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwort**

+++Target-Verbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Beachten Sie die Target-Verbindungs-ID aus der Antwort. Diese ID ist im nächsten Schritt beim Erstellen des Datenflusses zum Exportieren von Datensätzen erforderlich.

## Erstellen eines Datenflusses {#create-dataflow}

![Abbildung von Schritt 5 im Workflow &quot;Datensätze exportieren&quot;](../assets/api/export-datasets/export-datasets-api-workflow-set-up-dataflow.png)

Der letzte Schritt in der Zielkonfiguration besteht darin, einen Datenfluss einzurichten. Ein Datenfluss verknüpft zuvor erstellte Entitäten und bietet außerdem Optionen zum Konfigurieren des Datensatzexport-Zeitplans. Verwenden Sie zum Erstellen des Datenflusses je nach gewünschtem Cloud-Speicher-Ziel die folgenden Payloads und ersetzen Sie die Entitäts-IDs aus vorherigen Schritten.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

+ + + Datensatz-Datenfluss erstellen auf [!DNL Amazon S3] destination - Request

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "269ba276-16fc-47db-92b0-c1049a3c131f", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. Use "interval": 1 when you select "timeUnit": "day"
        "startTime": 1675901210 // UNIX timestamp start time (in seconds)
    }
}'
```

+++

**Antwort**

+++Datenfluss erstellen - Antwort

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure-Blobspeicher]

**Anfrage**

+ + + Datensatz-Datenfluss erstellen auf [!DNL Azure Blob Storage] destination - Request

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "95bd8965-fc8a-4119-b9c3-944c2c2df6d2", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwort**

+++Datenfluss erstellen - Antwort

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Anfrage**

+ + + Datensatz-Datenfluss erstellen auf [!DNL Azure Data Lake Gen 2(ADLS Gen2)] destination - Request

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "flowSpec": {
        "id": "17be2013-2549-41ce-96e7-a70363bec293", // Azure Data Lake Gen 2(ADLS Gen2) flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwort**

+++Datenfluss erstellen - Antwort

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Anfrage**

+ + + Datensatz-Datenfluss erstellen auf [!DNL Data Landing Zone] destination - Request

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Data Landing Zone cloud storage destination",
    "flowSpec": {
        "id": "cd2fc47e-e838-4f38-a581-8fff2f99b63a", // Data Landing Zone flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwort**

+++Datenfluss erstellen - Antwort

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Anfrage**

+ + + Datensatz-Datenfluss erstellen auf [!DNL Google Cloud Storage] destination - Request

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Google Cloud Storage destination",
    "flowSpec": {
        "id": "585c15c4-6cbf-4126-8f87-e26bff78b657", // Google Cloud Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwort**

+++Datenfluss erstellen - Antwort

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Anfrage**

+ + + Erstellen eines Datensatzdataflow zum SFTP-Ziel - Anfrage

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anforderung, wenn Sie die Anforderung kopieren und in Ihr Terminal Ihrer Wahl einfügen.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "354d6aad-4754-46e4-a576-1b384561c440", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwort**

+++Datenfluss erstellen - Antwort

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Notieren Sie die Datenfluss-ID aus der Antwort. Diese ID ist im nächsten Schritt beim Abrufen der Datenflüsse erforderlich, um die erfolgreichen Datensatzexporte zu validieren.

## Abrufen von Datenflüssen {#get-dataflow-runs}

![Abbildung von Schritt 6 im Workflow &quot;Datensätze exportieren&quot;](../assets/api/export-datasets/export-datasets-api-workflow-validate-dataflow.png)

Um die Ausführungen eines Datenflusses zu überprüfen, verwenden Sie die DataFlow-Ausführungen-API:

>[!BEGINSHADEBOX]

**Anfrage**

+++Abrufen von Datenfluss-Ausführungen - Anfrage

Fügen Sie in der Anfrage zum Abrufen der Datenflug-Ausführungen als Abfrageparameter die Datenflug-ID hinzu, die Sie beim Erstellen des Datenflusses im vorherigen Schritt erhalten haben.

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**Antwort**

+++Abrufen von Datenfluss-Ausführungen - Antwort

```json
{
    "items": [
        {
            "id": "4b7728dd-83c9-4c38-95a4-24ddab545404",
            "createdAt": 1675807718296,
            "updatedAt": 1675807731834,
            "createdBy": "aep_activation_batch@AdobeID",
            "updatedBy": "acp_foundation_connectors@AdobeID",
            "createdClient": "aep_activation_batch",
            "updatedClient": "acp_foundation_connectors",
            "sandboxId": "7dfdcd30-0a09-11ea-8ea6-7bf93ce86c28",
            "sandboxName": "sand-1",
            "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
            "flowId": "aae5ec63-b0ac-4808-9a44-abf2ea67bd5a",
            "flowSpec": {
                "id": "615d3489-36d2-4671-9467-4ae1129facd3",
                "version": "1.0"
            },
            "providerRefId": "ba56f98e0c49b572adb249980c39b1c7",
            "etag": "\"08005e9e-0000-0200-0000-63e2cbf30000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1675807719411,
                    "completedAtUTC": 1675807719416
                },
                "sizeSummary": {
                    "inputBytes": 0
                },
                "recordSummary": {
                    "inputRecordCount": 0,
                    "skippedRecordCount": 0,
                    "sourceSummaries": [
                        {
                            "id": "ea2b1205-4692-49de-b448-ebf75b1d188a",
                            "inputRecordCount": 0,
                            "skippedRecordCount": 0,
                            "entitySummaries": [
                                {
//...
```

+++

>[!ENDSHADEBOX]

Informationen zu [Verschiedene Parameter, die von der DataFlow-Ausführungs-API zurückgegeben werden](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) in der API-Referenzdokumentation.

## Überprüfen eines erfolgreichen Datensatzexports {#verify}

Beim Exportieren von Datensätzen erstellt Experience Platform eine `.json`- oder `.parquet`-Datei an dem von Ihnen angegebenen Speicherort. Erwarten Sie, dass eine neue Datei entsprechend dem Exportplan, den Sie beim Speichern angegeben haben, in Ihrem Speicherort abgelegt wird. [Erstellen eines Datenflusses](#create-dataflow).

Experience Platform erstellt eine Ordnerstruktur am angegebenen Speicherort, in der die exportierten Datensatzdateien abgelegt werden. Für jeden Exportzeitpunkt wird ein neuer Ordner erstellt, wobei das folgende Muster befolgt wird:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Der standardmäßige Dateiname wird nach dem Zufallsprinzip generiert, was sicherstellt, dass die Namen von exportierten Dateien eindeutig sind.

### Beispiele für Datensatzdateien {#sample-files}

Das Vorhandensein dieser Dateien an Ihrem Speicherort bestätigt einen erfolgreichen Export. Um zu verstehen, wie die exportierten Dateien strukturiert sind, können Sie eine [Parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet)- oder [JSON](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)-Beispieldatei herunterladen.

#### Komprimierte Datensatzdateien {#compressed-dataset-files}

Im Schritt zum [Erstellen einer Zielverbindung](#create-target-connection)können Sie die exportierten Datensatzdateien auswählen, die komprimiert werden sollen.

Beachten Sie bei der Komprimierung den Unterschied im Dateiformat zwischen den beiden Dateitypen:

* Beim Exportieren komprimierter JSON-Dateien ist das exportierte Dateiformat `json.gz`
* Beim Exportieren komprimierter Parquet-Dateien ist das exportierte Dateiformat `gz.parquet`

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Experience Platform API-Fehlermeldungsprinzipien. Siehe Abschnitt [API-Statuscodes](/help/landing/troubleshooting.md#api-status-codes) und [Fehler in der Anfragekopfzeile](/help/landing/troubleshooting.md#request-header-errors) Weitere Informationen zur Interpretation von Fehlerantworten finden Sie im Handbuch zur Fehlerbehebung bei Platform .

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie Platform erfolgreich mit einem Ihrer bevorzugten Batch-Cloud-Speicher-Ziele verbunden und einen Datenfluss zum entsprechenden Ziel eingerichtet, um Datensätze zu exportieren. Auf den folgenden Seiten finden Sie weitere Details, z. B. wie Sie vorhandene Datenflüsse mit der Flow Service-API bearbeiten:

* [Ziele – Übersicht](../home.md)
* [Zielkatalog – Übersicht](../catalog/overview.md)
* [Aktualisieren von Zieldatenflüssen mithilfe der Flow Service-API](../api/update-destination-dataflows.md)
