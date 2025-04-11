---
solution: Experience Platform
title: Exportieren von Datensätzen mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie mit der Flow Service-API Datensätze an ausgewählte Ziele exportieren können.
type: Tutorial
exl-id: f23a4b22-da04-4b3c-9b0c-790890077eaa
source-git-commit: 29fb232ecfbd119ef84d62599fc79249513dca43
workflow-type: tm+mt
source-wordcount: '5151'
ht-degree: 11%

---

# Exportieren von Datensätzen mithilfe der [!DNL Flow Service API]

>[!AVAILABILITY]
>
>* Diese Funktion steht Kunden zur Verfügung, die das Real-Time CDP Prime- und Ultimate-Paket, Adobe Journey Optimizer oder Customer Journey Analytics erworben haben. Weitere Informationen erhalten Sie vom Adobe-Support.

>[!IMPORTANT]
>
>**Aktionselement**: In der Version [September 2024 von Experience Platform](/help/release-notes/latest/latest.md#destinations) wurde die Option zum Festlegen eines `endTime` für den Export von Datensatzdatenflüssen eingeführt. Adobe hat außerdem das standardmäßige Enddatum 1. Mai 2025 für alle Datensatzexport-Datenflüsse eingeführt, die (*der Version vom September 2024) erstellt*.
>
>Für jeden dieser Datenflüsse müssen Sie das Enddatum im Datenfluss vor dem Enddatum manuell aktualisieren, da Ihre Exporte sonst an diesem Datum anhalten. Verwenden Sie die Experience Platform-Benutzeroberfläche, um anzuzeigen, welche Datenflüsse am 1. Mai 2025 beendet werden sollen.
>
>Entsprechend gilt für alle Datenflüsse, die Sie ohne Angabe eines `endTime` erstellen, standardmäßig eine Endzeit von sechs Monaten ab dem Zeitpunkt, zu dem sie erstellt werden.

<!--

>You can retrieve a list of such dataflows by performing the following API call: `https://platform.adobe.io/data/foundation/flowservice/flows?property=scheduleParams.endTime==UNIXTIMESTAMPTHATWEWILLUSE`
>

-->

In diesem Artikel wird der Workflow erläutert, der erforderlich ist, um [!DNL Flow Service API] zum Exportieren [Datensätze](/help/catalog/datasets/overview.md) von Adobe Experience Platform an Ihren bevorzugten Cloud-Speicherort wie [!DNL Amazon S3], SFTP-Speicherorte oder [!DNL Google Cloud Storage] zu verwenden.

>[!TIP]
>
>Sie können auch die Experience Platform-Benutzeroberfläche zum Exportieren von Datensätzen verwenden. Lesen Sie das [Tutorial zur Benutzeroberfläche für Datensätze exportieren](/help/destinations/ui/export-datasets.md) um weitere Informationen zu erhalten.

## Datensätze, die exportiert werden können {#datasets-to-export}

Die Datensätze, die Sie exportieren können, hängen von der Experience Platform-Anwendung (Real-Time CDP, Adobe Journey Optimizer), der Ebene (Prime oder Ultimate) und allen Add-ons ab, die Sie erworben haben (z. B. Data Distiller).

Informationen dazu, welche Datensätze Sie exportieren können[ finden Sie in der Tabelle auf ](/help/destinations/ui/export-datasets.md#datasets-to-export) Tutorial-Seite zur Benutzeroberfläche .

## Unterstützte Ziele {#supported-destinations}

Derzeit können Sie Datensätze in die Cloud-Speicher-Ziele exportieren, die im Screenshot hervorgehoben und unten aufgeführt sind.

![Ziele, die Datensatzexporte unterstützen](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Erste Schritte {#get-started}

![Übersicht - Schritte zum Erstellen eines Ziels und zum Exportieren von Datensätzen](../assets/api/export-datasets/export-datasets-api-workflow-get-started.png)

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Platform datasets]](/help/catalog/datasets/overview.md): Alle Daten, die erfolgreich in Adobe Experience Platform aufgenommen werden, bleiben als Datensätze im [!DNL Data Lake] erhalten. Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Datensätze enthalten auch Metadaten, die verschiedene Aspekte der in ihnen gespeicherten Daten beschreiben.
   * [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um Datensätze an Cloud-Speicher-Ziele in Experience Platform zu exportieren.

### Erforderliche Berechtigungen {#permissions}

Zum Exportieren von Datensätzen benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Datensätze anzeigen]** und **[!UICONTROL Datensatzziele verwalten und aktivieren]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um sicherzustellen, dass Sie über die erforderlichen Berechtigungen zum Exportieren von Datensätzen verfügen und dass das Ziel den Export von Datensätzen unterstützt, durchsuchen Sie den Zielkatalog. Wenn ein Ziel über die Steuerung **[!UICONTROL Aktivieren]** oder **[!UICONTROL Datensätze exportieren]** verfügt, dann haben Sie die entsprechenden Berechtigungen.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln der Werte für erforderliche und optionale Kopfzeilen {#gather-values-headers}

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Tutorial zur Experience Platform-Authentifizierung abschließen](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de). Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Ressourcen in [!DNL Experience Platform] lassen sich in spezifischen virtuellen Sandboxes isolieren. Bei Anfragen an [!DNL Experience Platform]-APIs können Sie den Namen und die ID der Sandbox angeben, in der der Vorgang ausgeführt werden soll. Dies sind optionale Parameter.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

### API-Referenzdokumentation {#api-reference-documentation}

Eine zugehörige Referenzdokumentation für alle API-Vorgänge finden Sie in diesem Tutorial. Weitere Informationen finden Sie in der Dokumentation zur [[!DNL Flow Service] -Destinations-API auf der Adobe Developer-Website](https://developer.adobe.com/experience-platform-apis/references/destinations/). Wir empfehlen, dass Sie dieses Tutorial und die API-Referenzdokumentation parallel verwenden.

### Glossar {#glossary}

Beschreibungen der Begriffe, auf die Sie in diesem API-Tutorial stoßen werden, finden Sie im [Glossarabschnitt](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) der API-Referenzdokumentation.

### Zusammenstellen von Verbindungsspezifikationen und Flussspezifikationen für Ihr gewünschtes Ziel {#gather-connection-spec-flow-spec}

Bevor Sie den Workflow zum Exportieren eines Datensatzes starten, identifizieren Sie die Verbindungsspezifikations- und Flussspezifikations-IDs des Ziels, an das Sie Datensätze exportieren möchten. Verwenden Sie die nachstehende Tabelle als Referenz.


| Ziel | Verbindungsspezifikation | Flussspezifikation |
---------|----------|---------|
| [!DNL Amazon S3] | `4fce964d-3f37-408f-9778-e597338a21ee` | `269ba276-16fc-47db-92b0-c1049a3c131f` |
| [!DNL Azure Blob Storage] | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `95bd8965-fc8a-4119-b9c3-944c2c2df6d2` |
| [!DNL Azure Data Lake Gen 2(ADLS Gen2)] | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| [!DNL Data Landing Zone(DLZ)] | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| [!DNL Google Cloud Storage] | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `354d6aad-4754-46e4-a576-1b384561c440` |

{style="table-layout:auto"}

Sie benötigen diese IDs, um verschiedene [!DNL Flow Service] zu erstellen. Sie müssen auch auf Teile der [!DNL Connection Spec] selbst verweisen, um bestimmte Entitäten einzurichten, damit Sie die [!DNL Connection Spec] aus [!DNL Flow Service APIs] abrufen können. Nachfolgend finden Sie die Beispiele zum Abrufen von Verbindungsspezifikationen für alle Ziele in der Tabelle:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

+++[!DNL connection spec] für [!DNL Amazon S3] abrufen

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

+++[!DNL connection spec] für [!DNL Azure Blob Storage] abrufen

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

>[!TAB Azure Data Lake Gen2 (ADLS Gen2)]

**Anfrage**

+++[!DNL connection spec] für [!DNL Azure Data Lake Gen 2(ADLS Gen2] abrufen)

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

>[!TAB Data Landing Zone(DLZ)]

**Anfrage**

+++[!DNL connection spec] für [!DNL Data Landing Zone(DLZ)] abrufen

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

+++[!DNL connection spec] für [!DNL Google Cloud Storage] abrufen

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

+++[!DNL connection spec] für SFTP abrufen

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

Gehen Sie wie folgt vor, um einen Datensatzdatenfluss zu einem Cloud-Speicher-Ziel einzurichten. Für einige Schritte unterscheiden sich die Anfragen und Antworten zwischen den verschiedenen Cloud-Speicher-Zielen. Verwenden Sie in diesen Fällen die Registerkarten auf der Seite, um die Anfragen und Antworten abzurufen, die spezifisch für das Ziel sind, zu dem Sie eine Verbindung herstellen und Datensätze exportieren möchten. Stellen Sie sicher, dass Sie die richtigen [!DNL connection spec] und [!DNL flow spec] für das Ziel verwenden, das Sie konfigurieren.

## Abrufen einer Liste von Datensätzen {#retrieve-list-of-available-datasets}

![Diagramm mit Schritt 1 im Workflow zum Exportieren von Datensätzen](../assets/api/export-datasets/export-datasets-api-workflow-retrieve-datasets.png)

Um eine Liste von Datensätzen abzurufen, die für die Aktivierung infrage kommen, führen Sie zunächst einen API-Aufruf an den folgenden Endpunkt durch.

>[!BEGINSHADEBOX]

**Anfrage**

+++Abrufen geeigneter Datensätze - Anfrage

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/23598e46-f560-407b-88d5-ea6207e49db0/configs?outputType=activationDatasets&outputField=datasets&start=0&limit=20&properties=name,state' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

Beachten Sie, dass zum Abrufen geeigneter Datensätze die in der Anfrage-URL verwendete [!DNL connection spec]-ID die Data-Lake-Quell-Verbindungsspezifikations-ID `23598e46-f560-407b-88d5-ea6207e49db0` sein muss und die beiden Abfrageparameter `outputField=datasets` und `outputType=activationDatasets` angegeben werden müssen. Alle anderen Abfrageparameter sind die Standardparameter, die von der [Catalog Service API) unterstützt ](https://developer.adobe.com/experience-platform-apis/references/catalog/).

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

Informationen zu den verschiedenen Antwortparametern für jeden zurückgegebenen Datensatz finden Sie in der Entwicklerdokumentation [Datasets-API](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets).

## Erstellen einer Quellverbindung {#create-source-connection}

![Diagramm mit Schritt 2 im Workflow zum Exportieren von Datensätzen](../assets/api/export-datasets/export-datasets-api-workflow-create-source-connection.png)

Nachdem Sie die Liste der Datensätze abgerufen haben, die Sie exportieren möchten, können Sie mit diesen Datensatz-IDs eine Quellverbindung erstellen.

>[!BEGINSHADEBOX]

**Anfrage**

+++Quellverbindung erstellen - Anfrage

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

Bei einer erfolgreichen Antwort werden die ID (`id`) der neu erstellten Quellverbindung und ein `etag` zurückgegeben. Notieren Sie sich die Quellverbindungs-ID, da Sie sie später beim Erstellen des Datenflusses benötigen werden.

Beachten Sie bitte auch Folgendes:

* Die in diesem Schritt erstellte Quellverbindung muss mit einem Datenfluss verknüpft sein, damit ihre Datensätze für ein Ziel aktiviert werden. Informationen [ Verknüpfen einer Quellverbindung mit einem Datenfluss finden ](#create-dataflow) im Abschnitt „Erstellen eines Datenflusses“.
* Die Datensatz-IDs einer Quellverbindung können nach der Erstellung nicht mehr geändert werden. Wenn Sie Datensätze zu einer Quellverbindung hinzufügen oder daraus entfernen müssen, müssen Sie eine neue Quellverbindung erstellen und die ID der neuen Quellverbindung mit dem Datenfluss verknüpfen.

## Erstellen einer (Ziel-)Basisverbindung {#create-base-connection}

![Diagramm mit Schritt 3 im Workflow zum Exportieren von Datensätzen](../assets/api/export-datasets/export-datasets-api-workflow-create-base-connection.png)

Eine Basisverbindung speichert die Anmeldeinformationen sicher in Ihrem Ziel. Je nach Zieltyp können die Anmeldeinformationen, die zur Authentifizierung für dieses Ziel erforderlich sind, variieren. Um diese Authentifizierungsparameter zu finden, rufen Sie zunächst die [!DNL connection spec] für Ihr gewünschtes Ziel ab, wie im Abschnitt [Zusammenstellen von Verbindungsspezifikationen und Flussspezifikationen](#gather-connection-spec-flow-spec) beschrieben, und betrachten Sie dann die `authSpec` der Antwort. Auf den folgenden Registerkarten finden Sie die `authSpec` Eigenschaften aller unterstützten Ziele.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] mit [!DNL auth spec]

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die Authentifizierungsparameter in der [!DNL connection spec] zu finden sind.

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

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] mit [!DNL auth spec]

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die Authentifizierungsparameter in der [!DNL connection spec] zu finden sind.

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


>[!TAB Azure Data Lake Gen2 (ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] mit [!DNL auth spec]

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die Authentifizierungsparameter in der [!DNL connection spec] zu finden sind.

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


>[!TAB Data Landing Zone(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] mit [!DNL auth spec]

>[!NOTE]
>
>Für das Ziel der Data Landing Zone ist keine [!DNL auth spec] erforderlich.

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

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] mit [!DNL auth spec]

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die Authentifizierungsparameter in der [!DNL connection spec] zu finden sind.

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

+++SFTP - [!DNL Connection spec] mit [!DNL auth spec]

>[!NOTE]
>
>Das SFTP-Ziel enthält zwei separate Elemente in der [!DNL auth spec], da es sowohl die Passwort- als auch die SSH-Schlüsselauthentifizierung unterstützt.

Beachten Sie die hervorgehobene Zeile mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die Authentifizierungsparameter in der [!DNL connection spec] zu finden sind.

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

Mithilfe der in der Authentifizierungsspezifikation angegebenen Eigenschaften (d. h. `authSpec` aus der Antwort) können Sie eine Basisverbindung mit den erforderlichen Anmeldeinformationen erstellen, die für jeden Zieltyp spezifisch sind, wie in den Beispielen unten dargestellt:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

+++[!DNL Amazon S3] - Basisverbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsdaten finden Sie im Abschnitt [Authentifizieren bei Ziel](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) der Zieldokumentationsseite für Amazon S3.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++Antwort der [!DNL Amazon S3]-Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure-Blobspeicher]

**Anfrage**

+++[!DNL Azure Blob Storage] - Basisverbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsdaten finden Sie im Abschnitt [Authentifizieren bei Ziel](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) der Zieldokumentationsseite für Azure Blob Storage.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++[!DNL Azure Blob Storage] - Antwort der Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen2 (ADLS Gen2)]

**Anfrage**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Basisverbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsdaten finden Sie im Abschnitt [Authentifizieren bei Ziel](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) der Zieldokumentationsseite zu Azure Data Lake Gen 2(ADLS Gen2).

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Antwort der Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone(DLZ)]

**Anfrage**

+++[!DNL Data Landing Zone(DLZ)] - Basisverbindungsanfrage

>[!TIP]
>
>Für das Data Landing Zone-Ziel sind keine Authentifizierungsdaten erforderlich. Weitere Informationen finden Sie im Abschnitt [Authentifizieren beim Ziel](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) der Zieldokumentationsseite für die Data Landing Zone.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone Base Connection",
  "connectionSpec": {
    "id": "3567r537-2a7b-4583-ac39-ed38d4b848e8",
    "version": "1.0"
  }
}'
```

+++

**Antwort**

+++[!DNL Data Landing Zone] - Antwort der Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Anfrage**

+++[!DNL Google Cloud Storage] - Basisverbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsdaten finden Sie im Abschnitt [Authentifizieren bei Ziel](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) der Zieldokumentationsseite für den Google Cloud-Speicher.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++[!DNL Google Cloud Storage] - Antwort der Basisverbindung

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Anfrage**

+++SFTP mit Passwort - Basisverbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsdaten finden Sie im Abschnitt [Authentifizieren bei Ziel](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) der Dokumentationsseite zum SFTP-Ziel.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++SFTP mit SSH-Schlüssel - Basisverbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Authentifizierungsdaten finden Sie im Abschnitt [Authentifizieren bei Ziel](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) der Dokumentationsseite zum SFTP-Ziel.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

![Diagramm mit Schritt 4 im Workflow zum Exportieren von Datensätzen](../assets/api/export-datasets/export-datasets-api-workflow-create-target-connection.png)

Als Nächstes müssen Sie eine Zielverbindung erstellen, die die Exportparameter für Ihre Datensätze speichert. Zu den Exportparametern gehören Speicherort, Dateiformat, Komprimierung und andere Details. Die unterstützten Eigenschaften für jeden Zieltyp werden durch die in der -Verbindungsspezifikation des Ziels bereitgestellten `targetSpec`-Eigenschaften erklärt. Auf den folgenden Registerkarten finden Sie die `targetSpec` Eigenschaften aller unterstützten Ziele.

>[!IMPORTANT]
>
>Exporte in JSON-Dateien werden nur im komprimierten Modus unterstützt. Exporte in [!DNL Parquet] Dateien werden sowohl im komprimierten als auch im unkomprimierten Modus unterstützt.
>
>Das Format der exportierten JSON-Datei ist NDJSON, das standardmäßige Austauschformat im Big-Data-Ökosystem. Adobe empfiehlt die Verwendung eines NDJSON-kompatiblen Clients zum Lesen der exportierten Dateien.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] mit Zielverbindungsparametern

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die [!DNL target spec] in der Verbindungsspezifikation zu finden sind. Im folgenden Beispiel können Sie auch sehen, welche Zielparameter für Datensatzexportziele *nicht* anwendbar sind.

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

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] mit Zielverbindungsparametern

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die [!DNL target spec] in der Verbindungsspezifikation zu finden sind. Im folgenden Beispiel können Sie auch sehen, welche Zielparameter für Datensatzexportziele *nicht* anwendbar sind.

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


>[!TAB Azure Data Lake Gen2 (ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] mit Zielverbindungsparametern

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die [!DNL target spec] in der Verbindungsspezifikation zu finden sind. Im folgenden Beispiel können Sie auch sehen, welche Zielparameter für Datensatzexportziele *nicht* anwendbar sind.

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

>[!TAB Data Landing Zone(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] mit Zielverbindungsparametern

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die [!DNL target spec] in der Verbindungsspezifikation zu finden sind. Im folgenden Beispiel können Sie auch sehen, welche Zielparameter für Datensatzexportziele *nicht* anwendbar sind.

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

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] mit Zielverbindungsparametern

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die [!DNL target spec] in der Verbindungsspezifikation zu finden sind. Im folgenden Beispiel können Sie auch sehen, welche Zielparameter für Datensatzexportziele *nicht* anwendbar sind.

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

+++SFTP - [!DNL Connection spec] mit Zielverbindungsparametern

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im folgenden [!DNL connection spec], die zusätzliche Informationen darüber enthalten, wo die [!DNL target spec] in der Verbindungsspezifikation zu finden sind. Im folgenden Beispiel können Sie auch sehen, welche Zielparameter für Datensatzexportziele *nicht* anwendbar sind.

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


Mithilfe der obigen Spezifikation können Sie eine Zielverbindungsanfrage für Ihr gewünschtes Cloud-Speicher-Ziel erstellen, wie in den folgenden Registerkarten dargestellt.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

+++[!DNL Amazon S3] - Target-Verbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Ausfüllen der Zieldetails](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) der Dokumentationsseite für das [!DNL Amazon S3].
>Weitere unterstützte Werte von `datasetFileType` finden Sie in der API-Referenzdokumentation.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++Zielverbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure-Blobspeicher]

**Anfrage**

+++[!DNL Azure Blob Storage] - Target-Verbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Ausfüllen der Zieldetails](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) der Dokumentationsseite für das [!DNL Azure Blob Storage].
>Weitere unterstützte Werte von `datasetFileType` finden Sie in der API-Referenzdokumentation.


Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++Zielverbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen2 (ADLS Gen2)]

**Anfrage**

+++[!DNL Azure Blob Storage] - Target-Verbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Zieldetails ausfüllen](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) der Zieldokumentationsseite für Azure [!DNL Data Lake Gen 2(ADLS Gen2)].
>Weitere unterstützte Werte von `datasetFileType` finden Sie in der API-Referenzdokumentation.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++Zielverbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone(DLZ)]

**Anfrage**

+++[!DNL Data Landing Zone] - Target-Verbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Ausfüllen der Zieldetails](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) der Dokumentationsseite für das [!DNL Data Landing Zone].
>Weitere unterstützte Werte von `datasetFileType` finden Sie in der API-Referenzdokumentation.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++Zielverbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Anfrage**

+++[!DNL Google Cloud Storage] - Target-Verbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Ausfüllen der Zieldetails](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) der Dokumentationsseite für das [!DNL Google Cloud Storage].
>Weitere unterstützte Werte von `datasetFileType` finden Sie in der API-Referenzdokumentation.


Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++Zielverbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Anfrage**

+++SFTP - Target-Verbindungsanfrage

>[!TIP]
>
>Informationen zum Abrufen der erforderlichen Zielparameter finden Sie im Abschnitt [Ausfüllen der Zieldetails](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) der Dokumentationsseite für SFTP-Ziele.
>Weitere unterstützte Werte von `datasetFileType` finden Sie in der API-Referenzdokumentation.

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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

+++Zielverbindung - Antwort

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Notieren Sie sich die Zielverbindungs-ID aus der Antwort. Diese ID ist im nächsten Schritt erforderlich, wenn der Datenfluss zum Exportieren von Datensätzen erstellt wird.

## Erstellen eines Datenflusses {#create-dataflow}

![Diagramm mit Schritt 5 im Workflow zum Exportieren von Datensätzen](../assets/api/export-datasets/export-datasets-api-workflow-set-up-dataflow.png)

Der letzte Schritt in der Zielkonfiguration besteht darin, einen Datenfluss einzurichten. Ein Datenfluss verbindet zuvor erstellte Entitäten und bietet außerdem Optionen zum Konfigurieren des Zeitplans für den Datensatzexport. Verwenden Sie zum Erstellen des Datenflusses die folgenden Payloads, je nach dem gewünschten Cloud-Speicher-Ziel, und ersetzen Sie die Entitäts-IDs aus den vorherigen Schritten.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Anfrage**

+++Erstellen eines Datensatzdatenflusses zum [!DNL Amazon S3] - Anfrage

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

Die nachstehende Tabelle enthält Beschreibungen aller Parameter im Abschnitt &quot;`scheduleParams`&quot;, mit denen Sie die Exportzeiten, die Häufigkeit, den Ort und mehr für Ihre Datensatzexporte anpassen können.

| Parameter | Beschreibung |
|---------|----------|
| `exportMode` | Wählen Sie `"DAILY_FULL_EXPORT"` oder `"FIRST_FULL_THEN_INCREMENTAL"` aus. Weitere Informationen zu den beiden Optionen finden Sie unter [Exportieren von vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Exportieren von inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) im Tutorial zur Aktivierung von Batch-Zielen. Die drei verfügbaren Exportoptionen sind: <br> **Vollständige Datei - Einmal**: `"DAILY_FULL_EXPORT"` kann nur in Kombination mit `timeUnit`:`day` und `interval`:`0` für einen einmaligen vollständigen Export des Datensatzes verwendet werden. Tägliche vollständige Exporte von Datensätzen werden nicht unterstützt. Wenn Sie tägliche Exporte benötigen, verwenden Sie die Option Inkrementeller Export . <br> **Inkrementelle tägliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` und `interval`:`1` für tägliche inkrementelle Exporte. <br> **Inkrementelle stündliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` und `interval` :`3`,`6`,`9` oder `12` für stündliche inkrementelle Exporte. |
| `timeUnit` | Wählen Sie `day` oder `hour` aus, je nach der Häufigkeit, mit der Sie Datensatzdateien exportieren möchten. |
| `interval` | Wählen Sie `1`, wenn der `timeUnit` Tag ist, und `3`,`6`,`9`,`12`, wenn die Zeiteinheit `hour` ist. |
| `startTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte beginnen sollen. |
| `endTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte enden sollen. |
| `foldernameTemplate` | Geben Sie die erwartete Ordnernamenstruktur an Ihrem Speicherort an, an dem die exportierten Dateien abgelegt werden. <ul><li><code>DATASET_ID</code> = <span>Eine eindeutige Kennung für den Datensatz.</span></li><li><code>ZIEL</code> = <span>Der Name des Ziels.</span></li><li><code>DATETIME</code> = <span>Datum und Uhrzeit formatiert als JJJJMMtt_HHMMSS.</span></li><li><code>EXPORTZEIT</code> = <span>Die geplante Zeit für den Datenexport, formatiert als `exportTime=YYYYMMDDHHMM`.</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>Der Name der spezifischen Instanz des Ziels.</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>Eindeutige Kennung für die Zielinstanz.</span></li><li><code>SANDBOX_NAME</code> = <span>Der Name der Sandbox-Umgebung.</span></li><li><code>ORGANISATION_NAME</code> = <span>Der Name der Organisation.</span></li></ul> |

{style="table-layout:auto"}
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

+++Erstellen eines Datensatzdatenflusses zum [!DNL Azure Blob Storage] - Anfrage

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

Die nachstehende Tabelle enthält Beschreibungen aller Parameter im Abschnitt &quot;`scheduleParams`&quot;, mit denen Sie die Exportzeiten, die Häufigkeit, den Ort und mehr für Ihre Datensatzexporte anpassen können.

| Parameter | Beschreibung |
|---------|----------|
| `exportMode` | Wählen Sie `"DAILY_FULL_EXPORT"` oder `"FIRST_FULL_THEN_INCREMENTAL"` aus. Weitere Informationen zu den beiden Optionen finden Sie unter [Exportieren von vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Exportieren von inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) im Tutorial zur Aktivierung von Batch-Zielen. Die drei verfügbaren Exportoptionen sind: <br> **Vollständige Datei - Einmal**: `"DAILY_FULL_EXPORT"` kann nur in Kombination mit `timeUnit`:`day` und `interval`:`0` für einen einmaligen vollständigen Export des Datensatzes verwendet werden. Tägliche vollständige Exporte von Datensätzen werden nicht unterstützt. Wenn Sie tägliche Exporte benötigen, verwenden Sie die Option Inkrementeller Export . <br> **Inkrementelle tägliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` und `interval`:`1` für tägliche inkrementelle Exporte. <br> **Inkrementelle stündliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` und `interval` :`3`,`6`,`9` oder `12` für stündliche inkrementelle Exporte. |
| `timeUnit` | Wählen Sie `day` oder `hour` aus, je nach der Häufigkeit, mit der Sie Datensatzdateien exportieren möchten. |
| `interval` | Wählen Sie `1`, wenn der `timeUnit` Tag ist, und `3`,`6`,`9`,`12`, wenn die Zeiteinheit `hour` ist. |
| `startTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte beginnen sollen. |
| `endTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte enden sollen. |
| `foldernameTemplate` | Geben Sie die erwartete Ordnernamenstruktur an Ihrem Speicherort an, an dem die exportierten Dateien abgelegt werden. <ul><li><code>DATASET_ID</code> = <span>Eine eindeutige Kennung für den Datensatz.</span></li><li><code>ZIEL</code> = <span>Der Name des Ziels.</span></li><li><code>DATETIME</code> = <span>Datum und Uhrzeit formatiert als JJJJMMtt_HHMMSS.</span></li><li><code>EXPORTZEIT</code> = <span>Die geplante Zeit für den Datenexport, formatiert als `exportTime=YYYYMMDDHHMM`.</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>Der Name der spezifischen Instanz des Ziels.</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>Eindeutige Kennung für die Zielinstanz.</span></li><li><code>SANDBOX_NAME</code> = <span>Der Name der Sandbox-Umgebung.</span></li><li><code>ORGANISATION_NAME</code> = <span>Der Name der Organisation.</span></li></ul> |

{style="table-layout:auto"}

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

>[!TAB Azure Data Lake Gen2 (ADLS Gen2)]

**Anfrage**

+++Erstellen eines Datensatzdatenflusses zum [!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Anfrage

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

Die nachstehende Tabelle enthält Beschreibungen aller Parameter im Abschnitt &quot;`scheduleParams`&quot;, mit denen Sie die Exportzeiten, die Häufigkeit, den Ort und mehr für Ihre Datensatzexporte anpassen können.

| Parameter | Beschreibung |
|---------|----------|
| `exportMode` | Wählen Sie `"DAILY_FULL_EXPORT"` oder `"FIRST_FULL_THEN_INCREMENTAL"` aus. Weitere Informationen zu den beiden Optionen finden Sie unter [Exportieren von vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Exportieren von inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) im Tutorial zur Aktivierung von Batch-Zielen. Die drei verfügbaren Exportoptionen sind: <br> **Vollständige Datei - Einmal**: `"DAILY_FULL_EXPORT"` kann nur in Kombination mit `timeUnit`:`day` und `interval`:`0` für einen einmaligen vollständigen Export des Datensatzes verwendet werden. Tägliche vollständige Exporte von Datensätzen werden nicht unterstützt. Wenn Sie tägliche Exporte benötigen, verwenden Sie die Option Inkrementeller Export . <br> **Inkrementelle tägliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` und `interval`:`1` für tägliche inkrementelle Exporte. <br> **Inkrementelle stündliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` und `interval` :`3`,`6`,`9` oder `12` für stündliche inkrementelle Exporte. |
| `timeUnit` | Wählen Sie `day` oder `hour` aus, je nach der Häufigkeit, mit der Sie Datensatzdateien exportieren möchten. |
| `interval` | Wählen Sie `1`, wenn der `timeUnit` Tag ist, und `3`,`6`,`9`,`12`, wenn die Zeiteinheit `hour` ist. |
| `startTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte beginnen sollen. |
| `endTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte enden sollen. |
| `foldernameTemplate` | Geben Sie die erwartete Ordnernamenstruktur an Ihrem Speicherort an, an dem die exportierten Dateien abgelegt werden. <ul><li><code>DATASET_ID</code> = <span>Eine eindeutige Kennung für den Datensatz.</span></li><li><code>ZIEL</code> = <span>Der Name des Ziels.</span></li><li><code>DATETIME</code> = <span>Datum und Uhrzeit formatiert als JJJJMMtt_HHMMSS.</span></li><li><code>EXPORTZEIT</code> = <span>Die geplante Zeit für den Datenexport, formatiert als `exportTime=YYYYMMDDHHMM`.</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>Der Name der spezifischen Instanz des Ziels.</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>Eindeutige Kennung für die Zielinstanz.</span></li><li><code>SANDBOX_NAME</code> = <span>Der Name der Sandbox-Umgebung.</span></li><li><code>ORGANISATION_NAME</code> = <span>Der Name der Organisation.</span></li></ul> |

{style="table-layout:auto"}

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

>[!TAB Data Landing Zone(DLZ)]

**Anfrage**

+++Erstellen eines Datensatzdatenflusses zum [!DNL Data Landing Zone] - Anfrage

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

Die nachstehende Tabelle enthält Beschreibungen aller Parameter im Abschnitt &quot;`scheduleParams`&quot;, mit denen Sie die Exportzeiten, die Häufigkeit, den Ort und mehr für Ihre Datensatzexporte anpassen können.

| Parameter | Beschreibung |
|---------|----------|
| `exportMode` | Wählen Sie `"DAILY_FULL_EXPORT"` oder `"FIRST_FULL_THEN_INCREMENTAL"` aus. Weitere Informationen zu den beiden Optionen finden Sie unter [Exportieren von vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Exportieren von inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) im Tutorial zur Aktivierung von Batch-Zielen. Die drei verfügbaren Exportoptionen sind: <br> **Vollständige Datei - Einmal**: `"DAILY_FULL_EXPORT"` kann nur in Kombination mit `timeUnit`:`day` und `interval`:`0` für einen einmaligen vollständigen Export des Datensatzes verwendet werden. Tägliche vollständige Exporte von Datensätzen werden nicht unterstützt. Wenn Sie tägliche Exporte benötigen, verwenden Sie die Option Inkrementeller Export . <br> **Inkrementelle tägliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` und `interval`:`1` für tägliche inkrementelle Exporte. <br> **Inkrementelle stündliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` und `interval` :`3`,`6`,`9` oder `12` für stündliche inkrementelle Exporte. |
| `timeUnit` | Wählen Sie `day` oder `hour` aus, je nach der Häufigkeit, mit der Sie Datensatzdateien exportieren möchten. |
| `interval` | Wählen Sie `1`, wenn der `timeUnit` Tag ist, und `3`,`6`,`9`,`12`, wenn die Zeiteinheit `hour` ist. |
| `startTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte beginnen sollen. |
| `endTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte enden sollen. |
| `foldernameTemplate` | Geben Sie die erwartete Ordnernamenstruktur an Ihrem Speicherort an, an dem die exportierten Dateien abgelegt werden. <ul><li><code>DATASET_ID</code> = <span>Eine eindeutige Kennung für den Datensatz.</span></li><li><code>ZIEL</code> = <span>Der Name des Ziels.</span></li><li><code>DATETIME</code> = <span>Datum und Uhrzeit formatiert als JJJJMMtt_HHMMSS.</span></li><li><code>EXPORTZEIT</code> = <span>Die geplante Zeit für den Datenexport, formatiert als `exportTime=YYYYMMDDHHMM`.</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>Der Name der spezifischen Instanz des Ziels.</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>Eindeutige Kennung für die Zielinstanz.</span></li><li><code>SANDBOX_NAME</code> = <span>Der Name der Sandbox-Umgebung.</span></li><li><code>ORGANISATION_NAME</code> = <span>Der Name der Organisation.</span></li></ul> |

{style="table-layout:auto"}
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

+++Erstellen eines Datensatzdatenflusses zum [!DNL Google Cloud Storage] - Anfrage

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

Die nachstehende Tabelle enthält Beschreibungen aller Parameter im Abschnitt &quot;`scheduleParams`&quot;, mit denen Sie die Exportzeiten, die Häufigkeit, den Ort und mehr für Ihre Datensatzexporte anpassen können.

| Parameter | Beschreibung |
|---------|----------|
| `exportMode` | Wählen Sie `"DAILY_FULL_EXPORT"` oder `"FIRST_FULL_THEN_INCREMENTAL"` aus. Weitere Informationen zu den beiden Optionen finden Sie unter [Exportieren von vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Exportieren von inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) im Tutorial zur Aktivierung von Batch-Zielen. Die drei verfügbaren Exportoptionen sind: <br> **Vollständige Datei - Einmal**: `"DAILY_FULL_EXPORT"` kann nur in Kombination mit `timeUnit`:`day` und `interval`:`0` für einen einmaligen vollständigen Export des Datensatzes verwendet werden. Tägliche vollständige Exporte von Datensätzen werden nicht unterstützt. Wenn Sie tägliche Exporte benötigen, verwenden Sie die Option Inkrementeller Export . <br> **Inkrementelle tägliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` und `interval`:`1` für tägliche inkrementelle Exporte. <br> **Inkrementelle stündliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` und `interval` :`3`,`6`,`9` oder `12` für stündliche inkrementelle Exporte. |
| `timeUnit` | Wählen Sie `day` oder `hour` aus, je nach der Häufigkeit, mit der Sie Datensatzdateien exportieren möchten. |
| `interval` | Wählen Sie `1`, wenn der `timeUnit` Tag ist, und `3`,`6`,`9`,`12`, wenn die Zeiteinheit `hour` ist. |
| `startTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte beginnen sollen. |
| `endTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte enden sollen. |
| `foldernameTemplate` | Geben Sie die erwartete Ordnernamenstruktur an Ihrem Speicherort an, an dem die exportierten Dateien abgelegt werden. <ul><li><code>DATASET_ID</code> = <span>Eine eindeutige Kennung für den Datensatz.</span></li><li><code>ZIEL</code> = <span>Der Name des Ziels.</span></li><li><code>DATETIME</code> = <span>Datum und Uhrzeit formatiert als JJJJMMtt_HHMMSS.</span></li><li><code>EXPORTZEIT</code> = <span>Die geplante Zeit für den Datenexport, formatiert als `exportTime=YYYYMMDDHHMM`.</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>Der Name der spezifischen Instanz des Ziels.</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>Eindeutige Kennung für die Zielinstanz.</span></li><li><code>SANDBOX_NAME</code> = <span>Der Name der Sandbox-Umgebung.</span></li><li><code>ORGANISATION_NAME</code> = <span>Der Name der Organisation.</span></li></ul> |

{style="table-layout:auto"}

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

+++Erstellen eines Datensatz-Datenflusses zum SFTP-Ziel - Anfrage

Beachten Sie die hervorgehobenen Zeilen mit Inline-Kommentaren im Anfragebeispiel, die zusätzliche Informationen bereitstellen. Entfernen Sie die Inline-Kommentare in der Anfrage, wenn Sie die Anfrage in das Terminal Ihrer Wahl kopieren.

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
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

Die nachstehende Tabelle enthält Beschreibungen aller Parameter im Abschnitt &quot;`scheduleParams`&quot;, mit denen Sie die Exportzeiten, die Häufigkeit, den Ort und mehr für Ihre Datensatzexporte anpassen können.

| Parameter | Beschreibung |
|---------|----------|
| `exportMode` | Wählen Sie `"DAILY_FULL_EXPORT"` oder `"FIRST_FULL_THEN_INCREMENTAL"` aus. Weitere Informationen zu den beiden Optionen finden Sie unter [Exportieren von vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Exportieren von inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) im Tutorial zur Aktivierung von Batch-Zielen. Die drei verfügbaren Exportoptionen sind: <br> **Vollständige Datei - Einmal**: `"DAILY_FULL_EXPORT"` kann nur in Kombination mit `timeUnit`:`day` und `interval`:`0` für einen einmaligen vollständigen Export des Datensatzes verwendet werden. Tägliche vollständige Exporte von Datensätzen werden nicht unterstützt. Wenn Sie tägliche Exporte benötigen, verwenden Sie die Option Inkrementeller Export . <br> **Inkrementelle tägliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` und `interval`:`1` für tägliche inkrementelle Exporte. <br> **Inkrementelle stündliche Exporte**: Wählen Sie `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` und `interval` :`3`,`6`,`9` oder `12` für stündliche inkrementelle Exporte. |
| `timeUnit` | Wählen Sie `day` oder `hour` aus, je nach der Häufigkeit, mit der Sie Datensatzdateien exportieren möchten. |
| `interval` | Wählen Sie `1`, wenn der `timeUnit` Tag ist, und `3`,`6`,`9`,`12`, wenn die Zeiteinheit `hour` ist. |
| `startTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte beginnen sollen. |
| `endTime` | Datum und Uhrzeit in UNIX-Sekunden, zu der Datensatzexporte enden sollen. |
| `foldernameTemplate` | Geben Sie die erwartete Ordnernamenstruktur an Ihrem Speicherort an, an dem die exportierten Dateien abgelegt werden. <ul><li><code>DATASET_ID</code> = <span>Eine eindeutige Kennung für den Datensatz.</span></li><li><code>ZIEL</code> = <span>Der Name des Ziels.</span></li><li><code>DATETIME</code> = <span>Datum und Uhrzeit formatiert als JJJJMMtt_HHMMSS.</span></li><li><code>EXPORTZEIT</code> = <span>Die geplante Zeit für den Datenexport, formatiert als `exportTime=YYYYMMDDHHMM`.</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>Der Name der spezifischen Instanz des Ziels.</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>Eindeutige Kennung für die Zielinstanz.</span></li><li><code>SANDBOX_NAME</code> = <span>Der Name der Sandbox-Umgebung.</span></li><li><code>ORGANISATION_NAME</code> = <span>Der Name der Organisation.</span></li></ul> |

{style="table-layout:auto"}

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

Notieren Sie die Datenfluss-ID aus der Antwort. Diese ID ist im nächsten Schritt erforderlich, wenn der Datenfluss abgerufen wird, um die erfolgreichen Datensatzexporte zu validieren.

## Abrufen der Datenflussausführungen {#get-dataflow-runs}

![Diagramm mit Schritt 6 im Workflow zum Exportieren von Datensätzen](../assets/api/export-datasets/export-datasets-api-workflow-validate-dataflow.png)

Um die Ausführungen eines Datenflusses zu überprüfen, verwenden Sie die Datenflussausführungs-API:

>[!BEGINSHADEBOX]

**Anfrage**

+++Datenflussausführungen abrufen - Anfrage

Fügen Sie in der Anfrage zum Abrufen des Datenflusses als Abfrageparameter die Datenfluss-ID hinzu, die Sie im vorherigen Schritt beim Erstellen des Datenflusses erhalten haben.

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

+++Abrufen von Datenflussausführungen - Antwort

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

Informationen zu den [verschiedenen von der Datenflussausführungs-API zurückgegebenen Parametern“ finden Sie ](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) der API-Referenzdokumentation.

## Überprüfen eines erfolgreichen Datensatzexports {#verify}

Beim Exportieren von Datensätzen erstellt Experience Platform eine `.json`- oder `.parquet`-Datei an dem von Ihnen angegebenen Speicherort. Erwarten Sie, dass eine neue Datei entsprechend dem Exportplan, den Sie beim Erstellen eines Datenflusses angegeben haben, an [ Speicherort abgelegt ](#create-dataflow).

Experience Platform erstellt eine Ordnerstruktur am angegebenen Speicherort, in der die exportierten Datensatzdateien abgelegt werden. Für jeden Exportzeitpunkt wird ein neuer Ordner erstellt, wobei das folgende Muster befolgt wird:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Der standardmäßige Dateiname wird nach dem Zufallsprinzip generiert, was sicherstellt, dass die Namen von exportierten Dateien eindeutig sind.

### Beispiele für Datensatzdateien {#sample-files}

Das Vorhandensein dieser Dateien an Ihrem Speicherort bestätigt einen erfolgreichen Export. Um zu verstehen, wie die exportierten Dateien strukturiert sind, können Sie eine [Parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet)- oder [JSON](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)-Beispieldatei herunterladen.

#### Komprimierte Datensatzdateien {#compressed-dataset-files}

Im Schritt zum [Erstellen einer Zielverbindung](#create-target-connection) können Sie die exportierten Datensatzdateien auswählen, die komprimiert werden sollen.

Beachten Sie den Unterschied im Dateiformat zwischen den beiden Dateitypen, wenn sie komprimiert werden:

* Beim Exportieren komprimierter JSON-Dateien wird das exportierte Dateiformat `json.gz`
* Beim Exportieren von komprimierten Parquet-Dateien wird das exportierte Dateiformat `gz.parquet`
* JSON-Dateien können nur im komprimierten Modus exportiert werden.

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Weitere Informationen [ Interpretieren von Fehlerantworten finden Sie unter ](/help/landing/troubleshooting.md#api-status-codes)API-Status-Codes[ und ](/help/landing/troubleshooting.md#request-header-errors)Fehler in der Anfragekopfzeile im Handbuch zur Fehlerbehebung bei Experience Platform .

## Bekannte Einschränkungen {#known-limitations}

Ansicht [Bekannte Einschränkungen](/help/destinations/ui/export-datasets.md#known-limitations) zu Datensatzexporten.

## Häufig gestellte Fragen {#faq}

Anzeigen einer [Liste häufig gestellter Fragen](/help/destinations/ui/export-datasets.md#faq) zu Datensatzexporten.

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie Experience Platform erfolgreich mit einem Ihrer bevorzugten Batch-Cloud-Speicher-Ziele verbunden und einen Datenfluss zum entsprechenden Ziel eingerichtet, um Datensätze zu exportieren. Auf den folgenden Seiten finden Sie weitere Details, z. B. wie Sie vorhandene Datenflüsse mit der Flow Service-API bearbeiten:

* [Ziele – Übersicht](../home.md)
* [Zielkatalog – Übersicht](../catalog/overview.md)
* [Aktualisieren von Zieldatenflüssen mithilfe der Flow Service-API](../api/update-destination-dataflows.md)